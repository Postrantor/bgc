---
tip: translate by openai@2023-07-20 19:26:56
...
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

> 这个头文件让我们访问固定位数的类型，或者至少是至少有那么多位的类型。

It also gives us handy macros to use.

## [21.1]{.header-section-number} Specific-Width Integers {#specific-width-integers number="21.1"}

There are three main classes of types defined here, signed and unsigned:

-   Integers of exactly a certain size (`int`*N*`_t`, `uint`*N*`_t`)
-   Integers that are at least a certain size (`int_least`*N*`_t`, `uint_least`*N*`_t`)

-   Integers that are at least a certain size and are as fast as possible (`int_fast`*N*`_t`, `uint_fast`*N*`_t`)

> 整数至少要达到一定大小，并且尽可能快（`int_fast`*N*`_t`，`uint_fast`*N*`_t`）


Where the *N* occurs, you substitute the number of bits, commonly multiples of 8, e.g. `uint16_t`.

> 在*N*出现的地方，你可以用常见的8的倍数的位数来替换，例如`uint16_t`。

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

> 其他的都是可选的，但是当系统拥有这些大小的整数，没有填充，并且使用二进制补码表示法时，你很可能也会有以下内容，这是Mac和PC以及其他许多系统的情况。简而言之，你很可能有这些：

::: {#cb483 .sourceCode}
``` {.sourceCode .c}
int8_t      uint8_t
int16_t     uint16_t
int32_t     uint32_t
int64_t     uint64_t
```
:::


Other numbers of bits can also be supported by an implementation if it wants to go all crazy with it.

> 也可以支持其他位数，如果实现想要疯狂地进行的话。

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

> 有几种可选的类型是能够容纳指针类型的整数。

::: {#cb485 .sourceCode}
``` {.sourceCode .c}
intptr_t
uintptr_t
```
:::


You can convert a `void*` to one of these types, and back again. And the `void*`s will compare equal.

> 你可以把一个`void*`转换成其中的一种类型，也可以再转回来。而且`void*`会相等。


The use case is any place you need an integer that represents a pointer for some reason.

> 使用案例是任何需要用整数表示指针的地方。


Also, there are a couple types that are just there to be the biggest possible integers your system supports:

> 此外，还有一些类型只是为了成为您的系统支持的最大整数。

::: {#cb486 .sourceCode}
``` {.sourceCode .c}
intmax_t
uintmax_t
```
:::


Fun fact: you can print these types with the `"%jd"` and `"%ju"` [`printf()`](stdio.html#man-printf) format specifiers.

> 事实上有趣的是，你可以使用“%jd”和“%ju”[`printf（）`](stdio.html#man-printf)格式说明符来打印这些类型。


There are also a bunch of macros in `<inttypes.h>`(#inttypes) that you can use to print any of the types mentioned, above.

> 在<inttypes.h>（#inttypes）中也有一堆宏，你可以用它们来打印上面提到的任何类型。

## [21.3]{.header-section-number} Macros {#macros-2 number="21.3"}


The following macros define the minimum and maximum values for these types:

> 以下宏定义了这些类型的最小值和最大值：

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

> 对于精确位大小的有符号类型，最小值正好是[\(-(2\^{N-1}) \)]{.math .inline}，最大值正好是[\(2\^{N-1}-1 \)]{.math .inline}。对于精确位大小的无符号类型，最大值正好是[\(2\^N-1 \)]{.math .inline}。


For the signed "least" and "fast" variants, the magnitude and sign of the minimum is at least [\\(-(2\^{N-1}-1)\\)]{.math .inline} and the maximum is at least [\\(2\^{N-1}-1\\)]{.math .inline}. And for unsigned it's at least [\\(2\^N-1\\)]{.math .inline}.

> 对于签名的“最小”和“快速”变体，最小值的大小和符号至少为[\\(-(2\^{N-1}-1)\\)]{.math .inline}，最大值至少为[\\(2\^{N-1}-1\\)]{.math .inline}。对于无符号数，最小值至少为[\\(2\^N-1\\)]{.math .inline}。

`INTMAX_MAX` is at least [\\(2\^{63}-1\\)]{.math .inline}, `INTMAX_MIN` is at least [\\(-(2\^{63}-1)\\)]{.math .inline} in sign and magnitude. And `UINTMAX_MAX` is at least [\\(2\^{64}-1\\)]{.math .inline}.


Finally, `INTPTR_MAX` is at least [\\(2\^{15}-1\\)]{.math .inline}, `INTPTR_MIN` is at least [\\(-(2\^{15}-1)\\)]{.math .inline} in sign and magnitude. And `UINTPTR_MAX` is at least [\\(2\^{16}-1\\)]{.math .inline}.

> 最后，`INTPTR_MAX`至少为[\(2\^{15}-1\)]{.math .inline}，`INTPTR_MIN`至少为[\(-(2\^{15}-1)\)]{.math .inline}，符号和大小都相同。`UINTPTR_MAX`至少为[\(2\^{16}-1\)]{.math .inline}。

## [21.4]{.header-section-number} Other Limits {#other-limits number="21.4"}


There are a bunch of types in `<inttypes.h>`(#inttypes) that have their limits defined here. (`<inttypes.h>` includes `<stdint.h>`.)

> 在<inttypes.h>（#inttypes）中有许多类型，它们的限制在这里定义。（<inttypes.h>包括<stdint.h>。）

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

> 规格说，`PTRDIFF_MIN`的大小至少为-65535，而`PTRDIFF_MAX`和`SIZE_MAX`的大小至少为65535。

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

> 你可以使用宏`INT`*N*`_C()`和`UINT`*N*`()`，其中*N*可以是`8`、`16`、`32`或`64`。

::: {#cb489 .sourceCode}
``` {.sourceCode .c}
uint_least16_t x = INT16_C(3490);
uint_least64_t y = INT64_C(1122334455);
```
:::


A variant on these is `INTMAX_C()` and `UINTMAX_C()`. They will make a constant suitable for storing in an `intmax_t` or `uintmax_t`.

> 这些的变体是`INTMAX_C()`和`UINTMAX_C()`。它们可以创建一个适合存储在`intmax_t`或`uintmax_t`中的常量。

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
