<script setup lang="ts">
import { nextTick, onMounted, ref, watch } from "vue";

interface Props {
  listItems?: string[];
  variant?:
    | "primary"
    | "secondary"
    | "tech"
    | "neutral"
    | "gradient-primary"
    | "gradient-secondary"
    | "gradient-tech"
    | "success"
    | "warning"
    | "error";
  enableLatex?: boolean;
  listStyle?: "dot" | "square";
}

const props = withDefaults(defineProps<Props>(), {
  variant: "neutral",
  enableLatex: false,
  listStyle: "square",
});

// Refs for DOM elements
const listRef = ref<HTMLElement>();

// KaTeX instance cache
let katex: any = null;

/**
 * Load KaTeX library dynamically
 * First tries window.katex (if loaded by Slidev), then dynamic import
 */
async function loadKaTeX() {
  if (katex) return katex;

  try {
    // Try window.katex first (if already loaded by Slidev)
    if ((window as any).katex) {
      katex = (window as any).katex;
      return katex;
    }

    // Try dynamic import
    const katexModule = await import("katex");
    katex = katexModule.default || katexModule;
    return katex;
  } catch (error) {
    console.warn("Failed to load KaTeX:", error);
    return null;
  }
}

/**
 * Process LaTeX math expressions in the component
 * Finds text nodes with $...$ patterns and renders them using KaTeX
 */
async function processMath() {
  if (!props.enableLatex || !listRef.value) return;

  await nextTick();

  try {
    const katexInstance = await loadKaTeX();
    if (!katexInstance || !katexInstance.render) {
      console.warn("KaTeX render method not available");
      return;
    }

    // Find all text nodes that contain LaTeX
    const walker = document.createTreeWalker(
      listRef.value,
      NodeFilter.SHOW_TEXT,
      null,
    );

    const textNodes: Text[] = [];
    let node = walker.nextNode();
    while (node) {
      if (node.textContent && /\$[^$]+\$/.test(node.textContent)) {
        textNodes.push(node as Text);
      }
      node = walker.nextNode();
    }

    // Process each text node
    textNodes.forEach((textNode) => {
      const text = textNode.textContent!;
      const parts = text.split(/(\$[^$]+\$)/g);

      if (parts.length > 1) {
        const fragment = document.createDocumentFragment();

        // Get computed styles from parent element to preserve styling
        const parentElement = textNode.parentElement;
        let inheritedStyles = "";

        if (parentElement) {
          const computedStyle = window.getComputedStyle(parentElement);
          const stylesToCopy = [
            "color",
            "font-family",
            "font-size",
            "font-weight",
            "font-style",
            "text-decoration",
            "background",
            "background-image",
            "background-clip",
            "-webkit-background-clip",
            "-webkit-text-fill-color",
          ];

          const styleRules = stylesToCopy
            .map((prop) => `${prop}: ${computedStyle.getPropertyValue(prop)}`)
            .filter(
              (rule) => !rule.includes("none") && !rule.includes("normal"),
            )
            .join("; ");

          if (styleRules) {
            inheritedStyles = styleRules;
          }
        }

        parts.forEach((part) => {
          if (part.startsWith("$") && part.endsWith("$") && part.length > 2) {
            // Render math expression
            const math = part.slice(1, -1); // Remove $ delimiters
            const span = document.createElement("span");

            try {
              katexInstance.render(math, span, {
                throwOnError: false,
                displayMode: false,
              });

              // Apply inherited styles to the KaTeX span
              if (inheritedStyles) {
                span.style.cssText = inheritedStyles;
              }

              // Apply styles to nested KaTeX elements
              const katexElements = span.querySelectorAll(".katex, .katex *");
              katexElements.forEach((elem: Element) => {
                if (elem instanceof HTMLElement && inheritedStyles) {
                  const colorMatch = inheritedStyles.match(/color:\s*([^;]+)/);
                  const backgroundMatch = inheritedStyles.match(
                    /background[^:]*:\s*([^;]+)/g,
                  );
                  const textFillMatch = inheritedStyles.match(
                    /-webkit-text-fill-color:\s*([^;]+)/,
                  );

                  if (colorMatch) {
                    elem.style.color = colorMatch[1];
                  }
                  if (textFillMatch) {
                    elem.style.webkitTextFillColor = textFillMatch[1];
                  }
                  if (backgroundMatch) {
                    backgroundMatch.forEach((bg) => {
                      const [prop, value] = bg.split(":");
                      elem.style.setProperty(prop.trim(), value.trim());
                    });
                    elem.style.webkitBackgroundClip = "text";
                    elem.style.backgroundClip = "text";
                  }
                }
              });

              fragment.appendChild(span);
            } catch (error) {
              console.warn("KaTeX render error:", error);
              fragment.appendChild(document.createTextNode(part));
            }
          } else if (part) {
            // Regular text
            fragment.appendChild(document.createTextNode(part));
          }
        });

        textNode.parentNode?.replaceChild(fragment, textNode);
      }
    });
  } catch (error) {
    console.warn("Error processing math:", error);
  }
}

// Lifecycle hooks
onMounted(() => {
  processMath();
});

// Re-process math when props change
watch([() => props.listItems], () => {
  processMath();
});

const dotClasses = {
  primary: "bg-sjtu-400",
  secondary: "bg-academic-400",
  tech: "bg-tech-electric-400",
  neutral: "bg-neutral-400",
  "gradient-primary": "bg-sjtu-400",
  "gradient-secondary": "bg-academic-400",
  "gradient-tech": "bg-tech-electric-400",
  success: "bg-success-400",
  warning: "bg-warning-400",
  error: "bg-error-400",
};
</script>

<template>
  <ul v-if="listItems && listItems.length" ref="listRef" class="space-y-2 ml--4">
    <li
      v-for="(item, index) in listItems"
      :key="index"
      class="flex flex-gap-4 items-center"
    >
      <!-- Square bullet (Slidev style) -->
      <div
        v-if="listStyle === 'square'"
        i-ph:square-duotone
        :class="dotClasses[variant]"
      />
      <!-- Round dot bullet -->
      <div v-else i-ph:circle-duotone :class="dotClasses[variant]" />
      <div class="text-on-surface flex-1">
        {{ item }}
      </div>
    </li>
  </ul>

  <!-- Default slot for custom content -->
  <div v-if="!listItems || !listItems.length">
    <slot />
  </div>
</template>
