# Browser and Export Verification

Use the installed CLI and the target talk's scripts. Keep temporary screenshots
and exports in a temporary directory; commit source and intended deliverables
only. A skill update alone does not require rebuilding every existing talk.

## Development Review

From `talks/<talk-name>/`:

```bash
bun run dev --port 3030
```

Use the URL actually printed by the server. With browser tools or Playwright,
inspect each changed slide and neighboring transitions; for a new deck, review
all slides. The overview is useful for pacing, but it does not replace reading
dense slides at presentation size.

Check the configured canvas at a typical presentation viewport (for example,
1280 × 720), then a smaller browser window. For custom interactive controls,
also check keyboard navigation and a reduced-motion setting. Review the modes
the deck actually supports; avoid changing a deliberate single-mode design
merely to satisfy a generic checklist.

Wait for fonts, images, diagrams, and data before capturing screenshots. Useful
browser readiness checks include `document.fonts.ready` and image `complete` /
`naturalWidth`; check for missing glyphs and failed network requests too.
Network idle alone may never occur with remote embeds or background requests.

For each changed slide, inspect:

- The initial, meaningful intermediate, and final click states; go backward too.
- Text wrapping, code, formulas, axes, captions, footer, and attribution.
- Clipped content, collisions, unexpected scrollbars, and broken assets.
- Console errors and controls that swallow navigation keys or lose focus.

DOM measurements can identify suspicious overflow, but hidden click elements,
intentional cropping, and the scaled Slidev canvas need interpretation. Confirm
problems visually before changing layout. If browser access is unavailable,
report that visual verification remains incomplete rather than claiming it passed.

## Build and Static Delivery

```bash
# From talks/<talk-name>/
bun run build
```

This writes to `../../dist/<talk-name>/`. Confirm the expected HTML and assets
exist and inspect build output for failures. If checking a deployed-style build,
serve the repository's `dist/` directory and navigate to `/<talk-name>/`; this
exercises the actual base path instead of assuming root-relative assets work.

The build script generates `dist/<talk-name>/slides.pdf` together with the SPA.
Inspect that generated file when verifying deployment output. The talk's separate
`export` script may write elsewhere; check its configured path before using it.
Generated PDFs and PPTX files under talk `assets/` directories are ignored by Git.

## Export Checks

For a temporary PDF check from the talk directory:

```bash
deck_check_dir=$(mktemp -d /tmp/slidev-review.XXXXXX)
bunx slidev export --per-slide --output "$deck_check_dir/deck.pdf"
# Add --range 1,3-5 to inspect selected slides.
# Add --with-clicks when each reveal needs a separate exported page.
```

Choose `--per-slide` when global layers rely on the current slide. In the
installed CLI it breaks cross-slide PDF links and the table of contents; omit
it when those features matter and verify global layers separately. Compare the
PDF to the browser, especially equations, fonts, clipping, and reveal-dependent
content. Confirm the output opens, has the intended page count, and includes the
last slide. A PNG export can help inspect selected slides:

```bash
bunx slidev export --format png --range 1-3 --output "$deck_check_dir/png"
```

The repository declares `playwright-chromium`; if its browser binary is missing,
use the workspace's `bunx playwright install chromium`. For slow rendering,
adjust `--timeout` / `--wait` based on the observed failure. Changing
`--wait-until` can bypass a hang but requires checking that all content rendered.

For PowerPoint, the installed Slidev 52.19.1 supports image-based `pptx`, which
preserves the rendered slide but does not create editable text boxes. Newer
upstream `pptx-editable` has different capabilities and limitations; only use it
after confirming support with `bunx slidev export --help`. Web demos and videos
need a meaningful static representation in exported formats.

For scientific visuals intended for publication, use the original plotting or
vector source for the figure rather than treating a slide screenshot as the
publication artifact.

## Completion

After corrections, repeat the checks affected by those corrections. Run the
repository linter for changed Vue/TypeScript code and format checks for supported
file types. The repository formatter excludes Slidev source Markdown; use an
appropriate Slidev formatter only when necessary, then inspect the result.

Report which deck, slide range, mode, build, and export were actually checked.
Identify missing browser checks, unavailable remote assets, or unsupported
export features specifically. Keep deployment and publication within the user's
authorized scope.

References: [exporting](https://sli.dev/guide/exporting),
[global layers](https://sli.dev/features/global-layers), and
[hosting](https://sli.dev/guide/hosting).
