# Visual Design for Technical Slides

Use this reference when creating or revising a deck's visual system. These are
starting points for this repository, not fixed requirements for every talk.

## Canvas and Hierarchy

Work within the configured `canvasWidth` and `aspectRatio`. Slidev scales that
canvas to the screen; viewport CSS such as `100vw` inside slide content can
break the intended composition. See [Slide Canvas Size](https://sli.dev/features/canvas-size).

For a new 980 × 551 canvas (16:9), useful starting values in canvas CSS pixels
are 40–56 px for major titles, 24–30 px for body text, and 18–22 px for code and
supporting labels. These are not WCAG thresholds. Inspect them at presentation
size, with the actual theme and viewing distance. Essential information belongs
in the readable text tier, not a tiny caption.

Establish a repeatable grid with generous edge margins, aligned content starts,
and a reserved footer area. Keep the claim visually strongest, then the evidence,
then attribution. Use empty space to group related material. For overflow,
remove repetition, shorten text, crop to the relevant figure region, or split
the slide before reducing font size or `zoom`.

## Typography and Color

Choose type for the language and subject. Retain the existing family when it
already serves the deck; support Chinese and mixed Latin/math text explicitly.
Use a small type scale and consistent line spacing. Avoid justified paragraphs
and line breaks that detach a unit from its value or a symbol from its meaning.

Define palette roles: background, primary text, secondary text, accent, and
semantic comparison colors. Use a stable accent to guide attention. The SJTU
template provides brand colors and semantic shortcuts in
`template/styles/preset-sjtu.ts`; reuse those when that identity is appropriate.

Measure contrast for meaningful text and interactive controls. Check the intended
light/dark mode and a washed-out projection view. Pair color with labels,
markers, patterns, or position for category distinctions. Do not use a faint
gray label for a condition needed to understand a result.

## Layout Follows the Content

| Content                     | Useful starting composition                     | Main check                                    |
| --------------------------- | ----------------------------------------------- | --------------------------------------------- |
| Main claim and result       | Claim above one large plot                      | Axes, conditions, and conclusion are readable |
| Before/after or two methods | Aligned columns with shared scales              | Comparable inputs and visual weight           |
| Method or architecture      | One flow with short node labels                 | Clear reading order and explained arrows      |
| Code explanation            | Focused code plus nearby annotation             | Highlight matches the spoken step             |
| Equation or derivation      | One relationship, then successive steps         | Symbols and assumptions are defined           |
| Closing                     | A few specific takeaways and a useful next step | Audience can recall the core argument         |

Choose the layout for the material instead of filling every slide with the same
card grid. Prefer real diagrams, measurements, screenshots, or specimens from
the subject over generic decorative icons. Keep institutional marks subordinate
to the content after the cover.

## Plots, Tables, and Equations

Redraw charts from the supplied data when possible. Keep units, baseline labels,
sample sizes, and uncertainty needed to interpret the claim. Use consistent
axis ranges for direct comparisons or call out differences clearly. Do not
truncate axes in a way that misstates the effect.

Use vector figures where practical and raster images with enough resolution
for the output. Crop irrelevant surrounding UI without removing context that
changes the meaning. Add a short citation near borrowed figures and retain the
complete reference in notes or a references slide.

Tables should support a particular comparison. Align numeric columns, keep
precision consistent, and highlight only the relevant cells. Move an exhaustive
table to the appendix instead of compressing it into unreadable type.

Use native LaTeX/KaTeX for equations. Name variables and explain the operation
being introduced. A screenshot of a full paper page rarely works as the primary
explanation; an enlarged excerpt plus a clear takeaway is more effective.

## Motion and Interaction

Use motion to show a change, relationship, or causal step. Prefer click-driven
reveals during a talk; keep intermediate states legible and stable. Preserve the
meaning when animations are reduced or the slide is exported as a still image.

For custom CSS, list transition properties explicitly and prefer opacity and
transform where suitable. Honor `prefers-reduced-motion` without revealing or
hiding content incorrectly. Avoid continuous decoration behind formulas and
plots. In the SJTU template, reduce `glowOpacity` for dense evidence slides when
the background competes with the material.

Give custom controls real button/link semantics, accessible names, keyboard
operation, and visible focus. Ensure a focused demo does not unintentionally
consume the keys needed to navigate the presentation.

## Final Visual Pass

Look at an overview of the deck for pacing and consistency, then inspect the
densest slide at full size. Check footer collisions, long CJK headings, equation
baselines, code wrapping, diagram labels, figure contrast, and the opening and
closing slides. Remove decoration that competes with the message. Preserve an
explicit visual preference from the user even when a generic design skill would
choose something else.
