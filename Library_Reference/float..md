---
tip: translate by openai@2023-07-20 18:16:36
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](fenv.html) \| [Contents](index.html) \| [Next](inttypes.html)
:::

------------------------------------------------------------------------

# [8]{.header-section-number} `<float.h>` Floating Point Limits {#float number="8"}


  -------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------
简体中文
  Macro                 Minimum Magnitude  Description

  -------------------- ------------------- --------------------------------------------------------------------------------------------

> -------------------- ------------------- --------------------------------------------------------------------------------------------
空白
  `FLT_ROUNDS`                             Current rounding mode

  `FLT_EVAL_METHOD`                        Types used for evaluation

  `FLT_HAS_SUBNORM`                        Subnormal support for `float`

  `DBL_HAS_SUBNORM`                        Subnormal support for `double`


  `LDBL_HAS_SUBNORM`                       Subnormal support for `long double`

> `long double`支持子规格

  `FLT_RADIX`                  `2`         Floating point radix (base)


  `FLT_MANT_DIG`                           Number of base `FLT_RADIX` digits in a `float`

> `FLT_MANT_DIG`：float的基数FLT_RADIX的位数


  `DBL_MANT_DIG`                           Number of base `FLT_RADIX` digits in a `double`

> `DBL_MANT_DIG`：双精度浮点数中基数`FLT_RADIX`的位数


  `LDBL_MANT_DIG`                          Number of base `FLT_RADIX` digits in a `long double`

> `LDBL_MANT_DIG`代表`long double`中基于`FLT_RADIX`的数字位数。


  `FLT_DECIMAL_DIG`            `6`         Number of decimal digits required to encode a `float`

> `FLT_DECIMAL_DIG` 6，表示编码一个`float`所需要的小数位数。


  `DBL_DECIMAL_DIG`           `10`         Number of decimal digits required to encode a `double`

> `DBL_DECIMAL_DIG` 10：编码一个`double`所需的小数位数


  `LDBL_DECIMAL_DIG`          `10`         Number of decimal digits required to encode a `long double`

> `LDBL_DECIMAL_DIG` 10：编码`long double`所需的小数位数。


  `DECIMAL_DIG`               `10`         Number of decimal digits required to encode the the widest floating point number supported

> `DECIMAL_DIG` 10：支持的最宽浮点数需要编码的小数位数。


  `FLT_DIG`                    `6`         Number of decimal digits that can be safely stored in a `float`

> `FLT_DIG` 6，float类型可以安全存储的小数位数。


  `DBL_DIG`                   `10`         Number of decimal digits that can be safely stored in a `double`

> `DBL_DIG` 10：可以安全存储在双精度浮点数中的小数位数。


  `LDBL_DIG`                  `10`         Number of decimal digits that can be safely stored in a `long double`

> `LDBL_DIG` 10，可以安全存储在`long double`中的十进制位数。


  `FLT_MIN_EXP`                            `FLT_RADIX` to the `FLT_MIN_EXP-1` power is the smallest normalized `float`

> `FLT_MIN_EXP`的`FLT_RADIX`次方是最小的归一化`float`


  `DBL_MIN_EXP`                            `FLT_RADIX` to the `DBL_MIN_EXP-1` power is the smallest normalized `double`

> `DBL_MIN_EXP`的`FLT_RADIX`的`DBL_MIN_EXP-1`次方是最小的归一化`double`


  `LDBL_MIN_EXP`                           `FLT_RADIX` to the `LDBL_MIN_EXP-1` power is the smallest normalized `long double`

> 最小的标准化长双精度数是以`LDBL_MIN_EXP-1`次幂的`FLT_RADIX`为底的数。


  `FLT_MIN_10_EXP`            `-37`        Minimum exponent such that `10` to this number is a normalized `float`

> FLT_MIN_10_EXP：-37，表示10的最小指数，使得它能够成为一个标准化的浮点数。


  `DBL_MIN_10_EXP`            `-37`        Minimum exponent such that `10` to this number is a normalized `double`

