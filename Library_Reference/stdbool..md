---
tip: translate by openai@2023-07-20 19:23:54
...
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

> 这是一个定义了许多方便布尔宏的小头文件。如果你真的需要这种东西。

  ----------------------------------------------------------------------
  Macro       Description
  ----------- ----------------------------------------------------------
  `bool`      Type for Boolean, expands to `_Bool`

  `true`      True value, expands to `1`

  `false`     False value, expands to `0`
  ----------------------------------------------------------------------


There's one more macro that I'm not putting in the table because it's such a long name it'll blow up the table alignment:

> 我没有把它放到表格里，因为它的名字太长了，会打乱表格对齐：

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

> 嗯，当时有很多C代码，人们定义了自己的`bool`类型，如果添加官方的`bool`类型，就会破坏这些`typedef`。


But C has already reserved all identifiers that start with an underscore followed by a capital letter, so it was clear to make up a new `_Bool` type and go with that.

> 但C已经预留了所有以下划线开头后跟大写字母的标识符，因此创建一个新的`_Bool`类型并采用它是很明显的。


And, if you know your code can handle it, you can include this header to get all this juicy syntax.

> 如果你知道你的代码能够处理它，你可以包含这个头文件来获取所有这些丰富的语法。


One more note on conversions: unlike converting to `int`, the *only* thing that converts to `false` in a `_Bool` is a scalar zero value. Anything at all that's not zero, like `-3490`, `0.12`, or `NaN`, converts to `true`.

> 关于转换的另一个注意事项：与转换为`int`不同，`_Bool`中唯一转换为`false`的是标量零值。除零以外的任何值，如`-3490`、`0.12`或`NaN`，都会转换为`true`。

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdatomic.html) \| [Contents](index.html) \| [Next](stddef.html)
:::
