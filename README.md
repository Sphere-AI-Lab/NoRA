# NoRA project page

A static project page for *Normalized Low-Rank Adaptation*, built to match the
visual language of https://spherelab.ai/PEFT-Arena/ (same type scale, color
tokens, left table-of-contents, breakout benchmark tables, card grids and
BibTeX block).

## Layout

```
page/
  index.html            # the whole page
  css/
    fonts.css           # Iowan Old Style BT / GT America / Chakra Petch aliases
    common.css          # design tokens, reset, fixed header, code
    typography.css      # body type, headings, blockquotes, figures
    blog-post.css       # post layout, TOC, cover, tables, cards, formulas
  static/images/
    fig1-nora-illustration.png   # Figure 1, rendered from the PDF at 300 dpi
    fig2-training-dynamics.png   # Figure 2, rendered from the PDF at 300 dpi
    paper-preview-01.png         # first page thumbnail (150 dpi)
```

Everything is static: open `index.html` directly, or serve the folder
(`python3 -m http.server`). No build step.

## Before publishing

Search `index.html` for `TODO(fill in)`:

1. **Paper button** — replace `https://arxiv.org/abs/XXXX.XXXXX`.
2. **Code button** — replace `https://github.com/YOUR-ORG/NoRA`.
3. **BibTeX** — replace the `arXiv:XXXX.XXXXX` journal field.
4. **Favicon** — add `static/images/favicon-32x32.png` and
   `apple-touch-icon.png`, then uncomment the two `<link>` tags in `<head>`.
5. **Header logo** — currently points at `https://spherelab.ai/blog`.
6. **Date** — the metadata block reads "August 2026".
7. **Paper preview** — swap `paper-preview-01.png` for the camera-ready first
   page if the layout changes.

Author list note: `Ziyin Yue` carries no affiliation superscript, matching the
PDF's author line. Add one if that was an oversight in the paper.

## Deploying to spherelab.ai/NoRA

GitHub Pages serves from the repository root, so move the contents of `page/`
up one level (or set Pages to serve from a `docs/` folder and rename `page/` to
`docs/`). All asset paths are relative, so nothing else needs to change.

## Regenerating the figures

The figures are vector art in the PDF; they were rasterized with poppler and
auto-trimmed:

```
pdftocairo -png -r 300 -f 4 -l 4 -x 250 -y 217 -W 2067 -H 458 NoRA_paper.pdf fig1
pdftocairo -png -r 300 -f 8 -l 8 -x 417 -y 317 -W 1730 -H 617 NoRA_paper.pdf fig2
pdftocairo -png -r 150 -f 1 -l 1 NoRA_paper.pdf page1
```

then cropped to the ink bounding box with a 24px margin. If a figure moves to a
different page, adjust `-f/-l` and the crop box.