> 最小指数，使得10的该数字是归一化的双精度数。


  `LDBL_MIN_10_EXP`           `-37`        Minimum exponent such that `10` to this number is a normalized `long_double`

> 最小指数，使得10的该数字是归一化的长双精度数为-37


  `FLT_MAX_EXP`                            `FLT_RADIX` to the `FLT_MAX_EXP-1` power is the largest finite `float`

> `FLT_MAX_EXP`的`FLT_RADIX`的`FLT_MAX_EXP-1`次方是最大的有限`float`


  `DBL_MAX_EXP`                            `FLT_RADIX` to the `DBL_MAX_EXP-1` power is the largest finite `double`

> `DBL_MAX_EXP`的`FLT_RADIX`的`DBL_MAX_EXP-1`次方是最大的有限`double`


  `LDBL_MAX_EXP`                           `FLT_RADIX` to the `LDBL_MAX_EXP-1` power is the largest finite `long double`

> 最大的有限`long double`是`LDBL_MAX_EXP-1`次方的`FLT_RADIX`。


  `FLT_MAX_10_EXP`            `-37`        Minimum exponent such that `10` to this number is a finite `float`

> FLT_MAX_10_EXP -37：10的最小指数，使得float有限。


  `DBL_MAX_10_EXP`            `-37`        Minimum exponent such that `10` to this number is a finite `double`

> 最小指数，使得10的这个数字成为有限的双精度数为-37。


  `LDBL_MAX_10_EXP`           `-37`        Minimum exponent such that `10` to this number is a finite `long_double`

> 最小指数，使得10的这个数字是有限的long_double。

  `FLT_MAX`                  `1E+37`       Largest finite `float`

  `DBL_MAX`                  `1E+37`       Largest finite `double`

  `LDBL_MAX`                 `1E+37`       Largest finite `long double`

  -------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------
简体中文


  -------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------
简体中文
  Macro                Maximum Value    Description

  ----------------- ------------------- -----------------------------------------------------------------------

> ----------------- ------------------- -----------------------------------------------------------------------
无限期的空白

  `FLT_EPSILON`           `1E-5`        Difference between 1 and the next biggest representable `float`

> FLT_EPSILON：1E-5：1和下一个最大可表示的浮点数之间的差异


  `DBL_EPSILON`           `1E-9`        Difference between 1 and the next biggest representable `double`

> DBL_EPSILON：1E-9：表示为double类型的1和下一个最大值之间的差异


  `LDBL_EPSILON`          `1E-9`        Difference between 1 and the next biggest representable `long double`

> LDBL_EPSILON：1E-9：最接近1的下一个可表示的long double之间的差异。


  `FLT_MIN`               `1E-37`       Minimum positive normalized `float`

> FLT_MIN 1E-37 代表最小的正常化浮点数。


  `DBL_MIN`               `1E-37`       Minimum positive normalized `double`

> 最小正常化双精度的值为1E-37


  `LDBL_MIN`              `1E-37`       Minimum positive normalized `long double`

> 最小正常化的长双精度数为1E-37

  `FLT_TRUE_MIN`          `1E-37`       Minimum positive `float`

  `DBL_TRUE_MIN`          `1E-37`       Minimum positive `double`

  `LDBL_TRUE_MIN`         `1E-37`       Minimum positive `long double`

  -------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------
简化中文


The minimum and maximum values here are from the spec---they should what you can at least expect across all platforms. Your super dooper machine might do better, still!

> 这里的最小和最大值来自规格——它们应该是你可以在所有平台上至少期望的值。你的超级机器可能会做得更好！

## [8.1]{.header-section-number} Background {#background-1 number="8.1"}


The spec allows a lot of leeway when it comes to how C represents floating point numbers. This header file spells out the limits on those numbers.

> 规范允许C在表示浮点数方面有很大的余地。此头文件阐明了这些数字的限制。


