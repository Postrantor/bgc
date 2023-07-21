---
tip: translate by openai@2023-07-21 16:10:42
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](tgmath.html) \| [Contents](index.html) \| [Next](time.html)
:::

------------------------------------------------------------------------

# [27]{.header-section-number} `<threads.h>` Multithreading Functions {#threads number="27"}


  ----------------------------------------------------------------------------------------------------------------

> ----------------------------------------------------------------------------------------------------------------
简化中文
  Function                                              Description

  ----------------------------------------------------- ----------------------------------------------------------

> ---------------------------------------------------------- ----------------------------------------------------------

  [`call_once()`](threads.html#man-call_once)           Call a function one time no matter how many threads try

> `call_once()`（threads.html#man-call_once）无论有多少线程尝试，只调用一次函数


  [`cnd_broadcast()`](threads.html#man-cnd_broadcast)   Wake up all threads waiting on a condition variable

> [`cnd_broadcast()`](threads.html#man-cnd_broadcast)：唤醒所有正在等待条件变量的线程。


  [`cnd_destroy()`](threads.html#man-cnd_destroy)       Free up resources from a condition variable

> `cnd_destroy()`（[threads.html#man-cnd_destroy](threads.html#man-cnd_destroy)）释放条件变量的资源。


  [`cnd_init()`](threads.html#man-cnd_init)             Initialize a condition variable to make it ready for use

> `cnd_init()` 初始化条件变量，使其准备使用


  [`cnd_signal()`](threads.html#man-cnd_signal)         Wake up a thread waiting on a condition variable

> [`cnd_signal()`](threads.html#man-cnd_signal) 唤醒一个正在等待条件变量的线程。


  [`cnd_timedwait()`](threads.html#man-cnd_timedwait)   Wait on a condition variable with a timeout

> 等待一个条件变量，带有一个超时时间


  [`cnd_wait()`](threads.html#man-cnd_wait)             Wait for a signal on a condition variable

> 等待条件变量上的信号


  [`mtx_destroy()`](threads.html#man-mtx_destroy)       Cleanup a mutex when done with it

> mtx_destroy()：在完成使用时清理互斥量。


  [`mtx_init()`](threads.html#man-mtx_init)             Initialize a mutex for use

> `mtx_init()` 初始化一个互斥量以供使用


  [`mtx_lock()`](threads.html#man-mtx_lock)             Acquire a lock on a mutex

> `mtx_lock()`获取一个互斥锁


  [`mtx_timedlock()`](threads.html#man-mtx_timedlock)   Lock a mutex allowing for timeout

> mtx_timedlock()：允许超时的锁定互斥量


  [`mtx_trylock()`](threads.html#man-mtx_trylock)       Try to lock a mutex, returning if not possible

> 尝试锁定一个互斥量，如果不可能则返回。


  [`mtx_unlock()`](threads.html#man-mtx_unlock)         Free a mutex when you're done with the critical section

> 释放互斥量，当你完成临界区时


  [`thrd_create()`](threads.html#man-thrd_create)       Create a new thread of execution

> `thrd_create()`（threads.html#man-thrd_create）创建一个新的执行线程


  [`thrd_current()`](threads.html#man-thrd_current)     Get the ID of the calling thread

> `thrd_current()`（[threads.html#man-thrd_current](threads.html#man-thrd_current)）获取调用线程的ID。


  [`thrd_detach()`](threads.html#man-thrd_detach)       Automatically clean up threads when they exit

> thrd_detach()：当线程退出时自动清理线程。


  [`thrd_equal()`](threads.html#man-thrd_equal)         Compare two thread descriptors for equality

> 比较两个线程描述符是否相等


  [`thrd_exit()`](threads.html#man-thrd_exit)           Stop and exit this thread

> thrd_exit()：停止并退出此线程


  [`thrd_join()`](threads.html#man-thrd_join)           Wait for a thread to exit

> 等待线程退出（thrd_join()）


  [`thrd_yield()`](threads.html#man-thrd_yield)         Stop running that other threads might run

> `thrd_yield()`（threads.html#man-thrd_yield）停止运行，以便其他线程可以运行


  [`tss_create()`](threads.html#man-tss_create)         Create new thread-specific storage

> 创建新的特定于线程的存储 tss_create()


  [`tss_delete()`](threads.html#man-tss_delete)         Clean up a thread-specific storage variable

> `tss_delete()`（threads.html#man-tss_delete）清理线程特定存储变量


  [`tss_get()`](threads.html#man-tss_get)               Get thread-specific data

> `tss_get()`（[threads.html#man-tss_get](threads.html#man-tss_get)）获取特定于线程的数据


  [`tss_set()`](threads.html#man-tss_set)               Set thread-specific data

> `tss_set()`（[threads.html#man-tss_set](threads.html#man-tss_set)）设置线程特定的数据

  ----------------------------------------------------------------------------------------------------------------

> ----------------------------------------------------------------------------------------------------------------
简化中文

We have a bunch of good things at our disposal with this one:

-   Threads
-   Mutexes
-   Condition Variables
-   Thread-Specific Storage
-   And, last but not least, the always-fun `call_once()` function!

Enjoy!

------------------------------------------------------------------------

## [27.1]{.header-section-number} `call_once()` {#man-call_once number="27.1"}

Call a function one time no matter how many threads try

### Synopsis {#synopsis-198 .unnumbered .unlisted}

::: {#cb681 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

void call_once(once_flag *flag, void (*func)(void));
```
:::

### Description {#description-198 .unnumbered .unlisted}


If you have a bunch of threads running over the same piece of code that calls a function, but you only want that function to run one time, `call_once()` can help you out.

> 如果你有一堆线程在运行同一段代码，而你只想让该函数运行一次，那么`call_once()`可以帮助你。


The catch is the function that is called doesn't return anything and takes no arguments.

> 陷阱是被调用的函数不返回任何内容，也不接受任何参数。


If you need more than that, you'll have to set a threadsafe flag such as `atomic_flag`, or one that you protect with a mutex.

> 如果你需要更多，你必须设置一个线程安全的标志，比如`atomic_flag`，或者一个用互斥量保护的标志。


To use this, you need to pass it a pointer to a function to execute, `func`, and also a pointer to a flag of type `once_flag`.

> 要使用它，您需要传递一个指向要执行的函数`func`的指针，以及一个指向类型`once_flag`的标志的指针。

`once_flag` is an opaque type, so all you need to know is that you initialize it to the value `ONCE_FLAG_INIT`.

### Return Value {#return-value-196 .unnumbered .unlisted}

Returns nothing.

### Example {#example-200 .unnumbered .unlisted}

::: {#cb682 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

once_flag of = ONCE_FLAG_INIT;  // Initialize it like this

void run_once_function(void)
{
    printf("I'll only run once!\n");
}

int run(void *arg)
{
    (void)arg;

    printf("Thread running!\n");

    call_once(&of, run_once_function);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, NULL);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);
}
```
:::

Output (might vary per run):

::: {#cb683 .sourceCode}
``` {.sourceCode .default}
Thread running!
Thread running!
I'll only run once!
Thread running!
Thread running!
Thread running!
```
:::

------------------------------------------------------------------------

## [27.2]{.header-section-number} `cnd_broadcast()` {#man-cnd_broadcast number="27.2"}

Wake up all threads waiting on a condition variable

### Synopsis {#synopsis-199 .unnumbered .unlisted}

::: {#cb684 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int cnd_broadcast(cnd_t *cond);
```
:::

### Description {#description-199 .unnumbered .unlisted}


This is just like `cnd_signal()` in that it wakes up threads that are waiting on a condition variable.... except instead of just rousing one thread, it wakes them all.

> 这就像`cnd_signal()`一样，它唤醒正在等待条件变量的线程......除了不仅唤醒一个线程，而是唤醒所有线程。


Of course, only one will get the mutex, and the rest will have to wait their turn. But instead of being asleep waiting for a signal, they'll be asleep waiting to reacquire the mutex. They're rearin' to go, in other words.

> 当然，只有一个人会获得互斥锁，其余的人只能等待轮到他们。但是，他们不是在睡眠中等待信号，而是在睡眠中等待重新获取互斥锁。换句话说，他们已经准备好了。


This can make a difference in a specific set of circumstances where `cnd_signal()` might leave you hanging.

> 这可以在特定情况下发挥作用，其中`cnd_signal()`可能会让你悬空。


If you're relying on subsequent threads to issue the next `cnd_signal()`, but you have the `cnd_wait()` in a `while` loop[^65^](footnotes.html#fn65){#fnref65 .footnote-ref role="doc-noteref"} that doesn't allow any threads to escape, you'll be stuck. No more threads will be woken up from the wait.

> 如果您依赖后续线程来发出下一个`cnd_signal()`，但您将`cnd_wait()`放在一个`while`循环中[^65^]（脚注。html＃fn65）{＃fnref65.footnote-ref role =“doc-noteref”}，不允许任何线程逃脱，您将被困住。没有更多的线程将从等待中醒来。


But if you `cnd_broadcast()`, all the threads will be woken, and presumably at least one of them will be allowed to escape the `while` loop, freeing it up to broadcast the next wakeup when its work is done.

> 如果你调用`cnd_broadcast()`，所有的线程都会被唤醒，其中一个线程将被允许从`while`循环中脱离出来，以便在完成工作后发出下一次唤醒信号。

### Return Value {#return-value-197 .unnumbered .unlisted}

Returns `thrd_success` or `thrd_error` depending on how well things went.

### Example {#example-201 .unnumbered .unlisted}


In the example below, we launch a bunch of threads, but they're only allowed to run if their ID matches the current ID. If it doesn't, they go back to waiting.

> 在下面的例子中，我们启动了一堆线程，但它们只有在ID与当前ID匹配时才允许运行。如果不匹配，它们就会回到等待状态。


If you `cnd_signal()` to wake the next thread, it might not be the one with the proper ID to run. If it's not, it goes back to sleep and we hang (because no thread is awake to hit `cnd_signal()` again).

> 如果你使用cnd_signal()唤醒下一个线程，可能不是具有正确ID运行的线程。如果不是，它会回到睡眠状态，我们就会挂起（因为没有线程是醒着的去再次触发cnd_signal()）。


But if you `cnd_broadcast()` to wake them all, then they'll all try (one after another) to get out of the `while` loop. And one of them will make it.

> 如果你使用`cnd_broadcast()`来唤醒他们，那么他们都会（一个接一个）试图跳出while循环。其中一个会成功。


Try switching the `cnd_broadcast()` to `cnd_signal()` to see likely deadlocks. It doesn't happen every time, but usually does.

> 尝试将`cnd_broadcast()`更改为`cnd_signal()`以查看可能出现死锁。 这不是每次都会发生，但通常会发生。

::: {#cb685 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    int id = *(int*)arg;

    static int current_id = 0;

    mtx_lock(&mutex);

    while (id != current_id) {
        printf("THREAD %d: waiting\n", id);
        cnd_wait(&condvar, &mutex);

        if (id != current_id)
            printf("THREAD %d: woke up, but it's not my turn!\n", id);
        else
            printf("THREAD %d: woke up, my turn! Let's go!\n", id);
    }

    current_id++;

    printf("THREAD %d: signaling thread %d to run\n", id, current_id);

    //cnd_signal(&condvar);
    cnd_broadcast(&condvar);
    mtx_unlock(&mutex);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];
    int id[] = {4, 3, 2, 1, 0};

    mtx_init(&mutex, mtx_plain);
    cnd_init(&condvar);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, id + i);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);

    mtx_destroy(&mutex);
    cnd_destroy(&condvar);
}
```
:::

Example run with `cnd_broadcast()`:

::: {#cb686 .sourceCode}
``` {.sourceCode .default}
THREAD 4: waiting
THREAD 1: waiting
THREAD 3: waiting
THREAD 2: waiting
THREAD 0: signaling thread 1 to run
THREAD 2: woke up, but it's not my turn!
THREAD 2: waiting
THREAD 4: woke up, but it's not my turn!
THREAD 4: waiting
THREAD 3: woke up, but it's not my turn!
THREAD 3: waiting
THREAD 1: woke up, my turn! Let's go!
THREAD 1: signaling thread 2 to run
THREAD 4: woke up, but it's not my turn!
THREAD 4: waiting
THREAD 3: woke up, but it's not my turn!
THREAD 3: waiting
THREAD 2: woke up, my turn! Let's go!
THREAD 2: signaling thread 3 to run
THREAD 4: woke up, but it's not my turn!
THREAD 4: waiting
THREAD 3: woke up, my turn! Let's go!
THREAD 3: signaling thread 4 to run
THREAD 4: woke up, my turn! Let's go!
THREAD 4: signaling thread 5 to run
```
:::

Example run with `cnd_signal()`:

::: {#cb687 .sourceCode}
``` {.sourceCode .default}
THREAD 4: waiting
THREAD 1: waiting
THREAD 3: waiting
THREAD 2: waiting
THREAD 0: signaling thread 1 to run
THREAD 4: woke up, but it's not my turn!
THREAD 4: waiting

[deadlock at this point]
```
:::


See how `THREAD 0` signaled that it was `THREAD 1`'s turn? But---bad news---it was `THREAD 4` that got woken up. So no one continued the process. `cnd_broadcast()` would have woken them all, so eventually `THREAD 1` would have run, gotten out of the `while`, and broadcast for the next thread to run.

> 看看线程0如何发出信号，表明现在是线程1的轮到？但是坏消息是，被唤醒的是线程4。因此没有人继续进行进程。cnd_broadcast()会唤醒所有线程，因此最终线程1会运行，从while循环中出来，并发出信号，让下一个线程运行。

### See Also {#see-also-187 .unnumbered .unlisted}


[`cnd_signal()`](signal.html#man-signal), [`mtx_lock()`](threads.html#man-mtx_lock), [`mtx_unlock()`](threads.html#man-mtx_unlock)

> `cnd_signal()`：信号（signal）
`mtx_lock()`：锁定（lock）
`mtx_unlock()`：解锁（unlock）

------------------------------------------------------------------------

## [27.3]{.header-section-number} `cnd_destroy()` {#man-cnd_destroy number="27.3"}

Free up resources from a condition variable

### Synopsis {#synopsis-200 .unnumbered .unlisted}

::: {#cb688 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

void cnd_destroy(cnd_t *cond);
```
:::

### Description {#description-200 .unnumbered .unlisted}


This is the opposite of `cnd_init()` and should be called when all threads are done using a condition variable.

> 这是`cnd_init()`的反义词，应该在所有线程使用条件变量完成后调用。

### Return Value {#return-value-198 .unnumbered .unlisted}

Returns nothing!

### Example {#example-202 .unnumbered .unlisted}


General-purpose condition variable example here, but you can see the `cnd_destroy()` down at the end.

> 一个通用条件变量的示例在这里，但你可以在最后看到`cnd_destroy()`。

::: {#cb689 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    mtx_lock(&mutex);

    printf("Thread: waiting...\n");
    cnd_wait(&condvar, &mutex);
    printf("Thread: running again!\n");

    mtx_unlock(&mutex);

    return 0;
}

int main(void)
{
    thrd_t t;

    mtx_init(&mutex, mtx_plain);
    cnd_init(&condvar);

    printf("Main creating thread\n");
    thrd_create(&t, run, NULL);

    // Sleep 0.1s to allow the other thread to wait
    thrd_sleep(&(struct timespec){.tv_nsec=100000000L}, NULL);

    mtx_lock(&mutex);
    printf("Main: signaling thread\n");
    cnd_signal(&condvar);
    mtx_unlock(&mutex);

    thrd_join(t, NULL);

    mtx_destroy(&mutex);
    cnd_destroy(&condvar);  // <-- DESTROY CONDITION VARIABLE
}
```
:::

Output:

::: {#cb690 .sourceCode}
``` {.sourceCode .default}
Main creating thread
Thread: waiting...
Main: signaling thread
Thread: running again!
```
:::

### See Also {#see-also-188 .unnumbered .unlisted}

[`cnd_init()`](threads.html#man-cnd_init)

------------------------------------------------------------------------

## [27.4]{.header-section-number} `cnd_init()` {#man-cnd_init number="27.4"}

Initialize a condition variable to make it ready for use

### Synopsis {#synopsis-201 .unnumbered .unlisted}

::: {#cb691 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int cnd_init(cnd_t *cond);
```
:::

### Description {#description-201 .unnumbered .unlisted}


This is the opposite of `cnd_destroy()`. This prepares a condition variable for use, doing behind-the-scenes work on it.

> 这是`cnd_destroy()`的相反操作。它会为条件变量做准备工作，并在背后进行处理。

Don't use a condition variable without calling this first!

### Return Value {#return-value-199 .unnumbered .unlisted}


If all goes well, returns `thrd_success`. It all doesn't go well, it could return `thrd_nomem` if the system is out of memory, or `thread_error` in the case of any other error.

> 如果一切顺利，返回`thrd_success`。如果一切不顺利，如果系统内存不足，可能会返回`thrd_nomem`，或者在其他任何错误的情况下返回`thread_error`。

### Example {#example-203 .unnumbered .unlisted}


General-purpose condition variable example here, but you can see the `cnd_init()` down at the start of `main()`.

> 一个通用条件变量的例子在这里，但你可以在main()函数开头看到cnd_init()函数。

::: {#cb692 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    mtx_lock(&mutex);

    printf("Thread: waiting...\n");
    cnd_wait(&condvar, &mutex);
    printf("Thread: running again!\n");

    mtx_unlock(&mutex);

    return 0;
}

int main(void)
{
    thrd_t t;

    mtx_init(&mutex, mtx_plain);
    cnd_init(&condvar);      // <-- INITIALIZE CONDITION VARIABLE

    printf("Main creating thread\n");
    thrd_create(&t, run, NULL);

    // Sleep 0.1s to allow the other thread to wait
    thrd_sleep(&(struct timespec){.tv_nsec=100000000L}, NULL);

    mtx_lock(&mutex);
    printf("Main: signaling thread\n");
    cnd_signal(&condvar);
    mtx_unlock(&mutex);

    thrd_join(t, NULL);

    mtx_destroy(&mutex);
    cnd_destroy(&condvar);
}
```
:::

Output:

::: {#cb693 .sourceCode}
``` {.sourceCode .default}
Main creating thread
Thread: waiting...
Main: signaling thread
Thread: running again!
```
:::

### See Also {#see-also-189 .unnumbered .unlisted}

[`cnd_destroy()`](threads.html#man-cnd_destroy)

------------------------------------------------------------------------

## [27.5]{.header-section-number} `cnd_signal()` {#man-cnd_signal number="27.5"}

Wake up a thread waiting on a condition variable

### Synopsis {#synopsis-202 .unnumbered .unlisted}

::: {#cb694 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int cnd_signal(cnd_t *cond);
```
:::

### Description {#description-202 .unnumbered .unlisted}


If you have a thread (or a bunch of threads) waiting on a condition variable, this function will wake one of them up to run.

> 如果你有一个（或一组）线程正在等待一个条件变量，这个函数将唤醒其中一个线程运行。


Compare to `cnd_broadcast()` that wakes up all the threads. See the [`cnd_broadcast()`](threads.html#man-cnd_broadcast) page for more information on when you're want to use that versus this.

> 相比起唤醒所有线程的`cnd_broadcast()`，查看[`cnd_broadcast()`](threads.html#man-cnd_broadcast)页面可以获取更多关于何时使用它而不是这个的信息。

### Return Value {#return-value-200 .unnumbered .unlisted}


Returns `thrd_success` or `thrd_error` depending on how happy your program is.

> 返回`thrd_success`或`thrd_error`取决于程序的快乐程度。

### Example {#example-204 .unnumbered .unlisted}


General-purpose condition variable example here, but you can see the `cnd_signal()` in the middle of `main()`.

> 一个通用条件变量的例子在这里，但你可以在main()函数中看到cnd_signal()。

::: {#cb695 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    mtx_lock(&mutex);

    printf("Thread: waiting...\n");
    cnd_wait(&condvar, &mutex);
    printf("Thread: running again!\n");

    mtx_unlock(&mutex);

    return 0;
}

int main(void)
{
    thrd_t t;

    mtx_init(&mutex, mtx_plain);
    cnd_init(&condvar);

    printf("Main creating thread\n");
    thrd_create(&t, run, NULL);

    // Sleep 0.1s to allow the other thread to wait
    thrd_sleep(&(struct timespec){.tv_nsec=100000000L}, NULL);

    mtx_lock(&mutex);
    printf("Main: signaling thread\n");
    cnd_signal(&condvar);    // <-- SIGNAL CHILD THREAD HERE!
    mtx_unlock(&mutex);

    thrd_join(t, NULL);

    mtx_destroy(&mutex);
    cnd_destroy(&condvar);
}
```
:::

Output:

::: {#cb696 .sourceCode}
``` {.sourceCode .default}
Main creating thread
Thread: waiting...
Main: signaling thread
Thread: running again!
```
:::

### See Also {#see-also-190 .unnumbered .unlisted}


[`cnd_init()`](threads.html#man-cnd_init), [`cnd_destroy()`](threads.html#man-cnd_destroy)

> [`cnd_init()`](threads.html#man-cnd_init)：初始化条件变量
[`cnd_destroy()`](threads.html#man-cnd_destroy)：销毁条件变量

------------------------------------------------------------------------

## [27.6]{.header-section-number} `cnd_timedwait()` {#man-cnd_timedwait number="27.6"}

Wait on a condition variable with a timeout

### Synopsis {#synopsis-203 .unnumbered .unlisted}

::: {#cb697 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int cnd_timedwait(cnd_t *restrict cond, mtx_t *restrict mtx,
                  const struct timespec *restrict ts);
```
:::

### Description {#description-203 .unnumbered .unlisted}


This is like [`cnd_wait()`](threads.html#man-cnd_wait) except we get to specify a timeout, as well.

> 这类似于[`cnd_wait()`](threads.html#man-cnd_wait)，但我们还可以指定超时时间。


Note that the thread still must reacquire the mutex to get more work done even after the timeout. The the main difference is that regular `cnd_wait()` will only try to get the mutex after a `cnd_signal()` or `cnd_broadcast()`, whereas `cnd_timedwait()` will do that, too, **and** try to get the mutex after the timeout.

> 注意，即使超时后，线程仍然必须重新获取互斥量才能完成更多工作。主要区别是，普通的`cnd_wait()`只有在`cnd_signal()`或`cnd_broadcast()`之后才会尝试获取互斥量，而`cnd_timedwait()`既会尝试获取互斥量，也会在超时后尝试获取互斥量。


The timeout is specified as an absolute UTC time since Epoch. You can get this with the [`timespec_get()`](time.html#man-timespec_get) function and then add values on to the result to timeout later than now, as shown in the example.

> 超时是以自标准时间（UTC）纪元以来的绝对时间指定的。您可以使用[`timespec_get()`](time.html#man-timespec_get)函数获取此值，然后在结果上添加值以比现在更晚地超时，如示例中所示。


Beware that you can't have more than 999999999 nanoseconds in the `tv_nsec` field of the `struct timespec`. Mod those so they stay in range.

> 警惕，在`struct timespec`的`tv_nsec`字段中，你不能拥有超过999999999纳秒。调整它们，以保持范围内。

### Return Value {#return-value-201 .unnumbered .unlisted}


If the thread wakes up for a non-timeout reason (e.g. signal or broadcast), returns `thrd_success`. If woken up due to timeout, returns `thrd_timedout`. Otherwise returns `thrd_error`.

> 如果线程因非超时原因而唤醒（例如信号或广播），则返回`thrd_success`。如果由于超时而唤醒，则返回`thrd_timedout`。否则返回`thrd_error`。

### Example {#example-205 .unnumbered .unlisted}


This example has a thread wait on a condition variable for a maximum of 1.75 seconds. And it always times out because no one ever sends a signal. Tragic.

> 这个例子最多等待1.75秒，但它总是超时，因为没有人发出信号。真是悲剧。

::: {#cb698 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <time.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    mtx_lock(&mutex);

    struct timespec ts;

    // Get the time now
    timespec_get(&ts, TIME_UTC);

    // Add on 1.75 seconds from now
    ts.tv_sec += 1;
    ts.tv_nsec += 750000000L;

    // Handle nsec overflow
    ts.tv_sec += ts.tv_nsec / 1000000000L;
    ts.tv_nsec = ts.tv_nsec % 1000000000L;

    printf("Thread: waiting...\n");
    int r = cnd_timedwait(&condvar, &mutex, &ts);

    switch (r) {
        case thrd_success:
            printf("Thread: signaled!\n");
            break;

        case thrd_timedout:
            printf("Thread: timed out!\n");
            return 1;

        case thrd_error:
            printf("Thread: Some kind of error\n");
            return 2;
    }

    mtx_unlock(&mutex);

    return 0;
}

int main(void)
{
    thrd_t t;

    mtx_init(&mutex, mtx_plain);
    cnd_init(&condvar);

    printf("Main creating thread\n");
    thrd_create(&t, run, NULL);

    // Sleep 3s to allow the other thread to timeout
    thrd_sleep(&(struct timespec){.tv_sec=3}, NULL);

    thrd_join(t, NULL);

    mtx_destroy(&mutex);
    cnd_destroy(&condvar);
}
```
:::

Output:

::: {#cb699 .sourceCode}
``` {.sourceCode .default}
Main creating thread
Thread: waiting...
Thread: timed out!
```
:::

### See Also {#see-also-191 .unnumbered .unlisted}


[`cnd_wait()`](threads.html#man-cnd_wait), [`timespec_get()`](time.html#man-timespec_get)

> [`cnd_wait()`](threads.html#man-cnd_wait)：等待条件变量
[`timespec_get()`](time.html#man-timespec_get)：获取时间规范

------------------------------------------------------------------------

## [27.7]{.header-section-number} `cnd_wait()` {#man-cnd_wait number="27.7"}

Wait for a signal on a condition variable

### Synopsis {#synopsis-204 .unnumbered .unlisted}

::: {#cb700 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int cnd_wait(cnd_t *cond, mtx_t *mtx);
```
:::

### Description {#description-204 .unnumbered .unlisted}


This puts the calling thread to sleep until it is awakened by a call to `cnd_signal()` or `cnd_broadcast()`.

> 这会使调用线程睡眠，直到它被`cnd_signal()`或`cnd_broadcast()`唤醒。

### Return Value {#return-value-202 .unnumbered .unlisted}


If everything's fantastic, returns `thrd_success`. Otherwise it returns `thrd_error` to report that something has gone fantastically, horribly awry.

> 如果一切都很棒，返回`thrd_success`。否则，它会返回`thrd_error`以报告某些事情出了糟糕的问题。

### Example {#example-206 .unnumbered .unlisted}


General-purpose condition variable example here, but you can see the `cnd_wait()` in the `run()` function.

> 一个通用条件变量的示例在这里，但你可以在`run()`函数中看到`cnd_wait()`。

::: {#cb701 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    mtx_lock(&mutex);

    printf("Thread: waiting...\n");
    cnd_wait(&condvar, &mutex);       // <-- WAIT HERE!
    printf("Thread: running again!\n");

    mtx_unlock(&mutex);

    return 0;
}

int main(void)
{
    thrd_t t;

    mtx_init(&mutex, mtx_plain);
    cnd_init(&condvar);

    printf("Main creating thread\n");
    thrd_create(&t, run, NULL);

    // Sleep 0.1s to allow the other thread to wait
    thrd_sleep(&(struct timespec){.tv_nsec=100000000L}, NULL);

    mtx_lock(&mutex);
    printf("Main: signaling thread\n");
    cnd_signal(&condvar);    // <-- SIGNAL CHILD THREAD HERE!
    mtx_unlock(&mutex);

    thrd_join(t, NULL);

    mtx_destroy(&mutex);
    cnd_destroy(&condvar);
}
```
:::

Output:

::: {#cb702 .sourceCode}
``` {.sourceCode .default}
Main creating thread
Thread: waiting...
Main: signaling thread
Thread: running again!
```
:::

### See Also {#see-also-192 .unnumbered .unlisted}

[`cnd_timedwait()`](threads.html#man-cnd_timedwait)

------------------------------------------------------------------------

## [27.8]{.header-section-number} `mtx_destroy()` {#man-mtx_destroy number="27.8"}

Cleanup a mutex when done with it

### Synopsis {#synopsis-205 .unnumbered .unlisted}

::: {#cb703 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

void mtx_destroy(mtx_t *mtx);
```
:::

### Description {#description-205 .unnumbered .unlisted}


The opposite of [`mtx_init()`](threads.html#man-mtx_init), this function frees up any resources associated with the given mutex.

> mtx_init() 的反义词，这个函数释放与给定的互斥量相关联的任何资源。

You should call this when all threads are done using the mutex.

### Return Value {#return-value-203 .unnumbered .unlisted}

Returns nothing, the selfish ingrate!

### Example {#example-207 .unnumbered .unlisted}


General-purpose mutex example here, but you can see the `mtx_destroy()` down at the end.

> 一般用途的互斥量示例在这里，但你可以在最后看到`mtx_destroy()`。

::: {#cb704 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    static int count = 0;

    mtx_lock(&mutex);

    printf("Thread: I got %d!\n", count);
    count++;

    mtx_unlock(&mutex);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    mtx_init(&mutex, mtx_plain);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, NULL);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);

    mtx_destroy(&mutex);   // <-- DESTROY THE MUTEX HERE
}
```
:::

Output:

::: {#cb705 .sourceCode}
``` {.sourceCode .default}
Thread: I got 0!
Thread: I got 1!
Thread: I got 2!
Thread: I got 3!
Thread: I got 4!
```
:::

### See Also {#see-also-193 .unnumbered .unlisted}

[`mtx_init()`](threads.html#man-mtx_init)

------------------------------------------------------------------------

## [27.9]{.header-section-number} `mtx_init()` {#man-mtx_init number="27.9"}

Initialize a mutex for use

### Synopsis {#synopsis-206 .unnumbered .unlisted}

::: {#cb706 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int mtx_init(mtx_t *mtx, int type);
```
:::

### Description {#description-206 .unnumbered .unlisted}


Before you can use a mutex variable, you have to initialize it with this call to get it all prepped and ready to go.

> 在使用互斥变量之前，必须通过调用来初始化它，以便使其准备就绪。


But wait! It's not quite that simple. You have to tell it what `type` of mutex you want to create.

> 但是等等！事情并不那么简单。你必须告诉它你想要创建什么类型的互斥锁。

  Type                        Description
  --------------------------- ----------------------------------------
  `mtx_plain`                 Regular ol' mutex
  `mtx_timed`                 Mutex that supports timeouts
  `mtx_plain|mtx_recursive`   Recursive mutex
  `mtx_timed|mtx_recursive`   Recursive mutex that supports timeouts


As you can see, you can make a plain or timed mutex *recursive* by bitwise-ORing the value with `mtx_recursive`.

> 你可以看到，你可以通过用`mtx_recursive`位或运算来创建一个普通或定时的可重入互斥量。


"Recursive" means that the holder of a lock can call `mtx_lock()` multiple times on the same lock. (They have to unlock it an equal number of times before anyone else can take the mutex.) This might ease coding from time to time, especially if you call a function that needs to lock the mutex when you already hold the mutex.

> "递归"意味着持有锁的人可以在同一把锁上多次调用`mtx_lock()`。（他们必须在任何其他人可以拿到互斥量之前解锁它相同数量的次数。）这可能会在某些时候简化编码，特别是当你已经持有互斥量时调用一个需要锁定互斥量的函数。


And the timeout gives a thread a chance to *try* to get the lock for a while, but then bail out if it can't get it in that timeframe. You use the [`mtx_timedlock()`](threads.html#man-mtx_timedlock) function with `mtx_timed` mutexes.

> 给线程设置超时时间可以让它有机会尝试获取锁，但如果在规定时间内无法获取，就会放弃。可以使用[`mtx_timedlock()`](threads.html#man-mtx_timedlock)函数来操作`mtx_timed`互斥量。

### Return Value {#return-value-204 .unnumbered .unlisted}


Returns `thrd_success` in a perfect world, and potentially `thrd_error` in an imperfect one.

> 在完美的世界中返回`thrd_success`，在不完美的世界中可能会返回`thrd_error`。

### Example {#example-208 .unnumbered .unlisted}


General-purpose mutex example here, but you can see the `mtx_init()` down at the top of `main()`:

> 一个通用的互斥锁示例，你可以在main()函数顶部看到mtx_init()：

::: {#cb707 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    static int count = 0;

    mtx_lock(&mutex);

    printf("Thread: I got %d!\n", count);
    count++;

    mtx_unlock(&mutex);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    mtx_init(&mutex, mtx_plain);  // <-- CREATE THE MUTEX HERE

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, NULL);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);

    mtx_destroy(&mutex);   // <-- DESTROY THE MUTEX HERE
}
```
:::

Output:

::: {#cb708 .sourceCode}
``` {.sourceCode .default}
Thread: I got 0!
Thread: I got 1!
Thread: I got 2!
Thread: I got 3!
Thread: I got 4!
```
:::

### See Also {#see-also-194 .unnumbered .unlisted}

[`mtx_destroy()`](threads.html#man-mtx_destroy)

------------------------------------------------------------------------

## [27.10]{.header-section-number} `mtx_lock()` {#man-mtx_lock number="27.10"}

Acquire a lock on a mutex

### Synopsis {#synopsis-207 .unnumbered .unlisted}

::: {#cb709 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int mtx_lock(mtx_t *mtx);
```
:::

### Description {#description-207 .unnumbered .unlisted}


If you're a thread and want to enter a critical section, do I have the function for you!

> 如果你是一根线程，想要进入一个临界区，我有专门的函数为你服务！


A thread that calls this function will wait until it can acquire the mutex, then it will grab it, wake up, and run!

> 一个调用此函数的线程将等待，直到它能够获取互斥量，然后它将抓住它，醒来，并运行！


If the mutex is recursive and is already locked by this thread, it will be locked again and the lock count will increase. If the mutex is not recursive and the thread already holds it, this call will error out.

> 如果互斥锁是递归的，并且已经被这个线程锁定，它将再次被锁定，锁定计数将增加。如果互斥锁不是递归的，并且线程已经持有它，这个调用将出错。

### Return Value {#return-value-205 .unnumbered .unlisted}

Returns `thrd_success` on goodness and `thrd_error` on badness.

### Example {#example-209 .unnumbered .unlisted}


General-purpose mutex example here, but you can see the `mtx_lock()` in the `run()` function:

> 这里有一个通用的互斥量示例，但你可以在`run()`函数中看到`mtx_lock()`：

::: {#cb710 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    static int count = 0;

    mtx_lock(&mutex);  // <-- LOCK HERE

    printf("Thread: I got %d!\n", count);
    count++;

    mtx_unlock(&mutex);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    mtx_init(&mutex, mtx_plain);  // <-- CREATE THE MUTEX HERE

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, NULL);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);

    mtx_destroy(&mutex);   // <-- DESTROY THE MUTEX HERE
}
```
:::

Output:

::: {#cb711 .sourceCode}
``` {.sourceCode .default}
Thread: I got 0!
Thread: I got 1!
Thread: I got 2!
Thread: I got 3!
Thread: I got 4!
```
:::

### See Also {#see-also-195 .unnumbered .unlisted}


[`mtx_unlock()`](threads.html#man-mtx_unlock), [`mtx_trylock()`](threads.html#man-mtx_trylock), [`mtx_timedlock()`](threads.html#man-mtx_timedlock)

> mtx_unlock()：解锁
mtx_trylock()：尝试锁定
mtx_timedlock()：定时锁定

------------------------------------------------------------------------

## [27.11]{.header-section-number} `mtx_timedlock()` {#man-mtx_timedlock number="27.11"}

Lock a mutex allowing for timeout

### Synopsis {#synopsis-208 .unnumbered .unlisted}

::: {#cb712 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int mtx_timedlock(mtx_t *restrict mtx, const struct timespec *restrict ts);
```
:::

### Description {#description-208 .unnumbered .unlisted}


This is just like [`mtx_lock()`](threads.html#man-mtx_lock) except you can add a timeout if you don't want to wait forever.

> 这就像[`mtx_lock()`](threads.html#man-mtx_lock)一样，只是如果你不想永远等待的话，你可以添加一个超时时间。


The timeout is specified as an absolute UTC time since Epoch. You can get this with the [`timespec_get()`](time.html#man-timespec_get) function and then add values on to the result to timeout later than now, as shown in the example.

> 超时是以自标准时间（UTC）纪元以来的绝对时间来指定的。您可以使用[`timespec_get()`](time.html#man-timespec_get)函数获取此值，然后在结果上添加值以比现在更晚地超时，如示例所示。


Beware that you can't have more than 999999999 nanoseconds in the `tv_nsec` field of the `struct timespec`. Mod those so they stay in range.

> 警惕，在'struct timespec'的'tv_nsec'字段中，你不能有超过999999999纳秒。将它们修改为保持在范围内。

### Return Value {#return-value-206 .unnumbered .unlisted}


If everything works and the mutex is obtained, returns `thrd_success`. If a timeout happens first, returns `thrd_timedout`.

> 如果一切正常，且获得互斥锁，则返回`thrd_success`。如果先超时，则返回`thrd_timedout`。


Otherwise, returns `thrd_error`. Because if nothing is right, everything is wrong.

> 如果没有什么是正确的，那么一切都是错误的，否则返回`thrd_error`。

### Example {#example-210 .unnumbered .unlisted}


This example has a thread wait on a mutex for a maximum of 1.75 seconds. And it always times out because no one ever sends a signal.

> 这个例子有一个线程在互斥量上等待最多1.75秒。它总是超时，因为没有人发出信号。

::: {#cb713 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <time.h>
#include <threads.h>

mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    struct timespec ts;

    // Get the time now
    timespec_get(&ts, TIME_UTC);

    // Add on 1.75 seconds from now
    ts.tv_sec += 1;
    ts.tv_nsec += 750000000L;

    // Handle nsec overflow
    ts.tv_sec += ts.tv_nsec / 1000000000L;
    ts.tv_nsec = ts.tv_nsec % 1000000000L;

    printf("Thread: waiting for lock...\n");
    int r = mtx_timedlock(&mutex, &ts);

    switch (r) {
        case thrd_success:
            printf("Thread: grabbed lock!\n");
            break;

        case thrd_timedout:
            printf("Thread: timed out!\n");
            break;

        case thrd_error:
            printf("Thread: Some kind of error\n");
            break;
    }

    mtx_unlock(&mutex);

    return 0;
}

int main(void)
{
    thrd_t t;

    mtx_init(&mutex, mtx_plain);

    mtx_lock(&mutex);

    printf("Main creating thread\n");
    thrd_create(&t, run, NULL);

    // Sleep 3s to allow the other thread to timeout
    thrd_sleep(&(struct timespec){.tv_sec=3}, NULL);

    mtx_unlock(&mutex);

    thrd_join(t, NULL);

    mtx_destroy(&mutex);
}
```
:::

Output:

::: {#cb714 .sourceCode}
``` {.sourceCode .default}
Main creating thread
Thread: waiting for lock...
Thread: timed out!
```
:::

### See Also {#see-also-196 .unnumbered .unlisted}


[`mtx_lock()`](threads.html#man-mtx_lock), [`mtx_trylock()`](threads.html#man-mtx_trylock), [`timespec_get()`](time.html#man-timespec_get)

> [`mtx_lock()`](threads.html#man-mtx_lock)：锁定互斥锁
[`mtx_trylock()`](threads.html#man-mtx_trylock)：尝试锁定互斥锁
[`timespec_get()`](time.html#man-timespec_get)：获取当前时间

------------------------------------------------------------------------

## [27.12]{.header-section-number} `mtx_trylock()` {#man-mtx_trylock number="27.12"}

Try to lock a mutex, returning if not possible

### Synopsis {#synopsis-209 .unnumbered .unlisted}

::: {#cb715 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int mtx_trylock(mtx_t *mtx);
```
:::

### Description {#description-209 .unnumbered .unlisted}


This works just like [`mtx_lock`](threads.html#man-mtx_lock) except that it returns instantly if a lock can't be obtained.

> 这和[`mtx_lock`](threads.html#man-mtx_lock)的工作方式一样，只是如果无法获得锁，它会立即返回。


The spec notes that there's a chance that `mtx_trylock()` might spuriously fail with `thrd_busy` even if there are no other threads holding the lock. I'm not sure why this is, but you should defensively code against it.

> 规格说明中提到，即使没有其他线程持有锁，`mtx_trylock()` 也有可能会伪失败，返回 `thrd_busy`。我不确定为什么会这样，但是你应该做好防御性编码以防止这种情况发生。

### Return Value {#return-value-207 .unnumbered .unlisted}


Returns `thrd_success` if all's well. Or `thrd_busy` if some other thread holds the lock. Or `thrd_error`, which means something went right. I mean "wrong".

> 如果一切正常，则返回`thrd_success`。如果其他线程持有锁，则返回`thrd_busy`。如果出现错误，则返回`thrd_error`，这意味着出现了错误。

### Example {#example-211 .unnumbered .unlisted}

::: {#cb716 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <time.h>
#include <threads.h>

mtx_t mutex;

int run(void *arg)
{
    int id = *(int*)arg;

    int r = mtx_trylock(&mutex);   // <-- TRY TO GRAB THE LOCK

    switch (r) {
        case thrd_success:
            printf("Thread %d: grabbed lock!\n", id);
            break;

        case thrd_busy:
            printf("Thread %d: lock already taken :(\n", id);
            return 1;

        case thrd_error:
            printf("Thread %d: Some kind of error\n", id);
            return 2;
    }

    mtx_unlock(&mutex);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];
    int id[THREAD_COUNT];

    mtx_init(&mutex, mtx_plain);

    for (int i = 0; i < THREAD_COUNT; i++) {
        id[i] = i;
        thrd_create(t + i, run, id + i);
    }

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);

    mtx_destroy(&mutex);
}
```
:::

Output (varies by run):

::: {#cb717 .sourceCode}
``` {.sourceCode .default}
Thread 0: grabbed lock!
Thread 1: lock already taken :(
Thread 4: lock already taken :(
Thread 3: grabbed lock!
Thread 2: lock already taken :(
```
:::

### See Also {#see-also-197 .unnumbered .unlisted}


[`mtx_lock()`](threads.html#man-mtx_lock), [`mtx_timedlock()`](threads.html#man-mtx_timedlock), [`mtx_unlock()`](threads.html#man-mtx_unlock)

> `mtx_lock()`：锁定互斥体
`mtx_timedlock()`：在指定时间内锁定互斥体
`mtx_unlock()`：解锁互斥体

------------------------------------------------------------------------

## [27.13]{.header-section-number} `mtx_unlock()` {#man-mtx_unlock number="27.13"}

Free a mutex when you're done with the critical section

### Synopsis {#synopsis-210 .unnumbered .unlisted}

::: {#cb718 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int mtx_unlock(mtx_t *mtx);
```
:::

### Description {#description-210 .unnumbered .unlisted}


After you've done all the dangerous stuff you have to do, wherein the involved threads should not be stepping on each other's toes... you can free up your stranglehold on the mutex by calling `mtx_unlock()`.

> 在你完成了所有危险的事情之后，其中涉及的线程不应该互相干扰... 你可以通过调用`mtx_unlock()`来释放你对互斥量的控制。

### Return Value {#return-value-208 .unnumbered .unlisted}


Returns `thrd_success` on success. Or `thrd_error` on error. It's not very original in this regard.

> 如果成功，返回`thrd_success`。如果失败，返回`thrd_error`。在这方面，它并不是很原创。

### Example {#example-212 .unnumbered .unlisted}


General-purpose mutex example here, but you can see the `mtx_unlock()` in the `run()` function:

> 一个通用的互斥锁示例，你可以在`run()`函数中看到`mtx_unlock()`。

::: {#cb719 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

cnd_t condvar;
mtx_t mutex;

int run(void *arg)
{
    (void)arg;

    static int count = 0;

    mtx_lock(&mutex);

    printf("Thread: I got %d!\n", count);
    count++;

    mtx_unlock(&mutex);  // <-- UNLOCK HERE

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    mtx_init(&mutex, mtx_plain);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, NULL);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);

    mtx_destroy(&mutex);
}
```
:::

Output:

::: {#cb720 .sourceCode}
``` {.sourceCode .default}
Thread: I got 0!
Thread: I got 1!
Thread: I got 2!
Thread: I got 3!
Thread: I got 4!
```
:::

### See Also {#see-also-198 .unnumbered .unlisted}


[`mtx_lock()`](threads.html#man-mtx_lock), [`mtx_timedlock()`](threads.html#man-mtx_timedlock), [`mtx_trylock()`](threads.html#man-mtx_trylock)

> `mtx_lock()`：锁定互斥锁
`mtx_timedlock()`：在指定的时间内尝试锁定互斥锁
`mtx_trylock()`：尝试锁定互斥锁

------------------------------------------------------------------------

## [27.14]{.header-section-number} `thrd_create()` {#man-thrd_create number="27.14"}

Create a new thread of execution

### Synopsis {#synopsis-211 .unnumbered .unlisted}

::: {#cb721 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int thrd_create(thrd_t *thr, thrd_start_t func, void *arg);
```
:::

### Description {#description-211 .unnumbered .unlisted}

Now *you* have the POWER!

Right?


This is how you launch new threads to make your program do multiple things at once[^66^](footnotes.html#fn66){#fnref66 .footnote-ref role="doc-noteref"}!

> 这就是你如何启动新线程，让你的程序同时完成多件事情！[^66^](footnotes.html#fn66){#fnref66 .footnote-ref role="doc-noteref"}


In order to make this happen, you need to pass a pointer to a `thrd_t` that will be used to represent the thread you're spawning.

> 要实现这一点，你需要传递一个指向`thrd_t`的指针，用来表示你要创建的线程。


That thread will start running the function you pass a pointer to in `func`. This is a value of type `thrd_start_t`, which is a pointer to a function that returns an `int` and takes a single `void*` as a parameter, i.e.:

> 那个线程将开始运行您传递指针到`func`中的函数。这是一个`thrd_start_t`类型的值，它是一个指向一个返回`int`并以单个`void *`作为参数的函数的指针，即：

::: {#cb722 .sourceCode}
``` {.sourceCode .c}
int thread_run_func(void *arg)
```
:::


And, as you might have guessed, the pointer you pass to `thrd_create()` for the `arg` parameter is passed on to the `func` function. This is how you can give additional information to the thread when it starts up.

> 当你传递给`thrd_create()`的指针作为`arg`参数，你可能已经猜到，这个指针会被传递给`func`函数。这就是你在线程启动时给它传递额外信息的方式。


Of course, for `arg`, you have to be sure to pass a pointer to an object that is thread-safe or per-thread.

> 当然，对于`arg`，你必须确保传递一个指向线程安全或每个线程的对象的指针。


If the thread returns from the function, it exits just as if it had called `thrd_exit()`.

> 如果线程从函数返回，它就会像调用`thrd_exit()`一样退出。


Finally, the value that the `func` function returns can be picked up by the parent thread with `thrd_join()`.

> 最后，父线程可以通过`thrd_join（）`捕获`func`函数返回的值。

### Return Value {#return-value-209 .unnumbered .unlisted}


In the case of goodness, returns `thrd_success`. If you're out of memory, will return `thrd_nomem`. Otherwise, `thrd_error`.

> 在善良的情况下，返回`thrd_success`。如果您没有内存，将返回`thrd_nomem`。否则，`thrd_error`。

### Example {#example-213 .unnumbered .unlisted}

::: {#cb723 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

int run(void *arg)
{
    int id = *(int*)arg;

    printf("Thread %d: I'm alive!!\n", id);

    return id;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];
    int id[THREAD_COUNT];  // One of these per thread

    for (int i = 0; i < THREAD_COUNT; i++) {
        id[i] = i; // Let's pass in the thread number as the ID
        thrd_create(t + i, run, id + i);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        int res;

        thrd_join(t[i], &res);

        printf("Main: thread %d exited with code %d\n", i, res);
    }
}
```
:::

Output (might vary from run to run):

::: {#cb724 .sourceCode}
``` {.sourceCode .default}
Thread 1: I'm alive!!
Thread 0: I'm alive!!
Thread 3: I'm alive!!
Thread 2: I'm alive!!
Main: thread 0 exited with code 0
Main: thread 1 exited with code 1
Main: thread 2 exited with code 2
Main: thread 3 exited with code 3
Thread 4: I'm alive!!
Main: thread 4 exited with code 4
```
:::

### See Also {#see-also-199 .unnumbered .unlisted}


[`thrd_exit()`](threads.html#man-thrd_exit), [`thrd_join()`](threads.html#man-thrd_join)

> `thrd_exit()`：线程退出
`thrd_join()`：线程加入

------------------------------------------------------------------------

## [27.15]{.header-section-number} `thrd_current()` {#man-thrd_current number="27.15"}

Get the ID of the calling thread

### Synopsis {#synopsis-212 .unnumbered .unlisted}

::: {#cb725 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

thrd_t thrd_current(void);
```
:::

### Description {#description-212 .unnumbered .unlisted}


Each thread has an opaque ID of type `thrd_t`. This is the value we see get initialized when we call [`thrd_create()`](threads.html#man-thrd_create).

> 每个线程都有一个类型为`thrd_t`的不透明ID。这就是我们在调用[`thrd_create()`](threads.html#man-thrd_create)时看到的初始化值。

But what if you want to get the ID of the currently running thread?

No problem! Just call this function and it will be returned to you.

Why? Who knows!

Well, to be honest, I could see it being used a couple places.


1.  You could use it to have a thread detach itself with `thrd_detach()`. I'm not sure why you'd want to do this, however.

> 你可以用它来使线程脱离自身，使用`thrd_detach()`。但我不确定你为什么要这么做。

2.  You could use it to compare this thread's ID with another you have stored in a variable somewhere by using the `thrd_equal()` function. Seems like the most legit use.

> 你可以用它来比较这个线程ID与另一个你存储在某个变量中的线程ID，使用`thrd_equal()`函数。似乎是最合法的用法。
3.  ...
4.  Profit!

If anyone has another use, please let me know.

### Return Value {#return-value-210 .unnumbered .unlisted}

Returns the calling thread's ID.

### Example {#example-214 .unnumbered .unlisted}


Here's a general example that shows getting the current thread ID and comparing it to a previously-recorded thread ID and taking exciting action based on the result! Starring Arnold Schwarzenegger!

> 这里有一个示例，它展示了如何获取当前线程ID并将其与先前记录的线程ID进行比较，并根据结果采取令人兴奋的行动！由阿诺德·施瓦辛格主演！

::: {#cb726 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

thrd_t first_thread_id;

int run(void *arg)
{
    (void)arg;

    thrd_t my_id = thrd_current();   // <-- GET MY THREAD ID

    if (thrd_equal(my_id, first_thread_id))
        printf("I'm the first thread!\n");
    else
        printf("I'm not the first!\n");

    return 0;
}

int main(void)
{
    thrd_t t;

    thrd_create(&first_thread_id, run, NULL);
    thrd_create(&t, run, NULL);

    thrd_join(first_thread_id, NULL);
    thrd_join(t, NULL);
}
```
:::

Output:

::: {#cb727 .sourceCode}
``` {.sourceCode .default}
Come on, you got what you want, Cohaagen! Give deez people ay-ah!
```
:::


No, wait, that's an Arnold Schwarzenegger quote from *Total Recall*, one of the best science fiction films of all time. Watch it now and then come back to finish this reference page.

> 不，等等，那是阿诺德·施瓦辛格在《回忆总动员》中的一句台词，是所有时代最好的科幻电影之一。现在就去看看，然后回来完成这个参考页面。

Man--what an ending! And Johnny Cab? So excellent. Anyway!

Output:

::: {#cb728 .sourceCode}
``` {.sourceCode .default}
I'm the first thread!
I'm not the first!
```
:::

### See Also {#see-also-200 .unnumbered .unlisted}


[`thrd_equal()`](threads.html#man-thrd_equal), [`thrd_detach()`](threads.html#man-thrd_detach)

> `thrd_equal()`：比较两个线程是否相同
`thrd_detach()`：分离线程

------------------------------------------------------------------------

## [27.16]{.header-section-number} `thrd_detach()` {#man-thrd_detach number="27.16"}

Automatically clean up threads when they exit

### Synopsis {#synopsis-213 .unnumbered .unlisted}

::: {#cb729 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int thrd_detach(thrd_t thr);
```
:::

### Description {#description-213 .unnumbered .unlisted}


Normally you have to `thrd_join()` to get resources associated with a deceased thread cleaned up. (Most notably, its exit status is still floating around waiting to get picked up.)

> 一般来说，你必须调用`thrd_join()`来清理与已经终止的线程相关的资源（最显著的是，它的退出状态仍然存在，等待被捕获）。


But if you call `thrd_detach()` on the thread first, manual cleanup isn't necessary. They just exit and are cleaned up by the OS.

> 如果你先调用thrd_detach()函数，就不需要手动清理了。它们只是退出，然后由操作系统进行清理。

(Note that when the main thread dies, all the threads die in any case.)

### Return Value {#return-value-211 .unnumbered .unlisted}

`thrd_success` if the thread successfully detaches, `thrd_error` otherwise.

### Example {#example-215 .unnumbered .unlisted}

::: {#cb730 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

thrd_t first_thread_id;

int run(void *arg)
{
    (void)arg;

    printf("Thread running!\n");

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t;

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_create(&t, run, NULL);
        thrd_detach(t);
    }

    // No need to thrd_join()!

    // Sleep a quarter second to let them all finish
    thrd_sleep(&(struct timespec){.tv_nsec=250000000}, NULL);
}
```
:::

### See Also {#see-also-201 .unnumbered .unlisted}


[`thrd_join()`](threads.html#man-thrd_join), [`thrd_exit()`](threads.html#man-thrd_exit)

> `thrd_join()`：等待线程结束，并获取其返回值
`thrd_exit()`：终止当前线程并返回一个值

------------------------------------------------------------------------

## [27.17]{.header-section-number} `thrd_equal()` {#man-thrd_equal number="27.17"}

Compare two thread descriptors for equality

### Synopsis {#synopsis-214 .unnumbered .unlisted}

::: {#cb731 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int thrd_equal(thrd_t thr0, thrd_t thr1);
```
:::

### Description {#description-214 .unnumbered .unlisted}


If you have two thread descriptors in `thrd_t` variables, you can test them for equality with this function.

> 如果你有两个`thrd_t`变量中的线程描述符，你可以使用这个函数来测试它们的相等性。


For example, maybe one of the threads has special powers the others don't, and the run function needs to be able to tell them apart, as in the example.

> 例如，也许其中一个线程拥有其他线程所不具备的特殊功能，而运行函数需要能够将它们区分开来，就像示例中那样。

### Return Value {#return-value-212 .unnumbered .unlisted}

Returns non-zero if the threads are equal. Returns `0` if they're not.

### Example {#example-216 .unnumbered .unlisted}


Here's a general example that shows getting the current thread ID and comparing it to a previously-recorded thread ID and taking boring action based on the result.

> 这里有一个示例，它展示了获取当前线程ID并将其与先前记录的线程ID进行比较，并根据结果采取乏味的行动。

::: {#cb732 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

thrd_t first_thread_id;

int run(void *arg)
{
    (void)arg;

    thrd_t my_id = thrd_current();

    if (thrd_equal(my_id, first_thread_id))  // <-- COMPARE!
        printf("I'm the first thread!\n");
    else
        printf("I'm not the first!\n");

    return 0;
}

int main(void)
{
    thrd_t t;

    thrd_create(&first_thread_id, run, NULL);
    thrd_create(&t, run, NULL);

    thrd_join(first_thread_id, NULL);
    thrd_join(t, NULL);
}
```
:::

Output:

::: {#cb733 .sourceCode}
``` {.sourceCode .default}
I'm the first thread!
I'm not the first!
```
:::

### See Also {#see-also-202 .unnumbered .unlisted}

[`thrd_current()`](threads.html#man-thrd_current)

------------------------------------------------------------------------

## [27.18]{.header-section-number} `thrd_exit()` {#man-thrd_exit number="27.18"}

Stop and exit this thread

### Synopsis {#synopsis-215 .unnumbered .unlisted}

::: {#cb734 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

_Noreturn void thrd_exit(int res);
```
:::

### Description {#description-215 .unnumbered .unlisted}


A thread commonly exits by returning from its run function. But if it wants to exit early (perhaps from deeper in the call stack), this function will get that done.

> 一个线程通常通过从其运行函数中返回来退出。但是如果它想提前退出（可能是从调用堆栈更深处），这个函数将会完成这项工作。


The `res` code can be picked up by a thread calling `thrd_join()`, and is equivalent to returning a value from the run function.

> 线程调用`thrd_join()`可以捡起`res`代码，相当于从运行函数中返回一个值。


Like with returning from the run function, this will also properly clean up all the thread-specific storage associated with this thread---all the destructors for the threads TSS variables will be called. If there are any remaining TSS variables with destructors after the first round of destruction[^67^](footnotes.html#fn67){#fnref67 .footnote-ref role="doc-noteref"}, the remaining destructors will be called. This happens repeatedly until there are no more, or the number of rounds of carnage reaches `TSS_DTOR_ITERATIONS`.

> 就像从运行函数返回一样，这也将正确清理与此线程相关的所有线程特定存储---将调用线程TSS变量的所有析构函数。如果在第一轮析构[^67^](footnotes.html#fn67){#fnref67 .footnote-ref role="doc-noteref"}之后还有具有析构函数的剩余TSS变量，则将调用剩余的析构函数。这将反复发生，直到没有更多，或者残杀回合数达到`TSS_DTOR_ITERATIONS`。


If the main thread calls this, it's as if you called `exit(EXIT_SUCCESS)`.

> 如果主线程调用这个，就好像你调用了`exit(EXIT_SUCCESS)`一样。

### Return Value {#return-value-213 .unnumbered .unlisted}


This function never returns because the thread calling it is killed in the process. Trippy!

> 这个函数永远不会返回，因为调用它的线程在过程中被杀死。真神奇！

### Example {#example-217 .unnumbered .unlisted}


Threads in this example exit early with result `22` if they get a `NULL` value for `arg`.

> 在这个例子中，如果线程获得一个空值作为参数，它们将以结果`22`提前退出。

::: {#cb735 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

thrd_t first_thread_id;

int run(void *arg)
{
    (void)arg;

    if (arg == NULL)
        thrd_exit(22);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, i == 2? NULL: "spatula");


    for (int i = 0; i < THREAD_COUNT; i++) {
        int res;
        thrd_join(t[i], &res);

        printf("Thread %d exited with code %d\n", i, res);
    }
}
```
:::

Output:

::: {#cb736 .sourceCode}
``` {.sourceCode .default}
Thread 0 exited with code 0
Thread 1 exited with code 0
Thread 2 exited with code 22
Thread 3 exited with code 0
Thread 4 exited with code 0
```
:::

### See Also {#see-also-203 .unnumbered .unlisted}

[`thrd_join()`](threads.html#man-thrd_join)

------------------------------------------------------------------------

## [27.19]{.header-section-number} `thrd_join()` {#man-thrd_join number="27.19"}

Wait for a thread to exit

### Synopsis {#synopsis-216 .unnumbered .unlisted}

::: {#cb737 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int thrd_join(thrd_t thr, int *res);
```
:::

### Description {#description-216 .unnumbered .unlisted}


When a parent thread fires off some child threads, it can wait for them to complete with this call

> 当父线程发起一些子线程时，它可以通过这个调用等待它们完成。

### Return Value {#return-value-214 .unnumbered .unlisted}

### Example {#example-218 .unnumbered .unlisted}


Threads in this example exit early with result `22` if they get a `NULL` value for `arg`. The parent thread picks up this result code with `thrd_join()`.

> 在这个例子中，如果线程收到一个`NULL`值作为`arg`，它们将提前以结果码`22`退出。父线程使用`thrd_join()`来捕获这个结果码。

::: {#cb738 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

thrd_t first_thread_id;

int run(void *arg)
{
    (void)arg;

    if (arg == NULL)
        thrd_exit(22);

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, i == 2? NULL: "spatula");


    for (int i = 0; i < THREAD_COUNT; i++) {
        int res;
        thrd_join(t[i], &res);

        printf("Thread %d exited with code %d\n", i, res);
    }
}
```
:::

Output:

::: {#cb739 .sourceCode}
``` {.sourceCode .default}
Thread 0 exited with code 0
Thread 1 exited with code 0
Thread 2 exited with code 22
Thread 3 exited with code 0
Thread 4 exited with code 0
```
:::

### See Also {#see-also-204 .unnumbered .unlisted}

[`thrd_exit()`](threads.html#man-thrd_exit)

## [27.20]{.header-section-number} `thrd_sleep()` {#man-thrd_sleep number="27.20"}

Sleep for a specific number of seconds and nanoseconds

### Synopsis {#synopsis-217 .unnumbered .unlisted}

::: {#cb740 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int thrd_sleep(const struct timespec *duration, struct timespec *remaining);
```
:::

### Description {#description-217 .unnumbered .unlisted}


This function puts the current thread to sleep for a while[^68^](footnotes.html#fn68){#fnref68 .footnote-ref role="doc-noteref"} allowing other threads to run.

> 这个函数使当前线程休眠一段时间[^68^]（脚注.html#fn68）{#fnref68 .footnote-ref role="doc-noteref"}，以便允许其他线程运行。


The calling thread will wake up after the time has elapsed, or if it gets interrupted by a signal or something.

> 调用线程将在时间过去后唤醒，或者如果它被信号或其他东西打断。


If it doesn't get interrupted, it'll sleep at least as long as you asked. Maybe a tad longer. You know how hard it can be to get out of bed.

> 如果没有被打断，它至少会睡多久，正如你所要求的。也许会稍微长一点。你知道起床有多难。

The structure looks like this:

::: {#cb741 .sourceCode}
``` {.sourceCode .c}
struct timespec {
    time_t tv_sec;   // Seconds
    long   tv_nsec;  // Nanoseconds (billionths of a second)
};
```
:::


Don't set `tv_nsec` greater than 999,999,999. I can't see what officially happens if you do, but on my system `thrd_sleep()` returns `-2` and fails.

> 不要将`tv_nsec`设置为大于999,999,999。我无法看到如果你这样做会发生什么，但是在我的系统上，`thrd_sleep()`会返回`-2`并失败。

### Return Value {#return-value-215 .unnumbered .unlisted}


Returns `0` on timeout, or `-1` if interrupted by a signal. Or any negative value on some other error. Weirdly, the spec allows this "other error negative value" to also be `-1`, so good luck with that.

> 超时会返回`0`，如果被信号中断则返回`-1`，其他错误则会返回负值。奇怪的是，规范允许这个"其他错误负值"也可以是`-1`，祝你好运。

### Example {#example-219 .unnumbered .unlisted}

::: {#cb742 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

int main(void)
{
    // Sleep for 3.25 seconds
    thrd_sleep(&(struct timespec){.tv_sec=3, .tv_nsec=250000000}, NULL);

    return 0;
}
```
:::

### See Also {#see-also-205 .unnumbered .unlisted}

[`thrd_yield()`](threads.html#man-thrd_yield)

------------------------------------------------------------------------

## [27.21]{.header-section-number} `thrd_yield()` {#man-thrd_yield number="27.21"}

Stop running that other threads might run

### Synopsis {#synopsis-218 .unnumbered .unlisted}

::: {#cb743 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

void thrd_yield(void);
```
:::

### Description {#description-218 .unnumbered .unlisted}


If you have a thread that's hogging the CPU and you want to give your other threads time to run, you can call `thrd_yield()`. If the system sees fit, it will put the calling thread to sleep and one of the other threads will run instead.

> 如果有一个线程占用了CPU，你想给其他线程更多的运行时间，你可以调用`thrd_yield()`。如果系统认为合适，它会把调用线程放入睡眠，其他线程就可以运行了。


It's a good way to be "polite" to the other threads in your program if you want the encourage them to run instead.

> 这是一个很好的方式，如果你想鼓励程序中的其他线程运行，就要“礼貌”地对待它们。

### Return Value {#return-value-216 .unnumbered .unlisted}

Returns nothing!

### Example {#example-220 .unnumbered .unlisted}


This example's kinda poor because the OS is probably going to reschedule threads on the output anyway, but it gets the point across.

> 这个例子有点糟糕，因为操作系统可能会在输出上重新调度线程，但它已经说明了问题。


The main thread is giving other threads a chance to run after every block of dumb work it does.

> 主线程在做完一块愚蠢的工作之后，会给其他线程一个机会去运行。

::: {#cb744 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

int run(void *arg)
{
    int main_thread = arg != NULL;

    if (main_thread) {
        long int total = 0;

        for (int i = 0; i < 10; i++) {
            for (long int j = 0; j < 1000L; j++)
                total++;

            printf("Main thread yielding\n");
            thrd_yield();                       // <-- YIELD HERE
        }
    } else
        printf("Other thread running!\n");

    return 0;
}

#define THREAD_COUNT 10

int main(void)
{
    thrd_t t[THREAD_COUNT];

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_create(t + i, run, i == 0? "main": NULL);

    for (int i = 0; i < THREAD_COUNT; i++)
        thrd_join(t[i], NULL);

    return 0;
}
```
:::


The output will vary from run to run. Notice that even after `thrd_yield()` other threads might not yet be ready to run and the main thread will continue.

> 输出每次运行都会有所不同。注意，即使在`thrd_yield()`之后，其他线程可能还没有准备好运行，主线程也会继续运行。

::: {#cb745 .sourceCode}
``` {.sourceCode .default}
Main thread yielding
Main thread yielding
Main thread yielding
Other thread running!
Other thread running!
Other thread running!
Other thread running!
Main thread yielding
Other thread running!
Other thread running!
Main thread yielding
Main thread yielding
Main thread yielding
Other thread running!
Main thread yielding
Main thread yielding
Main thread yielding
Other thread running!
Other thread running!
```
:::

### See Also {#see-also-206 .unnumbered .unlisted}

[`thrd_sleep()`](threads.html#man-thrd_sleep)

------------------------------------------------------------------------

## [27.22]{.header-section-number} `tss_create()` {#man-tss_create number="27.22"}

Create new thread-specific storage

### Synopsis {#synopsis-219 .unnumbered .unlisted}

::: {#cb746 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int tss_create(tss_t *key, tss_dtor_t dtor);
```
:::

### Description {#description-219 .unnumbered .unlisted}

This helps when you need per-thread storage of different values.


A common place this comes up is if you have a file scope variable that is shared between a bunch of functions and often returned. That's not threadsafe. One way to refactor is to replace it with thread-specific storage so that each thread gets their own code and doesn't step on other thread's toes.

> 一个常见的地方就是，如果你有一个文件范围的变量被许多函数共享，而且经常被返回，那么这是不线程安全的。一种重构的方法是用线程特定的存储来替换它，这样每个线程就可以获得自己的代码，而不会干扰其他线程。


To make this work, you pass in a pointer to a `tss_t` key---this is the variable you will use in subsequent `tss_set()` and `tss_get()` calls to set and get the value associated with the key.

> 要使这个工作，你传入一个指向`tss_t`键的指针---这是你在随后的`tss_set()`和`tss_get()`调用中用来设置和获取与键关联的值的变量。


The interesting part of this is the `dtor` destructor pointer of type `tss_dtor_t`. This is actually a pointer to a function that takes a `void*` argument and returns `void`, i.e.

> 有趣的部分是`dtor`析构函数指针类型`tss_dtor_t`。实际上，这是一个接受`void*`参数并返回`void`的函数指针。

::: {#cb747 .sourceCode}
``` {.sourceCode .c}
void dtor(void *p) { ... }
```
:::


This function will be called per thread when the thread exits with `thrd_exit()` (or returns from the run function).

> 这个函数会在线程使用thrd_exit()（或从运行函数返回）退出时被每个线程调用。


It's unspecified behavior to call this function while other threads' destructors are running.

> 这个函数在其他线程的析构函数正在运行时调用是未指定的行为。

### Return Value {#return-value-217 .unnumbered .unlisted}

Returns nothing!

### Example {#example-221 .unnumbered .unlisted}


This is a general-purpose TSS example. Note the TSS variable is created near the top of `main()`.

> 这是一个通用的TSS示例。注意TSS变量是在`main()`的顶部创建的。

::: {#cb748 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

tss_t str;

void some_function(void)
{
    // Retrieve the per-thread value of this string
    char *tss_string = tss_get(str);

    // And print it
    printf("TSS string: %s\n", tss_string);
}

int run(void *arg)
{
    int serial = *(int*)arg;  // Get this thread's serial number
    free(arg);

    // malloc() space to hold the data for this thread
    char *s = malloc(64);
    sprintf(s, "thread %d! :)", serial);  // Happy little string

    // Set this TSS variable to point at the string
    tss_set(str, s);

    // Call a function that will get the variable
    some_function();

    return 0; // Equivalent to thrd_exit(0); fires destructors
}

#define THREAD_COUNT 15

int main(void)
{
    thrd_t t[THREAD_COUNT];

    // Make a new TSS variable, the free() function is the destructor
    tss_create(&str, free);                  // <-- CREATE TSS VAR!

    for (int i = 0; i < THREAD_COUNT; i++) {
        int *n = malloc(sizeof *n);  // Holds a thread serial number
        *n = i;
        thrd_create(t + i, run, n);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }

    // And all threads are done, so let's free this
    tss_delete(str);
}
```
:::

Output:

::: {#cb749 .sourceCode}
``` {.sourceCode .default}
TSS string: thread 0! :)
TSS string: thread 2! :)
TSS string: thread 1! :)
TSS string: thread 5! :)
TSS string: thread 3! :)
TSS string: thread 6! :)
TSS string: thread 4! :)
TSS string: thread 7! :)
TSS string: thread 8! :)
TSS string: thread 9! :)
TSS string: thread 10! :)
TSS string: thread 13! :)
TSS string: thread 12! :)
TSS string: thread 11! :)
TSS string: thread 14! :)
```
:::

### See Also {#see-also-207 .unnumbered .unlisted}


[`tss_delete()`](threads.html#man-tss_delete), [`tss_set()`](threads.html#man-tss_set), [`tss_get()`](threads.html#man-tss_get), [`thrd_exit()`](threads.html#man-thrd_exit)

> [`tss_delete()`](threads.html#man-tss_delete)：删除线程存储设置
[`tss_set()`](threads.html#man-tss_set)：设置线程存储
[`tss_get()`](threads.html#man-tss_get)：获取线程存储
[`thrd_exit()`](threads.html#man-thrd_exit)：线程退出

------------------------------------------------------------------------

## [27.23]{.header-section-number} `tss_delete()` {#man-tss_delete number="27.23"}

Clean up a thread-specific storage variable

### Synopsis {#synopsis-220 .unnumbered .unlisted}

::: {#cb750 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

void tss_delete(tss_t key);
```
:::

### Description {#description-220 .unnumbered .unlisted}


This is the opposite of `tss_create()`. You create (initialize) the TSS variable before using it, then, when all the threads are done that need it, you delete (deinitialize/free) it with this.

> 这是`tss_create()`的相反。在使用它之前，你需要先创建（初始化）TSS变量，然后，当所有需要它的线程完成后，你可以使用它来删除（反初始化/释放）它。

This doesn't call any destructors! Those are all called by `thrd_exit()`!

### Return Value {#return-value-218 .unnumbered .unlisted}

Returns nothing!

### Example {#example-222 .unnumbered .unlisted}


This is a general-purpose TSS example. Note the TSS variable is deleted near the bottom of `main()`.

> 这是一个通用的TSS示例。注意TSS变量在main（）的底部被删除。

::: {#cb751 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

tss_t str;

void some_function(void)
{
    // Retrieve the per-thread value of this string
    char *tss_string = tss_get(str);

    // And print it
    printf("TSS string: %s\n", tss_string);
}

int run(void *arg)
{
    int serial = *(int*)arg;  // Get this thread's serial number
    free(arg);

    // malloc() space to hold the data for this thread
    char *s = malloc(64);
    sprintf(s, "thread %d! :)", serial);  // Happy little string

    // Set this TSS variable to point at the string
    tss_set(str, s);

    // Call a function that will get the variable
    some_function();

    return 0; // Equivalent to thrd_exit(0); fires destructors
}

#define THREAD_COUNT 15

int main(void)
{
    thrd_t t[THREAD_COUNT];

    // Make a new TSS variable, the free() function is the destructor
    tss_create(&str, free);

    for (int i = 0; i < THREAD_COUNT; i++) {
        int *n = malloc(sizeof *n);  // Holds a thread serial number
        *n = i;
        thrd_create(t + i, run, n);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }

    // And all threads are done, so let's free this
    tss_delete(str);    // <-- DELETE TSS VARIABLE!
}
```
:::

Output:

::: {#cb752 .sourceCode}
``` {.sourceCode .default}
TSS string: thread 0! :)
TSS string: thread 2! :)
TSS string: thread 1! :)
TSS string: thread 5! :)
TSS string: thread 3! :)
TSS string: thread 6! :)
TSS string: thread 4! :)
TSS string: thread 7! :)
TSS string: thread 8! :)
TSS string: thread 9! :)
TSS string: thread 10! :)
TSS string: thread 13! :)
TSS string: thread 12! :)
TSS string: thread 11! :)
TSS string: thread 14! :)
```
:::

### See Also {#see-also-208 .unnumbered .unlisted}


[`tss_create()`](threads.html#man-tss_create), [`tss_set()`](threads.html#man-tss_set), [`tss_get()`](threads.html#man-tss_get), [`thrd_exit()`](threads.html#man-thrd_exit)

> [`tss_create()`](threads.html#man-tss_create)：创建线程特定存储（TSS）
[`tss_set()`](threads.html#man-tss_set)：设置线程特定存储（TSS）
[`tss_get()`](threads.html#man-tss_get)：获取线程特定存储（TSS）
[`thrd_exit()`](threads.html#man-thrd_exit)：终止线程

------------------------------------------------------------------------

## [27.24]{.header-section-number} `tss_get()` {#man-tss_get number="27.24"}

Get thread-specific data

### Synopsis {#synopsis-221 .unnumbered .unlisted}

::: {#cb753 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

void *tss_get(tss_t key);
```
:::

### Description {#description-221 .unnumbered .unlisted}


Once you've set a variable with `tss_set()`, you can retrieve the value with `tss_get()`---just pass in the key and you'll get a pointer to the value back.

> 一旦你使用`tss_set()`设置了一个变量，你就可以使用`tss_get()`来检索其值---只需传入键，就可以得到一个指向该值的指针。

Don't call this from a destructor.

### Return Value {#return-value-219 .unnumbered .unlisted}


Returns the value stored for the given `key`, or `NULL` if there's trouble.

> 返回给定`键`存储的值，如果出现问题则返回`NULL`。

### Example {#example-223 .unnumbered .unlisted}


This is a general-purpose TSS example. Note the TSS variable is retrieved in `some_function()`, below.

> 这是一个通用的TSS示例。请注意，TSS变量在下面的`some_function()`中被检索。

::: {#cb754 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

tss_t str;

void some_function(void)
{
    // Retrieve the per-thread value of this string
    char *tss_string = tss_get(str);    // <-- GET THE VALUE

    // And print it
    printf("TSS string: %s\n", tss_string);
}

int run(void *arg)
{
    int serial = *(int*)arg;  // Get this thread's serial number
    free(arg);

    // malloc() space to hold the data for this thread
    char *s = malloc(64);
    sprintf(s, "thread %d! :)", serial);  // Happy little string

    // Set this TSS variable to point at the string
    tss_set(str, s);

    // Call a function that will get the variable
    some_function();

    return 0; // Equivalent to thrd_exit(0); fires destructors
}

#define THREAD_COUNT 15

int main(void)
{
    thrd_t t[THREAD_COUNT];

    // Make a new TSS variable, the free() function is the destructor
    tss_create(&str, free);

    for (int i = 0; i < THREAD_COUNT; i++) {
        int *n = malloc(sizeof *n);  // Holds a thread serial number
        *n = i;
        thrd_create(t + i, run, n);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }

    // And all threads are done, so let's free this
    tss_delete(str);
}
```
:::

Output:

::: {#cb755 .sourceCode}
``` {.sourceCode .default}
TSS string: thread 0! :)
TSS string: thread 2! :)
TSS string: thread 1! :)
TSS string: thread 5! :)
TSS string: thread 3! :)
TSS string: thread 6! :)
TSS string: thread 4! :)
TSS string: thread 7! :)
TSS string: thread 8! :)
TSS string: thread 9! :)
TSS string: thread 10! :)
TSS string: thread 13! :)
TSS string: thread 12! :)
TSS string: thread 11! :)
TSS string: thread 14! :)
```
:::

### See Also {#see-also-209 .unnumbered .unlisted}

[`tss_set()`](threads.html#man-tss_set)

------------------------------------------------------------------------

## [27.25]{.header-section-number} `tss_set()` {#man-tss_set number="27.25"}

Set thread-specific data

### Synopsis {#synopsis-222 .unnumbered .unlisted}

::: {#cb756 .sourceCode}
``` {.sourceCode .c}
#include <threads.h>

int tss_set(tss_t key, void *val);
```
:::

### Description {#description-222 .unnumbered .unlisted}


Once you've set up your TSS variable with `tss_create()`, you can set it on a per thread basis with `tss_set()`.

> 一旦你用`tss_create()`设置了你的TSS变量，你可以通过`tss_set()`在每个线程上设置它。

`key` is the identifier for this data, and `val` is a pointer to it.


The destructor specified in `tss_create()` will be called for the value set when the thread exits.

> `tss_create()`中指定的析构函数将在线程退出时被调用，以释放设置的值。


Also, if there's a destructor *and* there is already at value for this key in place, the destructor will not be called for the already-existing value. In fact, this function will never cause a destructor to be called. So you're on your own, there---best clean up the old value before overwriting it with the new one.

> 如果有析构函数，并且此键已经有值，则不会为已存在的值调用析构函数。实际上，此函数永远不会导致调用析构函数。因此，您需要自行处理---最好在覆盖旧值之前清理旧值。

### Return Value {#return-value-220 .unnumbered .unlisted}

Returns `thrd_success` when happy, and `thrd_error` when not.

### Example {#example-224 .unnumbered .unlisted}


This is a general-purpose TSS example. Note the TSS variable is set in `run()`, below.

> 这是一个通用的TSS示例。请注意，TSS变量在下面的`run（）`中设置。

::: {#cb757 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

tss_t str;

void some_function(void)
{
    // Retrieve the per-thread value of this string
    char *tss_string = tss_get(str);

    // And print it
    printf("TSS string: %s\n", tss_string);
}

int run(void *arg)
{
    int serial = *(int*)arg;  // Get this thread's serial number
    free(arg);

    // malloc() space to hold the data for this thread
    char *s = malloc(64);
    sprintf(s, "thread %d! :)", serial);  // Happy little string

    // Set this TSS variable to point at the string
    tss_set(str, s);    // <-- SET THE TSS VARIABLE

    // Call a function that will get the variable
    some_function();

    return 0; // Equivalent to thrd_exit(0); fires destructors
}

#define THREAD_COUNT 15

int main(void)
{
    thrd_t t[THREAD_COUNT];

    // Make a new TSS variable, the free() function is the destructor
    tss_create(&str, free);

    for (int i = 0; i < THREAD_COUNT; i++) {
        int *n = malloc(sizeof *n);  // Holds a thread serial number
        *n = i;
        thrd_create(t + i, run, n);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }

    // And all threads are done, so let's free this
    tss_delete(str);
}
```
:::

Output:

::: {#cb758 .sourceCode}
``` {.sourceCode .default}
TSS string: thread 0! :)
TSS string: thread 2! :)
TSS string: thread 1! :)
TSS string: thread 5! :)
TSS string: thread 3! :)
TSS string: thread 6! :)
TSS string: thread 4! :)
TSS string: thread 7! :)
TSS string: thread 8! :)
TSS string: thread 9! :)
TSS string: thread 10! :)
TSS string: thread 13! :)
TSS string: thread 12! :)
TSS string: thread 11! :)
TSS string: thread 14! :)
```
:::

### See Also {#see-also-210 .unnumbered .unlisted}

[`tss_get()`](threads.html#man-tss_get)

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](tgmath.html) \| [Contents](index.html) \| [Next](time.html)
:::
