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
  [`raise()`](signal.html#man-raise)     Cause a signal to be raised

Handle signals in a portable way, kind of!

These signals get raised for a variety of reasons such as CTRL-C being hit, requests to terminate for external programs, memory access violations, and so on.

Your OS likely defines a plethora of other signals, as well.

This system is pretty limited, as seen below. If you're on Unix, it's almost certain your OS has far superior signal handling capabilities than the C standard library. Check out [`sigaction`](https://man.archlinux.org/man/sigaction.2.en)[^35^](footnotes.html#fn35){#fnref35 .footnote-ref role="doc-noteref"}.

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

-   Ignore the signal
-   Perform the default action
-   Have a specific function called

The `signal()` function takes two arguments. The first, `sig`, is the name of the signal to handle.

  Signal      Description
  ----------- -------------------------------------------------------------------------------------------
  `SIGABRT`   Raised when `abort()` is called
  `SIGFPE`    Floating-point arithmetic exception
  `SIGILL`    CPU tried to execute an illegal instruction
  `SIGINT`    Interrupt signal, as if `CTRL-C` were pressed
  `SIGSEGV`   Segmention Violation: attempted to access restricted memory
  `SIGTERM`   Termination request[^36^](footnotes.html#fn36){#fnref36 .footnote-ref role="doc-noteref"}

So that's the first bit when you call `signal()`---tell it the signal in question:

::: {#cb398 .sourceCode}
``` {.sourceCode .c}
signal(SIGINT, ...
```
:::

But what's that `func` parameter?

For spoilers, it's a pointer to a function that takes an `int` argument and returns `void`. We can use this to call an arbitrary function when the signal occurs.

Before we do that, though, let's look at the easy ones: telling the system to ignore the signal or perform the default action (which it does by default if you never call `signal()`).

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

If the signal is **not** due to `abort()` or `raise()`, you're only allowed to call these functions from the standard library (though the spec doesn't prohibit calling other non-library functions):

-   [`abort()`](stdlib.html#man-abort)
-   [`_Exit()`](stdlib.html#man-exit)
-   [`quick_exit()`](stdlib.html#man-exit)
-   Functions in [`<stdatomic.h>`](stdatomic.html#stdatomic) when the atomic arguments are lock-free
-   `signal()` with a first argument equivalent to the argument that was passed into the handler

In addition, if the signal was **not** due to `abort()` or `raise()`, the handler can't access any object with static or thread-storage duration unless it's lock-free.

An exception is that you can assign to (but not read from!) a variable of type `volatile sig_atomic_t`.

It's up to the implementation, but the signal handler might be reset to `SIG_DFL` just before the handler is called.

It's undefined behavior to call `signal()` in a multithreaded program.

It's undefined behavior to return from the handler for `SIGFPE`, `SIGILL`, `SIGSEGV`, or any implementation-defined value. You must exit.

The implementation might or might not prevent other signals from arising while in the signal handler.

### Return Value {#return-value-113 .unnumbered .unlisted}

On success, `signal()` returns a pointer to the previous signal handler set by a call to `signal()` for that particular signal number. If you haven't called it set, returns `SIG_DFL`.

On failure, `SIG_ERR` is returned and `errno` is set to a positive value.

### Example {#example-114 .unnumbered .unlisted}

Here's a program that causes `SIGINT` to be ignored. Commonly you trigger this signal by hitting `CTRL-C`.

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

`raise()` returns after the signal handler has finished running.

Interestingly, if you cause a signal to happen with `raise()`, you can call library functions from within the signal handler without causing undefined behavior. I'm not sure how this fact is practically useful, though.

### Return Value {#return-value-114 .unnumbered .unlisted}

Returns `0` on success. Nonzero otherwise.

### Example {#example-115 .unnumbered .unlisted}

This program sets the signal handler, then raises the signal. The signal handler fires.

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
