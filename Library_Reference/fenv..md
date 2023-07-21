---
tip: translate by openai@2023-07-20 18:10:22
...
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

> -----------------------------------------------------------------------------------------------------------------------
无可奉告
  Function                                               Description

  ------------------------------------------------------ ----------------------------------------------------------------

> ---------------------------------------------------------- ----------------------------------------------------------------
简化中文：
---------------------------------------------------------- ----------------------------------------------------------------

  [`feclearexcept()`](fenv.html#man-feclearexcept)       Clear floating point exceptions

> 清除浮点异常。


  [`fegetexceptflag()`](fenv.html#man-fegetexceptflag)   Save the floating point exception flags

> fegetexceptflag()：保存浮点异常标志


  [`fesetexceptflag()`](fenv.html#man-fegetexceptflag)   Restore the floating point exception flags

> fesetexceptflag()（fenv.html#man-fegetexceptflag）恢复浮点异常标志


  [`feraiseexcept()`](fenv.html#man-feraiseexcept)       Raise a floating point exception through software

> 使用软件提高浮点异常。


  [`fetestexcept()`](fenv.html#man-fetestexcept)         Test to see if an exception has occurred

> 检查是否发生了异常


  [`fegetround()`](fenv.html#man-fegetround)             Get the rounding direction

> 获取舍入方向。


  [`fesetround()`](fenv.html#man-fegetround)             Set the rounding direction

> 设置舍入方向[`fesetround()`](fenv.html#man-fegetround)


  [`fegetenv()`](fenv.html#man-fegetenv)                 Save the entire floating point environment

> fegetenv()：保存整个浮点环境


  [`fesetenv()`](fenv.html#man-fegetenv)                 Restore the entire floating point environment

> fesetenv()（fenv.html#man-fegetenv）恢复整个浮点环境


  [`feholdexcept()`](fenv.html#man-feholdexcept)         Save floating point state and install non-stop mode

> feholdexcept()：保存浮点状态并安装非停止模式


  [`feupdateenv()`](fenv.html#man-feupdateenv)           Restore floating point environment and apply recent exceptions

> feupdateenv()：恢复浮点环境并应用最近的异常

  -----------------------------------------------------------------------------------------------------------------------

> -----------------------------------------------------------------------------------------------------------------------
无可奉告

## [7.1]{.header-section-number} Types and Macros {#types-and-macros number="7.1"}

There are two types defined in this header:

  ----------------------------------------------------------------------
  Type               Description
  ------------------ ---------------------------------------------------
  `fenv_t`           The entire floating point environment

  `fexcept_t`        A set of floating point exceptions
  ----------------------------------------------------------------------


The "environment" can be thought of as the status at this moment of the floating point processing system: this includes the exceptions, rounding, etc. It's an opaque type, so you won't be able to access it directly, and it must be done through the proper functions.

> 浮点处理系统的"环境"可以被认为是此刻的状态：这包括异常、舍入等。它是一种不透明的类型，因此您无法直接访问它，必须通过适当的函数来完成。


If the functions in question exist on your system (they might not be!), then you'll also have these macros defined to represent different exceptions:

> 如果问题中的函数存在于您的系统中（它们可能不存在！），那么您还将定义这些宏来表示不同的异常：

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

> 这个想法是你可以使用位或运算符来表示多个异常，例如：`FE_INVALID|FE_OVERFLOW`。


The functions, below, that have an `excepts` parameter will take these values.

> 以下具有`excepts`参数的函数将接受这些值。


See [`<math.h>`](math.html#math) for which functions raise which exceptions and when.

> 查看[`<math.h>`](math.html#math)，了解哪些函数会抛出哪些异常以及何时抛出。

## [7.2]{.header-section-number} Pragmas {#pragmas number="7.2"}


Normally C is free to optimize all kinds of stuff that might cause the flags to not look like you might expect. So if you're going to use this stuff, be sure to set this pragma:

> 通常C可以自由优化所有可能导致标志看起来不像预期的东西。因此，如果您要使用这些东西，请务必设置此编译指示：

::: {#cb187 .sourceCode}
``` {.sourceCode .c}
#pragma STDC FENV_ACCESS ON
```
:::


If you do this at global scope, it remains in effect until you turn it off:

> 如果你在全局范围内执行此操作，它将一直有效，直到你关闭它。

::: {#cb188 .sourceCode}
``` {.sourceCode .c}
#pragma STDC FENV_ACCESS OFF
```
:::


If you do it in block scope, it has to come before any statements or declarations. In this case, it has effect until the block ends (or until it is explicitly turned off.)

> 如果你在块作用域中进行，它必须在任何语句或声明之前。在这种情况下，它的效果一直持续到块结束（或显式关闭）。


**A caveat**: this program isn't supported on either of the compilers I have (gcc and clang) as of this writing, so though I have built the code, below, it's not particularly well-tested.

> **警告**：截至目前，我拥有的编译器（gcc和clang）都不支持此程序，因此尽管我已经构建了下面的代码，但它并不是特别经过测试的。

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

> [`feraiseexcept()`](fenv.html#man-feraiseexcept)：触发指定的异常
[`fetestexcept()`](fenv.html#man-fetestexcept)：测试指定的异常是否已被触发

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

> 使用这些函数将当前浮点环境保存或恢复到变量中。


Set `excepts` to the set of exceptions you want to save or restore the state of. Setting it to `FE_ALL_EXCEPT` will save or restore the entire state.

> 设置`excepts`为你想要保存或恢复状态的异常集合。将其设置为`FE_ALL_EXCEPT`将保存或恢复整个状态。

Note that `fexcept_t` is an opaque type---you don't know what's in it.

`excepts` can be set to zero for no effect.

### Return Value {#return-value-40 .unnumbered .unlisted}

Returns `0` on success or if `excepts` is zero.

Returns non-zero on failure.

### Example {#example-41 .unnumbered .unlisted}


This program saves the state (before any error has happened), then deliberately causes a domain error by trying to take [\\(\\sqrt{-1}\\)]{.math .inline}.

> 这个程序保存了状态（在任何错误发生之前），然后通过尝试取[\\(\\sqrt{-1}\\)]{.math .inline}来故意引发域错误。


After that, it restores the floating point state to before the error had occurred, thereby clearing it.

> 之后，它将浮点状态恢复到错误发生之前，从而清除它。

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

> 如果抛出`FE_UNDERFLOW`或`FE_OVERFLOW`，C *可能* 也会抛出`FE_INEXACT`。


If either `FE_UNDERFLOW` or `FE_OVERFLOW` is raised at the same time as `FE_INEXACT`, then `FE_UNDERFLOW` or `FE_OVERFLOW` will be raised *before* `FE_INEXACT` behind the scenes.

> 如果同时引发`FE_UNDERFLOW`或`FE_OVERFLOW`和`FE_INEXACT`，那么在幕后`FE_UNDERFLOW`或`FE_OVERFLOW`将先于`FE_INEXACT`被引发。

The order the other exceptions are raised is undefined.

### Return Value {#return-value-41 .unnumbered .unlisted}

Returns `0` if all the exceptions were raised or if `excepts` is `0`.

Returns non-zero otherwise.

### Example {#example-42 .unnumbered .unlisted}


This code deliberately raises a division-by-zero exception and then detects it.

> 这段代码故意引发一个除零异常，然后检测它。

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

> [`feclearexcept()`](fenv.html#man-feclearexcept)：清除浮点异常标志
[`fetestexcept()`](fenv.html#man-fetestexcept)：测试浮点异常标志

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

> 将你想要测试的异常放入`excepts`中，用位或操作将它们组合起来。

### Return Value {#return-value-42 .unnumbered .unlisted}

Returns the bitwise-OR of the exceptions that have been raised.

### Example {#example-43 .unnumbered .unlisted}


This code deliberately raises a division-by-zero exception and then detects it.

> 这段代码故意引发一个除零异常，然后检测它。

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

> [`feclearexcept()`](fenv.html#man-feclearexcept)：清除浮点异常标志
[`feraiseexcept()`](fenv.html#man-feraiseexcept)：设置浮点异常标志

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

> 使用这些来获取或设置许多数学函数使用的舍入方向。


Basically when a function "rounds" a number, it wants to know how to do it. By default, it does it how we tend to expect: if the fractional part is less than 0.5, it rounds down closer to zero, otherwise up farther from zero.

> 基本上，当一个函数“四舍五入”一个数字时，它想知道如何做到这一点。默认情况下，它会按我们的期望进行：如果小数部分小于0.5，它会向零靠近舍去，否则向零远离舍入。

  Macro             Description
  ----------------- ------------------------------------------------
  `FE_TONEAREST`    Round to the nearest whole number, the default
  `FE_TOWARDZERO`   Round toward zero always
  `FE_DOWNWARD`     Round toward the next lesser whole number
  `FE_UPWARD`       Round toward the next greater whole number


Some implementations don't support rounding. If it does, the above macros will be defined.

> 有些实现不支持舍入。如果支持，上面的宏定义将被定义。


Note that the `round()` function is always "to-nearest" and doesn't pay attention to the rounding mode.

> 注意，`round()`函数总是“最接近”的，不关注舍入模式。

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

> [nearbyint()](数学.html#man-nearbyint)，[nearbyintf()](数学.html#man-nearbyint)，[nearbyintl()](数学.html#man-nearbyint)，[rint()](数学.html#man-rint)，[rintf()](数学.html#man-rint)，[rintl()](数学.html#man-rint)，[lrint()](数学.html#man-lrint)，[lrintf()](数学.html#man-lrint)，[lrintl()](数学.html#man-lrint)，[llrint()](数学.html#man-lrint)，[llrintf()](数学.html#man-lrint)，[llrintl()](数学.html#man-lrint)

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

> 你可以通过调用`fegetenv()`来保存环境（例外，舍入方向等），并使用`fesetenv()`来恢复它。


Use this if you want to restore the state after a function call, i.e. hide from the caller that some floating point exceptions or changes occurred.

> 使用这个，如果你想在函数调用后恢复状态，即隐藏浮点异常或变化发生的事实。

### Return Value {#return-value-44 .unnumbered .unlisted}

`fegetenv()` and `fesetenv()` return `0` on success, and non-zero otherwise.

### Example {#example-45 .unnumbered .unlisted}


This example saves the environment, messes with the rounding and exceptions, then restores it. After the environment is restored, we see that the rounding is back to default and the exception is cleared.

> 这个例子保存环境，改变舍入和异常，然后恢复它。恢复环境后，我们发现舍入回到默认状态，异常也被清除了。

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

> [`feholdexcept()`](fenv.html#man-feholdexcept)：保存当前浮点环境并禁用所有异常
[`feupdateenv()`](fenv.html#man-feupdateenv)：恢复之前保存的浮点环境

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

> 这就像`fegetenv()`一样，只是它更新当前环境为*无限*模式，也就是说它不会因任何异常而停止。


It remains in this state until you restore the state with `fesetenv()` or `feupdateenv()`.

> 它一直处于这种状态，直到你使用`fesetenv()`或`feupdateenv()`恢复状态。

### Return Value {#return-value-45 .unnumbered .unlisted}

### Example {#example-46 .unnumbered .unlisted}


This example saves the environment and goes into non-stop mode, messes with the rounding and exceptions, then restores it. After the environment is restored, we see that the rounding is back to default and the exception is cleared. We'll also be out of non-stop mode.

> 这个例子保存了环境，进入了无限循环模式，并对舍入和异常进行了处理，然后恢复了环境。恢复环境后，我们发现舍入已经恢复到默认值，异常也被清除了。我们也退出了无限循环模式。

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

> [`fegetenv()`](fenv.html#man-fegetenv)：获取浮点环境
[`fesetenv()`](fenv.html#man-fegetenv)：设置浮点环境
[`feupdateenv()`](fenv.html#man-feupdateenv)：更新浮点环境

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

> 这类似于`fesetenv()`，但它修改传入的环境，以便在此期间更新发生的异常。


So let's say you had a function that might raise exceptions, but you wanted to hide those in the caller. One option might be to:

> 如果你有一个可能引发异常的函数，但你想在调用者中隐藏这些异常，一个选择可能是：

1.  Save the environment with `fegetenv()` or `feholdexcept()`.
2.  Do whatever you do that might raise exceptions.

3.  Restore the environment with `fesetenv()`, thereby hiding the exceptions that happened in step 2.

> 恢复环境，使用`fesetenv()`，从而隐藏步骤2中发生的异常。


But that hides *all* exceptions. What if you just wanted to hide some of them? You could use `feupdateenv()` like this:

> 但是这会隐藏所有的异常。如果你只想隐藏其中一些呢？你可以像这样使用`feupdateenv()`：

1.  Save the environment with `fegetenv()` or `feholdexcept()`.
2.  Do whatever you do that might raise exceptions.

3.  Call `feclearexcept()` to clear the exceptions you want to hide from the caller.

> 调用`feclearexcept()`清除您想要隐藏的异常信息以便调用者不受影响。

4.  Call `feupdateenv()` to restore the previous environment and update it with the other exceptions that have occurred.

> 调用`feupdateenv()`恢复先前的环境，并更新其他发生的异常。


So it's like a more capable way of restoring the environment than simply `fegetenv()`/`fesetenv()`.

> 这样就比只使用`fegetenv()`/`fesetenv()`更有能力地恢复环境了。

### Return Value {#return-value-46 .unnumbered .unlisted}

Returns `0` on success, non-zero otherwise.

### Example {#example-47 .unnumbered .unlisted}


This program saves state, raises some exceptions, then clears one of the exceptions, then restores and updates the state.

> 这个程序保存状态，引发一些异常，然后清除其中一个异常，然后恢复并更新状态。

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

> 在输出中，起初我们没有异常。然后我们引发了三个异常。然后在我们恢复/更新环境后，我们发现我们清除的（`FE_INVALID`）没有被应用：

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

> [`fegetenv()`](fenv.html#man-fegetenv)：取得浮点环境
[`fesetenv()`](fenv.html#man-fegetenv)：设置浮点环境
[`feholdexcept()`](fenv.html#man-feholdexcept)：保持浮点异常
[`feclearexcept()`](fenv.html#man-feclearexcept)：清除浮点异常

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](errno.html) \| [Contents](index.html) \| [Next](float.html)
:::
