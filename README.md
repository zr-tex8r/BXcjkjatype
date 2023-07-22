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

This is the main package of this bundle.

Please refer to the user manual for detail.

  * bxcjkjatype.pdf: the user manual (in English)
  * bxcjkjatype-ja.pdf: the user manual (in Japanese)

The bxcjkvert Package
---------------------

Thia package is a tailored version of the CJKvert package,
accommodated for Japanese typesetting, where mixture of horizontal
and vertical writings is common.

Please refer to the user manual for detail.

  * bxcjkvert.pdf: the user manual (in English)
  * bxcjkvert-ja.pdf: the user manual (in Japanese)

Revision History
----------------

  * Version 0.5  ‹2023/07/23›
      - Adjustment for the recent LaTeX kernel.

  * Version 0.4  ‹2016/11/11›
      - Added bxcjkvert package.
      - Added `CJKtildeasspace` option.
      - (Experimental) Added `defaultmingoth` option.

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
https://github.com/zr-tex8r