It gives a model that can describe any floating point number that I *know* you're going to absolutely love. It looks like this:

> 它提供了一个可以描述任何浮点数的模型，我知道你一定会喜欢。它看起来像这样：


[\\(\\displaystyle x=sb\^e\\sum\_{k=1}\^p f_k b\^{-k}, e\_{min} \\le e \\le e\_{max}\\)]{.math .inline}

> \(\displaystyle x=\sum_{k=1}^p f_k b^{e-k}, e_{min} \le e \le e_{max}\)

where:

            Variable           Meaning

  ---------------------------- ------------------------------------------------------------------------

> ---------------------------- ------------------------------------------------------------------------
简体中文：
---------------------------- ------------------------------------------------------------------------
    [\\(s\\)]{.math .inline}   Sign, [\\(-1\\)]{.math .inline} or [\\(1\\)]{.math .inline}
    [\\(b\\)]{.math .inline}   Base (radix), probably [\\(2\\)]{.math .inline} on your system
    [\\(e\\)]{.math .inline}   Exponent
    [\\(p\\)]{.math .inline}   Precision: how many base-[\\(b\\)]{.math .inline} digits in the number

   [\\(f_k\\)]{.math .inline}  The individual digits of the number, the significand

> [$f_k$]{.math .inline} 这个数字的个位数，尾数

But let's blissfully ignore all that for a second.


Let's assume your computer uses base 2 for it's floating point (it probably does). And that in the example below the 1s-and-0s numbers are in binary, and the rest are in decimal.

> 假设你的计算机使用二进制来表示它的浮点数（它很可能是这样）。在下面的例子中，1和0的数字是二进制的，其余的是十进制的。


The short of it is you could have floating point numbers like shown in this example:

> 简而言之，你可以像这个例子中所示的那样使用浮点数：

[\\(-0.10100101 \\times 2\^5 = -10100.101 = -20.625\\)]{.math .inline}


That's your fractional part multiplied by the base to the exponent's power. The exponent controls where the decimal point is. It "floats" around!

> 那是你的小数部分乘以底数的指数次方。指数控制小数点的位置。它“浮动”起来！

## [8.2]{.header-section-number} `FLT_ROUNDS` Details {#flt_rounds-details number="8.2"}


