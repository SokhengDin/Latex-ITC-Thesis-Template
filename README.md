# Thesis LaTeX Template

A generic starting point for a bachelor/engineering thesis, based on the Institute of
Technology of Cambodia (ITC) format. Compiles to a title page, acknowledgement, Khmer
summary, French résumé, English abstract, abbreviations, table of contents, lists of
figures/tables, numbered sections, and a bibliography.

## Folder structure

`main.tex` (main document) + `sections/` (chapters) + `figure/` + `references/references.bib`
+ `fonts/` (Khmer fonts) + `Cover.pdf` (title pages).

## Requirements

- **XeLaTeX** (won't compile with pdfLaTeX -- uses `fontspec`/`polyglossia` for Unicode text).
- **biber** for the bibliography.
- **Pygments** (`pip install pygments`) for syntax-highlighted code blocks (`minted`).
- `-shell-escape` enabled when compiling (required by `minted`).

### Where to get LaTeX

| Platform | Option |
|----------|--------|
| **Windows** | [MiKTeX](https://miktex.org/download) or [TeX Live](https://tug.org/texlive/) |
| **macOS**   | [MacTeX](https://tug.org/mactex/) |
| **No install** | [Overleaf](https://www.overleaf.com) -- upload this folder as a project |

TeX Live/MacTeX already bundle XeLaTeX, biber, and `minted`'s helper script -- install
Pygments on top and you're set. Any editor works: **TeXShop**/**TeXworks** (bundled
with MacTeX/MiKTeX), **VS Code** + [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop), or **Overleaf** in the browser.

## Fonts

Fonts are set **by name**, so they must be installed on your system (not referenced
by file path): **Times New Roman** and **STIX Two Math** (usually already available;
STIX Two Math is on [GitHub](https://github.com/stipub/stixfonts) if not) plus two
Khmer fonts included in `fonts/`.

- **macOS**: double-click each `.ttf` in `fonts/` → "Install Font".
- **Windows**: right-click each `.ttf` in `fonts/` → "Install".
- **Overleaf**: fonts can't be installed system-wide -- upload the `.ttf` files and
  load them with `Path=`, e.g. `\newfontfamily\khmerfont{KhmerOSSiemreapRegular.ttf}[Path=fonts/]`.

Don't need the Khmer summary? Remove it from `main.tex` and skip the Khmer fonts.

## Compiling

```bash
xelatex -interaction=nonstopmode -shell-escape main.tex
biber main
xelatex -interaction=nonstopmode -shell-escape main.tex
xelatex -interaction=nonstopmode -shell-escape main.tex
```

Three passes plus biber so the TOC, citations, and cross-references all resolve.
Set the engine to **XeLaTeX** with shell-escape enabled:

- **TeXShop/TeXworks**: compiler dropdown → "XeLaTeX".
- **VS Code (LaTeX Workshop)**: default recipe already runs xelatex → biber → xelatex → xelatex.
- **Overleaf**: Menu → Settings → Compiler → **XeLaTeX** (shell-escape and Pygments are already enabled).

## How to adapt this for your own thesis

1. **Cover page** -- replace `Cover.pdf` with your own title pages (or edit the
   `\includepdf[pages={1,2,3}]{Cover.pdf}` line in `main.tex` if your cover has a
   different number of pages).
2. **Front matter** -- in `main.tex`, fill in the Acknowledgement, Khmer summary,
   Résumé, and Abstract sections (each is marked with placeholder text). Remove the
   Résumé section if your institution doesn't require a French summary.
3. **Sections** -- edit `sections/introduction.tex`, `methodology.tex`,
   `resultDiscussion.tex`, and `futureWork.tex`. Each contains one worked example of
   a figure, table, equation, citation, algorithm, and code block so you can see the
   exact syntax to copy. Add more `.tex` files under `sections/` and `\input{}` them
   from `main.tex` as your thesis grows.
4. **Figures** -- drop your own images into `figure/` and reference them with
   `\includegraphics{figure/your-image.png}`.
5. **References** -- add your citations to `references/references.bib` (standard
   BibTeX/biblatex format) and cite them with `\cite{yourkey}`.
6. **Numbering** -- figures and tables are numbered per section automatically
   (e.g. Figure 2.1 is the first figure in Section 2); you don't need to number
   them by hand.
