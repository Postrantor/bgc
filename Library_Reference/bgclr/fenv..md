---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](errno.html) \| [Contents](index.html) \| [Next](float.html)
:::

------------------------------------------------------------------------

# [7]{.header-section-number} `<fenv.h>` Floating Point Exceptions and Environment {#fenv number="7"}

  -----------------------------------------------------------------------------------------------------------------------
  Function                                               Description
  ------------------------------------------------------ ----------------------------------------------------------------
  [`feclearexcept()`](fenv.html#man-feclearexcept)       Clear floating point exceptions

  [`fegetexceptflag()`](fenv.html#man-fegetexceptflag)   Save the floating point exception flags

  [`fesetexceptflag()`](fenv.html#man-fegetexceptflag)   Restore the floating point exception flags

  [`feraiseexcept()`](fenv.html#man-feraiseexcept)       Raise a floating point exception through software

  [`fetestexcept()`](fenv.html#man-fetestexcept)         Test to see if an exception has occurred

  [`fegetround()`](fenv.html#man-fegetround)             Get the rounding direction

  [`fesetround()`](fenv.html#man-fegetround)             Set the rounding direction

  [`fegetenv()`](fenv.html#man-fegetenv)                 Save the entire floating point environment

  [`fesetenv()`](fenv.html#man-fegetenv)                 Restore the entire floating point environment

  [`feholdexcept()`](fenv.html#man-feholdexcept)         Save floating point state and install non-stop mode

  [`feupdateenv()`](fenv.html#man-feupdateenv)           Restore floating point environment and apply recent exceptions
  -----------------------------------------------------------------------------------------------------------------------

## [7.1]{.header-section-number} Types and Macros {#types-and-macros number="7.1"}

There are two types defined in this header:

  ----------------------------------------------------------------------
  Type               Description
  ------------------ ---------------------------------------------------
  `fenv_t`           The entire floating point environment

  `fexcept_t`        A set of floating point exceptions
  ----------------------------------------------------------------------

The "environment" can be thought of as the status at this moment of the floating point processing system: this includes the exceptions, rounding, etc. It's an opaque type, so you won't be able to access it directly, and it must be done through the proper functions.

If the functions in question exist on your system (they might not be!), then you'll also have these macros defined to represent different exceptions:

  ----------------------------------------------------------------------
  Macro              Description
  ------------------ ---------------------------------------------------
  `FE_DIVBYZERO`     Division by zero

  `FE_INEXACT`       Result was not exact, was rounded

  `FE_INVALID`       Domain error

  `FE_OVERFLOW`      Numeric overflow

  `FE_UNDERFLOW`     Numeric underflow

  `FE_ALL_EXCEPT`    All of the above combined
  ----------------------------------------------------------------------

The idea is that you can bitwise-OR these together to represent multiple exceptions, e.g. `FE_INVALID|FE_OVERFLOW`.

The functions, below, that have an `excepts` parameter will take these values.

See [`<math.h>`](math.html#math) for which functions raise which exceptions and when.

## [7.2]{.header-section-number} Pragmas {#pragmas number="7.2"}

Normally C is free to optimize all kinds of stuff that might cause the flags to not look like you might expect. So if you're going to use this stuff, be sure to set this pragma:

::: {#cb187 .sourceCode}
``` {.sourceCode .c}
#pragma STDC FENV_ACCESS ON
```
:::

If you do this at global scope, it remains in effect until you turn it off:

::: {#cb188 .sourceCode}
``` {.sourceCode .c}
#pragma STDC FENV_ACCESS OFF
```
:::

If you do it in block scope, it has to come before any statements or declarations. In this case, it has effect until the block ends (or until it is explicitly turned off.)

**A caveat**: this program isn't supported on either of the compilers I have (gcc and clang) as of this writing, so though I have built the code, below, it's not particularly well-tested.

------------------------------------------------------------------------

## [7.3]{.header-section-number} `feclearexcept()` {#man-feclearexcept number="7.3"}

Clear floating point exceptions

### Synopsis {#synopsis-40 .unnumbered .unlisted}

::: {#cb189 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int feclearexcept(int excepts);
```
:::

### Description {#description-40 .unnumbered .unlisted}

If a floating point exception has occurred, this function can clear it.

Set `excepts` to a bitwise-OR list of exceptions to clear.

Passing `0` has no effect.

### Return Value {#return-value-39 .unnumbered .unlisted}

Returns `0` on success and non-zero on failure.

### Example {#example-40 .unnumbered .unlisted}

::: {#cb190 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    double f = sqrt(-1);

    int r = feclearexcept(FE_INVALID);

    printf("%d %f\n", r, f);
}
```
:::

### See Also {#see-also-37 .unnumbered .unlisted}

[`feraiseexcept()`](fenv.html#man-feraiseexcept), [`fetestexcept()`](fenv.html#man-fetestexcept)

------------------------------------------------------------------------

## [7.4]{.header-section-number} `fegetexceptflag()` `fesetexceptflag()` {#man-fegetexceptflag number="7.4"}

Save or restore the floating point exception flags

### Synopsis {#synopsis-41 .unnumbered .unlisted}

::: {#cb191 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int fegetexceptflag(fexcept_t *flagp, int excepts);

int fesetexceptflag(fexcept_t *flagp, int excepts);
```
:::

### Description {#description-41 .unnumbered .unlisted}

Use these functions to save or restore the current floating point environment in a variable.

Set `excepts` to the set of exceptions you want to save or restore the state of. Setting it to `FE_ALL_EXCEPT` will save or restore the entire state.

Note that `fexcept_t` is an opaque type---you don't know what's in it.

`excepts` can be set to zero for no effect.

### Return Value {#return-value-40 .unnumbered .unlisted}

Returns `0` on success or if `excepts` is zero.

Returns non-zero on failure.

### Example {#example-41 .unnumbered .unlisted}

This program saves the state (before any error has happened), then deliberately causes a domain error by trying to take [\\(\\sqrt{-1}\\)]{.math .inline}.

After that, it restores the floating point state to before the error had occurred, thereby clearing it.

::: {#cb192 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    fexcept_t flag;

    fegetexceptflag(&flag, FE_ALL_EXCEPT);  // Save state

    double f = sqrt(-1);                    // I imagine this won't work
    printf("%f\n", f);                      // "nan"

    if (fetestexcept(FE_INVALID))
        printf("1: Domain error\n");        // This prints!
    else
        printf("1: No domain error\n");

    fesetexceptflag(&flag, FE_ALL_EXCEPT);  // Restore to before error

    if (fetestexcept(FE_INVALID))
        printf("2: Domain error\n");
    else
        printf("2: No domain error\n");     // This prints!
}
```
:::

------------------------------------------------------------------------

## [7.5]{.header-section-number} `feraiseexcept()` {#man-feraiseexcept number="7.5"}

Raise a floating point exception through software

### Synopsis {#synopsis-42 .unnumbered .unlisted}

::: {#cb193 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int feraiseexcept(int excepts);
```
:::

### Description {#description-42 .unnumbered .unlisted}

This attempts to raise a floating point exception as if it had happened.

You can specify multiple exceptions to raise.

If either `FE_UNDERFLOW` or `FE_OVERFLOW` is raised, C *might* also raise `FE_INEXACT`.

If either `FE_UNDERFLOW` or `FE_OVERFLOW` is raised at the same time as `FE_INEXACT`, then `FE_UNDERFLOW` or `FE_OVERFLOW` will be raised *before* `FE_INEXACT` behind the scenes.

The order the other exceptions are raised is undefined.

### Return Value {#return-value-41 .unnumbered .unlisted}

Returns `0` if all the exceptions were raised or if `excepts` is `0`.

Returns non-zero otherwise.

### Example {#example-42 .unnumbered .unlisted}

This code deliberately raises a division-by-zero exception and then detects it.

::: {#cb194 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    feraiseexcept(FE_DIVBYZERO);

    if (fetestexcept(FE_DIVBYZERO) == FE_DIVBYZERO)
        printf("Detected division by zero\n");  // This prints!!
    else
        printf("This is fine.\n");
}
```
:::

### See Also {#see-also-38 .unnumbered .unlisted}

[`feclearexcept()`](fenv.html#man-feclearexcept), [`fetestexcept()`](fenv.html#man-fetestexcept)

------------------------------------------------------------------------

## [7.6]{.header-section-number} `fetestexcept()` {#man-fetestexcept number="7.6"}

Test to see if an exception has occurred

### Synopsis {#synopsis-43 .unnumbered .unlisted}

::: {#cb195 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int fetestexcept(int excepts);
```
:::

### Description {#description-43 .unnumbered .unlisted}

Put the exceptions you want to test in `excepts`, bitwise-ORing them together.

### Return Value {#return-value-42 .unnumbered .unlisted}

Returns the bitwise-OR of the exceptions that have been raised.

### Example {#example-43 .unnumbered .unlisted}

This code deliberately raises a division-by-zero exception and then detects it.

::: {#cb196 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    feraiseexcept(FE_DIVBYZERO);

    if (fetestexcept(FE_DIVBYZERO) == FE_DIVBYZERO)
        printf("Detected division by zero\n");  // This prints!!
    else
        printf("This is fine.\n");
}
```
:::

### See Also {#see-also-39 .unnumbered .unlisted}

[`feclearexcept()`](fenv.html#man-feclearexcept), [`feraiseexcept()`](fenv.html#man-feraiseexcept)

------------------------------------------------------------------------

## [7.7]{.header-section-number} `fegetround()` `fesetround()` {#man-fegetround number="7.7"}

Get or set the rounding direction

### Synopsis {#synopsis-44 .unnumbered .unlisted}

::: {#cb197 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int fegetround(void);

int fesetround(int round);
```
:::

### Description {#description-44 .unnumbered .unlisted}

Use these to get or set the rounding direction used by a variety of math functions.

Basically when a function "rounds" a number, it wants to know how to do it. By default, it does it how we tend to expect: if the fractional part is less than 0.5, it rounds down closer to zero, otherwise up farther from zero.

  Macro             Description
  ----------------- ------------------------------------------------
  `FE_TONEAREST`    Round to the nearest whole number, the default
  `FE_TOWARDZERO`   Round toward zero always
  `FE_DOWNWARD`     Round toward the next lesser whole number
  `FE_UPWARD`       Round toward the next greater whole number

Some implementations don't support rounding. If it does, the above macros will be defined.

Note that the `round()` function is always "to-nearest" and doesn't pay attention to the rounding mode.

### Return Value {#return-value-43 .unnumbered .unlisted}

`fegetround()` returns the current rounding direction, or a negative value on error.

`fesetround()` returns zero on success, or non-zero on failure.

### Example {#example-44 .unnumbered .unlisted}

This rounds some numbers

::: {#cb198 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

// Helper function to print the rounding mode
const char *rounding_mode_str(int mode)
{
    switch (mode) {
        case FE_TONEAREST:  return "FE_TONEAREST";
        case FE_TOWARDZERO: return "FE_TOWARDZERO";
        case FE_DOWNWARD:   return "FE_DOWNWARD";
        case FE_UPWARD:     return "FE_UPWARD";
    }

    return "Unknown";
}

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    int rm;

    rm = fegetround();

    printf("%s\n", rounding_mode_str(rm));    // Print current mode
    printf("%f %f\n", rint(2.1), rint(2.7));  // Try rounding

    fesetround(FE_TOWARDZERO);                // Set the mode

    rm = fegetround();

    printf("%s\n", rounding_mode_str(rm));    // Print it
    printf("%f %f\n", rint(2.1), rint(2.7));  // Try it now!
}
```
:::

Output:

::: {#cb199 .sourceCode}
``` {.sourceCode .default}
FE_TONEAREST
2.000000 3.000000
FE_TOWARDZERO
2.000000 2.000000
```
:::

### See Also {#see-also-40 .unnumbered .unlisted}

[`nearbyint()`](math.html#man-nearbyint), [`nearbyintf()`](math.html#man-nearbyint), [`nearbyintl()`](math.html#man-nearbyint), [`rint()`](math.html#man-rint), [`rintf()`](math.html#man-rint), [`rintl()`](math.html#man-rint), [`lrint()`](math.html#man-lrint), [`lrintf()`](math.html#man-lrint), [`lrintl()`](math.html#man-lrint), [`llrint()`](math.html#man-lrint), [`llrintf()`](math.html#man-lrint), [`llrintl()`](math.html#man-lrint)

------------------------------------------------------------------------

## [7.8]{.header-section-number} `fegetenv()` `fesetenv()` {#man-fegetenv number="7.8"}

Save or restore the entire floating point environment

### Synopsis {#synopsis-45 .unnumbered .unlisted}

::: {#cb200 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int fegetenv(fenv_t *envp);
int fesetenv(const fenv_t *envp);
```
:::

### Description {#description-45 .unnumbered .unlisted}

You can save the environment (exceptions, rounding direction, etc.) by calling `fegetenv()` and restore it with `fesetenv()`.

Use this if you want to restore the state after a function call, i.e. hide from the caller that some floating point exceptions or changes occurred.

### Return Value {#return-value-44 .unnumbered .unlisted}

`fegetenv()` and `fesetenv()` return `0` on success, and non-zero otherwise.

### Example {#example-45 .unnumbered .unlisted}

This example saves the environment, messes with the rounding and exceptions, then restores it. After the environment is restored, we see that the rounding is back to default and the exception is cleared.

::: {#cb201 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

void show_status(void)
{
    printf("Rounding is FE_TOWARDZERO: %d\n",
           fegetround() == FE_TOWARDZERO);

    printf("FE_DIVBYZERO is set: %d\n",
           fetestexcept(FE_DIVBYZERO) != 0);
}

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    fenv_t env;

    fegetenv(&env);  // Save the environment

    fesetround(FE_TOWARDZERO);    // Change rounding
    feraiseexcept(FE_DIVBYZERO);  // Raise an exception

    show_status();

    fesetenv(&env);  // Restore the environment

    show_status();
}
```
:::

Output:

::: {#cb202 .sourceCode}
``` {.sourceCode .default}
Rounding is FE_TOWARDZERO: 1
FE_DIVBYZERO is set: 1
Rounding is FE_TOWARDZERO: 0
FE_DIVBYZERO is set: 0
```
:::

### See Also {#see-also-41 .unnumbered .unlisted}

[`feholdexcept()`](fenv.html#man-feholdexcept), [`feupdateenv()`](fenv.html#man-feupdateenv)

------------------------------------------------------------------------

## [7.9]{.header-section-number} `feholdexcept()` {#man-feholdexcept number="7.9"}

Save floating point state and install non-stop mode

### Synopsis {#synopsis-46 .unnumbered .unlisted}

::: {#cb203 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int feholdexcept(fenv_t *envp);
```
:::

### Description {#description-46 .unnumbered .unlisted}

This is just like `fegetenv()` except that it updates the current environment to be in *non-stop* mode, namely it won't halt on any exceptions.

It remains in this state until you restore the state with `fesetenv()` or `feupdateenv()`.

### Return Value {#return-value-45 .unnumbered .unlisted}

### Example {#example-46 .unnumbered .unlisted}

This example saves the environment and goes into non-stop mode, messes with the rounding and exceptions, then restores it. After the environment is restored, we see that the rounding is back to default and the exception is cleared. We'll also be out of non-stop mode.

::: {#cb204 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

void show_status(void)
{
    printf("Rounding is FE_TOWARDZERO: %d\n",
           fegetround() == FE_TOWARDZERO);

    printf("FE_DIVBYZERO is set: %d\n",
           fetestexcept(FE_DIVBYZERO) != 0);
}

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    fenv_t env;

    // Save the environment and don't stop on exceptions
    feholdexcept(&env);

    fesetround(FE_TOWARDZERO);    // Change rounding
    feraiseexcept(FE_DIVBYZERO);  // Raise an exception

    show_status();

    fesetenv(&env);  // Restore the environment

    show_status();
}
```
:::

### See Also {#see-also-42 .unnumbered .unlisted}

[`fegetenv()`](fenv.html#man-fegetenv), [`fesetenv()`](fenv.html#man-fegetenv), [`feupdateenv()`](fenv.html#man-feupdateenv)

------------------------------------------------------------------------

## [7.10]{.header-section-number} `feupdateenv()` {#man-feupdateenv number="7.10"}

Restore floating point environment and apply recent exceptions

### Synopsis {#synopsis-47 .unnumbered .unlisted}

::: {#cb205 .sourceCode}
``` {.sourceCode .c}
#include <fenv.h>

int feupdateenv(const fenv_t *envp);
```
:::

### Description {#description-47 .unnumbered .unlisted}

This is like `fesetenv()` except that it modifies the passed-in environment so that it is updated with exceptions that have happened in the meantime.

So let's say you had a function that might raise exceptions, but you wanted to hide those in the caller. One option might be to:

1.  Save the environment with `fegetenv()` or `feholdexcept()`.
2.  Do whatever you do that might raise exceptions.
3.  Restore the environment with `fesetenv()`, thereby hiding the exceptions that happened in step 2.

But that hides *all* exceptions. What if you just wanted to hide some of them? You could use `feupdateenv()` like this:

1.  Save the environment with `fegetenv()` or `feholdexcept()`.
2.  Do whatever you do that might raise exceptions.
3.  Call `feclearexcept()` to clear the exceptions you want to hide from the caller.
4.  Call `feupdateenv()` to restore the previous environment and update it with the other exceptions that have occurred.

So it's like a more capable way of restoring the environment than simply `fegetenv()`/`fesetenv()`.

### Return Value {#return-value-46 .unnumbered .unlisted}

Returns `0` on success, non-zero otherwise.

### Example {#example-47 .unnumbered .unlisted}

This program saves state, raises some exceptions, then clears one of the exceptions, then restores and updates the state.

::: {#cb206 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <fenv.h>

void show_status(void)
{
    printf("FE_DIVBYZERO: %d\n", fetestexcept(FE_DIVBYZERO) != 0);
    printf("FE_INVALID  : %d\n", fetestexcept(FE_INVALID) != 0);
    printf("FE_OVERFLOW : %d\n\n", fetestexcept(FE_OVERFLOW) != 0);
}

int main(void)
{
    #pragma STDC FENV_ACCESS ON 

    fenv_t env;

    feholdexcept(&env);  // Save the environment

    // Pretend some bad math happened here:
    feraiseexcept(FE_DIVBYZERO);  // Raise an exception
    feraiseexcept(FE_INVALID);    // Raise an exception
    feraiseexcept(FE_OVERFLOW);   // Raise an exception

    show_status();

    feclearexcept(FE_INVALID);

    feupdateenv(&env);  // Restore the environment

    show_status();
}
```
:::

In the output, at first we have no exceptions. Then we have the three we raised. Then after we restore/update the environment, we see the one we cleared (`FE_INVALID`) hasn't been applied:

::: {#cb207 .sourceCode}
``` {.sourceCode .default}
FE_DIVBYZERO: 0
FE_INVALID  : 0
FE_OVERFLOW : 0

FE_DIVBYZERO: 1
FE_INVALID  : 1
FE_OVERFLOW : 1

FE_DIVBYZERO: 1
FE_INVALID  : 0
FE_OVERFLOW : 1
```
:::

### See Also {#see-also-43 .unnumbered .unlisted}

[`fegetenv()`](fenv.html#man-fegetenv), [`fesetenv()`](fenv.html#man-fegetenv), [`feholdexcept()`](fenv.html#man-feholdexcept), [`feclearexcept()`](fenv.html#man-feclearexcept)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](errno.html) \| [Contents](index.html) \| [Next](float.html)
:::
