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

Use this macro to indicate to the compiler that a function will never return to the caller. It's undefined behavior if the so-marked function does return.

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
