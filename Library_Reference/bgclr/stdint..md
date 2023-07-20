---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stddef.html) \| [Contents](index.html) \| [Next](stdio.html)
:::

------------------------------------------------------------------------

# [21]{.header-section-number} `<stdint.h>` More Integer Types {#stdint number="21"}

This header gives us access to (potentially) types of a fixed number of bits, or, at the very least, types that are at least that many bits.

It also gives us handy macros to use.

## [21.1]{.header-section-number} Specific-Width Integers {#specific-width-integers number="21.1"}

There are three main classes of types defined here, signed and unsigned:

-   Integers of exactly a certain size (`int`*N*`_t`, `uint`*N*`_t`)
-   Integers that are at least a certain size (`int_least`*N*`_t`, `uint_least`*N*`_t`)
-   Integers that are at least a certain size and are as fast as possible (`int_fast`*N*`_t`, `uint_fast`*N*`_t`)

Where the *N* occurs, you substitute the number of bits, commonly multiples of 8, e.g. `uint16_t`.

The following types are guaranteed to be defined:

::: {#cb482 .sourceCode}
``` {.sourceCode .c}
int_least8_t      uint_least8_t
int_least16_t     uint_least16_t
int_least32_t     uint_least32_t
int_least64_t     uint_least64_t

int_fast8_t       uint_fast8_t
int_fast16_t      uint_fast16_t
int_fast32_t      uint_fast32_t
int_fast64_t      uint_fast64_t
```
:::

Everything else is optional, but you'll probably also have the following, which are required when a system has integers of these sizes with no padding and two's-complement representation... which is the case for Macs and PCs and a lot of other systems. In short, you very likely have these:

::: {#cb483 .sourceCode}
``` {.sourceCode .c}
int8_t      uint8_t
int16_t     uint16_t
int32_t     uint32_t
int64_t     uint64_t
```
:::

Other numbers of bits can also be supported by an implementation if it wants to go all crazy with it.

Examples:

::: {#cb484 .sourceCode}
``` {.sourceCode .c}
#include <stdint.h>

int main(void)
{
    int16_t x = 32;
    int_fast32_t y = 3490;

    // ...
```
:::

## [21.2]{.header-section-number} Other Integer Types {#other-integer-types number="21.2"}

There are a couple optional types that are integers capable of holding pointer types.

::: {#cb485 .sourceCode}
``` {.sourceCode .c}
intptr_t
uintptr_t
```
:::

You can convert a `void*` to one of these types, and back again. And the `void*`s will compare equal.

The use case is any place you need an integer that represents a pointer for some reason.

Also, there are a couple types that are just there to be the biggest possible integers your system supports:

::: {#cb486 .sourceCode}
``` {.sourceCode .c}
intmax_t
uintmax_t
```
:::

Fun fact: you can print these types with the `"%jd"` and `"%ju"` [`printf()`](stdio.html#man-printf) format specifiers.

There are also a bunch of macros in `<inttypes.h>`(#inttypes) that you can use to print any of the types mentioned, above.

## [21.3]{.header-section-number} Macros {#macros-2 number="21.3"}

The following macros define the minimum and maximum values for these types:

::: {#cb487 .sourceCode}
``` {.sourceCode .c}
INT8_MAX           INT8_MIN           UINT8_MAX
INT16_MAX          INT16_MIN          UINT16_MAX
INT32_MAX          INT32_MIN          UINT32_MAX
INT64_MAX          INT64_MIN          UINT64_MAX

INT_LEAST8_MAX     INT_LEAST8_MIN     UINT_LEAST8_MAX
INT_LEAST16_MAX    INT_LEAST16_MIN    UINT_LEAST16_MAX
INT_LEAST32_MAX    INT_LEAST32_MIN    UINT_LEAST32_MAX
INT_LEAST64_MAX    INT_LEAST64_MIN    UINT_LEAST64_MAX

INT_FAST8_MAX      INT_FAST8_MIN      UINT_FAST8_MAX
INT_FAST16_MAX     INT_FAST16_MIN     UINT_FAST16_MAX
INT_FAST32_MAX     INT_FAST32_MIN     UINT_FAST32_MAX
INT_FAST64_MAX     INT_FAST64_MIN     UINT_FAST64_MAX

INTMAX_MAX         INTMAX_MIN         UINTMAX_MAX

INTPTR_MAX         INTPTR_MIN         UINTPTR_MAX
```
:::

For the exact-bit-size signed types, the minimum is exactly [\\(-(2\^{N-1})\\)]{.math .inline} and the maximum is exactly [\\(2\^{N-1}-1\\)]{.math .inline}. And for the exact-bit-size unsigned types, the max is exactly [\\(2\^N-1\\)]{.math .inline}.

For the signed "least" and "fast" variants, the magnitude and sign of the minimum is at least [\\(-(2\^{N-1}-1)\\)]{.math .inline} and the maximum is at least [\\(2\^{N-1}-1\\)]{.math .inline}. And for unsigned it's at least [\\(2\^N-1\\)]{.math .inline}.

`INTMAX_MAX` is at least [\\(2\^{63}-1\\)]{.math .inline}, `INTMAX_MIN` is at least [\\(-(2\^{63}-1)\\)]{.math .inline} in sign and magnitude. And `UINTMAX_MAX` is at least [\\(2\^{64}-1\\)]{.math .inline}.

Finally, `INTPTR_MAX` is at least [\\(2\^{15}-1\\)]{.math .inline}, `INTPTR_MIN` is at least [\\(-(2\^{15}-1)\\)]{.math .inline} in sign and magnitude. And `UINTPTR_MAX` is at least [\\(2\^{16}-1\\)]{.math .inline}.

## [21.4]{.header-section-number} Other Limits {#other-limits number="21.4"}

There are a bunch of types in `<inttypes.h>`(#inttypes) that have their limits defined here. (`<inttypes.h>` includes `<stdint.h>`.)

  -----------------------------------------------------------------------
  Macro                               Description
  ----------------------------------- -----------------------------------
  `PTRDIFF_MIN`                       Minimum `ptrdiff_t` value

  `PTRDIFF_MAX`                       Maximum `ptrdiff_t` value

  `SIG_ATOMIC_MIN`                    Minimum `sig_atomic_t` value

  `SIG_ATOMIC_MAX`                    Maximum `sig_atomic_t` value

  `SIZE_MAX`                          Maximum `size_t` value

  `WCHAR_MIN`                         Minimum `wchar_t` value

  `WCHAR_MAX`                         Maximum `wchar_t` value

  `WINT_MIN`                          Minimum `wint_t` value

  `WINT_MAX`                          Maximum `wint_t` value
  -----------------------------------------------------------------------

The spec says that `PTRDIFF_MIN` will be at least -65535 in magnitude. And `PTRDIFF_MAX` and `SIZE_MAX` will be at least 65535.

`SIG_ATOMIC_MIN` and `MAX` will be either -127 and 127 (if it's signed) or 0 and 255 (if it's unsigned).

Same for `WCHAR_MIN` and `MAX`.

`WINT_MIN` and `MAX` will be either -32767 and 32767 (if it's signed) or 0 and 65535 (if it's unsigned).

## [21.5]{.header-section-number} Macros for Declaring Constants {#macros-for-declaring-constants number="21.5"}

If you recall, you can specify a type for integer constants:

::: {#cb488 .sourceCode}
``` {.sourceCode .c}
int x = 12;
long int y = 12L;
unsigned long long int z = 12ULL;
```
:::

You can use the macros `INT`*N*`_C()` and `UINT`*N*`()` where *N* is `8`, `16`, `32` or `64`.

::: {#cb489 .sourceCode}
``` {.sourceCode .c}
uint_least16_t x = INT16_C(3490);
uint_least64_t y = INT64_C(1122334455);
```
:::

A variant on these is `INTMAX_C()` and `UINTMAX_C()`. They will make a constant suitable for storing in an `intmax_t` or `uintmax_t`.

::: {#cb490 .sourceCode}
``` {.sourceCode .c}
intmax_t x = INTMAX_C(3490);
uintmax_t x = UINTMAX_C(1122334455);
```
:::

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stddef.html) \| [Contents](index.html) \| [Next](stdio.html)
:::
