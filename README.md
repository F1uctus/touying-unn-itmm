# touying-unn-itmm

A [touying](https://github.com/touying-typ/touying) theme reproducing the
official UNN (Lobachevsky State University of Nizhny Novgorod) ITMM
defense-presentation template (`VKR-NNGU-ITMM-2026.pptx`).

The slide canvas is **720 x 405 pt**, identical to the pptx, so every
coordinate from the original template transfers 1:1 (PowerPoint pt =
Typst pt). Full-slide background images extracted from the pptx give
pixel-accurate backdrops by construction.

## Usage

```typst
#import "@local/unn-itmm:0.1.0": *

#show: unn-theme.with(config-info(
  title: [Тема выпускной квалификационной работы],
  subtitle: [Выпускная квалификационная работа бакалавра],
  author: [студент гр. 0000 И.И. Иванов],
  supervisor: [д.ф.-м.н. П.П. Петров],
  specialty: [«Фундаментальная информатика и искусственный интеллект»],
  program: [«Искусственный интеллект»],
  date: datetime(year: 2026, month: 6, day: 1),
))

#title-slide()

== Введение

- The level-2 heading becomes the slide title.

#thanks-slide(contact: [ivanov\@unn.ru])
```

Compile (Arial must be available to typst):

```sh
typst compile examples/demo.typ "examples/out/demo-{p}.png" -f png --ppi 144 --root .
```

## Slide functions

| Function | Purpose |
|---|---|
| `slide` | content slide (white, logo strip, title, slide number) |
| `title-slide` | title layout (layout5 of the pptx) |
| `thanks-slide` | closing slide ("Спасибо за внимание!", slide 27) |
| `focus-slide` / `section-slide` | single centered message on the blue backdrop |

## Components

| Component | Purpose |
|---|---|
| `stat(value, label)` | big number with a caption (brand-book style) |
| `pill(body)` | rounded plaque |
| `two-col(left, right)` | two-column layout |
| `result-map(items, current:, done:)` | row of progress plaques |
| `trust-chain(..steps)` | arrow chain of pipeline stages |

## Geometry

All constants live in `src/geometry.typ` and were read from the pptx XML
(EMU / 12700 = pt).

| Element | Position | Size | Font |
|---|---|---|---|
| Slide canvas | | 720 x 405 pt | Arial |
| Content: title | (23.5, 72.8) | 648.4 x 45.6 | ~22 pt bold `#00348A` |
| Content: body box | (29, 126) | 668 x 243 | 21 pt `#3D3D3E` |
| Content: slide number | (508.5, 375.4) | 175.7 x 21.6 | 9 pt `#888DB0`, right |
| Content margins | top 126, left 29, right 23, bottom 36 | | |
| Title: divider line | (26.8, 213.5) | 657.1 x 2.9 | white |
| Title: subtitle | (26.9, 99.9) | w 460.3 | 16 pt white |
| Title: thesis title | (26.9, 137.4) | w 583.1 | 21 pt white |
| Title: author | (27.5, 241.6) | w 264.1 | 12 pt white |
| Title: supervisor | (26.8, 288.2) | w 274.2 | 13 pt white |
| Title: specialty | (332.5, 241.6) | w 364.4 | 12 pt white |
| Title: program | (332.5, 291.3) | w 335.8 | 12 pt white |
| Title: date | (27.5, 352.4) | w 123.8 | 11 pt white |
| Thanks: message | y 170.7 | h 51.9 | 33 pt bold white, centered |

Palette (from `ppt/theme/theme1.xml`): primary `#00348A`, accent blue
`#1E52A8`, green `#14D49F`, orange `#FF9B71`, panels `#E2EEFF` /
`#F1F7FF`, text `#3D3D3E`, gray `#404040`, slide number `#888DB0`.

The slide number equals the physical page number (the title slide is
page 1), matching the pptx numbering.

## License

Code is MIT-licensed. The images under `assets/` originate from the UNN
brand book and remain the property of Lobachevsky State University of
Nizhny Novgorod; they are included solely to typeset presentations in
the official university style.
