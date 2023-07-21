---
tip: translate by openai@2023-07-20 19:04:57
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](math.html) \| [Contents](index.html) \| [Next](signal.html)
:::

------------------------------------------------------------------------

# [14]{.header-section-number} `<setjmp.h>` Non-local Goto {#setjmp number="14"}


These functions enable you to rewind the call stack to an earlier point, with a bunch of gotchas. It is rarely used.

> 这些功能可以让你将调用堆栈倒回到较早的点，但有许多坑。它很少被使用。

  Function      Description
  ------------- ------------------------------------------
  `longjmp()`   Return to the previously-placed bookmark
  `setjmp()`    Bookmark this place to return to later


There's also a new opaque type, `jmp_buf`, that holds all the information needed to pull off this magic trick.

> 还有一种新的不透明类型`jmp_buf`，它保存了所有完成这个魔术技巧所需的信息。


If you want your automatic local variables to be correct after a call to `longjmp()`. declare them as `volatile` where you called `setjmp()`.

> 如果你想要在调用`longjmp()`之后自动局部变量正确，在调用`setjmp()`的地方声明它们为`volatile`。

------------------------------------------------------------------------

## [14.1]{.header-section-number} `setjmp()` {#man-setjmp number="14.1"}

Save this location as one to return to later

### Synopsis {#synopsis-112 .unnumbered .unlisted}

