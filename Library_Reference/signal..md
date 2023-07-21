---
tip: translate by openai@2023-07-20 19:07:18
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](setjmp.html) \| [Contents](index.html) \| [Next](stdalign.html)
:::

------------------------------------------------------------------------

# [15]{.header-section-number} `<signal.h>` signal handling {#signal number="15"}

  Function                               Description
  -------------------------------------- -----------------------------------------

  [`signal()`](signal.html#man-signal)   Set a signal handler for a given signal

> 设置给定信号的信号处理程序
  [`raise()`](signal.html#man-raise)     Cause a signal to be raised

Handle signals in a portable way, kind of!


These signals get raised for a variety of reasons such as CTRL-C being hit, requests to terminate for external programs, memory access violations, and so on.

> 这些信号会由于多种原因而被触发，比如按下CTRL-C、外部程序的终止请求、内存访问违规等等。

Your OS likely defines a plethora of other signals, as well.


This system is pretty limited, as seen below. If you're on Unix, it's almost certain your OS has far superior signal handling capabilities than the C standard library. Check out [`sigaction`](https://man.archlinux.org/man/sigaction.2.en)[^35^](footnotes.html#fn35){#fnref35 .footnote-ref role="doc-noteref"}.

> 这个系统非常有限，如下所示。如果你使用Unix，你的操作系统信号处理能力几乎肯定比C标准库更强大。请查看[`sigaction`](https://man.archlinux.org/man/sigaction.2.en)[^35^](footnotes.html#fn35){#fnref35 .footnote-ref role="doc-noteref"}。

------------------------------------------------------------------------

## [15.1]{.header-section-number} `signal()` {#man-signal number="15.1"}

Set a signal handler for a given signal

### Synopsis {#synopsis-114 .unnumbered .unlisted}

::: {#cb397 .sourceCode}
``` {.sourceCode .c}
#include <signal.h>

void (*signal(int sig, void (*func)(int)))(int);
```
:::

### Description {#description-114 .unnumbered .unlisted}

How's *that* for a function declaration?

Let's ignore it for a moment and just talk about what this function does.


When a signal is raised, *something* is going to happen. This function lets you decide to do one of these things when the signal is raised:

> 当信号被触发时，*某事* 将会发生。此函数可以让您在信号被触发时决定做这些事情之一：

-   Ignore the signal
-   Perform the default action
-   Have a specific function called


The `signal()` function takes two arguments. The first, `sig`, is the name of the signal to handle.

> 信号（`signal()`）函数接受两个参数。第一个参数`sig`是要处理的信号的名称。

  Signal      Description

  ----------- -------------------------------------------------------------------------------------------

> ----------- -------------------------------------------------------------------------------------------
没有可翻译的内容
  `SIGABRT`   Raised when `abort()` is called
  `SIGFPE`    Floating-point arithmetic exception
  `SIGILL`    CPU tried to execute an illegal instruction
  `SIGINT`    Interrupt signal, as if `CTRL-C` were pressed
  `SIGSEGV`   Segmention Violation: attempted to access restricted memory

  `SIGTERM`   Termination request[^36^](footnotes.html#fn36){#fnref36 .footnote-ref role="doc-noteref"}

> `SIGTERM`：终止请求[^36^](footnotes.html#fn36){#fnref36 .footnote-ref role="doc-noteref"}


So that's the first bit when you call `signal()`---tell it the signal in question:

> 当你调用`signal()`时，这是第一步---告诉它有关的信号：

::: {#cb398 .sourceCode}
``` {.sourceCode .c}
signal(SIGINT, ...
```
:::

But what's that `func` parameter?


For spoilers, it's a pointer to a function that takes an `int` argument and returns `void`. We can use this to call an arbitrary function when the signal occurs.

> 对于剧透，它是一个指向接受一个`int`参数并返回`void`的函数的指针。当信号发生时，我们可以使用它来调用任意函数。


Before we do that, though, let's look at the easy ones: telling the system to ignore the signal or perform the default action (which it does by default if you never call `signal()`).

> 在做那件事之前，让我们先看看简单的：告诉系统忽略信号或执行默认操作（如果您从不调用`signal()`，它会默认执行）。

You can set `func` to one of two special values to make this happen:

  `func`      Description
  ----------- -------------------------------------------
  `SIG_DFL`   Perform the default action on this signal
  `SIG_IGN`   Ignore this signal

For example:

::: {#cb399 .sourceCode}
``` {.sourceCode .c}
signal(SIGTERM, SIG_DFL);  // Default action on SIGTERM
signal(SIGINT, SIG_IGN);   // Ignore SIGINT
```
:::


But what if you want to have your own handler do something instead of the default or ignoring it? You can pass in your own function to be called. That's what the crazy function signature is partially about. It's saying that the argument can be a pointer to a function that takes an `int` argument and returns `void`.

> 如果你想让你自己的处理程序做一些事情而不是使用默认的或忽略它，你可以传入你自己的函数来调用。这就是疯狂的函数签名部分的意思。它表明这个参数可以是一个指向接受一个`int`参数并返回`void`的函数的指针。

So if you wanted to call your handler, you could have code like this:

::: {#cb400 .sourceCode}
``` {.sourceCode .c}
int handler(int sig)
{
    // Handle the signal
}

int main(void)
{
    signal(SIGINT, handler);
```
:::

What can you do in the signal handler? Not much.


If the signal is due to `abort()` or `raise()`, the handler can't call `raise()`.

> 如果信号是由`abort()`或`raise()`引起的，处理程序不能调用`raise()`。


If the signal is **not** due to `abort()` or `raise()`, you're only allowed to call these functions from the standard library (though the spec doesn't prohibit calling other non-library functions):

> 如果信号不是由`abort()`或`raise()`引起的，你只能从标准库调用这些函数（尽管规范不禁止调用其他非库函数）：

-   [`abort()`](stdlib.html#man-abort)
-   [`_Exit()`](stdlib.html#man-exit)
-   [`quick_exit()`](stdlib.html#man-exit)

-   Functions in [`<stdatomic.h>`](stdatomic.html#stdatomic) when the atomic arguments are lock-free

> 函数在[`<stdatomic.h>`](stdatomic.html#stdatomic)中，当原子参数是无锁的时候
-   `signal()` with a first argument equivalent to the argument that was passed into the handler


In addition, if the signal was **not** due to `abort()` or `raise()`, the handler can't access any object with static or thread-storage duration unless it's lock-free.

> 此外，如果信号不是由`abort()`或`raise()`引起的，处理程序无法访问任何具有静态或线程存储持续时间的对象，除非它是无锁的。


An exception is that you can assign to (but not read from!) a variable of type `volatile sig_atomic_t`.

> 例外情况是，你可以给类型为`volatile sig_atomic_t`的变量赋值（但不能读取！）。


It's up to the implementation, but the signal handler might be reset to `SIG_DFL` just before the handler is called.

> 这取决于实现，但在调用处理程序之前可能会将信号处理程序重置为`SIG_DFL`。

It's undefined behavior to call `signal()` in a multithreaded program.


It's undefined behavior to return from the handler for `SIGFPE`, `SIGILL`, `SIGSEGV`, or any implementation-defined value. You must exit.

> 返回`SIGFPE`、`SIGILL`、`SIGSEGV`或任何实现定义的值的处理程序是未定义的行为，您必须退出。


The implementation might or might not prevent other signals from arising while in the signal handler.

> 实施可能会或可能不会阻止在信号处理程序中出现其他信号。

### Return Value {#return-value-113 .unnumbered .unlisted}


On success, `signal()` returns a pointer to the previous signal handler set by a call to `signal()` for that particular signal number. If you haven't called it set, returns `SIG_DFL`.

> 如果成功，`signal()`函数会返回之前由`signal()`调用设置的特定信号号的信号处理程序的指针。如果没有调用它，则返回`SIG_DFL`。

On failure, `SIG_ERR` is returned and `errno` is set to a positive value.

### Example {#example-114 .unnumbered .unlisted}


Here's a program that causes `SIGINT` to be ignored. Commonly you trigger this signal by hitting `CTRL-C`.

> 这是一个忽略`SIGINT`的程序。通常，您可以通过按`CTRL-C`来触发此信号。

::: {#cb401 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <signal.h>

int main(void)
{
    signal(SIGINT, SIG_IGN);

    printf("You can't hit CTRL-C to exit this program. Try it!\n\n");
    printf("Press return to exit, instead.");
    fflush(stdout);
    getchar();
}
```
:::

Output:

::: {#cb402 .sourceCode}
``` {.sourceCode .default}
You can't hit CTRL-C to exit this program. Try it!

Press return to exit, instead.^C^C^C^C^C^C^C^C^C^C^C
```
:::


This program sets the signal handler, then raises the signal. The signal handler fires.

> 这个程序设置信号处理程序，然后触发信号。信号处理程序被触发。

::: {#cb403 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <signal.h>

void handler(int sig)
{
    // Undefined behavior to call printf() if this handler was not
    // as the result of a raise(), i.e. if you hit CTRL-C.

    printf("Got signal %d!\n", sig);

    // Common to reset the handler just in case the implementation set
    // it to SIG_DFL when the signal occurred.

    signal(sig, handler);
}

int main(void)
{
    signal(SIGINT, handler);

    raise(SIGINT);
    raise(SIGINT);
    raise(SIGINT);
}
```
:::

Output:

::: {#cb404 .sourceCode}
``` {.sourceCode .default}
Got signal 2!
Got signal 2!
Got signal 2!
```
:::


This example catches `SIGINT` but then sets a flag to `1`. Then the main loop sees the flag and exits.

> 这个例子捕获`SIGINT`信号，然后将标志设置为`1`。然后主循环看到标志并退出。

::: {#cb405 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <signal.h>

volatile sig_atomic_t x;

void handler(int sig)
{
    x = 1;
}

int main(void)
{
    signal(SIGINT, handler);

    printf("Hit CTRL-C to exit\n");
    while (x != 1);
}
```
:::

### See Also {#see-also-107 .unnumbered .unlisted}

[`raise()`](signal.html#man-raise), [`abort()`](stdlib.html#man-abort)

------------------------------------------------------------------------

## [15.2]{.header-section-number} `raise()` {#man-raise number="15.2"}

Cause a signal to be raised

### Synopsis {#synopsis-115 .unnumbered .unlisted}

::: {#cb406 .sourceCode}
``` {.sourceCode .c}
#include <signal.h>

int raise(int sig);
```
:::

### Description {#description-115 .unnumbered .unlisted}


Causes the signal handler for the signal `sig` to be called. If the handler is `SIG_DFL` or `SIG_IGN`, then the default action or no action happens.

> 触发信号处理程序处理信号sig。如果处理程序是SIG_DFL或SIG_IGN，则会发生默认操作或不执行任何操作。

`raise()` returns after the signal handler has finished running.


Interestingly, if you cause a signal to happen with `raise()`, you can call library functions from within the signal handler without causing undefined behavior. I'm not sure how this fact is practically useful, though.

> 有趣的是，如果你使用`raise()`引发一个信号，你可以在信号处理程序中调用库函数而不会导致未定义的行为。不过我不确定这个事实有什么实际用处。

### Return Value {#return-value-114 .unnumbered .unlisted}

Returns `0` on success. Nonzero otherwise.

### Example {#example-115 .unnumbered .unlisted}


This program sets the signal handler, then raises the signal. The signal handler fires.

> 这个程序设置信号处理程序，然后提出信号。信号处理程序触发。

::: {#cb407 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <signal.h>

void handler(int sig)
{
    // Undefined behavior to call printf() if this handler was not
    // as the result of a raise(), i.e. if you hit CTRL-C.

    printf("Got signal %d!\n", sig);

    // Common to reset the handler just in case the implementation set
    // it to SIG_DFL when the signal occurred.

    signal(sig, handler);
}

int main(void)
{
    signal(SIGINT, handler);

    raise(SIGINT);
    raise(SIGINT);
    raise(SIGINT);
}
```
:::

Output:

::: {#cb408 .sourceCode}
``` {.sourceCode .default}
Got signal 2!
Got signal 2!
Got signal 2!
```
:::

### See Also {#see-also-108 .unnumbered .unlisted}

[`signal()`](signal.html#man-signal)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](setjmp.html) \| [Contents](index.html) \| [Next](stdalign.html)
:::
