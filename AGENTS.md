# AGENTS.md

This file provides guidance to coding agents working in this repository.

## Project overview

A [Slidev](https://sli.dev) monorepo for presentations. Each talk under `talks/` is its own Bun workspace. The repo builds to static HTML, deployed on Netlify.

## Commands

```bash
bun --bun run dev              # Interactive picker → launch slidev dev server for a talk
bun --bun run build            # Build all talks + generate metadata
bun --bun run typecheck        # Type-check with vue-tsc
bun --bun run lint             # oxlint (TypeScript + Vue + import plugins)
bun --bun run format           # oxfmt — format all files (skips Slidev markdown)
bun --bun run format:check     # oxfmt — check formatting only
bun --bun run metadata         # Generate talks-metadata.json only
bun --bun run update           # Regenerate netlify.toml redirects from talk dirs
```

Per-talk (inside `talks/<talk-name>/`):

```bash
bun --bun run dev              # Start slidev dev server for this talk
bun --bun run build            # Build + export PDF for this talk (calls scripts/build.ts)
bun --bun run export           # Export slides as PDF only
```

There are no tests in this repo.

### MCP server

Slidev exposes an MCP (Model Context Protocol) server at the dev server's `/__mcp` endpoint. An MCP-capable agent can connect to `http://localhost:3030/__mcp` to navigate slides and read or edit slide content.

The Slidev dev server must be running (via `bun run dev`) for the MCP server to be reachable. If the dev server is on a different port, adjust the URL accordingly. See the [MCP reference](.agents/skills/slidev/references/tool-mcp.md) for the standalone stdio option.

## Architecture

### Workspace structure

Each directory under `talks/` is a Bun workspace (`"workspaces": ["talks/*"]` in root `package.json`). Dependencies use Bun's **catalog protocol** — the root `package.json` defines version pins under `workspaces.catalog`, and individual talk `package.json` files reference `"catalog:"` strings. This ensures all talks share the same Slidev, UnoCSS, and Vite versions.

### Talk structure

Every talk has:

- `slides.md` — Slidev markdown with YAML frontmatter (title, lang, etc.). **Note:** oxfmt skips `slides.md` and `pages/*.md` — it cannot parse Slidev's YAML frontmatter syntax. Markdown formatting for these files requires `prettier-plugin-slidev` if needed.
- `metadata.json` — conference/location/tags/description (optional, merged into the global metadata)
- `package.json` — `dev`/`build`/`export` scripts calling slidev CLI or `scripts/build.ts`
- `components/`, `styles/`, `public/`, `pages/` — standard Slidev extension directories
- `vite.config.ts` — optional Vite config override (some talks include this)
- `global-bottom.vue` — per-talk global bottom component (speaker info, conference badge)
- `README.md` — first `# Title` line is used by the dev picker for display

### Template

`template/` is a canonical talk with SJTU branding. When creating a new talk, copy `template/` and adapt `slides.md` + `metadata.json`.

Key template components:

- **`GlassCard.vue`** — glassmorphism card with 10 color variants, 3 sizes, optional Iconify icon, and runtime KaTeX rendering for `$...$` math in titles/subtitles/list items
- **`List.vue`** — standalone list with the same KaTeX rendering as GlassCard, without card wrapping
- **`ProsCons.vue`** — two-column animated comparison (pros/cons) triggered on `v-click`
- **`Repo.vue`** — GitHub repository link with `carbon-logo-github` icon
- **`Emphasis.vue`** — inline code-style pill
- **`IconTest.vue`** — utility component for testing Iconify icon rendering and dynamic class binding

Template styles:

- **`styles/preset-sjtu.ts`** — UnoCSS preset defining SJTU color scales (blue/academic), tech sub-palettes, text/background gradients, glow effects, and 30+ theme-aware shortcuts
- **`styles/style.css`** — CSS custom properties for light/dark mode, Monaco editor overrides, KaTeX sizing, v-click transitions
- **`styles/index.ts`** — side-effect CSS import

Template documentation under `docs/`:

- **`COLOR_SYSTEM.md`** — color palette and theming reference
- **`THEME_SUPPORT.md`** — light/dark mode theme support guide
- **`USAGE_EXAMPLES.md`** — component usage examples

The template's `global-bottom.vue` generates animated polygon background layers using `seedrandom` for deterministic randomness. It reads per-slide frontmatter keys (`glow`, `glowOpacity`, `glowHue`, `glowSeed`) for configuration and adapts blend modes for light/dark themes.

### UnoCSS architecture

Root `uno.config.ts` is a trivial re-export of `@slidev/client/uno.config.ts`. The actual customization happens in `template/unocss.config.ts` (and per-talk copies), which merges the Slidev default with `presetSJTU()` and `presetWebFonts()` (Inter, JetBrains Mono, Ubuntu, Caveat — with local font caching via `createLocalFontProcessor()`).

### Scripts

- **`scripts/picker.ts`** — interactive CLI that lists date-prefixed talk folders (matching `^\d{4}-`), reads `README.md` titles, and launches slidev. Supports `-y` flag to auto-select the first folder. `bun dev` opens VS Code on the slides.md (via `code`) and starts the dev server.
- **`scripts/build-all.ts`** — clears `dist/`, discovers published talks from `metadata.json`, and builds them sequentially. Builds are sequential because Slidev's downloadable-PDF renderer uses a fixed local print-server port. It writes the metadata collection after all talks finish.
- **`scripts/build.ts`** — builds one talk's SPA and downloadable `slides.pdf` directly into `dist/<talk-name>/`. It locates the repo root via `findUp` on `bun.lock` and propagates non-zero Slidev exits.
- **`scripts/collect-metadata.ts`** — scans all `talks/` dirs (ignoring `reuse` and `template`) and parses Slidev YAML frontmatter with `gray-matter`. It validates dates, extracts speaker information, and generates deployed PDF URLs for published talks. The CLI writes `public/talks-metadata.json`; production builds write `dist/talks-metadata.json`.
- **`scripts/redirects.ts`** — auto-generates `netlify.toml` from scratch. Discovers all talks via `talks/*/package.json`. Published talks receive `/talk/pdf` → `/talk/slides.pdf` and SPA fallback redirects; all talks receive source redirects.
- **`scripts/random-icons.ts`** — utility to generate random icon lists from Iconify collections. Not integrated into the build pipeline.
- **`scripts/pdf2png.sh`** — Ghostscript-based PDF-to-PNG converter (300 DPI, transparent). Not called by any orchestration script.

### Metadata system

The metadata pipeline is documented in `docs/METADATA_SYSTEM.md`. Additional docs live under `docs/`:

- **`ARCHITECTURE.md`** — architecture decision records and design rationale
- **`IMPLEMENTATION_SUMMARY.md`** — implementation notes and summaries
- **`METADATA_JSON_TEMPLATE.md`** — metadata JSON schema reference
- **`NEXTJS_EXAMPLES.md`** — examples for consuming the metadata API
- **`QUICK_START.md`** — quick start guide
- **`README.md`** — docs index

A GitHub Action (`.github/workflows/update-metadata.yml`) runs `collect-metadata.ts` on every push to main that touches `talks/**`, commits the updated JSON back (with `[skip ci]`), and uploads it as a 90-day artifact. The JSON is served at `https://zheng-talks.netlify.app/talks-metadata.json` with `Access-Control-Allow-Origin: *` and 1-hour cache.

### Key dependencies

- **Slidev** (`@slidev/cli`, `@slidev/client`) — presentation framework
- **UnoCSS** — atomic CSS; root `uno.config.ts` re-exports `@slidev/client/uno.config.ts`
- **Bun** — package manager, runtime, and build tool
- **oxlint** — fast linter (TypeScript, Vue, import, unicorn, oxc plugins; `.oxlintrc.json`)
- **oxfmt** — fast formatter (80 char width; Slidev markdown excluded; `.oxfmtrc.json`)
- **Playwright Chromium** — used by Slidev for PDF export
- **Netlify** — hosting with SPA redirects

### TypeScript config

`tsconfig.json` targets `esnext` with `module: "esnext"`, uses `bundler` module resolution, `noEmit: true`, `allowImportingTsExtensions: true`, `allowSyntheticDefaultImports: true`. Excludes markdown files and `dist` directories.

`types.d.ts` declares an ambient module for `.css` imports so TypeScript doesn't error on CSS side-effect imports.

### Other directories

- **`fonts/`** — local font files for offline use/caching (used by `presetWebFonts` with `createLocalFontProcessor()`)
- **`.agents/skills/`** — shared repository skills, with one directory per skill
- **`.devcontainer/`** — VS Code Dev Container configuration for reproducible development environments
- **`dist/`** — ignored production output containing each published SPA, its generated `slides.pdf`, and the metadata collection
- **`shared-assets/`** — canonical large assets shared through per-talk `public/` symlinks; Vite materializes them into each production build

### Environment variables

No `.env` files exist. The only env var used is `BASE_URL` (in `collect-metadata.ts`).

## Project skills

Skills and their references live under `.agents/skills/`. Read only the skills
needed for the task; use their linked references for conditional detail.

| Skill                                                                  | When to read it                                                                  |
| ---------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| [slidev](.agents/skills/slidev/SKILL.md)                               | Creating/editing Slidev content, configuring features, building, or exporting    |
| [slidev-best-practices](.agents/skills/slidev-best-practices/SKILL.md) | New decks, substantial content changes, presentation redesign, or quality review |
| [frontend-design](.agents/skills/frontend-design/SKILL.md)             | Choosing or revising visual direction, typography, palette, and layout           |
| [web-design-guidelines](.agents/skills/web-design-guidelines/SKILL.md) | Requested UI/design/accessibility review of slides or custom web components      |

For a new deck, use `slidev` with `slidev-best-practices`. Use the two design
skills when their scope is relevant. Keep work in Vue, UnoCSS, and the existing
Slidev structure; preserve the talk's identity and the user's explicit visual
preferences. Check the installed Slidev version before using features from newer
upstream references. Skill updates do not imply dependency upgrades.

Source commits, licenses, local adaptations, and maintenance instructions are
listed in the [skill inventory](.agents/skills/README.md). `skills-lock.json`
records pinned upstream refs and installed folder hashes.
