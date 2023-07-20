---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](complex.html) \| [Contents](index.html) \| [Next](errno.html)
:::

------------------------------------------------------------------------

# [5]{.header-section-number} `<ctype.h>` Character Classification and Conversion {#ctype number="5"}

  -----------------------------------------------------------------------------------------------
  Function                                  Description
  ----------------------------------------- -----------------------------------------------------
  [`isalnum()`](ctype.html#man-isalnum)     Tests if a character is alphabetic or is a digit

  [`isalpha()`](ctype.html#man-isalpha)     Returns true if a character is alphabetic

  [`isblank()`](ctype.html#man-isblank)     Tests if a character is word-separating whitespace

  [`iscntrl()`](ctype.html#man-iscntrl)     Test if a character is a control character

  [`isdigit()`](ctype.html#man-isdigit)     Tests if a character is a digit

  [`isgraph()`](ctype.html#man-isgraph)     Tests if the character is printable and not a space

  [`islower()`](ctype.html#man-islower)     Tests if a character is lowercase

  [`isprint()`](ctype.html#man-isprint)     Tests if a character is printable

  [`ispunct()`](ctype.html#man-ispunct)     Test if a character is punctuation

  [`isspace()`](ctype.html#man-isspace)     Test if a character is whitespace

  [`isupper()`](ctype.html#man-isupper)     Tests if a character is uppercase

  [`isxdigit()`](ctype.html#man-isxdigit)   Tests if a character is a hexadecimal digit

  [`tolower()`](ctype.html#man-tolower)     Convert a letter to lowercase

  [`toupper()`](ctype.html#man-toupper)     Convert a letter to uppercase
  -----------------------------------------------------------------------------------------------

This collection of macros is good for testing characters to see if they're of a certain class, such as alphabetic, numeric, control characters, etc.

Surprisingly, they take `int` arguments instead of some kind of `char`. This is so you can feed `EOF` in for convenience if you have an integer representation of that. If not `EOF`, the value passed in has to be representable in an `unsigned char`. Otherwise it's (dun dun DUUNNNN) undefined behavior. So you can forget about passing in your UTF-8 multibyte characters.

You can portably avoid this undefined behavior by casting the arguments to these functions to `(unsigned char)`. This is irksome and ugly, admittedly. The values in the basic character set are all safe to use since they're positive values that fit into an `unsigned char`.

Also, the behavior of these functions varies based on locale.

In many of the pages in this section, I give some examples. These are from the "C" locale, and might vary if you've set a different locale.

Note that wide characters have their own set of classification functions, so don't try to use these on `wchar_t`s. Or *else*!

------------------------------------------------------------------------

## [5.1]{.header-section-number} `isalnum()` {#man-isalnum number="5.1"}

Tests if a character is alphabetic or is a digit

### Synopsis {#synopsis-25 .unnumbered .unlisted}

::: {#cb145 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isalnum(int c);
```
:::

### Description {#description-25 .unnumbered .unlisted}

Tests if a character is alphabetic (`A`-`Z` or `a`-`z`) or a digit (`0`-`9`).

Is equivalent to:

::: {#cb146 .sourceCode}
``` {.sourceCode .c}
isalpha(c) || isdigit(c)
```
:::

### Return Value {#return-value-25 .unnumbered .unlisted}

Returns true if a character is alphabetic (`A`-`Z` or `a`-`z`) or a digit (`0`-`9`).

### Example {#example-25 .unnumbered .unlisted}

::: {#cb147 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isalnum('a')? "yes": "no");  // yes
    printf("%s\n", isalnum('B')? "yes": "no");  // yes
    printf("%s\n", isalnum('5')? "yes": "no");  // yes
    printf("%s\n", isalnum('?')? "yes": "no");  // no
}
```
:::

### See Also {#see-also-22 .unnumbered .unlisted}

[`isalpha()`](ctype.html#man-isalpha), [`isdigit()`](ctype.html#man-isdigit)

------------------------------------------------------------------------

## [5.2]{.header-section-number} `isalpha()` {#man-isalpha number="5.2"}

Returns true if a character is alphabetic

### Synopsis {#synopsis-26 .unnumbered .unlisted}

::: {#cb148 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isalpha(int c);
```
:::

### Description {#description-26 .unnumbered .unlisted}

Returns true for alphabetic characters (`A`-`Z` or `a`-`z`).

Technically (and in the "C" locale) equivalent to:

::: {#cb149 .sourceCode}
``` {.sourceCode .c}
isupper(c) || islower(c)
```
:::

Extra super technically, because I know you're dying for this to be extra unnecessarily complex, it can also include some locale-specific characters for which this is true:

::: {#cb150 .sourceCode}
``` {.sourceCode .c}
!iscntrl(c) && !isdigit(c) && !ispunct(c) && !isspace(c)
```
:::

and this is true:

::: {#cb151 .sourceCode}
``` {.sourceCode .c}
isupper(c) || islower(c)
```
:::

### Return Value {#return-value-26 .unnumbered .unlisted}

Returns true for alphabetic characters (`A`-`Z` or `a`-`z`).

Or for any of the other crazy stuff in the description, above.

### Example {#example-26 .unnumbered .unlisted}

::: {#cb152 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isalpha('a')? "yes": "no");  // yes
    printf("%s\n", isalpha('B')? "yes": "no");  // yes
    printf("%s\n", isalpha('5')? "yes": "no");  // no
    printf("%s\n", isalpha('?')? "yes": "no");  // no
}
```
:::

### See Also {#see-also-23 .unnumbered .unlisted}

[`isalnum()`](ctype.html#man-isalnum)

------------------------------------------------------------------------

## [5.3]{.header-section-number} `isblank()` {#man-isblank number="5.3"}

Tests if a character is word-separating whitespace

### Synopsis {#synopsis-27 .unnumbered .unlisted}

::: {#cb153 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isblank(int c);
```
:::

### Description {#description-27 .unnumbered .unlisted}

True if the character is a whitespace character used to separate words in a single line.

For example, space (`' '`) or horizontal tab (`'\t'`). Other locales might define other blank characters.

### Return Value {#return-value-27 .unnumbered .unlisted}

Returns true if the character is a whitespace character used to separate words in a single line.

### Example {#example-27 .unnumbered .unlisted}

::: {#cb154 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isblank(' ')? "yes": "no");   // yes
    printf("%s\n", isblank('\t')? "yes": "no");  // yes
    printf("%s\n", isblank('\n')? "yes": "no");  // no
    printf("%s\n", isblank('a')? "yes": "no");   // no
    printf("%s\n", isblank('?')? "yes": "no");   // no
}
```
:::

### See Also {#see-also-24 .unnumbered .unlisted}

[`isspace()`](ctype.html#man-isspace)

------------------------------------------------------------------------

## [5.4]{.header-section-number} `iscntrl()` {#man-iscntrl number="5.4"}

Test if a character is a control character

### Synopsis {#synopsis-28 .unnumbered .unlisted}

::: {#cb155 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int iscntrl(int c);
```
:::

### Description {#description-28 .unnumbered .unlisted}

A *control character* is a locale-specific non-printing character.

For the "C" locale, this means control characters are in the range 0x00 to 0x1F (the character right before SPACE) and 0x7F (the DEL character).

Basically if it's not an ASCII (or Unicode less than 128) printable character, it's a control character in the "C" locale.

### Return Value {#return-value-28 .unnumbered .unlisted}

Returns true if `c` is a control character.

### Example {#example-28 .unnumbered .unlisted}

::: {#cb156 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", iscntrl('\t')? "yes": "no");  // yes (tab)
    printf("%s\n", iscntrl('\n')? "yes": "no");  // yes (newline)
    printf("%s\n", iscntrl('\r')? "yes": "no");  // yes (return)
    printf("%s\n", iscntrl('\a')? "yes": "no");  // yes (bell)
    printf("%s\n", iscntrl(' ')? "yes": "no");   // no
    printf("%s\n", iscntrl('a')? "yes": "no");   // no
    printf("%s\n", iscntrl('?')? "yes": "no");   // no
}
```
:::

### See Also {#see-also-25 .unnumbered .unlisted}

[`isgraph()`](ctype.html#man-isgraph), [`isprint()`](ctype.html#man-isprint)

------------------------------------------------------------------------

## [5.5]{.header-section-number} `isdigit()` {#man-isdigit number="5.5"}

Tests if a character is a digit

### Synopsis {#synopsis-29 .unnumbered .unlisted}

::: {#cb157 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isdigit(int c);
```
:::

### Description {#description-29 .unnumbered .unlisted}

Tests if `c` is a digit in the range `0`-`9`.

### Return Value {#return-value-29 .unnumbered .unlisted}

Returns true if the character is a digit, unsurprisingly.

### Example {#example-29 .unnumbered .unlisted}

::: {#cb158 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isdigit('0')? "yes": "no");   // yes
    printf("%s\n", isdigit('5')? "yes": "no");   // yes
    printf("%s\n", isdigit('a')? "yes": "no");   // no
    printf("%s\n", isdigit('B')? "yes": "no");   // no
    printf("%s\n", isdigit('?')? "yes": "no");   // no
}
```
:::

### See Also {#see-also-26 .unnumbered .unlisted}

[`isalnum()`](ctype.html#man-isalnum), [`isxdigit()`](ctype.html#man-isxdigit)

------------------------------------------------------------------------

## [5.6]{.header-section-number} `isgraph()` {#man-isgraph number="5.6"}

Tests if the character is printable and not a space

### Synopsis {#synopsis-30 .unnumbered .unlisted}

::: {#cb159 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isgraph(int c);
```
:::

### Description {#description-30 .unnumbered .unlisted}

Tests if `c` is any printable character that isn't a space (`' '`).

### Return Value {#return-value-30 .unnumbered .unlisted}

Returns true if `c` is any printable character that isn't a space (`' '`).

### Example {#example-30 .unnumbered .unlisted}

::: {#cb160 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isgraph('0')? "yes": "no");   // yes
    printf("%s\n", isgraph('a')? "yes": "no");   // yes
    printf("%s\n", isgraph('B')? "yes": "no");   // yes
    printf("%s\n", isgraph('?')? "yes": "no");   // yes
    printf("%s\n", isgraph(' ')? "yes": "no");   // no
    printf("%s\n", isgraph('\n')? "yes": "no");  // no
}
```
:::

### See Also {#see-also-27 .unnumbered .unlisted}

[`iscntrl()`](ctype.html#man-iscntrl), [`isprint()`](ctype.html#man-isprint)

------------------------------------------------------------------------

## [5.7]{.header-section-number} `islower()` {#man-islower number="5.7"}

Tests if a character is lowercase

### Synopsis {#synopsis-31 .unnumbered .unlisted}

::: {#cb161 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int islower(int c);
```
:::

### Description {#description-31 .unnumbered .unlisted}

Tests if a character is lowercase, in the range `a`-`z`.

In other locales, there could be other lowercase characters. In all cases, to be lowercase, the following must be true:

::: {#cb162 .sourceCode}
``` {.sourceCode .c}
!iscntrl(c) && !isdigit(c) && !ispunct(c) && !isspace(c)
```
:::

### Return Value {#return-value-31 .unnumbered .unlisted}

Returns true if the character is lowercase.

### Example {#example-31 .unnumbered .unlisted}

::: {#cb163 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", islower('c')? "yes": "no");   // yes
    printf("%s\n", islower('0')? "yes": "no");   // no
    printf("%s\n", islower('B')? "yes": "no");   // no
    printf("%s\n", islower('?')? "yes": "no");   // no
    printf("%s\n", islower(' ')? "yes": "no");   // no
}
```
:::

### See Also {#see-also-28 .unnumbered .unlisted}

[`isupper()`](ctype.html#man-isupper), [`isalpha()`](ctype.html#man-isalpha), [`toupper()`](ctype.html#man-toupper), [`tolower()`](ctype.html#man-tolower)

------------------------------------------------------------------------

## [5.8]{.header-section-number} `isprint()` {#man-isprint number="5.8"}

Tests if a character is printable

### Synopsis {#synopsis-32 .unnumbered .unlisted}

::: {#cb164 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isprint(int c);
```
:::

### Description {#description-32 .unnumbered .unlisted}

Tests if a character is printable, including space (`' '`). So like `isgraph()`, except space isn't left out in the cold.

### Return Value {#return-value-32 .unnumbered .unlisted}

Returns true if the character is printable, including space (`' '`).

### Example {#example-32 .unnumbered .unlisted}

::: {#cb165 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isprint('c')? "yes": "no");   // yes
    printf("%s\n", isprint('0')? "yes": "no");   // yes
    printf("%s\n", isprint(' ')? "yes": "no");   // yes
    printf("%s\n", isprint('\r')? "yes": "no");  // no
}
```
:::

### See Also {#see-also-29 .unnumbered .unlisted}

[`isgraph()`](ctype.html#man-isgraph), [`iscntrl()`](ctype.html#man-iscntrl)

------------------------------------------------------------------------

## [5.9]{.header-section-number} `ispunct()` {#man-ispunct number="5.9"}

Test if a character is punctuation

### Synopsis {#synopsis-33 .unnumbered .unlisted}

::: {#cb166 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int ispunct(int c);
```
:::

### Description {#description-33 .unnumbered .unlisted}

Tests if a character is punctuation.

In the "C" locale, this means:

::: {#cb167 .sourceCode}
``` {.sourceCode .c}
!isspace(c) && !isalnum(c)
```
:::

In other locales, there could be other punctuation characters (but they also can't be space or alphanumeric).

### Return Value {#return-value-33 .unnumbered .unlisted}

True if the character is punctuation.

### Example {#example-33 .unnumbered .unlisted}

::: {#cb168 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", ispunct(',')? "yes": "no");   // yes
    printf("%s\n", ispunct('!')? "yes": "no");   // yes
    printf("%s\n", ispunct('c')? "yes": "no");   // no
    printf("%s\n", ispunct('0')? "yes": "no");   // no
    printf("%s\n", ispunct(' ')? "yes": "no");   // no
    printf("%s\n", ispunct('\n')? "yes": "no");  // no
}
```
:::

### See Also {#see-also-30 .unnumbered .unlisted}

[`isspace()`](ctype.html#man-isspace), [`isalnum()`](ctype.html#man-isalnum)

------------------------------------------------------------------------

## [5.10]{.header-section-number} `isspace()` {#man-isspace number="5.10"}

Test if a character is whitespace

### Synopsis {#synopsis-34 .unnumbered .unlisted}

::: {#cb169 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isspace(int c);
```
:::

### Description {#description-34 .unnumbered .unlisted}

Tests if `c` is a whitespace character. These are:

-   Space (`' '`)
-   Formfeed (`'\f'`)
-   Newline (`'\n'`)
-   Carriage Return (`'\r'`)
-   Horizontal Tab (`'\t'`)
-   Vertical Tab (`'\v'`)

Other locales might specify other whitespace characters. `isalnum()` is false for all whitespace characters.

### Return Value {#return-value-34 .unnumbered .unlisted}

True if the character is whitespace.

### Example {#example-34 .unnumbered .unlisted}

::: {#cb170 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isspace(' ')? "yes": "no");   // yes
    printf("%s\n", isspace('\n')? "yes": "no");  // yes
    printf("%s\n", isspace('\t')? "yes": "no");  // yes
    printf("%s\n", isspace(',')? "yes": "no");   // no
    printf("%s\n", isspace('!')? "yes": "no");   // no
    printf("%s\n", isspace('c')? "yes": "no");   // no
}
```
:::

### See Also {#see-also-31 .unnumbered .unlisted}

[`isblank()`](ctype.html#man-isblank)

------------------------------------------------------------------------

## [5.11]{.header-section-number} `isupper()` {#man-isupper number="5.11"}

Tests if a character is uppercase

### Synopsis {#synopsis-35 .unnumbered .unlisted}

::: {#cb171 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isupper(int c);
```
:::

### Description {#description-35 .unnumbered .unlisted}

Tests if a character is uppercase, in the range `A`-`Z`.

In other locales, there could be other uppercase characters. In all cases, to be uppercase, the following must be true:

::: {#cb172 .sourceCode}
``` {.sourceCode .c}
!iscntrl(c) && !isdigit(c) && !ispunct(c) && !isspace(c)
```
:::

### Return Value {#return-value-35 .unnumbered .unlisted}

Returns true if the character is uppercase.

### Example {#example-35 .unnumbered .unlisted}

::: {#cb173 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isupper('B')? "yes": "no");   // yes
    printf("%s\n", isupper('c')? "yes": "no");   // no
    printf("%s\n", isupper('0')? "yes": "no");   // no
    printf("%s\n", isupper('?')? "yes": "no");   // no
    printf("%s\n", isupper(' ')? "yes": "no");   // no
}
```
:::

### See Also {#see-also-32 .unnumbered .unlisted}

[`islower()`](ctype.html#man-islower), [`isalpha()`](ctype.html#man-isalpha), [`toupper()`](ctype.html#man-toupper), [`tolower()`](ctype.html#man-tolower)

------------------------------------------------------------------------

## [5.12]{.header-section-number} `isxdigit()` {#man-isxdigit number="5.12"}

Tests if a character is a hexadecimal digit

### Synopsis {#synopsis-36 .unnumbered .unlisted}

::: {#cb174 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int isxdigit(int c);
```
:::

### Description {#description-36 .unnumbered .unlisted}

Returns true if the character is a hexadecimal digit. Namely if it's `0`-`9`, `a`-`f`, or `A`-`F`.

### Return Value {#return-value-36 .unnumbered .unlisted}

True if the character is a hexadecimal digit.

### Example {#example-36 .unnumbered .unlisted}

::: {#cb175 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             testing this char
    //                      v
    printf("%s\n", isxdigit('B')? "yes": "no");   // yes
    printf("%s\n", isxdigit('c')? "yes": "no");   // yes
    printf("%s\n", isxdigit('2')? "yes": "no");   // yes
    printf("%s\n", isxdigit('G')? "yes": "no");   // no
    printf("%s\n", isxdigit('?')? "yes": "no");   // no
}
```
:::

### See Also {#see-also-33 .unnumbered .unlisted}

[`isdigit()`](ctype.html#man-isdigit)

------------------------------------------------------------------------

## [5.13]{.header-section-number} `tolower()` {#man-tolower number="5.13"}

Convert a letter to lowercase

### Synopsis {#synopsis-37 .unnumbered .unlisted}

::: {#cb176 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int tolower(int c);
```
:::

### Description {#description-37 .unnumbered .unlisted}

If the character is uppercase (i.e. `isupper(c)` is true), this function returns the corresponding lowercase letter.

Different locales might have different upper- and lowercase letters.

### Return Value {#return-value-37 .unnumbered .unlisted}

Returns the lowercase value for an uppercase letter. If the letter isn't uppercase, returns it unchanged.

### Example {#example-37 .unnumbered .unlisted}

::: {#cb177 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             changing this char
    //                      v
    printf("%c\n", tolower('B'));  // b (made lowercase!)
    printf("%c\n", tolower('e'));  // e (unchanged)
    printf("%c\n", tolower('!'));  // ! (unchanged)
}
```
:::

### See Also {#see-also-34 .unnumbered .unlisted}

[`toupper()`](ctype.html#man-toupper), [`islower()`](ctype.html#man-islower), [`isupper()`](ctype.html#man-isupper)

------------------------------------------------------------------------

## [5.14]{.header-section-number} `toupper()` {#man-toupper number="5.14"}

Convert a letter to uppercase

### Synopsis {#synopsis-38 .unnumbered .unlisted}

::: {#cb178 .sourceCode}
``` {.sourceCode .c}
#include <ctype.h>

int toupper(int c);
```
:::

### Description {#description-38 .unnumbered .unlisted}

If the character is lower (i.e. `islower(c)` is true), this function returns the corresponding uppercase letter.

Different locales might have different upper- and lowercase letters.

### Return Value {#return-value-38 .unnumbered .unlisted}

Returns the uppercase value for a lowercase letter. If the letter isn't lowercase, returns it unchanged.

### Example {#example-38 .unnumbered .unlisted}

::: {#cb179 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int main(void)
{
    //             changing this char
    //                      v
    printf("%c\n", toupper('B'));  // B (unchanged)
    printf("%c\n", toupper('e'));  // E (made uppercase!)
    printf("%c\n", toupper('!'));  // ! (unchanged)
}
```
:::

### See Also {#see-also-35 .unnumbered .unlisted}

[`tolower()`](ctype.html#man-tolower), [`islower()`](ctype.html#man-islower), [`isupper()`](ctype.html#man-isupper)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](complex.html) \| [Contents](index.html) \| [Next](errno.html)
:::
