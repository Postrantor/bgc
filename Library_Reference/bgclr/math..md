---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](locale.html) \| [Contents](index.html) \| [Next](setjmp.html)
:::

------------------------------------------------------------------------

# [13]{.header-section-number} `<math.h>` Mathematics {#math number="13"}

Many of the following functions have `float` and `long double` variants as described [below](math.html#func-idioms) (e.g. `pow()`, `powf()`, `powl()`). The `float` and `long double` variants are omitted from the following table to keep your eyeballs from melting out.

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Function                                                                  Description
  ------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------
  [`acos()`](math.html#man-acos)                                            Calculate the arc cosine of a number.

  [`acosh()`](math.html#man-acosh)                                          Compute arc hyperbolic cosine.

  [`asin()`](math.html#man-asin)                                            Calculate the arc sine of a number.

  [`asinh()`](math.html#man-asinh)                                          Compute arc hyperbolic sine.

  [`atan()`](math.html#man-atan), [`atan2()`](math.html#man-atan)           Calculate the arc tangent of a number.

  [`atanh()`](math.html#man-atanh)                                          Compute the arc hyperbolic tangent.

  [`cbrt()`](math.html#man-cbrt)                                            Compute the cube root.

  [`ceil()`](math.html#man-ceil)                                            Ceiling---return the next whole number not smaller than the given number.

  [`copysign()`](math.html#man-copysign)                                    Copy the sign of one value into another.

  [`cos()`](math.html#man-cos)                                              Calculate the cosine of a number.

  [`cosh()`](math.html#man-cosh)                                            Compute the hyperbolic cosine.

  [`erf()`](math.html#man-erf)                                              Compute the error function of the given value.

  [`erfc()`](math.html#man-erfc)                                            Compute the complementary error function of a value.

  [`exp()`](math.html#man-exp)                                              Compute [\\(e\\)]{.math .inline} raised to a power.

  [`exp2()`](math.html#man-exp2)                                            Compute 2 to a power.

  [`expm1()`](math.html#man-expm1)                                          Compute [\\(e\^x-1\\)]{.math .inline}.

  [`fabs()`](math.html#man-fabs)                                            Compute the absolute value.

  [`fdim()`](math.html#man-fdim)                                            Return the positive difference between two numbers clamped at 0.

  [`floor()`](math.html#man-floor)                                          Compute the largest whole number not larger than the given value.

  [`fma()`](math.html#man-fma)                                              Floating (AKA "Fast") multiply and add.

  [`fmax()`](math.html#man-fmax), [`fmin()`](math.html#man-fmax)            Return the maximum or minimum of two numbers.

  [`fmod()`](math.html#man-fmod)                                            Compute the floating point remainder.

  [`fpclassify()`](math.html#man-fpclassify)                                Return the classification of a given floating point number.

  [`frexp()`](math.html#man-frexp)                                          Break a number into its fraction part and exponent (as a power of 2).

  [`hypot()`](math.html#man-hypot)                                          Compute the length of the hypotenuse of a triangle.

  [`ilogb()`](math.html#man-ilogb)                                          Return the exponent of a floating point number.

  [`isfinite()`](math.html#man-isnan)                                       True if the number is not infinite or NaN.

  [`isgreater()`](math.html#man-isgreater)                                  True if one argument is greater than another.

  [`isgreatereequal()`](math.html#man-isgreater)                            True if one argument is greater than or equal to another.

  [`isinf()`](math.html#man-isnan)                                          True if the number is infinite.

  [`isless()`](math.html#man-isgreater)                                     True if one argument is less than another.

  [`islesseequal()`](math.html#man-isgreater)                               True if one argument is less than or equal to another.

  [`islessgreater()`](math.html#man-islessgreater)                          Test if a floating point number is less than or greater than another.

  [`isnan()`](math.html#man-isnan)                                          True if the number is Not-a-Number.

  [`isnormal()`](math.html#man-isnan)                                       True if the number is normal.

  [`isunordered()`](math.html#man-isunordered)                              Macro returns true if either floating point argument is NaN.

  [`ldexp()`](math.html#man-ldexp)                                          Multiply a number by an integral power of 2.

  [`lgamma()`](math.html#man-lgamma)                                        Compute the natural logarithm of the absolute value of [\\(\\Gamma(x)\\)]{.math .inline}.

  [`log()`](math.html#man-log)                                              Compute the natural logarithm.

  [`log10()`](math.html#man-log10)                                          Compute the log-base-10 of a number.

  [`log2()`](math.html#man-log2)                                            Compute the base-2 logarithm of a number.

  [`logb()`](math.html#man-logb)                                            Extract the exponent of a number given `FLT_RADIX`.

  [`log1p()`](math.html#man-log1p)                                          Compute the natural logarithm of a number plus 1.

  [`lrint()`](math.html#man-lrint)                                          Returns `x` rounded in the current rounding direction as an integer.

  [`lround()`](math.html#man-lround), [`llround()`](math.html#man-lround)   Round a number in the good old-fashioned way, returning an integer.

  [`modf()`](math.html#man-modf)                                            Extract the integral and fractional parts of a number.

  [`nan()`](math.html#man-nan)                                              Return `NAN`.

  [`nearbyint()`](math.html#man-nearbyint)                                  Rounds a value in the current rounding direction.

  [`nextafter()`](math.html#man-nextafter)                                  Get the next (or previous) representable floating point value.

  [`nexttoward()`](math.html#man-nexttoward)                                Get the next (or previous) representable floating point value.

  [`pow()`](math.html#man-pow)                                              Compute a value raised to a power.

  [`remainder()`](math.html#man-remainder)                                  Compute the remainder IEC 60559-style.

  [`remquo()`](math.html#man-remquo)                                        Compute the remainder and (some of the) quotient.

  [`rint()`](math.html#man-rint)                                            Rounds a value in the current rounding direction.

  [`round()`](math.html#man-round)                                          Round a number in the good old-fashioned way.

  [`scalbn()`](math.html#man-scalb), [`scalbln()`](math.html#man-scalb)     Efficiently compute [\\(x\\times r\^n\\)]{.math .inline}, where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

  [`signbit()`](math.html#man-signbit)                                      Return the sign of a number.

  [`sin()`](math.html#man-sin)                                              Calculate the sine of a number.

  [`sqrt()`](math.html#man-sqrt)                                            Calculate the square root of a number.

  [`tan()`](math.html#man-tan)                                              Calculate the tangent of a number.

  [`tanh()`](math.html#man-tanh)                                            Compute the hyperbolic tangent.

  [`tgamma()`](math.html#man-tgamma)                                        Compute the gamma function, [\\(\\Gamma(x)\\)]{.math .inline}.

  [`trunc()`](math.html#man-trunc)                                          Truncate the fractional part off a floating point value.
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

It's your favorite subject: Mathematics! Hello, I'm Doctor Math, and I'll be making math FUN and EASY!

*\[vomiting sounds\]*

Ok, I know math isn't the grandest thing for some of you out there, but these are merely functions that quickly and easily do math you either know, want, or just don't care about. That pretty much covers it.

## [13.1]{.header-section-number} Math Function Idioms {#func-idioms number="13.1"}

Many of these math functions exist in three forms, each corresponding to the argument and/or return types the function uses, `float`, `double`, or `long double`.

The alternate form for `float` is made by appending `f` to the end of the function name.

The alternate form for `long double` is made by appending `l` to the end of the function name.

For example, the `pow()` function, which computes [\\(x\^y\\)]{.math .inline}, exists in these forms:

::: {#cb240 .sourceCode}
``` {.sourceCode .c}
double      pow(double x, double y);             // double
float       powf(float x, float y);              // float
long double powl(long double x, long double y);  // long double
```
:::

Remember that parameters are given values as if you assigned into them. So if you pass a `double` to `powf()`, it'll choose the closest `float` it can to hold the double. If the `double` doesn't fit, undefined behavior happens.

## [13.2]{.header-section-number} Math Types {#math-types number="13.2"}

We have two exciting new types in `<math.h>`:

-   `float_t`
-   `double_t`

The `float_t` type is at least as accurate as a `float`, and the `double_t` type is at least as accurate as a `double`.

The idea with these types is they can represent the most efficient way of storing numbers for maximum speed.

Their actual types vary by implementation, but can be determined by the value of the `FLT_EVAL_METHOD` macro.

  `FLT_EVAL_METHOD`   `float_t` type           `double_t` type
  ------------------- ------------------------ ------------------------
  `0`                 `float`                  `double`
  `1`                 `double`                 `double`
  `2`                 `long double`            `long double`
  Other               Implementation-defined   Implementation-defined

For all defined values of `FLT_EVAL_METHOD`, `float_t` is the least-precise type used for all floating calculations.

## [13.3]{.header-section-number} Math Macros {#math-macros number="13.3"}

There are actually a number of these defined, but we'll cover most of them in their relevant reference sections, below.

But here are a couple:

`NAN` represents Not-A-Number.

Defined in `<float.h>` is `FLT_RADIX`: the number base used by floating point numbers. This is commonly `2`, but could be anything.

## [13.4]{.header-section-number} Math Errors {#math-errors number="13.4"}

As we know, nothing can ever go wrong with math... except *everything*!

So there are just a couple errors that might occur when using some of these functions.

-   **Range errors** mean that some result is beyond what can be stored in the result type.

-   **Domain errors** mean that you've passed in an argument that doesn't have a defined result for this function.

-   **Pole errors** mean that the limit of the function as [\\(x\\)]{.math .inline} approaches the given argument is infinite.

-   **Overflow errors** are when the result is really large, but can't be stored without incurring large roundoff error.

-   **Underflow errors** are like overflow errors, except with very small numbers.

Now, the C math library can do a couple things when these errors occur:

-   Set `errno` to some value, or...
-   Raise a floating point exception.

Your system might vary on what happens. You can check it by looking at the value of the variable `math_errhandling`. It will be equivalent to one of the following[^22^](footnotes.html#fn22){#fnref22 .footnote-ref role="doc-noteref"}:

  ----------------------------------------------------------------------------------
  `math_errhandling`                  Description
  ----------------------------------- ----------------------------------------------
  `MATH_ERRNO`                        The system uses `errno` for math errors.

  `MATH_ERREXCEPT`                    The system uses exceptions for math errors.

  `MATH_ERRNO | MATH_ERREXCEPT`       The system does both! (That's a bitwise-OR!)
  ----------------------------------------------------------------------------------

You are not allowed to change `math_errhandling`.

For a fuller description on how exceptions work and their meanings, see the [`<fenv.h>`](fenv.html#fenv) section.

## [13.5]{.header-section-number} Math Pragmas {#math-pragmas number="13.5"}

In a nutshell, pragmas offer various ways to control the compiler's behavior. In this case, we're talking about controlling how C's math library works.

In specific, we have a pragma `FP_CONTRACT` that can be turned off and on.

What does it mean?

First of all, keep in mind that any operation in an expression can cause rounding error. So each step of the expression can introduce more rounding error.

But what if the compiler knows a *double secret* way of taking the expression you wrote and converting it to a single instruction that reduced the number of steps such that the intermediate rounding error didn't occur?

Could it use it? I mean, the results would be different than if you let the rounding error settle each step of the way...

Because the results would be different, you can tell the compiler if you want to allow it to do this or not.

If you want to allow it:

::: {#cb241 .sourceCode}
``` {.sourceCode .c}
#pragma STDC FP_CONTRACT ON
```
:::

and to disallow it:

::: {#cb242 .sourceCode}
``` {.sourceCode .c}
#pragma STDC FP_CONTRACT OFF
```
:::

If you do this at global scope, it stays at whatever state you set it to until you change it.

If you do it at block scope, it reverts to the value outside the block when the block ends.

The initial value of the `FP_CONTRACT` pragma varies from system to system.

------------------------------------------------------------------------

## [13.6]{.header-section-number} `fpclassify()` {#man-fpclassify number="13.6"}

Return the classification of a given floating point number.

### Synopsis {#synopsis-54 .unnumbered .unlisted}

::: {#cb243 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

int fpclassify(any_floating_type x);
```
:::

### Description {#description-54 .unnumbered .unlisted}

What kind of entity does this floating point number represent? What are the options?

We're used to floating point numbers being regular old things like `3.14` or `3490.0001`.

But floating point numbers can also represent things like infinity. Or Not-A-Number (NAN). This function will let you know which type of floating point number the argument is.

This is a macro, so you can use it with `float`, `double`, `long double` or anything similar.

### Return Value {#return-value-53 .unnumbered .unlisted}

Returns one of these macros depending on the argument's classification:

  Classification   Description
  ---------------- --------------------------------
  `FP_INFINITE`    Number is infinite.
  `FP_NAN`         Number is Not-A-Number (NAN).
  `FP_NORMAL`      Just a regular number.
  `FP_SUBNORMAL`   Number is a sub-normal number.
  `FP_ZERO`        Number is zero.

A discussion of subnormal numbers is beyond the scope of the guide, and is something that most devs go their whole lives without dealing with. In a nutshell, it's a way to represent really small numbers that might normally round down to zero. If you want to know more, see the Wikipedia page on [denormal numbers](https://en.wikipedia.org/wiki/Denormal_number)[^23^](footnotes.html#fn23){#fnref23 .footnote-ref role="doc-noteref"}.

### Example {#example-54 .unnumbered .unlisted}

Print various number classifications.

::: {#cb244 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

const char *get_classification(double n)
{
    switch (fpclassify(n)) {
        case FP_INFINITE: return "infinity";
        case FP_NAN: return "not a number";
        case FP_NORMAL: return "normal";
        case FP_SUBNORMAL: return "subnormal";
        case FP_ZERO: return "zero";
    }

    return "unknown";
}
 
int main(void)
{
    printf("    1.23: %s\n", get_classification(1.23));
    printf("     0.0: %s\n", get_classification(0.0));
    printf("sqrt(-1): %s\n", get_classification(sqrt(-1)));
    printf("1/tan(0): %s\n", get_classification(1/tan(0)));
    printf("  1e-310: %s\n", get_classification(1e-310));  // very small!
}
```
:::

Output[^24^](footnotes.html#fn24){#fnref24 .footnote-ref role="doc-noteref"}:

::: {#cb245 .sourceCode}
``` {.sourceCode .default}
    1.23: normal
     0.0: zero
sqrt(-1): not a number
1/tan(0): infinity
  1e-310: subnormal
```
:::

### See Also {#see-also-50 .unnumbered .unlisted}

[`isfinite()`](math.html#man-isnan), [`isinf()`](math.html#man-isnan), [`isnan()`](math.html#man-isnan), [`isnormal()`](math.html#man-isnan), [`signbit()`](math.html#man-signbit)

------------------------------------------------------------------------

## [13.7]{.header-section-number} `isfinite()`, `isinf()`, `isnan()`, `isnormal()` {#man-isnan number="13.7"}

Return true if a number matches a classification.

### Synopsis {#synopsis-55 .unnumbered .unlisted}

::: {#cb246 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

int isfinite(any_floating_type x);

int isinf(any_floating_type x);

int isnan(any_floating_type x);

int isnormal(any_floating_type x);
```
:::

### Description {#description-55 .unnumbered .unlisted}

These are helper macros to `fpclassify()`. Bring macros, they work on any floating point type.

  Macro          Description
  -------------- --------------------------------------------
  `isfinite()`   True if the number is not infinite or NaN.
  `isinf()`      True if the number is infinite.
  `isnan()`      True if the number is Not-a-Number.
  `isnormal()`   True if the number is normal.

For more superficial discussion on normal and subnormal numbers, see [`fpclassify()`](math.html#man-fpclassify).

### Return Value {#return-value-54 .unnumbered .unlisted}

Returns non-zero for true, and zero for false.

### Example {#example-55 .unnumbered .unlisted}

::: {#cb247 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("  isfinite(1.23): %d\n", isfinite(1.23));    // 1
    printf(" isinf(1/tan(0)): %d\n", isinf(1/tan(0)));   // 1
    printf(" isnan(sqrt(-1)): %d\n", isnan(sqrt(-1)));   // 1
    printf("isnormal(1e-310): %d\n", isnormal(1e-310));  // 0
}
```
:::

### See Also {#see-also-51 .unnumbered .unlisted}

[`fpclassify()`](math.html#man-fpclassify), [`signbit()`](math.html#man-signbit),

------------------------------------------------------------------------

## [13.8]{.header-section-number} `signbit()` {#man-signbit number="13.8"}

Return the sign of a number.

### Synopsis {#synopsis-56 .unnumbered .unlisted}

::: {#cb248 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

int signbit(any_floating_type x);
```
:::

### Description {#description-56 .unnumbered .unlisted}

This macro takes any floating point number and returns a value indicating the sign of the number, positive or negative.

### Return Value {#return-value-55 .unnumbered .unlisted}

Returns `1` if the sign is negative, otherwise `0`.

### Example {#example-56 .unnumbered .unlisted}

::: {#cb249 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%d\n", signbit(3490.0));  // 0
    printf("%d\n", signbit(-37.0));   // 1
}
```
:::

### See Also {#see-also-52 .unnumbered .unlisted}

[`fpclassify()`](math.html#man-fpclassify), [`isfinite()`](math.html#man-isnan), [`isinf()`](math.html#man-isnan), [`isnan()`](math.html#man-isnan), [`isnormal()`](math.html#man-isnan), [`copysign()`](math.html#man-copysign)

------------------------------------------------------------------------

## [13.9]{.header-section-number} `acos()`, `acosf()`, `acosl()` {#man-acos number="13.9"}

Calculate the arc cosine of a number.

### Synopsis {#synopsis-57 .unnumbered .unlisted}

::: {#cb250 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double acos(double x);
float acosf(float x);
long double acosl(long double x);
```
:::

### Description {#description-57 .unnumbered .unlisted}

Calculates the arc cosine of a number in radians. (That is, the value whose cosine is `x`.) The number must be in the range -1.0 to 1.0.

For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

::: {#cb251 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-56 .unnumbered .unlisted}

Returns the arc cosine of `x`, unless `x` is out of range. In that case, `errno` will be set to EDOM and the return value will be NaN. The variants return different types.

### Example {#example-57 .unnumbered .unlisted}

::: {#cb252 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double acosx;
    long double ldacosx;

    acosx = acos(0.2);
    ldacosx = acosl(0.3L);

    printf("%f\n", acosx);
    printf("%Lf\n", ldacosx);
}
```
:::

### See Also {#see-also-53 .unnumbered .unlisted}

[`asin()`](math.html#man-asin), [`atan()`](math.html#man-atan), [`atan2()`](math.html#man-atan), [`cos()`](math.html#man-cos)

------------------------------------------------------------------------

## [13.10]{.header-section-number} `asin()`, `asinf()`, `asinl()` {#man-asin number="13.10"}

Calculate the arc sine of a number.

### Synopsis {#synopsis-58 .unnumbered .unlisted}

::: {#cb253 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double asin(double x);
float asinf(float x);
long double asinl(long double x);
```
:::

### Description {#description-58 .unnumbered .unlisted}

Calculates the arc sine of a number in radians. (That is, the value whose sine is `x`.) The number must be in the range -1.0 to 1.0.

For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

::: {#cb254 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-57 .unnumbered .unlisted}

Returns the arc sine of `x`, unless `x` is out of range. In that case, `errno` will be set to EDOM and the return value will be NaN. The variants return different types.

### Example {#example-58 .unnumbered .unlisted}

::: {#cb255 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double asinx;
    long double ldasinx;

    asinx = asin(0.2);
    ldasinx = asinl(0.3L);

    printf("%f\n", asinx);
    printf("%Lf\n", ldasinx);
}
```
:::

### See Also {#see-also-54 .unnumbered .unlisted}

[`acos()`](math.html#man-acos), [`atan()`](math.html#man-atan), [`atan2()`](math.html#man-atan), [`sin()`](math.html#man-sin)

------------------------------------------------------------------------

## [13.11]{.header-section-number} `atan()`, `atanf()`, `atanl()`, `atan2()`, `atan2f()`, `atan2l()` {#man-atan number="13.11"}

Calculate the arc tangent of a number.

### Synopsis {#synopsis-59 .unnumbered .unlisted}

::: {#cb256 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double atan(double x);
float atanf(float x);
long double atanl(long double x);

double atan2(double y, double x);
float atan2f(float y, float x);
long double atan2l(long double y, long double x);
```
:::

### Description {#description-59 .unnumbered .unlisted}

Calculates the arc tangent of a number in radians. (That is, the value whose tangent is `x`.)

The `atan2()` variants are pretty much the same as using `atan()` with `y`/`x` as the argument...except that `atan2()` will use those values to determine the correct quadrant of the result.

For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

::: {#cb257 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-58 .unnumbered .unlisted}

The `atan()` functions return the arc tangent of `x`, which will be between PI/2 and -PI/2. The `atan2()` functions return an angle between PI and -PI.

### Example {#example-59 .unnumbered .unlisted}

::: {#cb258 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double atanx;
    long double ldatanx;

    atanx = atan(0.7);
    ldatanx = atanl(0.3L);

    printf("%f\n", atanx);
    printf("%Lf\n", ldatanx);

    atanx = atan2(7, 10);
    ldatanx = atan2l(3L, 10L);

    printf("%f\n", atanx);
    printf("%Lf\n", ldatanx);
}
```
:::

### See Also {#see-also-55 .unnumbered .unlisted}

[`tan()`](math.html#man-tan), [`asin()`](math.html#man-asin), [`atan()`](math.html#man-acos)

------------------------------------------------------------------------

## [13.12]{.header-section-number} `cos()`, `cosf()`, `cosl()` {#man-cos number="13.12"}

Calculate the cosine of a number.

### Synopsis {#synopsis-60 .unnumbered .unlisted}

::: {#cb259 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double cos(double x)
float cosf(float x)
long double cosl(long double x)
```
:::

### Description {#description-60 .unnumbered .unlisted}

Calculates the cosine of the value `x`, where `x` is in radians.

For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

::: {#cb260 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-59 .unnumbered .unlisted}

Returns the cosine of `x`. The variants return different types.

### Example {#example-60 .unnumbered .unlisted}

::: {#cb261 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double cosx;
    long double ldcosx;

    cosx = cos(3490.0); // round and round we go!
    ldcosx = cosl(3.490L);

    printf("%f\n", cosx);
    printf("%Lf\n", ldcosx);
}
```
:::

### See Also {#see-also-56 .unnumbered .unlisted}

[`sin()`](math.html#man-sin), [`tan()`](math.html#man-tan), [`acos()`](math.html#man-acos)

------------------------------------------------------------------------

## [13.13]{.header-section-number} `sin()`, `sinf()`, `sinl()` {#man-sin number="13.13"}

Calculate the sine of a number.

### Synopsis {#synopsis-61 .unnumbered .unlisted}

::: {#cb262 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double sin(double x);
float sinf(float x);
long double sinl(long double x);
```
:::

### Description {#description-61 .unnumbered .unlisted}

Calculates the sine of the value `x`, where `x` is in radians.

For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

::: {#cb263 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-60 .unnumbered .unlisted}

Returns the sine of `x`. The variants return different types.

### Example {#example-61 .unnumbered .unlisted}

::: {#cb264 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double sinx;
    long double ldsinx;

    sinx = sin(3490.0); // round and round we go!
    ldsinx = sinl(3.490L);

    printf("%f\n", sinx);
    printf("%Lf\n", ldsinx);
}
```
:::

### See Also {#see-also-57 .unnumbered .unlisted}

[`cos()`](math.html#man-cos), [`tan()`](math.html#man-tan), [`asin()`](math.html#man-asin)

------------------------------------------------------------------------

## [13.14]{.header-section-number} `tan()`, `tanf()`, `tanl()` {#man-tan number="13.14"}

Calculate the tangent of a number.

### Synopsis {#synopsis-62 .unnumbered .unlisted}

::: {#cb265 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double tan(double x)
float tanf(float x)
long double tanl(long double x)
```
:::

### Description {#description-62 .unnumbered .unlisted}

Calculates the tangent of the value `x`, where `x` is in radians.

For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

::: {#cb266 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-61 .unnumbered .unlisted}

Returns the tangent of `x`. The variants return different types.

### Example {#example-62 .unnumbered .unlisted}

::: {#cb267 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double tanx;
    long double ldtanx;

    tanx = tan(3490.0); // round and round we go!
    ldtanx = tanl(3.490L);

    printf("%f\n", tanx);
    printf("%Lf\n", ldtanx);
}
```
:::

### See Also {#see-also-58 .unnumbered .unlisted}

[`sin()`](math.html#man-sin), [`cos()`](math.html#man-cos), [`atan()`](math.html#man-atan), [`atan2()`](math.html#man-atan)

------------------------------------------------------------------------

## [13.15]{.header-section-number} `acosh()`, `acoshf()`, `acoshl()` {#man-acosh number="13.15"}

Compute arc hyperbolic cosine.

### Synopsis {#synopsis-63 .unnumbered .unlisted}

::: {#cb268 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double acosh(double x);

float acoshf(float x);

long double acoshl(long double x);
```
:::

### Description {#description-63 .unnumbered .unlisted}

Trig lovers can rejoice! C has arc hyperbolic cosine!

These functions return the nonnegative acosh of `x`, which must be greater than or equal to `1`.

### Return Value {#return-value-62 .unnumbered .unlisted}

Returns the arc hyperbolic cosince in the range [\\(\[0,+\\infty\]\\)]{.math .inline}.

### Example {#example-63 .unnumbered .unlisted}

::: {#cb269 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("acosh 1.8 = %f\n", acosh(1.8));  // 1.192911
}
```
:::

### See Also {#see-also-59 .unnumbered .unlisted}

[`asinh()`](math.html#man-asinh)

------------------------------------------------------------------------

## [13.16]{.header-section-number} `asinh()`, `asinhf()`, `asinhl()` {#man-asinh number="13.16"}

Compute arc hyperbolic sine.

### Synopsis {#synopsis-64 .unnumbered .unlisted}

::: {#cb270 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double asinh(double x);

float asinhf(float x);

long double asinhl(long double x);
```
:::

### Description {#description-64 .unnumbered .unlisted}

Trig lovers can rejoice! C has arc hyperbolic sine!

These functions return the asinh of `x`.

### Return Value {#return-value-63 .unnumbered .unlisted}

Returns the arc hyperbolic sine.

### Example {#example-64 .unnumbered .unlisted}

::: {#cb271 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("asinh 1.8 = %f\n", asinh(1.8));  // 1.350441
}
```
:::

### See Also {#see-also-60 .unnumbered .unlisted}

[`acosh()`](math.html#man-acosh)

------------------------------------------------------------------------

## [13.17]{.header-section-number} `atanh()`, `atanhf()`, `atanhl()` {#man-atanh number="13.17"}

Compute the arc hyperbolic tangent.

### Synopsis {#synopsis-65 .unnumbered .unlisted}

::: {#cb272 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double atanh(double x);

float atanhf(float x);

long double atanhl(long double x);
```
:::

### Description {#description-65 .unnumbered .unlisted}

These functions compute the arc hyperbolic tangent of `x`, which must be in the range [\\(\[-1,+1\]\\)]{.math .inline}. Passing exactly [\\(-1\\)]{.math .inline} or [\\(+1\\)]{.math .inline} might result in a pole error.

### Return Value {#return-value-64 .unnumbered .unlisted}

Returns the arc hyperbolic tangent of `x`.

### Example {#example-65 .unnumbered .unlisted}

::: {#cb273 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("atanh 0.5 = %f\n", atanh(0.5));  // 0.549306
}
```
:::

### See Also {#see-also-61 .unnumbered .unlisted}

[`acosh()`](math.html#man-acosh), [`asinh()`](math.html#man-asinh)

------------------------------------------------------------------------

## [13.18]{.header-section-number} `cosh()`, `coshf()`, `coshl()` {#man-cosh number="13.18"}

Compute the hyperbolic cosine.

### Synopsis {#synopsis-66 .unnumbered .unlisted}

::: {#cb274 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double cosh(double x);

float coshf(float x);

long double coshl(long double x);
```
:::

### Description {#description-66 .unnumbered .unlisted}

These functions predictably compute the hyperbolic cosine of `x`. A range error might occur if `x` is too large.

### Return Value {#return-value-65 .unnumbered .unlisted}

Returns the hyperbolic cosine of `x`.

### Example {#example-66 .unnumbered .unlisted}

::: {#cb275 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("cosh 0.5 = %f\n", cosh(0.5));  // 1.127626
}
```
:::

### See Also {#see-also-62 .unnumbered .unlisted}

[`sinh()`](math.html#man-sinh), [`tanh()`](math.html#man-tanh)

------------------------------------------------------------------------

## [13.19]{.header-section-number} `sinh()`, `sinhf()`, `sinhl()` {#man-sinh number="13.19"}

Compute the hyperbolic sine.

### Synopsis {#synopsis-67 .unnumbered .unlisted}

::: {#cb276 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double sinh(double x);

float sinhf(float x);

long double sinhl(long double x);
```
:::

### Description {#description-67 .unnumbered .unlisted}

These functions predictably compute the hyperbolic sine of `x`. A range error might occur if `x` is too large.

### Return Value {#return-value-66 .unnumbered .unlisted}

Returns the hyperbolic sine of `x`.

### Example {#example-67 .unnumbered .unlisted}

::: {#cb277 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("sinh 0.5 = %f\n", sinh(0.5));  // 0.521095
}
```
:::

### See Also {#see-also-63 .unnumbered .unlisted}

[`sinh()`](math.html#man-cosh), [`tanh()`](math.html#man-tanh)

------------------------------------------------------------------------

## [13.20]{.header-section-number} `tanh()`, `tanhf()`, `tanhl()` {#man-tanh number="13.20"}

Compute the hyperbolic tangent.

### Synopsis {#synopsis-68 .unnumbered .unlisted}

::: {#cb278 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double tanh(double x);

float tanhf(float x);

long double tanhl(long double x);
```
:::

### Description {#description-68 .unnumbered .unlisted}

These functions predictably compute the hyperbolic tangent of `x`.

Mercifully, this is the last trig-related man page I'm going to write.

### Return Value {#return-value-67 .unnumbered .unlisted}

Returns the hyperbolic tangent of `x`.

### Example {#example-68 .unnumbered .unlisted}

::: {#cb279 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("tanh 0.5 = %f\n", tanh(0.5));  // 0.462117
}
```
:::

### See Also {#see-also-64 .unnumbered .unlisted}

[`cosh()`](math.html#man-cosh), [`sinh()`](math.html#man-sinh)

------------------------------------------------------------------------

## [13.21]{.header-section-number} `exp()`, `expf()`, `expl()` {#man-exp number="13.21"}

Compute [\\(e\\)]{.math .inline} raised to a power.

### Synopsis {#synopsis-69 .unnumbered .unlisted}

::: {#cb280 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double exp(double x);

float expf(float x);

long double expl(long double x);
```
:::

### Description {#description-69 .unnumbered .unlisted}

Compute [\\(e\^x\\)]{.math .inline} where [\\(e\\)]{.math .inline} is [Euler's number](https://en.wikipedia.org/wiki/E_(mathematical_constant))[^25^](footnotes.html#fn25){#fnref25 .footnote-ref role="doc-noteref"}.

The number [\\(e\\)]{.math .inline} is named after Leonard Euler, born April 15, 1707, who is responsible, among other things, for making this reference page longer than it needed to be.

### Return Value {#return-value-68 .unnumbered .unlisted}

Returns [\\(e\^x\\)]{.math .inline}.

### Example {#example-69 .unnumbered .unlisted}

::: {#cb281 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("exp(1) = %f\n", exp(1));  // 2.718282
    printf("exp(2) = %f\n", exp(2));  // 7.389056
}
```
:::

### See Also {#see-also-65 .unnumbered .unlisted}

[`exp2()`](math.html#man-exp2), [`expm1()`](math.html#man-expm1), [`pow()`](math.html#man-pow), [`log()`](math.html#man-log)

------------------------------------------------------------------------

## [13.22]{.header-section-number} `exp2()`, `exp2f()`, `exp2l()` {#man-exp2 number="13.22"}

Compute 2 to a power.

### Synopsis {#synopsis-70 .unnumbered .unlisted}

::: {#cb282 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double exp2(double x);

float exp2f(float x);

long double exp2l(long double x);
```
:::

### Description {#description-70 .unnumbered .unlisted}

These functions raise 2 to a power. Very exciting, since computers are all about twos-to-powers!

These are likely to be faster than using `pow()` to do the same thing.

They support fractional exponents, as well.

A range error occurs if `x` is too large.

### Return Value {#return-value-69 .unnumbered .unlisted}

`exp2()` returns [\\(2\^x\\)]{.math .inline}.

### Example {#example-70 .unnumbered .unlisted}

::: {#cb283 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("2^3 = %f\n", exp2(3));      // 2^3 = 8.000000
    printf("2^8 = %f\n", exp2(8));      // 2^8 = 256.000000
    printf("2^0.5 = %f\n", exp2(0.5));  // 2^0.5 = 1.414214    
}
```
:::

### See Also {#see-also-66 .unnumbered .unlisted}

[`exp()`](math.html#man-exp), [`pow()`](math.html#man-pow)

------------------------------------------------------------------------

## [13.23]{.header-section-number} `expm1()`, `expm1f()`, `expm1l()` {#man-expm1 number="13.23"}

Compute [\\(e\^x-1\\)]{.math .inline}.

### Synopsis {#synopsis-71 .unnumbered .unlisted}

::: {#cb284 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double expm1(double x);

float expm1f(float x);

long double expm1l(long double x);
```
:::

### Description {#description-71 .unnumbered .unlisted}

This is just like `exp()` except---*plot twist!*--it computes that result minus one.

For more discussion about what [\\(e\\)]{.math .inline} is, see [the `exp()` man page](math.html#man-exp).

If `x` is giant, a range error might occur.

For small values of `x` near zero, `expm1(x)` might be more accurate than computing `exp(x)-1`.

### Return Value {#return-value-70 .unnumbered .unlisted}

Returns [\\(e\^x-1\\)]{.math .inline}.

### Example {#example-71 .unnumbered .unlisted}

::: {#cb285 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", expm1(2.34));  // 9.381237
}
```
:::

### See Also {#see-also-67 .unnumbered .unlisted}

[`exp()`](math.html#man-exp)

------------------------------------------------------------------------

## [13.24]{.header-section-number} `frexp()`, `frexpf()`, `frexpl()` {#man-frexp number="13.24"}

Break a number into its fraction part and exponent (as a power of 2).

### Synopsis {#synopsis-72 .unnumbered .unlisted}

::: {#cb286 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double frexp(double value, int *exp);

float frexpf(float value, int *exp);

long double frexpl(long double value, int *exp);
```
:::

### Description {#description-72 .unnumbered .unlisted}

If you have a floating point number, you can break it into its fractional part and exponent part (as a power of 2).

For example, if you have the number [\\(1234.56\\)]{.math .inline}, this can be represented as a multiple of a power of 2 like so:

[\\(1234.56=0.6028125\\times2\^{11}\\)]{.math .inline}

And you can use this function to get the [\\(0.6028125\\)]{.math .inline} and [\\(11\\)]{.math .inline} parts of that equation.

As for why, I have a simple answer: I don't know. I can't find a use. K&R2 and everyone else I can find just says *how* to use it, but not *why* you might want to.

The C99 Rationale document says:

> The functions `frexp`, `ldexp`, and `modf` are primitives used by the remainder of the library.
>
> There was some sentiment for dropping them for the same reasons that `ecvt`, `fcvt`, and `gcvt` were dropped, but their adherents rescued them for general use. Their use is problematic: on non-binary architectures, ldexp may lose precision and frexp may be inefficient.

So there you have it. If you need it.

### Return Value {#return-value-71 .unnumbered .unlisted}

`frexp()` returns the fractional part of `value` in the range 0.5 (inclusive) to 1 (exclusive), or 0. And it stores the exponent power-of-2 in the variable pointed to by `exp`.

If you pass in zero, the return value and the variable `exp` points to are both zero.

### Example {#example-72 .unnumbered .unlisted}

::: {#cb287 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double frac;
    int expt;

    frac = frexp(1234.56, &expt);
    printf("1234.56 = %.7f x 2^%d\n", frac, expt);  
}
```
:::

Output:

::: {#cb288 .sourceCode}
``` {.sourceCode .default}
1234.56 = 0.6028125 x 2^11
```
:::

### See Also {#see-also-68 .unnumbered .unlisted}

[`ldexp()`](math.html#man-ldexp), [`ilogb()`](math.html#man-ldexp), [`modf()`](math.html#man-modf)

------------------------------------------------------------------------

## [13.25]{.header-section-number} `ilogb()`, `ilogbf()`, `ilogbl()` {#man-ilogb number="13.25"}

Return the exponent of a floating point number.

### Synopsis {#synopsis-73 .unnumbered .unlisted}

::: {#cb289 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

int ilogb(double x);

int ilogbf(float x);

int ilogbl(long double x);
```
:::

### Description {#description-73 .unnumbered .unlisted}

This gives you the exponent of the given number... it's a little weird, because the exponent depends on the value of `FLT_RADIX`. Now, this is very often `2`---but no guarantees!

It actually returns [\\(\\log_r\|x\|\\)]{.math .inline} where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

Domain or range errors might occur for invalid values of `x`, or for return values that are outside the range of the return type.

### Return Value {#return-value-72 .unnumbered .unlisted}

The exponent of the absolute value of the given number, depending on `FLT_RADIX`.

Specifically [\\(\\log_r\|x\|\\)]{.math .inline} where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

If you pass in `0`, it'll return `FP_ILOGB0`.

If you pass in infinity, it'll return `INT_MAX`.

If you pass in NaN, it'll return `FP_ILOGBNAN`.

The spec goes on to say that the value of `FP_ILOGB0` will be either `INT_MIN` or `-INT_MAX`. And the value of `FP_ILOGBNAN` shall be either `INT_MAX` or `INT_MIN`, if that's useful in any way.

### Example {#example-73 .unnumbered .unlisted}

::: {#cb290 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%d\n", ilogb(257));  // 8
    printf("%d\n", ilogb(256));  // 8
    printf("%d\n", ilogb(255));  // 7
}
```
:::

### See Also {#see-also-69 .unnumbered .unlisted}

[`frexp()`](math.html#man-frexp), [`logb()`](math.html#man-logb)

------------------------------------------------------------------------

## [13.26]{.header-section-number} `ldexp()`, `ldexpf()`, `ldexpl()` {#man-ldexp number="13.26"}

Multiply a number by an integral power of 2.

### Synopsis {#synopsis-74 .unnumbered .unlisted}

::: {#cb291 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double ldexp(double x, int exp);

float ldexpf(float x, int exp);

long double ldexpl(long double x, int exp);
```
:::

### Description {#description-74 .unnumbered .unlisted}

These functions multiply the given number `x` by 2 raised to the `exp` power.

### Return Value {#return-value-73 .unnumbered .unlisted}

Returns [\\(x\\times2\^{exp}\\)]{.math .inline}.

### Example {#example-74 .unnumbered .unlisted}

::: {#cb292 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("1 x 2^10 = %f\n", ldexp(1, 10));
    printf("5.67 x 2^7 = %f\n", ldexp(5.67, 7));
}
```
:::

Output:

::: {#cb293 .sourceCode}
``` {.sourceCode .default}
1 x 2^10 = 1024.000000
5.67 x 2^7 = 725.760000
```
:::

### See Also {#see-also-70 .unnumbered .unlisted}

[`exp()`](math.html#man-exp)

------------------------------------------------------------------------

## [13.27]{.header-section-number} `log()`, `logf()`, `logl()` {#man-log number="13.27"}

Compute the natural logarithm.

### Synopsis {#synopsis-75 .unnumbered .unlisted}

::: {#cb294 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double log(double x);

float logf(float x);

long double logl(long double x);
```
:::

### Description {#description-75 .unnumbered .unlisted}

Natural logarithms! And there was much rejoycing.

These compute the base-[\\(e\\)]{.math .inline} logarithm of a number, [\\(\\log_ex\\)]{.math .inline}, [\\(\\ln x\\)]{.math .inline}.

In other words, for a given [\\(x\\)]{.math .inline}, solves [\\(x=e\^y\\)]{.math .inline} for [\\(y\\)]{.math .inline}.

### Return Value {#return-value-74 .unnumbered .unlisted}

The base-[\\(e\\)]{.math .inline} logarithm of the given value, [\\(\\log_ex\\)]{.math .inline}, [\\(\\ln x\\)]{.math .inline}.

### Example {#example-75 .unnumbered .unlisted}

::: {#cb295 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    const double e = 2.718281828459045;

    printf("%f\n", log(3490.2));  // 8.157714
    printf("%f\n", log(e));       // 1.000000
}
```
:::

### See Also {#see-also-71 .unnumbered .unlisted}

[`exp()`](math.html#man-exp), [`log10()`](math.html#man-log10), [`log1p()`](math.html#man-log10)

------------------------------------------------------------------------

## [13.28]{.header-section-number} `log10()`, `log10f()`, `log10l()` {#man-log10 number="13.28"}

Compute the log-base-10 of a number.

### Synopsis {#synopsis-76 .unnumbered .unlisted}

::: {#cb296 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double log10(double x);

float log10f(float x);

long double log10l(long double x);
```
:::

### Description {#description-76 .unnumbered .unlisted}

Just when you thought you might have to use Laws of Logarithms to compute this, here's a function coming out of the blue to save you.

These compute the base-[\\(10\\)]{.math .inline} logarithm of a number, [\\(\\log\_{10}x\\)]{.math .inline}.

In other words, for a given [\\(x\\)]{.math .inline}, solves [\\(x=10\^y\\)]{.math .inline} for [\\(y\\)]{.math .inline}.

### Return Value {#return-value-75 .unnumbered .unlisted}

Returns the log base-10 of `x`, [\\(\\log\_{10}x\\)]{.math .inline}.

### Example {#example-76 .unnumbered .unlisted}

::: {#cb297 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", log10(3490.2));   // 3.542850
    printf("%f\n", log10(10));       // 1.000000
}
```
:::

### See Also {#see-also-72 .unnumbered .unlisted}

[`pow()`](math.html#man-pow), [`log()`](math.html#man-log)

------------------------------------------------------------------------

## [13.29]{.header-section-number} `log1p()`, `log1pf()`, `log1pl()` {#man-log1p number="13.29"}

Compute the natural logarithm of a number plus 1.

### Synopsis {#synopsis-77 .unnumbered .unlisted}

::: {#cb298 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double log1p(double x);

float log1pf(float x);

long double log1pl(long double x);
```
:::

### Description {#description-77 .unnumbered .unlisted}

This computes [\\(\\log_e(1 + x)\\)]{.math .inline}, [\\(\\ln(1+x)\\)]{.math .inline}.

This works just like calling:

::: {#cb299 .sourceCode}
``` {.sourceCode .c}
log(1 + x)
```
:::

except it could be more accurate for small values of `x`.

So if your `x` is small magnitude, use this.

### Return Value {#return-value-76 .unnumbered .unlisted}

Returns [\\(\\log_e(1 + x)\\)]{.math .inline}, [\\(\\ln(1+x)\\)]{.math .inline}.

### Example {#example-77 .unnumbered .unlisted}

Compute some big and small logarithm values to see the difference between `log1p()` and `log()`:

::: {#cb300 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <float.h> // for LDBL_DECIMAL_DIG
#include <math.h>

int main(void)
{
    printf("Big log1p()  : %.*Lf\n", LDBL_DECIMAL_DIG-1, log1pl(9));
    printf("Big log()    : %.*Lf\n", LDBL_DECIMAL_DIG-1, logl(1 + 9));

    printf("Small log1p(): %.*Lf\n", LDBL_DECIMAL_DIG-1, log1pl(0.01));
    printf("Small log()  : %.*Lf\n", LDBL_DECIMAL_DIG-1, logl(1 + 0.01));
}
```
:::

Output on my system:

::: {#cb301 .sourceCode}
``` {.sourceCode .default}
Big log1p()  : 2.30258509299404568403
Big log()    : 2.30258509299404568403
Small log1p(): 0.00995033085316808305
Small log()  : 0.00995033085316809164
```
:::

### See Also {#see-also-73 .unnumbered .unlisted}

[`log()`](math.html#man-log)

------------------------------------------------------------------------

## [13.30]{.header-section-number} `log2()`, `log2f()`, `log2l()` {#man-log2 number="13.30"}

Compute the base-2 logarithm of a number.

### Synopsis {#synopsis-78 .unnumbered .unlisted}

::: {#cb302 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double log2(double x);

float log2f(float x);

long double log2l(long double x);
```
:::

### Description {#description-78 .unnumbered .unlisted}

Wow! Were you thinking we were done with the logarithm functions? We're only getting started!

This one computes [\\(\\log_2 x\\)]{.math .inline}. That is, computes [\\(y\\)]{.math .inline} that satisfies [\\(x=2\^y\\)]{.math .inline}.

Love me those powers of 2!

### Return Value {#return-value-77 .unnumbered .unlisted}

Returns the base-2 logarithm of the given value, [\\(\\log_2 x\\)]{.math .inline}.

### Example {#example-78 .unnumbered .unlisted}

::: {#cb303 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", log2(3490.2));  // 11.769094
    printf("%f\n", log2(256));     // 8.000000
}
```
:::

### See Also {#see-also-74 .unnumbered .unlisted}

[`log()`](math.html#man-log)

------------------------------------------------------------------------

## [13.31]{.header-section-number} `logb()`, `logbf()`, `logbl()` {#man-logb number="13.31"}

Extract the exponent of a number given `FLT_RADIX`.

### Synopsis {#synopsis-79 .unnumbered .unlisted}

::: {#cb304 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double logb(double x);

float logbf(float x);

long double logbl(long double x);
```
:::

### Description {#description-79 .unnumbered .unlisted}

This function returns the whole number portion of the exponent of the number with radix `FLT_RADIX`, namely the whole number portion [\\(\\log_r\|x\|\\)]{.math .inline} where [\\(r\\)]{.math .inline} is `FLT_RADIX`. Fractional numbers are truncated.

If the number is [subnormal](https://en.wikipedia.org/wiki/Denormal_number)[^26^](footnotes.html#fn26){#fnref26 .footnote-ref role="doc-noteref"}, `logb()` treats it as if it were normalized.

If `x` is `0`, there could be a domain error or pole error.

### Return Value {#return-value-78 .unnumbered .unlisted}

This function returns the whole number portion of [\\(\\log_r\|x\|\\)]{.math .inline} where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

### Example {#example-79 .unnumbered .unlisted}

::: {#cb305 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <float.h>  // For FLT_RADIX
#include <math.h>

int main(void)
{
    printf("FLT_RADIX = %d\n", FLT_RADIX);
    printf("%f\n", logb(3490.2));
    printf("%f\n", logb(256));
}
```
:::

Output:

::: {#cb306 .sourceCode}
``` {.sourceCode .default}
FLT_RADIX = 2
11.000000
8.000000
```
:::

### See Also {#see-also-75 .unnumbered .unlisted}

[`ilogb()`](math.html#man-ilogb)

------------------------------------------------------------------------

## [13.32]{.header-section-number} `modf()`, `modff()`, `modfl()` {#man-modf number="13.32"}

Extract the integral and fractional parts of a number.

### Synopsis {#synopsis-80 .unnumbered .unlisted}

::: {#cb307 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double modf(double value, double *iptr);

float modff(float value, float *iptr);

long double modfl(long double value, long double *iptr);
```
:::

### Description {#description-80 .unnumbered .unlisted}

If you have a floating point number, like `123.456`, this function will extract the integral part (`123.0`) and the fractional part (`0.456`). It's total coincidence that this is exactly the plot for the latest Jason Statham action spectacular.

Both the integral part and fractional parts keep the sign of the passed in `value`.

The integral part is stored in the address pointed to by `iptr`.

See the note in [`frexp()`](math.html#man-frexp) regarding why this is in the library.

### Return Value {#return-value-79 .unnumbered .unlisted}

These functions return the fractional part of the number. The integral part is stored in the address pointed to by `iptr`. Both the integral and fractional parts preserve the sign of the passed-in `value`.

### Example {#example-80 .unnumbered .unlisted}

::: {#cb308 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

void print_parts(double x)
{
    double i, f;

    f = modf(x, &i);

    printf("Entire number  : %f\n", x);
    printf("Integral part  : %f\n", i);
    printf("Fractional part: %f\n\n", f);
}

int main(void)
{
    print_parts(123.456);
    print_parts(-123.456);
}
```
:::

Output:

::: {#cb309 .sourceCode}
``` {.sourceCode .default}
Entire number  : 123.456000
Integral part  : 123.000000
Fractional part: 0.456000

Entire number  : -123.456000
Integral part  : -123.000000
Fractional part: -0.456000
```
:::

### See Also {#see-also-76 .unnumbered .unlisted}

[`frexp()`](math.html#man-frexp)

------------------------------------------------------------------------

## [13.33]{.header-section-number} `scalbn()`, `scalbnf()`, `scalbnl()` `scalbln()`, `scalblnf()`, `scalblnl()` {#man-scalb number="13.33"}

Efficiently compute [\\(x\\times r\^n\\)]{.math .inline}, where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

### Synopsis {#synopsis-81 .unnumbered .unlisted}

::: {#cb310 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double scalbn(double x, int n);

float scalbnf(float x, int n);

long double scalbnl(long double x, int n);

double scalbln(double x, long int n);

float scalblnf(float x, long int n);

long double scalblnl(long double x, long int n);
```
:::

### Description {#description-81 .unnumbered .unlisted}

These functions efficiently compute [\\(x\\times r\^n\\)]{.math .inline}, where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

If `FLT_RADIX` happens to be `2` (no guarantees!), then this works like [`exp2()`](math.html#man-exp2).

The name of this function should have an obvious meaning to you. Clearly they all start with the prefix "scalb" which means...

...OK, I confess! I have no idea what it means. My searches are futile!

But let's look at the suffixes:

  Suffix   Meaning
  -------- -----------------------------------------------------
  `n`      `scalbn()`---exponent `n` is an `int`
  `nf`     `scalbnf()`---`float` version of `scalbn()`
  `nl`     `scalbnl()`---`long double` version of `scalbn()`
  `ln`     `scalbln()`---exponent `n` is a `long int`
  `lnf`    `scalblnf()`---`float` version of `scalbln()`
  `lnl`    `scalblnl()`---`long double` version of `scalbln()`

So while I'm still in the dark about "scalb", at least I have that part down.

A range error might occur for large values.

### Return Value {#return-value-80 .unnumbered .unlisted}

Returns [\\(x\\times r\^n\\)]{.math .inline}, where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

### Example {#example-81 .unnumbered .unlisted}

::: {#cb311 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <float.h>

int main(void)
{
    printf("FLT_RADIX = %d\n\n", FLT_RADIX);
    printf("scalbn(3, 8)      = %f\n", scalbn(2, 8));
    printf("scalbnf(10.2, 20) = %f\n", scalbnf(10.2, 20));
}
```
:::

Output on my system:

::: {#cb312 .sourceCode}
``` {.sourceCode .default}
FLT_RADIX = 2

scalbn(3, 8)       = 512.000000
scalbn(10.2, 20.7) = 10695475.200000
```
:::

### See Also {#see-also-77 .unnumbered .unlisted}

[`exp2()`](math.html#man-exp2), [`pow()`](math.html#man-pow)

------------------------------------------------------------------------

## [13.34]{.header-section-number} `cbrt()`, `cbrtf()`, `cbrtl()` {#man-cbrt number="13.34"}

Compute the cube root.

### Synopsis {#synopsis-82 .unnumbered .unlisted}

::: {#cb313 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double cbrt(double x);

float cbrtf(float x);

long double cbrtl(long double x);
```
:::

### Description {#description-82 .unnumbered .unlisted}

Computes the cube root of `x`, [\\(x\^{1/3}\\)]{.math .inline}, [\\(\\sqrt\[3\]{x}\\)]{.math .inline}.

### Return Value {#return-value-81 .unnumbered .unlisted}

Returns the cube root of `x`, [\\(x\^{1/3}\\)]{.math .inline}, [\\(\\sqrt\[3\]{x}\\)]{.math .inline}.

### Example {#example-82 .unnumbered .unlisted}

::: {#cb314 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("cbrt(1729.03) = %f\n", cbrt(1729.03));
}
```
:::

Output:

::: {#cb315 .sourceCode}
``` {.sourceCode .default}
cbrt(1729.03) = 12.002384
```
:::

### See Also {#see-also-78 .unnumbered .unlisted}

[`sqrt()`](math.html#man-sqrt), [`pow()`](math.html#man-pow)

------------------------------------------------------------------------

## [13.35]{.header-section-number} `fabs()`, `fabsf()`, `fabsl()` {#man-fabs number="13.35"}

Compute the absolute value.

### Synopsis {#synopsis-83 .unnumbered .unlisted}

::: {#cb316 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double fabs(double x);

float fabsf(float x);

long double fabsl(long double x);
```
:::

### Description {#description-83 .unnumbered .unlisted}

These functions straightforwardly return the absolute value of `x`, that is [\\(\|x\|\\)]{.math .inline}.

If you're rusty on your absolute values, all it means is that the result will be positive, even if `x` is negative. It's just strips negative signs off.

### Return Value {#return-value-82 .unnumbered .unlisted}

Returns the absolute value of `x`, [\\(\|x\|\\)]{.math .inline}.

### Example {#example-83 .unnumbered .unlisted}

::: {#cb317 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("fabs(3490.0)  = %f\n", fabs(3490.0));  // 3490.000000
    printf("fabs(-3490.0) = %f\n", fabs(3490.0));  // 3490.000000
}
```
:::

### See Also {#see-also-79 .unnumbered .unlisted}

[`abs()`](stdlib.html#man-abs), [`copysign()`](math.html#man-copysign), [`imaxabs()`](inttypes.html#man-imaxabs)

------------------------------------------------------------------------

## [13.36]{.header-section-number} `hypot()`, `hypotf()`, `hypotl()` {#man-hypot number="13.36"}

Compute the length of the hypotenuse of a triangle.

### Synopsis {#synopsis-84 .unnumbered .unlisted}

::: {#cb318 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double hypot(double x, double y);

float hypotf(float x, float y);

long double hypotl(long double x, long double y);
```
:::

### Description {#description-84 .unnumbered .unlisted}

[Pythagorean Theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem)[^27^](footnotes.html#fn27){#fnref27 .footnote-ref role="doc-noteref"} fans rejoice! This is the function you've been waiting for!

If you know the lengths of the two sides of a right triangle, `x` and `y`, you can compute the length of the hypotenuse (the longest, diagonal side) with this function.

In particular, it computes the square root of the sum of the squares of the sides: [\\(\\sqrt{x\^2 + y\^2}\\)]{.math .inline}.

### Return Value {#return-value-83 .unnumbered .unlisted}

Returns the lenght of the hypotenuse of a right triangle with side lengths `x` and `y`: [\\(\\sqrt{x\^2 + y\^2}\\)]{.math .inline}.

### Example {#example-84 .unnumbered .unlisted}

::: {#cb319 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
printf("%f\n", hypot(3, 4));  // 5.000000
```
:::

### See Also {#see-also-80 .unnumbered .unlisted}

[`sqrt()`](math.html#man-sqrt)

------------------------------------------------------------------------

## [13.37]{.header-section-number} `pow()`, `powf()`, `powl()` {#man-pow number="13.37"}

Compute a value raised to a power.

### Synopsis {#synopsis-85 .unnumbered .unlisted}

::: {#cb320 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double pow(double x, double y);

float powf(float x, float y);

long double powl(long double x, long double y);
```
:::

### Description {#description-85 .unnumbered .unlisted}

Computes `x` raised to the `y`th power: [\\(x\^y\\)]{.math .inline}.

These arguments can be fractional.

### Return Value {#return-value-84 .unnumbered .unlisted}

Returns `x` raised to the `y`th power: [\\(x\^y\\)]{.math .inline}.

A domain error can occur if:

-   `x` is a finite negative number and `y` is a finite non-integer
-   `x` is zero and `y` is zero.

A domain error or pole error can occur if `x` is zero and `y` is negative.

A range error can occur for large values.

### Example {#example-85 .unnumbered .unlisted}

::: {#cb321 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
printf("%f\n", pow(3, 4));    // 3^4    = 81.000000
printf("%f\n", pow(2, 0.5));  // sqrt 2 = 1.414214
```
:::

### See Also {#see-also-81 .unnumbered .unlisted}

[`exp()`](math.html#man-exp), [`exp2()`](math.html#man-exp2), [`sqrt()`](math.html#man-sqrt), [`cbrt()`](math.html#man-cbrt)

------------------------------------------------------------------------

## [13.38]{.header-section-number} `sqrt()` {#man-sqrt number="13.38"}

Calculate the square root of a number.

### Synopsis {#synopsis-86 .unnumbered .unlisted}

::: {#cb322 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double sqrt(double x);

float sqrtf(float x);

long double sqrtl(long double x);
```
:::

### Description {#description-86 .unnumbered .unlisted}

Computes the square root of a number: [\\(\\sqrt{x}\\)]{.math .inline}. To those of you who don't know what a square root is, I'm not going to explain. Suffice it to say, the square root of a number delivers a value that when squared (multiplied by itself) results in the original number.

Ok, fine---I did explain it after all, but only because I wanted to show off. It's not like I'm giving you examples or anything, such as the square root of nine is three, because when you multiply three by three you get nine, or anything like that. No examples. I hate examples!

And I suppose you wanted some actual practical information here as well. You can see the usual trio of functions here---they all compute square root, but they take different types as arguments. Pretty straightforward, really.

A domain error occurs if `x` is negative.

### Return Value {#return-value-85 .unnumbered .unlisted}

Returns (and I know this must be something of a surprise to you) the square root of `x`: [\\(\\sqrt{x}\\)]{.math .inline}.

### Example {#example-86 .unnumbered .unlisted}

::: {#cb323 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
// example usage of sqrt()

float something = 10;

double x1 = 8.2, y1 = -5.4;
double x2 = 3.8, y2 = 34.9;
double dx, dy;

printf("square root of 10 is %.2f\n", sqrtf(something));

dx = x2 - x1;
dy = y2 - y1;
printf("distance between points (x1, y1) and (x2, y2): %.2f\n",
    sqrt(dx*dx + dy*dy));
```
:::

And the output is:

::: {#cb324 .sourceCode}
``` {.sourceCode .default}
square root of 10 is 3.16
distance between points (x1, y1) and (x2, y2): 40.54
```
:::

### See Also {#see-also-82 .unnumbered .unlisted}

[`hypot()`](math.html#man-hypot), [`pow()`](math.html#man-pow)

------------------------------------------------------------------------

## [13.39]{.header-section-number} `erf()`, `erff()`, `erfl()` {#man-erf number="13.39"}

Compute the error function of the given value.

### Synopsis {#synopsis-87 .unnumbered .unlisted}

::: {#cb325 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double erfc(double x);

float erfcf(float x);

long double erfcl(long double x);
```
:::

### Description {#description-87 .unnumbered .unlisted}

These functions compute the [error function](https://en.wikipedia.org/wiki/Error_function)[^28^](footnotes.html#fn28){#fnref28 .footnote-ref role="doc-noteref"} of a value.

### Return Value {#return-value-86 .unnumbered .unlisted}

Returns the error function of `x`:

[\\({\\displaystyle \\frac{2}{\\sqrt\\pi} \\int_0\^x e\^{-t\^2}\\,dt}\\)]{.math .inline}

### Example {#example-87 .unnumbered .unlisted}

::: {#cb326 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
for (float i = -2; i <= 2; i += 0.5)
    printf("% .1f: %f\n", i, erf(i));
```
:::

Output:

::: {#cb327 .sourceCode}
``` {.sourceCode .default}
-2.0: -0.995322
-1.5: -0.966105
-1.0: -0.842701
-0.5: -0.520500
 0.0: 0.000000
 0.5: 0.520500
 1.0: 0.842701
 1.5: 0.966105
 2.0: 0.995322
```
:::

### See Also {#see-also-83 .unnumbered .unlisted}

[`erfc()`](math.html#man-erfc)

------------------------------------------------------------------------

## [13.40]{.header-section-number} `erfc()`, `erfcf()`, `erfcl()` {#man-erfc number="13.40"}

Compute the complementary error function of a value.

### Synopsis {#synopsis-88 .unnumbered .unlisted}

::: {#cb328 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double erfc(double x);

float erfcf(float x);

long double erfcl(long double x);
```
:::

### Description {#description-88 .unnumbered .unlisted}

These functions compute the [complementary error function](https://en.wikipedia.org/wiki/Error_function)[^29^](footnotes.html#fn29){#fnref29 .footnote-ref role="doc-noteref"} of a value.

This is the same as:

::: {#cb329 .sourceCode}
``` {.sourceCode .c}
1 - erf(x)
```
:::

A range error can occur if `x` is too large.

### Return Value {#return-value-87 .unnumbered .unlisted}

Returns `1 - erf(x)`, namely:

[\\({\\displaystyle \\frac{2}{\\sqrt\\pi} \\int_x\^{\\infty} e\^{-t\^2}\\,dt}\\)]{.math .inline}

### Example {#example-88 .unnumbered .unlisted}

::: {#cb330 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
for (float i = -2; i <= 2; i += 0.5)
    printf("% .1f: %f\n", i, erfc(i));
```
:::

Output:

::: {#cb331 .sourceCode}
``` {.sourceCode .default}
-2.0: 1.995322
-1.5: 1.966105
-1.0: 1.842701
-0.5: 1.520500
 0.0: 1.000000
 0.5: 0.479500
 1.0: 0.157299
 1.5: 0.033895
 2.0: 0.004678
```
:::

### See Also {#see-also-84 .unnumbered .unlisted}

[`erf()`](math.html#man-erf)

------------------------------------------------------------------------

## [13.41]{.header-section-number} `lgamma()`, `lgammaf()`, `lgammal()` {#man-lgamma number="13.41"}

Compute the natural logarithm of the absolute value of [\\(\\Gamma(x)\\)]{.math .inline}.

### Synopsis {#synopsis-89 .unnumbered .unlisted}

::: {#cb332 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double lgamma(double x);

float lgammaf(float x);

long double lgammal(long double x);
```
:::

### Description {#description-89 .unnumbered .unlisted}

Compute the natural log of the absolute value of [gamma](https://en.wikipedia.org/wiki/Gamma_function)[^30^](footnotes.html#fn30){#fnref30 .footnote-ref role="doc-noteref"} `x`, [\\(\\log_e\|\\Gamma(x)\|\\)]{.math .inline}.

A range error can occur if `x` is too large.

A pole error can occur is `x` is non-positive.

### Return Value {#return-value-88 .unnumbered .unlisted}

Returns [\\(\\log_e\|\\Gamma(x)\|\\)]{.math .inline}.

### Example {#example-89 .unnumbered .unlisted}

::: {#cb333 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
for (float i = 0.5; i <= 4; i += 0.5)
    printf("%.1f: %f\n", i, lgamma(i));
```
:::

Output:

::: {#cb334 .sourceCode}
``` {.sourceCode .default}
0.5: 0.572365
1.0: 0.000000
1.5: -0.120782
2.0: 0.000000
2.5: 0.284683
3.0: 0.693147
3.5: 1.200974
4.0: 1.791759
```
:::

### See Also {#see-also-85 .unnumbered .unlisted}

[`tgamma()`](math.html#man-tgamma)

------------------------------------------------------------------------

## [13.42]{.header-section-number} `tgamma()`, `tgammaf()`, `tgammal()` {#man-tgamma number="13.42"}

Compute the gamma function, [\\(\\Gamma(x)\\)]{.math .inline}.

### Synopsis {#synopsis-90 .unnumbered .unlisted}

::: {#cb335 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double tgamma(double x);

float tgammaf(float x);

long double tgammal(long double x);
```
:::

### Description {#description-90 .unnumbered .unlisted}

Computes the [gamma function](https://en.wikipedia.org/wiki/Gamma_function)[^31^](footnotes.html#fn31){#fnref31 .footnote-ref role="doc-noteref"} of `x`, [\\(\\Gamma(x)\\)]{.math .inline}.

A domain or pole error might occur if `x` is non-positive.

A range error might occur if `x` is too large or too small.

### Return Value {#return-value-89 .unnumbered .unlisted}

Returns the gamma function of `x`, [\\(\\Gamma(x)\\)]{.math .inline}.

### Example {#example-90 .unnumbered .unlisted}

::: {#cb336 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
for (float i = 0.5; i <= 4; i += 0.5)
    printf("%.1f: %f\n", i, tgamma(i));
```
:::

Output:

::: {#cb337 .sourceCode}
``` {.sourceCode .default}
0.5: 1.772454
1.0: 1.000000
1.5: 0.886227
2.0: 1.000000
2.5: 1.329340
3.0: 2.000000
3.5: 3.323351
4.0: 6.000000
```
:::

### See Also {#see-also-86 .unnumbered .unlisted}

[`lgamma()`](math.html#man-lgamma)

------------------------------------------------------------------------

## [13.43]{.header-section-number} `ceil()`, `ceilf()`, `ceill()` {#man-ceil number="13.43"}

Ceiling---return the next whole number not smaller than the given number.

### Synopsis {#synopsis-91 .unnumbered .unlisted}

::: {#cb338 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double ceil(double x);

float ceilf(float x);

long double ceill(long double x);
```
:::

### Description {#description-91 .unnumbered .unlisted}

Returns the ceiling of the `x`: [\\(\\lceil{x}\\rceil\\)]{.math .inline}.

This is the next whole number not smaller than `x`.

Beware this minor dragon: it's not just "rounding up". Well, it is for positive numbers, but negative numbers effectively round toward zero. (Because the ceiling function is headed for the next largest whole number and [\\(-4\\)]{.math .inline} is larger than [\\(-5\\)]{.math .inline}.)

### Return Value {#return-value-90 .unnumbered .unlisted}

Returns the next largest whole number larger than `x`.

### Example {#example-91 .unnumbered .unlisted}

Notice for the negative numbers it heads toward zero, i.e. toward the next largest whole number---just like the positives head toward the next largest whole number.

::: {#cb339 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
printf("%f\n", ceil(4.0));   //  4.000000
printf("%f\n", ceil(4.1));   //  5.000000
printf("%f\n", ceil(-2.0));  // -2.000000
printf("%f\n", ceil(-2.1));  // -2.000000
printf("%f\n", ceil(-3.1));  // -3.000000
```
:::

### See Also {#see-also-87 .unnumbered .unlisted}

[`floor()`](math.html#man-floor), [`round()`](math.html#man-round)

------------------------------------------------------------------------

## [13.44]{.header-section-number} `floor()`, `floorf()`, `floorl()` {#man-floor number="13.44"}

Compute the largest whole number not larger than the given value.

### Synopsis {#synopsis-92 .unnumbered .unlisted}

::: {#cb340 .sourceCode}
``` {.sourceCode .c}
#include <math.h>
double floor(double x);
float floorf(float x);
long double floorl(long double x);
```
:::

### Description {#description-92 .unnumbered .unlisted}

Returns the floor of the value: [\\(\\lfloor{x}\\rfloor\\)]{.math .inline}. This is the opposite of `ceil()`.

This is the largest whole number that is not greater than `x`.

For positive numbers, this is like rounding down: `4.5` becomes `4.0`.

For negative numbers, it's like rounding up: `-3.6` becomes `-4.0`.

In both cases, those results are the largest whole number not bigger than the given number.

### Return Value {#return-value-91 .unnumbered .unlisted}

Returns the largest whole number not greater than `x`: [\\(\\lfloor{x}\\rfloor\\)]{.math .inline}.

### Example {#example-92 .unnumbered .unlisted}

Note how the negative numbers effectively round away from zero, unlike the positives.

::: {#cb341 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
printf("%f\n", floor(4.0));   //  4.000000
printf("%f\n", floor(4.1));   //  4.000000
printf("%f\n", floor(-2.0));  // -2.000000
printf("%f\n", floor(-2.1));  // -3.000000
printf("%f\n", floor(-3.1));  // -4.000000
```
:::

### See Also {#see-also-88 .unnumbered .unlisted}

[`ceil()`](math.html#man-ceil), [`round()`](math.html#man-round)

------------------------------------------------------------------------

## [13.45]{.header-section-number} `nearbyint()`, `nearbyintf()`, `nearbyintl()` {#man-nearbyint number="13.45"}

Rounds a value in the current rounding direction.

### Synopsis {#synopsis-93 .unnumbered .unlisted}

::: {#cb342 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double nearbyint(double x);

float nearbyintf(float x);

long double nearbyintl(long double x);
```
:::

### Description {#description-93 .unnumbered .unlisted}

This function rounds `x` to the nearest integer in the current rounding direction.

The rounding direction can be set with [`fesetround()`](fenv.html#man-fegetround) in `<fenv.h>`.

`nearbyint()` won't raise the "inexact" floating point exception.

### Return Value {#return-value-92 .unnumbered .unlisted}

Returns `x` rounded in the current rounding direction.

### Example {#example-93 .unnumbered .unlisted}

::: {#cb343 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

int main(void)
{
    #pragma STDC FENV_ACCESS ON        // If supported

    fesetround(FE_TONEAREST);          // round to nearest

    printf("%f\n", nearbyint(3.14));   // 3.000000
    printf("%f\n", nearbyint(3.74));   // 4.000000

    fesetround(FE_TOWARDZERO);         // round toward zero

    printf("%f\n", nearbyint(1.99));   // 1.000000
    printf("%f\n", nearbyint(-1.99));  // -1.000000
}
```
:::

### See Also {#see-also-89 .unnumbered .unlisted}

[`rint()`](math.html#man-rint), [`lrint()`](math.html#man-lrint), [`round()`](math.html#man-round), [`fesetround()`](fenv.html#man-fegetround), [`fegetround()`](fenv.html#man-fegetround)

------------------------------------------------------------------------

## [13.46]{.header-section-number} `rint()`, `rintf()`, `rintl()` {#man-rint number="13.46"}

Rounds a value in the current rounding direction.

### Synopsis {#synopsis-94 .unnumbered .unlisted}

::: {#cb344 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double rint(double x);

float rintf(float x);

long double rintl(long double x);
```
:::

### Description {#description-94 .unnumbered .unlisted}

This works just like [`nearbyint()`](math.html#man-nearbyint) except that is can raise the "inexact" floating point exception.

### Return Value {#return-value-93 .unnumbered .unlisted}

Returns `x` rounded in the current rounding direction.

### Example {#example-94 .unnumbered .unlisted}

::: {#cb345 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

int main(void)
{
    #pragma STDC FENV_ACCESS ON

    fesetround(FE_TONEAREST);

    printf("%f\n", rint(3.14));   // 3.000000
    printf("%f\n", rint(3.74));   // 4.000000

    fesetround(FE_TOWARDZERO);

    printf("%f\n", rint(1.99));   // 1.000000
    printf("%f\n", rint(-1.99));  // -1.000000
}
```
:::

### See Also {#see-also-90 .unnumbered .unlisted}

[`nearbyint()`](math.html#man-nearbyint), [`lrint()`](math.html#man-lrint), [`round()`](math.html#man-round), [`fesetround()`](fenv.html#man-fegetround), [`fegetround()`](fenv.html#man-fegetround)

------------------------------------------------------------------------

## [13.47]{.header-section-number} `lrint()`, `lrintf()`, `lrintl()`, `llrint()`, `llrintf()`, `llrintl()` {#man-lrint number="13.47"}

Returns `x` rounded in the current rounding direction as an integer.

### Synopsis {#synopsis-95 .unnumbered .unlisted}

::: {#cb346 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

long int lrint(double x);
long int lrintf(float x);
long int lrintl(long double x);

long long int llrint(double x);
long long int llrintf(float x);
long long int llrintl(long double x);
```
:::

### Description {#description-95 .unnumbered .unlisted}

Round a floating point number in the current rounding direction, but this time return an integer intead of a float. You know, just to mix it up.

These come in two variants:

-   `lrint()`---returns `long int`
-   `llrint()`---returns `long long int`

If the result doesn't fit in the return type, a domain or range error might occur.

### Return Value {#return-value-94 .unnumbered .unlisted}

The value of `x` rounded to an integer in the current rounding direction.

### Example {#example-95 .unnumbered .unlisted}

::: {#cb347 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

int main(void)
{
    #pragma STDC FENV_ACCESS ON

    fesetround(FE_TONEAREST);

    printf("%ld\n", lrint(3.14));   // 3
    printf("%ld\n", lrint(3.74));   // 4

    fesetround(FE_TOWARDZERO);

    printf("%ld\n", lrint(1.99));   // 1
    printf("%ld\n", lrint(-1.99));  // -1
}
```
:::

### See Also {#see-also-91 .unnumbered .unlisted}

[`nearbyint()`](math.html#man-nearbyint), [`rint()`](math.html#man-lrint), [`round()`](math.html#man-round), [`fesetround()`](fenv.html#man-fegetround), [`fegetround()`](fenv.html#man-fegetround)

------------------------------------------------------------------------

## [13.48]{.header-section-number} `round()`, `roundf()`, `roundl()` {#man-round number="13.48"}

Round a number in the good old-fashioned way.

### Synopsis {#synopsis-96 .unnumbered .unlisted}

::: {#cb348 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double round(double x);

float roundf(float x);

long double roundl(long double x);
```
:::

### Description {#description-96 .unnumbered .unlisted}

Rounds a number to the nearest whole value.

In case of halfsies, rounds away from zero (i.e. "round up" in magnitude).

The current rounding direction's Jedi mind tricks don't work on this function.

### Return Value {#return-value-95 .unnumbered .unlisted}

The rounded value of `x`.

### Example {#example-96 .unnumbered .unlisted}

::: {#cb349 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", round(3.14));   // 3.000000
    printf("%f\n", round(3.5));    // 4.000000

    printf("%f\n", round(-1.5));   // -2.000000
    printf("%f\n", round(-1.14));  // -1.000000
}
```
:::

### See Also {#see-also-92 .unnumbered .unlisted}

[`lround()`](math.html#man-lround), [`nearbyint()`](math.html#man-nearbyint), [`rint()`](math.html#man-lrint), [`lrint()`](math.html#man-lrint), [`trunc()`](math.html#man-trunc)

------------------------------------------------------------------------

## [13.49]{.header-section-number} `lround()`, `lroundf()`, `lroundl()` `llround()`, `llroundf()`, `llroundl()` {#man-lround number="13.49"}

Round a number in the good old-fashioned way, returning an integer.

### Synopsis {#synopsis-97 .unnumbered .unlisted}

::: {#cb350 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

long int lround(double x);
long int lroundf(float x);
long int lroundl(long double x);

long long int llround(double x);
long long int llroundf(float x);
long long int llroundl(long double x);
```
:::

### Description {#description-97 .unnumbered .unlisted}

These are just like [`round()`](math.html#man-round) except they return integers.

Halfway values round away from zero, e.g. [\\(1.5\\)]{.math .inline} rounds to [\\(2\\)]{.math .inline} and [\\(-1.5\\)]{.math .inline} rounds to [\\(-2\\)]{.math .inline}.

The functions are grouped by return type:

-   `lround()`---returns a `long int`
-   `llround()`---returns a `long long int`

If the rounded value can't fit in the return type, a domain or range error can occur.

### Return Value {#return-value-96 .unnumbered .unlisted}

Returns the rounded value of `x` as an integer.

### Example {#example-97 .unnumbered .unlisted}

::: {#cb351 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%ld\n", lround(3.14));   // 3
    printf("%ld\n", lround(3.5));    // 4

    printf("%ld\n", lround(-1.5));   // -2
    printf("%ld\n", lround(-1.14));  // -1
}
```
:::

### See Also {#see-also-93 .unnumbered .unlisted}

[`round()`](math.html#man-lround), [`nearbyint()`](math.html#man-nearbyint), [`rint()`](math.html#man-lrint), [`lrint()`](math.html#man-lrint), [`trunc()`](math.html#man-trunc)

------------------------------------------------------------------------

## [13.50]{.header-section-number} `trunc()`, `truncf()`, `truncl()` {#man-trunc number="13.50"}

Truncate the fractional part off a floating point value.

### Synopsis {#synopsis-98 .unnumbered .unlisted}

::: {#cb352 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double trunc(double x);

float truncf(float x);

long double truncl(long double x);
```
:::

### Description {#description-98 .unnumbered .unlisted}

These functions just drop the fractional part of a floating point number. Boom.

In other words, they always round toward zero.

### Return Value {#return-value-97 .unnumbered .unlisted}

Returns the truncated floating point number.

### Example {#example-98 .unnumbered .unlisted}

::: {#cb353 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", trunc(3.14));   // 3.000000
    printf("%f\n", trunc(3.8));    // 3.000000

    printf("%f\n", trunc(-1.5));   // -1.000000
    printf("%f\n", trunc(-1.14));  // -1.000000
}
```
:::

### See Also {#see-also-94 .unnumbered .unlisted}

[`round()`](math.html#man-lround), [`lround()`](math.html#man-lround), [`nearbyint()`](math.html#man-nearbyint), [`rint()`](math.html#man-lrint), [`lrint()`](math.html#man-lrint)

------------------------------------------------------------------------

## [13.51]{.header-section-number} `fmod()`, `fmodf()`, `fmodl()` {#man-fmod number="13.51"}

Compute the floating point remainder.

### Synopsis {#synopsis-99 .unnumbered .unlisted}

::: {#cb354 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double fmod(double x, double y);

float fmodf(float x, float y);

long double fmodl(long double x, long double y);
```
:::

### Description {#description-99 .unnumbered .unlisted}

Returns the remainder of [\\(\\frac{x}{y}\\)]{.math .inline}. The result will have the same sign as `x`.

Under the hood, the computation performed is:

::: {#cb355 .sourceCode}
``` {.sourceCode .c}
x - trunc(x / y) * y
```
:::

But it might be easier just to think of the remainder.

### Return Value {#return-value-98 .unnumbered .unlisted}

Returns the remainder of [\\(\\frac{x}{y}\\)]{.math .inline} with the same sign as `x`.

### Example {#example-99 .unnumbered .unlisted}

::: {#cb356 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", fmod(-9.2, 5.1));  // -4.100000
    printf("%f\n", fmod(9.2, 5.1));   //  4.100000
}
```
:::

### See Also {#see-also-95 .unnumbered .unlisted}

[`remainder()`](math.html#man-remainder)

------------------------------------------------------------------------

## [13.52]{.header-section-number} `remainder()`, `remainderf()`, `remainderl()` {#man-remainder number="13.52"}

Compute the remainder IEC 60559-style.

### Synopsis {#synopsis-100 .unnumbered .unlisted}

::: {#cb357 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double remainder(double x, double y);

float remainderf(float x, float y);

long double remainderl(long double x, long double y);
```
:::

### Description {#description-100 .unnumbered .unlisted}

This is similar to `fmod()`, but not quite the same. `fmod()` is probably what you're after if you're expecting remainders to wrap around like an odometer.

The C spec quotes IEC 60559 on how this works:

> When [\\(y\\neq0\\)]{.math .inline}, the remainder [\\(r=x\\)]{.math .inline} REM [\\(y\\)]{.math .inline} is defined regardless of the rounding mode by the mathematical relation [\\(r=x-ny\\)]{.math .inline}, where [\\(n\\)]{.math .inline} is the integer nearest the exact value of [\\(x/y\\)]{.math .inline}; whenever [\\(\|n-x/y\|=1/2\\)]{.math .inline}, then [\\(n\\)]{.math .inline} is even. If [\\(r=0\\)]{.math .inline}, its sign shall be that of [\\(x\\)]{.math .inline}.

Hope that clears it up!

OK, maybe not. Here's the upshot:

You know how if you `fmod()` something by, say `2.0` you get a result that is somewhere between `0.0` and `2.0`? And how if you just increase the number that you're modding by `2.0`, you can see the result climb up to `2.0` and then wrap around to `0.0` like your car's odometer?

`remainder()` works just like that, except if `y` is `2.0`, it wraps from `-1.0` to `1.0` instead of from `0.0` to `2.0`.

In other words, the range of the function runs from `-y/2` to `y/2`. Contrasted to `fmod()` that runs from `0.0` to `y`, `remainder()`'s output is just shifted down half a `y`.

And zero-remainder-anything is `0`.

Except if `y` is zero, the function might return zero or a domain error might occur.

### Return Value {#return-value-99 .unnumbered .unlisted}

The IEC 60559 result of `x`-remainder-`y`.

### Example {#example-100 .unnumbered .unlisted}

::: {#cb358 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", remainder(3.7, 4));  // -0.300000
    printf("%f\n", remainder(4.3, 4));  //  0.300000
}
```
:::

### See Also {#see-also-96 .unnumbered .unlisted}

[`fmod()`](math.html#man-fmod), [`remquo()`](math.html#man-remquo)

------------------------------------------------------------------------

## [13.53]{.header-section-number} `remquo()`, `remquof()`, `remquol()` {#man-remquo number="13.53"}

Compute the remainder and (some of the) quotient.

### Synopsis {#synopsis-101 .unnumbered .unlisted}

::: {#cb359 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double remquo(double x, double y, int *quo);

float remquof(float x, float y, int *quo);

long double remquol(long double x, long double y, int *quo);
```
:::

### Description {#description-101 .unnumbered .unlisted}

This is a funky little thing.

First of all, the return value is the remainder, the same as the [`remainder()`](math.html#man-remainder) function, so check that out.

And the quotient comes back in the `quo` pointer.

Or at least *some of it* does. You'll get at least 3 bits worth of the quotient.

But *why*?

So a couple things.

One is that the quotient of some very large floating point numbers can easily be far too gigantic to fit in even a `long long unsigned int`. So some of it might very well need to be lopped off, anyway.

But at 3 bits? How's that even useful? That only gets you from 0 to 7!

The C99 Rationale document states:

> The `remquo` functions are intended for implementing argument reductions which can exploit a few low-order bits of the quotient. Note that [\\(x\\)]{.math .inline} may be so large in magnitude relative to [\\(y\\)]{.math .inline} that an exact representation of the quotient is not practical.

So... implementing argument reductions... which can exploit a few low-order bits... Ooookay.

[CPPReference has this to say](https://en.cppreference.com/w/c/numeric/math/remquo)[^32^](footnotes.html#fn32){#fnref32 .footnote-ref role="doc-noteref"} on the matter, which is spoken so well, I will quote wholesale:

> This function is useful when implementing periodic functions with the period exactly representable as a floating-point value: when calculating [\\(\\sin(πx)\\)]{.math .inline} for a very large `x`, calling `sin` directly may result in a large error, but if the function argument is first reduced with `remquo`, the low-order bits of the quotient may be used to determine the sign and the octant of the result within the period, while the remainder may be used to calculate the value with high precision.

And there you have it. If you have another example that works for you... congratulations! :)

### Return Value {#return-value-100 .unnumbered .unlisted}

Returns the same as [`remainder`](math.html#man-remainder): The IEC 60559 result of `x`-remainder-`y`.

In addition, at least the lowest 3 bits of the quotient will be stored in `quo` with the same sign as `x/y`.

### Example {#example-101 .unnumbered .unlisted}

There's a [great `cos()` example at CPPReference](https://en.cppreference.com/w/c/numeric/math/remquo)[^33^](footnotes.html#fn33){#fnref33 .footnote-ref role="doc-noteref"} that covers a genuine use case.

But instead of stealing it, I'll just post a simple example here and you can visit their site for a real one.

::: {#cb360 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    int quo;
    double rem;

    rem = remquo(12.75, 2.25, &quo);

    printf("%d remainder %f\n", quo, rem);  // 6 remainder -0.750000
}
```
:::

### See Also {#see-also-97 .unnumbered .unlisted}

[`remainder()`](math.html#man-remainder), [`imaxdiv()`](inttypes.html#man-imaxdiv)

------------------------------------------------------------------------

## [13.54]{.header-section-number} `copysign()`, `copysignf()`, `copysignl()` {#man-copysign number="13.54"}

Copy the sign of one value into another.

### Synopsis {#synopsis-102 .unnumbered .unlisted}

::: {#cb361 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double copysign(double x, double y);

float copysignf(float x, float y);

long double copysignl(long double x, long double y);
```
:::

### Description {#description-102 .unnumbered .unlisted}

These functions return a number that has the magnitude of `x` and the sign of `y`. You can use them to coerce the sign to that of another value.

Neither `x` nor `y` are modified, of course. The return value holds the result.

### Return Value {#return-value-101 .unnumbered .unlisted}

Returns a value with the magnitude of `x` and the sign of `y`.

### Example {#example-102 .unnumbered .unlisted}

::: {#cb362 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    double x = 34.9;
    double y = -999.9;
    double z = 123.4;

    printf("%f\n", copysign(x, y)); // -34.900000
    printf("%f\n", copysign(x, z)); //  34.900000
}
```
:::

### See Also {#see-also-98 .unnumbered .unlisted}

[`signbit()`](math.html#man-signbit)

------------------------------------------------------------------------

## [13.55]{.header-section-number} `nan()`, `nanf()`, `nanl()` {#man-nan number="13.55"}

Return `NAN`.

### Synopsis {#synopsis-103 .unnumbered .unlisted}

::: {#cb363 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double nan(const char *tagp);

float nanf(const char *tagp);

long double nanl(const char *tagp);
```
:::

### Description {#description-103 .unnumbered .unlisted}

These functions return a quiet NaN[^34^](footnotes.html#fn34){#fnref34 .footnote-ref role="doc-noteref"}. It is produced as if calling [`strtod()`](stdlib.html#man-strtod) with `"NAN"` (or a variant thereof) as an argument.

`tagp` points to a string which could be several things, including empty. The contents of the string determine which variant of NaN might get returned depending on the implementation.

Which *version* of NaN? Did you even know it was possible to get this far into the weeds with something that wasn't a number?

Case 1 in which you pass in an empty string, in which case these are the same:

::: {#cb364 .sourceCode}
``` {.sourceCode .c}
nan("");

strtod("NAN()", NULL);
```
:::

Case 2 in which the string contains only digits 0-9, letters a-z, letters A-Z, and/or underscore:

::: {#cb365 .sourceCode}
``` {.sourceCode .c}
nan("goats");

strtod("NAN(goats)", NULL);
```
:::

And Case 3, in which the string contains anything else and is ignored:

::: {#cb366 .sourceCode}
``` {.sourceCode .c}
nan("!");

strtod("NAN", NULL);
```
:::

As for what `strtod()` does with those values in parens, see the \[`strtod()`\] reference page. Spoiler: it's implementation-defined.

### Return Value {#return-value-102 .unnumbered .unlisted}

Returns the requested quiet NaN, or 0 if such things aren't supported by your system.

### Example {#example-103 .unnumbered .unlisted}

::: {#cb367 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", nan(""));       // nan
    printf("%f\n", nan("goats"));  // nan
    printf("%f\n", nan("!"));      // nan
}
```
:::

### See Also {#see-also-99 .unnumbered .unlisted}

[`strtod()`](stdlib.html#man-strtod)

------------------------------------------------------------------------

## [13.56]{.header-section-number} `nextafter()`, `nextafterf()`, `nextafterl()` {#man-nextafter number="13.56"}

Get the next (or previous) representable floating point value.

### Synopsis {#synopsis-104 .unnumbered .unlisted}

::: {#cb368 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double nextafter(double x, double y);

float nextafterf(float x, float y);

long double nextafterl(long double x, long double y);
```
:::

### Description {#description-104 .unnumbered .unlisted}

As you probably know, floating point numbers can't represent *every* possible real number. There are limits.

And, as such, there exists a "next" and "previous" number after or before any floating point number.

These functions return the next (or previous) representable number. That is, no floating point numbers exist between the given number and the next one.

The way it figures it out is it works from `x` in the direction of `y`, answering the question of "what is the next representable number from `x` as we head toward `y`.

### Return Value {#return-value-103 .unnumbered .unlisted}

Returns the next representable floating point value from `x` in the direction of `y`.

If `x` equals `y`, returns `y`. And also `x`, I suppose.

### Example {#example-104 .unnumbered .unlisted}

::: {#cb369 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%.*f\n", DBL_DECIMAL_DIG, nextafter(0.5, 1.0));
    printf("%.*f\n", DBL_DECIMAL_DIG, nextafter(0.349, 0.0));
}
```
:::

Output on my system:

::: {#cb370 .sourceCode}
``` {.sourceCode .default}
0.50000000000000011
0.34899999999999992
```
:::

### See Also {#see-also-100 .unnumbered .unlisted}

[`nexttoward()`](math.html#man-nexttoward)

------------------------------------------------------------------------

## [13.57]{.header-section-number} `nexttoward()`, `nexttowardf()`, `nexttowardl()` {#man-nexttoward number="13.57"}

Get the next (or previous) representable floating point value.

### Synopsis {#synopsis-105 .unnumbered .unlisted}

::: {#cb371 .sourceCode}
``` {.sourceCode .c}
include <math.h>

double nexttoward(double x, long double y);

float nexttowardf(float x, long double y);

long double nexttowardl(long double x, long double y);
```
:::

### Description {#description-105 .unnumbered .unlisted}

These functions are the same as [`nextafter()`](math.html#man-nextafter) except the second parameter is always `long double`.

### Return Value {#return-value-104 .unnumbered .unlisted}

Returns the same as [`nextafter()`](math.html#man-nextafter) except if `x` equals `y`, returns `y` cast to the function's return type.

### Example {#example-105 .unnumbered .unlisted}

::: {#cb372 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <float.h>
#include <math.h>

int main(void)
{
    printf("%.*f\n", DBL_DECIMAL_DIG, nexttoward(0.5, 1.0));
    printf("%.*f\n", DBL_DECIMAL_DIG, nexttoward(0.349, 0.0));
}
```
:::

Output on my system:

::: {#cb373 .sourceCode}
``` {.sourceCode .default}
0.50000000000000011
0.34899999999999992
```
:::

### See Also {#see-also-101 .unnumbered .unlisted}

[`nextafter()`](math.html#man-nextafter)

------------------------------------------------------------------------

## [13.58]{.header-section-number} `fdim()`, `fdimf()`, `fdiml()` {#man-fdim number="13.58"}

Return the positive difference between two numbers clamped at 0.

### Synopsis {#synopsis-106 .unnumbered .unlisted}

::: {#cb374 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double fdim(double x, double y);

float fdimf(float x, float y);

long double fdiml(long double x, long double y);
```
:::

### Description {#description-106 .unnumbered .unlisted}

The positive difference between `x` and `y` is the difference... except if the difference is less than `0`, it's clamped to `0`.

These functions might throw a range error.

### Return Value {#return-value-105 .unnumbered .unlisted}

Returns the difference of `x-y` if the difference is greater than `0`. Otherwise it returns `0`.

### Example {#example-106 .unnumbered .unlisted}

::: {#cb375 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", fdim(10.0, 3.0));   // 7.000000
    printf("%f\n", fdim(3.0, 10.0));   // 0.000000, clamped
}
```
:::

------------------------------------------------------------------------

## [13.59]{.header-section-number} `fmax()`, `fmaxf()`, `fmaxl()`, `fmin()`, `fminf()`, `fminl()` {#man-fmax number="13.59"}

Return the maximum or minimum of two numbers.

### Synopsis {#synopsis-107 .unnumbered .unlisted}

::: {#cb376 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double fmax(double x, double y);

float fmaxf(float x, float y);

long double fmaxl(long double x, long double y);

double fmin(double x, double y);

float fminf(float x, float y);

long double fminl(long double x, long double y);
```
:::

### Description {#description-107 .unnumbered .unlisted}

Straightforwardly, these functions return the minimum or maximum of two given numbers.

If one of the numbers is NaN, the functions return the non-NaN number. If both arguments are NaN, the functions return NaN.

### Return Value {#return-value-106 .unnumbered .unlisted}

Returns the minimum or maximum values, with NaN handled as mentioned above.

### Example {#example-107 .unnumbered .unlisted}

::: {#cb377 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%f\n", fmin(10.0, 3.0));   //  3.000000
    printf("%f\n", fmax(3.0, 10.0));   // 10.000000
}
```
:::

------------------------------------------------------------------------

## [13.60]{.header-section-number} `fma()`, `fmaf()`, `fmal()` {#man-fma number="13.60"}

Floating (AKA "Fast") multiply and add.

### Synopsis {#synopsis-108 .unnumbered .unlisted}

::: {#cb378 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

double fma(double x, double y, double z);

float fmaf(float x, float y, float z);

long double fmal(long double x, long double y, long double z);
```
:::

### Description {#description-108 .unnumbered .unlisted}

This performs the operation [\\((x\\times{y})+z\\)]{.math .inline}, but does so in a nifty way. It does the computation as if it had infinite precision, and then rounds the final result to the final data type according to the current rounding mode.

Contrast to if you'd do the math yourself, where it would have rounded each step of the way, potentially.

Also some architectures have a CPU instruction to do exactly this calculation, so it can do it super quick. (If it doesn't, it's considerably slower.)

You can tell if your CPU supports the fast version by checking that the macro `FP_FAST_FMA` is set to `1`. (The `float` and `long` variants of `fma()` can be tested with `FP_FAST_FMAF` and `FP_FAST_FMAL`, respectively.)

These functions might cause a range error to occur.

### Return Value {#return-value-107 .unnumbered .unlisted}

Returns `(x * y) + z`.

### Example {#example-108 .unnumbered .unlisted}

::: {#cb379 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
printf("%f\n", fma(1.0, 2.0, 3.0));  // 5.000000
```
:::

------------------------------------------------------------------------

## [13.61]{.header-section-number} `isgreater()`, `isgreaterequal()`, `isless()`, `islessequal()` {#man-isgreater number="13.61"}

Floating point comparison macros.

### Synopsis {#synopsis-109 .unnumbered .unlisted}

::: {#cb380 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

int isgreater(any_floating_type x, any_floating_type y);

int isgreaterequal(any_floating_type x, any_floating_type y);

int isless(any_floating_type x, any_floating_type y);

int islessequal(any_floating_type x, any_floating_type y);
```
:::

### Description {#description-109 .unnumbered .unlisted}

These macros compare floating point numbers. Being macros, we can pass in any floating point type.

You might think you can already do that with just regular comparison operators---and you'd be right!

One one exception: the comparison operators raise the "invalid" floating exception if one or more of the operands is NaN. These macros do not.

Note that you must only pass floating point types into these functions. Passing an integer or any other type is undefined behavior.

### Return Value {#return-value-108 .unnumbered .unlisted}

`isgreater()` returns the result of `x > y`.

`isgreaterequal()` returns the result of `x >= y`.

`isless()` returns the result of `x < y`.

`islessequal()` returns the result of `x <= y`.

### Example {#example-109 .unnumbered .unlisted}

::: {#cb381 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%d\n", isgreater(10.0, 3.0));        // 1
    printf("%d\n", isgreaterequal(10.0, 10.0));  // 1
    printf("%d\n", isless(10.0, 3.0));           // 0
    printf("%d\n", islessequal(10.0, 3.0));      // 0
}
```
:::

### See Also {#see-also-102 .unnumbered .unlisted}

[`islessgreater()`](math.html#man-islessgreater), [`isunordered()`](math.html#man-isunordered)

------------------------------------------------------------------------

## [13.62]{.header-section-number} `islessgreater()` {#man-islessgreater number="13.62"}

Test if a floating point number is less than or greater than another.

### Synopsis {#synopsis-110 .unnumbered .unlisted}

::: {#cb382 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

int islessgreater(any_floating_type x, any_floating_type y);
```
:::

### Description {#description-110 .unnumbered .unlisted}

This macro is similar to `isgreater()` and all those, except it made the section name too long if I included it up there. So it gets its own spot.

This returns true if [\\(x \< y\\)]{.math .inline} or [\\(x \> y\\)]{.math .inline}.

Even though it's a macro, we can rest assured that `x` and `y` are only evaluated once.

And even if `x` or `y` are NaN, this will not throw an "invalid" exception, unlike the normal comparison operators.

If you pass in a non-floating type, the behavior is undefined.

### Return Value {#return-value-109 .unnumbered .unlisted}

Returns `(x < y) || (x > y)`.

### Example {#example-110 .unnumbered .unlisted}

::: {#cb383 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%d\n", islessgreater(10.0, 3.0));   // 1
    printf("%d\n", islessgreater(10.0, 30.0));  // 1
    printf("%d\n", islessgreater(10.0, 10.0));  // 0
}
```
:::

### See Also {#see-also-103 .unnumbered .unlisted}

[`isgreater()`](math.html#man-isgreater), [`isgreaterequal()`](math.html#man-isgreater), [`isless()`](math.html#man-isgreater), [`islessequal()`](math.html#man-isgreater), [`isunordered()`](math.html#man-isunordered)

------------------------------------------------------------------------

## [13.63]{.header-section-number} `isunordered()` {#man-isunordered number="13.63"}

Macro returns true if either floating point argument is NaN.

### Synopsis {#synopsis-111 .unnumbered .unlisted}

::: {#cb384 .sourceCode}
``` {.sourceCode .c}
#include <math.h>

int isunordered(any_floating_type x, any_floating_type y);
```
:::

### Description {#description-111 .unnumbered .unlisted}

The spec writes:

> The isunordered macro determines whether its arguments are unordered.

See? Told you C was easy!

It does also elaborate that the arguments are unordered if one or both of them are NaN.

### Return Value {#return-value-110 .unnumbered .unlisted}

This macro returns true if one or both of the arguments are NaN.

### Example {#example-111 .unnumbered .unlisted}

::: {#cb385 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>

int main(void)
{
    printf("%d\n", isunordered(1.0, 2.0));       // 0
    printf("%d\n", isunordered(1.0, sqrt(-1)));  // 1
    printf("%d\n", isunordered(NAN, 30.0));      // 1
    printf("%d\n", isunordered(NAN, NAN));       // 1
}
```
:::

### See Also {#see-also-104 .unnumbered .unlisted}

[`isgreater()`](math.html#man-isgreater), [`isgreaterequal()`](math.html#man-isgreater), [`isless()`](math.html#man-isgreater), [`islessequal()`](math.html#man-isgreater), [`islessgreater()`](math.html#man-islessgreater)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](locale.html) \| [Contents](index.html) \| [Next](setjmp.html)
:::
