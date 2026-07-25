# FeliCa Card User's Manual (Unofficial Edition)

An unofficial documentation of the FeliCa Standard specification, written in LaTeX
and published in Japanese and English.

[日本語版の README](README.ja.md)

## Structure

```
.
├── ja/card_usersmanual.tex   # Japanese edition (ltjsreport, LuaLaTeX)
├── en/card_usersmanual.tex   # English edition (report class, LuaLaTeX)
├── card_usersmanual.bib      # Shared bibliography
├── images/                   # Shared figures (\graphicspath)
└── assets/                   # Shared asset files
```

Both editions share `card_usersmanual.bib`, `images/` and `assets/`, and reference
them as `../card_usersmanual.bib` and `../images/`. The two editions are kept
structurally identical: they have the same chapters, sections and tables, and the
same table labels, so that a change to one can be mirrored in the other.

`web/index.html` is the landing page for the published website, and `build.mk4` is
the [make4ht](https://www.kodymirus.cz/make4ht/) build file used for the HTML
output.

## Build

```sh
cd ja   # or: cd en
latexmk -lualatex -output-directory=build card_usersmanual.tex
```

The document is built with LuaLaTeX. If you do not have a local TeX installation,
the `texlive/texlive:latest-full` Docker image can be used instead:

```sh
docker run --rm -v "$PWD":/work -w /work/ja texlive/texlive:latest-full \
  latexmk -lualatex -output-directory=build card_usersmanual.tex
```

GitHub Actions builds both editions on every push and uploads them as the
`card_usersmanual-ja` and `card_usersmanual-en` artifacts.

## Release

Pushing a tag that starts with `v` (for example `v1.0.0`) attaches both PDFs to the
corresponding GitHub Release as `card_usersmanual-ja-v1.0.0.pdf` and
`card_usersmanual-en-v1.0.0.pdf`.

```sh
git tag v1.0.0
git push origin v1.0.0
```

## Website

On every push to `main`, both editions are also converted to HTML with `make4ht`
and published to GitHub Pages together with the PDFs, under `/en/` and `/ja/`.
Enable it once in the repository settings under **Settings → Pages → Build and
deployment → Source: GitHub Actions**.

For the Japanese edition, `make4ht` cannot process the `ltjsreport` class, so the
source selects `report` + `luatexja` when it detects that it is being run by
tex4ht (`\ifdefined\HCode`), and keeps `ltjsreport` for the PDF build. Both paths
use LuaLaTeX, so the content stays single-source.
