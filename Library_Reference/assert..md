---
tip: translate by openai@2023-07-20 17:56:17
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}

[Prev](the-c-language.html) \| [Contents](index.html) \| [Next](complex.html)

> [上一页](the-c-language.html) \| [目录](index.html) \| [下一页](complex.html)
:::

------------------------------------------------------------------------

# [3]{.header-section-number} `<assert.h>` Runtime and Compile-time Diagnostics {#assert number="3"}

  Macro               Description
  ------------------- ------------------------
  `assert()`          Runtime assertion
  `static_assert()`   Compile-time assertion


This functionality has to do with things that Should Never Happen™. If you have something that should never be true and you want your program to bomb out because it happened, this is the header file for you.

> 这个功能与永远不会发生的事情有关。如果你有一些永远不会变为真的事情，并且你希望你的程序崩溃因为它发生了，那么这个头文件就是你需要的。


There are two types of assertions: compile-time assertions (called "static assertions") and runtime assertions. If the assertion *fails* (i.e. the thing that you need to be true is not true) then the program will bomb out either at compile-time or runtime.

> 有两种断言：编译时断言（称为“静态断言”）和运行时断言。如果断言*失败*（即需要为真的事情不为真），那么程序将在编译时或运行时崩溃。

## [3.1]{.header-section-number} Macros {#macros number="3.1"}


If you define the macro `NDEBUG` **before** you include `<assert.h>`, then the `assert()` macro will have no effect. You can define `NDEBUG` to be anything, but `1` seems like a good value.

> 如果在包含<assert.h>之前定义宏NDEBUG，那么assert()宏将不起作用。您可以将NDEBUG定义为任何值，但1似乎是一个不错的值。


Since `assert()` causes your program to bomb out at runtime, you might not desire this behavior when you go into production. Defining `NDEBUG` causes `assert()` to be ignored.

> 由于`assert()`会导致程序在运行时崩溃，因此在上线时可能不希望这种行为发生。定义`NDEBUG`会导致`assert()`被忽略。

`NDEBUG` has no effect on `static_assert()`.

------------------------------------------------------------------------

## [3.2]{.header-section-number} `assert()` {#man-assert number="3.2"}

Bomb out at runtime if a condition fails

### Synopsis {#synopsis .unnumbered .unlisted}

