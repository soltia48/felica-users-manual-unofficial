# FeliCaカードユーザーズマニュアル (非公式版)

FeliCa Standardの仕様をLaTeXで文書化した非公式のマニュアルです。日本語版と英語版があります。

[English README](README.md)

## 構成

```
.
├── ja/card_usersmanual.tex   # 日本語版 (ltjsreport, LuaLaTeX)
├── en/card_usersmanual.tex   # 英語版 (report クラス, LuaLaTeX)
├── card_usersmanual.bib      # 共有の参考文献データベース
├── images/                   # 共有の図版 (\graphicspath)
└── assets/                   # 共有の素材ファイル
```

両版は `card_usersmanual.bib`・`images/`・`assets/` を共有し、`../card_usersmanual.bib`
および `../images/` として参照しています。両版は章・節・表の構成と表のラベル名を一致
させてあるため、一方への変更をもう一方へ反映しやすくなっています。

## ビルド

```sh
cd ja   # または cd en
latexmk -lualatex -output-directory=build card_usersmanual.tex
```

ビルドにはLuaLaTeXを使用します。ローカルにTeX環境がない場合は、
`texlive/texlive:latest-full` のDockerイメージでビルドできます。

```sh
docker run --rm -v "$PWD":/work -w /work/ja texlive/texlive:latest-full \
  latexmk -lualatex -output-directory=build card_usersmanual.tex
```

GitHub Actionsはpushのたびに両版をビルドし、`card_usersmanual-ja` および
`card_usersmanual-en` という名前のアーティファクトとしてアップロードします。

## リリース

`v` で始まるタグ (例: `v1.0.0`) をpushすると、両版のPDFが
`card_usersmanual-ja-v1.0.0.pdf` および `card_usersmanual-en-v1.0.0.pdf` として
GitHub Releaseに添付されます。

```sh
git tag v1.0.0
git push origin v1.0.0
```
