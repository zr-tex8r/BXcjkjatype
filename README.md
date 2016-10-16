BXcjkjatype Package
===================

LaTeX: Support for Japanese typesetting with pdfLaTeX and CJK package

This package provides working configuration of the CJK package suitable
for Japanese typesetting of moderate quality. Moreover, it facilitates
use of the CJK package for pLaTeX users, by providing commands that
are similar to those used by the pLaTeX kernel and some other packages
used with it.

Note that while the CJK package supports many input encodings, this
package supports only UTF-8.

### System requirement

  * TeX format: LaTeX.
  * TeX engine: pdfTeX (DVI or PDF mode).
  * DVI driver: Anything. 
      - Non-default font settings require dvipdfmx or pdfTeX.
  * Dependent packages:
      - CJK, CJKutf8, CJKspace, CJKpunct, etoolbox; 
      - ipaex-type1 (when using default font mapping); 
      - zhmetrics (when using non-default font mapping).

### Installation

  - `*.sty` → $TEXMF/tex/latex/BXcjkjatype

### License

This package is distributed under the MIT License.

The bxcjkjatype Package
-----------------------

### Package Loading

    \usepackage[<option>,...]{bxcjkjatype}

The available options are described hereafter.

#### Options for auto-wrapping

These options enable one to wrap the document body with a `CJK(*)`
environemnt automatically and safely. They are suitable when a document
contains much amount of CJK text, or some “moving arguemnts” hold
CJK text.

  * `whole`, `wholeCJK*`: Wraps the whole document body with a `CJK*`
    environment (precisely speaking, with
    `\begin{uCJK*}` ... `\end{uCJK*}` ).
  * `wholeCJK`: Wraps the whole document body with a `CJK` environment
    (precisely speaking, with
    `\begin{uCJK}` ... `\end{uCJK}` ).
  * `nowhole` (default): Negation of `wholeCJK*` or `wholeCJK`.

#### Options for “auto-tilde”

The option `autotilde` triggers automatic invocation of `\CJKtilde`,
which makes a tilde character (`~`) insert “shibuaki”  (a thin space
between alphabetic and ideographic letters) rather than a no-break
space (standard). No-break spaces can still be inserted by the command
`\nbs`, and `\standardtilde` cancels the effect of `\CJKtilde`. (The
commands mentioned here belong to CJK package.)

  * `autotilde`: Makes `\CJKtilde` invoked at the beginning of every
    `CJK(*)` environemnt.
  * `noautotilde` (default): Negation of `autotilde`.

#### Options for font-mapping

One can use preset font mappings in the same way as in the [pxchfon
package]. Please refer to the manual of that package for detailed
explanation of this feature.

  * `oneweight`, `nooneweight`: The same as in pxchfon.
  * One can use font preset options (such as `ms`) which are available
    in pxchfon (except obsolete ones).
  * `ttfname=<pattern>`: Specifies the pattern of the TTF font names
    which are used when TTC substitution is employed. For example,
    when `ttfname=*_1` is given, the font “index 0 of mogam.ttc” will
    map to “mogam_1.ttf”, and similarly, “index 1” to “mogam_2.ttf”
    and so on.
  * `ipaex-type1`: Disables the font management of this package and
    directly uses the families provided by the ipaex-type1 package,
    namely `ipxm` and `ipxg`. In this setting the value of `\mcdefault`
    is `ipxm` and the value of `\gtdefault` and `\mgdefault` is `ipxg`,
    so that the higher level commands (such as `\sffamily` and
    `\gtfamily`) can work correctly.

[pxchfon package]: http://www.ctan.org/pkg/pxchfon

#### Options for CJK font scaling

  * `scale=<real>`: Sets the scaling factor for CJK fonts.

(With version 0.3 or later, one can employ the scaling even with the
`ipaex-type1` option.)

#### Other options

  * `everypage`: Outputs the font mapping information on every page of
    the resulted DVI document. Available only with `dvipdfmx` driver.
  * `noeverypage` (default): Negation of `everypage`.
  * driver options:
    `pdftex`, `dvipdfmx`, `dvips` and `none` are available. The driver
    setting is relevant only when using font mappings other than the
    default one (ipaex-type1 fonts), so one need not care of drivers
    in using default fonts. Moreover, non-default font mappings are
    supported only by `pdftex` and `dvipdfmx`, and these two values are
    auto-detected (`pdftex` is default in PDF mode and `dvipdfmx` in
    DVI mode). Thus one will never need to specify the driver.
  * `substmingoth`: Applies the substituion of families `min`, `goth`
    and `maru` (used conventionally for Japanese) with families `mc`,
    `gt` and `mg` (standard in this package).
  * `nosubstmingoth` (default): Negation of `substmingoth`.
  * `boldbyembolden` (default): Changes the implemention of `\CJKbold`
    (pseudo-bold) from “overstriking” to “synthetic emboldening”.
  * `noboldbyembolden`: Negation of `boldbyembolden`.

### Usage

#### Selecting CJK fonts

The present package provides three “generic” CJK families in the same
way as pLaTeX plus the [japanese-otf package]: Mincho family
(`\mcfamily`), Gothic family (`\gtfamily`), and Maru-gothic family
(`\mgfamily`). In default setting, the font set from the ipaex-type1
package are allocated; Mincho family uses IPAex Mincho font, and Gothic
and Maru-gothic families use IPAex Gothic font. This allocation can be
altered by users.

  * `\mcfamily`: Changes the CJK family to Mincho family. Equivalent
    to `\CJKfamily{\mcdefault}`.
  * `\gtfamily`: Changes the CJK family to Gothic family. Equivalent
    to `\CJKfamily{\gtdefault}`.
  * `\mgfamily`: Changes the CJK family to Maru-gothic family.
    Equivalent to `\CJKfamily{\mgdefault}`.

