---
tip: translate by openai@2023-07-21 12:48:09
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdlib.html) \| [Contents](index.html) \| [Next](stringref.html)
:::

------------------------------------------------------------------------

# [24]{.header-section-number} `<stdnoreturn.h>` Macros for Non-Returning Functions {#stdnoreturn number="24"}


This header provides a macro `noreturn` that is a handy alias for `_Noreturn`.

> 这个头文件提供了一个宏`noreturn`，它是`_Noreturn`的一个方便的别名。


Use this macro to indicate to the compiler that a function will never return to the caller. It's undefined behavior if the so-marked function does return.

> 使用此宏向编译器表明函数永远不会返回调用者。如果标记为此的函数返回，则行为是未定义的。

Here's a usage example:

::: {#cb645 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <stdnoreturn.h>

noreturn void foo(void) // This function should never return!
{
    printf("Happy days\n");

    exit(1);            // And it doesn't return--it exits here!
}

int main(void)
{
    foo();
}
```
:::

That's all there is to it.

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdlib.html) \| [Contents](index.html) \| [Next](stringref.html)
:::
