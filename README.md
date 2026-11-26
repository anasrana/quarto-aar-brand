# quarto-aar-brand

The shared look of Anas A Rana's sites: ET Book text, IBM Plex Mono code, the Tufte-style stylesheet with light and dark palettes, and a small house-style filter. Used by [the homepage](https://anasrana.github.io) and [the EMS practicals](https://anasrana.github.io/ems-practicals/).

## Install

```bash
quarto add anasrana/quarto-aar-brand
```

This copies the extension into `_extensions/anasrana/tufte-brand/`; commit that folder. Update later with `quarto update anasrana/quarto-aar-brand`. Needs Quarto 1.11 or later.

## Use

```yaml
format:
  tufte-brand-html:
    page-layout: article
    # optional project-specific rules, layered after the shared stylesheet
    theme:
      light: [site.scss]
      dark: [site.scss]
```

Installing the extension also sets the project's `brand:` to the extension's `_brand.yml`, so a project needs no `_brand.yml` of its own.

In a project stylesheet, start with `/*-- scss:rules --*/` and use the `$tufte-*` variables (`$tufte-ink`, `$tufte-paper`, `$tufte-muted`, `$tufte-rule`, `$tufte-red`, `$tufte-orange`, `$tufte-code-bg`, `$tufte-serif`); they take the dark values in the dark theme.

## What is in it

| File | Purpose |
|---|---|
| `_brand.yml` | Colours (light and `*-dark`) and font families |
| `fonts.css` | `@font-face` rules for the web fonts (a plain stylesheet, so Quarto copies it and the font files into the site) |
| `tufte.scss` | Tufte typography: headings, small caps, margin notes, tables, code panels, syntax colours, footer |
| `tufte-dark.scss` | Dark palette; inverts SVG figures (opt out with `.no-invert`) |
| `tufte.lua` | Acronyms in small caps, tadpole end mark (`endmark: false` to turn off), `***` section break, hanging quotes, code language labels, compact profile header when `person` metadata exists |
| `fonts/` | ET Book (MIT) and IBM Plex Mono (OFL), with licences: `.woff2` for the web, plus `.otf`/`.ttf` desktop files for R plots and PDF (see each folder's README) |
| `logo/` | Frog logo, favicons, tadpole |

Favicons are not added automatically; each site links them itself (for example with `book: favicon:` or an `include-in-header` file).

## Licence

The stylesheets, filter and `_brand.yml` are under the MIT licence (see `LICENSE`). The logo files in `logo/` (frog logo, favicons, tadpole) are not: they are © Anas A Rana, all rights reserved, and are not for reuse without permission. If you reuse this extension, replace the logo with your own. The fonts keep their own licences, included alongside them: ET Book under MIT (`fonts/et-book/LICENSE`) and IBM Plex Mono under the SIL Open Font License 1.1 (`fonts/ibm-plex-mono/LICENSE`).

## Fonts in R plots and PDF

Register the desktop files before plotting with a font-aware device such as `ragg`:

```r
f <- "_extensions/anasrana/tufte-brand/fonts/"
systemfonts::register_font("ET Book",
  plain  = paste0(f, "et-book/et-book-roman.otf"),
  italic = paste0(f, "et-book/et-book-italic.otf"),
  bold   = paste0(f, "et-book/et-book-bold.otf"))
```