This tells you the rounding mode. It can be changed with a call to [`fesetround()`](fenv.html#man-fegetround).

> 这告诉体你舍入模式。可以通过调用[`fesetround()`](fenv.html#man-fegetround)来更改它。

   Mode  Description
  ------ -----------------------------------------
   `-1`  Indeterminable
   `0`   Toward zero
   `1`   To nearest
   `2`   Toward positive infinity
   `3`   Toward negative infinity... and beyond!


Unlike every other macro in this here header, `FLT_ROUNDS` might not be a constant expression.

> 不像这里的其他宏一样，`FLT_ROUNDS`可能不是一个常量表达式。

## [8.3]{.header-section-number} `FLT_EVAL_METHOD` Details {#flt_eval_method-details number="8.3"}


This basically tells you how floating point values are promoted to different types in expressions.

> 这基本上告诉你在表达式中浮点值如何被提升到不同的类型。


  -------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------
简体中文
   Method   Description

  --------- ---------------------------------------------------------------------------------------------

> --------- ---------------------------------------------------------------------------------------------
空白
    `-1`    Indeterminable

     `0`    Evaluate all operations and constants to the precision of their respective types

     `1`    Evaluate `float` and `double` operations as `double` and `long double` ops as `long double`

     `2`    Evaluate all operations and constants as `long double`

  -------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------
简体中文

## [8.4]{.header-section-number} Subnormal Numbers {#subnormal-numbers number="8.4"}


The macros `FLT_HAS_SUBNORM`, `DBL_HAS_SUBNORM`, and `LDBL_HAS_SUBNORM` all let you know if those types support [subnormal numbers](https://en.wikipedia.org/wiki/Subnormal_number)[^18^](footnotes.html#fn18){#fnref18 .footnote-ref role="doc-noteref"}.

> 宏`FLT_HAS_SUBNORM`、`DBL_HAS_SUBNORM`和`LDBL_HAS_SUBNORM`都可以让您知道这些类型是否支持[次规格数字](https://en.wikipedia.org/wiki/Subnormal_number)[^18^](footnotes.html#fn18){#fnref18 .footnote-ref role="doc-noteref"}。

   Value  Description
  ------- ----------------------------------------
   `-1`   Indeterminable
    `0`   Subnormals not supported for this type
    `1`   Subnormals supported for this type

## [8.5]{.header-section-number} How Many Decimal Places Can I Use? {#how-many-decimal-places-can-i-use number="8.5"}

It depends on what you want to do.


The safe thing is if you never use more than `FLT_DIG` base-10 digits in your `float`, you're good. (Same for `DBL_DIG` and `LDBL_DIG` for their types.)

> 安全的做法是，如果你在浮点数中仅使用`FLT_DIG`个十进制数字，就可以了（对于它们的类型，`DBL_DIG`和`LDBL_DIG`也是如此）。

And by "use" I mean print out, have in code, read from the keyboard, etc.


You can print out that many decimal places with `printf()` and the `%g` format specifier:

> 你可以使用`printf()`和`%g`格式说明符打印出许多小数位：

::: {#cb208 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <float.h>

int main(void)
{
    float pi = 3.1415926535897932384626433832795028841971;

    // With %g or %G, the precision refers to the number of significant
    // digits:

    printf("%.*g\n", FLT_DIG, pi);  // For me: 3.14159

    // But %f prints too many, since the precision is the number of
    // digits to the right of the decimal--it doesn't count the digits
    // to the left of it:

    printf("%.*f\n", FLT_DIG, pi);  // For me: 3.14159... 3 ???
}
```
:::


That's the end, but stay tuned for the exciting conclusion of "How Many Decimal Places Can I Use?"

> 那就是结束了，但请继续关注“我能使用多少位小数？”的激动人心的结局！


Because base 10 and base 2 (your typical `FLT_RADIX`) don't mix very well, you can actually have more than `FLT_DIG` in your `float`; the bits of storage go out a little farther. But these might round in a way you don't expect.

> 因为十进制和二进制（你的典型`FLT_RADIX`）不太好混合，你可以在`float`中拥有超过`FLT_DIG`的存储位；存储位会超出一点。但是这些可能会以你意想不到的方式舍入。


But if you want to convert a floating point number to base 10 and then be able to convert it back again to the exact same floating point number, you'll need `FLT_DECIMAL_DIG` digits from your `float` to make sure you get those extra bits of storage represented. (And `DBL_DECIMAL_DIG` and `LDBL_DECIMAL_DIG` for those corresponding types.)

> 如果你想将浮点数转换为十进制，然后又能够将其准确地转换回原来的浮点数，你需要从你的`float`中获取`FLT_DECIMAL_DIG`位数，以确保你能够表示那些额外的存储位。（对于相应类型，还有`DBL_DECIMAL_DIG`和`LDBL_DECIMAL_DIG`。）


Here's some example output that shows how the value stored might have some extra decimal places at the end.

> 这里有一些示例输出，它显示存储的值可能会在末尾有一些额外的小数位。

::: {#cb209 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <assert.h>
#include <float.h>

int main(void)
{
    printf("FLT_DIG = %d\n", FLT_DIG);
    printf("FLT_DECIMAL_DIG = %d\n\n", FLT_DECIMAL_DIG);

    assert(FLT_DIG == 6);  // Code below assumes this

    for (float x = 0.123456; x < 0.12346; x += 0.000001) {
        printf("As written: %.*g\n", FLT_DIG, x);
        printf("As stored:  %.*g\n\n", FLT_DECIMAL_DIG, x);
    }
}
```
:::


And the output on my machine, starting at `0.123456` and incrementing by `0.000001` each time:

> 以及我机器上的输出，从0.123456开始，每次增加0.000001：

::: {#cb210 .sourceCode}
``` {.sourceCode .default}
FLT_DIG = 6
FLT_DECIMAL_DIG = 9

As written: 0.123456
As stored:  0.123456001

As written: 0.123457
As stored:  0.123457

As written: 0.123458
As stored:  0.123457998

As written: 0.123459
As stored:  0.123458996

As written: 0.12346
As stored:  0.123459995
```
:::


You can see that the value stored isn't always the value we're expecting since base-2 can't represent all base-10 fractions exactly. The best it can do is store more places and then round.

> 你可以看到，存储的值并不总是我们期望的值，因为二进制无法精确表示所有十进制分数。它能做的最好的就是存储更多的位数，然后进行四舍五入。


Also notice that even though we tried to stop the `for` loop *before* `0.123460`, it actually ran including that value since the stored version of that number was `0.123459995`, which is still less than `0.123460`.

> 此外，请注意，尽管我们试图在`0.123460`之前停止`for`循环，但由于存储的该数字为`0.123459995`，它仍然小于`0.123460`，因此实际上它还是运行了包括该值的循环。

Aren't floating point numbers fun?

## [8.6]{.header-section-number} Comprehensive Example {#comprehensive-example number="8.6"}

Here's a program that prints out the details for a particular machine:

::: {#cb211 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <float.h>

int main(void)
{
    printf("FLT_RADIX: %d\n", FLT_RADIX);
    printf("FLT_ROUNDS: %d\n", FLT_ROUNDS);
    printf("FLT_EVAL_METHOD: %d\n", FLT_EVAL_METHOD);
    printf("DECIMAL_DIG: %d\n\n", DECIMAL_DIG);

    printf("FLT_HAS_SUBNORM: %d\n", FLT_HAS_SUBNORM);
    printf("FLT_MANT_DIG: %d\n", FLT_MANT_DIG);
    printf("FLT_DECIMAL_DIG: %d\n", FLT_DECIMAL_DIG);
    printf("FLT_DIG: %d\n", FLT_DIG);
    printf("FLT_MIN_EXP: %d\n", FLT_MIN_EXP);
    printf("FLT_MIN_10_EXP: %d\n", FLT_MIN_10_EXP);
    printf("FLT_MAX_EXP: %d\n", FLT_MAX_EXP);
    printf("FLT_MAX_10_EXP: %d\n", FLT_MAX_10_EXP);
    printf("FLT_MIN: %.*e\n", FLT_DECIMAL_DIG, FLT_MIN);
    printf("FLT_MAX: %.*e\n", FLT_DECIMAL_DIG, FLT_MAX);
    printf("FLT_EPSILON: %.*e\n", FLT_DECIMAL_DIG, FLT_EPSILON);
    printf("FLT_TRUE_MIN: %.*e\n\n", FLT_DECIMAL_DIG, FLT_TRUE_MIN);

    printf("DBL_HAS_SUBNORM: %d\n", DBL_HAS_SUBNORM);
    printf("DBL_MANT_DIG: %d\n", DBL_MANT_DIG);
    printf("DBL_DECIMAL_DIG: %d\n", DBL_DECIMAL_DIG);
    printf("DBL_DIG: %d\n", DBL_DIG);
    printf("DBL_MIN_EXP: %d\n", DBL_MIN_EXP);
    printf("DBL_MIN_10_EXP: %d\n", DBL_MIN_10_EXP);
    printf("DBL_MAX_EXP: %d\n", DBL_MAX_EXP);
    printf("DBL_MAX_10_EXP: %d\n", DBL_MAX_10_EXP);
    printf("DBL_MIN: %.*e\n", DBL_DECIMAL_DIG, DBL_MIN);
    printf("DBL_MAX: %.*e\n", DBL_DECIMAL_DIG, DBL_MAX);
    printf("DBL_EPSILON: %.*e\n", DBL_DECIMAL_DIG, DBL_EPSILON);
    printf("DBL_TRUE_MIN: %.*e\n\n", DBL_DECIMAL_DIG, DBL_TRUE_MIN);

    printf("LDBL_HAS_SUBNORM: %d\n", LDBL_HAS_SUBNORM);
    printf("LDBL_MANT_DIG: %d\n", LDBL_MANT_DIG);
    printf("LDBL_DECIMAL_DIG: %d\n", LDBL_DECIMAL_DIG);
    printf("LDBL_DIG: %d\n", LDBL_DIG);
    printf("LDBL_MIN_EXP: %d\n", LDBL_MIN_EXP);
    printf("LDBL_MIN_10_EXP: %d\n", LDBL_MIN_10_EXP);
    printf("LDBL_MAX_EXP: %d\n", LDBL_MAX_EXP);
    printf("LDBL_MAX_10_EXP: %d\n", LDBL_MAX_10_EXP);
    printf("LDBL_MIN: %.*Le\n", LDBL_DECIMAL_DIG, LDBL_MIN);
    printf("LDBL_MAX: %.*Le\n", LDBL_DECIMAL_DIG, LDBL_MAX);
    printf("LDBL_EPSILON: %.*Le\n", LDBL_DECIMAL_DIG, LDBL_EPSILON);
    printf("LDBL_TRUE_MIN: %.*Le\n\n", LDBL_DECIMAL_DIG, LDBL_TRUE_MIN);
    
    printf("sizeof(float): %zu\n", sizeof(float));
    printf("sizeof(double): %zu\n", sizeof(double));
    printf("sizeof(long double): %zu\n", sizeof(long double));
}
```
:::

And here's the output on my machine:

::: {#cb212 .sourceCode}
``` {.sourceCode .default}
FLT_RADIX: 2
FLT_ROUNDS: 1
FLT_EVAL_METHOD: 0
DECIMAL_DIG: 21

FLT_HAS_SUBNORM: 1
FLT_MANT_DIG: 24
FLT_DECIMAL_DIG: 9
FLT_DIG: 6
FLT_MIN_EXP: -125
FLT_MIN_10_EXP: -37
FLT_MAX_EXP: 128
FLT_MAX_10_EXP: 38
FLT_MIN: 1.175494351e-38
FLT_MAX: 3.402823466e+38
FLT_EPSILON: 1.192092896e-07
FLT_TRUE_MIN: 1.401298464e-45

DBL_HAS_SUBNORM: 1
DBL_MANT_DIG: 53
DBL_DECIMAL_DIG: 17
DBL_DIG: 15
DBL_MIN_EXP: -1021
DBL_MIN_10_EXP: -307
DBL_MAX_EXP: 1024
DBL_MAX_10_EXP: 308
DBL_MIN: 2.22507385850720138e-308
DBL_MAX: 1.79769313486231571e+308
DBL_EPSILON: 2.22044604925031308e-16
DBL_TRUE_MIN: 4.94065645841246544e-324

LDBL_HAS_SUBNORM: 1
LDBL_MANT_DIG: 64
LDBL_DECIMAL_DIG: 21
LDBL_DIG: 18
LDBL_MIN_EXP: -16381
LDBL_MIN_10_EXP: -4931
LDBL_MAX_EXP: 16384
LDBL_MAX_10_EXP: 4932
LDBL_MIN: 3.362103143112093506263e-4932
LDBL_MAX: 1.189731495357231765021e+4932
LDBL_EPSILON: 1.084202172485504434007e-19
LDBL_TRUE_MIN: 3.645199531882474602528e-4951

sizeof(float): 4
sizeof(double): 8
sizeof(long double): 16
```
:::

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](fenv.html) \| [Contents](index.html) \| [Next](inttypes.html)
:::
