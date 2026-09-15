# Xpdf, as bundled by pdfalto

**This is not the official Xpdf repository.** Xpdf is written and maintained by Derek Noonburg at
Glyph & Cog, LLC. The official source releases, documentation and support forum are at
<https://www.xpdfreader.com/> (downloads: <https://www.xpdfreader.com/download.html>). Please report
Xpdf bugs there, not here, unless they only appear in pdfalto.

This repository holds the Xpdf source tree used as a git submodule by
[pdfalto](https://github.com/kermitt2/pdfalto), a PDF-to-ALTO converter built on Xpdf's parsing and
text-extraction code. It is the unmodified upstream release tarball plus a small set of patches that
pdfalto needs. The upstream `README`, `CHANGES`, `COPYING` and `COPYING3` files are kept as shipped.

Current base: Xpdf 4.06 (2025-11-14). The previous base, Xpdf 4.05 with the same patches, is tagged
`xpdf-4.05-pdfalto`.

## What differs from upstream

- `xpdf/GlobalParams.{cc,h}`: a `GlobalParams(cfgFileName, executablePath)` constructor that resolves
  the resource files named in `xpdfrc` (`nameToUnicode`, `cidToUnicode`, `unicodeToUnicode`,
  `unicodeMap`, `cMapDir`, `toUnicodeDir`, `unicodeRemapping`, `fontFile`, `fontFileCC`) relative to
  the executable, so pdfalto can ship its `languages/` directory beside the binary;
  `mapNumericCharNames` off by default.
- `xpdf/CharCodeToUnicode.{cc,h}`: `makeUnicodeToUnicode()` and UTF-16 handling in `ToUnicode` CMaps.
- `xpdf/GfxFont.cc`: encoding and `ToUnicode` fallbacks for Type 3 fonts whose glyph names are
  arbitrary `CharProcs` keys.
- `xpdf/UnicodeToUnicodeFontRules.h`: added.
- `xpdf/Array.h`, `xpdf/Catalog.h`: include order.
- CMake (`CMakeLists.txt`, `cmake-config.txt`, `xpdf/CMakeLists.txt`, `xpdf-qt/CMakeLists.txt`): build
  a static `libxpdf`, skip the Qt viewer and its detection, libpaper handling.

Everything else is upstream Xpdf, under the licences in `COPYING` (GPL v2) and `COPYING3` (GPL v3).
