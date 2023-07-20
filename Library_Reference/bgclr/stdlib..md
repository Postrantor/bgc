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

  -------------------------------------------------------------------------------------------------------------
  Function                                             Description
  ---------------------------------------------------- --------------------------------------------------------
  [`_Exit()`](stdlib.html#man-exit)                    Exit the currently-running program and don't look back

  [`abort()`](stdlib.html#man-abort)                   Abruptly end program execution

  [`abs()`](stdlib.html#man-abs)                       Compute the absolute value of an integer

  [`aligned_alloc()`](stdlib.html#man-aligned_alloc)   Allocate specifically-aligned memory

  [`at_quick_exit()`](stdlib.html#man-atexit)          Set up handlers to run when the program quickly exits

  [`atexit()`](stdlib.html#man-atexit)                 Set up handlers to run when the program exits

  [`atof()`](stdlib.html#man-atof)                     Convert a string to a floating point value

  [`atoi()`](stdlib.html#man-atoi)                     Convert an integer in a string into a integer type

  [`bsearch()`](stdlib.html#man-bsearch)               Binary Search (maybe) an array of objects

  [`calloc()`](stdlib.html#man-malloc)                 Allocate and clear memory for arbitrary use

  [`div()`](stdlib.html#man-div)                       Compute the quotient and remainder of two numbers

  [`exit()`](stdlib.html#man-exit)                     Exit the currently-running program

  [`free()`](stdlib.html#man-free)                     Free a memory region

  [`getenv()`](stdlib.html#man-getenv)                 Get the value of an environment variable

  [`malloc()`](man-malloc)                             Allocate memory for arbitrary use

  [`mblen()`](stdlib.html#man-mblen)                   Return the number of bytes in a multibyte character

  [`mbstowcs()`](stdlib.html#man-mbstowcs)             Convert a multibyte string to a wide character string

  [`mbtowc()`](stdlib.html#man-mbtowc)                 Convert a multibyte character to a wide character

  [`qsort()`](stdlib.html#man-qsort)                   Quicksort (maybe) some data

  [`quick_exit()`](stdlib.html#man-exit)               Exit the currently-running program quickly

  [`rand()`](stdlib.html#man-rand)                     Return a pseudorandom number

  [`realloc()`](stdlib.html#man-realloc)               Resize a previously allocated stretch of memory

  [`srand()`](stdlib.html#man-srand)                   Seed the built-in pseudorandom number generator

  [`strtod()`](stdlib.html#man-strtod)                 Convert a string to a floating point number

  [`strtol()`](stdlib.html#man-strtol)                 Convert a string to an integer

  [`system()`](stdlib.html#man-system)                 Run an external program

  [`wcstombs()`](stdlib.html#man-wcstombs)             Convert a wide character string to a multibyte string

  [`wctomb()`](stdlib.html#man-wctomb)                 Convert a wide character to a multibyte character
  -------------------------------------------------------------------------------------------------------------

The `<stdlib.h>` header has all kinds of---dare I say---miscellaneous functions bundled into it. This functionality includes:

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

  -------------------------------------------------------------------------------
  Type                                Description
  ----------------------------------- -------------------------------------------
  `size_t`                            Returned from `sizeof` and used elsewhere

  `wchar_t`                           For wide character operations

  `div_t`                             For the `div()` function

  `ldiv_t`                            For the `ldiv()` function

  `lldiv_t`                           for the `lldiv()` function
  -------------------------------------------------------------------------------

And some macros:

  ------------------------------------------------------------------------------------------------------------
  Type                                Description
  ----------------------------------- ------------------------------------------------------------------------
  `NULL`                              Our good pointer friend

  `EXIT_SUCCESS`                      Good exit status when things go well

  `EXIT_FAILURE`                      Good exit status when things go poorly

  `RAND_MAX`                          The maximum value that can be returned by the `rand()` function

  `MB_CUR_MAX`                        Maximum number of bytes in a multibyte character in the current locale
  ------------------------------------------------------------------------------------------------------------

And there you have it. Just a lot of fun, useful functions in here. Let's check 'em out!

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

But the gist is the same: we're going to convert a string with numbers and (optionally) a decimal point into a floating point value. Leading whitespace is ignored, and translation stops at the first invalid character.

If the result doesn't fit in a `double`, behavior is undefined.

It generally works as if you'd called [`strtod()`](stdlib.html#man-strtod):

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

These functions take a string with a number in them and convert it to an integer of the specified return type. Leading whitespace is ignored. Translation stops at the first invalid character.

If the result doesn't fit in the return type, behavior is undefined.

It generally works as if you'd called [`strtol()`](stdlib.html#man-strtol) family of functions:

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

Firstly, leading whitespace is skipped.

Then the functions attempt to convert characters into the floating point result. Finally, when an invalid character (or NUL character) is reached, they set `endptr` to point to the invalid character.

Set `endptr` to `NULL` if you don't care about where the first invalid character is.

If you didn't set `endptr` to `NULL`, it will point to a NUL character if the translation didn't find any bad characters. That is:

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

If `nptr` points to a string containing `INF` or `INFINITY` (upper or lowercase), the value for Infinity will be returned.

If `nptr` points to a string containing `NAN`, then (a quiet, non-signalling) NaN will be returned. You can tag the `NAN` with a sequence of characters from the set `0`-`9`, `a`-`z`, `A`-`Z`, and `_` by enclosing them in parens:

::: {#cb579 .sourceCode}
``` {.sourceCode .c}
NAN(foobar_3490)
```
:::

What your compiler does with this is implementation-defined, but it can be used to specify different kinds of NaN.

You can also specify a number in hexadecimal with a power-of-two exponent ([\\(2\^x\\)]{.math .inline}) if you lead with `0x` (or `0X`). For the exponent, use a `p` followed by a base 10 exponent. (You can't use `e` because that's a valid hex digit!)

Example:

::: {#cb580 .sourceCode}
``` {.sourceCode .c}
0xabc.123p15
```
:::

Which computes to [\\(0xabc.123\\times2\^{15}\\)]{.math .inline}.

You can put in `FLT_DECIMAL_DIG`, `DBL_DECIMAL_DIG`, or `LDBL_DECIMAL_DIG` digits and get a correctly-rounded result for the type.

### Return Value {#return-value-160 .unnumbered .unlisted}

Returns the converted number. If there was no number, returns `0`. `endptr` is set to point to the first invalid character, or the NUL terminator if all characters were consumed.

If there's an overflow, `HUGE_VAL`, `HUGE_VALF`, or `HUGE_VALL` is returned, signed like the input, and `errno` is set to `ERANGE`.

If there's an underflow, it returns the smallest number closest to zero with the input sign. `errno` may be set to `ERANGE`.

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

Most notable, they can tell you where conversion started going wrong, i.e. where invalid characters, if any, appear. Leading spaces are ignored. A `+` or `-` sign may precede the number.

The basic idea is that if things go well, these functions will return the integer values contained in the strings. And if you pass in the `char**` typed `endptr`, it'll set it to point at the NUL at the end of the string.

If things don't go well, they'll set `endptr` to point at the first character where things have gone awry. That is, if you're converting a value `103z2!` in base 10, they'll send `endptr` to point at the `z` because that's the first non-numeric character.

You can pass in `NULL` for `endptr` if you don't care to do any of that kind of error checking.

Wait---did I just say we could set the number base for the conversion? Yes! Yes, I did. Now [number bases](https://en.wikipedia.org/wiki/Radix)[^52^](footnotes.html#fn52){#fnref52 .footnote-ref role="doc-noteref"} are out of scope for this document, but certainly some of the more well-known are binary (base 2), octal (base 8), decimal (base 10), and hexadecimal (base 16).

You can specify the number base for the conversion as the third parameter. Bases from 2 to 36 are supported, with case-insensitive digits running from `0` to `Z`.

If you specify a base of `0`, the function will make an effort to determine it. It'll default to base 10 except for a couple cases:

-   If the number has a leading `0`, it will be octal (base 8)
-   If the number has a leading `0x` or `0X`, it will be hex (base 16)

The locale might affect the behavior of these functions.

### Return Value {#return-value-161 .unnumbered .unlisted}

Returns the converted value.

`endptr`, if not `NULL` is set to the first invalid character, or to the beginning of the string if no conversion was performed, or to the string terminal NUL if all characters were valid.

If there's overflow, one of these values will be returned: `LONG_MIN`, `LONG_MAX`, `LLONG_MIN`, `LLONG_MAX`, `ULONG_MAX`, `ULLONG_MAX`. And `errno` is set to `ERANGE`.

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

If you want to force this to a certain range, the classic way to do this is to force it with the modulo operator `%`, although [this introduces biases](https://stackoverflow.com/questions/10984974/why-do-people-say-there-is-modulo-bias-when-using-a-random-number-generator)[^53^](footnotes.html#fn53){#fnref53 .footnote-ref role="doc-noteref"} if `RAND_MAX+1` is not a multiple of the number you're modding by. Dealing with this is out of scope for this guide.

If you want to to make a floating point number between `0` and `1` inclusive, you can divide the result by `RAND_MAX`. Or `RAND_MAX+1` if you don't want to include `1`. But of course, there are out-of-scope [problems with this, as well](https://mumble.net/~campbell/2014/04/28/uniform-random-float)[^54^](footnotes.html#fn54){#fnref54 .footnote-ref role="doc-noteref"}.

In short, `rand()` is a great way to get potentially poor random numbers with ease. Probably good enough for the game you're writing.

The spec elaborates:

> There are no guarantees as to the quality of the random sequence produced and some implementations are known to produce sequences with distressingly non-random low-order bits. Applications with particular requirements should use a generator that is known to be sufficient for their needs.

Your system probably has a good random number generator on it if you need a stronger source. Linux users have `getrandom()`, for example, and Windows has `CryptGenRandom()`.

For other more demanding random number work, you might find a library like the [GNU Scientific Library](https://www.gnu.org/software/gsl/doc/html/rng.html)[^55^](footnotes.html#fn55){#fnref55 .footnote-ref role="doc-noteref"} of use.

With most implementations, the numbers produced by `rand()` will be the same from run to run. To get around this, you need to start it off in a different place by passing a *seed* into the random number generator. You can do this with [`srand()`](stdlib.html#man-srand).

### Return Value {#return-value-162 .unnumbered .unlisted}

Returns a random number in the range `0` to `RAND_MAX`, inclusive.

### Example {#example-165 .unnumbered .unlisted}

Note that all of these examples don't produce perfectly uniform distributions. But good enough for the untrained eye, and really common in general use when mediocre random number quality is acceptable.

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

If you use `rand()` and run your program several times, you might notice something *fishy*: they produce the same random numbers over and over again.

To mix it up, we need to give the pseudorandom number generator a new "starting point", if you will. We call that the *seed*. It's just a number, but it is used as the basic for subsequent number generation. Give a different seed, and you'll get a different sequence of random numbers. Give the same seed, and you'll get the same sequence of random numbers corresponding to it[^56^](footnotes.html#fn56){#fnref56 .footnote-ref role="doc-noteref"}.

So if you call `srand(3490)` before you start generating numbers with `rand()`, you'll get the same sequence every time. `srand(37)` would also give you the same sequence every time, but it would be a different sequence than the one you got with `srand(3490)`.

But if you can't hardcode the seed (because that would give you the same sequence every time), how are you supposed to do this?

It's really common to use the number of seconds since January 1, 1970 (this date is known as the [*Unix epoch*](https://en.wikipedia.org/wiki/Unix_time)[^57^](footnotes.html#fn57){#fnref57 .footnote-ref role="doc-noteref"}) to seed the generator. This sounds pretty arbitrary except for the fact that it's exactly the value most implementations return from the library call `time(NULL)`[^58^](footnotes.html#fn58){#fnref58 .footnote-ref role="doc-noteref"}.

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

Normally you don't have to think about this, since `malloc()` and `realloc()` both provide memory regions that are suitably [aligned](https://en.wikipedia.org/wiki/Data_structure_alignment)[^59^](footnotes.html#fn59){#fnref59 .footnote-ref role="doc-noteref"} for use with any data type.

But if you need a more specific alignment, you can specify it with this function.

When you're done using the memory region, be sure to free it with a call to [`free()`](stdlib.html#man-free).

Don't pass in `0` for the size. It probably won't do anything you want.

In case you're wondering, all dynamically-allocated memory is automatically freed by the system when the program ends. That said, it's considered to be *Good Form* to explicitly `free()` everything you allocate. This way other programmers don't think you were being sloppy.

### Return Value {#return-value-164 .unnumbered .unlisted}

Returns a pointer to the newly-allocated memory, aligned as specified. Returns `NULL` if something goes wrong.

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

`malloc()` allocates exactly the specified number of bytes of memory in a contiguous block. The memory might be full of garbage data. (You can clear it with [`memset()`](stringref.html#man-memset), if you wish.)

`calloc()` is different in that it allocates space for `nmemb` objects of `size` bytes each. (You can do the same with `malloc()`, but you have to do the multiplication yourself.)

`calloc()` has an additional feature: it clears all the memory to `0`.

So if you're planning to zero the memory anyway, `calloc()` is probably the way to go. If you're not, you can avoid that overhead by calling `malloc()`.

When you're done using the memory region, free it with a call to `free()`.

Don't pass in `0` for the size. It probably won't do anything you want.

In case you're wondering, all dynamically-allocated memory is automatically freed by the system when the program ends. That said, it's considered to be *Good Form* to explicitly `free()` everything you allocate. This way other programmers don't think you were being sloppy.

### Return Value {#return-value-165 .unnumbered .unlisted}

Both functions return a pointer to the shiny, newly-allocated memory. Or `NULL` if something's gone awry.

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

If you don't do this, the memory will stay allocated FOREVER AND EVER! (Well, until your program exits, anyway.)

Fun fact: `free(NULL)` does nothing. You can safely call that. Sometimes it's convenient.

Don't `free()` a pointer that's already been `free()`d. Don't `free()` a pointer that you didn't get back from one of the allocation functions. It would be *Bad*[^60^](footnotes.html#fn60){#fnref60 .footnote-ref role="doc-noteref"}.

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

If the new size is smaller than the old size, any data larger than the new size is discarded.

If the new size is larger than the old size, the new larger part is uninitialized. (You can clear it with [`memset()`](stringref.html#man-memset).)

Important note: the memory might move! If you resize, the system might need to relocate the memory to a larger continguous chunk. If this happens, `realloc()` will copy the old data to the new location for you.

Because of this, it's important to save the returned value to your pointer to update it to the new location if things move. (Also, be sure to error-check so that you don't overwrite your old pointer with `NULL`, leaking the memory.)

You can also `relloc()` memory allocated with `aligned_alloc()`, but it will potentially lose its alignment if the block is moved.

### Return Value {#return-value-167 .unnumbered .unlisted}

Returns a pointer to the resized memory region. This might be equivalent to the `ptr` passed in, or it might be some other location.

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

Open streams might not be flushed. Temporary files created might not be removed. Exit handlers are not called.

A non-zero exit status is returned to the environment.

On some systems, `abort()` might [dump core](https://en.wikipedia.org/wiki/Core_dump)[^61^](footnotes.html#fn61){#fnref61 .footnote-ref role="doc-noteref"}, but this is outside the scope of the spec.

You can cause the equivalent of an `abort()` by calling `raise(SIGABRT)`, but I don't know why you'd do that.

The only portable way to stop an `abort()` call midway is to use `signal()` to catch `SIGABRT` and then `exit()` in the signal handler.

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

Think of it like, "Hey, when you're about to exit, do these extra things."

For the `quick_exit()` call, you can use the `at_quick_exit()` function to register handlers for that[^62^](footnotes.html#fn62){#fnref62 .footnote-ref role="doc-noteref"}. There's no crossover in handlers from `exit()` to `quick_exit()`, i.e. for a call to one, none of the other's handlers will fire.

You can register multiple handlers to fire---at least 32 handlers are supported by both `exit()` and `quick_exit()`.

The argument `func` to the functions looks a little weird---it's a pointer to a function to call. Basically just put the function name to call in there (without parentheses after). See the example, below.

If you call `atexit()` from inside your `atexit()` handler (or equivalent in your `at_quick_exit()` handler), it's unspecified if it will get called. So get them all registered before you exit.

When exiting, the functions will be called in the reverse order they were registered.

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

`exit()` does the most cleanup and is the most normal exit.

`quick_exit()` is the second most.

`_Exit()` unceremoniously drops everything and ragequits on the spot.

Calling either of `exit()` or `quick_exit()` causes their respective `atexit()` or `at_quick_exit()` handlers to be called in the reverse order in which they were registered.

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

Of course the exact details are system dependent, but these variables are key/value pairs, and you can get the value by passing the key to `getenv()` as the `name` parameter.

You're not allowed to overwrite the string that's returned.

This is pretty limited in the standard, but your OS often provides better functionality.

### Return Value {#return-value-171 .unnumbered .unlisted}

Returns a pointer to the environment variable value, or `NULL` if the variable doesn't exist.

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

Not all systems have this capability, but you can test for it by passing `NULL` to `system()` and seeing if it returns 0 (no command processor is available) or non-zero (a command processor is available! Yay!)

If you're getting user input and passing it to the `system()` call, be extremely careful to escape all special shell characters (everything that's not alphanumeric) with a backslash to keep a villain from running something you don't want them to.

### Return Value {#return-value-172 .unnumbered .unlisted}

If `NULL` is passed, returns nonzero if a command processor is available (i.e. `system()` will work at all).

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

However, the array must be sorted! So binary search seems likely.

-   `key` is a pointer to the value to find.
-   `base` is a pointer to the start of the array---the array must be sorted!
-   `nmemb` is the number of elements in the array.
-   `size` is the `sizeof` each element in the array.
-   `compar` is a pointer to a function that will compare the key against other values.

The comparison function takes the key as the first argument and the value to compare against as the second. It should return a negative number if the key is less than the value, `0` if the key equals the value, and a positive number if the key is greater than the value.

This is commonly computed by taking the difference between the key and the value to be compared. If subtraction is supported.

The return value from the [`strcmp()`](stringref.html#man-strcmp) function can be used for comparing strings.

Again, the array must be sorted according to the order of the comparison function before running `bsearch()`. Luckily for you, you can just call [`qsort()`](stdlib.html#man-qsort) with the same comparison function to get this done.

It's a general-purpose function---it'll search any type of array for anything. The catch is you have to write the comparison function.

And that's not as scary as it looks. Jump down to the example

### Return Value {#return-value-173 .unnumbered .unlisted}

The function returns a pointer to the found value, or `NULL` if it can't be found.

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

Like `bsearch()`, it's data-agnostic. Any data for which you can define a relative ordering can be sorted, whether `int`s, `struct`s, or anything else.

Also like `bsearch()`, you have to give a comparison function to do the actual compare.

-   `base` is a pointer to the start of the array to be sorted.
-   `nmemb` is the number of elements in the array.
-   `size` is the `sizeof` each element.
-   `compar` is a pointer to the comparison function.

The comparison function takes pointers to two elements of the array as arguments and compares them. It should return a negative number if the first argument is less than the second, `0` if they are equal, and a positive number if the first argument is greater than the second.

This is commonly computed by taking the difference between the first argument and the second. If subtraction is supported.

The return value from the [`strcmp()`](stringref.html#man-strcmp) function can provide sort order for strings.

If you have to sort a `struct`, just subtract the specific field you want to sort by.

This comparison function can be used by [`bsearch()`](stdlib.html#man-bsearch) to do searches after the list is sorted.

To reverse the sort, subtract the second argument from the first, i.e. negate the return value from `compar()`.

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

In other words, if `j` is negative, return it as a positive. If it's positive, return it as a positive. Always be positive. Enjoy life.

If the result cannot be represented, the behavior is undefined. Be especially aware of the upper half of unsigned numbers.

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

They return a structure that has two fields, `quot`, and `rem`, the types of which match types of `numer` and `denom`. Note how each function returns a different variant of `div_t`.

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

           `numer`                    `denom`                     `quot`                     `rem`
  -------------------------- -------------------------- -------------------------- --------------------------
   [\\(+\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(+\\)]{.math .inline}
   [\\(-\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(-\\)]{.math .inline}
   [\\(+\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(+\\)]{.math .inline}
   [\\(-\\)]{.math .inline}   [\\(-\\)]{.math .inline}   [\\(+\\)]{.math .inline}   [\\(-\\)]{.math .inline}

### Return Value {#return-value-176 .unnumbered .unlisted}

A `div_t`, `ldiv_t`, or `lldiv_t` structure with the `quot` and `rem` fields loaded with the quotient and remainder of the operation of `numer/denom`.

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

`n` is the maximum number of bytes `mblen()` will scan before giving up.

If `s` is a `NULL` pointer, tests if this encoding has state dependency, as noted in the return value, below. It also resets the state, if there is one.

The behavior of this function is influenced by the locale.

### Return Value {#return-value-177 .unnumbered .unlisted}

Returns the number of bytes used to encode this character, or `-1` if there is no valid multibyte character in the next `n` bytes.

Or, if `s` is NULL, returns true if this encoding has state dependency.

### Example {#example-180 .unnumbered .unlisted}

For the example, I used my extended character set to put Unicode characters in the source. If this doesn't work for you, use the `\uXXXX` escape.

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

If `pwc` is `NULL`, the resulting character will not be stored. (Useful for just getting the return value.)

If `s` is a `NULL` pointer, tests if this encoding has state dependency, as noted in the return value, below. It also resets the state, if there is one.

The behavior of this function is influenced by the locale.

### Return Value {#return-value-178 .unnumbered .unlisted}

Returns the number of bytes used in the encoded wide character, or `-1` if there is no valid multibyte character in the next `n` bytes.

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

The wide character `wc` is stored as a multibyte character in the string pointed to by `s`. The buffer `s` points to should be at least `MB_CUR_MAX` characters long. Note that `MB_CUR_MAX` changes with locale.

If `wc` is a NUL wide character, a NUL is stored in `s` after the bytes needed to reset the shift state (if any).

If `s` is a `NULL` pointer, tests if this encoding has state dependency, as noted in the return value, below. It also resets the state, if there is one.

The behavior of this function is influenced by the locale.

### Return Value {#return-value-179 .unnumbered .unlisted}

Returns the number of bytes used in the encoded multibyte character, or `-1` if `wc` does not correspond to any valid multibyte character.

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

At most `n` wide characters are written to the destination `pwcs` from the source `s`.

A NUL character is stored as a wide NUL character.

Non-portable POSIX extension: if you're using a POSIX-complaint library, this function allows `pwcs` to be `NULL` if you're only interested in the return value. Most notably, this will give you the number of characters in a multibyte string (as opposed to [`strlen()`](stringref.html#man-strlen) which counts the bytes.)

### Return Value {#return-value-180 .unnumbered .unlisted}

Returns the number of wide characters written to the destination `pwcs`.

If an invalid multibyte character was found, returns `(size_t)(-1)`.

If the return value is `n`, it means the result was *not* NUL-terminated.

### Example {#example-183 .unnumbered .unlisted}

This source uses an extended character set. If your compiler doesn't support it, you'll have to replace them with `\u` escapes.

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

It'll take the wide characters pointed to by `pwcs` and convert them to multibyte characters stored in `s`. No more than `n` bytes will be written to `s`.

Non-portable POSIX extension: if you're using a POSIX-complaint library, this function allows `s` to be `NULL` if you're only interested in the return value. Most notably, this will give you the number of bytes needed to encode the wide characters in a multibyte string.

### Return Value {#return-value-181 .unnumbered .unlisted}

Returns the number of bytes written to `s`, or `(size_t)(-1)` if one of the characters can't be encoded into a multibyte string.

If the return value is `n`, it means the result was *not* NUL-terminated.

### Example {#example-184 .unnumbered .unlisted}

This source uses an extended character set. If your compiler doesn't support it, you'll have to replace them with `\u` escapes.

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

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdio.html) \| [Contents](index.html) \| [Next](stdnoreturn.html)
:::
