---
tip: translate by openai@2023-07-21 13:23:36
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](wchar.html) \| [Contents](index.html) \| [Next](footnotes.html)
:::

------------------------------------------------------------------------

# [31]{.header-section-number} `<wctype.h>` Wide Character Classification and Transformation {#wctype number="31"}


  -------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------
简体中文
  Function                                     Description

  -------------------------------------------- ----------------------------------------------------------

> -------------------------------------------- ----------------------------------------------------------
简体中文：-------------------------------------------- ----------------------------------------------------------

  [`iswalnum()`](wctype.html#man-iswalnum)     Test if a wide character is alphanumeric.

> 检查宽字符是否为字母数字。


  [`iswalpha()`](wctype.html#man-iswalpha)     Tests if a wide character is alphabetic

> 检查宽字符是否为字母字符。


  [`iswblank()`](wctype.html#man-iswblank)     Tests if this is a wide blank character

> 检查这是否是一个宽空白字符。


  [`iswcntrl()`](wctype.html#man-iswcntrl)     Tests if this is a wide control character.

> [iswcntrl()](wctype.html#man-iswcntrl) 测试这是否是一个宽控制字符。


  [`iswctype()`](wctype.html#man-iswctype)     Determine wide character classification

> `iswctype()`（wctype.html#man-iswctype）检测宽字符分类。


  [`iswdigit()`](wctype.html#man-iswdigit)     Test if this wide character is a digit

> [`iswdigit()`](wctype.html#man-iswdigit) 测试这个宽字符是否是数字。


  [`iswgraph()`](wctype.html#man-iswgraph)     Test to see if a wide character is a printable non-space

> 检查宽字符是否为可打印的非空字符


  [`iswlower()`](wctype.html#man-iswlower)     Tests if a wide character is lowercase

> 检查宽字符是否为小写字母。


  [`iswprint()`](wctype.html#man-iswprint)     Tests if a wide character is printable

> [`iswprint()`](wctype.html#man-iswprint) 测试宽字符是否可打印。


  [`iswpunct()`](wctype.html#man-iswpunct)     Test if a wide character is punctuation

> 检查宽字符是否为标点符号（iswpunct()）


  [`iswspace()`](wctype.html#man-iswspace)     Test if a wide character is whitespace

> [`iswspace()`](wctype.html#man-iswspace) 测试宽字符是否为空格。


  [`iswupper()`](wctype.html#man-iswupper)     Tests if a wide character is uppercase

> [`iswupper()`](wctype.html#man-iswupper) 测试宽字符是否为大写字母。


  [`iswxdigit()`](wctype.html#man-iswxdigit)   Tests if a wide character is a hexadecimal digit

> [`iswxdigit()`](wctype.html#man-iswxdigit) 测试宽字符是否为十六进制数字


  [`towctrans()`](wctype.html#man-towctrans)   Convert wide characters to upper or lowercase

> [`towctrans()`](wctype.html#man-towctrans) 将宽字符转换为大写或小写。


  [`towlower()`](wctype.html#man-towlower)     Convert an uppercase wide character to lowercase

> [`towlower()`](wctype.html#man-towlower) 将大写宽字符转换为小写。


  [`towupper()`](wctype.html#man-towupper)     Convert a lowercase wide character to uppercase

> [`towupper()`](wctype.html#man-towupper) 将小写宽字符转换为大写


  [`wctrans()`](wctype.html#man-wctrans)       Helper function for `towctrans()`

> `wctrans()`（wctype.html#man-wctrans）是`towctrans()`的辅助函数。


  [`wctype()`](wctype.html#man-wctype)         Helper function for `iswctype()`

> `wctype()`（wctype.html#man-wctype）帮助函数用于`iswctype()`

  -------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------
简化中文

This is like [`<ctype.h>`](ctype.html#ctype) except for wide characters.


With it you can test for character classifications (like "is this character whitespace?") or do basic character conversions (like "force this character to lowercase").

> 你可以用它来测试字符分类（比如“这个字符是空格吗？”）或者做基本的字符转换（比如“将这个字符强制转换为小写”）。

------------------------------------------------------------------------

## [31.1]{.header-section-number} `iswalnum()` {#man-iswalnum number="31.1"}

Test if a wide character is alphanumeric.

### Synopsis {#synopsis-267 .unnumbered .unlisted}

::: {#cb902 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswalnum(wint_t wc);
```
:::

### Description {#description-267 .unnumbered .unlisted}


Basically tests if a character is alphabetic (`A`-`Z` or `a`-`z`) or a digit (`0`-`9`). But some other characters might also qualify based on the locale.

> 基本上测试一个字符是否为字母（A-Z或a-z）或数字（0-9）。但是根据地区，其他一些字符也可能符合要求。

This is equivalent to testing if `iswalpha()` or `iswdigit()` is true.

### Return Value {#return-value-265 .unnumbered .unlisted}

Returns true if the character is alphanumeric.

### Example {#example-269 .unnumbered .unlisted}

::: {#cb903 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                  testing this char
    //                           v
    wprintf(L"%ls\n", iswalnum(L'a')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswalnum(L'B')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswalnum(L'5')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswalnum(L'?')? L"yes": L"no");  // no
}
```
:::

### See Also {#see-also-254 .unnumbered .unlisted}


[`iswalpha()`](wctype.html#man-iswalpha), [`iswdigit()`](wctype.html#man-iswdigit), [`isalnum()`](ctype.html#man-isalnum)

> [`iswalpha()`](wctype.html#man-iswalpha)：检查宽字符是否为字母
[`iswdigit()`](wctype.html#man-iswdigit)：检查宽字符是否为数字
[`isalnum()`](ctype.html#man-isalnum)：检查字符是否为字母或数字

------------------------------------------------------------------------

## [31.2]{.header-section-number} `iswalpha()` {#man-iswalpha number="31.2"}

Tests if a wide character is alphabetic

### Synopsis {#synopsis-268 .unnumbered .unlisted}

::: {#cb904 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswalpha(wint_t wc);
```
:::

### Description {#description-268 .unnumbered .unlisted}


Basically tests if a character is alphabetic (`A`-`Z` or `a`-`z`). But some other characters might also qualify based on the locale. (If other characters qualify, they won't be control characters, digits, punctuation, or spaces.)

> 基本上测试一个字符是否为字母（`A`-`Z`或`a`-`z`）。但是根据地区，其他一些字符也可能符合要求。（如果其他字符符合要求，它们不会是控制字符、数字、标点符号或空格。）

This is the same as testing for `iswupper()` or `iswlower()`.

### Return Value {#return-value-266 .unnumbered .unlisted}

Returns true if the character is alphabetic.

### Example {#example-270 .unnumbered .unlisted}

::: {#cb905 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                  testing this char
    //                           v
    wprintf(L"%ls\n", iswalpha(L'a')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswalpha(L'B')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswalpha(L'5')? L"yes": L"no");  // no
    wprintf(L"%ls\n", iswalpha(L'?')? L"yes": L"no");  // no
}
```
:::

### See Also {#see-also-255 .unnumbered .unlisted}


[`iswalnum()`](wctype.html#man-iswalnum), [`isalpha()`](ctype.html#man-isalpha)

> [`iswalnum()`](wctype.html#man-iswalnum)：检查宽字符是否为字母或数字
[`isalpha()`](ctype.html#man-isalpha)：检查字符是否为字母

------------------------------------------------------------------------

## [31.3]{.header-section-number} `iswblank()` {#man-iswblank number="31.3"}

Tests if this is a wide blank character

### Synopsis {#synopsis-269 .unnumbered .unlisted}

::: {#cb906 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswblank(wint_t wc);
```
:::

### Description {#description-269 .unnumbered .unlisted}


Blank characters are whitespace that are also used as word separators on the same line. In the "C" locale, the only blank characters are space and tab.

> 空白字符是在同一行上也用作单词分隔符的空白字符。在“C”语言环境中，唯一的空白字符是空格和制表符。

Other locales might define other blank characters.

### Return Value {#return-value-267 .unnumbered .unlisted}

Returns true if this is a blank character.

### Example {#example-271 .unnumbered .unlisted}

::: {#cb907 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswblank(L' ')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswblank(L'\t')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswblank(L'\n')? L"yes": L"no");  // no
    wprintf(L"%ls\n", iswblank(L'a')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswblank(L'?')? L"yes": L"no");   // no
}
```
:::

### See Also {#see-also-256 .unnumbered .unlisted}


[`iswspace()`](wctype.html#man-iswspace), [`isblank()`](ctype.html#man-isblank)

> [`iswspace()`](wctype.html#man-iswspace)：检查宽字符是否为空白字符（空格、换行符、制表符等）
[`isblank()`](ctype.html#man-isblank)：检查字符是否为空格或制表符

------------------------------------------------------------------------

## [31.4]{.header-section-number} `iswcntrl()` {#man-iswcntrl number="31.4"}

Tests if this is a wide control character.

### Synopsis {#synopsis-270 .unnumbered .unlisted}

::: {#cb908 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswcntrl(wint_t wc);
```
:::

### Description {#description-270 .unnumbered .unlisted}


The spec is pretty barren, here. But I'm just going to assume that it works like the non-wide version. So let's look at that.

> 这里的规格相当空洞。但我只是假设它像非宽版本一样工作。所以让我们来看看它。

A *control character* is a locale-specific non-printing character.


For the "C" locale, this means control characters are in the range 0x00 to 0x1F (the character right before SPACE) and 0x7F (the DEL character).

> 对于“C”语言环境，这意味着控制字符的范围为0x00至0x1F（SPACE之前的字符）和0x7F（DEL字符）。


Basically if it's not an ASCII (or Unicode less than 128) printable character, it's a control character in the "C" locale.

> 基本上，如果不是ASCII（或Unicode小于128）可打印字符，那么它就是“C”语言环境中的控制字符。

Probably.

### Return Value {#return-value-268 .unnumbered .unlisted}

Returns true if this is a control character.

### Example {#example-272 .unnumbered .unlisted}

::: {#cb909 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswcntrl(L'\t')? L"yes": L"no");  // yes (tab)
    wprintf(L"%ls\n", iswcntrl(L'\n')? L"yes": L"no");  // yes (newline)
    wprintf(L"%ls\n", iswcntrl(L'\r')? L"yes": L"no");  // yes (return)
    wprintf(L"%ls\n", iswcntrl(L'\a')? L"yes": L"no");  // yes (bell)
    wprintf(L"%ls\n", iswcntrl(L' ')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswcntrl(L'a')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswcntrl(L'?')? L"yes": L"no");   // no
}
```
:::

### See Also {#see-also-257 .unnumbered .unlisted}

[`iscntrl()`](ctype.html#man-iscntrl)

------------------------------------------------------------------------

## [31.5]{.header-section-number} `iswdigit()` {#man-iswdigit number="31.5"}

Test if this wide character is a digit

### Synopsis {#synopsis-271 .unnumbered .unlisted}

::: {#cb910 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswdigit(wint_t wc);
```
:::

### Description {#description-271 .unnumbered .unlisted}

Tests if the wide character is a digit (`0`-`9`).

### Return Value {#return-value-269 .unnumbered .unlisted}

Returns true if the character is a digit.

### Example {#example-273 .unnumbered .unlisted}

::: {#cb911 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswdigit(L'0')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswdigit(L'5')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswdigit(L'a')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswdigit(L'B')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswdigit(L'?')? L"yes": L"no");   // no
}
```
:::

### See Also {#see-also-258 .unnumbered .unlisted}


[`iswalnum()`](wctype.html#man-iswalnum), [`isdigit()`](ctype.html#man-isdigit)

> [`iswalnum()`](wctype.html#man-iswalnum)：检查宽字符是否为字母或数字。
[`isdigit()`](ctype.html#man-isdigit)：检查字符是否为数字。

------------------------------------------------------------------------

## [31.6]{.header-section-number} `iswgraph()` {#man-iswgraph number="31.6"}

Test to see if a wide character is a printable non-space

### Synopsis {#synopsis-272 .unnumbered .unlisted}

::: {#cb912 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswgraph(wint_t wc);
```
:::

### Description {#description-272 .unnumbered .unlisted}


Returns true if this is a printable (non-control) character and also not a whitespace character.

> 返回true如果这是一个可打印（非控制）字符，而且也不是空白字符。

Basically if `iswprint()` is true and `iswspace()` is false.

### Return Value {#return-value-270 .unnumbered .unlisted}

Returns true if this is a printable non-space character.

### Example {#example-274 .unnumbered .unlisted}

::: {#cb913 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswgraph(L'0')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswgraph(L'a')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswgraph(L'B')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswgraph(L'?')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswgraph(L' ')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswgraph(L'\n')? L"yes": L"no");  // no
}
```
:::

### See Also {#see-also-259 .unnumbered .unlisted}


[`iswprint()`](wctype.html#man-iswprint), [`iswspace()`](wctype.html#man-iswspace), [`isgraph()`](ctype.html#man-isgraph)

> [`iswprint()`](wctype.html#man-iswprint)：检查宽字符是否可打印
[`iswspace()`](wctype.html#man-iswspace)：检查宽字符是否为空格
[`isgraph()`](ctype.html#man-isgraph)：检查字符是否可打印（除空格外）

------------------------------------------------------------------------

## [31.7]{.header-section-number} `iswlower()` {#man-iswlower number="31.7"}

Tests if a wide character is lowercase

### Synopsis {#synopsis-273 .unnumbered .unlisted}

::: {#cb914 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswlower(wint_t wc);
```
:::

### Description {#description-273 .unnumbered .unlisted}

Tests if a character is lowercase, in the range `a`-`z`.


In other locales, there could be other lowercase characters. In all cases, to be lowercase, the following must be true:

> 在其他地区，可能会有其他小写字符。无论如何，要使其小写，必须满足以下条件：

::: {#cb915 .sourceCode}
``` {.sourceCode .c}
!iswcntrl(c) && !iswdigit(c) && !iswpunct(c) && !iswspace(c)
```
:::

### Return Value {#return-value-271 .unnumbered .unlisted}

Returns true if the wide character is lowercase.

### Example {#example-275 .unnumbered .unlisted}

::: {#cb916 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswlower(L'c')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswlower(L'0')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswlower(L'B')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswlower(L'?')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswlower(L' ')? L"yes": L"no");   // no
}
```
:::

### See Also {#see-also-260 .unnumbered .unlisted}


[`islower()`](ctype.html#man-islower), [`iswupper()`](ctype.html#man-isupper), [`iswalpha()`](ctype.html#man-isalpha), [`towupper()`](ctype.html#man-toupper), [`towlower()`](ctype.html#man-tolower)

> [`islower()`](ctype.html#man-islower)：检查字符是否为小写字母
[`iswupper()`](ctype.html#man-isupper)：检查字符是否为大写字母
[`iswalpha()`](ctype.html#man-isalpha)：检查字符是否为字母
[`towupper()`](ctype.html#man-toupper)：将字符转换为大写字母
[`towlower()`](ctype.html#man-tolower)：将字符转换为小写字母

------------------------------------------------------------------------

## [31.8]{.header-section-number} `iswprint()` {#man-iswprint number="31.8"}

Tests if a wide character is printable

### Synopsis {#synopsis-274 .unnumbered .unlisted}

::: {#cb917 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswprint(wint_t wc);
```
:::

### Description {#description-274 .unnumbered .unlisted}


Tests if a wide character is printable, including space (`' '`). So like `isgraph()`, except space isn't left out in the cold.

> 检查宽字符是否可打印，包括空格（' '）。就像`isgraph()`一样，只是空格不冷落在外面。

### Return Value {#return-value-272 .unnumbered .unlisted}

Returns true if the wide character is printable, including space (`' '`).

### Example {#example-276 .unnumbered .unlisted}

::: {#cb918 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswprint(L'c')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswprint(L'0')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswprint(L' ')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswprint(L'\r')? L"yes": L"no");  // no
}
```
:::

### See Also {#see-also-261 .unnumbered .unlisted}


[`isprint()`](ctype.html#man-isprint), [`iswgraph()`](wctype.html#man-iswgraph), [`iswcntrl()`](wctype.html#man-iswcntrl)

> [`isprint()`](ctype.html#man-isprint)：检查字符是否可打印
[`iswgraph()`](wctype.html#man-iswgraph)：检查宽字符是否可打印
[`iswcntrl()`](wctype.html#man-iswcntrl)：检查宽字符是否为控制字符

------------------------------------------------------------------------

## [31.9]{.header-section-number} `iswpunct()` {#man-iswpunct number="31.9"}

Test if a wide character is punctuation

### Synopsis {#synopsis-275 .unnumbered .unlisted}

::: {#cb919 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswpunct(wint_t wc);
```
:::

### Description {#description-275 .unnumbered .unlisted}

Tests if a wide character is punctuation.

This means for any given locale:

::: {#cb920 .sourceCode}
``` {.sourceCode .c}
!isspace(c) && !isalnum(c)
```
:::

### Return Value {#return-value-273 .unnumbered .unlisted}

True if the wide character is punctuation.

### Example {#example-277 .unnumbered .unlisted}

Results may vary based on locale.

::: {#cb921 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswpunct(L',')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswpunct(L'!')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswpunct(L'c')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswpunct(L'0')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswpunct(L' ')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswpunct(L'\n')? L"yes": L"no");  // no
}
```
:::

### See Also {#see-also-262 .unnumbered .unlisted}


[`ispunct()`](ctype.html#man-ispunct), [`iswspace()`](wctype.html#man-iswspace), [`iswalnum()`](wctype.html#man-iswalnum)

> [`ispunct()`](ctype.html#man-ispunct)：检查字符是否为标点符号
[`iswspace()`](wctype.html#man-iswspace)：检查宽字符是否为空白字符
[`iswalnum()`](wctype.html#man-iswalnum)：检查宽字符是否为字母或数字

------------------------------------------------------------------------

## [31.10]{.header-section-number} `iswspace()` {#man-iswspace number="31.10"}

Test if a wide character is whitespace

### Synopsis {#synopsis-276 .unnumbered .unlisted}

::: {#cb922 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswspace(wint_t wc);
```
:::

### Description {#description-276 .unnumbered .unlisted}

Tests if `c` is a whitespace character. These are probably:

-   Space (`' '`)
-   Formfeed (`'\f'`)
-   Newline (`'\n'`)
-   Carriage Return (`'\r'`)
-   Horizontal Tab (`'\t'`)
-   Vertical Tab (`'\v'`)


Other locales might specify other whitespace characters. `iswalnum()`, `iswgraph()`, and `iswpunct()` are all false for all whitespace characters.

> 其他语言环境可能会指定其他空白字符。`iswalnum()`、`iswgraph()`和`iswpunct()`对所有空白字符都为假。

### Return Value {#return-value-274 .unnumbered .unlisted}

True if the character is whitespace.

### Example {#example-278 .unnumbered .unlisted}

Results may vary based on locale.

::: {#cb923 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswspace(L' ')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswspace(L'\n')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswspace(L'\t')? L"yes": L"no");  // yes
    wprintf(L"%ls\n", iswspace(L',')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswspace(L'!')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswspace(L'c')? L"yes": L"no");   // no
}
```
:::

### See Also {#see-also-263 .unnumbered .unlisted}


[`isspace()`](ctype.html#man-isspace), [`iswblank()`](wctype.html#man-iswblank)

> [`isspace()`](ctype.html#man-isspace)：检查字符是否为空白字符
[`iswblank()`](wctype.html#man-iswblank)：检查宽字符是否为空白字符

------------------------------------------------------------------------

## [31.11]{.header-section-number} `iswupper()` {#man-iswupper number="31.11"}

Tests if a wide character is uppercase

### Synopsis {#synopsis-277 .unnumbered .unlisted}

::: {#cb924 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswupper(wint_t wc);
```
:::

### Description {#description-277 .unnumbered .unlisted}

Tests if a character is uppercase in the current locale.

To be uppercase, the following must be true:

::: {#cb925 .sourceCode}
``` {.sourceCode .c}
!iscntrl(c) && !isdigit(c) && !ispunct(c) && !isspace(c)
```
:::

### Return Value {#return-value-275 .unnumbered .unlisted}

Returns true if the wide character is uppercase.

### Example {#example-279 .unnumbered .unlisted}

::: {#cb926 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                   testing this char
    //                           v
    wprintf(L"%ls\n", iswupper(L'B')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswupper(L'c')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswupper(L'0')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswupper(L'?')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswupper(L' ')? L"yes": L"no");   // no
}
```
:::

### See Also {#see-also-264 .unnumbered .unlisted}


[`isupper()`](ctype.html#man-isupper), [`iswlower()`](wctype.html#man-iswlower), [`iswalpha()`](wctype.html#man-iswalpha), [`towupper()`](wctype.html#man-towupper), [`towlower()`](wctype.html#man-towlower)

> [`isupper()`](ctype.html#man-isupper)，[`iswlower()`](wctype.html#man-iswlower)，[`iswalpha()`](wctype.html#man-iswalpha)，[`towupper()`](wctype.html#man-towupper)，[`towlower()`](wctype.html#man-towlower)

------------------------------------------------------------------------

## [31.12]{.header-section-number} `iswxdigit()` {#man-iswxdigit number="31.12"}

Tests if a wide character is a hexadecimal digit

### Synopsis {#synopsis-278 .unnumbered .unlisted}

::: {#cb927 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswxdigit(wint_t wc);
```
:::

### Description {#description-278 .unnumbered .unlisted}


Returns true if the wide character is a hexadecimal digit. Namely if it's `0`-`9`, `a`-`f`, or `A`-`F`.

> 返回真，如果宽字符是十六进制数字。也就是说，如果它是`0`-`9`、`a`-`f`或`A`-`F`。

### Return Value {#return-value-276 .unnumbered .unlisted}

True if the character is a hexadecimal digit.

### Example {#example-280 .unnumbered .unlisted}

::: {#cb928 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                    testing this char
    //                            v
    wprintf(L"%ls\n", iswxdigit(L'B')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswxdigit(L'c')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswxdigit(L'2')? L"yes": L"no");   // yes
    wprintf(L"%ls\n", iswxdigit(L'G')? L"yes": L"no");   // no
    wprintf(L"%ls\n", iswxdigit(L'?')? L"yes": L"no");   // no
}
```
:::

### See Also {#see-also-265 .unnumbered .unlisted}


[`isxdigit()`](ctype.html#man-isxdigit), [`iswdigit()`](wctype.html#man-iswdigit)

> [`isxdigit()`](ctype.html#man-isxdigit)：检查字符是否为十六进制数字（0-9，a-f，A-F）
[`iswdigit()`](wctype.html#man-iswdigit)：检查宽字符是否为数字（0-9）

------------------------------------------------------------------------

## [31.13]{.header-section-number} `iswctype()` {#man-iswctype number="31.13"}

Determine wide character classification

### Synopsis {#synopsis-279 .unnumbered .unlisted}

::: {#cb929 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

int iswctype(wint_t wc, wctype_t desc);
```
:::

### Description {#description-279 .unnumbered .unlisted}


This is the Swiss Army knife of classification functions; it's all the other ones rolled into one.

> 这是一把瑞士军刀式的分类功能，它把其它所有的功能都汇集到一起。

You call it with something like this:

::: {#cb930 .sourceCode}
``` {.sourceCode .c}
if (iswctype(c, wctype("digit")))  // or "alpha" or "space" or...
```
:::

and it behaves just like you'd called:

::: {#cb931 .sourceCode}
``` {.sourceCode .c}
if (iswdigit(c))
```
:::


The difference is that you can specify the type of matching you want to do as a string at runtime, which might be convenient.

> 可以在运行时以字符串的形式指定要进行的匹配类型，这可能很方便。

`iswctype()` relies on the return value from the [`wctype()`](wctype.html#man-wctype) call to get its work done.


Stolen from the spec, here are the `iswctype()` calls and their equivalents:

> 从规格中偷来的，这里是`iswctype()`调用及其等价物：

  `iswctype()` call                 Hard-coded equivalent
  --------------------------------- -----------------------
  `iswctype(c, wctype("alnum"))`    `iswalnum(c)`
  `iswctype(c, wctype("alpha"))`    `iswalpha(c)`
  `iswctype(c, wctype("blank"))`    `iswblank(c)`
  `iswctype(c, wctype("cntrl"))`    `iswcntrl(c)`
  `iswctype(c, wctype("digit"))`    `iswdigit(c)`
  `iswctype(c, wctype("graph"))`    `iswgraph(c)`
  `iswctype(c, wctype("lower"))`    `iswlower(c)`
  `iswctype(c, wctype("print"))`    `iswprint(c)`
  `iswctype(c, wctype("punct"))`    `iswpunct(c)`
  `iswctype(c, wctype("space"))`    `iswspace(c)`
  `iswctype(c, wctype("upper"))`    `iswupper(c)`
  `iswctype(c, wctype("xdigit"))`   `iswxdigit(c)`


See the [`wctype()` documentation](wctype.html#man-wctype) for how that helper function works.

> 查看[`wctype()`文档](wctype.html#man-wctype)了解该辅助函数的工作原理。

### Return Value {#return-value-277 .unnumbered .unlisted}


Returns true if the wide character `wc` matches the character class in `desc`.

> 如果宽字符`wc`与`desc`中的字符类匹配，则返回true。

### Example {#example-281 .unnumbered .unlisted}


Test for a given character classification at when the classification isn't known at compile time:

> 测试在编译时未知的给定字符分类：

::: {#cb932 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>  // for fflush(stdout)
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    wchar_t c;        // Holds a single wide character (to test)
    char desc[128];   // Holds the character class

    // Get the character and classification from the user
    wprintf(L"Enter a character and character class: ");
    fflush(stdout);
    wscanf(L"%lc %s", &c, desc);

    // Compute the type from the given class
    wctype_t t = wctype(desc);

    if (t == 0)
        // If the type is 0, it's an unknown class
        wprintf(L"Unknown character class: \"%s\"\n", desc);
    else {
        // Otherwise, let's test the character and see if its that
        // classification
        if (iswctype(c, t))
            wprintf(L"Yes! '%lc' is %s!\n", c, desc);
        else
            wprintf(L"Nope! '%lc' is not %s.\n", c, desc);
    }
}
```
:::

Output:

::: {#cb933 .sourceCode}
``` {.sourceCode .default}
Enter a character and character class: 5 digit
Yes! '5' is digit!

Enter a character and character class: b digit
Nope! 'b' is not digit.

Enter a character and character class: x alnum
Yes! 'x' is alnum!
```
:::

### See Also {#see-also-266 .unnumbered .unlisted}

[`wctype()`](wctype.html#man-wctype)

------------------------------------------------------------------------

## [31.14]{.header-section-number} `wctype()` {#man-wctype number="31.14"}

Helper function for `iswctype()`

### Synopsis {#synopsis-280 .unnumbered .unlisted}

::: {#cb934 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

wctype_t wctype(const char *property);
```
:::

### Description {#description-280 .unnumbered .unlisted}


This function returns an opaque value for the given `property` that is meant to be passed as the second argument to [`iswctype()`](wctype.html#man-iswctype).

> 此函数为给定的`property`返回一个不透明的值，该值旨在作为[`iswctype()`](wctype.html#man-iswctype)的第二个参数传递。

The returned value is of type `wctype_t`.

Valid properties in all locales are:

::: {#cb935 .sourceCode}
``` {.sourceCode .c}
"alnum"   "alpha"   "blank"   "cntrl"
"digit"   "graph"   "lower"   "print"
"punct"   "space"   "upper"   "xdigit"
```
:::


Other properties might be defined as determined by the `LC_CTYPE` category of the current locale.

> 其他属性可能会根据当前区域设置的`LC_CTYPE`类别来定义。


See the [`iswctype()` reference page](wctype.html#man-iswctype) for more usage details.

> 查看[`iswctype()`参考页面](wctype.html#man-iswctype)以获取更多使用细节。

### Return Value {#return-value-278 .unnumbered .unlisted}

Returns the `wctype_t` value associated with the given `property`.

If an invalid value is passed for `property`, returns `0`.

### Example {#example-282 .unnumbered .unlisted}


Test for a given character classification at when the classification isn't known at compile time:

> 测试在编译时不知道分类的情况下给定字符的分类：

::: {#cb936 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>  // for fflush(stdout)
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    wchar_t c;        // Holds a single wide character (to test)
    char desc[128];   // Holds the character class

    // Get the character and classification from the user
    wprintf(L"Enter a character and character class: ");
    fflush(stdout);
    wscanf(L"%lc %s", &c, desc);

    // Compute the type from the given class
    wctype_t t = wctype(desc);

    if (t == 0)
        // If the type is 0, it's an unknown class
        wprintf(L"Unknown character class: \"%s\"\n", desc);
    else {
        // Otherwise, let's test the character and see if its that
        // classification
        if (iswctype(c, t))
            wprintf(L"Yes! '%lc' is %s!\n", c, desc);
        else
            wprintf(L"Nope! '%lc' is not %s.\n", c, desc);
    }
}
```
:::

Output:

::: {#cb937 .sourceCode}
``` {.sourceCode .default}
Enter a character and character class: 5 digit
Yes! '5' is digit!

Enter a character and character class: b digit
Nope! 'b' is not digit.

Enter a character and character class: x alnum
Yes! 'x' is alnum!
```
:::

### See Also {#see-also-267 .unnumbered .unlisted}

[`iswctype()`](wctype.html#man-iswctype)

------------------------------------------------------------------------

## [31.15]{.header-section-number} `towlower()` {#man-towlower number="31.15"}

Convert an uppercase wide character to lowercase

### Synopsis {#synopsis-281 .unnumbered .unlisted}

::: {#cb938 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

wint_t towlower(wint_t wc);
```
:::

### Description {#description-281 .unnumbered .unlisted}


If the character is upper (i.e. `iswupper(c)` is true), this function returns the corresponding lowercase letter.

> 如果字符是大写的（即`iswupper(c)`为真），此函数将返回相应的小写字母。

Different locales might have different upper and lowercase letters.

### Return Value {#return-value-279 .unnumbered .unlisted}


If the letter `wc` is uppercase, a lowercase version of that letter will be returned according to the current locale.

> 如果字母`wc`是大写字母，根据当前的语言环境，将返回一个小写版本的字母。

If the letter is not uppercase, `wc` is returned unchanged.

### Example {#example-283 .unnumbered .unlisted}

::: {#cb939 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                  changing this char
    //                           v
    wprintf(L"%lc\n", towlower(L'B'));  // b (made lowercase!)
    wprintf(L"%lc\n", towlower(L'e'));  // e (unchanged)
    wprintf(L"%lc\n", towlower(L'!'));  // ! (unchanged)
}
```
:::

### See Also {#see-also-268 .unnumbered .unlisted}


[`tolower()`](ctype.html#man-tolower), [`towupper()`](wctype.html#man-towupper), [`iswlower()`](wctype.html#man-iswlower), [`iswupper()`](wctype.html#man-iswupper)

> [`tolower()`](ctype.html#man-tolower)，[`towupper()`](wctype.html#man-towupper)，[`iswlower()`](wctype.html#man-iswlower)，[`iswupper()`](wctype.html#man-iswupper)

------------------------------------------------------------------------

## [31.16]{.header-section-number} `towupper()` {#man-towupper number="31.16"}

Convert a lowercase wide character to uppercase

### Synopsis {#synopsis-282 .unnumbered .unlisted}

::: {#cb940 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

wint_t towupper(wint_t wc);
```
:::

### Description {#description-282 .unnumbered .unlisted}


If the character is lower (i.e. `iswlower(c)` is true), this function returns the corresponding uppercase letter.

> 如果字符是小写字母（即`iswlower(c)`为真），此函数将返回相应的大写字母。

Different locales might have different upper and lowercase letters.

### Return Value {#return-value-280 .unnumbered .unlisted}


If the letter `wc` is lowercase, an uppercase version of that letter will be returned according to the current locale.

> 如果字母“wc”是小写，根据当前区域设置将返回大写版本的字母。

If the letter is not lowercase, `wc` is returned unchanged.

### Example {#example-284 .unnumbered .unlisted}

::: {#cb941 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    //                  changing this char
    //                           v
    wprintf(L"%lc\n", towupper(L'B'));  // B (unchanged)
    wprintf(L"%lc\n", towupper(L'e'));  // E (made uppercase!)
    wprintf(L"%lc\n", towupper(L'!'));  // ! (unchanged)
}
```
:::

### See Also {#see-also-269 .unnumbered .unlisted}


[`toupper()`](ctype.html#man-toupper), [`towlower()`](wctype.html#man-towlower), [`iswlower()`](wctype.html#man-iswlower), [`iswupper()`](wctype.html#man-iswupper)

> [`toupper()`](ctype.html#man-toupper)，[`towlower()`](wctype.html#man-towlower)，[`iswlower()`](wctype.html#man-iswlower)，[`iswupper()`](wctype.html#man-iswupper)

------------------------------------------------------------------------

## [31.17]{.header-section-number} `towctrans()` {#man-towctrans number="31.17"}

Convert wide characters to upper or lowercase

### Synopsis {#synopsis-283 .unnumbered .unlisted}

::: {#cb942 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

wint_t towctrans(wint_t wc, wctrans_t desc);
```
:::

### Description {#description-283 .unnumbered .unlisted}


This is the Swiss Army knife of character conversion functions; it's all the other ones rolled into one. And by "all the other ones" I mean `towupper()` and `towlower()`, since those are the only ones there are.

> 这是一把瑞士军刀般的字符转换功能；它把所有其他功能都放在一起。我所说的“所有其他功能”指的是`towupper()`和`towlower()`，因为除此之外没有其他功能了。

You call it with something like this:

::: {#cb943 .sourceCode}
``` {.sourceCode .c}
if (towctrans(c, wctrans("toupper")))  // or "tolower"
```
:::

and it behaves just like you'd called:

::: {#cb944 .sourceCode}
``` {.sourceCode .c}
towupper(c);
```
:::


The difference is that you can specify the type of conversion you want to do as a string at runtime, which might be convenient.

> 你可以在运行时以字符串的形式指定要进行的转换类型，这可能很方便。

`towctrans()` relies on the return value from the [`wctrans()`](wctype.html#man-wctrans) call to get its work done.

  `towctrans()` call                   Hard-coded equivalent
  ------------------------------------ -----------------------
  `towctrans(c, wctrans("toupper"))`   `towupper(c)`
  `towctrans(c, wctrans("tolower"))`   `towlower(c)`


See the [`wctrans()` documentation](wctype.html#man-wctrans) for how that helper function works.

> 查看[`wctrans()`文档](wctype.html#man-wctrans)了解该辅助函数的工作原理。

### Return Value {#return-value-281 .unnumbered .unlisted}


Returns the character `wc` as if run through `towupper()` or `towlower()`, depending on the value of `desc`.

> 根据`desc`的值，将字符`wc`作为通过`towupper()`或`towlower()`处理后的结果返回。


If the character already matches the classification, it is returned as-is.

> 如果字符已经符合分类，则会原样返回。

### Example {#example-285 .unnumbered .unlisted}

::: {#cb945 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>  // for fflush(stdout)
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    wchar_t c;        // Holds a single wide character (to test)
    char desc[128];   // Holds the conversion type

    // Get the character and conversion type from the user
    wprintf(L"Enter a character and conversion type: ");
    fflush(stdout);
    wscanf(L"%lc %s", &c, desc);

    // Compute the type from the given conversion type
    wctrans_t t = wctrans(desc);

    if (t == 0)
        // If the type is 0, it's an unknown conversion type
        wprintf(L"Unknown conversion: \"%s\"\n", desc);
    else {
        // Otherwise, let's do the conversion
        wint_t result = towctrans(c, t);
        wprintf(L"'%lc' -> %s -> '%lc'\n", c, desc, result);
    }
}
```
:::

Output on my system:

::: {#cb946 .sourceCode}
``` {.sourceCode .default}
Enter a character and conversion type: b toupper
'b' -> toupper -> 'B'

Enter a character and conversion type: B toupper
'B' -> toupper -> 'B'

Enter a character and conversion type: B tolower
'B' -> tolower -> 'b'

Enter a character and conversion type: ! toupper
'!' -> toupper -> '!'
```
:::

### See Also {#see-also-270 .unnumbered .unlisted}


[`wctrans()`](wctype.html#man-wctrans), [`towupper()`](wctype.html#man-towupper), [`towlower()`](wctype.html#man-towlower)

> [`wctrans()`](wctype.html#man-wctrans)：将字符映射转换为另一个字符
[`towupper()`](wctype.html#man-towupper)：将字符转换为大写字符
[`towlower()`](wctype.html#man-towlower)：将字符转换为小写字符

------------------------------------------------------------------------

## [31.18]{.header-section-number} `wctrans()` {#man-wctrans number="31.18"}

Helper function for `towctrans()`

### Synopsis {#synopsis-284 .unnumbered .unlisted}

::: {#cb947 .sourceCode}
``` {.sourceCode .c}
#include <wctype.h>

wctrans_t wctrans(const char *property);
```
:::

### Description {#description-284 .unnumbered .unlisted}


This is a helper function for generating the second argument to [`towctrans()`](wctype.html#man-towctrans).

> 这是一个用于生成[`towctrans()`](wctype.html#man-towctrans)的第二个参数的辅助函数。

You can pass in one of two things for the `property`:

-   `toupper` to make `towctrans()` behave like `towupper()`
-   `tolower` to make `towctrans()` behave like `towlower()`

### Return Value {#return-value-282 .unnumbered .unlisted}


On success, returns a value that can be used as the `desc` argument to `towctrans()`.

> 如果成功，返回的值可以用作`towctrans()`的`desc`参数。

Otherwise, if the `property` isn't recognized, returns `0`.

### Example {#example-286 .unnumbered .unlisted}

::: {#cb948 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>  // for fflush(stdout)
#include <wchar.h>
#include <wctype.h>

int main(void)
{
    wchar_t c;        // Holds a single wide character (to test)
    char desc[128];   // Holds the conversion type

    // Get the character and conversion type from the user
    wprintf(L"Enter a character and conversion type: ");
    fflush(stdout);
    wscanf(L"%lc %s", &c, desc);

    // Compute the type from the given conversion type
    wctrans_t t = wctrans(desc);

    if (t == 0)
        // If the type is 0, it's an unknown conversion type
        wprintf(L"Unknown conversion: \"%s\"\n", desc);
    else {
        // Otherwise, let's do the conversion
        wint_t result = towctrans(c, t);
        wprintf(L"'%lc' -> %s -> '%lc'\n", c, desc, result);
    }
}
```
:::

Output on my system:

::: {#cb949 .sourceCode}
``` {.sourceCode .default}
Enter a character and conversion type: b toupper
'b' -> toupper -> 'B'

Enter a character and conversion type: B toupper
'B' -> toupper -> 'B'

Enter a character and conversion type: B tolower
'B' -> tolower -> 'b'

Enter a character and conversion type: ! toupper
'!' -> toupper -> '!'
```
:::

### See Also {#see-also-271 .unnumbered .unlisted}

[`towctrans()`](wctype.html#man-towctrans)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](wchar.html) \| [Contents](index.html) \| [Next](footnotes.html)
:::
