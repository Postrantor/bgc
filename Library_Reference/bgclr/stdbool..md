---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdatomic.html) \| [Contents](index.html) \| [Next](stddef.html)
:::

------------------------------------------------------------------------

# [19]{.header-section-number} `<stdbool.h>` Boolean Types {#stdbool number="19"}

This is a small header file that defines a number of convenient Boolean macros. If you really need that kind of thing.

  ----------------------------------------------------------------------
  Macro       Description
  ----------- ----------------------------------------------------------
  `bool`      Type for Boolean, expands to `_Bool`

  `true`      True value, expands to `1`

  `false`     False value, expands to `0`
  ----------------------------------------------------------------------

There's one more macro that I'm not putting in the table because it's such a long name it'll blow up the table alignment:

::: {#cb470 .sourceCode}
``` {.sourceCode .c}
__bool_true_false_are_defined
```
:::

which expands to `1`.

## [19.1]{.header-section-number} Example {#example-135 number="19.1"}

Here's a lame example that shows off these macros.

::: {#cb471 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdbool.h>

int main(void)
{
    bool x;

    x = (3 > 2);

    if (x == true)
        printf("The universe still makes sense.\n");

    x = false;

    printf("x is now %d\n", x);  // 0
}
```
:::

Output:

::: {#cb472 .sourceCode}
``` {.sourceCode .default}
The universe still makes sense.
x is now 0
```
:::

## [19.2]{.header-section-number} `_Bool`? {#bool number="19.2"}

What's the deal with `_Bool`? Why didn't they just make it `bool`?

Well, there was a lot of C code out there where people had defined their own `bool` type and adding an official `bool` would have broken those `typedef`s.

But C has already reserved all identifiers that start with an underscore followed by a capital letter, so it was clear to make up a new `_Bool` type and go with that.

And, if you know your code can handle it, you can include this header to get all this juicy syntax.

One more note on conversions: unlike converting to `int`, the *only* thing that converts to `false` in a `_Bool` is a scalar zero value. Anything at all that's not zero, like `-3490`, `0.12`, or `NaN`, converts to `true`.

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdatomic.html) \| [Contents](index.html) \| [Next](stddef.html)
:::
