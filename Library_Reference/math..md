---
tip: translate by openai@2023-07-20 18:38:17
...
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

> 许多以下函数有`float`和`long double`变体，如[下文](math.html#func-idioms)所述（例如`pow()`，`powf()`，`powl()`）。为了避免让你的眼睛融化，以下表格中省略了`float`和`long double`变体。


  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
给我一点帮助吧！

  Function                                                                  Description

> 功能                                                                   描述

  ------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------
简体中文：------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------

  [`acos()`](math.html#man-acos)                                            Calculate the arc cosine of a number.

> 计算一个数字的反余弦值。


  [`acosh()`](math.html#man-acosh)                                          Compute arc hyperbolic cosine.

> 计算反双曲余弦。


  [`asin()`](math.html#man-asin)                                            Calculate the arc sine of a number.

> 计算一个数字的反正弦。


  [`asinh()`](math.html#man-asinh)                                          Compute arc hyperbolic sine.

> 计算反双曲正弦。


  [`atan()`](math.html#man-atan), [`atan2()`](math.html#man-atan)           Calculate the arc tangent of a number.

> 计算一个数字的反正切值。


  [`atanh()`](math.html#man-atanh)                                          Compute the arc hyperbolic tangent.

> 计算反双曲正切。


  [`cbrt()`](math.html#man-cbrt)                                            Compute the cube root.

> 计算立方根。


  [`ceil()`](math.html#man-ceil)                                            Ceiling---return the next whole number not smaller than the given number.

> ceil()---返回大于给定数字的下一个整数。


  [`copysign()`](math.html#man-copysign)                                    Copy the sign of one value into another.

> 复制一个值的符号到另一个值中。


  [`cos()`](math.html#man-cos)                                              Calculate the cosine of a number.

> 计算一个数字的余弦值。


  [`cosh()`](math.html#man-cosh)                                            Compute the hyperbolic cosine.

> 计算双曲余弦。


  [`erf()`](math.html#man-erf)                                              Compute the error function of the given value.

> 计算给定值的误差函数。


  [`erfc()`](math.html#man-erfc)                                            Compute the complementary error function of a value.

> 计算值的互补误差函数。


  [`exp()`](math.html#man-exp)                                              Compute [\\(e\\)]{.math .inline} raised to a power.

> 计算[\(e\)]{.math .inline}的幂。


  [`exp2()`](math.html#man-exp2)                                            Compute 2 to a power.

> 计算2的幂。


  [`expm1()`](math.html#man-expm1)                                          Compute [\\(e\^x-1\\)]{.math .inline}.

> 计算[\\(e\^x-1\\)]{.math .inline}。


  [`fabs()`](math.html#man-fabs)                                            Compute the absolute value.

> 计算绝对值。


  [`fdim()`](math.html#man-fdim)                                            Return the positive difference between two numbers clamped at 0.

> 返回两个数字在0处被钳住的正差值。


  [`floor()`](math.html#man-floor)                                          Compute the largest whole number not larger than the given value.

> 计算给定值以下的最大整数。


  [`fma()`](math.html#man-fma)                                              Floating (AKA "Fast") multiply and add.

> [`fma()`](math.html#man-fma)：浮点（也称为“快速”）乘法和加法。


  [`fmax()`](math.html#man-fmax), [`fmin()`](math.html#man-fmax)            Return the maximum or minimum of two numbers.

> [`fmax()`](math.html#man-fmax)，[`fmin()`](math.html#man-fmax) 返回两个数字的最大值或最小值。


  [`fmod()`](math.html#man-fmod)                                            Compute the floating point remainder.

> 计算浮点余数。


  [`fpclassify()`](math.html#man-fpclassify)                                Return the classification of a given floating point number.

> 返回给定浮点数的分类。


  [`frexp()`](math.html#man-frexp)                                          Break a number into its fraction part and exponent (as a power of 2).

> `frexp()`函数将一个数字分解为它的小数部分和指数（以2的幂形式）。


  [`hypot()`](math.html#man-hypot)                                          Compute the length of the hypotenuse of a triangle.

> 计算三角形斜边的长度。


  [`ilogb()`](math.html#man-ilogb)                                          Return the exponent of a floating point number.

> 返回浮点数的指数。


  [`isfinite()`](math.html#man-isnan)                                       True if the number is not infinite or NaN.

> 如果数字不是无穷大或非数字，则为真。


  [`isgreater()`](math.html#man-isgreater)                                  True if one argument is greater than another.

> `isgreater()`：如果一个参数大于另一个参数，则返回True。


  [`isgreatereequal()`](math.html#man-isgreater)                            True if one argument is greater than or equal to another.

> `isgreatereequal()`函数用于比较两个参数，如果一个参数大于或等于另一个参数，则返回真。


  [`isinf()`](math.html#man-isnan)                                          True if the number is infinite.

> `isinf()`函数会返回True，如果数字是无穷大的。


  [`isless()`](math.html#man-isgreater)                                     True if one argument is less than another.

> `isless()`：如果一个参数小于另一个参数，则为真。


  [`islesseequal()`](math.html#man-isgreater)                               True if one argument is less than or equal to another.

> 如果一个参数小于或等于另一个参数，则为真。


  [`islessgreater()`](math.html#man-islessgreater)                          Test if a floating point number is less than or greater than another.

> [`islessgreater()`](math.html#man-islessgreater) 函数测试一个浮点数是否小于或大于另一个数。


  [`isnan()`](math.html#man-isnan)                                          True if the number is Not-a-Number.

> `isnan()`函数会返回True，如果数字不是一个数字。


  [`isnormal()`](math.html#man-isnan)                                       True if the number is normal.

> 如果数字是正常的，则为真。


  [`isunordered()`](math.html#man-isunordered)                              Macro returns true if either floating point argument is NaN.

> `isunordered()`宏如果任一浮点参数是NaN，则返回true。


  [`ldexp()`](math.html#man-ldexp)                                          Multiply a number by an integral power of 2.

> `ldexp()`函数用于将一个数乘以2的整数次幂。


  [`lgamma()`](math.html#man-lgamma)                                        Compute the natural logarithm of the absolute value of [\\(\\Gamma(x)\\)]{.math .inline}.

> 计算[\(\Gamma(x)\)]{.math .inline}的绝对值的自然对数。


  [`log()`](math.html#man-log)                                              Compute the natural logarithm.

> 计算自然对数。


  [`log10()`](math.html#man-log10)                                          Compute the log-base-10 of a number.

> 计算一个数的以10为底的对数。


  [`log2()`](math.html#man-log2)                                            Compute the base-2 logarithm of a number.

> 计算一个数字的以2为底的对数。


  [`logb()`](math.html#man-logb)                                            Extract the exponent of a number given `FLT_RADIX`.

> 提取给定`FLT_RADIX`的数字的指数。


  [`log1p()`](math.html#man-log1p)                                          Compute the natural logarithm of a number plus 1.

> 计算一个数字加1的自然对数。


  [`lrint()`](math.html#man-lrint)                                          Returns `x` rounded in the current rounding direction as an integer.

> lrint()函数返回按当前舍入方向舍入后的整数x。


  [`lround()`](math.html#man-lround), [`llround()`](math.html#man-lround)   Round a number in the good old-fashioned way, returning an integer.

> [`lround()`](math.html#man-lround)，[`llround()`](math.html#man-lround)，以传统的方式对数字进行舍入，返回整数。


  [`modf()`](math.html#man-modf)                                            Extract the integral and fractional parts of a number.

> 提取数字的整数部分和小数部分。


  [`nan()`](math.html#man-nan)                                              Return `NAN`.

> 返回NAN。


  [`nearbyint()`](math.html#man-nearbyint)                                  Rounds a value in the current rounding direction.

> nearbyint() 将值按当前舍入方向进行四舍五入。


  [`nextafter()`](math.html#man-nextafter)                                  Get the next (or previous) representable floating point value.

> 获取下一个（或上一个）可表示的浮点值。


  [`nexttoward()`](math.html#man-nexttoward)                                Get the next (or previous) representable floating point value.

> 获取下一个（或上一个）可表示的浮点值。


  [`pow()`](math.html#man-pow)                                              Compute a value raised to a power.

> 计算一个值的幂。


  [`remainder()`](math.html#man-remainder)                                  Compute the remainder IEC 60559-style.

> 计算IEC 60559样式的余数。


  [`remquo()`](math.html#man-remquo)                                        Compute the remainder and (some of the) quotient.

> 计算余数和（部分）商。


  [`rint()`](math.html#man-rint)                                            Rounds a value in the current rounding direction.

> 对当前舍入方向的值进行舍入。


  [`round()`](math.html#man-round)                                          Round a number in the good old-fashioned way.

> 使用传统的方式将数字四舍五入。


  [`scalbn()`](math.html#man-scalb), [`scalbln()`](math.html#man-scalb)     Efficiently compute [\\(x\\times r\^n\\)]{.math .inline}, where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

> [`scalbn()`](math.html#man-scalb)和[`scalbln()`](math.html#man-scalb)可有效地计算[\\(x\\times r\^n\\)]{.math .inline}，其中[\\(r\\)]{.math .inline}为`FLT_RADIX`。


  [`signbit()`](math.html#man-signbit)                                      Return the sign of a number.

> 返回数字的符号。


  [`sin()`](math.html#man-sin)                                              Calculate the sine of a number.

> 计算一个数字的正弦值。


  [`sqrt()`](math.html#man-sqrt)                                            Calculate the square root of a number.

> 计算一个数的平方根。


  [`tan()`](math.html#man-tan)                                              Calculate the tangent of a number.

> 计算一个数字的正切值。


  [`tanh()`](math.html#man-tanh)                                            Compute the hyperbolic tangent.

> 计算双曲正切。


  [`tgamma()`](math.html#man-tgamma)                                        Compute the gamma function, [\\(\\Gamma(x)\\)]{.math .inline}.

> 计算伽马函数[\(\Gamma(x)\)]{.math .inline}。


  [`trunc()`](math.html#man-trunc)                                          Truncate the fractional part off a floating point value.

> 截断浮点值的小数部分。

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
简体中文：


It's your favorite subject: Mathematics! Hello, I'm Doctor Math, and I'll be making math FUN and EASY!

> 哦，你最喜欢的科目：数学！你好，我是数学博士，我会让数学变得有趣而又容易！

*\[vomiting sounds\]*


Ok, I know math isn't the grandest thing for some of you out there, but these are merely functions that quickly and easily do math you either know, want, or just don't care about. That pretty much covers it.

> 好的，我知道数学对你们中的一些人来说不是最伟大的事情，但这些只是快速轻松地完成你所知道、想要或者不在乎的数学运算的函数。几乎就是这样了。

## [13.1]{.header-section-number} Math Function Idioms {#func-idioms number="13.1"}


Many of these math functions exist in three forms, each corresponding to the argument and/or return types the function uses, `float`, `double`, or `long double`.

> 许多这些数学函数以三种形式存在，每种形式对应于函数使用的参数和/或返回类型`float`、`double`或`long double`。


The alternate form for `float` is made by appending `f` to the end of the function name.

> 浮点数的另一种形式是在函数名称后面加上`f`。


The alternate form for `long double` is made by appending `l` to the end of the function name.

> 长双精度的替代形式是在函数名称末尾添加`l`。


For example, the `pow()` function, which computes [\\(x\^y\\)]{.math .inline}, exists in these forms:

> 例如，计算[\(x\^y\)]{.math .inline}的`pow()`函数有以下形式：

::: {#cb240 .sourceCode}
``` {.sourceCode .c}
double      pow(double x, double y);             // double
float       powf(float x, float y);              // float
long double powl(long double x, long double y);  // long double
```
:::


Remember that parameters are given values as if you assigned into them. So if you pass a `double` to `powf()`, it'll choose the closest `float` it can to hold the double. If the `double` doesn't fit, undefined behavior happens.

> 记住，参数是给定的值，就像你赋予它们一样。因此，如果你将一个`double`传递给`powf（）`，它会选择最接近的`float`来保存`double`。如果`double`不适合，就会发生未定义的行为。

## [13.2]{.header-section-number} Math Types {#math-types number="13.2"}

We have two exciting new types in `<math.h>`:

-   `float_t`
-   `double_t`


The `float_t` type is at least as accurate as a `float`, and the `double_t` type is at least as accurate as a `double`.

> `float_t`类型至少和`float`一样精确，而`double_t`类型至少和`double`一样精确。


The idea with these types is they can represent the most efficient way of storing numbers for maximum speed.

> 这些类型的想法是它们可以表示存储数字的最有效方式，以获得最大的速度。


Their actual types vary by implementation, but can be determined by the value of the `FLT_EVAL_METHOD` macro.

> 他们的实际类型因实现而异，但可以通过`FLT_EVAL_METHOD`宏的值来确定。

  `FLT_EVAL_METHOD`   `float_t` type           `double_t` type
  ------------------- ------------------------ ------------------------
  `0`                 `float`                  `double`
  `1`                 `double`                 `double`
  `2`                 `long double`            `long double`
  Other               Implementation-defined   Implementation-defined


For all defined values of `FLT_EVAL_METHOD`, `float_t` is the least-precise type used for all floating calculations.

> 对于所有定义的FLT_EVAL_METHOD值，float_t是用于所有浮点计算的最不精确的类型。

## [13.3]{.header-section-number} Math Macros {#math-macros number="13.3"}


There are actually a number of these defined, but we'll cover most of them in their relevant reference sections, below.

> 实际上定义了许多这样的内容，但我们将在下面的相关参考部分中涵盖其中的大部分。

But here are a couple:

`NAN` represents Not-A-Number.


Defined in `<float.h>` is `FLT_RADIX`: the number base used by floating point numbers. This is commonly `2`, but could be anything.

> 在<float.h>中定义的FLT_RADIX是浮点数使用的数字基数。通常是2，但也可以是其他数字。

## [13.4]{.header-section-number} Math Errors {#math-errors number="13.4"}

As we know, nothing can ever go wrong with math... except *everything*!


So there are just a couple errors that might occur when using some of these functions.

> 这样，当使用其中一些功能时，可能会发生几个错误。

-   **Range errors** mean that some result is beyond what can be stored in the result type.


-   **Domain errors** mean that you've passed in an argument that doesn't have a defined result for this function.

> **域错误**意味着您传入的参数对于此函数没有定义的结果。


-   **Pole errors** mean that the limit of the function as [\\(x\\)]{.math .inline} approaches the given argument is infinite.

> 错误极限意味着，当x接近给定参数时，函数的极限是无穷大的。


-   **Overflow errors** are when the result is really large, but can't be stored without incurring large roundoff error.

> 溢出错误是指当结果非常大，但是如果不进行大的舍入误差就无法存储的时候发生的错误。

-   **Underflow errors** are like overflow errors, except with very small numbers.

Now, the C math library can do a couple things when these errors occur:

-   Set `errno` to some value, or...
-   Raise a floating point exception.


Your system might vary on what happens. You can check it by looking at the value of the variable `math_errhandling`. It will be equivalent to one of the following[^22^](footnotes.html#fn22){#fnref22 .footnote-ref role="doc-noteref"}:

> 你的系统可能会有不同的发生情况。你可以通过查看变量`math_errhandling`的值来检查它。它将等同于以下之一[^22^](footnotes.html#fn22){#fnref22 .footnote-ref role="doc-noteref"}：

  ----------------------------------------------------------------------------------
  `math_errhandling`                  Description
  ----------------------------------- ----------------------------------------------

  `MATH_ERRNO`                        The system uses `errno` for math errors.

> 系统使用`errno`来处理数学错误。


  `MATH_ERREXCEPT`                    The system uses exceptions for math errors.

> 系统使用异常来处理数学错误。


  `MATH_ERRNO | MATH_ERREXCEPT`       The system does both! (That's a bitwise-OR!)

> 系统同时执行两者！（这是一个位或运算！）
  ----------------------------------------------------------------------------------

You are not allowed to change `math_errhandling`.


For a fuller description on how exceptions work and their meanings, see the [`<fenv.h>`](fenv.html#fenv) section.

> 对于关于异常如何工作及其含义的更详细描述，请参阅[`<fenv.h>`](fenv.html#fenv)部分。

## [13.5]{.header-section-number} Math Pragmas {#math-pragmas number="13.5"}


In a nutshell, pragmas offer various ways to control the compiler's behavior. In this case, we're talking about controlling how C's math library works.

> 总之，宏指令提供了多种控制编译器行为的方式。在这种情况下，我们谈论的是如何控制C语言的数学库的工作方式。


In specific, we have a pragma `FP_CONTRACT` that can be turned off and on.

> 具体来说，我们有一个可以打开和关闭的宏`FP_CONTRACT`。

What does it mean?


First of all, keep in mind that any operation in an expression can cause rounding error. So each step of the expression can introduce more rounding error.

> 首先，要记住任何表达式中的操作都可能导致舍入误差。因此，表达式的每一步都可能引入更多的舍入误差。


But what if the compiler knows a *double secret* way of taking the expression you wrote and converting it to a single instruction that reduced the number of steps such that the intermediate rounding error didn't occur?

> 但是如果编译器知道一种*双重秘密*的方式来处理您编写的表达式，并将其转换为单个指令，从而减少步骤数，从而不会发生中间舍入误差，怎么办？


Could it use it? I mean, the results would be different than if you let the rounding error settle each step of the way...

> 你能用它吗？我的意思是，结果会比如果你让舍入误差每一步都结算的结果不同...


Because the results would be different, you can tell the compiler if you want to allow it to do this or not.

> 因为结果会有所不同，你可以告诉编译器是否允许它这么做。

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

> 如果你在全局范围内这样做，它会保持你设置的状态，直到你改变它。


If you do it at block scope, it reverts to the value outside the block when the block ends.

> 如果你在块作用域中做，当块结束时，它会恢复到块外的值。


The initial value of the `FP_CONTRACT` pragma varies from system to system.

> 初始值FP_CONTRACT宏的变化因系统而异。

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

> 这个浮点数代表什么样的实体？有哪些选项？


We're used to floating point numbers being regular old things like `3.14` or `3490.0001`.

> 我们习惯于浮点数是像`3.14`或`3490.0001`这样的常规数字。


But floating point numbers can also represent things like infinity. Or Not-A-Number (NAN). This function will let you know which type of floating point number the argument is.

> 但是浮点数也可以表示无穷大或者非数（NAN）等东西。这个函数可以让你知道参数是哪种浮点数。


This is a macro, so you can use it with `float`, `double`, `long double` or anything similar.

> 这是一个宏，所以你可以用它来处理`float`、`double`、`long double`或类似的东西。

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

> 讨论次正常数超出了本指南的范围，大多数开发人员一生都不会接触到它。简而言之，它是一种表示非常小的数字，这些数字可能会被舍入为零。如果你想了解更多，请参阅维基百科上关于[非正常数](https://en.wikipedia.org/wiki/Denormal_number)的页面。

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

> 输出[^24^](footnotes.html#fn24){#fnref24 .footnote-ref role="doc-noteref"}：

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

> [`isfinite()`](math.html#man-isnan)：检查是否为有限数；[`isinf()`](math.html#man-isnan)：检查是否为无穷大；[`isnan()`](math.html#man-isnan)：检查是否为非数字；[`isnormal()`](math.html#man-isnan)：检查是否为正常数；[`signbit()`](math.html#man-signbit)：检查符号位。

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

> 这些是 fpclassify() 的辅助宏。把宏带来，它们可以在任何浮点类型上工作。

  Macro          Description
  -------------- --------------------------------------------
  `isfinite()`   True if the number is not infinite or NaN.
  `isinf()`      True if the number is infinite.
  `isnan()`      True if the number is Not-a-Number.
  `isnormal()`   True if the number is normal.


For more superficial discussion on normal and subnormal numbers, see [`fpclassify()`](math.html#man-fpclassify).

> 对于关于正常数和次正常数的更浅层次的讨论，请参阅[`fpclassify()`](math.html#man-fpclassify)。

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

> `fpclassify()`：浮点数分类
`signbit()`：符号位

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

> 这个宏接受任何浮点数，并返回一个指示数字符号的值，正或负。

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

> [`fpclassify()`](math.html#man-fpclassify)：浮点数分类
[`isfinite()`](math.html#man-isnan)：有限值检查
[`isinf()`](math.html#man-isnan)：无穷检查
[`isnan()`](math.html#man-isnan)：非数值检查
[`isnormal()`](math.html#man-isnan)：正常值检查
[`copysign()`](math.html#man-copysign)：复制符号

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

> 计算以弧度为单位的数字的反余弦值（即，其余弦为x的值）。该数字必须在-1.0到1.0的范围内。


For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

> 对于那些不记得的人，弧度是另一种测量角度的方式，就像度一样。要从度转换为弧度或反之亦然，请使用以下代码：

::: {#cb251 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-56 .unnumbered .unlisted}


Returns the arc cosine of `x`, unless `x` is out of range. In that case, `errno` will be set to EDOM and the return value will be NaN. The variants return different types.

> 返回`x`的反余弦值，除非`x`超出范围。在这种情况下，`errno`将被设置为EDOM，返回值将为NaN。变体返回不同类型。

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

> [`asin()`](数学.html#man-asin)、[`atan()`](数学.html#man-atan)、[`atan2()`](数学.html#man-atan2)、[`cos()`](数学.html#man-cos)

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

> 计算弧度中的数字的反正弦值（即，其正弦值为x的值）。该数字必须在-1.0到1.0的范围内。


For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

> 对于那些不记得的人，弧度是另一种测量角度的方式，就像度一样。要从度转换为弧度或反之亦然，请使用以下代码：

::: {#cb254 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-57 .unnumbered .unlisted}


Returns the arc sine of `x`, unless `x` is out of range. In that case, `errno` will be set to EDOM and the return value will be NaN. The variants return different types.

> 返回x的反正弦值，除非x超出范围。在这种情况下，errno将被设置为EDOM，返回值将为NaN。变体返回不同类型。

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

> [`acos()`](math.html#man-acos)：反余弦函数，[`atan()`](math.html#man-atan)：反正切函数，[`atan2()`](math.html#man-atan)：双参数反正切函数，[`sin()`](math.html#man-sin)：正弦函数

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

> 计算一个数字的弧度正切值（即其正切值为x的值）。


The `atan2()` variants are pretty much the same as using `atan()` with `y`/`x` as the argument...except that `atan2()` will use those values to determine the correct quadrant of the result.

> atan2() 的变体和使用 y/x 作为参数的 atan() 基本上是一样的...除了 atan2() 会使用这些值来确定结果的正确象限。


For those of you who don't remember, radians are another way of measuring an angle, just like degrees. To convert from degrees to radians or the other way around, use the following code:

> 对于那些不记得的人，弧度是另一种测量角度的方式，就像度一样。要从度转换为弧度或者反过来，请使用以下代码：

::: {#cb257 .sourceCode}
``` {.sourceCode .c}
pi = 3.14159265358979;
degrees = radians * 180 / pi;
radians = degrees * pi / 180;
```
:::

### Return Value {#return-value-58 .unnumbered .unlisted}


The `atan()` functions return the arc tangent of `x`, which will be between PI/2 and -PI/2. The `atan2()` functions return an angle between PI and -PI.

> 函数atan()返回x的反正切值，值介于PI/2和-PI/2之间。函数atan2()返回介于PI和-PI之间的角度。

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

> [`tan()`](math.html#man-tan)：正切函数
[`asin()`](math.html#man-asin)：反正弦函数
[`atan()`](math.html#man-acos)：反正切函数

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

> 对于那些不记得的人，弧度是另一种测量角度的方式，就像度一样。要从度转换为弧度或反之亦然，请使用以下代码：

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

> [`sin()`](math.html#man-sin)，[`tan()`](math.html#man-tan)，[`acos()`](math.html#man-acos)

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

> 对于那些不记得的人，弧度是另一种测量角度的方式，就像度一样。要从度转换为弧度或反之亦然，请使用以下代码：

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

> [`cos()`](数学.html#man-cos), [`tan()`](数学.html#man-tan), [`asin()`](数学.html#man-asin)

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

> 对于那些不记得的人，弧度是另一种测量角度的方式，就像度一样。要从度转换为弧度或反之亦然，请使用以下代码：

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

> [`sin()`](数学.html#man-sin)、[`cos()`](数学.html#man-cos)、[`atan()`](数学.html#man-atan)、[`atan2()`](数学.html#man-atan2)

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

> 这些函数返回x的非负反双曲余弦，x必须大于或等于1。

### Return Value {#return-value-62 .unnumbered .unlisted}


Returns the arc hyperbolic cosince in the range [\\(\[0,+\\infty\]\\)]{.math .inline}.

> 返回反双曲余弦值范围[\(\[0, +\infty\]\)]{.math .inline}。

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

> 这些函数计算x的反双曲正切，x必须在[\(-1,+1\)]范围内。传递完全[\(-1\)]或[\(+1\)]可能会导致极错误。

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

> 这些函数可预测地计算x的双曲余弦。如果x太大，可能会发生范围错误。

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

> 这些函数可预测地计算x的双曲正弦值。如果x太大，可能会发生范围错误。

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

> 计算[\\(e\^x\\)]{.math .inline}，其中[\\(e\\)]{.math .inline}是[欧拉常数](https://en.wikipedia.org/wiki/E_(mathematical_constant))[^25^](footnotes.html#fn25){#fnref25 .footnote-ref role="doc-noteref"}。


The number [\\(e\\)]{.math .inline} is named after Leonard Euler, born April 15, 1707, who is responsible, among other things, for making this reference page longer than it needed to be.

> 数字[\(e\)]{.math .inline}以Leonard Euler的名字命名，他出生于1707年4月15日，他负责的事情之一就是使这个参考页面比需要的更长。

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

> [`exp2()`](math.html#man-exp2)：求2的幂次方
[`expm1()`](math.html#man-expm1)：求e的幂次方减1
[`pow()`](math.html#man-pow)：求x的y次方
[`log()`](math.html#man-log)：求以e为底的对数

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

> 这些函数将2提升到一个幂。非常令人兴奋，因为计算机就是关于2的幂！

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

> 这就像`exp()`一样，只是---*惊喜转折！*--它计算的结果减去一。


For more discussion about what [\\(e\\)]{.math .inline} is, see [the `exp()` man page](math.html#man-exp).

> 对于有关[\(e\)]{.math .inline}是什么的更多讨论，请参阅[`exp()`手册页](math.html#man-exp)。

If `x` is giant, a range error might occur.


For small values of `x` near zero, `expm1(x)` might be more accurate than computing `exp(x)-1`.

> 对于接近零的小值x，使用expm1(x)可能比计算exp(x)-1更精确。

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

> 如果你有一个浮点数，你可以将它分解为它的小数部分和指数部分（以2的幂形式）。


For example, if you have the number [\\(1234.56\\)]{.math .inline}, this can be represented as a multiple of a power of 2 like so:

> 例如，如果你有数字[\\（1234.56\\)]{.math .inline}，它可以表示为2的幂的倍数，如下所示：

[\\(1234.56=0.6028125\\times2\^{11}\\)]{.math .inline}


And you can use this function to get the [\\(0.6028125\\)]{.math .inline} and [\\(11\\)]{.math .inline} parts of that equation.

> 你可以使用这个函数来获得[\\(0.6028125\\)]{.math .inline}和[\\(11\\)]{.math .inline}这个方程式的部分。


As for why, I have a simple answer: I don't know. I can't find a use. K&R2 and everyone else I can find just says *how* to use it, but not *why* you might want to.

> 至于为什么，我有一个简单的答案：我不知道。我找不到用处。K&R2和其他我能找到的人只是说*如何*使用它，但没有*为什么*你可能想要使用它。

The C99 Rationale document says:

> The functions `frexp`, `ldexp`, and `modf` are primitives used by the remainder of the library.
>
> There was some sentiment for dropping them for the same reasons that `ecvt`, `fcvt`, and `gcvt` were dropped, but their adherents rescued them for general use. Their use is problematic: on non-binary architectures, ldexp may lose precision and frexp may be inefficient.

So there you have it. If you need it.

### Return Value {#return-value-71 .unnumbered .unlisted}

`frexp()` returns the fractional part of `value` in the range 0.5 (inclusive) to 1 (exclusive), or 0. And it stores the exponent power-of-2 in the variable pointed to by `exp`.


If you pass in zero, the return value and the variable `exp` points to are both zero.

> 如果你传入零，返回值和`exp`指向的变量都是零。

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

> [`ldexp()`](math.html#man-ldexp)：乘以2的幂次方
[`ilogb()`](math.html#man-ldexp)：计算以2为底的对数
[`modf()`](math.html#man-modf)：将浮点数分解为整数和小数部分

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

> 这给你给定数字的指数...有点奇怪，因为指数取决于`FLT_RADIX`的值。现在，这通常是`2`---但没有保证！


It actually returns [\\(\\log_r\|x\|\\)]{.math .inline} where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

> 实际上，它返回[\\(\\log_r\|x\|\\)]{.math .inline}，其中[\\(r\\)]{.math .inline}是`FLT_RADIX`。


Domain or range errors might occur for invalid values of `x`, or for return values that are outside the range of the return type.

> 可能会因为`x`的无效值或返回值超出返回类型范围而发生域或范围错误。

### Return Value {#return-value-72 .unnumbered .unlisted}


The exponent of the absolute value of the given number, depending on `FLT_RADIX`.

> 给定数字的绝对值的指数取决于`FLT_RADIX`。


Specifically [\\(\\log_r\|x\|\\)]{.math .inline} where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

> 具体来说，[\\(\\log_r\|x\|\\)]{.math .inline}，其中[\\(r\\)]{.math .inline}是FLT_RADIX。

If you pass in `0`, it'll return `FP_ILOGB0`.

If you pass in infinity, it'll return `INT_MAX`.

If you pass in NaN, it'll return `FP_ILOGBNAN`.


The spec goes on to say that the value of `FP_ILOGB0` will be either `INT_MIN` or `-INT_MAX`. And the value of `FP_ILOGBNAN` shall be either `INT_MAX` or `INT_MIN`, if that's useful in any way.

> 该规范进一步指出，`FP_ILOGB0`的值将是`INT_MIN`或`-INT_MAX`。如果有用的话，`FP_ILOGBNAN`的值将是`INT_MAX`或`INT_MIN`。

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

> 这些函数将给定数字x乘以2的exp次幂。

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

> 这些计算基于[\(e\)]{.math .inline}的数字的对数，[\(\log_ex\)]{.math .inline}，[\(\ln x\)]{.math .inline}。


In other words, for a given [\\(x\\)]{.math .inline}, solves [\\(x=e\^y\\)]{.math .inline} for [\\(y\\)]{.math .inline}.

> 就是说，对于给定的[\(x\)]{.math .inline}，求解[\(x=e\^y\)]{.math .inline}的[\(y\)]{.math .inline}。

### Return Value {#return-value-74 .unnumbered .unlisted}


The base-[\\(e\\)]{.math .inline} logarithm of the given value, [\\(\\log_ex\\)]{.math .inline}, [\\(\\ln x\\)]{.math .inline}.

> 求给定值的底数为e的对数，即[\(\log_ex\)]{.math .inline}，[\(\ln x\)]{.math .inline}。

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

> [`exp()`](数学.html#man-exp), [`log10()`](数学.html#man-log10), [`log1p()`](数学.html#man-log10)

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

> 当你以为你必须使用对数定律来计算这个时，突然有一个函数出现来拯救你。


These compute the base-[\\(10\\)]{.math .inline} logarithm of a number, [\\(\\log\_{10}x\\)]{.math .inline}.

> 这些计算数字的基[\(10\)]{.math .inline}对数，[\(\log_{10}x\)]{.math .inline}。


In other words, for a given [\\(x\\)]{.math .inline}, solves [\\(x=10\^y\\)]{.math .inline} for [\\(y\\)]{.math .inline}.

> 就是说，对于给定的[\\(x\\)]{.math .inline}，求解[\\(x=10\^y\\)]{.math .inline}中的[\\(y\\)]{.math .inline}。

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

> 这计算[\( \log_e(1 + x) \)]{.math .inline}，[\( \ln(1+x) \)]{.math .inline}。

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

> 返回[\\(\\log_e(1 + x)\\)]{.math .inline}，[\\(\\ln(1+x)\\)]{.math .inline}。

### Example {#example-77 .unnumbered .unlisted}


Compute some big and small logarithm values to see the difference between `log1p()` and `log()`:

> 计算一些大的和小的对数值，以查看`log1p()`和`log()`之间的区别：

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

> 哇！你以为我们已经完成了对对数函数的学习了吗？我们才刚刚开始！


This one computes [\\(\\log_2 x\\)]{.math .inline}. That is, computes [\\(y\\)]{.math .inline} that satisfies [\\(x=2\^y\\)]{.math .inline}.

> 这个计算[\\(\\log_2 x\\)]{.math .inline}。也就是说，计算[\\(y\\)]{.math .inline}满足[\\(x=2\^y\\)]{.math .inline}的值。

Love me those powers of 2!

### Return Value {#return-value-77 .unnumbered .unlisted}


Returns the base-2 logarithm of the given value, [\\(\\log_2 x\\)]{.math .inline}.

> [\\( \log_2 x \\)]{.math .inline} 的二进制对数

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

> 这个函数返回数字的指数部分，其中指数的底数为`FLT_RADIX`，即[\\(\\log_r\|x\|\\)]{.math .inline}，其中[\\(r\\)]{.math .inline}是`FLT_RADIX`。小数部分会被截断。


If the number is [subnormal](https://en.wikipedia.org/wiki/Denormal_number)[^26^](footnotes.html#fn26){#fnref26 .footnote-ref role="doc-noteref"}, `logb()` treats it as if it were normalized.

> 如果数字是[次正常](https://en.wikipedia.org/wiki/Denormal_number)[^26^](footnotes.html#fn26){#fnref26 .footnote-ref role="doc-noteref"}，`logb()`将其视为正常化处理。

If `x` is `0`, there could be a domain error or pole error.

### Return Value {#return-value-78 .unnumbered .unlisted}


This function returns the whole number portion of [\\(\\log_r\|x\|\\)]{.math .inline} where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

> 这个函数返回[\\(\\log_r\|x\|\\)]{.math .inline}的整数部分，其中[\\(r\\)]{.math .inline}是`FLT_RADIX`。

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

> 如果你有一个浮点数，比如`123.456`，这个函数将提取整数部分（`123.0`）和小数部分（`0.456`）。这正好是最新杰森·斯坦森动作大片的情节，这完全是巧合。


Both the integral part and fractional parts keep the sign of the passed in `value`.

> 两个整数部分和小数部分都保留传入值的符号。

The integral part is stored in the address pointed to by `iptr`.


See the note in [`frexp()`](math.html#man-frexp) regarding why this is in the library.

> 请参阅[`frexp()`](math.html#man-frexp)中关于为什么这在库中的注释。

### Return Value {#return-value-79 .unnumbered .unlisted}


These functions return the fractional part of the number. The integral part is stored in the address pointed to by `iptr`. Both the integral and fractional parts preserve the sign of the passed-in `value`.

> 这些函数返回数字的小数部分。整数部分存储在由`iptr`指向的地址中。整数部分和小数部分都保留传入的`value`的符号。

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

> 计算[\\(x\\times r\^n\\)]{.math .inline}，其中[\\(r\\)]{.math .inline}是`FLT_RADIX`，高效地计算。

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

> 这些函数有效地计算[\\(x\\times r\^n\\)]{.math .inline}，其中[\\(r\\)]{.math .inline}是`FLT_RADIX`。


If `FLT_RADIX` happens to be `2` (no guarantees!), then this works like [`exp2()`](math.html#man-exp2).

> 如果`FLT_RADIX`恰好是`2`（没有保证！），那么它就像[`exp2()`](math.html#man-exp2)一样工作。


The name of this function should have an obvious meaning to you. Clearly they all start with the prefix "scalb" which means...

> 这个函数的名字对你应该有明显的含义。显然，它们都以"scalb"为前缀，意思是...

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

> 我对“scalb”还一无所知，但至少我已经搞清楚了那部分。

A range error might occur for large values.

### Return Value {#return-value-80 .unnumbered .unlisted}


Returns [\\(x\\times r\^n\\)]{.math .inline}, where [\\(r\\)]{.math .inline} is `FLT_RADIX`.

> 返回[\\(x\\times r\^n\\)]{.math .inline}，其中[\\(r\\)]{.math .inline}是FLT_RADIX。

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

> 计算x的立方根[\\(x\^{1/3}\\)]{.math .inline}，[\\(\\sqrt\[3\]{x}\\)]{.math .inline}。

### Return Value {#return-value-81 .unnumbered .unlisted}


Returns the cube root of `x`, [\\(x\^{1/3}\\)]{.math .inline}, [\\(\\sqrt\[3\]{x}\\)]{.math .inline}.

> 返回x的立方根[\\(x\^{1/3}\\)]{.math .inline}, [\\(\\sqrt\[3\]{x}\\)]{.math .inline}。

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

> 这些函数直接返回x的绝对值，即[\\(\|x\|\\)]{.math .inline}。


If you're rusty on your absolute values, all it means is that the result will be positive, even if `x` is negative. It's just strips negative signs off.

> 如果你对绝对值感到生疏，这意味着即使`x`是负数，结果也会是正数。它只是去掉负号。

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

> [`abs()`](stdlib.html#man-abs)：绝对值
[`copysign()`](math.html#man-copysign)：复制符号
[`imaxabs()`](inttypes.html#man-imaxabs)：最大绝对值

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

> 毕达哥拉斯定理的粉丝们欢呼雀跃！这就是你们一直等待的函数！


If you know the lengths of the two sides of a right triangle, `x` and `y`, you can compute the length of the hypotenuse (the longest, diagonal side) with this function.

> 如果你知道直角三角形的两边长度`x`和`y`，你可以用这个函数计算斜边（最长的对角线）的长度。


In particular, it computes the square root of the sum of the squares of the sides: [\\(\\sqrt{x\^2 + y\^2}\\)]{.math .inline}.

> 特别是，它计算了边的平方和的平方根：[\\（\\ sqrt {x \ ^ 2 + y \ ^ 2} \\）] {.math .inline}。

### Return Value {#return-value-83 .unnumbered .unlisted}


Returns the lenght of the hypotenuse of a right triangle with side lengths `x` and `y`: [\\(\\sqrt{x\^2 + y\^2}\\)]{.math .inline}.

> 返回直角三角形的斜边长度，其边长分别为x和y：[\\(\\sqrt{x\^2 + y\^2}\\)]{.math .inline}。

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

> 如果x等于零而y为负数，可能会发生域错误或极错误。

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

> [`exp()`](math.html#man-exp)：指数函数，[`exp2()`](math.html#man-exp2)：2的指数函数，[`sqrt()`](math.html#man-sqrt)：平方根函数，[`cbrt()`](math.html#man-cbrt)：立方根函数

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

> 计算一个数的平方根：[\( \sqrt{x} \)]{.math .inline}。对于那些不知道什么是平方根的人，我不会解释。只要说，一个数的平方根会产生一个值，当平方（自乘）后，结果就是原来的数。


Ok, fine---I did explain it after all, but only because I wanted to show off. It's not like I'm giving you examples or anything, such as the square root of nine is three, because when you multiply three by three you get nine, or anything like that. No examples. I hate examples!

> 好吧，我确实解释了，但只是因为我想炫耀一下。我不会给你举例，比如说九的平方根是三，因为三乘以三就是九，或者类似的东西。没有例子。我讨厌例子！


And I suppose you wanted some actual practical information here as well. You can see the usual trio of functions here---they all compute square root, but they take different types as arguments. Pretty straightforward, really.

> 我想你也想要一些实际的信息。这里你可以看到常见的三个函数——它们都计算平方根，但它们接受不同类型的参数。其实很简单。

A domain error occurs if `x` is negative.

### Return Value {#return-value-85 .unnumbered .unlisted}


Returns (and I know this must be something of a surprise to you) the square root of `x`: [\\(\\sqrt{x}\\)]{.math .inline}.

> 返回[\\(\\sqrt{x}\\)]{.math .inline}（我知道这可能会让你感到惊讶），即x的平方根。

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

> 这些函数计算[错误函数](https://en.wikipedia.org/wiki/Error_function)[^28^](footnotes.html#fn28){#fnref28 .footnote-ref role="doc-noteref"}的值。

### Return Value {#return-value-86 .unnumbered .unlisted}

Returns the error function of `x`:


[\\({\\displaystyle \\frac{2}{\\sqrt\\pi} \\int_0\^x e\^{-t\^2}\\,dt}\\)]{.math .inline}

> [\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2}\,dt}\\)]{.math .inline}

简化的中文：从0到x的2除以$\sqrt{\pi}$的积分$\int_0^x e^{-t^2}\,dt$。

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

> 这些函数计算[补充误差函数](https://en.wikipedia.org/wiki/Error_function)[^29^](footnotes.html#fn29){#fnref29 .footnote-ref role="doc-noteref"}的值。

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

> [\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_x^{\infty} e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_x^{\infty} e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_x^{\infty} e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_x^{\infty} e^{-t^2}\,dt}\\)]{.math .inline}

[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_{x}^{\infty} e^{-t^2}\,dt}\\)]{.math .inline}

简化中文：[\\({\displaystyle \frac{2}{\sqrt{\pi}} \int_{x}^{\infty} e^{-t^2}\,dt}\\)]{.math .inline}

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

> 计算[\\(\\Gamma(x)\\)]{.math .inline}的自然对数的绝对值。

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

> 计算[Γ(x)]{.math .inline}的自然对数的绝对值，[\\(\\log_e\|\\Gamma(x)\|\\)]{.math .inline}。

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

> 计算[伽玛函数](https://zh.wikipedia.org/wiki/%E4%BC%BD%E7%8E%9B%E5%87%BD%E6%95%B0)[^31^](footnotes.html#fn31){#fnref31 .footnote-ref role="doc-noteref"}  中的x，[\\(\\Gamma(x)\\)]{.math .inline}。

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

> 小心这条小龙：它不仅仅是“四舍五入”。好吧，对于正数来说是这样，但是负数实际上会向零舍入。（因为向上取整函数会往最接近的最大整数去取，而[\\(-4\\)]{.math .inline}比[\\(-5\\)]{.math .inline}要大。）

### Return Value {#return-value-90 .unnumbered .unlisted}

Returns the next largest whole number larger than `x`.

### Example {#example-91 .unnumbered .unlisted}


Notice for the negative numbers it heads toward zero, i.e. toward the next largest whole number---just like the positives head toward the next largest whole number.

> 注意负数朝着零，也就是朝着下一个最大的整数，就像正数朝着下一个最大的整数一样。

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

> 返回值的地板：[\(\lfloor{x}\rfloor\)]{.math .inline}。这是ceil()的相反。

This is the largest whole number that is not greater than `x`.

For positive numbers, this is like rounding down: `4.5` becomes `4.0`.

For negative numbers, it's like rounding up: `-3.6` becomes `-4.0`.


In both cases, those results are the largest whole number not bigger than the given number.

> 在这两种情况下，这些结果都是不大于给定数字的最大整数。

### Return Value {#return-value-91 .unnumbered .unlisted}


Returns the largest whole number not greater than `x`: [\\(\\lfloor{x}\\rfloor\\)]{.math .inline}.

> 返回不大于x的最大整数：[\(\lfloor{x}\rfloor\)]{.math .inline}。

### Example {#example-92 .unnumbered .unlisted}


Note how the negative numbers effectively round away from zero, unlike the positives.

> 注意负数如何有效地围绕零向外舍入，而正数则不然。

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

> 这个函数按照当前的舍入方向将x四舍五入到最接近的整数。


The rounding direction can be set with [`fesetround()`](fenv.html#man-fegetround) in `<fenv.h>`.

> 可以使用<fenv.h>中的fesetround()来设置舍入方向。

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

> [rint()](math.html#man-rint)，[lrint()](math.html#man-lrint)，[round()](math.html#man-round)，[fesetround()](fenv.html#man-fegetround)，[fegetround()](fenv.html#man-fegetround)

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

> 这个函数的工作方式和[`nearbyint()`](math.html#man-nearbyint)相似，但它可以引发“不精确”的浮点异常。

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

> nearbyint()，lrint()，round()，fesetround()，fegetround()

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

> 四舍五入浮点数，但这次返回一个整数而不是浮点数，换句话说，只是为了改变一下。

These come in two variants:

-   `lrint()`---returns `long int`
-   `llrint()`---returns `long long int`


If the result doesn't fit in the return type, a domain or range error might occur.

> 如果结果不符合返回类型，可能会发生域或范围错误。

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

> nearbyint()，rint()，round()，fesetround()，fegetround()

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

> 在半数的情况下，从零开始取整（即“按绝对值向上取整”）。


The current rounding direction's Jedi mind tricks don't work on this function.

> 当前的舍入方向的绝地心灵技巧对这个函数无效。

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

> [`lround()`](math.html#man-lround)：取最接近的整数
[`nearbyint()`](math.html#man-nearbyint)：取最接近的整数
[`rint()`](math.html#man-lrint)：取最接近的整数
[`lrint()`](math.html#man-lrint)：取最接近的整数
[`trunc()`](math.html#man-trunc)：取整

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

> 这些就像round()一样，只不过它们会返回整数。


Halfway values round away from zero, e.g. [\\(1.5\\)]{.math .inline} rounds to [\\(2\\)]{.math .inline} and [\\(-1.5\\)]{.math .inline} rounds to [\\(-2\\)]{.math .inline}.

> 半数值四舍五入，例如[\(1.5\)]{.math .inline}四舍五入为[\(2\)]{.math .inline}，[\(-1.5\)]{.math .inline}四舍五入为[\(-2\)]{.math .inline}。

The functions are grouped by return type:

-   `lround()`---returns a `long int`
-   `llround()`---returns a `long long int`


If the rounded value can't fit in the return type, a domain or range error can occur.

> 如果舍入后的值无法适应返回类型，可能会发生域或范围错误。

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

> [`round()`](数学.html#man-lround)、[`nearbyint()`](数学.html#man-nearbyint)、[`rint()`](数学.html#man-lrint)、[`lrint()`](数学.html#man-lrint)、[`trunc()`](数学.html#man-trunc)

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

> 这些函数只是舍弃浮点数的小数部分。砰！

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

> [`round()`](math.html#man-lround)，[`lround()`](math.html#man-lround)，[`nearbyint()`](math.html#man-nearbyint)，[`rint()`](math.html#man-lrint)，[`lrint()`](math.html#man-lrint)

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

> 返回[\\(\\frac{x}{y}\\)]{.math .inline}的余数。结果的符号与x相同。

Under the hood, the computation performed is:

::: {#cb355 .sourceCode}
``` {.sourceCode .c}
x - trunc(x / y) * y
```
:::

But it might be easier just to think of the remainder.

### Return Value {#return-value-98 .unnumbered .unlisted}


Returns the remainder of [\\(\\frac{x}{y}\\)]{.math .inline} with the same sign as `x`.

> 返回[\\(\\frac{x}{y}\\)]{.math .inline}的余数，与x的符号相同。

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

> 这类似于`fmod()`，但不完全相同。如果你期望余数像里程表一样绕行，`fmod()`可能就是你要的。

The C spec quotes IEC 60559 on how this works:

> When [\\(y\\neq0\\)]{.math .inline}, the remainder [\\(r=x\\)]{.math .inline} REM [\\(y\\)]{.math .inline} is defined regardless of the rounding mode by the mathematical relation [\\(r=x-ny\\)]{.math .inline}, where [\\(n\\)]{.math .inline} is the integer nearest the exact value of [\\(x/y\\)]{.math .inline}; whenever [\\(\|n-x/y\|=1/2\\)]{.math .inline}, then [\\(n\\)]{.math .inline} is even. If [\\(r=0\\)]{.math .inline}, its sign shall be that of [\\(x\\)]{.math .inline}.

Hope that clears it up!

OK, maybe not. Here's the upshot:


You know how if you `fmod()` something by, say `2.0` you get a result that is somewhere between `0.0` and `2.0`? And how if you just increase the number that you're modding by `2.0`, you can see the result climb up to `2.0` and then wrap around to `0.0` like your car's odometer?

> 你知道如果你用fmod()函数对某个数字，比如2.0，取模，你会得到一个结果，它的值在0.0和2.0之间吗？如果你只是把取模的数字增加2.0，你会看到结果从0.0上升到2.0，然后像你汽车的里程表一样回到0.0？

`remainder()` works just like that, except if `y` is `2.0`, it wraps from `-1.0` to `1.0` instead of from `0.0` to `2.0`.


In other words, the range of the function runs from `-y/2` to `y/2`. Contrasted to `fmod()` that runs from `0.0` to `y`, `remainder()`'s output is just shifted down half a `y`.

> 换句话说，函数的范围从-y/2到y/2。与fmod()从0.0到y的输出相比，remainder()的输出只是向下移动了一半的y。

And zero-remainder-anything is `0`.


Except if `y` is zero, the function might return zero or a domain error might occur.

> 除非`y`等于零，否则函数可能会返回零，或者可能会发生域错误。

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

> 首先，返回值是余数，与[`remainder()`](math.html#man-remainder)函数相同，所以请查看一下。

And the quotient comes back in the `quo` pointer.


Or at least *some of it* does. You'll get at least 3 bits worth of the quotient.

> 至少有一部分是这样的。你至少会得到3位的商数。

But *why*?

So a couple things.


One is that the quotient of some very large floating point numbers can easily be far too gigantic to fit in even a `long long unsigned int`. So some of it might very well need to be lopped off, anyway.

> 一种情况是，某些非常大的浮点数的商可能很容易变得太巨大，以至于无法容纳在一个“long long unsigned int”中。所以其中的一些可能需要被削减。

But at 3 bits? How's that even useful? That only gets you from 0 to 7!

The C99 Rationale document states:

> The `remquo` functions are intended for implementing argument reductions which can exploit a few low-order bits of the quotient. Note that [\\(x\\)]{.math .inline} may be so large in magnitude relative to [\\(y\\)]{.math .inline} that an exact representation of the quotient is not practical.


So... implementing argument reductions... which can exploit a few low-order bits... Ooookay.

> 所以...实施参数简化...可以利用一些低位位...好的。


[CPPReference has this to say](https://en.cppreference.com/w/c/numeric/math/remquo)[^32^](footnotes.html#fn32){#fnref32 .footnote-ref role="doc-noteref"} on the matter, which is spoken so well, I will quote wholesale:

> [CPPReference有这么说](https://en.cppreference.com/w/c/numeric/math/remquo)[^32^](footnotes.html#fn32){#fnref32 .footnote-ref role="doc-noteref"}关于这个问题，说得很好，我将它完整引用：

> This function is useful when implementing periodic functions with the period exactly representable as a floating-point value: when calculating [\\(\\sin(πx)\\)]{.math .inline} for a very large `x`, calling `sin` directly may result in a large error, but if the function argument is first reduced with `remquo`, the low-order bits of the quotient may be used to determine the sign and the octant of the result within the period, while the remainder may be used to calculate the value with high precision.


And there you have it. If you have another example that works for you... congratulations! :)

> 那就是这样了。如果你有另一个对你有用的例子...祝贺你！ :)

### Return Value {#return-value-100 .unnumbered .unlisted}


Returns the same as [`remainder`](math.html#man-remainder): The IEC 60559 result of `x`-remainder-`y`.

> 返回与[`remainder`](math.html#man-remainder)相同的结果：IEC 60559对`x`取余`y`的结果。


In addition, at least the lowest 3 bits of the quotient will be stored in `quo` with the same sign as `x/y`.

> 此外，商的最低3位至少会被存储在`quo`中，且其符号与`x/y`相同。

### Example {#example-101 .unnumbered .unlisted}


There's a [great `cos()` example at CPPReference](https://en.cppreference.com/w/c/numeric/math/remquo)[^33^](footnotes.html#fn33){#fnref33 .footnote-ref role="doc-noteref"} that covers a genuine use case.

> 这里有一个[在CPPReference上的很棒的`cos()`例子](https://en.cppreference.com/w/c/numeric/math/remquo)[^33^](footnotes.html#fn33){#fnref33 .footnote-ref role="doc-noteref"}，可以覆盖一个真实的用例。


But instead of stealing it, I'll just post a simple example here and you can visit their site for a real one.

> 但是我不会偷它，我只会在这里发布一个简单的例子，你可以访问他们的网站来获得一个真实的例子。

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

> [`remainder()`](math.html#man-remainder)：余数（）
[`imaxdiv()`](inttypes.html#man-imaxdiv)：imaxdiv（）

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

> 这些函数返回一个数字，该数字的大小与`x`相同，符号与`y`相同。您可以使用它们来强制将符号转换为另一个值的符号。


Neither `x` nor `y` are modified, of course. The return value holds the result.

> 无论x还是y都没有被修改，当然。返回值保存了结果。

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

> 这些函数返回一个安静的NaN[^34^]（脚注）。它的产生就好像调用[`strtod()`](stdlib.html#man-strtod)，并将`"NAN"`（或其变体）作为参数。

`tagp` points to a string which could be several things, including empty. The contents of the string determine which variant of NaN might get returned depending on the implementation.


Which *version* of NaN? Did you even know it was possible to get this far into the weeds with something that wasn't a number?

> 哪个版本的NaN？你知道有可能用不是数字的东西走到这么深的层面吗？


Case 1 in which you pass in an empty string, in which case these are the same:

> 在传入空字符串的情况下，情况1和情况2是相同的。

::: {#cb364 .sourceCode}
``` {.sourceCode .c}
nan("");

strtod("NAN()", NULL);
```
:::


Case 2 in which the string contains only digits 0-9, letters a-z, letters A-Z, and/or underscore:

> 情况2：字符串仅包含数字0-9、小写字母a-z、大写字母A-Z和/或下划线。

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

> 至于`strtod()`如何处理括号中的值，请参阅[`strtod()`]参考页面。剧透：这是实现定义的。

### Return Value {#return-value-102 .unnumbered .unlisted}


Returns the requested quiet NaN, or 0 if such things aren't supported by your system.

> 返回所请求的安静NaN，如果您的系统不支持这样的东西，则返回0。

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

> 你可能知道，浮点数不能表示所有的实数。有限制。


And, as such, there exists a "next" and "previous" number after or before any floating point number.

> 浮点数之前或之后，都存在一个“下一个”和“上一个”数字。


These functions return the next (or previous) representable number. That is, no floating point numbers exist between the given number and the next one.

> 这些函数返回下一个（或上一个）可表示的数字。也就是说，在给定的数字和下一个数字之间不存在浮点数。


The way it figures it out is it works from `x` in the direction of `y`, answering the question of "what is the next representable number from `x` as we head toward `y`.

> 从`x`朝着`y`的方向工作，回答“从`x`朝着`y`前进时下一个可表示的数字是什么？”的问题，这就是它如何计算出来的。

### Return Value {#return-value-103 .unnumbered .unlisted}


Returns the next representable floating point value from `x` in the direction of `y`.

> 返回从x朝向y的下一个可表示的浮点值。

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

> 这些函数与[`nextafter()`](math.html#man-nextafter)相同，只是第二个参数始终是`long double`。

### Return Value {#return-value-104 .unnumbered .unlisted}


Returns the same as [`nextafter()`](math.html#man-nextafter) except if `x` equals `y`, returns `y` cast to the function's return type.

> 返回与[`nextafter()`](math.html#man-nextafter)相同的结果，除非`x`等于`y`，此时返回`y`转换为函数的返回类型。

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

> 正差异x和y之间的差异是......除非差异小于0，否则将其限制为0。

These functions might throw a range error.

### Return Value {#return-value-105 .unnumbered .unlisted}


Returns the difference of `x-y` if the difference is greater than `0`. Otherwise it returns `0`.

> 如果x-y的差值大于0，则返回x-y的差值，否则返回0。

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

> 这些函数直接返回给定两个数字的最小值或最大值。


If one of the numbers is NaN, the functions return the non-NaN number. If both arguments are NaN, the functions return NaN.

> 如果其中一个数字是NaN，函数将返回非NaN数字。如果两个参数都是NaN，函数将返回NaN。

### Return Value {#return-value-106 .unnumbered .unlisted}


Returns the minimum or maximum values, with NaN handled as mentioned above.

> 返回最小或最大值，以上述方式处理NaN。

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

> 这个操作执行[\((x\times{y})+z\)]{.math .inline}，但是以一种精巧的方式来完成。它以无限精度的方式执行计算，然后根据当前的舍入模式将最终结果舍入到最终数据类型。


Contrast to if you'd do the math yourself, where it would have rounded each step of the way, potentially.

> 相比起如果你自己做数学，可能会在每一步都进行四舍五入。


Also some architectures have a CPU instruction to do exactly this calculation, so it can do it super quick. (If it doesn't, it's considerably slower.)

> 也有一些架构有一个CPU指令来完成这个计算，所以它可以非常快速地完成。（如果没有，它就会变得相对较慢。）


You can tell if your CPU supports the fast version by checking that the macro `FP_FAST_FMA` is set to `1`. (The `float` and `long` variants of `fma()` can be tested with `FP_FAST_FMAF` and `FP_FAST_FMAL`, respectively.)

> 你可以通过检查宏`FP_FAST_FMA`设置为`1`来检查你的CPU是否支持快速版本。（可以使用`FP_FAST_FMAF`和`FP_FAST_FMAL`分别测试`float`和`long`变体的`fma()`。）

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

> 这些宏比较浮点数。由于是宏，我们可以传入任何浮点类型。


You might think you can already do that with just regular comparison operators---and you'd be right!

> 你可能会认为只用常规比较运算符就可以做到这一点---而且你是对的！


One one exception: the comparison operators raise the "invalid" floating exception if one or more of the operands is NaN. These macros do not.

> 除一个例外：如果操作数中有一个或多个是NaN，比较操作符会引发“无效”浮点异常。而这些宏则不会。


Note that you must only pass floating point types into these functions. Passing an integer or any other type is undefined behavior.

> 注意，你只能传入浮点类型到这些函数中。传入整数或其他类型是未定义的行为。

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

> [`islessgreater()`](math.html#man-islessgreater)：比较两个值是否不相等
[`isunordered()`](math.html#man-isunordered)：检查两个值是否未排序

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

> 这个宏类似于`isgreater()`等，但如果我把它放在上面，就会使节名过长。所以它有自己的位置。


This returns true if [\\(x \< y\\)]{.math .inline} or [\\(x \> y\\)]{.math .inline}.

> 这将返回true，如果\\（x < y\\）或\\（x > y\\）。


Even though it's a macro, we can rest assured that `x` and `y` are only evaluated once.

> 即使它是一个宏，我们也可以放心，`x`和`y`只会被评估一次。


And even if `x` or `y` are NaN, this will not throw an "invalid" exception, unlike the normal comparison operators.

> 即使`x`或`y`是NaN，这也不会抛出一个“无效”异常，不像正常的比较运算符。

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

> [`isgreater()`](math.html#man-isgreater)，[`isgreaterequal()`](math.html#man-isgreater)，[`isless()`](math.html#man-isgreater)，[`islessequal()`](math.html#man-isgreater)，[`isunordered()`](math.html#man-isunordered)

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

> 它也阐述了，如果其中一个或两个参数是NaN，那么参数是无序的。

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

> [`isgreater()`](math.html#man-isgreater)，[`isgreaterequal()`](math.html#man-isgreater)，[`isless()`](math.html#man-isgreater)，[`islessequal()`](math.html#man-isgreater)，[`islessgreater()`](math.html#man-islessgreater)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](locale.html) \| [Contents](index.html) \| [Next](setjmp.html)
:::
