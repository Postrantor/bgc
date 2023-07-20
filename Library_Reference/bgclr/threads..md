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
  Function                                              Description
  ----------------------------------------------------- ----------------------------------------------------------
  [`call_once()`](threads.html#man-call_once)           Call a function one time no matter how many threads try

  [`cnd_broadcast()`](threads.html#man-cnd_broadcast)   Wake up all threads waiting on a condition variable

  [`cnd_destroy()`](threads.html#man-cnd_destroy)       Free up resources from a condition variable

  [`cnd_init()`](threads.html#man-cnd_init)             Initialize a condition variable to make it ready for use

  [`cnd_signal()`](threads.html#man-cnd_signal)         Wake up a thread waiting on a condition variable

  [`cnd_timedwait()`](threads.html#man-cnd_timedwait)   Wait on a condition variable with a timeout

  [`cnd_wait()`](threads.html#man-cnd_wait)             Wait for a signal on a condition variable

  [`mtx_destroy()`](threads.html#man-mtx_destroy)       Cleanup a mutex when done with it

  [`mtx_init()`](threads.html#man-mtx_init)             Initialize a mutex for use

  [`mtx_lock()`](threads.html#man-mtx_lock)             Acquire a lock on a mutex

  [`mtx_timedlock()`](threads.html#man-mtx_timedlock)   Lock a mutex allowing for timeout

  [`mtx_trylock()`](threads.html#man-mtx_trylock)       Try to lock a mutex, returning if not possible

  [`mtx_unlock()`](threads.html#man-mtx_unlock)         Free a mutex when you're done with the critical section

  [`thrd_create()`](threads.html#man-thrd_create)       Create a new thread of execution

  [`thrd_current()`](threads.html#man-thrd_current)     Get the ID of the calling thread

  [`thrd_detach()`](threads.html#man-thrd_detach)       Automatically clean up threads when they exit

  [`thrd_equal()`](threads.html#man-thrd_equal)         Compare two thread descriptors for equality

  [`thrd_exit()`](threads.html#man-thrd_exit)           Stop and exit this thread

  [`thrd_join()`](threads.html#man-thrd_join)           Wait for a thread to exit

  [`thrd_yield()`](threads.html#man-thrd_yield)         Stop running that other threads might run

  [`tss_create()`](threads.html#man-tss_create)         Create new thread-specific storage

  [`tss_delete()`](threads.html#man-tss_delete)         Clean up a thread-specific storage variable

  [`tss_get()`](threads.html#man-tss_get)               Get thread-specific data

  [`tss_set()`](threads.html#man-tss_set)               Set thread-specific data
  ----------------------------------------------------------------------------------------------------------------

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

The catch is the function that is called doesn't return anything and takes no arguments.

If you need more than that, you'll have to set a threadsafe flag such as `atomic_flag`, or one that you protect with a mutex.

To use this, you need to pass it a pointer to a function to execute, `func`, and also a pointer to a flag of type `once_flag`.

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

Of course, only one will get the mutex, and the rest will have to wait their turn. But instead of being asleep waiting for a signal, they'll be asleep waiting to reacquire the mutex. They're rearin' to go, in other words.

This can make a difference in a specific set of circumstances where `cnd_signal()` might leave you hanging.

If you're relying on subsequent threads to issue the next `cnd_signal()`, but you have the `cnd_wait()` in a `while` loop[^65^](footnotes.html#fn65){#fnref65 .footnote-ref role="doc-noteref"} that doesn't allow any threads to escape, you'll be stuck. No more threads will be woken up from the wait.

But if you `cnd_broadcast()`, all the threads will be woken, and presumably at least one of them will be allowed to escape the `while` loop, freeing it up to broadcast the next wakeup when its work is done.

### Return Value {#return-value-197 .unnumbered .unlisted}

Returns `thrd_success` or `thrd_error` depending on how well things went.

### Example {#example-201 .unnumbered .unlisted}

In the example below, we launch a bunch of threads, but they're only allowed to run if their ID matches the current ID. If it doesn't, they go back to waiting.

If you `cnd_signal()` to wake the next thread, it might not be the one with the proper ID to run. If it's not, it goes back to sleep and we hang (because no thread is awake to hit `cnd_signal()` again).

But if you `cnd_broadcast()` to wake them all, then they'll all try (one after another) to get out of the `while` loop. And one of them will make it.

Try switching the `cnd_broadcast()` to `cnd_signal()` to see likely deadlocks. It doesn't happen every time, but usually does.

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

### See Also {#see-also-187 .unnumbered .unlisted}

[`cnd_signal()`](signal.html#man-signal), [`mtx_lock()`](threads.html#man-mtx_lock), [`mtx_unlock()`](threads.html#man-mtx_unlock)

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

### Return Value {#return-value-198 .unnumbered .unlisted}

Returns nothing!

### Example {#example-202 .unnumbered .unlisted}

General-purpose condition variable example here, but you can see the `cnd_destroy()` down at the end.

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

Don't use a condition variable without calling this first!

### Return Value {#return-value-199 .unnumbered .unlisted}

If all goes well, returns `thrd_success`. It all doesn't go well, it could return `thrd_nomem` if the system is out of memory, or `thread_error` in the case of any other error.

### Example {#example-203 .unnumbered .unlisted}

General-purpose condition variable example here, but you can see the `cnd_init()` down at the start of `main()`.

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

Compare to `cnd_broadcast()` that wakes up all the threads. See the [`cnd_broadcast()`](threads.html#man-cnd_broadcast) page for more information on when you're want to use that versus this.

### Return Value {#return-value-200 .unnumbered .unlisted}

Returns `thrd_success` or `thrd_error` depending on how happy your program is.

### Example {#example-204 .unnumbered .unlisted}

General-purpose condition variable example here, but you can see the `cnd_signal()` in the middle of `main()`.

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

Note that the thread still must reacquire the mutex to get more work done even after the timeout. The the main difference is that regular `cnd_wait()` will only try to get the mutex after a `cnd_signal()` or `cnd_broadcast()`, whereas `cnd_timedwait()` will do that, too, **and** try to get the mutex after the timeout.

The timeout is specified as an absolute UTC time since Epoch. You can get this with the [`timespec_get()`](time.html#man-timespec_get) function and then add values on to the result to timeout later than now, as shown in the example.

Beware that you can't have more than 999999999 nanoseconds in the `tv_nsec` field of the `struct timespec`. Mod those so they stay in range.

### Return Value {#return-value-201 .unnumbered .unlisted}

If the thread wakes up for a non-timeout reason (e.g. signal or broadcast), returns `thrd_success`. If woken up due to timeout, returns `thrd_timedout`. Otherwise returns `thrd_error`.

### Example {#example-205 .unnumbered .unlisted}

This example has a thread wait on a condition variable for a maximum of 1.75 seconds. And it always times out because no one ever sends a signal. Tragic.

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

### Return Value {#return-value-202 .unnumbered .unlisted}

If everything's fantastic, returns `thrd_success`. Otherwise it returns `thrd_error` to report that something has gone fantastically, horribly awry.

### Example {#example-206 .unnumbered .unlisted}

General-purpose condition variable example here, but you can see the `cnd_wait()` in the `run()` function.

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

You should call this when all threads are done using the mutex.

### Return Value {#return-value-203 .unnumbered .unlisted}

Returns nothing, the selfish ingrate!

### Example {#example-207 .unnumbered .unlisted}

General-purpose mutex example here, but you can see the `mtx_destroy()` down at the end.

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

But wait! It's not quite that simple. You have to tell it what `type` of mutex you want to create.

  Type                        Description
  --------------------------- ----------------------------------------
  `mtx_plain`                 Regular ol' mutex
  `mtx_timed`                 Mutex that supports timeouts
  `mtx_plain|mtx_recursive`   Recursive mutex
  `mtx_timed|mtx_recursive`   Recursive mutex that supports timeouts

As you can see, you can make a plain or timed mutex *recursive* by bitwise-ORing the value with `mtx_recursive`.

"Recursive" means that the holder of a lock can call `mtx_lock()` multiple times on the same lock. (They have to unlock it an equal number of times before anyone else can take the mutex.) This might ease coding from time to time, especially if you call a function that needs to lock the mutex when you already hold the mutex.

And the timeout gives a thread a chance to *try* to get the lock for a while, but then bail out if it can't get it in that timeframe. You use the [`mtx_timedlock()`](threads.html#man-mtx_timedlock) function with `mtx_timed` mutexes.

### Return Value {#return-value-204 .unnumbered .unlisted}

Returns `thrd_success` in a perfect world, and potentially `thrd_error` in an imperfect one.

### Example {#example-208 .unnumbered .unlisted}

General-purpose mutex example here, but you can see the `mtx_init()` down at the top of `main()`:

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

A thread that calls this function will wait until it can acquire the mutex, then it will grab it, wake up, and run!

If the mutex is recursive and is already locked by this thread, it will be locked again and the lock count will increase. If the mutex is not recursive and the thread already holds it, this call will error out.

### Return Value {#return-value-205 .unnumbered .unlisted}

Returns `thrd_success` on goodness and `thrd_error` on badness.

### Example {#example-209 .unnumbered .unlisted}

General-purpose mutex example here, but you can see the `mtx_lock()` in the `run()` function:

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

The timeout is specified as an absolute UTC time since Epoch. You can get this with the [`timespec_get()`](time.html#man-timespec_get) function and then add values on to the result to timeout later than now, as shown in the example.

Beware that you can't have more than 999999999 nanoseconds in the `tv_nsec` field of the `struct timespec`. Mod those so they stay in range.

### Return Value {#return-value-206 .unnumbered .unlisted}

If everything works and the mutex is obtained, returns `thrd_success`. If a timeout happens first, returns `thrd_timedout`.

Otherwise, returns `thrd_error`. Because if nothing is right, everything is wrong.

### Example {#example-210 .unnumbered .unlisted}

This example has a thread wait on a mutex for a maximum of 1.75 seconds. And it always times out because no one ever sends a signal.

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

The spec notes that there's a chance that `mtx_trylock()` might spuriously fail with `thrd_busy` even if there are no other threads holding the lock. I'm not sure why this is, but you should defensively code against it.

### Return Value {#return-value-207 .unnumbered .unlisted}

Returns `thrd_success` if all's well. Or `thrd_busy` if some other thread holds the lock. Or `thrd_error`, which means something went right. I mean "wrong".

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

### Return Value {#return-value-208 .unnumbered .unlisted}

Returns `thrd_success` on success. Or `thrd_error` on error. It's not very original in this regard.

### Example {#example-212 .unnumbered .unlisted}

General-purpose mutex example here, but you can see the `mtx_unlock()` in the `run()` function:

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

In order to make this happen, you need to pass a pointer to a `thrd_t` that will be used to represent the thread you're spawning.

That thread will start running the function you pass a pointer to in `func`. This is a value of type `thrd_start_t`, which is a pointer to a function that returns an `int` and takes a single `void*` as a parameter, i.e.:

::: {#cb722 .sourceCode}
``` {.sourceCode .c}
int thread_run_func(void *arg)
```
:::

And, as you might have guessed, the pointer you pass to `thrd_create()` for the `arg` parameter is passed on to the `func` function. This is how you can give additional information to the thread when it starts up.

Of course, for `arg`, you have to be sure to pass a pointer to an object that is thread-safe or per-thread.

If the thread returns from the function, it exits just as if it had called `thrd_exit()`.

Finally, the value that the `func` function returns can be picked up by the parent thread with `thrd_join()`.

### Return Value {#return-value-209 .unnumbered .unlisted}

In the case of goodness, returns `thrd_success`. If you're out of memory, will return `thrd_nomem`. Otherwise, `thrd_error`.

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

But what if you want to get the ID of the currently running thread?

No problem! Just call this function and it will be returned to you.

Why? Who knows!

Well, to be honest, I could see it being used a couple places.

1.  You could use it to have a thread detach itself with `thrd_detach()`. I'm not sure why you'd want to do this, however.
2.  You could use it to compare this thread's ID with another you have stored in a variable somewhere by using the `thrd_equal()` function. Seems like the most legit use.
3.  ...
4.  Profit!

If anyone has another use, please let me know.

### Return Value {#return-value-210 .unnumbered .unlisted}

Returns the calling thread's ID.

### Example {#example-214 .unnumbered .unlisted}

Here's a general example that shows getting the current thread ID and comparing it to a previously-recorded thread ID and taking exciting action based on the result! Starring Arnold Schwarzenegger!

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

But if you call `thrd_detach()` on the thread first, manual cleanup isn't necessary. They just exit and are cleaned up by the OS.

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

For example, maybe one of the threads has special powers the others don't, and the run function needs to be able to tell them apart, as in the example.

### Return Value {#return-value-212 .unnumbered .unlisted}

Returns non-zero if the threads are equal. Returns `0` if they're not.

### Example {#example-216 .unnumbered .unlisted}

Here's a general example that shows getting the current thread ID and comparing it to a previously-recorded thread ID and taking boring action based on the result.

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

The `res` code can be picked up by a thread calling `thrd_join()`, and is equivalent to returning a value from the run function.

Like with returning from the run function, this will also properly clean up all the thread-specific storage associated with this thread---all the destructors for the threads TSS variables will be called. If there are any remaining TSS variables with destructors after the first round of destruction[^67^](footnotes.html#fn67){#fnref67 .footnote-ref role="doc-noteref"}, the remaining destructors will be called. This happens repeatedly until there are no more, or the number of rounds of carnage reaches `TSS_DTOR_ITERATIONS`.

If the main thread calls this, it's as if you called `exit(EXIT_SUCCESS)`.

### Return Value {#return-value-213 .unnumbered .unlisted}

This function never returns because the thread calling it is killed in the process. Trippy!

### Example {#example-217 .unnumbered .unlisted}

Threads in this example exit early with result `22` if they get a `NULL` value for `arg`.

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

### Return Value {#return-value-214 .unnumbered .unlisted}

### Example {#example-218 .unnumbered .unlisted}

Threads in this example exit early with result `22` if they get a `NULL` value for `arg`. The parent thread picks up this result code with `thrd_join()`.

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

The calling thread will wake up after the time has elapsed, or if it gets interrupted by a signal or something.

If it doesn't get interrupted, it'll sleep at least as long as you asked. Maybe a tad longer. You know how hard it can be to get out of bed.

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

### Return Value {#return-value-215 .unnumbered .unlisted}

Returns `0` on timeout, or `-1` if interrupted by a signal. Or any negative value on some other error. Weirdly, the spec allows this "other error negative value" to also be `-1`, so good luck with that.

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

It's a good way to be "polite" to the other threads in your program if you want the encourage them to run instead.

### Return Value {#return-value-216 .unnumbered .unlisted}

Returns nothing!

### Example {#example-220 .unnumbered .unlisted}

This example's kinda poor because the OS is probably going to reschedule threads on the output anyway, but it gets the point across.

The main thread is giving other threads a chance to run after every block of dumb work it does.

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

To make this work, you pass in a pointer to a `tss_t` key---this is the variable you will use in subsequent `tss_set()` and `tss_get()` calls to set and get the value associated with the key.

The interesting part of this is the `dtor` destructor pointer of type `tss_dtor_t`. This is actually a pointer to a function that takes a `void*` argument and returns `void`, i.e.

::: {#cb747 .sourceCode}
``` {.sourceCode .c}
void dtor(void *p) { ... }
```
:::

This function will be called per thread when the thread exits with `thrd_exit()` (or returns from the run function).

It's unspecified behavior to call this function while other threads' destructors are running.

### Return Value {#return-value-217 .unnumbered .unlisted}

Returns nothing!

### Example {#example-221 .unnumbered .unlisted}

This is a general-purpose TSS example. Note the TSS variable is created near the top of `main()`.

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

This doesn't call any destructors! Those are all called by `thrd_exit()`!

### Return Value {#return-value-218 .unnumbered .unlisted}

Returns nothing!

### Example {#example-222 .unnumbered .unlisted}

This is a general-purpose TSS example. Note the TSS variable is deleted near the bottom of `main()`.

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

Don't call this from a destructor.

### Return Value {#return-value-219 .unnumbered .unlisted}

Returns the value stored for the given `key`, or `NULL` if there's trouble.

### Example {#example-223 .unnumbered .unlisted}

This is a general-purpose TSS example. Note the TSS variable is retrieved in `some_function()`, below.

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

`key` is the identifier for this data, and `val` is a pointer to it.

The destructor specified in `tss_create()` will be called for the value set when the thread exits.

Also, if there's a destructor *and* there is already at value for this key in place, the destructor will not be called for the already-existing value. In fact, this function will never cause a destructor to be called. So you're on your own, there---best clean up the old value before overwriting it with the new one.

### Return Value {#return-value-220 .unnumbered .unlisted}

Returns `thrd_success` when happy, and `thrd_error` when not.

### Example {#example-224 .unnumbered .unlisted}

This is a general-purpose TSS example. Note the TSS variable is set in `run()`, below.

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
