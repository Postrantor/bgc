---
tip: translate by openai@2023-07-20 19:11:47
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdalign.html) \| [Contents](index.html) \| [Next](stdatomic.html)
:::

------------------------------------------------------------------------

# [17]{.header-section-number} `<stdarg.h>` Variable Arguments {#stdarg number="17"}


  ---------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------
无论如何，我们都要努力前行。
  Macro                                      Description

  ------------------------------------------ --------------------------------------------------------------

> ------------------------------------------ --------------------------------------------------------------
简体中文：
------------------------------------------ --------------------------------------------------------------

  [`va_arg()`](stdarg.html#man-va_arg)       Get the next variable argument

> `va_arg()`（stdarg.html#man-va_arg）获取下一个可变参数


  [`va_copy()`](stdarg.html#man-va_copy)     Copy a `va_list` and the work done so far

> va_copy()（stdarg.html#man-va_copy）复制va_list及其之前完成的工作。


  [`va_end()`](stdarg.html#man-va_end)       Signify we're done processing variable arguments

> va_end()：表明我们已经处理完可变参数。


  [`va_start()`](stdarg.html#man-va_start)   Initialize a `va_list` to start variable argument processing

> `va_start()`（stdarg.html#man-va_start）初始化一个`va_list`以开始变量参数处理

  ---------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------
简化中文


This header file is what allows you to write functions that take a variable number of arguments.

> 这个头文件允许你编写可以接受可变数量参数的函数。


In addition to the macros, you get a new type that helps C keep track of where it is in the variable-number-of-arguments-processing: `va_list`. This type is opaque, and you'll be passing it around to the various macros to help get at the arguments.

> 除了宏，您还可以获得一种新类型，它可以帮助C跟踪它在可变参数处理中的位置：`va_list`。这种类型是不透明的，您将把它传递给各种宏，以帮助获取参数。


Note that every variadic function requires at least one non-variable parameter. You need this to kick off processing with `va_start()`.

> 注意，每个变参函数至少需要一个非变参数。您需要使用`va_start（）`来启动处理。

------------------------------------------------------------------------

## [17.1]{.header-section-number} `va_arg()` {#man-va_arg number="17.1"}

Get the next variable argument

### Synopsis {#synopsis-118 .unnumbered .unlisted}

::: {#cb421 .sourceCode}
``` {.sourceCode .c}
#include <stdarg.h>

type va_arg(va_list ap, type);
```
:::

### Description {#description-118 .unnumbered .unlisted}


If you have a variable argument list you've initialized with `va_start()`, pass it to this one along with the type of argument you're trying to get, e.g.

> 如果你已经使用`va_start()`初始化了一个可变参数列表，请把它传递给这个函数，同时也传递你想要获取的参数类型，例如。

::: {#cb422 .sourceCode}
``` {.sourceCode .c}
int   x = va_arg(args, int);
float y = va_arg(args, float);
```
:::

### Return Value {#return-value-116 .unnumbered .unlisted}

Evaluates to the value and type of the next variable argument.

### Example {#example-118 .unnumbered .unlisted}


Here's a demo that adds together an arbitrary number of integers. The first argument is the number of integers to add together. We'll make use of that to figure out how many times we have to call `va_arg()`.

> 这里有一个演示，它可以把任意数量的整数相加。第一个参数是要相加的整数的数量。我们将利用它来弄清楚我们要调用多少次`va_arg()`。

::: {#cb423 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdarg.h>

int add(int count, ...)
{
    int total = 0;
    va_list va;

    va_start(va, count);   // Start with arguments after "count"

    for (int i = 0; i < count; i++) {
        int n = va_arg(va, int);   // Get the next int

        total += n;
    }

    va_end(va);  // All done

    return total;
}

int main(void)
{
    printf("%d\n", add(4, 6, 2, -4, 17));  // 6 + 2 - 4 + 17 = 21
    printf("%d\n", add(2, 22, 44));        // 22 + 44 = 66
}
```
:::

### See Also {#see-also-111 .unnumbered .unlisted}


[`va_start()`](stdarg.html#man-va_start), [`va_end()`](stdarg.html#man-va_end)

> `va_start()`：开始使用变参
`va_end()`：结束使用变参

------------------------------------------------------------------------

## [17.2]{.header-section-number} `va_copy()` {#man-va_copy number="17.2"}

Copy a `va_list` and the work done so far

### Synopsis {#synopsis-119 .unnumbered .unlisted}

::: {#cb424 .sourceCode}
``` {.sourceCode .c}
#include <stdarg.h>

void va_copy(va_list dest, va_list src);
```
:::

### Description {#description-119 .unnumbered .unlisted}


The main intended use of this is to save your state partway through processing variable arguments so you can scan ahead and then rewind back to the save point.

> 这个的主要用途是在处理可变参数的过程中保存状态，以便您可以提前扫描，然后回到保存点。

You pass in a `src` `va_list` and it copies it to `dest`.


If you've already called this once for a particular `dest`, you can't call it (or `va_start()`) again with the same `dest` unless you call `va_end()` on that `dest` first.

> 如果你已经为特定的'dest'调用了一次，除非先调用'dest'上的'va_end()'，否则你不能再次使用相同的'dest'调用它（或'va_start()'）。

::: {#cb425 .sourceCode}
``` {.sourceCode .c}
va_copy(dest, src);
va_copy(dest, src2);  // BAD!

va_copy(dest, src);
va_start(dest, var);  // BAD!

va_copy(dest, src);
va_end(dest);
va_copy(dest, src2);  // OK!

va_copy(dest, src);
va_end(dest);
va_start(dest, var);  // OK!
```
:::

### Return Value {#return-value-117 .unnumbered .unlisted}

Returns nothing.

### Example {#example-119 .unnumbered .unlisted}


Here's an example where we're adding together all the variable arguments, but then we want to go back and add on all the numbers past the first two, for example if the arguments are:

> 例如，我们把所有可变参数加起来，但是我们想回头再加上第一个和第二个之后的所有数字，例如，如果参数是：

::: {#cb426 .sourceCode}
``` {.sourceCode .default}
10 20 30 40
```
:::


First we add them all for `100`, and then we add on everything from the third number on, so add on `30+40` for a total of `170`.

> 首先我们把它们全部加起来为100，然后从第三个数字开始，我们再加上30+40，总计170。


We'll do this by saving our place in the variable argument processing with `va_copy` and then using that later to reprocess the trailing arguments.

> 我们将通过使用`va_copy`保存变量参数处理中的位置，然后稍后使用它来重新处理尾随参数来完成这一点。


(And yes, I know there's a mathematical way to do this without all the rewinding, but I'm having an heck of a time coming up with a good example!)

> （而且我知道有一种数学方法可以在不重复的情况下完成这件事，但我很难找到一个好的例子！）

::: {#cb427 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdarg.h>

// Add all the numbers together, but then add on all the numbers
// past the second one again.
int contrived_adder(int count, ...)
{
    if (count < 3) return 0; // OK, I'm being lazy. You got me.

    int total = 0;

    va_list args, mid_args;

    va_start(args, count);

    for (int i = 0; i < count; i++) {

        // If we're at the second number, save our place in
        // mid_args:

        if (i == 2)
            va_copy(mid_args, args);

        total += va_arg(args, int);
    }

    va_end(args); // Done with this

    // But now let's start with mid_args and add all those on:
    for (int i = 0; i < count - 2; i++)
        total += va_arg(mid_args, int);

    va_end(mid_args); // Done with this, too

    return total;
}

int main(void)
{
    // 10+20+30 + 30 == 90
    printf("%d\n", contrived_adder(3, 10, 20, 30));

    // 10+20+30+40+50 + 30+40+50 == 270
    printf("%d\n", contrived_adder(5, 10, 20, 30, 40, 50));
}
```
:::

### See Also {#see-also-112 .unnumbered .unlisted}


[`va_start()`](stdarg.html#man-va_start), [`va_arg()`](stdarg.html#man-va_arg), [`va_end()`](stdarg.html#man-va_end)

> `va_start()`：开始使用可变参数
`va_arg()`：获取可变参数
`va_end()`：结束使用可变参数

------------------------------------------------------------------------

## [17.3]{.header-section-number} `va_end()` {#man-va_end number="17.3"}

Signify we're done processing variable arguments

### Synopsis {#synopsis-120 .unnumbered .unlisted}

::: {#cb428 .sourceCode}
``` {.sourceCode .c}
#include <stdarg.h>

void va_end(va_list ap);
```
:::

### Description {#description-120 .unnumbered .unlisted}


After you've `va_start()`ed or `va_copy`'d a new `va_list`, you **must** call `va_end()` with it before it goes out of scope.

> 在你使用`va_start()`或`va_copy`创建一个新的`va_list`之后，在它的作用域结束之前，你必须调用`va_end()`来释放它。


You also have to do this if you're going to call `va_start()` or `va_copy()` *again* on a variable you've already done that to.

> 如果你要再次对已经使用过`va_start()`或`va_copy()`的变量使用这些函数，你也必须这样做。

Them's the rules if you want to avoid undefined behavior.


But just think of it as cleanup. You called `va_start()`, so you'll call `va_end()` when you're done.

> 想想这只是清理工作。你调用了`va_start()`，所以当你完成时，你会调用`va_end()`。

### Return Value {#return-value-118 .unnumbered .unlisted}

Returns nothing.

### Example {#example-120 .unnumbered .unlisted}


Here's a demo that adds together an arbitrary number of integers. The first argument is the number of integers to add together. We'll make use of that to figure out how many times we have to call `va_arg()`.

> 这里有一个演示，它可以将任意数量的整数相加。第一个参数是要相加的整数的数量。我们将利用它来确定我们要调用多少次`va_arg()`。

::: {#cb429 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdarg.h>

int add(int count, ...)
{
    int total = 0;
    va_list va;

    va_start(va, count);   // Start with arguments after "count"

    for (int i = 0; i < count; i++) {
        int n = va_arg(va, int);   // Get the next int

        total += n;
    }

    va_end(va);  // All done

    return total;
}

int main(void)
{
    printf("%d\n", add(4, 6, 2, -4, 17));  // 6 + 2 - 4 + 17 = 21
    printf("%d\n", add(2, 22, 44));        // 22 + 44 = 66
}
```
:::

### See Also {#see-also-113 .unnumbered .unlisted}


[`va_start()`](stdarg.html#man-va_start), [`va_copy()`](stdarg.html#man-va_copy)

> `va_start()`：开始使用可变参数列表
`va_copy()`：复制可变参数列表

------------------------------------------------------------------------

## [17.4]{.header-section-number} `va_start()` {#man-va_start number="17.4"}

Initialize a `va_list` to start variable argument processing

### Synopsis {#synopsis-121 .unnumbered .unlisted}

::: {#cb430 .sourceCode}
``` {.sourceCode .c}
#include <stdarg.h>

void va_start(va_list ap, parmN);
```
:::

### Description {#description-121 .unnumbered .unlisted}


You've declared a variable of type `va_list` to keep track of the variable argument processing... now how to initialize it so you can start calling `va_arg()` to get those arguments?

> 你声明了一个类型为`va_list`的变量来跟踪可变参数处理...现在如何初始化它，以便你可以开始调用`va_arg()`来获取这些参数？

`va_start()` to the rescue!


What you do is pass in your `va_list`, here shown as parameter `ap`. Just pass the list, not a pointer to it.

> 你要做的就是传入你的`va_list`，这里以参数`ap`表示。只要传入这个列表，而不是它的指针。


Then for the second argument to `va_start()`, you give the name of the parameter that you want to start processing arguments *after*. This must be the parameter right before the `...` in the argument list.

> 然后，对于`va_start()`的第二个参数，你提供想要从哪个参数开始处理参数的参数名称。这必须是参数列表中`...`之前的参数。


If you've already called `va_start()` on a particular `va_list` and you want to call `va_start()` on it again, you **must** call `va_end()` first!

> 如果你已经在某个特定的va_list上调用了va_start()，而你又想再次调用它，你必须先调用va_end()！

### Return Value {#return-value-119 .unnumbered .unlisted}

Returns nothing!

### Example {#example-121 .unnumbered .unlisted}


Here's a demo that adds together an arbitrary number of integers. The first argument is the number of integers to add together. We'll make use of that to figure out how many times we have to call `va_arg()`.

> 这里有一个演示，它可以将任意数量的整数相加。第一个参数是要相加的整数的数量。我们将利用它来弄清楚我们要调用多少次`va_arg()`。

::: {#cb431 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdarg.h>

int add(int count, ...)
{
    int total = 0;
    va_list va;

    va_start(va, count);   // Start with arguments after "count"

    for (int i = 0; i < count; i++) {
        int n = va_arg(va, int);   // Get the next int

        total += n;
    }

    va_end(va);  // All done

    return total;
}

int main(void)
{
    printf("%d\n", add(4, 6, 2, -4, 17));  // 6 + 2 - 4 + 17 = 21
    printf("%d\n", add(2, 22, 44));        // 22 + 44 = 66
}
```
:::

### See Also {#see-also-114 .unnumbered .unlisted}


[`va_arg()`](stdarg.html#man-va_arg), [`va_end()`](stdarg.html#man-va_end)

> `va_arg()`：取可变参数列表的下一个参数
`va_end()`：结束可变参数列表的使用

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdalign.html) \| [Contents](index.html) \| [Next](stdatomic.html)
:::
