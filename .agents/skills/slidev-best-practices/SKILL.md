---
name: slidev-best-practices
description: Plan, build, and refine Slidev presentations with clear narrative, readable technical content, deliberate visual design, and verified browser/PDF output. Use for new decks, substantial slide revisions, presentation redesigns, or quality reviews in this repository. Pair with slidev for syntax; skip for isolated CLI or syntax fixes.
---

# Slidev Presentation Best Practices

Use this skill with [slidev](../slidev/SKILL.md) and the repository's
[AGENTS.md](../../../AGENTS.md). Scale the workflow to the task: a single-slide
edit needs a local check; a new deck needs a coherent story and full review.

## Establish the Talk

Read the target deck, `metadata.json`, package scripts, and relevant theme
components before choosing a direction. Identify the audience, time budget,
language, main takeaway, and delivery format from the request and repository.
Ask only for missing information that would change the work; otherwise state
useful assumptions and proceed.

For a new talk, use a date-prefixed folder such as `talks/YYYY-MM-DD-topic/`
so the repository's dev picker can discover it. Copy `template/` and update the
package name, README title, metadata, speaker, date, assets, and scripts. In the copied
package, replace the template's dated build argument with
`bun ../../scripts/build.ts` and set export output to
`./assets/<talk-name>.pdf`. Retain `catalog:` dependencies. Start the new deck
with actual talk content rather than the template's component showcase.

Run `bun install` from the repository root after adding a workspace so its
`catalog:` dependencies resolve. Keep metadata consumed by the collector on
single-line headmatter values; put richer descriptions in `metadata.json`.
Before handing off a new talk, run `bun run metadata` and `bun run update` from
the root to refresh the talk index and Netlify routes, then inspect the generated
diffs. See [verification.md](references/verification.md) for build/export checks.

## Build the Argument Before Styling

Sketch the narrative in the working conversation, notes, or an existing outline:
what problem matters, what the audience needs to understand, what the evidence
shows, and what they should remember or do. A research talk may need assumptions,
method, baseline, limitations, and results; a tutorial may need worked examples
and practice. Adapt to the material instead of imposing a fixed slide count.

- Give each slide one primary claim, question, or teaching objective. A title
  such as “Boundary errors dominate near the wall” is useful only when the
  supplied evidence supports it; otherwise use an honest descriptive title.
- Pair a claim with the most direct evidence: a figure, equation, code excerpt,
  example, or comparison. Keep caveats needed to interpret it on the slide.
- Move supporting derivations, references, and secondary examples into speaker
  notes or backup slides. Split dense content before shrinking the type.
- Use speaker notes for the spoken explanation, transitions, and click cues.
  The visible slide should support the speaker without becoming a transcript.
- Keep measured data, citations, units, and uncertainty accurate. Do not
  invent benchmark values, references, collaborators, or scientific conclusions.

## Choose the Visual Language

For a new visual direction, read
[frontend-design](../frontend-design/SKILL.md), then use
[visual-design.md](references/visual-design.md) to translate it to slides.
For an existing deck, start from its typography, palette, layouts, and component
conventions. Use meaningful variation: a result figure can occupy most of a
slide while a comparison benefits from aligned columns.

Prototype the slides that expose the real constraints early: typically the
cover, a dense technical slide, and a result/comparison slide. Check their
rendered appearance before propagating a visual system through the deck.

## Implement with Slidev

- Choose semantic layouts (`cover`, `section`, `two-cols`, `image-right`, etc.)
  before writing custom positioning. Put repeated compositions into the talk's
  `layouts/` or `components/`; keep one-off adjustments local to the slide.
- Use grid and flex for content flow. Reserve absolute positioning for anchored
  labels or overlays with a clear relationship to the figure. Leave room for
  `global-bottom.vue`, captions, and navigation.
- Prefer readable Markdown, built-in Vue components, and existing UnoCSS
  shortcuts. Avoid large nested HTML blocks for ordinary text. Preserve blank
  lines around Markdown within Vue blocks and keep headmatter separate from
  per-slide frontmatter.
- For long decks, split logical sections into `pages/` with `src:` imports when
  that helps maintenance. Check final slide numbering and imported frontmatter.
- Keep important assets in the talk's `public/` directory and use paths that
  work under the deployed `/<talk-name>/` base. Check fonts and CJK glyphs in
  the actual browser/export environment.
- Use short, focused code excerpts with syntax highlighting. Reveal or
  highlight the lines being explained; use magic move when the change itself
  is the point. Avoid essential code hidden behind a scroll area.
- Define equation symbols near first use. Break derivations into explainable
  steps and make plots readable without relying only on their legend or color.
- Use `v-click` for meaningful teaching steps. Rehearse forward and backward
  navigation and make each visible state understandable. Limit automatic motion
  and keep content available with reduced motion and in the static export.
- Give demos a static explanation or captured result for PDF/offline use.
  Distinguish working interactions from illustrations of an interaction.

See the [Slidev reference index](../slidev/SKILL.md) for feature-specific syntax.
Confirm newer features against the installed version before adopting them.

## Verify the Deliverable

Follow [verification.md](references/verification.md) for browser inspection,
overflow checks, click states, and export commands. A successful build establishes
that the deck compiles; inspect rendered slides to establish that it reads well.
Use [web-design-guidelines](../web-design-guidelines/SKILL.md) for a requested
design/accessibility review of custom components and surrounding web UI.

When handing off, identify the deck and meaningful changes, report the checks
actually completed, and state any remaining rendering or export limitation.
Publishing is a separate action governed by the user's request.

## Technical Sources

- [Slidev syntax](https://sli.dev/guide/syntax) for Markdown, notes, and frontmatter.
- [Layouts](https://sli.dev/guide/layout) and [writing layouts](https://sli.dev/guide/write-layout)
  for reusable compositions.
- [Animations](https://sli.dev/guide/animations) for click sequencing.
- [Exporting](https://sli.dev/guide/exporting) for format capabilities and limitations.

The presentation and design guidance here is repository-maintained editorial
practice; it is not an upstream Slidev requirement.
