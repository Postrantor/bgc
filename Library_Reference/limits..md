---
tip: translate by openai@2023-07-20 18:30:59
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](iso646.html) \| [Contents](index.html) \| [Next](locale.html)
:::

------------------------------------------------------------------------

# [11]{.header-section-number} `<limits.h>` Numeric Limits {#limits number="11"}


Important note: the "minimum magnitude" in the table below is the minimum allowed by the spec. It's very likely that the values on your bad-ass system exceed those, below.

> 重要提示：下表中的“最小幅度”是按规范规定的最小值。很可能您的强大系统的值会超过下面的值。


  -------------------------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告
  Macro          Minimum Magnitude            Description

  -------------- ---------------------------- -----------------------------------------------------------------------------------------------------------

> -------------- ---------------------------- -----------------------------------------------------------------------------------------------------------
线条 -------------- ---------------------------- -----------------------------------------------------------------------------------------------------------
  `CHAR_BIT`     `8`                          Number of bits in a byte


  `SCHAR_MIN`    `-127`                       Minimum value of a `signed char`

> 最小值为有符号字符的SCHAR_MIN为-127


  `SCHAR_MAX`    `127`                        Maximum value of a `signed char`

> 最大的有符号字符的值为127


  `UCHAR_MAX`    `255`                        Maximum value of an `unsigned char`[^19^](footnotes.html#fn19){#fnref19 .footnote-ref role="doc-noteref"}

> 最大值的无符号字符为255

  `CHAR_MIN`     `0` or `SCHAR_MIN`           More detail below

  `CHAR_MAX`     `SCHAR_MAX` or `UCHAR_MAX`   More detail below


  `MB_LEN_MAX`   `1`                          Maximum number of bytes in a multibyte character on any locale

> `MB_LEN_MAX` 1 表示任何地区的多字节字符的最大字节数

  `SHRT_MIN`     `-32767`                     Minimum value of a `short`

  `SHRT_MAX`     `32767`                      Maximum value of a `short`


  `USHRT_MAX`    `65535`                      Maximum value of an `unsigned short`

> 无符号短整型的最大值为65535。

  `INT_MIN`      `-32767`                     Minimum vale of an `int`

  `INT_MAX`      `32767`                      Maximum value of an `int`


  `UINT_MAX`     `65535`                      Maximum value of an `unsigned int`

> `unsigned int`的最大值为65535。

  `LONG_MIN`     `-2147483647`                Minimum value of a `long`

  `LONG_MAX`     `2147483647`                 Maximum value of a `long`


  `ULONG_MAX`    `4294967295`                 Maximum value of an `unsigned long`

> 最大的无符号长整型值为4294967295。


  `LLONG_MIN`    `-9223372036854775807`       Minimum value of a `long long`

> 最小`long long`值为-9223372036854775807


  `LLONG_MAX`    `9223372036854775807`        Maximum value of a `long long`

> 最大的`long long`值为9223372036854775807


  `ULLONG_MAX`   `18446744073709551615`       Maximum value of an `unsigned long long`

> 无符号长整型的最大值为18446744073709551615。

  -------------------------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。

## [11.1]{.header-section-number} `CHAR_MIN` and `CHAR_MAX` {#char_min-and-char_max number="11.1"}


When it comes to the `CHAR_MIN` and `CHAR_MAX` macros, it all depends on if your `char` type is signed or unsigned by default. Remember that C leaves that up to the implementation? No? Well, it does.

> 当涉及到`CHAR_MIN`和`CHAR_MAX`宏时，这取决于你的`char`类型是默认情况下是有符号的还是无符号的。记住，C把这留给实现吗？不？嗯，它确实是这样。


So if it's signed, the values of `CHAR_MIN` and `CHAR_MAX` are the same as `SCHAR_MIN` and `SCHAR_MAX`.

> 如果签名了，`CHAR_MIN`和`CHAR_MAX`的值就和`SCHAR_MIN`和`SCHAR_MAX`的值相同。


And if it's unsigned, the values of `CHAR_MIN` and `CHAR_MAX` are the same as `0` and `UCHAR_MAX`.

> 如果是无符号的，`CHAR_MIN`和`CHAR_MAX`的值与`0`和`UCHAR_MAX`相同。


Side benefit: you can tell at runtime if the system has signed or unsigned chars by checking to see if `CHAR_MIN` is `0`.

> 附加好处：您可以通过检查CHAR_MIN是否为0来在运行时判断系统是有符号字符还是无符号字符。

::: {#cb229 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <limits.h>

int main(void)
{
    printf("chars are %ssigned\n", CHAR_MIN == 0? "un": "");
}
```
:::

On my system, `char`s are signed.

## [11.2]{.header-section-number} Choosing the Correct Type {#choosing-the-correct-type number="11.2"}


If you want to be super portable, choose a type you know will be at least as big as you need by the table, above.

> 如果你想要超级便携，选择一种你知道按照表格要求至少会有足够大小的类型。


That said, a lot of code, for better or (likely) worse, assumes `int`s are 32-bits, when in actuality it's only guaranteed to be 16.

> 话虽如此，很多代码，不管是好是坏，都假定`int`是32位的，而实际上只能保证是16位的。


If you need a guaranteed bit size, check out the `int_leastN_t` types in [`<stdint.h>`](stdint.html#stdint).

> 如果你需要一个保证的位大小，请查看[`<stdint.h>`](stdint.html#stdint)中的`int_leastN_t`类型。

## [11.3]{.header-section-number} Whither Two's Complement? {#whither-twos-complement number="11.3"}


If you were looking closely and have *a priori* knowledge of the matter, you might have thought I erred in the minimum values of the macros, above.

> 如果你仔细观察并且具有先验知识，你可能会认为我在上面的宏的最小值中犯了错误。

"`short` goes from `32767` to `-32767`? Shouldn't it go to `-32768?`"


No, I have it right. The spec list the minimum magnitudes for those macros, and some old-timey systems might have used a different encoding for their signed values that could only go that far.

> 不，我搞对了。规格列出了这些宏的最小值，一些老式系统可能使用不同的编码来表示有符号值，而且只能达到那么远。


Virtually every modern system uses [Two's Complement](https://en.wikipedia.org/wiki/Two%27s_complement)[^20^](footnotes.html#fn20){#fnref20 .footnote-ref role="doc-noteref"} for signed numbers, and those would go from `32767` to `-32768` for a `short`. Your system probably does, too.

> 几乎所有现代系统都使用[二进制补码](https://zh.wikipedia.org/wiki/%E4%BA%8C%E8%BF%9B%E5%88%B6%E8%A1%A5%E7%A0%81)[^20^](footnotes.html#fn20){#fnref20 .footnote-ref role="doc-noteref"}来表示有符号数，对于`short`类型来说，数值范围从`32767`到`-32768`。你的系统可能也是这样。

## [11.4]{.header-section-number} Demo Program {#demo-program number="11.4"}

Here's a program to print out the values of the macros:

::: {#cb230 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <limits.h>

int main(void)
{
    printf("CHAR_BIT = %d\n", CHAR_BIT);
    printf("SCHAR_MIN = %d\n", SCHAR_MIN);
    printf("SCHAR_MAX = %d\n", SCHAR_MAX);
    printf("UCHAR_MAX = %d\n", UCHAR_MAX);
    printf("CHAR_MIN = %d\n", CHAR_MIN);
    printf("CHAR_MAX = %d\n", CHAR_MAX);
    printf("MB_LEN_MAX = %d\n", MB_LEN_MAX);
    printf("SHRT_MIN = %d\n", SHRT_MIN);
    printf("SHRT_MAX = %d\n", SHRT_MAX);
    printf("USHRT_MAX = %u\n", USHRT_MAX);
    printf("INT_MIN = %d\n", INT_MIN);
    printf("INT_MAX = %d\n", INT_MAX);
    printf("UINT_MAX = %u\n", UINT_MAX);
    printf("LONG_MIN = %ld\n", LONG_MIN);
    printf("LONG_MAX = %ld\n", LONG_MAX);
    printf("ULONG_MAX = %lu\n", ULONG_MAX);
    printf("LLONG_MIN = %lld\n", LLONG_MIN);
    printf("LLONG_MAX = %lld\n", LLONG_MAX);
    printf("ULLONG_MAX = %llu\n", ULLONG_MAX);
}
```
:::

On my 64-bit Intel system with clang, this outputs:

::: {#cb231 .sourceCode}
``` {.sourceCode .default}
CHAR_BIT = 8
SCHAR_MIN = -128
SCHAR_MAX = 127
UCHAR_MAX = 255
CHAR_MIN = -128
CHAR_MAX = 127
MB_LEN_MAX = 6
SHRT_MIN = -32768
SHRT_MAX = 32767
USHRT_MAX = 65535
INT_MIN = -2147483648
INT_MAX = 2147483647
UINT_MAX = 4294967295
LONG_MIN = -9223372036854775808
LONG_MAX = 9223372036854775807
ULONG_MAX = 18446744073709551615
LLONG_MIN = -9223372036854775808
LLONG_MAX = 9223372036854775807
ULLONG_MAX = 18446744073709551615
```
:::


Looks like my system probably uses two's-complement encoding for signed numbers, my `char`s are signed, and my `int`s are 32-bit.

> 看起来我的系统可能使用二进制补码编码来表示有符号数，我的`char`是有符号的，而我的`int`是32位的。

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](iso646.html) \| [Contents](index.html) \| [Next](locale.html)
:::
