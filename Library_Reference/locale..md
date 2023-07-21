---
tip: translate by openai@2023-07-20 18:33:30
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](limits.html) \| [Contents](index.html) \| [Next](math.html)
:::

------------------------------------------------------------------------

# [12]{.header-section-number} `<locale.h>` locale handling {#locale number="12"}


  --------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------
无论如何，我们都会努力。
  Function                                       Description

  ---------------------------------------------- ---------------------------------------------------

> ---------------------------------------------- ---------------------------------------------------
简体中文：---------------------------------------------- ---------------------------------------------------
  [`setlocale()`](locale.html#man-setlocale)     Set the locale


  [`localeconv()`](locale.html#man-localeconv)   Get information about the current locale

> `localeconv()`（[locale.html#man-localeconv](locale.html#man-localeconv)）获取有关当前区域设置的信息

  --------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------
无论如何，我们都要努力前行。


The "locale" is the details of how the program should run given its physical location on the planet.

> "Locale"是给定程序在地球上的物理位置时，程序应如何运行的细节。


For example, in one locale, a unit of money might be printed as `$123`, and in another `€123`.

> 例如，在一个地区，货币可能会被打印为“$123”，而在另一个地区则是“€123”。

Or one locale might use ASCII encoding and another UTF-8 encoding.


By default, the program runs in the "C" locale. It has a basic set of characters with a single-byte encoding. If you try to print UTF-8 characters in the C locale, nothing will print. You have to switch to a proper locale.

> 默认情况下，程序以“C”地区设置运行。它具有具有单字节编码的基本字符集。如果您尝试在C地区设置中打印UTF-8字符，则不会打印任何内容。您必须切换到适当的地区设置。

------------------------------------------------------------------------

## [12.1]{.header-section-number} `setlocale()` {#man-setlocale number="12.1"}

Set the locale

### Synopsis {#synopsis-52 .unnumbered .unlisted}

::: {#cb232 .sourceCode}
``` {.sourceCode .c}
#include <locale.h>

char *setlocale(int category, const char *locale);
```
:::

### Description {#description-52 .unnumbered .unlisted}

Sets the `locale` for the given `category`.

Category is one of the following:


  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
简体中文
  Category                            Description

  ----------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ----------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------
简体中文：
----------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `LC_ALL`                            All of the following categories


  `LC_COLLATE`                        Affects the [`strcoll()`](stringref.html#man-strcoll) and [`strxfrm()`](stringref.html#man-strxfrm) functions

> `LC_COLLATE` 影响[`strcoll()`](stringref.html#man-strcoll)和[`strxfrm()`](stringref.html#man-strxfrm)函数。


  `LC_CTYPE`                          Affects the functions in [`<ctype.h>`](ctype.html#ctype)

> `LC_CTYPE` 影响 [`<ctype.h>`](ctype.html#ctype) 中的函数


  `LC_MONETARY`                       Affects the monetary information returned from [`localeconv()`](locale.html#man-localeconv)

> `LC_MONETARY` 影响从[`localeconv()`](locale.html#man-localeconv)返回的货币信息。


  `LC_NUMERIC`                        Affects the decimal point for formatted I/O and formatted string functions, and the monetary information returned from [`localeconv()`](locale.html#man-localeconv)

> `LC_NUMERIC` 影响格式化I/O和格式化字符串函数的小数点，以及从[`localeconv()`](locale.html#man-localeconv)返回的货币信息。


  `LC_TIME`                           Affects the [`strftime()`](time.html#man-strftime) and [`wcsftime()`](wchar.html#man-wcsftime) functions

> `LC_TIME` 影响[`strftime()`](time.html#man-strftime) 和 [`wcsftime()`](wchar.html#man-wcsftime) 函数。

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
简体中文


And there are three portable things you can pass in for `locale`; any other string passed in is implementation-defined and non-portable.

> 而且有三种可供传入`locale`的可移植物；任何其他传入的字符串都是由实现定义的，不可移植的。


  --------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------
简体中文
  Locale                              Description

  ----------------------------------- --------------------------------------------------------------------

> ----------------------------------- --------------------------------------------------------------------
简体中文：----------------------------------- --------------------------------------------------------------------
  `"C"`                               Set the program to the C locale


  `""`                                (Empty string) Set the program to the native locale of this system

> 将程序设置为此系统的本地化语言


  `NULL`                              Change nothing; just return the current locale

> 无变化；只返回当前区域设置


  Other                               Set the program to an implementation-defined locale

> 将程序设置为实现定义的区域设置

  --------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------
简体中文

The most common call, I'd wager, is this:

::: {#cb233 .sourceCode}
``` {.sourceCode .c}
// Set all locale settings to the local, native locale

setlocale(LC_ALL, "");
```
:::


Handily, `setlocale()` returns the locale that was just set, so you could see what the actual locale is on your system.

> 手动地，`setlocale()`会返回刚刚设置的区域设置，因此您可以查看系统上实际的区域设置。

### Return Value {#return-value-51 .unnumbered .unlisted}


On success, returns a pointer to the string representing the current locale. You may not modify this string, and it might be changed by subsequent calls to `setlocale()`.

> 如果成功，返回一个指向表示当前区域设置的字符串的指针。您不能修改此字符串，并且可能会被后续调用'setlocale（）'的函数所改变。

On failure, returns `NULL`.

### Example {#example-52 .unnumbered .unlisted}


Here we get the current locale. Then we set it to the native locale, and print out what that is.

> 在这里我们获取当前的区域设置。然后将其设置为本地区域设置，并打印出它是什么。

::: {#cb234 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <locale.h>

int main(void)
{
    char *loc;

    // Get the current locale
    loc = setlocale(LC_ALL, NULL);

    printf("Starting locale: %s\n", loc);

    // Set (and get) the locale to native locale
    loc = setlocale(LC_ALL, "");
    
    printf("Native locale: %s\n", loc);
}
```
:::

Output on my system:

::: {#cb235 .sourceCode}
``` {.sourceCode .default}
Starting locale: C
Native locale: en_US.UTF-8
```
:::


Note that my native locale (on a Linux box) might be different from what you see.

> 注意，我的本地化（在Linux系统上）可能与您看到的不同。


Nevertheless, I can explicitly set it on my system without a problem, or to any other locale I have installed:

> 然而，我可以毫无问题地在我的系统上明确设置它，或者设置到我已安装的任何其他区域设置。

::: {#cb236 .sourceCode startfrom="13"}
``` {.sourceCode .numberSource .c .numberLines}
    loc = setlocale(LC_ALL, "en_US.UTF-8");   // Non-portable
```
:::

But again, your system might have different locales defined.

### See Also {#see-also-48 .unnumbered .unlisted}


[`localeconv()`](locale.html#man-localeconv), [`strcoll()`](stringref.html#man-strcoll), [`strxfrm()`](stringref.html#man-strxfrm), [`strftime()`](time.html#man-strftime), [`wcsftime()`](wchar.html#man-wcsftime), [`printf()`](stdio.html#man-printf), [`scanf()`](stdio.html#man-scanf), [`<ctype.h>`](ctype.html#ctype)

> [`localeconv()`](locale.html#man-localeconv)：本地化转换
[`strcoll()`](stringref.html#man-strcoll)：字符串比较
[`strxfrm()`](stringref.html#man-strxfrm)：字符串转换
[`strftime()`](time.html#man-strftime)：格式化时间
[`wcsftime()`](wchar.html#man-wcsftime)：宽字符串格式化时间
[`printf()`](stdio.html#man-printf)：格式化输出
[`scanf()`](stdio.html#man-scanf)：格式化输入
[`<ctype.h>`](ctype.html#ctype)：字符类型

------------------------------------------------------------------------

## [12.2]{.header-section-number} `localeconv()` {#man-localeconv number="12.2"}

Get information about the current locale

### Synopsis {#synopsis-53 .unnumbered .unlisted}

::: {#cb237 .sourceCode}
``` {.sourceCode .c}
#include <locale.h>

struct lconv *localeconv(void);
```
:::

### Description {#description-53 .unnumbered .unlisted}


This function just returns a pointer to a `struct lconv`, but is still a bit of a powerhouse.

> 这个函数只是返回一个指向`struct lconv`的指针，但仍然是一个强大的功能。


The returned structure contains *tons* of information about the locale. Here are the fields of `struct lconv` and their meanings.

> 返回的结构包含有关区域设置的*大量*信息。以下是`struct lconv`的字段及其含义。


First, some conventions. In the field names, below, a `_p_` means "positive", and `_n_` means "negative", and `int_` means "international". Though a lot of these are type `char` or `char*`, most (or the strings they point to) are actually treated as integers[^21^](footnotes.html#fn21){#fnref21 .footnote-ref role="doc-noteref"}.

> 首先，一些约定。在下面的字段名称中，`_p_`表示“正”，`_n_`表示“负”，`int_`表示“国际”。尽管大多数是`char`或`char*`类型，但大多数（或它们指向的字符串）实际上被视为整数[^21^](footnotes.html#fn21){#fnref21 .footnote-ref role="doc-noteref"}。


Before we go further, know that `CHAR_MAX` (from `<limits.h>`) is the maximum value that can be held in a `char`. And that many of the following `char` values use that to indicate the value isn't available in the given locale.

> 在我们继续之前，要知道`CHAR_MAX`（来自`<limits.h>`）是可以存储在`char`中的最大值。而且许多下面的`char`值使用它来表示在给定的区域设置中没有可用的值。


  -------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------
简体中文
  Field                       Description

  --------------------------- ---------------------------------------------------------------------------------------------------------

> --------------------------- ---------------------------------------------------------------------------------------------------------
空白

  `char *mon_decimal_point`   Decimal pointer character for money, e.g. `"."`.

> 字符指针，用于表示金钱的小数点，例如“。”


  `char *mon_thousands_sep`   Thousands separator character for money, e.g. `","`.

> 字符指针mon_thousands_sep，表示货币千位分隔符，例如“，”。

  `char *mon_grouping`        Grouping description for money (see below).


  `char *positive_sign`       Positive sign for money, e.g. `"+"` or `""`.

> 字符指针positive_sign：用于货币的正号，例如“+”或“”。

  `char *negative_sign`       Negative sign for money, e.g. `"-"`.

  `char *currency_symbol`     Currency symbol, e.g. `"$"`.


  `char frac_digits`          When printing monetary amounts, how many digits to print past the decimal point, e.g. `2`.

> 当打印货币金额时，要在小数点后打印多少位数字，例如`2`。


  `char p_cs_precedes`        `1` if the `currency_symbol` comes before the value for a non-negative monetary amount, `0` if after.

> `char p_cs_precedes`：如果货币符号出现在非负货币金额之前，则为`1`；如果出现在之后，则为`0`。


  `char n_cs_precedes`        `1` if the `currency_symbol` comes before the value for a negative monetary amount, `0` if after.

> 如果货币符号在负金额之前，则为1；如果在之后，则为0。


  `char p_sep_by_space`       Determines the separation of the `currency symbol` from the value for non-negative amounts (see below).

> `char p_sep_by_space`决定了非负金额的货币符号和值之间的分隔（见下文）。


  `char n_sep_by_space`       Determines the separation of the `currency symbol` from the value for negative amounts (see below).

> `char n_sep_by_space`决定负数金额的货币符号与值之间的分隔（见下文）。


  `char p_sign_posn`          Determines the `positive_sign` position for non-negative values.

> `char p_sign_posn`：用于确定非负值的正号位置。


  `char p_sign_posn`          Determines the `positive_sign` position for negative values.

> `char p_sign_posn`：用于确定负值的`正号`位置。


  `char *int_curr_symbol`     International currency symbol, e.g. `"USD "`.

> 字符指针int_curr_symbol：国际货币符号，例如“USD”。

  `char int_frac_digits`      International value for `frac_digits`.

  `char int_p_cs_precedes`    International value for `p_cs_precedes`.

  `char int_n_cs_precedes`    International value for `n_cs_precedes`.

  `char int_p_sep_by_space`   International value for `p_sep_by_space`.

  `char int_n_sep_by_space`   International value for `n_sep_by_space`.

  `char int_p_sign_posn`      International value for `p_sign_posn`.

  `char int_n_sign_posn`      International value for `n_sign_posn`.

  -------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------
简体中文


Even though many of these have `char` type, the value stored within is meant to be accessed as an integer.

> 即使许多这些都有`char`类型，存储在其中的值也应该作为整数来访问。


All the `sep_by_space` variants deal with spacing around the currency sign. Valid values are:

> 所有的`sep_by_space`变体都处理货币符号周围的空格。有效值为：


  -----------------------------------------------------------------------------------------------------------------------------------------------------------------

> -----------------------------------------------------------------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。
        Value       Description

  ----------------- -----------------------------------------------------------------------------------------------------------------------------------------------

> ----------------- -----------------------------------------------------------------------------------------------------------------------------------------------
简体中文：----------------- -----------------------------------------------------------------------------------------------------------------------------------------------
         `0`        No space between currency symbol and value.

         `1`        Separate the currency symbol (and sign, if any) from the value with a space.

         `2`        Separate the sign symbol from the currency symbol (if adjacent) with a space, otherwise separate the sign symbol from the value with a space.

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------

> -----------------------------------------------------------------------------------------------------------------------------------------------------------------
无论如何，我们都要努力。

The `sign_posn` variants are determined by the following values:

   Value  Description
  ------- ----------------------------------------------------------------
    `0`   Put parens around the value and the currency symbol.
    `1`   Put the sign string in front of the currency symbol and value.
    `2`   Put the sign string after the currency symbol and value.
    `3`   Put the sign string directly in front of the currency symbol.
    `4`   Put the sign string directly behind the currency symbol.

### Return Value {#return-value-52 .unnumbered .unlisted}

Returns a pointer to the structure containing the locale information.

The program may not modify this structure.


Subsequent calls to `localeconv()` may overwrite this structure, as might calls to `setlocale()` with `LC_ALL`, `LC_MONETARY`, or `LC_NUMERIC`.

> 后续调用`localeconv()`可能会覆盖这个结构，调用`setlocale()`的`LC_ALL`、`LC_MONETARY`或`LC_NUMERIC`也可能会这样。

### Example {#example-53 .unnumbered .unlisted}

Here's a program to print the locale information for the native locale.

::: {#cb238 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <locale.h>
#include <limits.h>  // for CHAR_MAX

void print_grouping(char *mg)
{
    int done = 0;

    while (!done) {
        if (*mg == CHAR_MAX)
            printf("CHAR_MAX ");
        else
            printf("%c ", *mg + '0');
        done = *mg == CHAR_MAX || *mg == 0;
        mg++;
    }
}

int main(void)
{
    setlocale(LC_ALL, "");

    struct lconv *lc = localeconv();

    printf("mon_decimal_point : %s\n", lc->mon_decimal_point);
    printf("mon_thousands_sep : %s\n", lc->mon_thousands_sep);
    printf("mon_grouping      : ");
    print_grouping(lc->mon_grouping);
    printf("\n");
    printf("positive_sign     : %s\n", lc->positive_sign);
    printf("negative_sign     : %s\n", lc->negative_sign);
    printf("currency_symbol   : %s\n", lc->currency_symbol);
    printf("frac_digits       : %c\n", lc->frac_digits);
    printf("p_cs_precedes     : %c\n", lc->p_cs_precedes);
    printf("n_cs_precedes     : %c\n", lc->n_cs_precedes);
    printf("p_sep_by_space    : %c\n", lc->p_sep_by_space);
    printf("n_sep_by_space    : %c\n", lc->n_sep_by_space);
    printf("p_sign_posn       : %c\n", lc->p_sign_posn);
    printf("p_sign_posn       : %c\n", lc->p_sign_posn);
    printf("int_curr_symbol   : %s\n", lc->int_curr_symbol);
    printf("int_frac_digits   : %c\n", lc->int_frac_digits);
    printf("int_p_cs_precedes : %c\n", lc->int_p_cs_precedes);
    printf("int_n_cs_precedes : %c\n", lc->int_n_cs_precedes);
    printf("int_p_sep_by_space: %c\n", lc->int_p_sep_by_space);
    printf("int_n_sep_by_space: %c\n", lc->int_n_sep_by_space);
    printf("int_p_sign_posn   : %c\n", lc->int_p_sign_posn);
    printf("int_n_sign_posn   : %c\n", lc->int_n_sign_posn);
}
```
:::

Output on my system:

::: {#cb239 .sourceCode}
``` {.sourceCode .default}
mon_decimal_point : .
mon_thousands_sep : ,
mon_grouping      : 3 3 0 
positive_sign     : 
negative_sign     : -
currency_symbol   : $
frac_digits       : 2
p_cs_precedes     : 1
n_cs_precedes     : 1
p_sep_by_space    : 0
n_sep_by_space    : 0
p_sign_posn       : 1
p_sign_posn       : 1
int_curr_symbol   : USD 
int_frac_digits   : 2
int_p_cs_precedes : 1
int_n_cs_precedes : 1
int_p_sep_by_space: 1
int_n_sep_by_space: 1
int_p_sign_posn   : 1
int_n_sign_posn   : 1
```
:::

### See Also {#see-also-49 .unnumbered .unlisted}

[`setlocale()`](locale.html#man-setlocale)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](limits.html) \| [Contents](index.html) \| [Next](math.html)
:::