::: {#cb57 .sourceCode}
``` {.sourceCode .c}
#include <assert.h>

void assert(scalar expression);
```
:::

### Description {#description .unnumbered .unlisted}


You pass in an expression to this macro. If it evaluates to false, the program will crash with an assertion failure (by calling the `abort()` function).

> 你向这个宏传递一个表达式。如果它的计算结果为假，程序将通过调用`abort()`函数而导致断言失败而崩溃。


Basically, you're saying, "Hey, I'm assuming this condition is true, and if it's not, I don't want to continue running."

> 基本上，你是在说：“嘿，我假设这个条件是正确的，如果不是，我不想继续运行了。”


This is used while debugging to make sure no unexpected conditions arise. And if you find during development that the condition does arise, maybe you should modify the code to handle it before going to production.

> 这是在调试时使用的，以确保不会出现意外情况。如果在开发过程中发现条件出现，也许你应该在上线前修改代码来处理它。


If you've defined the macro `NDEBUG` to any value before `<assert.h>` was included, the `assert()` macro is ignored. This is a good idea before production.

> 如果在包含<assert.h>之前定义了宏NDEBUG，那么assert()宏将被忽略。在生产之前，这是一个好主意。


Unlike `static_assert()`, this macro doesn't allow you to print an arbitrary message. If you want to do this, you can roll your own assert as a preprocessor macro:

> 与`static_assert()`不同，此宏不允许您打印任意消息。如果您想这样做，可以将自己的断言作为预处理器宏：

::: {#cb58 .sourceCode}
``` {.sourceCode .c}
#define ASSERT(c, m) \
do { \
    if (!(c)) { \
        fprintf(stderr, __FILE__ ":%d: assertion %s failed: %s\n", \
                        __LINE__, #c, m); \
        exit(1); \
    } \
} while(0)
```
:::

### Return Value {#return-value .unnumbered .unlisted}

This macro doesn't return (since it calls `abort()` which never returns).


If `NDEBUG` is set, the macro evaluates to `((void)0)`, which does nothing.

> 如果设置了`NDEBUG`，宏将被评估为`((void)0)`，这没有任何作用。

### Example {#example .unnumbered .unlisted}


Here's a function that divides the size of our goat herd. But we're assuming we'll never get a `0` passed to us.

> 这是一个可以分割我们山羊群大小的函数，但我们假设我们永远不会收到一个“0”。

So we assert that `amount != 0`... and if it is, the program aborts/

::: {#cb59 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
//#define NDEBUG 1   // uncomment this to disable the assert

#include <stdio.h>
#include <assert.h>

int goat_count = 10;

void divide_goat_herd_by(int amount)
{
    assert(amount != 0);

    goat_count /= amount;
}  

int main(void)
{
    divide_goat_herd_by(2);  // OK

    divide_goat_herd_by(0);  // Causes the assert to fire
}
```
:::


When I run this and pass `0` to the function, I get the following on my system (the exact output may vary):

> 当我运行这个并将`0`传递给函数时，我在我的系统上得到了以下结果（具体输出可能会有所不同）：

::: {#cb60 .sourceCode}
``` {.sourceCode .default}
assert: assert.c:10: divide_goat_herd_by: Assertion `amount != 0' failed.
```
:::

### See Also {#see-also .unnumbered .unlisted}


[`static_assert()`](assert.html#man-static_assert), [`abort()`](stdlib.html#man-abort)

> `static_assert()`：静态断言；`abort()`：中止。

------------------------------------------------------------------------

## [3.3]{.header-section-number} `static_assert()` {#man-static_assert number="3.3"}

Bomb out at compile-time if a condition fails

### Synopsis {#synopsis-1 .unnumbered .unlisted}

::: {#cb61 .sourceCode}
``` {.sourceCode .c}
#include <assert.h>

static_assert(constant-expression, string-literal);
```
:::

### Description {#description-1 .unnumbered .unlisted}


This macro prevents your program from even compiling if a condition isn't true.

> 这个宏可以防止你的程序在某个条件不满足时甚至无法编译。

And it prints the string literal you give it.


Basically if `constant-expression` is false, then compilation will cease and the `string-literal` will be printed.

> 如果`常量表达式`为假，编译将停止，并打印`字符串文字`。


The constant expression must be truly constant--just values, no variables. And the same is true for the string literal: no variables, just a literal string in double quotes. (It has to be this way since the program's not running at this point.)

> 常量表达式必须是真正的常量——只有值，没有变量。字符串文字也是一样：没有变量，只有双引号中的字面字符串。（由于程序此时还没有运行，所以必须是这样。）

### Return Value {#return-value-1 .unnumbered .unlisted}

Not applicable, as this is a compile-time feature.

### Example {#example-1 .unnumbered .unlisted}


Here's a partial example with an algorithm that presumably has poor performance or memory issues if the size of the local array is too large. We prevent that eventuality at compile-time by catching it with the `static_assert()`.

> 这里有一个部分示例，其中包含一种算法，如果本地数组的大小太大，可能会导致性能或内存问题。我们通过使用`static_assert()`在编译时捕获它，以防止这种可能性。

::: {#cb62 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <assert.h>

#define ARRAY_SIZE 16

int main(void)
{
    static_assert(ARRAY_SIZE > 32, "ARRAY_SIZE too small");

    int a[ARRAY_SIZE];

    a[32] = 10;

    printf("%d\n", a[32]);
}
```
:::


On my system, when I try to compile it, this prints (your output may vary):

> 在我的系统上，当我尝试编译它时，会打印出（您的输出可能会有所不同）：

::: {#cb63 .sourceCode}
``` {.sourceCode .default}
In file included from static_assert.c:2:
static_assert.c: In function ‘main’:
static_assert.c:8:5: error: static assertion failed: "ARRAY_SIZE too small"
    8 |     static_assert(ARRAY_SIZE > 32, "ARRAY_SIZE too small");
      |     ^~~~~~~~~~~~~
```
:::

### See Also {#see-also-1 .unnumbered .unlisted}

[`assert()`](assert.html#man-assert)

------------------------------------------------------------------------

::: {style="text-align:center"}

[Prev](the-c-language.html) \| [Contents](index.html) \| [Next](complex.html)

> [上一页](the-c-language.html) | [目录](index.html) | [下一页](complex.html)
:::
