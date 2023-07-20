---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](assert.html) \| [Contents](index.html) \| [Next](ctype.html)
:::

------------------------------------------------------------------------

# [4]{.header-section-number} `<complex.h>` Complex Number Functionality {#complex number="4"}

The complex functions in this reference section come in three flavors each: `double complex`, `float complex`, and `long double complex`.

The `float` variants end with `f` and the `long double` variants end with `l`, e.g. for complex cosine:

::: {#cb64 .sourceCode}
``` {.sourceCode .c}
ccos()   double complex
ccosf()  float complex
ccosl()  long double complex
```
:::

The table below only lists the `double complex` version for brevity.

  -------------------------------------------------------------------------------------------------------
  Function                                Description
  --------------------------------------- ---------------------------------------------------------------
  [`cabs()`](complex.html#man-cabs)       Compute the complex absolute value

  [`cacos()`](complex.html#man-cacos)     Compute the complex arc-cosine

  [`cacosh()`](complex.html#man-cacosh)   Compute the complex arc hyperbolic cosine

  [`carg()`](complex.html#man-carg)       Compute the complex argument

  [`casin()`](complex.html#man-casin)     Compute the complex arc-sine

  [`casinh()`](complex.html#man-casinh)   Compute the complex arc hyperbolic sine

  [`catan()`](complex.html#man-catan)     Compute the complex arc-tangent

  [`catanh()`](complex.html#man-catanh)   Compute the complex arc hyperbolic tangent

  [`ccos()`](complex.html#man-ccos)       Compute the complex cosine

  [`ccosh()`](complex.html#man-ccosh)     Compute the complex hyperbolic cosine

  [`cexp()`](complex.html#man-cexp)       Compute the complex base-[\\(e\\)]{.math .inline} exponential

  [`cimag()`](complex.html#man-cimag)     Returns the imaginary part of a complex number

  [`clog()`](complex.html#man-clog)       Compute the complex logarithm

  [`CMPLX()`](complex.html#man-CMPLX)     Build a complex value from real and imaginary types

  [`conj()`](complex.html#man-conj)       Compute the conjugate of a complex number

  [`cproj()`](complex.html#man-cproj)     Compute the projection of a complex number

  [`creal()`](complex.html#man-creal)     Returns the real part of a complex number

  [`csin()`](complex.html#man-csin)       Compute the complex sine

  [`csinh()`](complex.html#man-csinh)     Compute the complex hyperbolic sine

  [`csqrt()`](complex.html#man-csqrt)     Compute the complex square root

  [`ctan()`](complex.html#man-ctan)       Compute the complex tangent

  [`ctanh()`](complex.html#man-ctanh)     Compute the complex hyperbolic tangent
  -------------------------------------------------------------------------------------------------------

You can test for complex number support by looking at the `__STDC_NO_COMPLEX__` macro. If it's defined, complex numbers aren't available.

There are possibly two types of numbers defined: *complex* and *imaginary*. No system I'm currently aware of implements imaginary types.

The complex types, which are a real value plus a multiple of [\\(i\\)]{.math .inline}, are:

::: {#cb65 .sourceCode}
``` {.sourceCode .c}
float complex
double complex
long double complex
```
:::

The imaginary types, which hold a multiple of [\\(i\\)]{.math .inline}, are:

::: {#cb66 .sourceCode}
``` {.sourceCode .c}
float imaginary
double imaginary
long double imaginary
```
:::

The mathematical value [\\(i=\\sqrt{-1}\\)]{.math .inline} is represented by the symbol `_Complex_I` or `_Imaginary_I`, if it exists.

The The macro `I` will be preferentially set to `_Imaginary_I` (if it exists), or to `_Complex_I` otherwise.

You can write imaginary literals (if supported) using this notation:

::: {#cb67 .sourceCode}
``` {.sourceCode .c}
double imaginary x = 3.4 * I;
```
:::

You can write complex literals using regular complex notation:

::: {#cb68 .sourceCode}
``` {.sourceCode .c}
double complex x = 1.2 + 3.4 * I;
```
:::

or build them with the `CMPLX()` macro:

::: {#cb69 .sourceCode}
``` {.sourceCode .c}
double complex x = CMPLX(1.2, 3.4);  // Like 1.2 + 3.4 * I
```
:::

The latter has the advantage of handing special cases of complex numbers correctly (like those involving infinity or signed zeroes) as if `_Imaginary_I` were present, even if it's not.

All angular values are in radians.

Some functions have discontinuities called *branch cuts*. Now, I'm no mathematician so I can't really talk sensibly about this, but if you're here, I like to think you know what you're doing when it comes to this side of things.

If you system has signed zeroes, you can tell which side of the cut you're on by the sign. And you can't if you don't. The spec elaborates:

> Implementations that do not support a signed zero \[...\] cannot distinguish the sides of branch cuts. These implementations shall map a cut so the function is continuous as the cut is approached coming around the finite endpoint of the cut in a counter clockwise direction. (Branch cuts for the functions specified here have just one finite endpoint.) For example, for the square root function, coming counter clockwise around the finite endpoint of the cut along the negative real axis approaches the cut from above, so the cut maps to the positive imaginary axis.

Finally, there's a pragma called `CX_LIMITED_RANGE` that can be turned on and off (default is off). You can turn it on with:

::: {#cb70 .sourceCode}
``` {.sourceCode .c}
#pragma STDC CX_LIMITED_RANGE ON
```
:::

It allows for certain intermediate operations to underflow, overflow, or deal badly with infinity, presumably for a tradeoff in speed. If you're sure these types of errors won't occur with the numbers you're using AND you're trying to get as much speed out as you can, you could turn this macro on.

The spec also elaborates here:

> The purpose of the pragma is to allow the implementation to use the formulas:
>
> [\\((x+iy)\\times(u+iv) = (xu-yv)+i(yu+xv)\\)]{.math .inline}
>
> [\\((x+iy)/(u+iv) = \[(xu+yv)+i(yu-xv)\]/(u\^2+v\^2)\\)]{.math .inline}
>
> [\\(\|x+iy\|=\\sqrt{x\^2+y\^2}\\)]{.math .inline}
>
> where the programmer can determine they are safe.

------------------------------------------------------------------------

## [4.1]{.header-section-number} `cacos()`, `cacosf()`, `cacosl()` {#man-cacos number="4.1"}

Compute the complex arc-cosine

### Synopsis {#synopsis-2 .unnumbered .unlisted}

::: {#cb71 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex cacos(double complex z);

float complex cacosf(float complex z);

long double complex cacosl(long double complex z);
```
:::

### Description {#description-2 .unnumbered .unlisted}

Computes the complex arc-cosine of a complex number.

The complex number `z` will have an imaginary component in the range [\\(\[0,\\pi\]\\)]{.math .inline}, and the real component is unbounded.

There are branch cuts outside the interval [\\(\[-1,+1\]\\)]{.math .inline} on the real axis.

### Return Value {#return-value-2 .unnumbered .unlisted}

Returns the complex arc-cosine of `z`.

### Example {#example-2 .unnumbered .unlisted}

::: {#cb72 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = cacos(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb73 .sourceCode}
``` {.sourceCode .default}
Result: 0.195321 + -2.788006i
```
:::

### See Also {#see-also-2 .unnumbered .unlisted}

[`ccos()`](complex.html#man-ccos), [`casin()`](complex.html#man-casin), [`catan()`](complex.html#man-catan)

------------------------------------------------------------------------

## [4.2]{.header-section-number} `casin()`, `casinf()`, `casinl()` {#man-casin number="4.2"}

Compute the complex arc-sine

### Synopsis {#synopsis-3 .unnumbered .unlisted}

::: {#cb74 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex casin(double complex z);

float complex casinf(float complex z);

long double complex casinl(long double complex z);
```
:::

### Description {#description-3 .unnumbered .unlisted}

Computes the complex arc-sine of a complex number.

The complex number `z` will have an imaginary component in the range [\\(\[-\\pi/2,+\\pi/2\]\\)]{.math .inline}, and the real component is unbounded.

There are branch cuts outside the interval [\\(\[-1,+1\]\\)]{.math .inline} on the real axis.

### Return Value {#return-value-3 .unnumbered .unlisted}

Returns the complex arc-sine of `z`.

### Example {#example-3 .unnumbered .unlisted}

::: {#cb75 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = casin(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb76 .sourceCode}
``` {.sourceCode .default}
Result: 1.375476 + 2.788006i
```
:::

### See Also {#see-also-3 .unnumbered .unlisted}

[`csin()`](complex.html#man-csin), [`cacos()`](complex.html#man-cacos), [`catan()`](complex.html#man-catan)

------------------------------------------------------------------------

## [4.3]{.header-section-number} `catan()`, `catanf()`, `catanl()` {#man-catan number="4.3"}

Compute the complex arc-tangent

### Synopsis {#synopsis-4 .unnumbered .unlisted}

::: {#cb77 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex catan(double complex z);

float complex catanf(float complex z);

long double complex catanl(long double complex z);
```
:::

### Description {#description-4 .unnumbered .unlisted}

Computes the complex arc-tangent of a complex number.

The complex number `z` will have an real component in the range [\\(\[-\\pi/2,+\\pi/2\]\\)]{.math .inline}, and the imaginary component is unbounded.

There are branch cuts outside the interval [\\(\[-i,+i\]\\)]{.math .inline} on the imaginary axis.

### Return Value {#return-value-4 .unnumbered .unlisted}

Returns the complex arc-tangent of `z`.

### Example {#example-4 .unnumbered .unlisted}

::: {#cb78 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double wheat = 8;
    double sheep = 1.5708;

    double complex x = wheat + sheep * I;

    double complex y = catan(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb79 .sourceCode}
``` {.sourceCode .default}
Result: 1.450947 + 0.023299i
```
:::

### See Also {#see-also-4 .unnumbered .unlisted}

[`ctan()`](complex.html#man-ctan), [`cacos()`](complex.html#man-cacos), [`casin()`](complex.html#man-casin)

------------------------------------------------------------------------

## [4.4]{.header-section-number} `ccos()`, `ccosf()`, `ccosl()` {#man-ccos number="4.4"}

Compute the complex cosine

### Synopsis {#synopsis-5 .unnumbered .unlisted}

::: {#cb80 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex ccos(double complex z);

float complex ccosf(float complex z);

long double complex ccosl(long double complex z);
```
:::

### Description {#description-5 .unnumbered .unlisted}

Computes the complex cosine of a complex number.

### Return Value {#return-value-5 .unnumbered .unlisted}

Returns the complex cosine of `z`.

### Example {#example-5 .unnumbered .unlisted}

::: {#cb81 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = ccos(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb82 .sourceCode}
``` {.sourceCode .default}
Result: -0.365087 + -2.276818i
```
:::

### See Also {#see-also-5 .unnumbered .unlisted}

[`csin()`](complex.html#man-csin), [`ctan()`](complex.html#man-ctan), [`cacos()`](complex.html#man-cacos)

------------------------------------------------------------------------

## [4.5]{.header-section-number} `csin()`, `csinf()`, `csinl()` {#man-csin number="4.5"}

Compute the complex sine

### Synopsis {#synopsis-6 .unnumbered .unlisted}

::: {#cb83 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex csin(double complex z);

float complex csinf(float complex z);

long double complex csinl(long double complex z);
```
:::

### Description {#description-6 .unnumbered .unlisted}

Computes the complex sine of a complex number.

### Return Value {#return-value-6 .unnumbered .unlisted}

Returns the complex sine of `z`.

### Example {#example-6 .unnumbered .unlisted}

::: {#cb84 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = csin(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb85 .sourceCode}
``` {.sourceCode .default}
Result: 2.482485 + -0.334840i
```
:::

### See Also {#see-also-6 .unnumbered .unlisted}

[`ccos()`](complex.html#man-ccos), [`ctan()`](complex.html#man-ctan), [`casin()`](complex.html#man-casin)

------------------------------------------------------------------------

## [4.6]{.header-section-number} `ctan()`, `ctanf()`, `ctanl()` {#man-ctan number="4.6"}

Compute the complex tangent

### Synopsis {#synopsis-7 .unnumbered .unlisted}

::: {#cb86 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex ctan(double complex z);

float complex ctanf(float complex z);

long double complex ctanl(long double complex z);
```
:::

### Description {#description-7 .unnumbered .unlisted}

Computes the complex tangent of a complex number.

### Return Value {#return-value-7 .unnumbered .unlisted}

Returns the complex tangent of `z`.

### Example {#example-7 .unnumbered .unlisted}

::: {#cb87 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = ctan(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb88 .sourceCode}
``` {.sourceCode .default}
Result: -0.027073 + 1.085990i
```
:::

### See Also {#see-also-7 .unnumbered .unlisted}

[`ccos()`](complex.html#man-ccos), [`csin()`](complex.html#man-csin), [`catan()`](complex.html#man-catan)

------------------------------------------------------------------------

## [4.7]{.header-section-number} `cacosh()`, `cacoshf()`, `cacoshl()` {#man-cacosh number="4.7"}

Compute the complex arc hyperbolic cosine

### Synopsis {#synopsis-8 .unnumbered .unlisted}

::: {#cb89 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex cacosh(double complex z);

float complex cacoshf(float complex z);

long double complex cacoshl(long double complex z);
```
:::

### Description {#description-8 .unnumbered .unlisted}

Computes the complex arc hyperbolic cosine of a complex number.

There is a branch cut at values less than [\\(1\\)]{.math .inline} on the real axis.

The return value will be non-negative on the real number axis, and in the range [\\(\[-i\\pi,+i\\pi\]\\)]{.math .inline} on the imaginary axis.

### Return Value {#return-value-8 .unnumbered .unlisted}

Returns the complex arc hyperbolic cosine of `z`.

### Example {#example-8 .unnumbered .unlisted}

::: {#cb90 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = cacosh(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb91 .sourceCode}
``` {.sourceCode .default}
Result: 2.788006 + 0.195321i
```
:::

### See Also {#see-also-8 .unnumbered .unlisted}

[`casinh()`](complex.html#man-casinh), [`catanh()`](complex.html#man-catanh), [`acosh()`](math.html#man-acosh)

------------------------------------------------------------------------

## [4.8]{.header-section-number} `casinh()`, `casinhf()`, `casinhl()` {#man-casinh number="4.8"}

Compute the complex arc hyperbolic sine

### Synopsis {#synopsis-9 .unnumbered .unlisted}

::: {#cb92 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex casinh(double complex z);

float complex casinhf(float complex z);

long double complex casinhl(long double complex z);
```
:::

### Description {#description-9 .unnumbered .unlisted}

Computes the complex arc hyperbolic sine of a complex number.

There are branch cuts outside [\\(\[-i,+i\]\\)]{.math .inline} on the imaginary axis.

The return value will be unbounded on the real number axis, and in the range [\\(\[-i\\pi/2,+i\\pi/2\]\\)]{.math .inline} on the imaginary axis.

### Return Value {#return-value-9 .unnumbered .unlisted}

Returns the complex arc hyperbolic sine of `z`.

### Example {#example-9 .unnumbered .unlisted}

::: {#cb93 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = casinh(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb94 .sourceCode}
``` {.sourceCode .default}
Result: 2.794970 + 0.192476i
```
:::

### See Also {#see-also-9 .unnumbered .unlisted}

[`cacosh()`](complex.html#man-cacosh), [`catanh()`](complex.html#man-catanh), [`asinh()`](math.html#man-asinh)

------------------------------------------------------------------------

## [4.9]{.header-section-number} `catanh()`, `catanhf()`, `catanhl()` {#man-catanh number="4.9"}

Compute the complex arc hyperbolic tangent

### Synopsis {#synopsis-10 .unnumbered .unlisted}

::: {#cb95 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex catanh(double complex z);

float complex catanhf(float complex z);

long double complex catanhl(long double complex z);
```
:::

### Description {#description-10 .unnumbered .unlisted}

Computes the complex arc hyperbolic tangent of a complex number.

There are branch cuts outside [\\(\[-1,+1\]\\)]{.math .inline} on the real axis.

The return value will be unbounded on the real number axis, and in the range [\\(\[-i\\pi/2,+i\\pi/2\]\\)]{.math .inline} on the imaginary axis.

### Return Value {#return-value-10 .unnumbered .unlisted}

Returns the complex arc hyperbolic tangent of `z`.

### Example {#example-10 .unnumbered .unlisted}

::: {#cb96 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = catanh(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb97 .sourceCode}
``` {.sourceCode .default}
Result: 0.120877 + 1.546821i
```
:::

### See Also {#see-also-10 .unnumbered .unlisted}

[`cacosh()`](complex.html#man-cacosh), [`casinh()`](complex.html#man-casinh), [`atanh()`](math.html#man-atanh)

------------------------------------------------------------------------

## [4.10]{.header-section-number} `ccosh()`, `ccoshf()`, `ccoshl()` {#man-ccosh number="4.10"}

Compute the complex hyperbolic cosine

### Synopsis {#synopsis-11 .unnumbered .unlisted}

::: {#cb98 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex ccosh(double complex z);

float complex ccoshf(float complex z);

long double complex ccoshl(long double complex z);
```
:::

### Description {#description-11 .unnumbered .unlisted}

Computes the complex hyperbolic cosine of a complex number.

### Return Value {#return-value-11 .unnumbered .unlisted}

Returns the complex hyperbolic cosine of `z`.

### Example {#example-11 .unnumbered .unlisted}

::: {#cb99 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = ccosh(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb100 .sourceCode}
``` {.sourceCode .default}
Result: -0.005475 + 1490.478826i
```
:::

### See Also {#see-also-11 .unnumbered .unlisted}

[`csinh()`](complex.html#man-csinh), [`ctanh()`](complex.html#man-ctanh), [`ccos()`](complex.html#man-ccos)

------------------------------------------------------------------------

## [4.11]{.header-section-number} `csinh()`, `csinhf()`, `csinhl()` {#man-csinh number="4.11"}

Compute the complex hyperbolic sine

### Synopsis {#synopsis-12 .unnumbered .unlisted}

::: {#cb101 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex csinh(double complex z);

float complex csinhf(float complex z);

long double complex csinhl(long double complex z);
```
:::

### Description {#description-12 .unnumbered .unlisted}

Computes the complex hyperbolic sine of a complex number.

### Return Value {#return-value-12 .unnumbered .unlisted}

Returns the complex hyperbolic sine of `z`.

### Example {#example-12 .unnumbered .unlisted}

::: {#cb102 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = csinh(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb103 .sourceCode}
``` {.sourceCode .default}
Result: -0.005475 + 1490.479161i
```
:::

### See Also {#see-also-12 .unnumbered .unlisted}

[`ccosh()`](complex.html#man-ccosh), [`ctanh()`](complex.html#man-ctanh), [`csin()`](complex.html#man-csin)

------------------------------------------------------------------------

## [4.12]{.header-section-number} `ctanh()`, `ctanhf()`, `ctanhl()` {#man-ctanh number="4.12"}

Compute the complex hyperbolic tangent

### Synopsis {#synopsis-13 .unnumbered .unlisted}

::: {#cb104 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex ctanh(double complex z);

float complex ctanhf(float complex z);

long double complex ctanhl(long double complex z);
```
:::

### Description {#description-13 .unnumbered .unlisted}

Computes the complex hyperbolic tangent of a complex number.

### Return Value {#return-value-13 .unnumbered .unlisted}

Returns the complex hyperbolic tangent of `z`.

### Example {#example-13 .unnumbered .unlisted}

::: {#cb105 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 8 + 1.5708 * I;

    double complex y = ctanh(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb106 .sourceCode}
``` {.sourceCode .default}
Result: 1.000000 + -0.000000i
```
:::

### See Also {#see-also-13 .unnumbered .unlisted}

[`ccosh()`](complex.html#man-ccosh), [`csinh()`](complex.html#man-csinh), [`ctan()`](complex.html#man-ctan)

------------------------------------------------------------------------

## [4.13]{.header-section-number} `cexp()`, `cexpf()`, `cexpl()` {#man-cexp number="4.13"}

Compute the complex base-[\\(e\\)]{.math .inline} exponential

### Synopsis {#synopsis-14 .unnumbered .unlisted}

::: {#cb107 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex cexp(double complex z);

float complex cexpf(float complex z);

long double complex cexpl(long double complex z);
```
:::

### Description {#description-14 .unnumbered .unlisted}

Computes the complex base-[\\(e\\)]{.math .inline} exponential of `z`.

### Return Value {#return-value-14 .unnumbered .unlisted}

Returns the complex base-[\\(e\\)]{.math .inline} exponential of `z`.

### Example {#example-14 .unnumbered .unlisted}

::: {#cb108 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double complex y = cexp(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb109 .sourceCode}
``` {.sourceCode .default}
Result: -1.131204 + 2.471727i
```
:::

### See Also {#see-also-14 .unnumbered .unlisted}

[`cpow()`](complex.html#man-cpow), [`clog()`](complex.html#man-clog), [`exp()`](math.html#man-exp)

------------------------------------------------------------------------

## [4.14]{.header-section-number} `clog()`, `clogf()`, `clogl()` {#man-clog number="4.14"}

Compute the complex logarithm

### Synopsis {#synopsis-15 .unnumbered .unlisted}

::: {#cb110 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex clog(double complex z);

float complex clogf(float complex z);

long double complex clogl(long double complex z);
```
:::

### Description {#description-15 .unnumbered .unlisted}

Compute the base-[\\(e\\)]{.math .inline} complex logarithm of `z`. There is a branch cut on the negative real axis.

The returns value is unbounded on the real axis and in the range [\\(\[-i\\pi,+i\\pi\]\\)]{.math .inline} on the imaginary axis.

### Return Value {#return-value-15 .unnumbered .unlisted}

Returns the base-[\\(e\\)]{.math .inline} complex logarithm of `z`.

### Example {#example-15 .unnumbered .unlisted}

::: {#cb111 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double complex y = clog(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb112 .sourceCode}
``` {.sourceCode .default}
Result: 0.804719 + 1.107149i
```
:::

### See Also {#see-also-15 .unnumbered .unlisted}

[`cexp()`](complex.html#man-cexp), [`log()`](math.html#man-log)

------------------------------------------------------------------------

## [4.15]{.header-section-number} `cabs()`, `cabsf()`, `cabsl()` {#man-cabs number="4.15"}

Compute the complex absolute value

### Synopsis {#synopsis-16 .unnumbered .unlisted}

::: {#cb113 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double cabs(double complex z);

float cabsf(float complex z);

long double cabsl(long double complex z);
```
:::

### Description {#description-16 .unnumbered .unlisted}

Computes the complex absolute value of `z`.

### Return Value {#return-value-16 .unnumbered .unlisted}

Returns the complex absolute value of `z`.

### Example {#example-16 .unnumbered .unlisted}

::: {#cb114 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double complex y = cabs(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb115 .sourceCode}
``` {.sourceCode .default}
Result: 2.236068 + 0.000000i
```
:::

### See Also {#see-also-16 .unnumbered .unlisted}

[`fabs()`](math.html#man-fabs), [`abs()`](stdlib.html#man-abs)

------------------------------------------------------------------------

## [4.16]{.header-section-number} `cpow()`, `cpowf()`, `cpowl()` {#man-cpow number="4.16"}

Compute complex power

### Synopsis {#synopsis-17 .unnumbered .unlisted}

::: {#cb116 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex cpow(double complex x, double complex y);

float complex cpowf(float complex x, float complex y);

long double complex cpowl(long double complex x,
                          long double complex y);
```
:::

### Description {#description-17 .unnumbered .unlisted}

Computes the complex [\\(x\^y\\)]{.math .inline}.

There is a branch cut for `x` along the negative real axis.

### Return Value {#return-value-17 .unnumbered .unlisted}

Returns the complex [\\(x\^y\\)]{.math .inline}.

### Example {#example-17 .unnumbered .unlisted}

::: {#cb117 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;
    double complex y = 3 + 4 * I;

    double r = cpow(x, y);

    printf("Result: %f + %fi\n", creal(r), cimag(r));
}
```
:::

Result:

::: {#cb118 .sourceCode}
``` {.sourceCode .default}
Result: 0.129010 + 0.000000i
```
:::

### See Also {#see-also-17 .unnumbered .unlisted}

[`csqrt()`](complex.html#man-csqrt), [`cexp()`](complex.html#man-cexp)

------------------------------------------------------------------------

## [4.17]{.header-section-number} `csqrt()`, `csqrtf()`, `csqrtl()` {#man-csqrt number="4.17"}

Compute the complex square root

### Synopsis {#synopsis-18 .unnumbered .unlisted}

::: {#cb119 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex csqrt(double complex z);

float complex csqrtf(float complex z);

long double complex csqrtl(long double complex z);
```
:::

### Description {#description-18 .unnumbered .unlisted}

Computes the complex square root of `z`.

There is a branch cut along the negative real axis.

The return value is in the right half of the complex plane and includes the imaginary axis.

### Return Value {#return-value-18 .unnumbered .unlisted}

Returns the complex square root of `z`.

### Example {#example-18 .unnumbered .unlisted}

::: {#cb120 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double complex y = csqrt(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb121 .sourceCode}
``` {.sourceCode .default}
Result: 1.272020 + 0.786151i
```
:::

### See Also {#see-also-18 .unnumbered .unlisted}

[`cpow()`](complex.html#man-cpow), [`sqrt()`](math.html#man-sqrt)

------------------------------------------------------------------------

## [4.18]{.header-section-number} `carg()`, `cargf()`, `cargl()` {#man-carg number="4.18"}

Compute the complex argument

### Synopsis {#synopsis-19 .unnumbered .unlisted}

::: {#cb122 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double carg(double complex z);

float cargf(float complex z);

long double cargl(long double complex z);
```
:::

### Description {#description-19 .unnumbered .unlisted}

Computes the complex argument (AKA phase angle) of `z`.

There is a branch cut along the negative real axis.

Returns a value in the range [\\(\[-\\pi,+\\pi\]\\)]{.math .inline}.

### Return Value {#return-value-19 .unnumbered .unlisted}

Returns the complex argument of `z`.

### Example {#example-19 .unnumbered .unlisted}

::: {#cb123 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double y = carg(x);

    printf("Result: %f\n", y);
}
```
:::

Output:

::: {#cb124 .sourceCode}
``` {.sourceCode .default}
Result: 1.107149
```
:::

------------------------------------------------------------------------

## [4.19]{.header-section-number} `cimag()`, `cimagf()`, `cimagl()` {#man-cimag number="4.19"}

Returns the imaginary part of a complex number

### Synopsis {#synopsis-20 .unnumbered .unlisted}

::: {#cb125 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double cimag(double complex z);

float cimagf(float complex z);

long double cimagl(long double complex z);
```
:::

### Description {#description-20 .unnumbered .unlisted}

Returns the imaginary part of `z`.

As a footnote, the spec points out that any complex number `x` is part of the following equivalency:

::: {#cb126 .sourceCode}
``` {.sourceCode .c}
x == creal(x) + cimag(x) * I;
```
:::

### Return Value {#return-value-20 .unnumbered .unlisted}

Returns the imaginary part of `z`.

### Example {#example-20 .unnumbered .unlisted}

::: {#cb127 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double y = cimag(x);

    printf("Result: %f\n", y);
}
```
:::

Output---just the imaginary part:

::: {#cb128 .sourceCode}
``` {.sourceCode .default}
Result: 2.000000
```
:::

### See Also {#see-also-19 .unnumbered .unlisted}

[`creal()`](complex.html#man-creal)

------------------------------------------------------------------------

## [4.20]{.header-section-number} `CMPLX()`, `CMPLXF()`, `CMPLXL()` {#man-CMPLX number="4.20"}

Build a complex value from real and imaginary types

### Synopsis {#synopsis-21 .unnumbered .unlisted}

::: {#cb129 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex CMPLX(double x, double y);

float complex CMPLXF(float x, float y);

long double complex CMPLXL(long double x, long double y);
```
:::

### Description {#description-21 .unnumbered .unlisted}

These macros build a complex value from real and imaginary types.

Now I know what you're thinking. "But I can already build a complex value from real and imaginary types using the `I` macro, like in the example you're about to give us."

::: {#cb130 .sourceCode}
``` {.sourceCode .c}
double complex x = 1 + 2 * I;
```
:::

And that's true.

But the reality of the matter is weird and complex.

Maybe `I` got undefined, or maybe you redefined it.

Or maybe `I` was defined as `_Complex_I` which doesn't necessarily preserve the sign of a zero value.

As the spec points out, these macros build complex numbers as if `_Imaginary_I` were defined (thus preserving your zero sign) even if it's not. That is, they are defined equivalently to:

::: {#cb131 .sourceCode}
``` {.sourceCode .c}
#define CMPLX(x, y)  ((double complex)((double)(x) + \
                     _Imaginary_I * (double)(y)))

#define CMPLXF(x, y) ((float complex)((float)(x) + \
                     _Imaginary_I * (float)(y)))

#define CMPLXL(x, y) ((long double complex)((long double)(x) + \
                     _Imaginary_I * (long double)(y)))
```
:::

### Return Value {#return-value-21 .unnumbered .unlisted}

Returns the complex number for the given real `x` and imaginary `y` components.

### Example {#example-21 .unnumbered .unlisted}

::: {#cb132 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = CMPLX(1, 2);  // Like 1 + 2 * I

    printf("Result: %f + %fi\n", creal(x), cimag(x));
}
```
:::

Output:

::: {#cb133 .sourceCode}
``` {.sourceCode .default}
Result: 1.000000 + 2.000000i
```
:::

### See Also {#see-also-20 .unnumbered .unlisted}

[`creal()`](complex.html#man-creal), [`cimag()`](complex.html#man-cimag)

------------------------------------------------------------------------

## [4.21]{.header-section-number} `conj()`, `conjf()`, `conjl()` {#man-conj number="4.21"}

Compute the conjugate of a complex number

### Synopsis {#synopsis-22 .unnumbered .unlisted}

::: {#cb134 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex conj(double complex z);

float complex conjf(float complex z);

long double complex conjl(long double complex z);
```
:::

### Description {#description-22 .unnumbered .unlisted}

This function computes the [complex conjugate](https://en.wikipedia.org/wiki/Complex_conjugate)[^13^](footnotes.html#fn13){#fnref13 .footnote-ref role="doc-noteref"} of `z`. Apparently it does this by reversing the sign of the imaginary part, but dammit, I'm a programmer not a mathematician, Jim!

### Return Value {#return-value-22 .unnumbered .unlisted}

Returns the complex conjugate of `z`

### Example {#example-22 .unnumbered .unlisted}

::: {#cb135 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double complex y = conj(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb136 .sourceCode}
``` {.sourceCode .default}
Result: 1.000000 + -2.000000i
```
:::

------------------------------------------------------------------------

## [4.22]{.header-section-number} `cproj()`, `cproj()`, `cproj()` {#man-cproj number="4.22"}

Compute the projection of a complex number

### Synopsis {#synopsis-23 .unnumbered .unlisted}

::: {#cb137 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double complex cproj(double complex z);

float complex cprojf(float complex z);

long double complex cprojl(long double complex z);
```
:::

### Description {#description-23 .unnumbered .unlisted}

Computes the projection of `z` onto a [Riemann sphere](https://en.wikipedia.org/wiki/Riemann_sphere)[^14^](footnotes.html#fn14){#fnref14 .footnote-ref role="doc-noteref"}.

Now we're *really* outside my expertise. The spec has this to say, which I'm quoting verbatim because I'm not knowledgable enough to rewrite it sensibly. Hopefully it makes sense to anyone who would need to use this function.

> `z` projects to `z` except that all complex infinities (even those with one infinite part and one `NaN` part) project to positive infinity on the real axis. If `z` has an infinite part, then `cproj(z)` is equivalent to
>
>     INFINITY + I * copysign(0.0, cimag(z))

So there you have it.

### Return Value {#return-value-23 .unnumbered .unlisted}

Returns the projection of `z` onto a Riemann sphere.

### Example {#example-23 .unnumbered .unlisted}

Fingers crossed this is a remotely sane example...

::: {#cb139 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>
#include <math.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double complex y = cproj(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));

    x = INFINITY + 2 * I;
    y = cproj(x);

    printf("Result: %f + %fi\n", creal(y), cimag(y));
}
```
:::

Output:

::: {#cb140 .sourceCode}
``` {.sourceCode .default}
Result: 1.000000 + 2.000000i
Result: inf + 0.000000i
```
:::

------------------------------------------------------------------------

## [4.23]{.header-section-number} `creal()`, `crealf()`, `creall()` {#man-creal number="4.23"}

Returns the real part of a complex number

### Synopsis {#synopsis-24 .unnumbered .unlisted}

::: {#cb141 .sourceCode}
``` {.sourceCode .c}
#include <complex.h>

double creal(double complex z);

float crealf(float complex z);

long double creall(long double complex z);
```
:::

### Description {#description-24 .unnumbered .unlisted}

Returns the real part of `z`.

As a footnote, the spec points out that any complex number `x` is part of the following equivalency:

::: {#cb142 .sourceCode}
``` {.sourceCode .c}
x == creal(x) + cimag(x) * I;
```
:::

### Return Value {#return-value-24 .unnumbered .unlisted}

Returns the real part of `z`.

### Example {#example-24 .unnumbered .unlisted}

::: {#cb143 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2 * I;

    double y = creal(x);

    printf("Result: %f\n", y);
}
```
:::

Output---just the real part:

::: {#cb144 .sourceCode}
``` {.sourceCode .default}
Result: 1.000000
```
:::

### See Also {#see-also-21 .unnumbered .unlisted}

[`cimag()`](complex.html#man-cimag)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](assert.html) \| [Contents](index.html) \| [Next](ctype.html)
:::
