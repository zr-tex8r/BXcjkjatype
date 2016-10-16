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

### パッケージ読込

    \usepackage[<option>,...]{bxcjkjatype}

利用可能なオプションを以下で挙げる。

#### 自動囲み込み

文書本体を `CJK(*)` 環境で自動的かつ安全に囲うためのオプション。文書中に
多量の CJK テキストが含まれる場合、或いは「動く引数」に CJK テキストが
含まれる場合はこれを指定するのが適切である。

  * `whole`、`wholeCJK*`： 文書全体を `CJK*` 環境で囲む。（厳密に言うと
    `\begin{uCJK*}`～`\end{uCJK*}` で囲む。）
  * `wholeCJK`： 文書全体を `CJK` 環境で囲む。（厳密に言うと
    `\begin{uCJK}`～`\end{uCJK}` で囲む。）
  * `nowhole`（既定）： `wholeCJK*` 及び `wholeCJK` の否定。

#### 「自動チルダ」

`autotilde` オプションを指定すると、`\CJKtilde` が自動的に呼び出されて
`~` が和欧文間空白（四分空き）の意味になる。なお、`\CJKtilde` 有効時は
`\nbs` で非分割欧文空白（本来の `~` の意味）が挿入できる。また、
`\standardtilde` は `\CJKtilde` の効力を打ち消す。（これらは CJK
パッケージの機能である。）

  * `autotilde`： 全ての `CJK(*)` 環境の先頭で `\autotilde` が呼び出され
    るようにする。
  * `noautotilde`（既定）： `autotilde` の否定。

#### フォントマップ設定

[pxchfon パッケージ] と同等のフォントマップのプリセットが利用できる。
詳細についてはそちらの解説文書を参照されたい。

  * `oneweight`、`nooneweight`： pxchfon と同様。
  * pxchfon で利用可能なプリセットオプション（`ms` 等）が利用できる。
    （旧式のものを除く。）
  * `ttfname=<パターン>`： TTC 代替（後述）を行う場合の TTF フォント名の
    パターンを指定する。
  * `ipaex-type1`： 本パッケージのフォント管理を無効にし、ipaex-type1
    パッケージのファミリ（`ipxm` と `ipxg`）を直接用いる。この設定では
    `\mcdefault` の値は `ipxm` に、`\gtdefault` の値は `ipxg` になる。

[pxchfon パッケージ]: http://www.ctan.org/pkg/pxchfon

#### CJK フォントスケール

  * `scale=<実数>`： CJK フォントに対するスケール値を設定する。

※0.3 版より、`ipaex-type1` 指定時も CJK フォントスケールが利用できるよう
になった。

#### その他のオプション

  * `everypage`： フォントマップ情報を出力 DVI 文書の全てのページに出力
    する。`dvipdfmx` ドライバでのみ有効。
  * `noeverypage`（既定）： `everypage` の否定。
  * ドライバオプション：
    `pdftex`、`dvipdfmx`、`dvips`、`none` が指定できる。ドライバ設定は
    既定（ipaex-type1）以外のフォントマップの使用時にのみ意味をもつ。
    さらに、フォントマップ変更は `pdftex` と `dvipdfmx` でのみサポート
    されまたこの 2 つの値は常に自動判定可能（PDF モードでは `pdftex`、
    DVI モードでは `dvipdfmx` が既定）なので、実際にはドライバを指定する
    必要はない。
  * `substmingoth`： CJK パッケージの日本語用総称ファミリとして慣習的に
    使われているファミリの `min`／`goth`／`maru` について、LaTeX レベル
    で、本パッケージにおける標準ファミリである `mc`／`gt`／`mg` への代替
    を設定する。これにより、`min` 等のファミリの使用を前提とした日本語湯
    テンプレート等を使う場合においても、論理フォントレベルでの代替設定を
    行う必要がなくなる。
  * `nosubstmingoth`（既定）： `substmingoth` の否定。
  * `boldbyembolden`（既定）： CJK パッケージの“擬似太字”（`\CJKbold`）
    の処理方法を“重ね打ち”から“合成太字”に変更する。
  * `noboldbyembolden`： `boldbyembolden` の否定。

