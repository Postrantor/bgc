---
tip: translate by openai@2023-07-21 12:29:24
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdio.html) \| [Contents](index.html) \| [Next](stdnoreturn.html)
:::

------------------------------------------------------------------------

# [23]{.header-section-number} `<stdlib.h>` Standard Library Functions {#stdlib number="23"}


Some of the following functions have variants that handle different types: `atoi()`, `strtod()`, `strtol()`, `abs()`, and `div()`. Only a single one is listed here for brevity.

> 以下函数中有一些有多种版本，可以处理不同类型的数据：`atoi()`、`strtod()`、`strtol()`、`abs()`和`div()`，为了简洁起见，只列出了一个。


  -------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------
简化中文
  Function                                             Description

  ---------------------------------------------------- --------------------------------------------------------

> ---------------------------------------------------------- ----------------------------------------------------------
简体中文：
---------------------------------------------------------- ----------------------------------------------------------

  [`_Exit()`](stdlib.html#man-exit)                    Exit the currently-running program and don't look back

> [`_Exit()`](stdlib.html#man-exit) 退出当前正在运行的程序，不要再回头看


  [`abort()`](stdlib.html#man-abort)                   Abruptly end program execution

> [`abort()`](stdlib.html#man-abort) 意外终止程序执行


  [`abs()`](stdlib.html#man-abs)                       Compute the absolute value of an integer

> `abs()`（stdlib.html#man-abs）计算整数的绝对值


  [`aligned_alloc()`](stdlib.html#man-aligned_alloc)   Allocate specifically-aligned memory

> 分配特定对齐的内存


  [`at_quick_exit()`](stdlib.html#man-atexit)          Set up handlers to run when the program quickly exits

> 调用`at_quick_exit()`函数可以设置程序快速退出时运行的处理程序。


  [`atexit()`](stdlib.html#man-atexit)                 Set up handlers to run when the program exits

> 设置程序退出时运行的处理程序，使用atexit()


  [`atof()`](stdlib.html#man-atof)                     Convert a string to a floating point value

> [`atof()`](stdlib.html#man-atof) 将字符串转换为浮点值


  [`atoi()`](stdlib.html#man-atoi)                     Convert an integer in a string into a integer type

> [`atoi()`](stdlib.html#man-atoi) 将字符串中的整数转换为整数类型


  [`bsearch()`](stdlib.html#man-bsearch)               Binary Search (maybe) an array of objects

> `bsearch()`：二分搜索（可能）一个对象数组


  [`calloc()`](stdlib.html#man-malloc)                 Allocate and clear memory for arbitrary use

> `calloc()`分配和清除用于任意用途的内存


  [`div()`](stdlib.html#man-div)                       Compute the quotient and remainder of two numbers

> [`div()`](stdlib.html#man-div)：计算两个数字的商和余数


  [`exit()`](stdlib.html#man-exit)                     Exit the currently-running program

> [`exit()`](stdlib.html#man-exit)： 退出当前正在运行的程序


  [`free()`](stdlib.html#man-free)                     Free a memory region

> [`free()`](stdlib.html#man-free)：释放一个内存区域


  [`getenv()`](stdlib.html#man-getenv)                 Get the value of an environment variable

> `getenv()`（stdlib.html#man-getenv）获取环境变量的值


  [`malloc()`](man-malloc)                             Allocate memory for arbitrary use

> 分配内存供任意使用（malloc()）


  [`mblen()`](stdlib.html#man-mblen)                   Return the number of bytes in a multibyte character

> `mblen()`函数返回多字节字符的字节数


  [`mbstowcs()`](stdlib.html#man-mbstowcs)             Convert a multibyte string to a wide character string

> mbstowcs() 将多字节字符串转换为宽字符串


  [`mbtowc()`](stdlib.html#man-mbtowc)                 Convert a multibyte character to a wide character

> mbtowc()（stdlib.html#man-mbtowc）将多字节字符转换为宽字符


  [`qsort()`](stdlib.html#man-qsort)                   Quicksort (maybe) some data

> 对数据进行快速排序（可能），[`qsort()`](stdlib.html#man-qsort)


  [`quick_exit()`](stdlib.html#man-exit)               Exit the currently-running program quickly

> 快速退出（`quick_exit()`）（参见stdlib.html#man-exit）：快速退出当前正在运行的程序


  [`rand()`](stdlib.html#man-rand)                     Return a pseudorandom number

> 返回一个伪随机数


  [`realloc()`](stdlib.html#man-realloc)               Resize a previously allocated stretch of memory

> `realloc()`（[stdlib.html#man-realloc](stdlib.html#man-realloc)）：调整先前分配的内存块的大小。


  [`srand()`](stdlib.html#man-srand)                   Seed the built-in pseudorandom number generator

> `srand()`函数用于种植内置的伪随机数发生器。


  [`strtod()`](stdlib.html#man-strtod)                 Convert a string to a floating point number

> `strtod()`（stdlib.html#man-strtod）将字符串转换为浮点数


  [`strtol()`](stdlib.html#man-strtol)                 Convert a string to an integer

> `strtol()`（[stdlib.html#man-strtol](stdlib.html#man-strtol)）将字符串转换为整数


  [`system()`](stdlib.html#man-system)                 Run an external program

> [`system()`](stdlib.html#man-system)：运行外部程序


  [`wcstombs()`](stdlib.html#man-wcstombs)             Convert a wide character string to a multibyte string

> `wcstombs()` 将宽字符串转换为多字节字符串。


  [`wctomb()`](stdlib.html#man-wctomb)                 Convert a wide character to a multibyte character

> `wctomb()` 将宽字符转换为多字节字符

  -------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------
简化中文


The `<stdlib.h>` header has all kinds of---dare I say---miscellaneous functions bundled into it. This functionality includes:

> <stdlib.h>头文件中包含各种（敢说）杂项功能。这些功能包括：

-   Conversions from numbers to strings
-   Conversions from strings to numbers
-   Pseudorandom number generation
-   Dynamic memory allocation
-   Various ways to exit the program
-   Ability to run external programs
-   Binary search (or some fast search)
-   Quicksort (or some fast sort)
-   Integer arithmetic functions
-   Multibyte and wide character and string conversions

So, you know... a little of everything.

## [23.1]{.header-section-number} `<stdlib.h>` Types and Macros {#stdlib.h-types-and-macros number="23.1"}


A couple new types and macros are introduced, though some of these might also be defined elsewhere:

> 新的几种类型和宏被引入，尽管其中一些可能也在其他地方定义：

  -------------------------------------------------------------------------------
  Type                                Description
  ----------------------------------- -------------------------------------------

  `size_t`                            Returned from `sizeof` and used elsewhere

> `size_t` 是由 `sizeof` 返回并在其他地方使用的类型。

  `wchar_t`                           For wide character operations

  `div_t`                             For the `div()` function

  `ldiv_t`                            For the `ldiv()` function

  `lldiv_t`                           for the `lldiv()` function
  -------------------------------------------------------------------------------

And some macros:


  ------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------
简化中文
  Type                                Description

  ----------------------------------- ------------------------------------------------------------------------

> ----------------------------------- ------------------------------------------------------------------------
简体中文：
----------------------------------- ------------------------------------------------------------------------
  `NULL`                              Our good pointer friend


  `EXIT_SUCCESS`                      Good exit status when things go well

> 退出成功，事情进展顺利时的良好退出状态


  `EXIT_FAILURE`                      Good exit status when things go poorly

> 退出失败


  `RAND_MAX`                          The maximum value that can be returned by the `rand()` function

> `rand()`函数可以返回的最大值为`RAND_MAX`。


  `MB_CUR_MAX`                        Maximum number of bytes in a multibyte character in the current locale

> MB_CUR_MAX：当前区域设置中多字节字符的最大字节数

  ------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。


And there you have it. Just a lot of fun, useful functions in here. Let's check 'em out!

> 那就是它了。这里有很多有趣的、有用的功能。让我们一起来看看吧！

------------------------------------------------------------------------

## [23.2]{.header-section-number} `atof()` {#man-atof number="23.2"}

Convert a string to a floating point value

### Synopsis {#synopsis-160 .unnumbered .unlisted}

::: {#cb571 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

double atof(const char *nptr);
```
:::

### Description {#description-160 .unnumbered .unlisted}


This stood for ["ASCII-To-Floating" back in the day](http://man.cat-v.org/unix-1st/3/atof)[^50^](footnotes.html#fn50){#fnref50 .footnote-ref role="doc-noteref"}, but no one would dare to use such coarse language now.

> 这在当时代表"ASCII-To-Floating"，但现在没人敢用这么粗鲁的语言了。


But the gist is the same: we're going to convert a string with numbers and (optionally) a decimal point into a floating point value. Leading whitespace is ignored, and translation stops at the first invalid character.

> 但大意是一样的：我们将把一个带有数字和（可选）小数点的字符串转换为浮点值。忽略前导空格，并在第一个无效字符处停止翻译。

If the result doesn't fit in a `double`, behavior is undefined.


It generally works as if you'd called [`strtod()`](stdlib.html#man-strtod):

> 它通常的工作方式就好像你调用了strtod()一样。

::: {#cb572 .sourceCode}
``` {.sourceCode .c}
strtod(nptr, NULL)
```
:::

So check out [that reference page](stdlib.html#man-strtod) for more info.

In fact, `strtod()` is just better and you should probably use that.

### Return Value {#return-value-158 .unnumbered .unlisted}

Returns the string converted to a `double`.

### Example {#example-161 .unnumbered .unlisted}

::: {#cb573 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    double x = atof("3.141593");

    printf("%f\n", x);  // 3.141593
}
```
:::

### See Also {#see-also-152 .unnumbered .unlisted}

[`atoi()`](stdlib.html#man-atoi), [`strtod()`](stdlib.html#man-strtod)

------------------------------------------------------------------------

## [23.3]{.header-section-number} `atoi()`, `atol()`, `atoll()` {#man-atoi number="23.3"}

Convert an integer in a string into a integer type

### Synopsis {#synopsis-161 .unnumbered .unlisted}

::: {#cb574 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int atoi(const char *nptr);

long int atol(const char *nptr);

long long int atoll(const char *nptr);
```
:::

### Description {#description-161 .unnumbered .unlisted}


Back in the day, `atoi()` stood for ["ASCII-To_Integer"](http://man.cat-v.org/unix-1st/3/atoi)[^51^](footnotes.html#fn51){#fnref51 .footnote-ref role="doc-noteref"} but now the spec makes no mention of that.

> 回到那个时候，`atoi（）`代表[“ASCII-To_Integer”]（http://man.cat-v.org/unix-1st/3/atoi）[^51^]（footnotes.html#fn51）{#fnref51 .footnote-ref role =“doc-noteref”}，但现在规范中没有提到这一点。


These functions take a string with a number in them and convert it to an integer of the specified return type. Leading whitespace is ignored. Translation stops at the first invalid character.

> 这些函数接受一个带有数字的字符串，并将其转换为指定返回类型的整数。忽略前导空格。翻译在第一个无效字符处停止。

If the result doesn't fit in the return type, behavior is undefined.


It generally works as if you'd called [`strtol()`](stdlib.html#man-strtol) family of functions:

> 它通常的工作方式就像你调用strtol()函数系列一样。

::: {#cb575 .sourceCode}
``` {.sourceCode .c}
atoi(nptr)                 // is basically the same as...
(int)strtol(nptr, NULL, 10)

atol(nptr)                 // is basically the same as...
strtol(nptr, NULL, 10)

atoll(nptr)                // is basically the same as...
strtoll(nptr, NULL, 10)
```
:::


Again, the [`strtol()`](stdlib.html#man-strtol) functions are generally better, so I recommend them instead of these.

> 再次，[`strtol()`](stdlib.html#man-strtol)函数通常更好，因此我推荐它们而不是这些。

### Return Value {#return-value-159 .unnumbered .unlisted}

Returns an integer result corresponding to the return type.

### Example {#example-162 .unnumbered .unlisted}

::: {#cb576 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int x = atoi("3490");

    printf("%d\n", x);  // 3490
}
```
:::

### See Also {#see-also-153 .unnumbered .unlisted}

[`atof()`](stdlib.html#man-atof), [`strtol()`](stdlib.html#man-strtol)

------------------------------------------------------------------------

## [23.4]{.header-section-number} `strtod()`, `strtof()`, `strtold()` {#man-strtod number="23.4"}

Convert a string to a floating point number

### Synopsis {#synopsis-162 .unnumbered .unlisted}

::: {#cb577 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

double strtod(const char * restrict nptr, char ** restrict endptr);

float strtof(const char * restrict nptr, char ** restrict endptr);

long double strtold(const char * restrict nptr, char ** restrict endptr);
```
:::

### Description {#description-162 .unnumbered .unlisted}


These are some neat functions that convert strings to floating point numbers (or even NaN or Infinity) and provide some error checking, besides.

> 这些是一些很棒的函数，可以将字符串转换为浮点数（甚至是NaN或Infinity），并且提供一些错误检查。

Firstly, leading whitespace is skipped.


Then the functions attempt to convert characters into the floating point result. Finally, when an invalid character (or NUL character) is reached, they set `endptr` to point to the invalid character.

> 然后，函数试图将字符转换为浮点结果。最后，当遇到无效字符（或NUL字符）时，它们将`endptr`指向无效字符。


Set `endptr` to `NULL` if you don't care about where the first invalid character is.

> 如果你不关心第一个无效字符在哪里，请将`endptr`设置为`NULL`。


If you didn't set `endptr` to `NULL`, it will point to a NUL character if the translation didn't find any bad characters. That is:

> 如果您没有将`endptr`设置为`NULL`，则如果翻译没有发现任何不良字符，它将指向NUL字符。也就是说：

::: {#cb578 .sourceCode}
``` {.sourceCode .c}
if (*endptr == '\0') {
    printf("What a perfectly-formed number!\n");
} else {
    printf("I found badness in your number: \"%s\"\n", endptr);
}
```
:::


But guess what! You can also translate strings into special values, like NaN and Infinity!

> 哎呀！你知道吗？你还可以把字符串翻译成特殊值，比如NaN和Infinity！


If `nptr` points to a string containing `INF` or `INFINITY` (upper or lowercase), the value for Infinity will be returned.

> 如果nptr指向一个包含INF或INFINITY（大写或小写）的字符串，将返回无穷大的值。


If `nptr` points to a string containing `NAN`, then (a quiet, non-signalling) NaN will be returned. You can tag the `NAN` with a sequence of characters from the set `0`-`9`, `a`-`z`, `A`-`Z`, and `_` by enclosing them in parens:

> 如果nptr指向一个包含NAN的字符串，那么将返回一个静默的、非信号的NaN。您可以使用从0-9、a-z、A-Z和_中的一系列字符将NAN用括号括起来：

::: {#cb579 .sourceCode}
``` {.sourceCode .c}
NAN(foobar_3490)
```
:::


What your compiler does with this is implementation-defined, but it can be used to specify different kinds of NaN.

> 你的编译器如何处理这个是由实现定义的，但它可以用来指定不同类型的NaN。


You can also specify a number in hexadecimal with a power-of-two exponent ([\\(2\^x\\)]{.math .inline}) if you lead with `0x` (or `0X`). For the exponent, use a `p` followed by a base 10 exponent. (You can't use `e` because that's a valid hex digit!)

> 你也可以用以2为底的指数([\(2\^x\)]{.math .inline})来指定十六进制数，只需在前面加上`0x`（或`0X`）。指数采用`p`加以10为底的指数（不能使用`e`，因为它是一个有效的十六进制数字！）。

Example:

::: {#cb580 .sourceCode}
``` {.sourceCode .c}
0xabc.123p15
```
:::

Which computes to [\\(0xabc.123\\times2\^{15}\\)]{.math .inline}.


You can put in `FLT_DECIMAL_DIG`, `DBL_DECIMAL_DIG`, or `LDBL_DECIMAL_DIG` digits and get a correctly-rounded result for the type.

> 你可以在FLT_DECIMAL_DIG、DBL_DECIMAL_DIG或LDBL_DECIMAL_DIG中输入数字，并且能够获得正确舍入的结果。

### Return Value {#return-value-160 .unnumbered .unlisted}


Returns the converted number. If there was no number, returns `0`. `endptr` is set to point to the first invalid character, or the NUL terminator if all characters were consumed.

> 返回转换后的数字。如果没有数字，则返回`0`。`endptr`被设置为指向第一个无效字符或NUL终止符（如果所有字符都被消耗）。


If there's an overflow, `HUGE_VAL`, `HUGE_VALF`, or `HUGE_VALL` is returned, signed like the input, and `errno` is set to `ERANGE`.

> 如果发生溢出，将返回HUGE_VAL、HUGE_VALF或HUGE_VALL，其符号与输入相同，并将errno设置为ERANGE。


If there's an underflow, it returns the smallest number closest to zero with the input sign. `errno` may be set to `ERANGE`.

> 如果发生溢出，它将返回与输入符号最接近零的最小数字。 `errno`可能被设置为`ERANGE`。

### Example {#example-163 .unnumbered .unlisted}

::: {#cb581 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *inp = "   123.4567beej";
    char *badchar;

    double val = strtod(inp, &badchar);

    printf("Converted string to %f\n", val);
    printf("Encountered bad characters: %s\n", badchar);

    val = strtod("987.654321beej", NULL);
    printf("Ignoring bad chars for result: %f\n", val);

    val = strtod("11.2233", &badchar);

    if (*badchar == '\0')
        printf("No bad chars: %f\n", val);
    else
        printf("Found bad chars: %f, %s\n", val, badchar);
}
```
:::

Output:

::: {#cb582 .sourceCode}
``` {.sourceCode .default}
Converted string to 123.456700
Encountered bad characters: beej
Ignoring bad chars: 987.654321
No bad chars: 11.223300
```
:::

### See Also {#see-also-154 .unnumbered .unlisted}

[`atof()`](stdlib.html#man-atof), [`strtol()`](stdlib.html#man-strtol)

------------------------------------------------------------------------

## [23.5]{.header-section-number} `strtol()`, `strtoll()`, `strtoul()`, `strtoull()` {#man-strtol number="23.5"}

Convert a string to an integer

### Synopsis {#synopsis-163 .unnumbered .unlisted}

::: {#cb583 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

long int strtol(const char * restrict nptr,
                char ** restrict endptr, int base);

long long int strtoll(const char * restrict nptr,
                      char ** restrict endptr, int base);

unsigned long int strtoul(const char * restrict nptr,
                          char ** restrict endptr, int base);

unsigned long long int strtoull(const char * restrict nptr,
                                char ** restrict endptr, int base);
```
:::

### Description {#description-163 .unnumbered .unlisted}


These convert a string to an integer like `atoi()`, but they have a few more bells and whistles.

> 这些函数像`atoi()`一样将字符串转换为整数，但它们具有更多的功能。


Most notable, they can tell you where conversion started going wrong, i.e. where invalid characters, if any, appear. Leading spaces are ignored. A `+` or `-` sign may precede the number.

> 最值得注意的是，它们可以告诉您转换开始出错的地方，即如果有的话，哪里出现了无效字符。忽略前导空格。可以在数字前面加上`+`或`-`号。


The basic idea is that if things go well, these functions will return the integer values contained in the strings. And if you pass in the `char**` typed `endptr`, it'll set it to point at the NUL at the end of the string.

> 基本思想是，如果一切顺利，这些函数将返回字符串中包含的整数值。如果您传入类型为`char**`的`endptr`，它将被设置为指向字符串末尾的NUL。


If things don't go well, they'll set `endptr` to point at the first character where things have gone awry. That is, if you're converting a value `103z2!` in base 10, they'll send `endptr` to point at the `z` because that's the first non-numeric character.

> 如果事情进展不顺利，他们会将`endptr`指向事情出现问题的第一个字符。也就是说，如果你正在以10进制的方式转换`103z2!`，他们会将`endptr`指向`z`，因为它是第一个非数字字符。


You can pass in `NULL` for `endptr` if you don't care to do any of that kind of error checking.

> 你可以将`NULL`传入`endptr`，如果你不想进行任何这类错误检查的话。


Wait---did I just say we could set the number base for the conversion? Yes! Yes, I did. Now [number bases](https://en.wikipedia.org/wiki/Radix)[^52^](footnotes.html#fn52){#fnref52 .footnote-ref role="doc-noteref"} are out of scope for this document, but certainly some of the more well-known are binary (base 2), octal (base 8), decimal (base 10), and hexadecimal (base 16).

> 等等---我刚刚说我们可以设置转换的数字基数吗？是的！是的，我确实这样说了。现在，[数字基数](https://en.wikipedia.org/wiki/Radix)[^52^](footnotes.html#fn52){#fnref52 .footnote-ref role="doc-noteref"}不在本文档的范围之内，但一些较为熟知的基数包括二进制（基数2）、八进制（基数8）、十进制（基数10）和十六进制（基数16）。


You can specify the number base for the conversion as the third parameter. Bases from 2 to 36 are supported, with case-insensitive digits running from `0` to `Z`.

> 你可以将第三个参数指定为转换的数字基数。支持2到36的基数，大小写数字从`0`到`Z`。


If you specify a base of `0`, the function will make an effort to determine it. It'll default to base 10 except for a couple cases:

> 如果您指定基数为“0”，该函数将尝试确定它。除了几种情况外，它将默认为基数10。

-   If the number has a leading `0`, it will be octal (base 8)
-   If the number has a leading `0x` or `0X`, it will be hex (base 16)

The locale might affect the behavior of these functions.

### Return Value {#return-value-161 .unnumbered .unlisted}

Returns the converted value.

`endptr`, if not `NULL` is set to the first invalid character, or to the beginning of the string if no conversion was performed, or to the string terminal NUL if all characters were valid.


If there's overflow, one of these values will be returned: `LONG_MIN`, `LONG_MAX`, `LLONG_MIN`, `LLONG_MAX`, `ULONG_MAX`, `ULLONG_MAX`. And `errno` is set to `ERANGE`.

> 如果溢出，将返回以下值之一：`LONG_MIN`，`LONG_MAX`，`LLONG_MIN`，`LLONG_MAX`，`ULONG_MAX`，`ULLONG_MAX`。`errno`被设置为`ERANGE`。

### Example {#example-164 .unnumbered .unlisted}

::: {#cb584 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // All output in decimal (base 10)

    printf("%ld\n", strtol("123", NULL, 0));      // 123
    printf("%ld\n", strtol("123", NULL, 10));     // 123
    printf("%ld\n", strtol("101010", NULL, 2));   // binary, 42
    printf("%ld\n", strtol("123", NULL, 8));      // octal, 83
    printf("%ld\n", strtol("123", NULL, 16));     // hex, 291

    printf("%ld\n", strtol("0123", NULL, 0));     // octal, 83
    printf("%ld\n", strtol("0x123", NULL, 0));    // hex, 291

    char *badchar;
    long int x = strtol("   1234beej", &badchar, 0);

    printf("Value is %ld\n", x);               // Value is 1234
    printf("Bad chars at \"%s\"\n", badchar);  // Bad chars at "beej"
}
```
:::

Output:

::: {#cb585 .sourceCode}
``` {.sourceCode .default}
123
123
42
83
291
83
291
Value is 1234
Bad chars at "beej"
```
:::

### See Also {#see-also-155 .unnumbered .unlisted}


[`atoi()`](stdlib.html#man-atoi), [`strtod()`](stdlib.html#man-strtod), [`setlocale()`](locale.html#man-setlocale), [`strtoimax()`](inttypes.html#man-strtoimax), [`strtoumax()`](inttypes.html#man-strtoimax)

> 1. [`atoi()`](stdlib.html#man-atoi)：将字符串转换为整数
2. [`strtod()`](stdlib.html#man-strtod)：将字符串转换为双精度浮点数
3. [`setlocale()`](locale.html#man-setlocale)：设置本地化环境
4. [`strtoimax()`](inttypes.html#man-strtoimax)：将字符串转换为最大整数
5. [`strtoumax()`](inttypes.html#man-strtoimax)：将字符串转换为最大无符号整数

------------------------------------------------------------------------

## [23.6]{.header-section-number} `rand()` {#man-rand number="23.6"}

Return a pseudorandom number

### Synopsis {#synopsis-164 .unnumbered .unlisted}

::: {#cb586 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int rand(void);
```
:::

### Description {#description-164 .unnumbered .unlisted}


This gives us back a pseudorandom number in the range `0` to `RAND_MAX`, inclusive. (`RAND_MAX` will be at least [\\(32767\\)]{.math .inline}.)

> 这给我们一个从0到RAND_MAX（至少为32767）的伪随机数。


If you want to force this to a certain range, the classic way to do this is to force it with the modulo operator `%`, although [this introduces biases](https://stackoverflow.com/questions/10984974/why-do-people-say-there-is-modulo-bias-when-using-a-random-number-generator)[^53^](footnotes.html#fn53){#fnref53 .footnote-ref role="doc-noteref"} if `RAND_MAX+1` is not a multiple of the number you're modding by. Dealing with this is out of scope for this guide.

> 如果您想将其强制转换为某个特定范围，则传统的方法是使用模运算符`％`来强制转换，尽管如果`RAND_MAX + 1`不是您要取模的数字的倍数，[这会引入偏差](https://stackoverflow.com/questions/10984974/why-do-people-say-there-is-modulo-bias-when-using-a-random-number-generator)[^53^](footnotes.html#fn53){#fnref53 .footnote-ref role="doc-noteref"}。处理此问题超出了本指南的范围。


If you want to to make a floating point number between `0` and `1` inclusive, you can divide the result by `RAND_MAX`. Or `RAND_MAX+1` if you don't want to include `1`. But of course, there are out-of-scope [problems with this, as well](https://mumble.net/~campbell/2014/04/28/uniform-random-float)[^54^](footnotes.html#fn54){#fnref54 .footnote-ref role="doc-noteref"}.

> 如果你想要在0和1之间创建一个浮点数（包括0和1），你可以将结果除以RAND_MAX。如果你不想包括1，可以除以RAND_MAX+1。但是当然，这也存在一些超出范围的问题（参见[^54^]）。


In short, `rand()` is a great way to get potentially poor random numbers with ease. Probably good enough for the game you're writing.

> 简而言之，`rand()`是一种轻松获得潜在差的随机数的好方法。可能足够好用于你正在编写的游戏。

The spec elaborates:

> There are no guarantees as to the quality of the random sequence produced and some implementations are known to produce sequences with distressingly non-random low-order bits. Applications with particular requirements should use a generator that is known to be sufficient for their needs.


Your system probably has a good random number generator on it if you need a stronger source. Linux users have `getrandom()`, for example, and Windows has `CryptGenRandom()`.

> 你的系统可能有一个很好的随机数生成器，如果你需要更强的来源。例如，Linux用户有`getrandom()`，而Windows有`CryptGenRandom()`。


For other more demanding random number work, you might find a library like the [GNU Scientific Library](https://www.gnu.org/software/gsl/doc/html/rng.html)[^55^](footnotes.html#fn55){#fnref55 .footnote-ref role="doc-noteref"} of use.

> 对于更高要求的随机数工作，您可能会发现像[GNU科学库](https://www.gnu.org/software/gsl/doc/html/rng.html)[^55^](footnotes.html#fn55){#fnref55 .footnote-ref role="doc-noteref"}这样的库很有用。


With most implementations, the numbers produced by `rand()` will be the same from run to run. To get around this, you need to start it off in a different place by passing a *seed* into the random number generator. You can do this with [`srand()`](stdlib.html#man-srand).

> 大多数实现中，`rand()`产生的数字会在运行时保持一致。为了解决这个问题，您需要通过将*种子*传递给随机数生成器来从不同的位置开始。您可以使用[`srand()`](stdlib.html#man-srand)来完成此操作。

### Return Value {#return-value-162 .unnumbered .unlisted}

Returns a random number in the range `0` to `RAND_MAX`, inclusive.

### Example {#example-165 .unnumbered .unlisted}


Note that all of these examples don't produce perfectly uniform distributions. But good enough for the untrained eye, and really common in general use when mediocre random number quality is acceptable.

> 注意，所有这些示例都不能产生完全均匀的分布。但对于未经训练的眼睛来说足够好，在普通使用中，当普通的随机数质量可以接受时，这种情况非常普遍。

::: {#cb587 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    printf("RAND_MAX = %d\n", RAND_MAX);

    printf("0 to 9: %d\n", rand() % 10);

    printf("10 to 44: %d\n", rand() % 35 + 10);
    printf("0 to 0.99999: %f\n", rand() / ((float)RAND_MAX + 1));
    printf("10.5 to 15.7: %f\n", 10.5 + 5.2 * rand() / (float)RAND_MAX);
}
```
:::

Output on my system:

::: {#cb588 .sourceCode}
``` {.sourceCode .default}
RAND_MAX = 2147483647
0 to 9: 3
10 to 44: 21
0 to 0.99999: 0.783099
10.5 to 15.7: 14.651888
```
:::

Example of seeding the RNG with the time:

::: {#cb589 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(void)
{
    // time(NULL) very likely returns the number of seconds since
    // January 1, 1970:

    srand(time(NULL));

    for (int i = 0; i < 5; i++)
        printf("%d\n", rand());
}
```
:::

### See Also {#see-also-156 .unnumbered .unlisted}

[`srand()`](stdlib.html#man-srand)

------------------------------------------------------------------------

## [23.7]{.header-section-number} `srand()` {#man-srand number="23.7"}

Seed the built-in pseudorandom number generator

### Synopsis {#synopsis-165 .unnumbered .unlisted}

::: {#cb590 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

void srand(unsigned int seed);
```
:::

### Description {#description-165 .unnumbered .unlisted}


The dirty little secret of pseudorandom number generation is that they're completely deterministic. There's nothing random about them. They just look random.

> 伪随机数生成的肮脏的小秘密是它们完全是确定性的。它们没有任何随机的东西。它们只是看起来像随机的。


If you use `rand()` and run your program several times, you might notice something *fishy*: they produce the same random numbers over and over again.

> 如果你使用`rand()`并多次运行程序，你可能会注意到一些可疑的情况：它们会不断重复产生相同的随机数。


To mix it up, we need to give the pseudorandom number generator a new "starting point", if you will. We call that the *seed*. It's just a number, but it is used as the basic for subsequent number generation. Give a different seed, and you'll get a different sequence of random numbers. Give the same seed, and you'll get the same sequence of random numbers corresponding to it[^56^](footnotes.html#fn56){#fnref56 .footnote-ref role="doc-noteref"}.

> 为了混合它，我们需要给伪随机数生成器一个新的“起点”，如果你愿意的话。我们称之为*种子*。它只是一个数字，但它被用作后续数字生成的基础。给出一个不同的种子，你会得到一个不同的随机数序列。给出相同的种子，你会得到与它相对应的相同的随机数序列[^56^]（脚注。HTML#fn56）{#fnref56 .footnote-ref role="doc-noteref"}。


So if you call `srand(3490)` before you start generating numbers with `rand()`, you'll get the same sequence every time. `srand(37)` would also give you the same sequence every time, but it would be a different sequence than the one you got with `srand(3490)`.

> 如果你在使用`rand()`生成数字之前调用`srand(3490)`，你会得到相同的序列每次。`srand(37)`也会给你相同的序列每次，但它会是一个不同于你用`srand(3490)`得到的序列。


But if you can't hardcode the seed (because that would give you the same sequence every time), how are you supposed to do this?

> 如果你不能硬编码种子（因为这会给你每次相同的序列），你该怎么做？


It's really common to use the number of seconds since January 1, 1970 (this date is known as the [*Unix epoch*](https://en.wikipedia.org/wiki/Unix_time)[^57^](footnotes.html#fn57){#fnref57 .footnote-ref role="doc-noteref"}) to seed the generator. This sounds pretty arbitrary except for the fact that it's exactly the value most implementations return from the library call `time(NULL)`[^58^](footnotes.html#fn58){#fnref58 .footnote-ref role="doc-noteref"}.

> 使用自1970年1月1日以来的秒数（这个日期被称为Unix epoch[^57^](footnotes.html#fn57){#fnref57 .footnote-ref role="doc-noteref"}）来种子生成器是很常见的。除了它正是大多数实现从库调用`time（NULL）`[^58^](footnotes.html#fn58){#fnref58 .footnote-ref role="doc-noteref"}返回的值之外，这听起来似乎很随意。

We'll do that in the example.

If you don't call `srand()`, it's as if you called `srand(1)`.

### Return Value {#return-value-163 .unnumbered .unlisted}

Returns nothing!

### Example {#example-166 .unnumbered .unlisted}

::: {#cb591 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <time.h>    // for the time() call

int main(void)
{
    srand(time(NULL));

    for (int i = 0; i < 5; i++)
        printf("%d\n", rand() % 32);
}
```
:::

Output:

::: {#cb592 .sourceCode}
``` {.sourceCode .default}
4
20
22
14
9
```
:::

Output from a subsequent run:

::: {#cb593 .sourceCode}
``` {.sourceCode .default}
19
0
31
31
24
```
:::

### See Also {#see-also-157 .unnumbered .unlisted}

[`rand()`](stdlib.html#man-rand), [`time()`](time.html#man-time)

------------------------------------------------------------------------

## [23.8]{.header-section-number} `aligned_alloc()` {#man-aligned_alloc number="23.8"}

Allocate specifically-aligned memory

### Synopsis {#synopsis-166 .unnumbered .unlisted}

::: {#cb594 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

void *aligned_alloc(size_t alignment, size_t size);
```
:::

### Description {#description-166 .unnumbered .unlisted}


Maybe you wanted [`malloc()`](stdlib.html#man-malloc) or [`calloc()`](stdlib.html#man-malloc) instead of this. But if you're sure you don't, read on!

> 也许你想要`malloc()`或`calloc()`而不是这个。但如果你确定不是，继续阅读！


Normally you don't have to think about this, since `malloc()` and `realloc()` both provide memory regions that are suitably [aligned](https://en.wikipedia.org/wiki/Data_structure_alignment)[^59^](footnotes.html#fn59){#fnref59 .footnote-ref role="doc-noteref"} for use with any data type.

> 通常，您不必考虑这个问题，因为`malloc()`和`realloc()`都提供了适合用于任何数据类型的对齐内存区域。


But if you need a more specific alignment, you can specify it with this function.

> 如果你需要更具体的对齐，你可以使用这个函数指定它。


When you're done using the memory region, be sure to free it with a call to [`free()`](stdlib.html#man-free).

> 当你使用完内存区域后，一定要用`free()`函数来释放它。

Don't pass in `0` for the size. It probably won't do anything you want.


In case you're wondering, all dynamically-allocated memory is automatically freed by the system when the program ends. That said, it's considered to be *Good Form* to explicitly `free()` everything you allocate. This way other programmers don't think you were being sloppy.

> 如果你想知道，当程序结束时，系统会自动释放所有动态分配的内存。尽管如此，明确地调用`free()`来释放你分配的内存被认为是好的做法。这样，其他程序员就不会认为你粗心大意了。

### Return Value {#return-value-164 .unnumbered .unlisted}


Returns a pointer to the newly-allocated memory, aligned as specified. Returns `NULL` if something goes wrong.

> 返回一个按指定对齐的新分配的内存的指针。如果出现问题，则返回`NULL`。

### Example {#example-167 .unnumbered .unlisted}

::: {#cb595 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>

int main(void)
{
    int *p = aligned_alloc(256, 10 * sizeof(int));

    // Just for fun, let's convert to intptr_t and mod with 256
    // to make sure we're actually aligned on a 256-byte boundary.
    //
    // This is probably some kind of implementation-defined
    // behavior, but I'll bet it works.

    intptr_t ip = (intptr_t)p;

    printf("%ld\n", ip % 256);   // 0!

    // Free it up
    free(p);
}
```
:::

### See Also {#see-also-158 .unnumbered .unlisted}


[`malloc()`](stdlib.html#man-malloc), [`calloc()`](stdlib.html#man-malloc), [`free()`](stdlib.html#man-free)

> `malloc()`，`calloc()`，`free()`

------------------------------------------------------------------------

## [23.9]{.header-section-number} `calloc()`, `malloc()` {#man-malloc number="23.9"}

Allocate memory for arbitrary use

### Synopsis {#synopsis-167 .unnumbered .unlisted}

::: {#cb596 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

void *calloc(size_t nmemb, size_t size);

void *malloc(size_t size);
```
:::

### Description {#description-167 .unnumbered .unlisted}


Both of these functions allocate memory for general-purpose use. It will be aligned such that it's useable for storing any data type.

> 这两个函数都为通用目的分配内存。它将被对齐，以便可以用于存储任何数据类型。

`malloc()` allocates exactly the specified number of bytes of memory in a contiguous block. The memory might be full of garbage data. (You can clear it with [`memset()`](stringref.html#man-memset), if you wish.)

`calloc()` is different in that it allocates space for `nmemb` objects of `size` bytes each. (You can do the same with `malloc()`, but you have to do the multiplication yourself.)

`calloc()` has an additional feature: it clears all the memory to `0`.


So if you're planning to zero the memory anyway, `calloc()` is probably the way to go. If you're not, you can avoid that overhead by calling `malloc()`.

> 如果你打算把内存清零，那么 `calloc()` 可能是最好的选择。如果不这样做，你可以通过调用 `malloc()` 来避免这种开销。


When you're done using the memory region, free it with a call to `free()`.

> 当你使用完内存区域后，请使用`free()`函数释放它。

Don't pass in `0` for the size. It probably won't do anything you want.


In case you're wondering, all dynamically-allocated memory is automatically freed by the system when the program ends. That said, it's considered to be *Good Form* to explicitly `free()` everything you allocate. This way other programmers don't think you were being sloppy.

> 如果你想知道，当程序结束时，系统会自动释放所有动态分配的内存。尽管如此，明确地调用`free()`函数释放所有分配的内存仍然被认为是好的编程风格。这样其他程序员就不会认为你编写的代码很马虎。

### Return Value {#return-value-165 .unnumbered .unlisted}


Both functions return a pointer to the shiny, newly-allocated memory. Or `NULL` if something's gone awry.

> 两个函数都会返回一个指向新分配的闪亮内存的指针。如果出现问题，则返回`NULL`。

### Example {#example-168 .unnumbered .unlisted}

Comparison of `malloc()` and `calloc()` for allocating 5 `int`s:

::: {#cb597 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdlib.h>

int main(void)
{
    // Allocate space for 5 ints
    int *p = malloc(5 * sizeof(int));

    p[0] = 12;
    p[1] = 30;

    // Allocate space for 5 ints
    // (Also clear that memory to 0)
    int *q = calloc(5, sizeof(int));

    q[0] = 12;
    q[1] = 30;

    // All done
    free(p);
    free(q);
}
```
:::

### See Also {#see-also-159 .unnumbered .unlisted}


[`aligned_alloc()`](stdlib.html#man-aligned_alloc), [`free()`](stdlib.html#man-free)

> [aligned_alloc()](stdlib.html#man-aligned_alloc)：对齐分配 
[free()](stdlib.html#man-free)：释放

------------------------------------------------------------------------

## [23.10]{.header-section-number} `free()` {#man-free number="23.10"}

Free a memory region

### Synopsis {#synopsis-168 .unnumbered .unlisted}

::: {#cb598 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

void free(void *ptr);
```
:::

### Description {#description-168 .unnumbered .unlisted}


You know that pointer you got back from `malloc()`, `calloc()`, or `aligned_alloc()`? You pass that pointer to `free()` to free the memory associated with it.

> 你知道你从`malloc()`、`calloc()`或`aligned_alloc()`获得的指针吗？你把这个指针传递给`free()`来释放与它相关的内存。


If you don't do this, the memory will stay allocated FOREVER AND EVER! (Well, until your program exits, anyway.)

> 如果你不这么做，内存将永远保留！（好吧，直到你的程序退出为止）


Fun fact: `free(NULL)` does nothing. You can safely call that. Sometimes it's convenient.

> 事实上：`free（NULL）`什么都不做。你可以安全地调用它。有时候这很方便。


Don't `free()` a pointer that's already been `free()`d. Don't `free()` a pointer that you didn't get back from one of the allocation functions. It would be *Bad*[^60^](footnotes.html#fn60){#fnref60 .footnote-ref role="doc-noteref"}.

> 不要释放已经被释放的指针。不要释放没有从分配函数中获得的指针。这将是非常糟糕的。

### Return Value {#return-value-166 .unnumbered .unlisted}

Returns nothing!

### Example {#example-169 .unnumbered .unlisted}

::: {#cb599 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdlib.h>

int main(void)
{
    // Allocate space for 5 ints
    int *p = malloc(5 * sizeof(int));

    p[0] = 12;
    p[1] = 30;

    // Free that space
    free(p);
}
```
:::

### See Also {#see-also-160 .unnumbered .unlisted}


[`malloc()`](stdlib.html#man-malloc), [`calloc()`](stdlib.html#man-malloc), [`aligned_alloc()`](stdlib.html#man-aligned_alloc)

> `malloc()`，`calloc()`，`aligned_alloc()`（[stdlib.html#man-malloc](stdlib.html#man-malloc)）

------------------------------------------------------------------------

## [23.11]{.header-section-number} `realloc()` {#man-realloc number="23.11"}

Resize a previously allocated stretch of memory

### Synopsis {#synopsis-169 .unnumbered .unlisted}

::: {#cb600 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

void *realloc(void *ptr, size_t size);
```
:::

### Description {#description-169 .unnumbered .unlisted}


This takes a pointer to some memory previously allocated with `malloc()` or `calloc()` and resizes it to the new size.

> 这将一个指针指向先前用`malloc()`或`calloc()`分配的内存，并将其调整为新的大小。


If the new size is smaller than the old size, any data larger than the new size is discarded.

> 如果新的尺寸比旧的尺寸小，则大于新尺寸的任何数据都会被丢弃。


If the new size is larger than the old size, the new larger part is uninitialized. (You can clear it with [`memset()`](stringref.html#man-memset).)

> 如果新的尺寸大于旧的尺寸，新的较大部分未初始化。（可以使用[`memset()`](stringref.html#man-memset)来清除它。）


Important note: the memory might move! If you resize, the system might need to relocate the memory to a larger continguous chunk. If this happens, `realloc()` will copy the old data to the new location for you.

> 重要提示：内存可能会移动！如果你调整大小，系统可能需要将内存重新定位到一个更大的连续块中。如果发生这种情况，`realloc（）`将为您将旧数据复制到新位置。


Because of this, it's important to save the returned value to your pointer to update it to the new location if things move. (Also, be sure to error-check so that you don't overwrite your old pointer with `NULL`, leaking the memory.)

> 由于这个原因，将返回值保存到指针中以更新其到新位置是很重要的（同时，确保进行错误检查，以免将旧指针覆盖为`NULL`，从而泄漏内存）。


You can also `relloc()` memory allocated with `aligned_alloc()`, but it will potentially lose its alignment if the block is moved.

> 你也可以使用`aligned_alloc()`重新定位分配的内存，但如果块被移动，它可能会失去对齐。

### Return Value {#return-value-167 .unnumbered .unlisted}


Returns a pointer to the resized memory region. This might be equivalent to the `ptr` passed in, or it might be some other location.

> 返回一个指向调整大小的内存区域的指针。这可能与传入的`ptr`相同，也可能是其他位置。

### Example {#example-170 .unnumbered .unlisted}

::: {#cb601 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // Allocate space for 5 ints
    int *p = malloc(5 * sizeof(int));

    p[0] = 12;
    p[1] = 30;

    // Reallocate for 10 bytes
    int *new_p = realloc(p, 10 * sizeof(int));

    if (new_p == NULL) {
        printf("Error reallocing\n");
    } else {
        p = new_p;  // It's good; let's keep it
        p[7] = 99;
    }

    // All done
    free(p);
}
```
:::

### See Also {#see-also-161 .unnumbered .unlisted}


[`malloc()`](stdlib.html#man-malloc), [`calloc()`](stdlib.html#man-malloc)

> `malloc()`，`calloc()`（[stdlib.html#man-malloc](stdlib.html#man-malloc)）

------------------------------------------------------------------------

## [23.12]{.header-section-number} `abort()` {#man-abort number="23.12"}

Abruptly end program execution

### Synopsis {#synopsis-170 .unnumbered .unlisted}

::: {#cb602 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

_Noreturn void abort(void);
```
:::

### Description {#description-170 .unnumbered .unlisted}


This ends program execution *abnormally* and immediately. Use this in rare, unexpected circumstances.

> 这结束程序执行*异常*并立即结束。在罕见的、意外的情况下使用它。


Open streams might not be flushed. Temporary files created might not be removed. Exit handlers are not called.

> 打开的流可能不会被刷新。创建的临时文件可能不会被移除。退出处理程序不会被调用。

A non-zero exit status is returned to the environment.


On some systems, `abort()` might [dump core](https://en.wikipedia.org/wiki/Core_dump)[^61^](footnotes.html#fn61){#fnref61 .footnote-ref role="doc-noteref"}, but this is outside the scope of the spec.

> 在某些系统上，`abort()`可能会[转储内核](https://en.wikipedia.org/wiki/Core_dump)[^61^](footnotes.html#fn61){#fnref61 .footnote-ref role="doc-noteref"}，但这超出了规范的范围。


You can cause the equivalent of an `abort()` by calling `raise(SIGABRT)`, but I don't know why you'd do that.

> 你可以通过调用`raise(SIGABRT)`来引发等效的`abort()`，但我不知道你为什么要这么做。


The only portable way to stop an `abort()` call midway is to use `signal()` to catch `SIGABRT` and then `exit()` in the signal handler.

> 唯一可以在中途停止`abort()`调用的便携式方法是使用`signal()`捕获`SIGABRT`，然后在信号处理程序中使用`exit()`。

### Return Value {#return-value-168 .unnumbered .unlisted}

This function never returns.

### Example {#example-171 .unnumbered .unlisted}

::: {#cb603 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int bad_thing = 1;

    if (bad_thing) {
        printf("This should never have happened!\n");
        fflush(stdout);  // Make sure the message goes out
        abort();
    }
}
```
:::

On my system, this outputs:

::: {#cb604 .sourceCode}
``` {.sourceCode .default}
This should never have happened!
zsh: abort (core dumped)  ./foo
```
:::

### See Also {#see-also-162 .unnumbered .unlisted}

[`signal()`](signal.html#man-signal)

------------------------------------------------------------------------

## [23.13]{.header-section-number} `atexit()`, `at_quick_exit()` {#man-atexit number="23.13"}

Set up handlers to run when the program exits

### Synopsis {#synopsis-171 .unnumbered .unlisted}

::: {#cb605 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int atexit(void (*func)(void));

int at_quick_exit(void (*func)(void));
```
:::

### Description {#description-171 .unnumbered .unlisted}


When the program does a normal exit with `exit()` or returns from `main()`, it looks for previously-registered handlers to call on the way out. These handlers are registered with the `atexit()` call.

> 当程序使用`exit()`正常退出或从`main()`返回时，它会查找之前注册的处理程序以在退出时调用。这些处理程序是使用`atexit()`调用注册的。


Think of it like, "Hey, when you're about to exit, do these extra things."

> 想象它就像是说：“嘿，当你准备离开的时候，做一些额外的事情。”


For the `quick_exit()` call, you can use the `at_quick_exit()` function to register handlers for that[^62^](footnotes.html#fn62){#fnref62 .footnote-ref role="doc-noteref"}. There's no crossover in handlers from `exit()` to `quick_exit()`, i.e. for a call to one, none of the other's handlers will fire.

> 对于`quick_exit()`调用，您可以使用`at_quick_exit()`函数来注册处理程序[^62^]（footnotes.html#fn62）{#fnref62 .footnote-ref role="doc-noteref"}。从`exit()`到`quick_exit()`的处理程序没有交叉，即对于一个调用，另一个的处理程序都不会触发。


You can register multiple handlers to fire---at least 32 handlers are supported by both `exit()` and `quick_exit()`.

> 你可以注册多个处理程序来触发，exit（）和quick_exit（）都支持至少32个处理程序。


The argument `func` to the functions looks a little weird---it's a pointer to a function to call. Basically just put the function name to call in there (without parentheses after). See the example, below.

> 参数`func`对函数来说看起来有点奇怪---它是一个指向要调用的函数的指针。基本上只需要在里面放入要调用的函数名（不需要括号）。参见下面的示例。


If you call `atexit()` from inside your `atexit()` handler (or equivalent in your `at_quick_exit()` handler), it's unspecified if it will get called. So get them all registered before you exit.

> 如果你从atexit()处理程序（或在at_quick_exit()处理程序中的等效物）内部调用atexit()，则不确定它是否会被调用。因此，在退出之前，请将它们全部注册。


When exiting, the functions will be called in the reverse order they were registered.

> 当退出时，函数将按照它们注册的相反顺序被调用。

### Return Value {#return-value-169 .unnumbered .unlisted}

These functions return `0` on success, or nonzero on failure.

### Example {#example-172 .unnumbered .unlisted}

`atexit()`:

::: {#cb606 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

void exit_handler_1(void)
{
    printf("Exit handler 1 called!\n");
}

void exit_handler_2(void)
{
    printf("Exit handler 2 called!\n");
}

int main(void)
{
    atexit(exit_handler_1);
    atexit(exit_handler_2);

    exit(0);
}
```
:::

For the output:

::: {#cb607 .sourceCode}
``` {.sourceCode .default}
Exit handler 2 called!
Exit handler 1 called!
```
:::

And a similar example with `quick_exit()`:

::: {#cb608 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

void exit_handler_1(void)
{
    printf("Exit handler 1 called!\n");
}

void exit_handler_2(void)
{
    printf("Exit handler 2 called!\n");
}

int main(void)
{
    at_quick_exit(exit_handler_1);
    at_quick_exit(exit_handler_2);

    quick_exit(0);
}
```
:::

### See Also {#see-also-163 .unnumbered .unlisted}

[`exit()`](stdlib.html#man-exit), [`quick_exit()`](stdlib.html#man-exit)

------------------------------------------------------------------------

## [23.14]{.header-section-number} `exit()`, `quick_exit()`, `_Exit()` {#man-exit number="23.14"}

Exit the currently-running program

### Synopsis {#synopsis-172 .unnumbered .unlisted}

::: {#cb609 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

_Noreturn void exit(int status);

_Noreturn void quick_exit(int status);

_Noreturn void _Exit(int status);
```
:::

### Description {#description-172 .unnumbered .unlisted}


All these functions cause the program to exit, with various levels of cleanup performed.

> 所有这些函数都会导致程序退出，并执行不同程度的清理工作。

`exit()` does the most cleanup and is the most normal exit.

`quick_exit()` is the second most.

`_Exit()` unceremoniously drops everything and ragequits on the spot.


Calling either of `exit()` or `quick_exit()` causes their respective `atexit()` or `at_quick_exit()` handlers to be called in the reverse order in which they were registered.

> 调用`exit()`或`quick_exit()`中的任一个，会导致它们各自的`atexit()`或`at_quick_exit()`处理程序以与它们注册的顺序相反的顺序被调用。

`exit()` will flush all streams and delete all temporary files.

`quick_exit()` or `_Exit()` might not perform that nicety.

`_Exit()` doesn't call any of the at-exit handlers, either.

For all functions, the exit `status` is returned to the environment.

Defined exit statuses are:

  Status               Description
  -------------------- --------------------------------------------------
  `EXIT_SUCCESS`       Typically returned when good things happen
  `0`                  Same as `EXIT_SUCCESS`
  `EXIT_FAILURE`       Oh noes! Definitely failure!
  Any positive value   Generally indicates another failure of some kind

OS X note: `quick_exit()` is not supported.

### Return Value {#return-value-170 .unnumbered .unlisted}

None of these functions ever return.

### Example {#example-173 .unnumbered .unlisted}

::: {#cb610 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdlib.h>

int main(void)
{
    int contrived_exit_type = 1;

    switch(contrived_exit_type) {
        case 1:
            exit(EXIT_SUCCESS);

        case 2:
            // Not supported in OS X
            quick_exit(EXIT_SUCCESS);

        case 3:
            _Exit(2);
    }
}
```
:::

### See Also {#see-also-164 .unnumbered .unlisted}


[`atexit()`](stdlib.html#man-atexit), [`at_quick_exit()`](stdlib.html#man-atexit)

> atexit()：退出时调用
at_quick_exit()：快速退出时调用

------------------------------------------------------------------------

## [23.15]{.header-section-number} `getenv()` {#man-getenv number="23.15"}

Get the value of an environment variable

### Synopsis {#synopsis-173 .unnumbered .unlisted}

::: {#cb611 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

char *getenv(const char *name);
```
:::

### Description {#description-173 .unnumbered .unlisted}


The environment often provides variables that are set before the program run that you can access at runtime.

> 环境经常在程序运行之前提供可以在运行时访问的变量。


Of course the exact details are system dependent, but these variables are key/value pairs, and you can get the value by passing the key to `getenv()` as the `name` parameter.

> 当然，确切的细节取决于系统，但这些变量是键/值对，您可以通过将键传递给`getenv（）`作为`name`参数来获取值。

You're not allowed to overwrite the string that's returned.


This is pretty limited in the standard, but your OS often provides better functionality.

> 这在标准中是相当有限的，但您的操作系统通常提供更好的功能。

### Return Value {#return-value-171 .unnumbered .unlisted}


Returns a pointer to the environment variable value, or `NULL` if the variable doesn't exist.

> 返回指向环境变量值的指针，如果变量不存在则返回`NULL`。

### Example {#example-174 .unnumbered .unlisted}

::: {#cb612 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    printf("PATH is %s\n", getenv("PATH"));
}
```
:::

Output (truncated in my case):

::: {#cb613 .sourceCode}
``` {.sourceCode .default}
PATH is /usr/bin:/usr/local/bin:/usr/sbin:/home/beej/.cargo/bin [...]
```
:::

------------------------------------------------------------------------

## [23.16]{.header-section-number} `system()` {#man-system number="23.16"}

Run an external program

### Synopsis {#synopsis-174 .unnumbered .unlisted}

::: {#cb614 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int system(const char *string);
```
:::

### Description {#description-174 .unnumbered .unlisted}

This will run an external program and then return to the caller.


The manner in which it runs the program is system-defined, but typically you can pass something to it just like you'd run on the command line, searching the `PATH`, etc.

> 程序运行的方式是系统定义的，但通常你可以像在命令行上运行一样传递参数，搜索`PATH`等。


Not all systems have this capability, but you can test for it by passing `NULL` to `system()` and seeing if it returns 0 (no command processor is available) or non-zero (a command processor is available! Yay!)

> 不是所有的系统都有这个功能，但你可以通过将`NULL`传递给`system()`来测试它，看看它是否返回0（没有命令处理器可用）或非零（有命令处理器可用！耶！）


If you're getting user input and passing it to the `system()` call, be extremely careful to escape all special shell characters (everything that's not alphanumeric) with a backslash to keep a villain from running something you don't want them to.

> 如果你正在获取用户输入并将其传递给`system()`调用，请务必用反斜杠转义所有特殊shell字符（非字母数字），以防止恶棍运行你不想他们运行的东西。

### Return Value {#return-value-172 .unnumbered .unlisted}


If `NULL` is passed, returns nonzero if a command processor is available (i.e. `system()` will work at all).

> 如果传入`NULL`，则如果有命令处理器可用（即`system()`可以正常工作），则返回非零值。

Otherwise returns an implementation-defined value.

### Example {#example-175 .unnumbered .unlisted}

::: {#cb615 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    printf("Here's a directory listing:\n\n");

    system("ls -l");   // Run this command and return

    printf("\nAll done!\n");
}
```
:::

Output:

::: {#cb616 .sourceCode}
``` {.sourceCode .default}
Here's a directory listing:

total 92
drwxr-xr-x 3 beej beej  4096 Oct 14 21:38 bin
drwxr-xr-x 2 beej beej  4096 Dec 20 20:07 examples
-rwxr-xr-x 1 beej beej 16656 Feb 23 21:49 foo
-rw-rw-rw- 1 beej beej   155 Feb 23 21:49 foo.c
-rw-r--r-- 1 beej beej  1350 Jan 27 22:11 Makefile
-rw-r--r-- 1 beej beej  4644 Jan 18 09:12 README.md
drwxr-xr-x 3 beej beej  4096 Feb 23 20:21 src
drwxr-xr-x 6 beej beej  4096 Feb 21 20:24 stage
drwxr-xr-x 2 beej beej  4096 Sep 27 20:54 translations
drwxr-xr-x 2 beej beej  4096 Sep 27 20:54 website

All done!
```
:::

------------------------------------------------------------------------

## [23.17]{.header-section-number} `bsearch()` {#man-bsearch number="23.17"}

Binary Search (maybe) an array of objects

### Synopsis {#synopsis-175 .unnumbered .unlisted}

::: {#cb617 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

void *bsearch(const void *key, const void *base,
              size_t nmemb, size_t size,
              int (*compar)(const void *, const void *));
```
:::

### Description {#description-175 .unnumbered .unlisted}

This crazy-looking function searches an array for a value.


It probably is a binary search or some fast, efficient search. But the spec doesn't really say.

> 可能是二分查找或者某种快速高效的搜索。但是规范并没有真正说明。

However, the array must be sorted! So binary search seems likely.

-   `key` is a pointer to the value to find.
-   `base` is a pointer to the start of the array---the array must be sorted!
-   `nmemb` is the number of elements in the array.
-   `size` is the `sizeof` each element in the array.
-   `compar` is a pointer to a function that will compare the key against other values.


The comparison function takes the key as the first argument and the value to compare against as the second. It should return a negative number if the key is less than the value, `0` if the key equals the value, and a positive number if the key is greater than the value.

> 比较函数将键作为第一个参数，将要比较的值作为第二个参数。如果键小于值，则应返回负数；如果键等于值，则应返回0；如果键大于值，则应返回正数。


This is commonly computed by taking the difference between the key and the value to be compared. If subtraction is supported.

> 这通常是通过计算键和要比较的值之间的差异来计算的，如果支持减法。


The return value from the [`strcmp()`](stringref.html#man-strcmp) function can be used for comparing strings.

> 函数[`strcmp()`](stringref.html#man-strcmp)的返回值可用于比较字符串。


Again, the array must be sorted according to the order of the comparison function before running `bsearch()`. Luckily for you, you can just call [`qsort()`](stdlib.html#man-qsort) with the same comparison function to get this done.

> 再次，在运行`bsearch()`之前，数组必须按照比较函数的顺序进行排序。幸运的是，您可以使用相同的比较函数调用[`qsort()`](stdlib.html#man-qsort)来完成此操作。


It's a general-purpose function---it'll search any type of array for anything. The catch is you have to write the comparison function.

> 它是一个通用函数---它可以搜索任何类型的数组。唯一的限制是你必须编写比较函数。

And that's not as scary as it looks. Jump down to the example

### Return Value {#return-value-173 .unnumbered .unlisted}


The function returns a pointer to the found value, or `NULL` if it can't be found.

> 该函数返回找到的值的指针，如果找不到则返回`NULL`。

### Example {#example-176 .unnumbered .unlisted}

::: {#cb618 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int compar(const void *key, const void *value)
{
    const int *k = key, *v = value;  // Need ints, not voids

    return *k - *v;
}

int main(void)
{
    int a[9] = {2, 6, 9, 12, 13, 18, 20, 32, 47};

    int *r, key;

    key = 12;  // 12 is in there
    r = bsearch(&key, a, 9, sizeof(int), compar);
    printf("Found %d\n", *r);

    key = 30;  // Won't find a 30
    r = bsearch(&key, a, 9, sizeof(int), compar);
    if (r == NULL)
        printf("Didn't find 30\n");

    // Searching with an unnamed key, pointer to 32
    r = bsearch(&(int){32}, a, 9, sizeof(int), compar);
    printf("Found %d\n", *r);  // Found it
}
```
:::

Output:

::: {#cb619 .sourceCode}
``` {.sourceCode .default}
Found 12
Didn't find 30
Found 32
```
:::

### See Also {#see-also-165 .unnumbered .unlisted}


[`strcmp()`](stringref.html#man-strcmp), [`qsort()`](stdlib.html#man-qsort)

> `strcmp()`：比较字符串；`qsort()`：快速排序

------------------------------------------------------------------------

## [23.18]{.header-section-number} `qsort()` {#man-qsort number="23.18"}

Quicksort (maybe) some data

### Synopsis {#synopsis-176 .unnumbered .unlisted}

::: {#cb620 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

void qsort(void *base, size_t nmemb, size_t size,
           int (*compar)(const void *, const void *));
```
:::

### Description {#description-176 .unnumbered .unlisted}


This function will quicksort (or some other sort, probably speedy) an array of data in-place[^63^](footnotes.html#fn63){#fnref63 .footnote-ref role="doc-noteref"}.

> 这个函数将会（可能是快速排序或其他排序）在原地对一个数据数组进行排序[^63^](footnotes.html#fn63){#fnref63 .footnote-ref role="doc-noteref"}。


Like `bsearch()`, it's data-agnostic. Any data for which you can define a relative ordering can be sorted, whether `int`s, `struct`s, or anything else.

> 就像`bsearch()`一样，它是数据无关的。只要你能定义相对顺序，就可以对任何数据进行排序，无论是`int`、`struct`还是其他任何东西。


Also like `bsearch()`, you have to give a comparison function to do the actual compare.

> 也像`bsearch()`一样，你必须提供一个比较函数来进行实际的比较。

-   `base` is a pointer to the start of the array to be sorted.
-   `nmemb` is the number of elements in the array.
-   `size` is the `sizeof` each element.
-   `compar` is a pointer to the comparison function.


The comparison function takes pointers to two elements of the array as arguments and compares them. It should return a negative number if the first argument is less than the second, `0` if they are equal, and a positive number if the first argument is greater than the second.

> 比较函数接受两个数组元素的指针作为参数，并进行比较。如果第一个参数小于第二个参数，则应返回负数；如果它们相等，则返回0；如果第一个参数大于第二个参数，则应返回正数。


This is commonly computed by taking the difference between the first argument and the second. If subtraction is supported.

> 这通常是通过计算第一个参数和第二个参数之间的差异来计算的。如果支持减法。


The return value from the [`strcmp()`](stringref.html#man-strcmp) function can provide sort order for strings.

> 函数`strcmp()`的返回值可以为字符串提供排序顺序。


If you have to sort a `struct`, just subtract the specific field you want to sort by.

> 如果你需要对一个`struct`进行排序，只需要减去你想要排序的特定字段即可。


This comparison function can be used by [`bsearch()`](stdlib.html#man-bsearch) to do searches after the list is sorted.

> 这个比较函数可以用[`bsearch()`](stdlib.html#man-bsearch)在列表排序后进行搜索。


To reverse the sort, subtract the second argument from the first, i.e. negate the return value from `compar()`.

> 反转排序，将第二个参数从第一个参数中减去，即将`compar()`的返回值取反。

### Return Value {#return-value-174 .unnumbered .unlisted}

Returns nothing!

### Example {#example-177 .unnumbered .unlisted}

::: {#cb621 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int compar(const void *elem0, const void *elem1)
{
    const int *x = elem0, *y = elem1;  // Need ints, not voids

    if (*x > *y) return 1;
    if (*x < *y) return -1;
    return 0;
}

int main(void)
{
    int a[9] = {14, 2, 3, 17, 10, 8, 6, 1, 13};

    // Sort the list

    qsort(a, 9, sizeof(int), compar);

    // Print sorted list

    for (int i = 0; i < 9; i++)
        printf("%d ", a[i]);

    putchar('\n');

    // Use the same compar() function to binary search
    // for 17 (passed in as an unnamed object)

    int *r = bsearch(&(int){17}, a, 9, sizeof(int), compar);
    printf("Found %d!\n", *r);
}
```
:::

Output:

::: {#cb622 .sourceCode}
``` {.sourceCode .default}
1 2 3 6 8 10 13 14 17
Found 17!
```
:::

### See Also {#see-also-166 .unnumbered .unlisted}


[`strcmp()`](stringref.html#man-strcmp), [`bsearch()`](stdlib.html#man-bsearch)

> `strcmp()`：比较字符串
`bsearch()`：二分查找

------------------------------------------------------------------------

## [23.19]{.header-section-number} `abs()`, `labs()`, `llabs()` {#man-abs number="23.19"}

Compute the absolute value of an integer

### Synopsis {#synopsis-177 .unnumbered .unlisted}

::: {#cb623 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int abs(int j);

long int labs(long int j);

long long int llabs(long long int j);
```
:::

### Description {#description-177 .unnumbered .unlisted}


Compute the absolute value of `j`. If you don't remember, that's how far from zero `j` is.

> 计算j的绝对值。如果你不记得，那就是j离零有多远。


In other words, if `j` is negative, return it as a positive. If it's positive, return it as a positive. Always be positive. Enjoy life.

> 如果`j`是负数，把它变成正数。如果它是正数，也把它变成正数。总是保持积极的心态。享受生活。


If the result cannot be represented, the behavior is undefined. Be especially aware of the upper half of unsigned numbers.

> 如果结果无法表示，行为是不确定的。特别要注意无符号数的上半部分。

### Return Value {#return-value-175 .unnumbered .unlisted}

Returns the absolute value of `j`, [\\(\|j\|\\)]{.math .inline}.

### Example {#example-178 .unnumbered .unlisted}

::: {#cb624 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    printf("|-2| = %d\n", abs(-2));
    printf("|4|  = %d\n", abs(4));
}
```
:::

Output:

::: {#cb625 .sourceCode}
``` {.sourceCode .default}
|-2| = 2
|4|  = 4
```
:::

### See Also {#see-also-167 .unnumbered .unlisted}

[`fabs()`](math.html#man-fabs)

------------------------------------------------------------------------

## [23.20]{.header-section-number} `div()`, `ldiv()`, `lldiv()` {#man-div number="23.20"}

Compute the quotient and remainder of two numbers

### Synopsis {#synopsis-178 .unnumbered .unlisted}

::: {#cb626 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

div_t div(int numer, int denom);

ldiv_t ldiv(long int numer, long int denom);

lldiv_t lldiv(long long int numer, long long int denom);
```
:::

### Description {#description-178 .unnumbered .unlisted}


These functions get you the quotient and remainder of a pair of numbers in one go.

> 这些函数可以一次性获得一对数字的商和余数。


They return a structure that has two fields, `quot`, and `rem`, the types of which match types of `numer` and `denom`. Note how each function returns a different variant of `div_t`.

> 他们返回一个结构，其中有两个字段'quot'和'rem'，它们的类型与'numer'和'denom'的类型相匹配。注意每个函数都返回div_t的不同变体。

These `div_t` variants are equivalent to the following:

::: {#cb627 .sourceCode}
``` {.sourceCode .c}
typedef struct {
    int quot, rem;
} div_t;

typedef struct {
    long int quot, rem;
} ldiv_t;

typedef struct {
    long long int quot, rem;
} lldiv_t;
```
:::

Why use these instead of the division operator?

The C99 Rationale says:

> Because C89 had implementation-defined semantics for division of signed integers when negative operands were involved, `div` and `ldiv`, and `lldiv` in C99, were invented to provide well-specified semantics for signed integer division and remainder operations. The semantics were adopted to be the same as in Fortran. Since these functions return both the quotient and the remainder, they also serve as a convenient way of efficiently modeling underlying hardware that computes both results as part of the same operation. Table 7.2 summarizes the semantics of these functions.

Indeed, K&R2 (C89) says:

> The direction of truncation for `/` and the sign of the result for `%` are machine-dependent for negative operands \[...\]


The Rationale then goes on to spell out what the signs of the quotient and remainder will be given the signs of a numerator and denominator when using the `div()` functions:

> 然后，理由将详细说明，当使用`div()`函数时，给定分子和分母的符号，商和余数的符号将是什么。

           `numer`                    `denom`                     `quot`                     `rem`

  -------------------------- -------------------------- -------------------------- --------------------------

> -------------------------- -------------------------- -------------------------- --------------------------

无

   [\\(+\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(+\\)]{.math .inline}

> [\(+\)]{.math .inline}[\(+\)]{.math .inline}[\(+\)]{.math .inline}[\(+\)]{.math .inline}

   [\\(-\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(-\\)]{.math .inline}

> [\(-\)] + [\(+\)] - [\(-\)] - [\(-\)]

   [\\(+\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(+\\)]{.math .inline}

> [\(+\)]、[\(-\)]、[\(-\)]、[\(+\)]

   [\\(-\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(-\\)]{.math .inline}

> [(-)] [-] [+] [-]

### Return Value {#return-value-176 .unnumbered .unlisted}


A `div_t`, `ldiv_t`, or `lldiv_t` structure with the `quot` and `rem` fields loaded with the quotient and remainder of the operation of `numer/denom`.

> 一个`div_t`、`ldiv_t`或`lldiv_t`结构，其中`quot`和`rem`字段中装载了`numer/denom`运算的商和余数。

### Example {#example-179 .unnumbered .unlisted}

::: {#cb628 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    div_t d = div(64, -7);

    printf("64 / -7 = %d\n", d.quot);
    printf("64 %% -7 = %d\n", d.rem);
}
```
:::

Output:

::: {#cb629 .sourceCode}
``` {.sourceCode .default}
64 / -7 = -9
64 % -7 = 1
```
:::

### See Also {#see-also-168 .unnumbered .unlisted}

[`fmod()`](math.html#man-fmod), [`remainder()`](math.html#man-remainder)

------------------------------------------------------------------------

## [23.21]{.header-section-number} `mblen()` {#man-mblen number="23.21"}

Return the number of bytes in a multibyte character

### Synopsis {#synopsis-179 .unnumbered .unlisted}

::: {#cb630 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int mblen(const char *s, size_t n);
```
:::

### Description {#description-179 .unnumbered .unlisted}


If you have a multibyte character in a string, this will tell you how many bytes long it is.

> 如果字符串中有多字节字符，这将告诉您它有多长。

`n` is the maximum number of bytes `mblen()` will scan before giving up.


If `s` is a `NULL` pointer, tests if this encoding has state dependency, as noted in the return value, below. It also resets the state, if there is one.

> 如果`s`是一个`NULL`指针，测试这种编码是否具有状态依赖性，如下面的返回值所示。如果有状态，它也会重置状态。

The behavior of this function is influenced by the locale.

### Return Value {#return-value-177 .unnumbered .unlisted}


Returns the number of bytes used to encode this character, or `-1` if there is no valid multibyte character in the next `n` bytes.

> 返回用于编码此字符所使用的字节数，如果下一个`n`个字节中没有有效的多字节字符，则返回`-1`。

Or, if `s` is NULL, returns true if this encoding has state dependency.

### Example {#example-180 .unnumbered .unlisted}


For the example, I used my extended character set to put Unicode characters in the source. If this doesn't work for you, use the `\uXXXX` escape.

> 举个例子，我使用了扩展字符集来在源中放入Unicode字符。如果这对你不起作用，请使用`\uXXXX`转义字符。

::: {#cb631 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>

int main(void)
{
    setlocale(LC_ALL, "");

    printf("State dependency: %d\n", mblen(NULL, 0));
    printf("Bytes for €: %d\n", mblen("€", 5));
    printf("Bytes for \u00e9: %d\n", mblen("\u00e9", 5));  // \u00e9 == é
    printf("Bytes for &: %d\n", mblen("&", 5));
}
```
:::

Output (in my case, the encoding is UTF-8, but your mileage may vary):

::: {#cb632 .sourceCode}
``` {.sourceCode .default}
State dependency: 0
Bytes for €: 3
Bytes for é: 2
Bytes for &: 1
```
:::

### See Also {#see-also-169 .unnumbered .unlisted}


[`mbtowc()`](stdlib.html#man-mbtowc), [`mbstowcs())`](stdlib.html#man-mbstowcs), [`setlocale()`](locale.html#man-setlocale)

> [`mbtowc()`](stdlib.html#man-mbtowc)：将多字节字符转换为宽字符
[`mbstowcs()`](stdlib.html#man-mbstowcs)：将多字节字符串转换为宽字符串
[`setlocale()`](locale.html#man-setlocale)：设置地区信息

------------------------------------------------------------------------

## [23.22]{.header-section-number} `mbtowc()` {#man-mbtowc number="23.22"}

Convert a multibyte character to a wide character

### Synopsis {#synopsis-180 .unnumbered .unlisted}

::: {#cb633 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int mbtowc(wchar_t * restrict pwc, const char * restrict s, size_t n);
```
:::

### Description {#description-180 .unnumbered .unlisted}


If you have a multibyte character, this function will convert it to a wide character and stored at the address pointed to by `pwc`. Up to `n` bytes of the multibyte character will be analyzed.

> 如果您有一个多字节字符，此函数将其转换为宽字符并存储在由`pwc`指向的地址。将分析多字节字符的最多`n`个字节。


If `pwc` is `NULL`, the resulting character will not be stored. (Useful for just getting the return value.)

> 如果`pwc`为`NULL`，则不会存储生成的字符（对于只获取返回值很有用）。


If `s` is a `NULL` pointer, tests if this encoding has state dependency, as noted in the return value, below. It also resets the state, if there is one.

> 如果`s`是一个`NULL`指针，测试这种编码是否具有状态依赖性，如下面的返回值所示。如果有状态，它也会重置状态。

The behavior of this function is influenced by the locale.

### Return Value {#return-value-178 .unnumbered .unlisted}


Returns the number of bytes used in the encoded wide character, or `-1` if there is no valid multibyte character in the next `n` bytes.

> 返回编码宽字符使用的字节数，如果接下来的`n`个字节中没有有效的多字节字符，则返回`-1`。

Returns `0` if `s` points to the NUL character.

Or, if `s` is NULL, returns true if this encoding has state dependency.

### Example {#example-181 .unnumbered .unlisted}

::: {#cb634 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <wchar.h>

int main(void)
{
    setlocale(LC_ALL, "");

    printf("State dependency: %d\n", mbtowc(NULL, NULL, 0));

    wchar_t wc;
    int bytes;

    bytes = mbtowc(&wc, "€", 5);

    printf("L'%lc' takes %d bytes as multibyte char '€'\n", wc, bytes);
}
```
:::

Output on my system:

::: {#cb635 .sourceCode}
``` {.sourceCode .default}
State dependency: 0
L'€' takes 3 bytes as multibyte char '€'
```
:::

### See Also {#see-also-170 .unnumbered .unlisted}


[`mblen()`](stdlib.html#man-mblen), [`mbstowcs()`](stdlib.html#man-mbstowcs), [`wcstombs()`](stdlib.html#man-wcstombs), [`setlocale()`](locale.html#man-setlocale)

> [`mblen()`](stdlib.html#man-mblen)：计算多字节字符的字节数
[`mbstowcs()`](stdlib.html#man-mbstowcs)：将多字节字符串转换为宽字符串
[`wcstombs()`](stdlib.html#man-wcstombs)：将宽字符串转换为多字节字符串
[`setlocale()`](locale.html#man-setlocale)：设置地区信息

------------------------------------------------------------------------

## [23.23]{.header-section-number} `wctomb()` {#man-wctomb number="23.23"}

Convert a wide character to a multibyte character

### Synopsis {#synopsis-181 .unnumbered .unlisted}

::: {#cb636 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

int wctomb(char *s, wchar_t wc);
```
:::

### Description {#description-181 .unnumbered .unlisted}


If you have your hands on a wide character, you can use this to make it multibyte.

> 如果你拥有一个宽字符，你可以用它来制作多字节字符。


The wide character `wc` is stored as a multibyte character in the string pointed to by `s`. The buffer `s` points to should be at least `MB_CUR_MAX` characters long. Note that `MB_CUR_MAX` changes with locale.

> 宽字符`wc`存储在由`s`指向的字符串中作为多字节字符。`s`指向的缓冲区应至少有`MB_CUR_MAX`个字符长。注意，`MB_CUR_MAX`会随着区域设置而改变。


If `wc` is a NUL wide character, a NUL is stored in `s` after the bytes needed to reset the shift state (if any).

> 如果`wc`是一个NUL宽字符，那么在重置移位状态（如果有的话）所需的字节之后，一个NUL就会存储在`s`中。


If `s` is a `NULL` pointer, tests if this encoding has state dependency, as noted in the return value, below. It also resets the state, if there is one.

> 如果`s`是一个`NULL`指针，测试这种编码是否具有状态依赖性，如下面的返回值所示。如果有状态，它也会重置状态。

The behavior of this function is influenced by the locale.

### Return Value {#return-value-179 .unnumbered .unlisted}


Returns the number of bytes used in the encoded multibyte character, or `-1` if `wc` does not correspond to any valid multibyte character.

> 返回编码的多字节字符所使用的字节数，如果`wc`不对应任何有效的多字节字符，则返回`-1`。

Or, if `s` is NULL, returns true if this encoding has state dependency.

### Example {#example-182 .unnumbered .unlisted}

::: {#cb637 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <wchar.h>

int main(void)
{
    setlocale(LC_ALL, "");

    printf("State dependency: %d\n", mbtowc(NULL, NULL, 0));

    int bytes;
    char mb[MB_CUR_MAX + 1];

    bytes = wctomb(mb, L'€');
    mb[bytes] = '\0';

    printf("L'€' takes %d bytes as multibyte char '%s'\n", bytes, mb);
}
```
:::

Output on my system:

::: {#cb638 .sourceCode}
``` {.sourceCode .default}
State dependency: 0
L'€' takes 3 bytes as multibyte char '€'
```
:::

### See Also {#see-also-171 .unnumbered .unlisted}


[`mbtowc()`](stdlib.html#man-mbtowc), [`mbstowcs()`](stdlib.html#man-mbstowcs), [`wcstombs()`](stdlib.html#man-wcstombs), [`setlocale()`](locale.html#man-setlocale)

> [`mbtowc()`](stdlib.html#man-mbtowc)：将多字节字符转换为宽字符
[`mbstowcs()`](stdlib.html#man-mbstowcs)：将多字节字符串转换为宽字符串
[`wcstombs()`](stdlib.html#man-wcstombs)：将宽字符串转换为多字节字符串
[`setlocale()`](locale.html#man-setlocale)：设置地区信息

------------------------------------------------------------------------

## [23.24]{.header-section-number} `mbstowcs()` {#man-mbstowcs number="23.24"}

Convert a multibyte string to a wide character string

### Synopsis {#synopsis-182 .unnumbered .unlisted}

::: {#cb639 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

size_t mbstowcs(wchar_t * restrict pwcs, const char * restrict s, size_t n);
```
:::

### Description {#description-182 .unnumbered .unlisted}


If you have a multibyte string (AKA a regular string), you can convert it wto a wide character string with this function.

> 如果您有一个多字节字符串（也称为常规字符串），您可以使用此函数将其转换为宽字符串。


At most `n` wide characters are written to the destination `pwcs` from the source `s`.

> 最多从源`s`写入`n`个宽字符到目标`pwcs`。

A NUL character is stored as a wide NUL character.


Non-portable POSIX extension: if you're using a POSIX-complaint library, this function allows `pwcs` to be `NULL` if you're only interested in the return value. Most notably, this will give you the number of characters in a multibyte string (as opposed to [`strlen()`](stringref.html#man-strlen) which counts the bytes.)

> 如果您使用POSIX兼容库，此功能允许`pwcs`为`NULL`，如果您只对返回值感兴趣，则可以使用非便携式POSIX扩展。最显著的是，这将给您多字节字符串中的字符数（与[`strlen（）`](stringref.html#man-strlen)，它计算字节数不同）。

### Return Value {#return-value-180 .unnumbered .unlisted}

Returns the number of wide characters written to the destination `pwcs`.

If an invalid multibyte character was found, returns `(size_t)(-1)`.

If the return value is `n`, it means the result was *not* NUL-terminated.

### Example {#example-183 .unnumbered .unlisted}


This source uses an extended character set. If your compiler doesn't support it, you'll have to replace them with `\u` escapes.

> 这个源代码使用了扩展字符集。如果你的编译器不支持它，你需要用`\u`转义来替换它们。

::: {#cb640 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <string.h>

int main(void)
{
    setlocale(LC_ALL, "");

    wchar_t wcs[128];
    char *s = "€200 for this spoon?";  // 20 characters

    size_t char_count, byte_count;

    char_count = mbstowcs(wcs, s, 128);
    byte_count = strlen(s);

    printf("Wide string: L\"%ls\"\n", wcs);
    printf("Char count : %zu\n", char_count);    // 20
    printf("Byte count : %zu\n\n", byte_count);  // 22 on my system

    // POSIX Extension that allows you to pass NULL for
    // the destination so you can just use the return
    // value (which is the character count of the string, 
    // if no errors have occurred)

    s = "§¶°±π€•";  // 7 characters

    char_count = mbstowcs(NULL, s, 0);  // POSIX-only, nonportable
    byte_count = strlen(s);

    printf("Multibyte str: \"%s\"\n", s);
    printf("Char count   : %zu\n", char_count);  // 7
    printf("Byte count   : %zu\n", byte_count);  // 16 on my system
}
```
:::

Output on my system (byte count will depend on your encoding):

::: {#cb641 .sourceCode}
``` {.sourceCode .default}
Wide string: L"€200 for this spoon?"
Char count : 20
Byte count : 22

Multibyte str: "§¶°±π€•"
Char count   : 7
Byte count   : 16
```
:::

### See Also {#see-also-172 .unnumbered .unlisted}


[`mblen()`](stdlib.html#man-mblen), [`mbtowc()`](stdlib.html#man-mbtowc), [`wcstombs()`](stdlib.html#man-wcstombs), [`setlocale()`](locale.html#man-setlocale)

> [`mblen()`](stdlib.html#man-mblen)：计算多字节字符的长度
[`mbtowc()`](stdlib.html#man-mbtowc)：将多字节字符转换为宽字符
[`wcstombs()`](stdlib.html#man-wcstombs)：将宽字符转换为多字节字符
[`setlocale()`](locale.html#man-setlocale)：设置地区信息

------------------------------------------------------------------------

## [23.25]{.header-section-number} `wcstombs()` {#man-wcstombs number="23.25"}

Convert a wide character string to a multibyte string

### Synopsis {#synopsis-183 .unnumbered .unlisted}

::: {#cb642 .sourceCode}
``` {.sourceCode .c}
#include <stdlib.h>

size_t wcstombs(char * restrict s, const wchar_t * restrict pwcs, size_t n);
```
:::

### Description {#description-183 .unnumbered .unlisted}


If you have a wide character string and you want it as multibyte string, this is the function for you!

> 如果你有一个宽字符串，你想要它成为多字节字符串，这就是你需要的函数！


It'll take the wide characters pointed to by `pwcs` and convert them to multibyte characters stored in `s`. No more than `n` bytes will be written to `s`.

> 它会把指向`pwcs`的宽字符转换成存储在`s`中的多字节字符。最多只会写入`n`个字节到`s`中。


Non-portable POSIX extension: if you're using a POSIX-complaint library, this function allows `s` to be `NULL` if you're only interested in the return value. Most notably, this will give you the number of bytes needed to encode the wide characters in a multibyte string.

> 如果您使用POSIX兼容库，此功能允许`s`为`NULL`，如果您只对返回值感兴趣，则可以使用非便携式POSIX扩展。最显著的是，这将给您在多字节字符串中编码宽字符所需的字节数。

### Return Value {#return-value-181 .unnumbered .unlisted}


Returns the number of bytes written to `s`, or `(size_t)(-1)` if one of the characters can't be encoded into a multibyte string.

> 返回写入`s`的字节数，如果其中一个字符无法编码为多字节字符串，则返回`(size_t)(-1)`。

If the return value is `n`, it means the result was *not* NUL-terminated.

### Example {#example-184 .unnumbered .unlisted}


This source uses an extended character set. If your compiler doesn't support it, you'll have to replace them with `\u` escapes.

> 这个源代码使用了扩展字符集。如果你的编译器不支持，你需要用`\u`转义来替换它们。

::: {#cb643 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <string.h>

int main(void)
{
    setlocale(LC_ALL, "");

    char mbs[128];
    wchar_t *wcs = L"€200 for this spoon?";  // 20 characters

    size_t byte_count;

    byte_count = wcstombs(mbs, wcs, 128);

    printf("Wide string: L\"%ls\"\n", wcs);
    printf("Multibyte  : \"%s\"\n", mbs);
    printf("Byte count : %zu\n\n", byte_count);  // 22 on my system

    // POSIX Extension that allows you to pass NULL for
    // the destination so you can just use the return
    // value (which is the character count of the string, 
    // if no errors have occurred)

    wcs = L"§¶°±π€•";  // 7 characters

    byte_count = wcstombs(NULL, wcs, 0);  // POSIX-only, nonportable

    printf("Wide string: L\"%ls\"\n", wcs);
    printf("Byte count : %zu\n", byte_count);  // 16 on my system
}
```
:::

Output on my system (byte count will depend on your encoding):

::: {#cb644 .sourceCode}
``` {.sourceCode .default}
Wide string: L"€200 for this spoon?"
Multibyte  : "€200 for this spoon?"
Byte count : 22

Wide string: L"§¶°±π€•"
Byte count : 16
```
:::

### See Also {#see-also-173 .unnumbered .unlisted}


[`mblen()`](stdlib.html#man-mblen), [`wctomb()`](stdlib.html#man-wctomb), [`mbstowcs()`](stdlib.html#man-mbstowcs), [`setlocale()`](locale.html#man-setlocale)

> [`mblen()`](stdlib.html#man-mblen)：计算多字节字符的字节数
[`wctomb()`](stdlib.html#man-wctomb)：将宽字符转换为多字节字符
[`mbstowcs()`](stdlib.html#man-mbstowcs)：将多字节字符串转换为宽字符串
[`setlocale()`](locale.html#man-setlocale)：设置地区信息

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdio.html) \| [Contents](index.html) \| [Next](stdnoreturn.html)
:::
