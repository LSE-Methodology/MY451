# MY451 Coursepack source

[![Render and deploy](https://github.com/LSE-Methodology/MY451/actions/workflows/deploy_bookdown.yml/badge.svg?branch=master)](https://github.com/LSE-Methodology/MY451/actions/workflows/deploy_bookdown.yml)
[![Netlify Status](https://api.netlify.com/api/v1/badges/lse-methodology-my451/deploy-status)](https://app.netlify.com/sites/lse-methodology-my451/deploys)

Source for the course pack and main text of **MY451 — Introduction to Quantitative Analysis**, taught in the Department of Methodology at the London School of Economics and Political Science.

Published at: <https://lse-methodology.github.io/MY451/>

## What this repo contains

The course pack is authored in [R Markdown](https://rmarkdown.rstudio.com/) and built with [bookdown](https://bookdown.org/). One chapter per file:

- `index.Rmd` — preface ("Course information")
- `01-MY451-intro.Rmd` … `10-MY451-more.Rmd` — chapters
- `11-MY451-appendix.Rmd` — appendix
- `images/` — figures (one `.png` for HTML/EPUB and one `.pdf` for the LaTeX/PDF build per figure)
- `_output.yml`, `_bookdown.yml` — bookdown configuration
- `preamble.tex`, `pandoc-conversion-templates/` — LaTeX-side settings for the PDF build
- `style.css` — light CSS tweaks on top of `bookdown::bs4_book`

The HTML output uses bookdown's modern Bootstrap 4 theme (`bs4_book`). A PDF version and an EPUB version are also produced from the same source.

## Editing and contributing

1. Clone the repo.
2. Edit any `.Rmd` file.
3. Commit and push to `master`.

A GitHub Actions workflow (`.github/workflows/deploy_bookdown.yml`) renders the book and publishes it to GitHub Pages. There is no need to build locally to publish.

If you do want to build locally:

```r
install.packages(c("rmarkdown", "bookdown", "downlit", "bslib"))
bookdown::render_book("index.Rmd")          # all formats
bookdown::render_book("index.Rmd", "bookdown::bs4_book")  # HTML only
```

For an authoring reference (Markdown, tables, figures, equations, cross-references), see [`AUTHORING.md`](AUTHORING.md).

For details on the deploy workflow, see [`devel.md`](devel.md).

## License

See [LICENSE](LICENSE).
