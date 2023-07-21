---
tip: translate by openai@2023-07-20 19:14:47
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdarg.html) \| [Contents](index.html) \| [Next](stdbool.html)
:::

------------------------------------------------------------------------

# [18]{.header-section-number} `<stdatomic.h>` Atomic-Related Functions {#stdatomic number="18"}


  --------------------------------------------------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------------------------------------------------
简体中文

  Function                                                                                    Description

> 功能                                                                                    描述

  ------------------------------------------------------------------------------------------- ------------------------------------------------------

> -------------------------------------------------------------------------------------------
--------------------------------------------------------
简体中文：

-------------------------------------------------------------------------------------------
--------------------------------------------------------

  [`atomic_compare_exchange_strong_explicit()`](stdatomic.html#man-atomic_compare_exchange)   Atomic compare and exchange, strong, explicit

> 原子比较和交换，强，明确


  [`atomic_compare_exchange_strong()`](stdatomic.html#man-atomic_compare_exchange)            Atomic compare and exchange, strong

> 原子比较和交换，强大的


  [`atomic_compare_exchange_weak_explicit()`](stdatomic.html#man-atomic_compare_exchange)     Atomic compare and exchange, weak, explicit

> 原子比较和交换，弱，明确


  [`atomic_compare_exchange_weak()`](stdatomic.html#man-atomic_compare_exchange)              Atomic compare and exchange, weak

> 原子比较和交换，弱


  [`atomic_exchange_explicit()`](stdatomic.html#man-atomic_exchange)                          Replace a value in an atomic object, explicit

> `atomic_exchange_explicit()`函数用于显式地替换原子对象中的值。


  [`atomic_exchange()`](stdatomic.html#man-atomic_exchange)                                   Replace a value in an atomic object

> `atomic_exchange()`：用原子对象替换一个值


  [`atomic_fetch_add_explicit()`](stdatomic.html#man-atomic_fetch)                            Atomically add to an atomic integer, explicit

> 原子地添加一个原子整数，明确地


  [`atomic_fetch_add()`](stdatomic.html#man-atomic_fetch)                                     Atomically add to an atomic integer

> `atomic_fetch_add()`（stdatomic.html#man-atomic_fetch）原子性地增加原子整数


  [`atomic_fetch_and_explicit()`](stdatomic.html#man-atomic_fetch)                            Atomically bitwise-AND an atomic integer, explicit

> 原子地位运算一个原子整数，显式地


  [`atomic_fetch_and()`](stdatomic.html#man-atomic_fetch)                                     Atomically bitwise-AND an atomic integer

> `atomic_fetch_and()`原子地对原子整数进行位与操作


  [`atomic_fetch_or_explicit()`](stdatomic.html#man-atomic_fetch)                             Atomically bitwise-OR an atomic integer, explicit

> 原子地位或一个原子整数，明确


  [`atomic_fetch_or()`](stdatomic.html#man-atomic_fetch)                                      Atomically bitwise-OR an atomic integer

> atomically 使用按位或操作原子地更新一个原子整数


  [`atomic_fetch_sub_explicit()`](stdatomic.html#man-atomic_fetch)                            Atomically subtract from an atomic integer, explicit

> 原子地从原子整数中减去，明确地


  [`atomic_fetch_sub()`](stdatomic.html#man-atomic_fetch)                                     Atomically subtract from an atomic integer

> 原子性地从原子整数中减去


  [`atomic_fetch_xor_explicit()`](stdatomic.html#man-atomic_fetch)                            Atomically bitwise-XOR an atomic integer, explicit

> 原子操作地对一个原子整数进行位异或操作，明确指定


  [`atomic_fetch_xor()`](stdatomic.html#man-atomic_fetch)                                     Atomically bitwise-XOR an atomic integer

> `atomic_fetch_xor()`原子地位元异或一个原子整数


  [`atomic_flag_clear_explicit()`](stdatomic.html#man-atomic_flag_clear)                      Clear an atomic flag, explicit

> 清除原子旗标，明确


  [`atomic_flag_clear()`](stdatomic.html#man-atomic_flag_clear)                               Clear an atomic flag

> atomic_flag_clear()（stdatomic.html#man-atomic_flag_clear）清除原子标志


  [`atomic_flag_test_and_set_explicit()`](stdatomic.html#man-atomic_flag_test_and_set)        Test and set an atomic flag, explicit

> `atomic_flag_test_and_set_explicit()`：显式地测试并设置原子标志


  [`atomic_flag_test_and_set()`](stdatomic.html#man-atomic_flag_test_and_set)                 Test and set an atomic flag

> `atomic_flag_test_and_set()`（stdatomic.html#man-atomic_flag_test_and_set）测试并设置原子标志


  [`atomic_init()`](stdatomic.html#man-atomic_init)                                           Initialize an atomic variable

> `atomic_init()` 初始化原子变量


  [`atomic_is_lock_free()`](stdatomic.html#man-atomic_is_lock_free)                           Determine if an atomic type is lock free

> `atomic_is_lock_free()`（stdatomic.html#man-atomic_is_lock_free）确定原子类型是否无锁。


  [`atomic_load_explicit()`](stdatomic.html#man-atomic_load)                                  Return a value from an atomic variable, explicit

> 从原子变量中显式地返回一个值


  [`atomic_load()`](stdatomic.html#man-atomic_load)                                           Return a value from an atomic variable

> `atomic_load()`返回原子变量中的一个值


  [`atomic_signal_fence()`](stdatomic.html#man-atomic_signal_fence)                           Fence for intra-thread signal handlers

> `atomic_signal_fence()`（[stdatomic.html#man-atomic_signal_fence]）：用于线程内信号处理程序的栅栏


  [`atomic_store_explicit()`](stdatomic.html#man-atomic_store)                                Store a value in an atomic variable, explicit

> 在原子变量中显式地存储一个值


  [`atomic_store()`](stdatomic.html#man-atomic_store)                                         Store a value in an atomic variable

> `atomic_store()`函数用于在原子变量中存储一个值。


  [`atomic_thread_fence()`](stdatomic.html#man-atomic_thread_fence)                           Set up a fence

> `atomic_thread_fence()`设置一个栅栏


  [`ATOMIC_VAR_INIT()`](stdatomic.html#man-ATOMIC_VAR_INIT)                                   Create an initializer for an atomic variable

> `ATOMIC_VAR_INIT()` 创建原子变量的初始化器


  [`kill_dependency()`](stdatomic.html#man-kill_dependency)                                   End a dependency chain

> 结束依赖链

  --------------------------------------------------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告


You might need to add `-latomic` to your compilation command line on Unix-like operating systems.

> 你可能需要在类Unix操作系统的编译命令行中添加`-latomic`。

## [18.1]{.header-section-number} Atomic Types {#atomic-types number="18.1"}

A bunch of types are predefined by this header:

  -----------------------------------------------------------------------
  Atomic type                         Longhand equivalent
  ----------------------------------- -----------------------------------
  `atomic_bool`                       `_Atomic _Bool`

  `atomic_char`                       `_Atomic char`

  `atomic_schar`                      `_Atomic signed char`

  `atomic_uchar`                      `_Atomic unsigned char`

  `atomic_short`                      `_Atomic short`

  `atomic_ushort`                     `_Atomic unsigned short`

  `atomic_int`                        `_Atomic int`

  `atomic_uint`                       `_Atomic unsigned int`

  `atomic_long`                       `_Atomic long`

  `atomic_ulong`                      `_Atomic unsigned long`

  `atomic_llong`                      `_Atomic long long`

  `atomic_ullong`                     `_Atomic unsigned long long`

  `atomic_char16_t`                   `_Atomic char16_t`

  `atomic_char32_t`                   `_Atomic char32_t`

  `atomic_wchar_t`                    `_Atomic wchar_t`

  `atomic_int_least8_t`               `_Atomic int_least8_t`

  `atomic_uint_least8_t`              `_Atomic uint_least8_t`

  `atomic_int_least16_t`              `_Atomic int_least16_t`

  `atomic_uint_least16_t`             `_Atomic uint_least16_t`

  `atomic_int_least32_t`              `_Atomic int_least32_t`

  `atomic_uint_least32_t`             `_Atomic uint_least32_t`

  `atomic_int_least64_t`              `_Atomic int_least64_t`

  `atomic_uint_least64_t`             `_Atomic uint_least64_t`

  `atomic_int_fast8_t`                `_Atomic int_fast8_t`

  `atomic_uint_fast8_t`               `_Atomic uint_fast8_t`

  `atomic_int_fast16_t`               `_Atomic int_fast16_t`

  `atomic_uint_fast16_t`              `_Atomic uint_fast16_t`

  `atomic_int_fast32_t`               `_Atomic int_fast32_t`

  `atomic_uint_fast32_t`              `_Atomic uint_fast32_t`

  `atomic_int_fast64_t`               `_Atomic int_fast64_t`

  `atomic_uint_fast64_t`              `_Atomic uint_fast64_t`

  `atomic_intptr_t`                   `_Atomic intptr_t`

  `atomic_uintptr_t`                  `_Atomic uintptr_t`

  `atomic_size_t`                     `_Atomic size_t`

  `atomic_ptrdiff_t`                  `_Atomic ptrdiff_t`

  `atomic_intmax_t`                   `_Atomic intmax_t`

  `atomic_uintmax_t`                  `_Atomic uintmax_t`
  -----------------------------------------------------------------------

You can make your own additional types with the `_Atomic` type qualifier:

::: {#cb432 .sourceCode}
``` {.sourceCode .c}
_Atomic double x;
```
:::

or the `_Atomic()` type specifier:

::: {#cb433 .sourceCode}
``` {.sourceCode .c}
_Atomic(double) x;
```
:::

## [18.2]{.header-section-number} Lock-free Macros {#lock-free-macros number="18.2"}

These macros let you know if a type is lock-free or not. Maybe.


They can be used at compile time with `#if`. They apply to both signed and unsigned types.

> 他们可以在编译时使用`#if`。它们适用于有符号和无符号类型。

  -----------------------------------------------------------------------
  Atomic Type                         Lock Free Macro
  ----------------------------------- -----------------------------------
  `atomic_bool`                       `ATOMIC_BOOL_LOCK_FREE`

  `atomic_char`                       `ATOMIC_CHAR_LOCK_FREE`

  `atomic_char16_t`                   `ATOMIC_CHAR16_T_LOCK_FREE`

  `atomic_char32_t`                   `ATOMIC_CHAR32_T_LOCK_FREE`

  `atomic_wchar_t`                    `ATOMIC_WCHAR_T_LOCK_FREE`

  `atomic_short`                      `ATOMIC_SHORT_LOCK_FREE`

  `atomic_int`                        `ATOMIC_INT_LOCK_FREE`

  `atomic_long`                       `ATOMIC_LONG_LOCK_FREE`

  `atomic_llong`                      `ATOMIC_LLONG_LOCK_FREE`

  `atomic_intptr_t`                   `ATOMIC_POINTER_LOCK_FREE`
  -----------------------------------------------------------------------

These macros can interestingly have *three* different values:

  Value   Meaning

  ------- ----------------------------------------------------------------------------------------------

> ------- ----------------------------------------------------------------------------------------------
简体中文：------- ----------------------------------------------------------------------------------------------
  `0`     Never lock-free.

  `1`     *Sometimes* lock-free[^38^](footnotes.html#fn38){#fnref38 .footnote-ref role="doc-noteref"}.

> 有时是无锁的。
  `2`     Always lock-free.

## [18.3]{.header-section-number} Atomic Flag {#atomic-flag number="18.3"}


The `atomic_flag` opaque type is the only time guaranteed to be lock-free. Though your PC implementation probably does a lot more.

> 原子标志不透明类型是唯一保证无锁的类型。尽管你的PC实现可能做更多的工作。


It is accessed through the [`atomic_flag_test_and_set()`](stdatomic.html#man-atomic_flag_test_and_set) and [`atomic_flag_clear()`](stdatomic.html#man-atomic_flag_clear) functions.

> 它可以通过[`atomic_flag_test_and_set()`](stdatomic.html#man-atomic_flag_test_and_set)和[`atomic_flag_clear()`](stdatomic.html#man-atomic_flag_clear)函数访问。

Before use, it can be initialized to a clear state with:

::: {#cb434 .sourceCode}
``` {.sourceCode .c}
atomic_flag f = ATOMIC_FLAG_INIT;
```
:::

## [18.4]{.header-section-number} Memory Order {#memory-order number="18.4"}


This header introduces a new `enum` type called `memory_order`. This is used by a bunch of the functions to specify memory orders other than sequential consistency.

> 这个头文件引入了一种新的枚举类型叫做memory_order。这被一系列的函数用来指定比顺序一致性更高的内存顺序。

  -----------------------------------------------------------------------
  `memory_order`                      Description
  ----------------------------------- -----------------------------------
  `memory_order_seq_cst`              Sequential Consistency

  `memory_order_acq_rel`              Acquire/Release

  `memory_order_release`              Release

  `memory_order_acquire`              Acquire

  `memory_order_consume`              Consume

  `memory_order_relaxed`              Relaxed
  -----------------------------------------------------------------------

You can feed these into atomic functions with the `_explicit` suffix.


The non-`_explcit` versions of the functions are the same as if you'd called the `_explicit` counterpart with `memory_order_seq_cst`.

> 非显式版本的函数与调用具有memory_order_seq_cst的显式对应物相同。

------------------------------------------------------------------------

## [18.5]{.header-section-number} `ATOMIC_VAR_INIT()` {#man-ATOMIC_VAR_INIT number="18.5"}

Create an initializer for an atomic variable

### Synopsis {#synopsis-122 .unnumbered .unlisted}

::: {#cb435 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

#define ATOMIC_VAR_INIT(C value)   // Deprecated
```
:::

### Description {#description-122 .unnumbered .unlisted}


This macro expands to an initializer, so you can use it when a variable is defined.

> 这个宏展开为一个初始化器，所以你可以在定义变量时使用它。

The type of the `value` should be the base type of the atomic variable.

The initialization itself is *not* an atomic operation, ironically.


[CPPReference says this is deprecated](https://en.cppreference.com/w/cpp/atomic/ATOMIC_VAR_INIT)[^39^](footnotes.html#fn39){#fnref39 .footnote-ref role="doc-noteref"} and likely to be removed. Standards document [p1138r0](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1138r0.pdf)[^40^](footnotes.html#fn40){#fnref40 .footnote-ref role="doc-noteref"} elaborates that the macro is limited in that it can't properly initialize atomic `struct`s, and its original *raison d'être* turned out to not be useful.

> CPPReference 说这是已经弃用的，可能会被移除。标准文档 p1138r0 详细阐述了该宏的局限性，它无法正确初始化原子 `struct`，而且它最初的目的也没有被有效利用。

Just initialize the variable straight-up, instead.

### Return Value {#return-value-120 .unnumbered .unlisted}

Expands to an initializer suitable for this atomic variable.

### Example {#example-122 .unnumbered .unlisted}

::: {#cb436 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    atomic_int x = ATOMIC_VAR_INIT(3490);  // Deprecated
    printf("%d\n", x);
}
```
:::

### See Also {#see-also-115 .unnumbered .unlisted}

[`atomic_init()`](stdatomic.html#man-atomic_init)

------------------------------------------------------------------------

## [18.6]{.header-section-number} `atomic_init()` {#man-atomic_init number="18.6"}

Initialize an atomic variable

### Synopsis {#synopsis-123 .unnumbered .unlisted}

::: {#cb437 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

void atomic_init(volatile A *obj, C value);
```
:::

### Description {#description-123 .unnumbered .unlisted}

You can use this to initialize an atomic variable.

The type of the `value` should be the base type of the atomic variable.

The initialization itself is *not* an atomic operation, ironically.


As far as I can tell, there's no difference between this and assigning directly to the atomic variable. The spec says it's there to allow the compiler to inject any additional initialization that needs doing, but everything seems fine without it. If anyone has more info, send it my way.

> 就我所知，这和直接赋值给原子变量没有什么区别。规范中说它是为了允许编译器注入任何需要做的额外初始化，但是没有它一切似乎都很正常。如果有人有更多的信息，请发给我。

### Return Value {#return-value-121 .unnumbered .unlisted}

Returns nothing!

### Example {#example-123 .unnumbered .unlisted}

::: {#cb438 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    atomic_int x;
    
    atomic_init(&x, 3490);

    printf("%d\n", x);
}
```
:::

### See Also {#see-also-116 .unnumbered .unlisted}


[`ATOMIC_VAR_INIT()`](stdatomic.html#man-ATOMIC_VAR_INIT), [`atomic_store()`](stdatomic.html#man-atomic_store), [`atomic_store_explicit()`](stdatomic.html#man-atomic_store)

> [ATOMIC_VAR_INIT()](stdatomic.html#man-ATOMIC_VAR_INIT)：原子变量初始化
[atomic_store()](stdatomic.html#man-atomic_store)：原子存储
[atomic_store_explicit()](stdatomic.html#man-atomic_store)：显式原子存储

------------------------------------------------------------------------

## [18.7]{.header-section-number} `kill_dependency()` {#man-kill_dependency number="18.7"}

End a dependency chain

### Synopsis {#synopsis-124 .unnumbered .unlisted}

::: {#cb439 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

type kill_dependency(type y);
```
:::

### Description {#description-124 .unnumbered .unlisted}


This is potentially useful for optimizing if you're using `memory_order_consume` anywhere.

> 这可能有助于优化，如果您在任何地方使用`memory_order_consume`。


And if you know what you're doing. If unsure, learn more before trying to use this.

> 如果你知道你在做什么，如果不确定，在尝试使用之前先学习更多。

### Return Value {#return-value-122 .unnumbered .unlisted}

Returns the value passed in.

### Example {#example-124 .unnumbered .unlisted}


In this example, `i` carries a dependency into `x`. And would do into `y`, except for the call to `kill_dependency()`.

> 在这个例子中，`i`将依赖性传递给`x`。它也会传递给`y`，除非调用`kill_dependency()`。

::: {#cb440 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    atomic_int a;
    int i = 10, x, y;

    atomic_store_explicit(&a, 3490, memory_order_release);

    i = atomic_load_explicit(&a, memory_order_consume);
    x = i;
    y = kill_dependency(i);

    printf("%d %d\n", x, y);  // 3490 and either 3490 or 10
}
```
:::

------------------------------------------------------------------------

## [18.8]{.header-section-number} `atomic_thread_fence()` {#man-atomic_thread_fence number="18.8"}

Set up a fence

### Synopsis {#synopsis-125 .unnumbered .unlisted}

::: {#cb441 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

void atomic_thread_fence(memory_order order);
```
:::

### Description {#description-125 .unnumbered .unlisted}

This sets up a memory fence with the specified `order`.

  `order`                  Description
  ------------------------ -------------------------------------------------
  `memory_order_seq_cst`   Sequentially consistency acquire/release fence
  `memory_order_acq_rel`   Acquire/release dence
  `memory_order_release`   Release fence
  `memory_order_acquire`   Acquire fence
  `memory_order_consume`   Acquire fence (again)

  `memory_order_relaxed`   No fence at all---no point in calling with this

> `memory_order_relaxed` 没有任何栅栏---没有必要调用它。


You might try to avoid using these and just stick with the different modes with [`atomic_store_explicit()`](stdatomic.html#man-atomic_store) and [`atomic_load_explicit()`](stdatomic.html#man-atomic_load). Or not.

> 你可以尝试避免使用这些，只使用[`atomic_store_explicit()`](stdatomic.html#man-atomic_store)和[`atomic_load_explicit()`](stdatomic.html#man-atomic_load)的不同模式。或者不用。

### Return Value {#return-value-123 .unnumbered .unlisted}

Returns nothing!

### Example {#example-125 .unnumbered .unlisted}

::: {#cb442 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>
#include <stdatomic.h>

atomic_int shared_1 = 1;
atomic_int shared_2 = 2;

int thread_1(void *arg)
{
    (void)arg;

    atomic_store_explicit(&shared_1, 10, memory_order_relaxed);

    atomic_thread_fence(memory_order_release);

    atomic_store_explicit(&shared_2, 20, memory_order_relaxed);

    return 0;
}

int thread_2(void *arg)
{
    (void)arg;

    // If this fence runs after the release fence, we're
    // guaranteed to see thread_1's changes to the shared
    // varaibles.

    atomic_thread_fence(memory_order_acquire);

    if (shared_2 == 20) {
        printf("Shared_1 better be 10 and it's %d\n", shared_1);
    } else {
        printf("Anything's possible: %d %d\n", shared_1, shared_2);
    }

    return 0;
}

int main(void)
{
    thrd_t t1, t2;

    thrd_create(&t2, thread_2, NULL);
    thrd_create(&t1, thread_1, NULL);

    thrd_join(t1, NULL);
    thrd_join(t2, NULL);
}
```
:::

### See Also {#see-also-117 .unnumbered .unlisted}


[`atomic_store_explicit()`](stdatomic.html#man-atomic_store), [`atomic_load_explicit()`](stdatomic.html#man-atomic_load), [`atomic_signal_fence()`](stdatomic.html#man-atomic_signal_fence)

> 1. `atomic_store_explicit()`：原子存储显式
2. `atomic_load_explicit()`：原子加载显式
3. `atomic_signal_fence()`：原子信号栅栏

------------------------------------------------------------------------

## [18.9]{.header-section-number} `atomic_signal_fence()` {#man-atomic_signal_fence number="18.9"}

Fence for intra-thread signal handlers

### Synopsis {#synopsis-126 .unnumbered .unlisted}

::: {#cb443 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

void atomic_signal_fence(memory_order order);
```
:::

### Description {#description-126 .unnumbered .unlisted}


This works like `atomic_thread_fence()` except its purpose is within in a single thread; notably for use in a signal handler in that thread.

> 这与`atomic_thread_fence()`的作用相似，但它的目的是在单个线程内部使用；特别是在该线程的信号处理程序中使用。


Since signals can happen at any time, we might need a way to be certain that any writes by the thread that happened before the signal handler be visible within that signal handler.

> 由于信号可能随时发生，我们可能需要一种方法来确保线程在信号处理程序之前发生的任何写入在该信号处理程序中可见。

### Return Value {#return-value-124 .unnumbered .unlisted}

Returns nothing!

### Example {#example-126 .unnumbered .unlisted}


Partial demo. (Note that it's technically undefined behavior to call `printf()` in a signal handler.)

> 部分演示。（注意，在信号处理程序中调用`printf()`技术上是未定义的行为。）

::: {#cb444 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <signal.h>
#include <stdatomic.h>

int global;

void handler(int sig)
{
    (void)sig;

    // If this runs before the release, the handler will
    // potentially see global == 0.
    //
    // Otherwise, it will definitely see global == 10.

    atomic_signal_fence(memory_order_acquire);

    printf("%d\n", global);
}

int main(void)
{
    signal(SIGINT, handler);

    global = 10;

    atomic_signal_fence(memory_order_release);

    // If the signal handler runs after the release
    // it will definitely see the value 10 in global.
}
```
:::

### See Also {#see-also-118 .unnumbered .unlisted}


[`atomic_thread_fence()`](stdatomic.html#man-atomic_thread_fence), [`signal()`](signal.html#man-signal)

> atomic_thread_fence()：原子线程围栏
signal()：信号

------------------------------------------------------------------------

## [18.10]{.header-section-number} `atomic_is_lock_free()` {#man-atomic_is_lock_free number="18.10"}

Determine if an atomic type is lock free

### Synopsis {#synopsis-127 .unnumbered .unlisted}

::: {#cb445 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

_Bool atomic_is_lock_free(const volatile A *obj);
```
:::

### Description {#description-127 .unnumbered .unlisted}


Determines if the variable `obj` of type `A` is lock-free. Can be used with any type.

> 判断类型为A的变量obj是否是无锁的。可以用于任何类型。


Unlike the [lock-free macros](stdatomic.html#lock-free-macros) which can be used at compile-time, this is strictly a run-time function. So in places where the macros say "maybe", this function will definitely tell you one way or another if the atomic variable is lock-free.

> 与可在编译时使用的[无锁宏](stdatomic.html#lock-free-macros)不同，这是一个严格的运行时函数。因此，在宏中说“也许”的地方，此函数将肯定告诉您原子变量是否无锁。


This is useful when you're defining your own atomic variables and want to know their lock-free status.

> 这在你定义自己的原子变量并想知道它们的无锁状态时很有用。

### Return Value {#return-value-125 .unnumbered .unlisted}

True if the variable is lock-free, false otherwise.

### Example {#example-127 .unnumbered .unlisted}


Test if a couple `struct`s and an atomic `double` are lock-free. On my system, the larger `struct` is too big to be lock-free, but the other two are OK.

> 在我的系统上，测试一对`struct`和一个原子`double`是否是无锁的。较大的`struct`太大而不能无锁，但其他两个可以。

::: {#cb446 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    struct foo {
        int x, y;
    };

    struct bar {
        int x, y, z;
    };

    _Atomic(double) a;
    struct foo b;
    struct bar c;

    printf("a is lock-free: %d\n", atomic_is_lock_free(&a));
    printf("b is lock-free: %d\n", atomic_is_lock_free(&b));
    printf("c is lock-free: %d\n", atomic_is_lock_free(&c));
}
```
:::

Output on my system (YMMV):

::: {#cb447 .sourceCode}
``` {.sourceCode .default}
a is lock-free: 1
b is lock-free: 1
c is lock-free: 0
```
:::

### See Also {#see-also-119 .unnumbered .unlisted}

[Lock-free Macros](stdatomic.html#lock-free-macros)

------------------------------------------------------------------------

## [18.11]{.header-section-number} `atomic_store()` {#man-atomic_store number="18.11"}

Store a value in an atomic variable

### Synopsis {#synopsis-128 .unnumbered .unlisted}

::: {#cb448 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

void atomic_store(volatile A *object, C desired);

void atomic_store_explicit(volatile A *object,
                           C desired, memory_order order);
```
:::

### Description {#description-128 .unnumbered .unlisted}

Store a value in an atomic variable, possible synchronized.

This is like a plain assignment, but with more flexibility.

These have the same storage effect for an `atomic_int x`:

::: {#cb449 .sourceCode}
``` {.sourceCode .c}
x = 10;
atomic_store(&x, 10);
atomic_store_explicit(&x, 10, memory_order_seq_cst);
```
:::


But the last function, `atomic_store_explicit()`, lets you specify the memory order.

> 但最后一个函数`atomic_store_explicit()`可以让您指定内存顺序。


Since this is a "release-y" operation, none of the "acquire-y" memory orders are legal. `order` can be only be `memory_order_seq_cst`, `memory_order_release`, or `memory_order_relaxed`.

> 由于这是一个“发布”操作，所以所有的“获取”内存顺序都是非法的。`order`只能是`memory_order_seq_cst`、`memory_order_release`或`memory_order_relaxed`。

`order` cannot be `memory_order_acq_rel`, `memory_order_acquire`, or `memory_order_consume`.

### Return Value {#return-value-126 .unnumbered .unlisted}

Returns nothing!

### Example {#example-128 .unnumbered .unlisted}

::: {#cb450 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    atomic_int x = 0;
    atomic_int y = 0;

    atomic_store(&x, 10);

    atomic_store_explicit(&y, 20, memory_order_relaxed);

    // Will print either "10 20" or "10 0":
    printf("%d %d\n", x, y);
}
```
:::

### See Also {#see-also-120 .unnumbered .unlisted}


[`atomic_init()`](stdatomic.html#man-atomic_init), [`atomic_load()`](stdatomic.html#man-atomic_load), [`atomic_load_explicit()`](stdatomic.html#man-atomic_load), [`atomic_exchange()`](stdatomic.html#man-atomic_exchange),\

> `atomic_init()`：原子初始化
`atomic_load()`：原子载入
`atomic_load_explicit()`：显式原子载入
`atomic_exchange()`：原子交换

[`atomic_exchange_explicit()`](stdatomic.html#man-atomic_exchange), [`atomic_compare_exchange_strong()`](stdatomic.html#man-atomic_compare_exchange),\

> `atomic_exchange_explicit()`：原子交换显式（explicit）
`atomic_compare_exchange_strong()`：原子比较交换强（strong）

[`atomic_compare_exchange_strong_explicit()`](stdatomic.html#man-atomic_compare_exchange), [`atomic_compare_exchange_weak()`](stdatomic.html#man-atomic_compare_exchange),\

> `atomic_compare_exchange_strong_explicit()`：显式原子比较交换强（strong）
`atomic_compare_exchange_weak()`：原子比较交换弱（weak）

[`atomic_compare_exchange_weak_explicit()`](stdatomic.html#man-atomic_compare_exchange), [`atomic_fetch_*()`](stdatomic.html#man-atomic_fetch)

> `atomic_compare_exchange_weak_explicit()`：显式弱原子比较交换；`atomic_fetch_*()`：原子获取。

------------------------------------------------------------------------

## [18.12]{.header-section-number} `atomic_load()` {#man-atomic_load number="18.12"}

Return a value from an atomic variable

### Synopsis {#synopsis-129 .unnumbered .unlisted}

::: {#cb451 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

C atomic_load(const volatile A *object);

C atomic_load_explicit(const volatile A *object, memory_order order);
```
:::

### Description {#description-129 .unnumbered .unlisted}


For a pointer to an `object` of type `A`, atomically returns its value `C`. This is a generic function that can be used with any type.

> 对于类型A的对象的指针，原子地返回其值C。这是一个可以用于任何类型的通用函数。

The function `atomic_load_explicit()` lets you specify the memory order.


Since this is an "acquire-y" operation, none of the "release-y" memory orders are legal. `order` can be only be `memory_order_seq_cst`, `memory_order_acquire`, `memory_order_consume`, or `memory_order_relaxed`.

> 由于这是一个"获取"操作，所以所有的"释放"内存指令都是不合法的。`order`只能是`memory_order_seq_cst`、`memory_order_acquire`、`memory_order_consume`或`memory_order_relaxed`。

`order` cannot be `memory_order_acq_rel` or `memory_order_release`.

### Return Value {#return-value-127 .unnumbered .unlisted}

Returns the value stored in `object`.

### Example {#example-129 .unnumbered .unlisted}

::: {#cb452 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    atomic_int x = 10;

    int v = atomic_load(&x);

    printf("%d\n", v);  // 10
}
```
:::

### See Also {#see-also-121 .unnumbered .unlisted}


[`atomic_store()`](stdatomic.html#man-atomic_store), [`atomic_store_explicit()`](stdatomic.html#man-atomic_store)

> `atomic_store()`，[`atomic_store_explicit()`](stdatomic.html#man-atomic_store)：原子存储值

------------------------------------------------------------------------

## [18.13]{.header-section-number} `atomic_exchange()` {#man-atomic_exchange number="18.13"}

Replace a value in an atomic object

### Synopsis {#synopsis-130 .unnumbered .unlisted}

::: {#cb453 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

C atomic_exchange(volatile A *object, C desired);

C atomic_exchange_explicit(volatile A *object, C desired,
                           memory_order order);
```
:::

### Description {#description-130 .unnumbered .unlisted}

Sets the value in `object` to `desired`.

`object` is type `A`, some atomic type.

`desired` is type `C`, the respective non-atomic type to `A`.


This is very similar to `atomic_store()`, except the previous value is atomically returned.

> 这与`atomic_store()`非常相似，只是先前的值会以原子方式返回。

### Return Value {#return-value-128 .unnumbered .unlisted}

Returns the previous value of `object`.

### Example {#example-130 .unnumbered .unlisted}

::: {#cb454 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    atomic_int x = 10;

    int previous = atomic_exchange(&x, 20);

    printf("x is  %d\n", x);
    printf("x was %d\n", previous);
}
```
:::

Output:

::: {#cb455 .sourceCode}
``` {.sourceCode .default}
x is  20
x was 10
```
:::

### See Also {#see-also-122 .unnumbered .unlisted}


[`atomic_init()`](stdatomic.html#man-atomic_init), [`atomic_load()`](stdatomic.html#man-atomic_load), [`atomic_load_explicit()`](stdatomic.html#man-atomic_load), [`atomic_store()`](stdatomic.html#man-atomic_store),\

> 1. `atomic_init()`：原子初始化
2. `atomic_load()`：原子载入
3. `atomic_load_explicit()`：显式原子载入
4. `atomic_store()`：原子存储

[`atomic_store_explicit()`](stdatomic.html#man-atomic_store) [`atomic_compare_exchange_strong()`](stdatomic.html#man-atomic_compare_exchange),\

> `atomic_store_explicit()` 和 `atomic_compare_exchange_strong()`

[`atomic_compare_exchange_strong_explicit()`](stdatomic.html#man-atomic_compare_exchange), [`atomic_compare_exchange_weak()`](stdatomic.html#man-atomic_compare_exchange),\

> `atomic_compare_exchange_strong_explicit()`：原子比较交换强显式（Atomic Compare Exchange Strong Explicit）
`atomic_compare_exchange_weak()`：原子比较交换弱（Atomic Compare Exchange Weak）

[`atomic_compare_exchange_weak_explicit()`](stdatomic.html#man-atomic_compare_exchange)

> `atomic_compare_exchange_weak_explicit()`函数提供了一种原子的方式来比较并交换两个变量的值，并且可以指定内存顺序。

------------------------------------------------------------------------

## [18.14]{.header-section-number} `atomic_compare_exchange_*()` {#man-atomic_compare_exchange number="18.14"}

Atomic compare and exchange

### Synopsis {#synopsis-131 .unnumbered .unlisted}

::: {#cb456 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

_Bool atomic_compare_exchange_strong(volatile A *object,
                                     C *expected, C desired);

_Bool atomic_compare_exchange_strong_explicit(volatile A *object,
                                              C *expected, C desired,
                                              memory_order success,
                                              memory_order failure);

_Bool atomic_compare_exchange_weak(volatile A *object,
                                   C *expected, C desired);

_Bool atomic_compare_exchange_weak_explicit(volatile A *object,
                                            C *expected, C desired,
                                            memory_order success,
                                            memory_order failure);
```
:::

### Description {#description-131 .unnumbered .unlisted}

The venerable basis for some many things lock-free: compare and exchange.


In the above prototypes, `A` is the type of the atomic object, and `C` is the equivalent base type.

> 在上面的原型中，`A`是原子对象的类型，`C`是等效的基本类型。

Ignoring the `_explicit` versions for a moment, what these do is:


-   If the value pointed to by `object` is equal to the value pointed to by `expected`, then the value pointed to by `object` is set to `desired`. And the function returns `true` indicating the exchange did take place.

> 如果`object`指向的值等于`expected`指向的值，那么`object`指向的值就会被设置为`desired`。函数返回`true`，表示交换已经发生。


-   Else the value pointed to by `expected` (yes, `expected`) is set to `desired` and the function returns `false` indicating the exchange did not take place.

> 如果没有，那么指向`expected`的值（是的，`expected`）将被设置为`desired`，函数返回`false`，表明交换没有发生。


Pseudocode for the exchange would look like this[^41^](footnotes.html#fn41){#fnref41 .footnote-ref role="doc-noteref"}:

> 伪代码的交换看起来像这样[^41^](footnotes.html#fn41){#fnref41 .footnote-ref role="doc-noteref"}：

::: {#cb457 .sourceCode}
``` {.sourceCode .c}
bool compare_exchange(atomic_A *object, C *expected, C desired)
{
    if (*object is the same as *expected) {
        *object = desired
        return true
    }

    *expected = desired
    return false
}
```
:::


The `_weak` variants might spontaneously fail, so even if `*object == *desired`, it might not change the value and will return `false`. So you'll want that in a loop if you use it[^42^](footnotes.html#fn42){#fnref42 .footnote-ref role="doc-noteref"}.

> 弱变体可能会自发地失败，因此即使*对象==*期望，它也可能不会改变值并返回false。因此，如果您使用它，您将希望在循环中使用它[^42^]（脚注.html#fn42）{#fnref42 .footnote-ref role="doc-noteref"}。


The `_explicit` variants have two memory orders: `success` if `*object` is set to `desired`, and `failure` if it is not.

> 显式变体有两种内存顺序：如果*对象设置为期望值，则为成功；如果不是，则为失败。


These are test-and-set functions, so you can use `memory_order_acq_rel` with the `_explicit` variants.

> 这些是测试和设置函数，因此您可以使用带有`_explicit`变体的`memory_order_acq_rel`。

### Return Value {#return-value-129 .unnumbered .unlisted}

Returns `true` if `*object` was `*expected`. Otherwise, `false`.

### Example {#example-131 .unnumbered .unlisted}


A contrived example where multiple threads add `2` to a shared value in a lock-free way.

> 一个示例，多个线程以无锁的方式将共享值加2。


(It would be better to use `+= 2` to get this done in real life unless you were using some `_explicit` wizardry.)

> 最好使用`+= 2`来实现这一目标，除非你使用某种`_explicit`魔法。

::: {#cb458 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>
#include <stdatomic.h>

#define LOOP_COUNT 10000

atomic_int value;

int run(void *arg)
{
    (void)arg;

    for(int i = 0; i < LOOP_COUNT; i++) {

        int cur = value;
        int next;

        do {
            next = cur + 2;
        } while (!atomic_compare_exchange_strong(&value, &cur, next));
    }

    return 0;
}

int main(void)
{
    thrd_t t1, t2;

    thrd_create(&t1, run, NULL);
    thrd_create(&t2, run, NULL);

    thrd_join(t1, NULL);
    thrd_join(t2, NULL);
    
    printf("%d should equal %d\n", value, LOOP_COUNT * 4);
}
```
:::

Just replacing this with `value = value + 2` causes data trampling.

### See Also {#see-also-123 .unnumbered .unlisted}


[`atomic_load()`](stdatomic.html#man-atomic_load), [`atomic_load_explicit()`](stdatomic.html#man-atomic_load), [`atomic_store()`](stdatomic.html#man-atomic_store), [`atomic_store_explicit()`](stdatomic.html#man-atomic_store), [`atomic_exchange()`](stdatomic.html#man-atomic_exchange), [`atomic_exchange_explicit()`](stdatomic.html#man-atomic_exchange), [`atomic_fetch_*()`](stdatomic.html#man-atomic_fetch)

> [`atomic_load()`](stdatomic.html#man-atomic_load)：原子加载，
[`atomic_load_explicit()`](stdatomic.html#man-atomic_load)：显式原子加载，
[`atomic_store()`](stdatomic.html#man-atomic_store)：原子存储，
[`atomic_store_explicit()`](stdatomic.html#man-atomic_store)：显式原子存储，
[`atomic_exchange()`](stdatomic.html#man-atomic_exchange)：原子交换，
[`atomic_exchange_explicit()`](stdatomic.html#man-atomic_exchange)：显式原子交换，
[`atomic_fetch_*()`](stdatomic.html#man-atomic_fetch)：原子获取*。

------------------------------------------------------------------------

## [18.15]{.header-section-number} `atomic_fetch_*()` {#man-atomic_fetch number="18.15"}

Atomically modify atomic variables

### Synopsis {#synopsis-132 .unnumbered .unlisted}

::: {#cb459 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

C atomic_fetch_KEY(volatile A *object, M operand);

C atomic_fetch_KEY_explicit(volatile A *object, M operand,
                            memory_order order);
```
:::

### Description {#description-132 .unnumbered .unlisted}


These are actually a group of 10 functions. You substitute one of the following for `KEY` to perform that operation:

> 这些实际上是一组10个函数。您用以下其中一个替换`KEY`来执行该操作：

-   `add`
-   `sub`
-   `or`
-   `xor`
-   `and`


So these functions can add or subtract values to or from an atomic variable, or can perform bitwise-OR, XOR, or AND on them.

> 这些函数可以向原子变量添加或减去值，或对它们执行位或、异或或与运算。


Use it with integer or pointer types. Though the spec is a little vague on the matter, other types make C unhappy. It goes out of its way to avoid undefined behavior with signed integers, as well:

> 使用整数或指针类型。虽然规范在这个问题上有点模糊，但其他类型会让C不高兴。它也会特别小心地避免有符号整数的未定义行为：

C18 §7.17.7.5 ¶3:

> For signed integer types, arithmetic is defined to use two's complement representation with silent wrap-around on overflow; there are no undefined results.


In the synopsis, above, `A` is an atomic type, and `M` is the corresponding non-atomic type for `A` (or `ptrdiff_t` for atomic pointers), and `C` is the corresponding non-atomic type for `A`.

> 在上面的概要中，`A`是原子类型，`M`是`A`的相应非原子类型（或原子指针的`ptrdiff_t`），`C`是`A`的相应非原子类型。

For example, here are some operations on an `atomic_int`.

::: {#cb460 .sourceCode}
``` {.sourceCode .c}
atomic_fetch_add(&x, 20);
atomic_fetch_sub(&x, 37);
atomic_fetch_xor(&x, 3490);
```
:::


They are the same as `+=`, `-=`, `|=`, `^=` and `&=`, except the return value is the *previous* value of the atomic object. (With the assignment operators, the value of the expression is that *after* its evaluation.)

> 它们与`+=`、`-=`、`|=`、`^=`和`&=`相同，只是返回的是原子对象的先前值。（使用赋值运算符，表达式的值是其计算后的值。）

::: {#cb461 .sourceCode}
``` {.sourceCode .c}
atomic_int x = 10;
int prev = atomic_fetch_add(&x, 20);
printf("%d %d\n", prev, x);  // 10 30
```
:::

versus:

::: {#cb462 .sourceCode}
``` {.sourceCode .c}
atomic_int x = 10;
int prev = (x += 20);
printf("%d %d\n", prev, x);  // 30 30
```
:::


And, of course, the `_explicit` version allows you to specify a memory order and all the assignment operators are `memory_order_seq_cst`.

> 而且，当然，`_explicit`版本允许您指定内存顺序，所有的赋值运算符都是`memory_order_seq_cst`。

### Return Value {#return-value-130 .unnumbered .unlisted}

Returns the previous value of the atomic object before the modification.

### Example {#example-132 .unnumbered .unlisted}

::: {#cb463 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    atomic_int x = 0;
    int prev;

    atomic_fetch_add(&x, 3490);
    atomic_fetch_sub(&x, 12);
    atomic_fetch_xor(&x, 444);
    atomic_fetch_or(&x, 12);
    prev = atomic_fetch_and(&x, 42);

    printf("%d %d\n", prev, x);   // 3118 42
}
```
:::

### See Also {#see-also-124 .unnumbered .unlisted}


[`atomic_exchange()`](stdatomic.html#man-atomic_exchange), [`atomic_exchange_explicit()`](stdatomic.html#man-atomic_exchange), [`atomic_compare_exchange_strong()`](stdatomic.html#man-atomic_compare_exchange),\

> [`atomic_exchange()`](stdatomic.html#man-atomic_exchange)：原子交换；
[`atomic_exchange_explicit()`](stdatomic.html#man-atomic_exchange)：显式原子交换；
[`atomic_compare_exchange_strong()`](stdatomic.html#man-atomic_compare_exchange)：强原子比较交换。

[`atomic_compare_exchange_strong_explicit()`](stdatomic.html#man-atomic_compare_exchange), [`atomic_compare_exchange_weak()`](stdatomic.html#man-atomic_compare_exchange),\

> `atomic_compare_exchange_strong_explicit()`：显式原子比较交换强（strong）
`atomic_compare_exchange_weak()`：原子比较交换弱（weak）

[`atomic_compare_exchange_weak_explicit()`](stdatomic.html#man-atomic_compare_exchange)

> `atomic_compare_exchange_weak_explicit()`函数可以用来比较和交换原子变量的值，并且可以指定内存顺序。

------------------------------------------------------------------------

## [18.16]{.header-section-number} `atomic_flag_test_and_set()` {#man-atomic_flag_test_and_set number="18.16"}

Test and set an atomic flag

### Synopsis {#synopsis-133 .unnumbered .unlisted}

::: {#cb464 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

_Bool atomic_flag_test_and_set(volatile atomic_flag *object);

_Bool atomic_flag_test_and_set_explicit(volatile atomic_flag *object,
                                        memory_order order);
```
:::

### Description {#description-133 .unnumbered .unlisted}


One of the venerable old functions of lock-free programming, this function sets the given atomic flag in `object`, and returns the previous value of the flag.

> 一种古老的无锁编程功能，该函数在`对象`中设置给定的原子标志，并返回标志的先前值。


As usual, the `_explicit` allows you to specify an alternate memory order.

> 正如往常，`_explicit`允许您指定替代的内存顺序。

### Return Value {#return-value-131 .unnumbered .unlisted}

Returns `true` if the flag was set previously, and `false` if it wasn't.

### Example {#example-133 .unnumbered .unlisted}


Using test-and-set to implement a spin lock[^43^](footnotes.html#fn43){#fnref43 .footnote-ref role="doc-noteref"}:

> 使用测试和设置来实现自旋锁[^43^](footnotes.html#fn43){#fnref43 .footnote-ref role="doc-noteref"}：

::: {#cb465 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>
#include <stdatomic.h>

// Shared non-atomic struct
struct {
    int x, y, z;
} s = {1, 2, 3};

atomic_flag f = ATOMIC_FLAG_INIT;

int run(void *arg)
{
    int tid = *(int*)arg;

    printf("Thread %d: waiting for lock...\n", tid);

    while (atomic_flag_test_and_set(&f));

    printf("Thread %d: got lock, s is {%d, %d, %d}\n", tid,
                                                       s.x, s.y, s.z);
    s.x = (tid + 1) * 5 + 0;
    s.y = (tid + 1) * 5 + 1;
    s.z = (tid + 1) * 5 + 2;
    printf("Thread %d: set s to {%d, %d, %d}\n", tid, s.x, s.y, s.z);

    printf("Thread %d: releasing lock...\n", tid);
    atomic_flag_clear(&f);

    return 0;
}

int main(void)
{
    thrd_t t1, t2;
    int tid[] = {0, 1};

    thrd_create(&t1, run, tid+0);
    thrd_create(&t2, run, tid+1);

    thrd_join(t1, NULL);
    thrd_join(t2, NULL);
}
```
:::

Example output (varies run to run):

::: {#cb466 .sourceCode}
``` {.sourceCode .default}
Thread 0: waiting for lock...
Thread 0: got lock, s is {1, 2, 3}
Thread 1: waiting for lock...
Thread 0: set s to {5, 6, 7}
Thread 0: releasing lock...
Thread 1: got lock, s is {5, 6, 7}
Thread 1: set s to {10, 11, 12}
Thread 1: releasing lock...
```
:::

### See Also {#see-also-125 .unnumbered .unlisted}

[`atomic_flag_clear()`](stdatomic.html#man-atomic_flag_clear)

------------------------------------------------------------------------

## [18.17]{.header-section-number} `atomic_flag_clear()` {#man-atomic_flag_clear number="18.17"}

Clear an atomic flag

### Synopsis {#synopsis-134 .unnumbered .unlisted}

::: {#cb467 .sourceCode}
``` {.sourceCode .c}
#include <stdatomic.h>

void atomic_flag_clear(volatile atomic_flag *object);

void atomic_flag_clear_explicit(volatile atomic_flag *object,
                                memory_order order);
```
:::

### Description {#description-134 .unnumbered .unlisted}

Clears an atomic flag.


As usual, the `_explicit` allows you to specify an alternate memory order.

> 通常，`_explicit`允许您指定替代的内存顺序。

### Return Value {#return-value-132 .unnumbered .unlisted}

Returns nothing!

### Example {#example-134 .unnumbered .unlisted}


Using test-and-set to implement a spin lock[^44^](footnotes.html#fn44){#fnref44 .footnote-ref role="doc-noteref"}:

> 使用测试和设置来实现自旋锁[^44^](footnotes.html#fn44){#fnref44 .footnote-ref role="doc-noteref"}：

::: {#cb468 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>
#include <stdatomic.h>

// Shared non-atomic struct
struct {
    int x, y, z;
} s = {1, 2, 3};

atomic_flag f = ATOMIC_FLAG_INIT;

int run(void *arg)
{
    int tid = *(int*)arg;

    printf("Thread %d: waiting for lock...\n", tid);

    while (atomic_flag_test_and_set(&f));

    printf("Thread %d: got lock, s is {%d, %d, %d}\n", tid,
                                                       s.x, s.y, s.z);
    s.x = (tid + 1) * 5 + 0;
    s.y = (tid + 1) * 5 + 1;
    s.z = (tid + 1) * 5 + 2;
    printf("Thread %d: set s to {%d, %d, %d}\n", tid, s.x, s.y, s.z);

    printf("Thread %d: releasing lock...\n", tid);
    atomic_flag_clear(&f);

    return 0;
}

int main(void)
{
    thrd_t t1, t2;
    int tid[] = {0, 1};

    thrd_create(&t1, run, tid+0);
    thrd_create(&t2, run, tid+1);

    thrd_join(t1, NULL);
    thrd_join(t2, NULL);
}
```
:::

Example output (varies run to run):

::: {#cb469 .sourceCode}
``` {.sourceCode .default}
Thread 0: waiting for lock...
Thread 0: got lock, s is {1, 2, 3}
Thread 1: waiting for lock...
Thread 0: set s to {5, 6, 7}
Thread 0: releasing lock...
Thread 1: got lock, s is {5, 6, 7}
Thread 1: set s to {10, 11, 12}
Thread 1: releasing lock...
```
:::

### See Also {#see-also-126 .unnumbered .unlisted}


[`atomic_flag_test_and_set()`](stdatomic.html#man-atomic_flag_test_and_set)

> `atomic_flag_test_and_set()`函数用于测试并设置原子标志。

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdarg.html) \| [Contents](index.html) \| [Next](stdbool.html)
:::
