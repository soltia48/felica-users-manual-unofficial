# FeliCa Card Users Manual (Unofficial) / FeliCa カードユーザーズマニュアル (非公式版)

## Structure / 構成

```
.
├── ja/card_usersmanual.tex   # 日本語版 (ltjsreport, LuaLaTeX)
├── en/card_usersmanual.tex   # English edition (report class, LuaLaTeX)
├── card_usersmanual.bib      # 共有の参考文献データベース / shared bibliography
├── images/                   # 共有の図版 / shared figures (\graphicspath)
└── assets/                   # 共有の素材ファイル / shared asset files
```

Both editions share `card_usersmanual.bib`, `images/`, and `assets/`; they reference
them as `../card_usersmanual.bib` and `../images/`.

## Build / ビルド

```sh
cd ja   # or: cd en
latexmk -lualatex -output-directory=build card_usersmanual.tex
```

GitHub Actions builds both editions on every push and uploads them as the
`card_usersmanual-ja` and `card_usersmanual-en` artifacts.
