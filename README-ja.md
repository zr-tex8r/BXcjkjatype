BXcjkjatype パッケージバンドル
==============================

LaTeX: pdfLaTeX と CJK パッケージを利用した日本語組版の支援

本パッケージは、日本語組版に適した CJK パッケージの設定を提供する。その
上で、pLaTeX ユーザにとって CJK パッケージの使用が容易にするために、
pLaTeX カーネルや pLaTeX 用パッケージのものに類似した命令を提供する。

なお、CJK パッケージ自体は多種の入力エンコーディングをサポートしている
が、本パッケージでは UTF-8 のみをサポートすることに注意。

### 前提環境

  * フォーマット： LaTeX
  * エンジン： pdfTeX（DVI・PDF モード共に可）
  * DVIウェア： 不問
      - 既定以外のフォント設定では dvipdfmx／pdfTeX が必須。
  * 依存パッケージ：
      - CJK、CJKutf8、CJKspace、CJKpunct、etoolbox
      - ipaex-type1（既定のフォントマップ使用時）
      - zhmetrics（既定以外のフォントマップ使用時）

### インストール

  - `*.sty` → $TEXMF/tex/latex/BXcjkjatype

bxcjkjatype パッケージ
----------------------

本バンドルの本体のパッケージである。

詳細についてはユーザマニュアルを参照されたい。

  * bxcjkjatype.pdf： ユーザマニュアル（英語版）
  * bxcjkjatype-ja.pdf： ユーザマニュアル（日本語版）

bxcjkvert パッケージ
--------------------

CJKvert パッケージの改造版であり、縦組と横組の混在が普通に起こりうる
日本語組版に適合させたものである。

詳細についてはユーザマニュアルを参照されたい。

  * bxcjkvert.pdf： ユーザマニュアル（英語版）
  * bxcjkvert-ja.pdf： ユーザマニュアル（日本語版）

更新履歴
--------

  * Version 0.5  ‹2023/07/23›
      - 最新の LaTeX への対応。

  * Version 0.4  ‹2016/11/11›
      - bxcjkvert パッケージを追加。
      - `CJKtildeasspace` オプションを追加。
      - （試験的） `defaultmingoth` オプションを追加。

  * Version 0.3  ‹2016/10/15›
      - CJKvert パッケージによる縦組と共存を可能にした。
      - hyperref での PDF 文字列の文字化けを防止し。
      - `ipaex-type1` 指定時もフォントスケールを可能にした。
      - `boldbyembolden` 機能を実装。
      - `ttfname` オプションを追加。
      - `substmingoth` オプションを追加。

  * Version 0.2c ‹2013/10/18›
      - CJK フォントスケールをサポートした。
      - `\CJKforce`、`\CJKunforce`、`\@` を追加。

  * Version 0.2b ‹2013/09/28›
      - `\UTF`、`\CJKecglue` を追加。

  * Version 0.2a ‹2013/08/08›
      - `autotilde` オプションを追加。

  * Version 0.2  ‹2013/08/08›
      - 最初の公開版。

--------------------
Takayuki YATO (aka. "ZR")  
https://github.com/zr-tex8r
