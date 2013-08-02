BXcjkipafont パッケージ
========================

LaTeX の CJK パッケージで IPA フォントを「とても簡単に」使えるように
するための LaTeX パッケージ

### 前提環境

  - 処理系： 欧文LaTeX
  - DVIウェア： dvipdfmx, pdfTeX
  - 前提パッケージ
      * CJK パッケージ
      * zhmetrics パッケージ
  - IPAフォントのインストールが必要。

### インストール

  - \*.sty   → $TEXMF/tex/latex/BXcjkipafont

bxcjkipafont - 本体
-------------------

### 機能

パッケージ読込は以下の通り。オプションは（今は）ない。

    \usepackage{bxcjkipafont}

以下の 2 つの CJK フォントファミリが利用可能になる。

  - ipam = IPA明朝
  - ipag = IPAゴシック

更新履歴
--------

  * Version 0.2  <2013/02/03>
      - 最初の公開版