More advanced commands:

  * `\mcdefault`/`\gtdefault`/`\mgdefault`: The names of CJK families
    corresponding to the three generic families. In the standard
    allocation their values are `mc`/`gt`/`mg` respectively and the
    allocation is used as default.

  * `\setCJKfamilydefault{<CJK-family>}`: Declares the default CJK
    family. This default value is used when family names are missing
    in some commands, such as `\CJKfamily{}` and `\begin{CJK}{UTF8}{}`.
    The (redefined) `\normalfont` also switches the CJK family to the
    family specified by this command.

    The default value of this default family is the “counterpart” of
    the alphabetic font family which is in effect at the beginning of
    the document body. (See the next subsection.)

[japanese-otf package]: http://www.ctan.org/pkg/japanese-otf

#### Synchronization of CJK and non-CJK families

The CJK package (and pTeX engine) manages separate “current families”
for CJK and alphabetic (non-CJK) families. While this treatment has its
merit, synchronization of the two “current families” is convenient in
many cases. Accordingly, tHe present package redefines some of the
LaTeX commands that switches current alphabetic font families so that
the CJK family will be switched to the counterpart of the current
alphabetic family, where the “counterpart” is defined as follows:

  * `\rmfamily` (Serif) → `\mcfamily` (Mincho)
  * `\sffamily` (Sans-serif) → `\gtfamily` (Gothic)
  * `\ttfamily` (Monospace) → `\gtfamily` (Gothic)
  * The counterpart of the other families is `\mcfamily`.

Redefined commands:

  * `\rmfamily`/`\sffamily`/`\ttfamily`: Changes the CJK family to
    the counterpart of the alphabetic font family after executing the
    original function.
  * `\normalfont`: Changes the CJK family to the default CJK family
    specified by `\setCJKfamilydefault` command.

There are shorthand forms of `CJK`/`CJK*` environemnts:

  * `\begin{uCJK*}...\end{uCJK*}`: Equivalent to:

        \begin{CJK*}{UTF8}{counterpart}...\end{CJK*}

    where `counterpart` means the counterpart of the current alphabetic
    font family.

    Note that this is *not* equivalent to

        \begin{CJK*}{UTF8}{}...\end{CJK*}

    structure, which uses the default CJK family.

  * `\begin{uCJK}...\end{uCJK}`: Equivalent to:

        \begin{CJK}{UTF8}{counterpart}...\end{CJK}

#### Font mapping

The usage of these commands are the same as in the pxchfon package.
Please refer to the manual of that package for detail.

  * `\setminchofont[<id>]{<font-file>}`
  * `\setgothicfont[<id>]{<font-file>}`
  * `\setmarugothicfont[<id>]{<font-file>}`
  * `\setmediumminchofont[<id>]{<font-file>}`
  * `\setboldminchofont[<id>]{<font-file>}`
  * `\setmediumgothicfont[<id>]{<font-file>}`
  * `\setboldgothicfont[<id>]{<font-file>}`
  * `\setxboldgothicfont[<id>]{<font-file>}`

However there is a major limitation as to the use of font mapping with
the pdfTeX engine. One can use only TrueType fonts and moreover
TTC format is not allowed. (One can use any flavor of OpenType fonts
when using dvipdfmx.)

Note: The present package does not support the light-weight Mincho font,
and thus `\setlightminchofont` does nothing useful.

#### Other commands

  * `\UTF{<hexadecimal-number>}`: Inputs a CJK character through Unicode
    codepoint value. `\UTF{5B57}` is equivalent to `\Unicode{"5B}{"57}`.

  * `\CJKforce{<character>...}`: Afterwards Treats the characters given
    in the argument as CJK characters (printed using CJK fonts).

  * `\CJKunforce{<character>...}`: Cancels the effect of the `\CJKforce`
    command.

  * `\@<character>`: Treats the next character (only that occurrence)
    as a CJK character, when the character is outside ASCII; othersize
    the normal meaning of `\@` is retained.

  * `\CJKecglue`: Insers a “shibuaki” space. This will be invoked by
    `~` when `\CJKtilde` is in effect. This command can be redefined by
    users to adjust the value of shibuaki space, just as `\CJKglue` can
    be redefined to adjust inter-ideographic space.

    For example:

        \renewcommand{\CJKecglue}{\hspace{0.125em minus 0.125em}}

### Remarks

  * The standard font families provided by this package does *not*
    support vertical writing, even when using default ipaex-type1 font
    set. However, the families provided by ipaex-type1 (`ipxm` and
    `ipxg`) do support vertical writing, and one can utilize these
    families directly by specifying `ipaex-type1` option.

Revision History
----------------

  * Version 0.3  ‹2016/10/15›
      - Made the vertical writing work well (with CJKvert).
      - Avoided garbling of PDF strings created by hyperref.
      - Allowed font scaling even when `ipaex-type1` is set.
      - Added `boldbyembolden` feature.
      - Added `ttfname` option.
      - Added `substmingoth` option.

  * Version 0.2c ‹2013/10/18›
      - Added support of CJK font scaling.
      - Added `\CJKforce`, `\CJKunforce`, `\@`.

  * Version 0.2b ‹2013/09/28›
      - Added `\UTF`, `\CJKecglue`.

  * Version 0.2a ‹2013/08/08›
      - Added `autotilde` option.

  * Version 0.2  ‹2013/08/08›
      - The first public version.

--------------------
Takayuki YATO (aka. "ZR")  
http://zrbabbler.sp.land.to/
