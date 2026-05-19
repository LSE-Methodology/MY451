# Authoring guide

Quick reference for editing the MY451 course pack. The source is [Pandoc-flavored Markdown](https://pandoc.org/MANUAL.html) processed by [bookdown](https://bookdown.org/). There is no R code in these chapters, so any text editor works.

## Recommended editors

- **[Visual Studio Code](https://code.visualstudio.com/)** is the easiest general-purpose choice. The built-in Markdown support handles `.Rmd` files fine; for richer support, install the [R extension](https://marketplace.visualstudio.com/items?itemName=REditorSupport.r) (syntax-aware editing for `.Rmd`) or the [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) extension. VS Code's Git integration also covers the commit/push workflow needed to publish.
- **[RStudio](https://posit.co/download/rstudio-desktop/)** is a good alternative if you already use R. It opens `.Rmd` files natively, can preview the book locally with the "Build Book" button (which calls `bookdown::render_book("index.Rmd")`), and includes Git integration.

Either editor is fine — pick whichever you are more comfortable with.

## Headings

```markdown
# Top-level header (chapter)
## Section
### Subsection
#### Subsubsection
```

Headings are automatically numbered. To exclude a heading from numbering, append `{-}`:

```markdown
# Appendix {-}
```

## Emphasis and lists

```markdown
*italic*, **bold**, ***bold italic***

1. Numbered item
2. Numbered item

* Unnumbered item
  + Sub-item
```

## Tables

Simple table:

```markdown
  Region               Frequency   Proportion       %
  ------------------ ----------- ------------ -------
  Africa                      48        0.310    31.0
  Asia                        44        0.284    28.4

  : (\#tab:t-region)Frequency distribution of region.
```

The horizontal rule sets column widths; first-line alignment of each column sets the alignment of the whole column.

Multiline table (cells that span multiple lines):

```markdown
-------------------------------------------------------------
 Centered   Default           Right Left
  Header    Aligned         Aligned Aligned
----------- ------- --------------- -------------------------
   First    row                12.0 Example of a row that
                                    spans multiple lines.

  Second    row                 5.0 Another row. Note the
                                    blank line between rows.
-------------------------------------------------------------

  : Example of a multiline table.
```

## Figures

Figures live in `images/`. Provide **both** a `.pdf` (used by the LaTeX/PDF build) and a `.png` (used by HTML/EPUB) with the same base name. Reference the image by base name only — no extension:

```markdown
![(\#fig:bar-attitude)Caption text.](bar_attitude)
```

Leave a blank line before and after the image, or it will not be numbered/captioned in the PDF.

## Equations

In-line: `$ ... $` with a space before the opening `$`.

Display (unnumbered): `$$ ... $$`.

Display, labeled and auto-numbered:

```latex
\begin{equation}
\bar{Y} = \frac{\sum Y_i}{n} \label{eq:mean}
\end{equation}
```

Equations can only be cross-referenced from within the same chapter file.

## Cross-references

Anything with an identifier can be referenced with `\@ref(...)`:

```markdown
See Section \@ref(c-intro).
See Table \@ref(tab:t-region).
See Figure \@ref(fig:bar-attitude).
See Equation \@ref(eq:mean).
```

Prefixes: `tab:` for tables, `fig:` for figures, `eq:` for equations. Headings take no prefix.

To label a heading:

```markdown
# Introduction {#c-intro}
```

A heading can be either labeled (`{#id}`) or unnumbered (`{-}`), not both.

## Footnotes

```markdown
Honeymoon salad is made from lettuce alone.^[The Late Show, CBS, 16 September 2016.]
```

## Building and publishing

Push to `master`. GitHub Actions renders the book and publishes the HTML to GitHub Pages. To preview locally:

```r
bookdown::render_book("index.Rmd", "bookdown::bs4_book")
```

The full PDF build additionally needs a LaTeX distribution (e.g. [TinyTeX](https://yihui.org/tinytex/)).
