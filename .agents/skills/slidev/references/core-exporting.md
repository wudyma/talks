---
name: exporting
description: Export presentations to PDF, PPTX, PNG, or Markdown
---

# Exporting Slides

Export presentations to PDF, PPTX, PNG, or Markdown.

## Browser Exporter

Access at `http://localhost:3030/export`:

- Select format and options
- Preview and download

## CLI Export

This repository declares `playwright-chromium` at the workspace root:

```bash
bun install
```

### PDF Export

```bash
slidev export
slidev export --output my-slides.pdf
```

### PowerPoint Export

```bash
slidev export --format pptx
```

### Editable PowerPoint (Newer CLI Only)

Current upstream also documents `slidev export --format pptx-editable`, which
reconstructs supported content as editable shapes. Some elements remain images,
and rendering can differ from the browser. This format is **not supported by
the repository's Slidev 52.19.1**; check the installed CLI before using it.
See the [official export guide](https://sli.dev/guide/exporting#editable-pptx).

### PNG Export

```bash
slidev export --format png
slidev export --format png --range 1-5
```

### Markdown Export

```bash
slidev export --format md
```

## Export Options

### With Click Steps

Export each click as separate page:

```bash
slidev export --with-clicks
```

### Dark Mode

```bash
slidev export --dark
```

### Slide Range

```bash
slidev export --range 1,4-7,10
```

### Table of Contents

PDF with clickable outline:

```bash
slidev export --with-toc
```

### Timeout

For slow-rendering slides:

```bash
slidev export --timeout 60000
```

### Wait

Wait before capture:

```bash
slidev export --wait 2000
```

### Wait Until

Wait condition:

```bash
slidev export --wait-until networkidle   # Default
slidev export --wait-until domcontentloaded
slidev export --wait-until load
slidev export --wait-until none
```

### Transparent Background

```bash
slidev export --omit-background
```

### Custom Browser

```bash
slidev export --executable-path /path/to/chrome
```

## Headmatter Options

```yaml
---
exportFilename: my-presentation
download: true # Add download button in build
export:
  format: pdf
  timeout: 30000
  withClicks: false
---
```

## Troubleshooting

### Missing Content

Increase wait time:

```bash
slidev export --wait 3000 --timeout 60000
```

### Wrong Global Layer State

Use `--per-slide` or use `slide-top.vue` instead of `global-top.vue`.
`--per-slide` breaks cross-slide PDF links and the table of contents, so choose
the export mode according to the deliverable and inspect the result.

### Broken Emojis

Use system fonts or install emoji font on server.

### CI/CD Export

Install playwright browsers:

```bash
bunx playwright install chromium
```
