---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](float.html) \| [Contents](index.html) \| [Next](iso646.html)
:::

------------------------------------------------------------------------

# [9]{.header-section-number} `<inttypes.h>` More Integer Conversions {#inttypes number="9"}

  --------------------------------------------------------------------------------------------------
  Function                                       Description
  ---------------------------------------------- ---------------------------------------------------
  [`imaxabs()`](inttypes.html#man-imaxabs)       Compute the absolute value of an `intmax_t`

  [`imaxdiv()`](inttypes.html#man-imaxdiv)       Compute the quotient and remainder of `intmax_t`s

  [`strtoimax()`](inttypes.html#man-strtoimax)   Convert strings to type `intmax_t`

  [`strtoumax()`](inttypes.html#man-strtoimax)   Convert strings to type `uintmax_t`

  [`wcstoimax()`](inttypes.html#man-wcstoimax)   Convert wide strings to type `intmax_t`

  [`wcstoumax()`](inttypes.html#man-wcstoimax)   Convert wide strings to type `uintmax_t`
  --------------------------------------------------------------------------------------------------

This header does conversions to maximum sized integers, division with maximum sized integers, and also provides format specifiers for [`printf()`](stdio.html#man-printf) and [`scanf()`](stdio.html#man-scanf) for a variety of types defined in [`<stdint.h>`](stdint.html#stdint).

The header [`<stdint.h>`](stdint.html#stdint) is included by this one.

## [9.1]{.header-section-number} Macros {#macros-1 number="9.1"}

These are to help with [`printf()`](stdio.html#man-printf) and [`scanf()`](stdio.html#man-scanf) when you use a type such as `int_least16_t`... what format specifiers do you use?

Let's start with `printf()`---all these macros start with `PRI` and then are followed by the format specifier you'd typically use for that type. Lastly, the number of bits is added on.

For example, the format specifier for a 64-bit integer is `PRId64`---the `d` is because you usually print integers with `"%d"`.

An unsigned 16-bit integer could be printed with `PRIu16`.

These macros expand to string literals. We can take advantage of the fact that C automatically concatenates neighboring string literals and use these specifiers like this:

::: {#cb213 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>     // for printf()
#include <inttypes.h>

int main(void)
{
    int16_t x = 32;

    printf("The value is %" PRId16 "!\n", x);
}
```
:::

There's nothing magical happening on line 8, above. Indeed, if I print out the value of the macro:

::: {#cb214 .sourceCode}
``` {.sourceCode .c}
printf("%s\n", PRId16);
```
:::

we get this on my system:

::: {#cb215 .sourceCode}
``` {.sourceCode .default}
hd
```
:::

which is a `printf()` format specifier meaning "short signed integer" .

So back to line 8, after string literal concatenation, it's just as if I'd typed:

::: {#cb216 .sourceCode startfrom="8"}
``` {.sourceCode .numberSource .c .numberLines}
    printf("The value is %hd!\n", x);
```
:::

Here's a table of all the macros you can use for `printf()` format specifiers... substitute the number of bits for *N*, usually 8, 16, 32, or 64.

  ----------- ---------------- --------------- ----------- -----------
  `PRId`*N*   `PRIdLEAST`*N*   `PRIdFAST`*N*   `PRIdMAX`   `PRIdPTR`
  `PRIi`*N*   `PRIiLEAST`*N*   `PRIiFAST`*N*   `PRIiMAX`   `PRIiPTR`
  `PRIo`*N*   `PRIoLEAST`*N*   `PRIoFAST`*N*   `PRIoMAX`   `PRIoPTR`
  `PRIu`*N*   `PRIuLEAST`*N*   `PRIuFAST`*N*   `PRIuMAX`   `PRIuPTR`
  `PRIx`*N*   `PRIxLEAST`*N*   `PRIxFAST`*N*   `PRIxMAX`   `PRIxPTR`
  `PRIX`*N*   `PRIXLEAST`*N*   `PRIXFAST`*N*   `PRIXMAX`   `PRIXPTR`
  ----------- ---------------- --------------- ----------- -----------

Note again how the lowercase center letter represents the usual format specifiers you'd pass to `printf()`: `d`, `i`, `o`, `u`, `x`, and `X`.

And we have a similar set of macros for `scanf()` for reading in these various types:

  ----------- ---------------- --------------- ----------- -----------
  `SCNd`*N*   `SCNdLEAST`*N*   `SCNdFAST`*N*   `SCNdMAX`   `SCNdPTR`
  `SCNi`*N*   `SCNiLEAST`*N*   `SCNiFAST`*N*   `SCNiMAX`   `SCNiPTR`
  `SCNo`*N*   `SCNoLEAST`*N*   `SCNoFAST`*N*   `SCNoMAX`   `SCNoPTR`
  `SCNu`*N*   `SCNuLEAST`*N*   `SCNuFAST`*N*   `SCNuMAX`   `SCNuPTR`
  `SCNx`*N*   `SCNxLEAST`*N*   `SCNxFAST`*N*   `SCNxMAX`   `SCNxPTR`
  ----------- ---------------- --------------- ----------- -----------

The rule is that for each type defined in `<stdint.h>` there will be corresponding `printf()` and `scanf()` macros defined here.

------------------------------------------------------------------------

## [9.2]{.header-section-number} `imaxabs()` {#man-imaxabs number="9.2"}

Compute the absolute value of an `intmax_t`

### Synopsis {#synopsis-48 .unnumbered .unlisted}

::: {#cb217 .sourceCode}
``` {.sourceCode .c}
#include <inttypes.h>

intmax_t imaxabs(intmax_t j);
```
:::

### Description {#description-48 .unnumbered .unlisted}

When you need the absolute value of the biggest integer type on the system, this is the function for you.

The spec notes that if the absolute value of the number cannot be represented, the behavior is undefined. This would happen if you tried to take the absolute value of the smallest possible negative number in a two's-complement system.

### Return Value {#return-value-47 .unnumbered .unlisted}

Returns the absolute value of the input, [\\(\|j\|\\)]{.math .inline}.

### Example {#example-48 .unnumbered .unlisted}

::: {#cb218 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <inttypes.h>

int main(void)
{
    intmax_t j = -3490;

    printf("%jd\n", imaxabs(j));    // 3490
}
```
:::

### See Also {#see-also-44 .unnumbered .unlisted}

[`fabs()`](math.html#man-fabs)

------------------------------------------------------------------------

## [9.3]{.header-section-number} `imaxdiv()` {#man-imaxdiv number="9.3"}

Compute the quotient and remainder of `intmax_t`s

### Synopsis {#synopsis-49 .unnumbered .unlisted}

::: {#cb219 .sourceCode}
``` {.sourceCode .c}
#include <inttypes.h>

imaxdiv_t imaxdiv(intmax_t numer, intmax_t denom);
```
:::

### Description {#description-49 .unnumbered .unlisted}

When you want to do integer division and remainder in a single operation, this function will do it for you.

It computes `numer/denom` and `numer%denom` and returns the result in a structure of type `imaxdiv_t`.

This structure has two `imaxdiv_t` fields, `quot` and `rem`, that you use to retrieve the sought-after values.

### Return Value {#return-value-48 .unnumbered .unlisted}

Returns an `imaxdiv_t` containing the quotient and remainder of the operation.

### Example {#example-49 .unnumbered .unlisted}

::: {#cb220 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <inttypes.h>

int main(void)
{
    intmax_t numer = INTMAX_C(3490);
    intmax_t denom = INTMAX_C(17);

    imaxdiv_t r = imaxdiv(numer, denom);

    printf("Quotient: %jd, remainder: %jd\n", r.quot, r.rem);
}
```
:::

Output:

::: {#cb221 .sourceCode}
``` {.sourceCode .default}
Quotient: 205, remainder: 5
```
:::

### See Also {#see-also-45 .unnumbered .unlisted}

[`remquo()`](math.html#man-remquo)

------------------------------------------------------------------------

## [9.4]{.header-section-number} `strtoimax()` `strtoumax()` {#man-strtoimax number="9.4"}

Convert strings to types `intmax_t` and `uintmax_t`

### Synopsis {#synopsis-50 .unnumbered .unlisted}

::: {#cb222 .sourceCode}
``` {.sourceCode .c}
#include <inttypes.h>

intmax_t strtoimax(const char * restrict nptr, char ** restrict endptr,
                   int base);

uintmax_t strtoumax(const char * restrict nptr, char ** restrict endptr,
                   int base);
```
:::

### Description {#description-50 .unnumbered .unlisted}

These work just like the [`strtol()`](stdlib.html#man-strtol) family of functions, except they return an `intmax_t` or `uintmax_t`.

See the [`strtol()`](stdlib.html#man-strtol) reference page for details.

### Return Value {#return-value-49 .unnumbered .unlisted}

Returns the converted string as an `intmax_t` or `uintmax_t`.

If the result is out of range, the returned value will be `INTMAX_MAX`, `INTMAX_MIN`, or `UINTMAX_MAX`, as appropriate. And the `errno` variable will be set to `ERANGE`.

### Example {#example-50 .unnumbered .unlisted}

The following example converts a base-10 number to an `intmax_t`. Then it attempts to convert an invalid base-2 number, catching the error.

::: {#cb223 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <inttypes.h>

int main(void)
{
    intmax_t r;
    char *endptr;

    // Valid base-10 number
    r = strtoimax("123456789012345", &endptr, 10);

    if (*endptr != '\0')
        printf("Invalid digit: %c\n", *endptr);
    else
        printf("Value is %jd\n", r);
    
    // The following binary number contains an invalid digit
    r = strtoimax("0100102010101101", &endptr, 2);

    if (*endptr != '\0')
        printf("Invalid digit: %c\n", *endptr);
    else
        printf("Value is %jd\n", r);
}
```
:::

Output:

::: {#cb224 .sourceCode}
``` {.sourceCode .default}
Value is 123456789012345
Invalid digit: 2
```
:::

### See Also {#see-also-46 .unnumbered .unlisted}

[`strtol()`](stdlib.html#man-strtol), [`errno`](errno.html#errno)

------------------------------------------------------------------------

## [9.5]{.header-section-number} `wcstoimax()` `wcstoumax()` {#man-wcstoimax number="9.5"}

Convert wide strings to types `intmax_t` and `uintmax_t`

### Synopsis {#synopsis-51 .unnumbered .unlisted}

::: {#cb225 .sourceCode}
``` {.sourceCode .c}
#include <stddef.h> // for wchar_t
#include <inttypes.h>

intmax_t wcstoimax(const wchar_t * restrict nptr,
                   wchar_t ** restrict endptr, int base);

uintmax_t wcstoumax(const wchar_t * restrict nptr,
                    wchar_t ** restrict endptr, int base);
```
:::

### Description {#description-51 .unnumbered .unlisted}

These work just like the [`wcstol()`](wchar.html#man-wcstol) family of functions, except they return an `intmax_t` or `uintmax_t`.

See the [`wcstol()`](wchar.html#man-wcstol) reference page for details.

### Return Value {#return-value-50 .unnumbered .unlisted}

Returns the converted wide string as an `intmax_t` or `uintmax_t`.

If the result is out of range, the returned value will be `INTMAX_MAX`, `INTMAX_MIN`, or `UINTMAX_MAX`, as appropriate. And the `errno` variable will be set to `ERANGE`.

### Example {#example-51 .unnumbered .unlisted}

The following example converts a base-10 number to an `intmax_t`. Then it attempts to convert an invalid base-2 number, catching the error.

::: {#cb226 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <inttypes.h>

int main(void)
{
    intmax_t r;
    wchar_t *endptr;

    // Valid base-10 number
    r = wcstoimax(L"123456789012345", &endptr, 10);

    if (*endptr != '\0')
        wprintf(L"Invalid digit: %lc\n", *endptr);
    else
        wprintf(L"Value is %jd\n", r);
    
    // The following binary number contains an invalid digit
    r = wcstoimax(L"0100102010101101", &endptr, 2);

    if (*endptr != '\0')
        wprintf(L"Invalid digit: %lc\n", *endptr);
    else
        wprintf(L"Value is %jd\n", r);
}
```
:::

::: {#cb227 .sourceCode}
``` {.sourceCode .default}
Value is 123456789012345
Invalid digit: 2
```
:::

### See Also {#see-also-47 .unnumbered .unlisted}

[`wcstol()`](wchar.html#man-wcstol), [`errno`](errno.html#errno)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](float.html) \| [Contents](index.html) \| [Next](iso646.html)
:::