::: {#cb386 .sourceCode}
``` {.sourceCode .c}
#include <setjmp.h>

int setjmp(jmp_buf env);
```
:::

### Description {#description-112 .unnumbered .unlisted}


This is how you save your position so you can `longjmp()` back it, later. Think of it as setting up a warp destination for later use.

> 这就是你如何保存你的位置，以便稍后可以使用`longjmp()`回到它。把它想象成为为以后使用设置一个传送目的地。


Basically, you call this, giving it an `env` it can fill in with all the information it needs to come back here later. This `env` is one you'll pass to `longjmp()` later when you want to teleport back here.

> 基本上，你给它一个`env`，它可以用所有需要回到这里的信息填充它。当你想瞬移回来时，你会把这个`env`传给`longjmp()`。

And the really funky part is this can return two different ways:


1.  It can return `0` from the call where you set up the jump destination.

> 它可以从设置跳转目标的调用中返回`0`。


2.  If can return non-zero when you actually warp back here as the result of a call to `longjmp()`.

> 如果你通过调用longjmp()回到这里，可以返回非零值。

What you can do is check the return value to see which case has occurred.


You're only allowed to call `setjmp()` in a limited number of circumstances.

> 你只能在有限的情况下调用`setjmp()`。

1.  As a standalone expression:

    ::: {#cb387 .sourceCode}
    ``` {.sourceCode .c}
    setjmp(env);
    ```
    :::

    You can also cast it to `(void)` if you really wanted to do such a thing.

2.  As the complete controlling expression in an `if` or `switch`.

    ::: {#cb388 .sourceCode}
    ``` {.sourceCode .c}
    if (setjmp(env)) { ... }

    switch (setjmp(env)) { ... }
    ```
    :::

    But not this as it's not the complete controlling expression in this case:

    ::: {#cb389 .sourceCode}
    ``` {.sourceCode .c}
    if (x == 2 && setjmp()) { ... }   // Undefined behavior
    ```
    :::


3.  The same as (2), above, except with a comparison to an integer constant:

> 3. 与上面（2）相同，但与整数常量进行比较。

    ::: {#cb390 .sourceCode}
    ``` {.sourceCode .c}
    if (setjmp(env) == 0) { ... }

    if (setjmp(env) > 2) { ... }
    ```
    :::

4.  As the operand to the not (`!`) operator:

    ::: {#cb391 .sourceCode}
    ``` {.sourceCode .c}
    if (!setjmp(env)) { ... }
    ```
    :::

Anything else is (you guessed it) undefined behavior!


This can be a macro or a function, but you'll treat it the same way in any case.

> 无论如何，你都要以相同的方式处理它，它可以是宏，也可以是函数。

### Return Value {#return-value-111 .unnumbered .unlisted}

This one is funky. It returns one of two things:

Returns `0` if this was the call to `setjmp()` to set it up.


Returns non-zero if being here was the result of a call to `longjmp()`. (Namely, it returns the value passed into the `longjmp()` function.)

> 返回非零值，如果此处是`longjmp()`调用的结果。（也就是说，它返回传递给`longjmp()`函数的值。）

### Example {#example-112 .unnumbered .unlisted}


Here's a function that calls `setjmp()` to set things up (where it returns `0`), then calls a couple levels deep into functions, and finally short-circuits the return path by `longjmp()`ing back to the place where `setjmp()` was called, earlier. This time, it passes `3490` as a value, which `setjmp()` returns.

> 这里有一个函数，它调用`setjmp()`来设置（返回`0`），然后调用几个层次的函数，最后通过`longjmp()`回到之前调用`setjmp()`的位置。这次，它传递的值是`3490`，`setjmp()`返回这个值。

::: {#cb392 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <setjmp.h>

jmp_buf env;

void depth2(void)
{
    printf("Entering depth 2\n");
    longjmp(env, 3490);           // Jump back to setjmp()!!
    printf("Leaving depth 2\n");  // This won't happen
}

void depth1(void)
{
    printf("Entering depth 1\n");
    depth2();
    printf("Leaving depth 1\n");  // This won't happen
}

int main(void)
{
    switch (setjmp(env)) {
        case 0:
            printf("Calling into functions, setjmp() returned 0\n");
            depth1();
            printf("Returned from functions\n");  // This won't happen
            break;

        case 3490:
            printf("Bailed back to main, setjmp() returned 3490\n");
            break;
    }
}
```
:::

When run, this outputs:

::: {#cb393 .sourceCode}
``` {.sourceCode .default}
Calling into functions, setjmp() returned 0
Entering depth 1
Entering depth 2
Bailed back to main, setjmp() returned 3490
```
:::


Notice that the second `printf()` in `case 0` didn't run; it got jumped over by `longjmp()`!

> 注意，在case 0中的第二个printf（）没有运行；它被longjmp（）跳过了！

### See Also {#see-also-105 .unnumbered .unlisted}

[`longjmp()`](setjmp.html#man-longjmp)

------------------------------------------------------------------------

## [14.2]{.header-section-number} `longjmp()` {#man-longjmp number="14.2"}

Return to the previous `setjmp()` location

### Synopsis {#synopsis-113 .unnumbered .unlisted}

::: {#cb394 .sourceCode}
``` {.sourceCode .c}
 #include <setjmp.h>

_Noreturn void longjmp(jmp_buf env, int val);
```
:::

### Description {#description-113 .unnumbered .unlisted}


This returns to a previous call to `setjmp()` back in the call history. `setjmp()` will return the `val` passed into `longjmp()`.

> 这将返回到调用历史中之前对`setjmp()`的调用。`setjmp()`将返回传入`longjmp()`的`val`。


The `env` passed to `setjmp()` should be the same one you pass into `longjmp()`.

> 传递给`setjmp()`的`env`应该是和你传递给`longjmp()`的相同的。


There are a bunch of potential issues with doing this, so you'll want to be careful that you avoid undefined behavior by not doing the following:

> 这样做可能会有很多问题，所以你要小心，避免未定义的行为，不要做以下事情：


1.  Don't call `longjmp()` if the corresponding `setjmp()` was in a different thread.

> 不要在不同的线程中调用`longjmp()`如果对应的`setjmp()`已经被调用了。

2.  Don't call `longjmp()` if you didn't call `setjmp()` first.


3.  Don't call `longjmp()` if the function that called `setjmp()` has completed.

> 不要在调用了`setjmp()`的函数已经完成后再调用`longjmp()`。


4.  Don't call `longjmp()` if the call to `setjmp()` had a variable length array (VLA) in scope and the scope has ended.

> 不要在变长数组（VLA）的作用域已经结束的情况下调用`longjmp()`函数。


5.  Don't call `longjmp()` if there are any VLAs in any active scopes between the `setjmp()` and the `longjmp()`. A good rule of thumb here is to not mix VLAs and `longjmp()`.

> 不要在setjmp()和longjmp()之间调用longjmp()，如果有任何活动作用域中的VLAs。这里有一个很好的经验法则：不要混合VLAs和longjmp()。


Though `longjmp()` attempts to restore the machine to the state at the `setjmp()`, including local variables, there are some things that aren't brought back to life:

> 尽管`longjmp()`试图恢复机器到`setjmp()`时的状态，包括局部变量，但有一些东西无法恢复生机：

-   Non-volatile local variables that might have changed
-   Floating point status flags
-   Open files
-   Any other component of the abstract machine

### Return Value {#return-value-112 .unnumbered .unlisted}


This one is also funky in that it is one of the few functions in C that never returns!

> 这个也很有趣，因为它是C中少数从不返回的函数之一！

### Example {#example-113 .unnumbered .unlisted}


Here's a function that calls `setjmp()` to set things up (where it returns `0`), then calls a couple levels deep into functions, and finally short-circuits the return path by `longjmp()`ing back to the place where `setjmp()` was called, earlier. This time, it passes `3490` as a value, which `setjmp()` returns.

> 这里有一个函数，它调用`setjmp()`来设置事情（返回`0`），然后调用几个深层次的函数，最后通过`longjmp()`回到`setjmp()`被调用的地方，传递`3490`作为一个值，`setjmp()`返回。

::: {#cb395 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <setjmp.h>

jmp_buf env;

void depth2(void)
{
    printf("Entering depth 2\n");
    longjmp(env, 3490);           // Jump back to setjmp()!!
    printf("Leaving depth 2\n");  // This won't happen
}

void depth1(void)
{
    printf("Entering depth 1\n");
    depth2();
    printf("Leaving depth 1\n");  // This won't happen
}

int main(void)
{
    switch (setjmp(env)) {
        case 0:
            printf("Calling into functions, setjmp() returned 0\n");
            depth1();
            printf("Returned from functions\n");  // This won't happen
            break;

        case 3490:
            printf("Bailed back to main, setjmp() returned 3490\n");
            break;
    }
}
```
:::

When run, this outputs:

::: {#cb396 .sourceCode}
``` {.sourceCode .default}
Calling into functions, setjmp() returned 0
Entering depth 1
Entering depth 2
Bailed back to main, setjmp() returned 3490
```
:::


Notice that the second `printf()` in `case 0` didn't run; it got jumped over by `longjmp()`!

> 注意，`case 0`中的第二个`printf()`没有运行；它被`longjmp()`跳过了！

### See Also {#see-also-106 .unnumbered .unlisted}

[`setjmp()`](setjmp.html#man-setjmp)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](math.html) \| [Contents](index.html) \| [Next](signal.html)
:::