#### TTC 代替

pdfTeX エンジンは TTC 形式のフォントをサポートしていない（サポートして
いる OpenType の形式は単体の TTF グリフのものだけである）。従って、
`\setminchofont` 命令などで TTC フォントを使おうと望むなら、適当なツール
を使って TTC フォントファイルを個々の TTF フォントファイルに分解する処理
を行うことが必須になる。

これはエンジン側の制限仕様のため仕方がないだろう。しかし本パッケージを
用いる場合には他に問題がある。変換後の TTF フォントはファイル名が元のもの
と異なるため、プリセット設定（`mobo-moga` 等のオプション）が使えないので
ある。これを解決するために、0.3 版で `ttfname` オプションが新設された。

例えば、パッケージ読込時に `ttfname=*_1` が指定されたとする。この状態で
本パッケージの処理において「mogam.ttc の最初（0 番）」が要求された場合、
代わりに「mogam_1.ttf」というファイルが使われる。同様に、「mogam.ttc の
1 番、2 番、……」については「mogam_2.ttf」「mogam_3.ttf」……での代替が
行われる。

`ttfname` で指定するファイル名のパターンには「`*_1`」「`TEMP-*-00.TTF`」
のように「`*` を 1 つ含み、数字列を含む文字列」が指定できる。この `*` の
部分は要求の TTC ファイルのベース名（`mogam` 等）で置き換えられ、かつ、
拡張子がない場合は `.ttf` が補われる。その結果の文字列が TTC の最初（0
番）のフォントに対する代替ファイル名となる。後続（1 番、2 番、……）の
代替ファイル名は数字部分をインクリメントしたものになる。

### 機能

#### CJK フォントの選択

本パッケージでは、pLaTeX + [japanese-otf パッケージ] で用いられるものと
同等の 3 つの「総称」CJK ファミリを用意する： 明朝（`\mcfamily`）、
ゴシック（`\gtfamily`）、丸ゴシック（`\mgfamily`）。既定では ipaex-type1
パッケージのフォントが割り当てられている：明朝→IPAex明朝、ゴシック→
IPAexゴシック。この割り当ては変更可能である。

  * `\mcfamily`： CJK ファミリを明朝ファミリに変更する。
    `\CJKfamily{\mcdefault}` と等価である。
  * `\gtfamily`： CJK ファミリをゴシックファミリに変更する。
    `\CJKfamily{\gtdefault}` と等価である。
  * `\mgfamily`： CJK ファミリを丸ゴシックファミリに変更する。
    `\CJKfamily{\mgdefault}` と等価である。

高度な命令：

  * `\mcdefault`／`\gtdefault`／`\mgdefault`： 総称ファミリに対応する
    CJK ファミリ名である。標準の割当ではこれらの値は `mc`／`gt`／`mg` で
    ありこの割当が既定で用いられる。

  * `\setCJKfamilydefault{<CJKファミリ>}`： 既定の CJK ファミリを設定
    する。この既定値は、ある種の命令（例えば `\CJKfamily{}` や
    `\begin{CJK}{UTF8}{}`）でファミリ名が省略された時に用いられる。
    （再定義後の）`\normalfont` は CJK ファミリをこの命令で設定した既定
    ファミリに変更する。

    この既定ファミリの既定値は、文書の本体の先頭で有効である欧文ファミリ
    の「対応ファミリ」となる。（次小節を参照。）

[japanese-otf パッケージ]: http://www.ctan.org/pkg/japanese-otf

#### CJK と欧文のファミリの連動

CJK パッケージ（および pTeX エンジン）では CJK と欧文で別々の「現在
ファミリ」を管理する。この取扱は利点もあるが、多くの場合はこの 2 つの
「現在ファミリ」を連動させた方が都合がよい。この為、本パッケージでは現在
欧文フォントを切り替える幾つかの LaTeX 命令について、CJK ファミリを欧文
の「対応ファミリ」に切り替えるように再定義する。ここで「対応ファミリ」は
以下のように定められる：

  * `\rmfamily`（セリフ） → `\mcfamily`（明朝）
  * `\sffamily`（サンセリフ） → `\gtfamily`（ゴシック）
  * `\ttfamily`（等幅） → `\gtfamily`（ゴシック）
  * その他のファミリについては、対応ファミリは `\mcfamily` とする。

