---
tip: translate by openai@2023-07-20 19:24:36
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdbool.html) \| [Contents](index.html) \| [Next](stdint.html)
:::

------------------------------------------------------------------------

# [20]{.header-section-number} `<stddef.h>` A Few Standard Definitions {#stddef number="20"}

Despite its name, I've haven't seen this frequently included.

It includes several types and macros.


  ---------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------
简体中文
  Name                                           Description

  ---------------------------------------------- ----------------------------------------------------

> ---------------------------------------------- ----------------------------------------------------
简体中文：---------------------------------------------- ----------------------------------------------------

  [`ptrdiff_t`](stddef.html#man-ptrdiff_t)       Signed integer difference between two pointers

> `ptrdiff_t` 是指两个指针之间的有符号整数差值。


  [`size_t`](stddef.html#man-size_t)             Unsigned integer type returned by `sizeof`

> `size_t`（[stddef.html#man-size_t](stddef.html#man-size_t)）是`sizeof`函数返回的无符号整数类型。


  [`max_align_t`](stddef.html#man-max_align_t)   Declare a type with the biggest possible alignment

> [`max_align_t`](stddef.html#man-max_align_t) 声明一个具有最大可能对齐的类型

  [`wchar_t`](stddef.html#man-wchar_t)           Wide character type


  `NULL`                                         `NULL` pointer, as defined a number of places

> 空指针，在许多地方被定义为无效的指针。


  [`offsetof`](stddef.html#man-offsetof)         Get the byte offsets of `struct` or `union` fields

> 获取结构体或联合体字段的字节偏移量

  ---------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------
简体中文

## [20.1]{.header-section-number} `ptrdiff_t` {#man-ptrdiff_t number="20.1"}


This holds the different between two pointers. You could store this in another type, but the result of a pointer subtraction is an implementation-defined type; you can be maximally portable by using `ptrdiff_t`.

> 这个保存了两个指针之间的差异。你可以用另一种类型来存储，但是指针减法的结果是实现定义的类型；你可以通过使用`ptrdiff_t`来获得最大的可移植性。

::: {#cb473 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stddef.h>

int main(void)
{
    int cats[100];

    int *f = cats + 20;
    int *g = cats + 60;

    ptrdiff_t d = g - f;  // difference is 40
```
:::

And you can print it by prefixing the integer format specifier with `t`:

::: {#cb474 .sourceCode startfrom="13"}
``` {.sourceCode .numberSource .c .numberLines}
    printf("%td\n", d);  // Print decimal: 40
    printf("%tX\n", d);  // Print hex:     28
}
```
:::

## [20.2]{.header-section-number} `size_t` {#man-size_t number="20.2"}


This is the type returned by `sizeof` and used in a few other places. It's an unsigned integer.

> 这是由`sizeof`返回的类型，并在其他一些地方使用。它是一个无符号整数。

You can print it using the `z` prefix in `printf()`:

::: {#cb475 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <uchar.h>
#include <string.h>
#include <stddef.h>

int main(void)
{
    size_t x;

    x = sizeof(int);

    printf("%zu\n", x);
```
:::


Some functions return negative numbers cast to `size_t` as error values (such as [`mbrtoc16()`](uchar.html#man-mbrtoc16)). If you want to print these as negative values, you can do it with `%zd`:

> 一些函数会将负数作为错误值返回为`size_t`（例如[`mbrtoc16()`](uchar.html#man-mbrtoc16)）。如果你想将其作为负值打印出来，可以使用`%zd`：

::: {#cb476 .sourceCode startfrom="14"}
``` {.sourceCode .numberSource .c .numberLines}
    char16_t a;
    mbstate_t mbs;
    memset(&mbs, 0, sizeof mbs);

    x = mbrtoc16(&a, "b", 8, &mbs);

    printf("%zd\n", x);
}
```
:::

## [20.3]{.header-section-number} `max_align_t` {#man-max_align_t number="20.3"}


As far as I can tell, this exists to allow the runtime computation of the maximum fundamental [alignment](https://en.wikipedia.org/wiki/Data_structure_alignment)[^45^](footnotes.html#fn45){#fnref45 .footnote-ref role="doc-noteref"} on the current platform. Someone please mail me if there's another use.

> 据我所知，这是为了允许在当前平台上运行时计算最大基本[对齐](https://en.wikipedia.org/wiki/Data_structure_alignment)[^45^](footnotes.html#fn45){#fnref45 .footnote-ref role="doc-noteref"}。如果有其他用途，请有人给我发邮件。


Maybe you need this if you're writing your own memory allocator or somesuch.

> 也许如果你正在编写自己的内存分配器之类的东西，你就需要这个了。

::: {#cb477 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stddef.h>
#include <stdio.h>      // For printf()
#include <stdalign.h>   // For alignof

int main(void)
{
    int max = alignof(max_align_t);

    printf("Maximum fundamental alignment: %d\n", max);
}
```
:::

On my system, this prints:

::: {#cb478 .sourceCode}
``` {.sourceCode .default}
Maximum fundamental alignment: 16
```
:::


See also [`alignas`](stdalign.html#man-alignas), [`alignof`](stdalign.html#man-alignof).

> 另见[`alignas`](stdalign.html#man-alignas)，[`alignof`](stdalign.html#man-alignof)。

## [20.4]{.header-section-number} `wchar_t` {#man-wchar_t number="20.4"}

This is analogous to `char`, except it's for wide characters.


It's an integer type that has enough range to hold unique values for all characters in all supported locales.

> 它是一种整数类型，具有足够的范围来容纳所有支持的本地化环境中所有字符的唯一值。

The value `0` is the wide `NUL` character.


Finally, the values of character constants from the basic character set will be the same as their corresponding `wchar_t` values... unless `__STDC_MB_MIGHT_NEQ_WC__` is defined.

> 最后，基本字符集中的字符常量的值将与其对应的`wchar_t`值相同... 除非定义了`__STDC_MB_MIGHT_NEQ_WC__`。

## [20.5]{.header-section-number} `offsetof` {#man-offsetof number="20.5"}


If you have a `struct` or `union`, you can use this to get the byte offset of fields within that type.

> 如果你有一个`struct`或`union`，你可以使用它来获取该类型中字段的字节偏移量。

Usage is:

::: {#cb479 .sourceCode}
``` {.sourceCode .c}
offsetof(type, fieldname);
```
:::

The resulting value has type `size_t`.

Here's an example that prints the field offsets of a `struct`:

::: {#cb480 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stddef.h>

struct foo {
    int a;
    char b;
    char c;
    float d;
};

int main(void)
{
    printf("a: %zu\n", offsetof(struct foo, a));
    printf("b: %zu\n", offsetof(struct foo, b));
    printf("c: %zu\n", offsetof(struct foo, c));
    printf("d: %zu\n", offsetof(struct foo, d));
}
```
:::

On my system, this outputs:

::: {#cb481 .sourceCode}
``` {.sourceCode .default}
a: 0
b: 4
c: 5
d: 8
```
:::

And you can't use `offsetof` on a bitfield, so don't get your hopes up.

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdbool.html) \| [Contents](index.html) \| [Next](stdint.html)
:::