再定義される命令：

  * `\rmfamily`／`\sffamily`／`\ttfamily`： 本来の動作の後、CJKファミリ
    を欧文ファミリの「対応ファミリ」に変更する。
  * `\normalfont`： CJK ファミリを、`\setCJKfamilydefault` 命令により
    指定された既定 CJK ファミリに変更する。

`CJK`／`CJK*` 環境の省略系：

  * `\begin{uCJK*}...\end{uCJK*}`： 次のものと等価：

        \begin{CJK*}{UTF8}{対応ファミリ}...\end{CJK*}

    ただし `対応ファミリ` は現在の欧文ファミリの対応ファミリを表す。

    次のものと等価ではないことに注意：

        \begin{CJK*}{UTF8}{}...\end{CJK*}

    こちらは既定の CJK ファミリを使用する。

  * `\begin{uCJK}...\end{uCJK}`： 次のものと等価：

        \begin{CJK}{UTF8}{対応ファミリ}...\end{CJK}

#### フォントマップ設定

これらの命令の使い方は pxchfon パッケージの時と同じであるので、詳細に
ついてはそちらの解説文書を参照されたい。

  * `\setminchofont[<ID>]{<フォントファイル名>}`
  * `\setgothicfont[<ID>]{<フォントファイル名>}`
  * `\setmarugothicfont[<ID>]{<フォントファイル名>}`
  * `\setmediumminchofont[<ID>]{<フォントファイル名>}`
  * `\setboldminchofont[<ID>]{<フォントファイル名>}`
  * `\setmediumgothicfont[<ID>]{<フォントファイル名>}`
  * `\setboldgothicfont[<ID>]{<フォントファイル名>}`
  * `\setxboldgothicfont[<ID>]{<フォントファイル名>}`

ところが、pdfTeX エンジンについてはフォントマップの仕様に関して重大な
制限が存在する。TrueType グリフであってかつ TTC 形式でないフォントのみ
が使用できる。（dvipdfmx 使用時は全ての種類の OpenType フォントが使用
可能。）

注意： 本パッケージは「明朝・細字」のフォントをサポートしない。従って、
`\setlightminchofont` は動作しない。

#### その他の命令

  * `\UTF{<16進数字>}`： CJK 文字を Unicode 符号値で入力する。例えば、
    `\UTF{5B57}` は `\Unicode{"5B}{"57}` と等価である。

  * `\CJKforce{<character>...}`： 以降は引数の中にある各々の文字を CJK
    文字として扱う（CJK フォントで出力される）。

  * `\CJKunforce{<character>...}`： `\CJKforce` の効果を打ち消す。

  * `\@<character>`： 非 ASCII 文字の前に `\@` がある場合は、その文字
    （その出現のみ）を CJK 文字として扱う。ASCII 文字の前の `\@` は
     LaTeX 本来の意味を保持する。

  * `\CJKecglue`： 和欧文間空白を挿入する。`\CJKtilde` が有効な時は `~`
    はこの命令を呼び出す。この命令をユーザが再定義して和欧文間空白の量を
    調節することができる（和文間空白の `\CJKglue` と同様）。

    使用例：

        \renewcommand{\CJKecglue}{\hspace{0.125em minus 0.125em}}

### 補足事項

  * 本パッケージで標準に用いられるフォントは、例えそれに ipaex-type1 の
    フォントが割り当てられている場合でも、縦書きをサポートしない。しかし
    ipaex-type1 が提供するファミリ（`ipxm` と `ipxg`）は縦書きをサポート
    しており、`ipaex-type1` オプションを指定することでそれらのファミリを
    直接使うことができる。

更新履歴
--------

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
http://zrbabbler.sp.land.to/
