---
tip: translate by openai@2023-07-21 09:24:23
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](uchar.html) \| [Contents](index.html) \| [Next](wctype.html)
:::

------------------------------------------------------------------------

# [30]{.header-section-number} `<wchar.h>` Wide Character Handling {#wchar number="30"}


  ---------------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------------
简体中文
  Function                                    Description

  ------------------------------------------- -------------------------------------------------------------------

> ------------------------------------------- -------------------------------------------------------------------
简体中文：------------------------------------------- -------------------------------------------------------------------

  [`btowc()`](wchar.html#man-btowc)           Convert a single byte character to a wide character

> btowc()：将单字节字符转换为宽字符


  [`fgetwc()`](wchar.html#man-getwc)          Get a wide character from a wide stream

> fgetwc()（wchar.html#man-getwc）从宽字符流中获取一个宽字符。


  [`fgetws()`](wchar.html#man-fgetws)         Read a wide string from a wide stream

> `fgetws()`（wchar.html#man-fgetws）从宽流中读取宽字符串。


  [`fputwc()`](wchar.html#man-putwc)          Write a wide character to a wide stream

> fputwc()（wchar.html#man-putwc）将宽字符写入宽流


  [`fputws()`](wchar.html#man-fputws)         Write a wide string to a wide stream

> `fputws()`（wchar.html#man-fputws）将宽字符串写入宽流


  [`fwide()`](wchar.html#man-fwide)           Get or set the orientation of the stream

> [`fwide()`](wchar.html#man-fwide)：获取或设置流的方向。


  [`fwprintf()`](wchar.html#man-wprintf)      Formatted wide output to a wide stream

> fwprintf()：格式化宽字符输出到宽字符流


  [`fwscanf()`](wchar.html#man-wscanf)        Formatted wide input from a wide stream

> `fwscanf()`：从宽字符流中格式化宽字符输入


  [`getwchar()`](wchar.html#man-getwc)        Get a wide character from `stdin`

> 从`stdin`获取一个宽字符。


  [`getwc()`](wchar.html#man-getwc)           Get a wide character from `stdin`

> 从`stdin`获取宽字符（getwc()）


  [`mbrlen()`](wchar.html#man-mbrlen)         Compute the number of bytes in a multibyte character restartably

> `mbrlen()`计算多字节字符的字节数，可重新启动。


  [`mbrtowc()`](wchar.html#man-mbrtowc)       Convert multibyte to wide characters restartably

> mbrtowc()（wchar.html#man-mbrtowc）可重新启动地将多字节转换为宽字符


  [`mbsinit()`](wchar.html#man-mbsinit)       Test if an `mbstate_t` is in the initial conversion state

> 检查mbstate_t是否处于初始转换状态


  [`mbsrtowcs()`](wchar.html#man-mbsrtowcs)   Convert a multibyte string to a wide character string restartably

> mbsrtowcs() 可重新开始地将多字节字符串转换为宽字符串


  [`putwchar()`](wchar.html#man-putwc)        Write a wide character to `stdout`

> 将宽字符写入标准输出流stdout


  [`putwc()`](wchar.html#man-putwc)           Write a wide character to `stdout`

> 写一个宽字符到标准输出（stdout），使用putwc()函数


  [`swprintf()`](wchar.html#man-wprintf)      Formatted wide output to a wide string

> swprintf()：格式化宽字符输出到宽字符串


  [`swscanf()`](wchar.html#man-wscanf)        Formatted wide input from a wide string

> swscanf()：从宽字符串获取格式化的宽输入


  [`ungetwc()`](wchar.html#man-ungetwc)       Pushes a wide character back into the input stream

> `ungetwc()`（wchar.html#man-ungetwc）将一个宽字符推回输入流中。


  [`vfwprintf()`](wchar.html#man-wprintf)     Variadic formatted wide output to a wide stream

> `vfwprintf()`（[wchar.html#man-wprintf](wchar.html#man-wprintf)）：根据格式化输出可变参数到宽字符流。


  [`vfwscanf()`](wchar.html#man-wscanf)       Variadic formatted wide input from a wide stream

> `vfwscanf()`：从宽字符流中进行变参格式化宽字符输入


  [`vswprintf()`](wchar.html#man-wprintf)     Variadic formatted wide output to a wide string

> [`vswprintf()`](wchar.html#man-wprintf)：将可变参数格式化的宽字符串输出到宽字符串中


  [`vswscanf()`](wchar.html#man-wscanf)       Variadic formatted wide input from a wide string

> `vswscanf()`：从宽字符串中格式化可变参数的宽输入


  [`vwprintf()`](wchar.html#man-wprintf)      Variadic formatted wide output

> `vwprintf()`（wchar.html#man-wprintf）：可变参数格式的宽字符输出


  [`vwscanf()`](wchar.html#man-wscanf)        Variadic formatted wide input

> `vwscanf()`：可变参数格式化的宽字符输入


  [`wcscat()`](wchar.html#man-wcscat)         Concatenate wide strings dangerously

> wcscat()危险地连接宽字符串


  [`wcschr()`](wchar.html#man-wcschr)         Find a wide character in a wide string

> 找到宽字符串中的宽字符（wcschr()）

  [`wcscmp()`](wchar.html#man-wcscmp)         Compare wide strings


  [`wcscoll()`](wchar.html#man-wcscoll)       Compare two wide strings accounting for locale

> 比较两个宽字符串，考虑本地化


  [`wcscpy()`](wchar.html#man-wcscpy)         Copy a wide string dangerously

> wcscpy()函数危险地复制一个宽字符串。


  [`wcscspn()`](wchar.html#man-wcsspn)        Count characters not from a start at the front of a wide string

> `wcscspn()`函数用于计算宽字符串开头不包含指定字符的字符数。


  [`wcsftime()`](wchar.html#man-wcsftime)     Formatted date and time output

> `wcsftime()`：格式化的日期和时间输出


  [`wcslen()`](wchar.html#man-wcslen)         Returns the length of a wide string

> `wcslen()` 返回宽字符串的长度


  [`wcsncat()`](wchar.html#man-wcscat)        Concatenate wide strings more safely

> wcsncat() 安全地连接宽字符串


  [`wcsncmp()`](wchar.html#man-wcscmp)        Compare wide strings, length limited

> 比较宽字符串，长度受限


  [`wcsncpy()`](wchar.html#man-wcscpy)        Copy a wide string more safely

> wcsncpy() 安全地复制一个宽字符串


  [`wcspbrk()`](wchar.html#man-wcspbrk)       Search a wide string for one of a set of wide characters

> `wcspbrk()`函数搜索宽字符串中的一组宽字符。


  [`wcsrchr()`](wchar.html#man-wcschr)        Find a wide character in a wide string from the end

> 找到宽字符串中从末尾开始的宽字符（wcsrchr()）


  [`wcsrtombs()`](wchar.html#man-wcsrtombs)   Convert a wide character string to a multibyte string restartably

> wcsrtombs()：可重新开始地将宽字符串转换为多字节字符串。


  [`wcsspn()`](wchar.html#man-wcsspn)         Count characters from a set at the front of a wide string

> `wcsspn()`函数计算宽字符串开头的字符数量，这些字符来自一组字符集。


  [`wcsstr()`](wchar.html#man-wcsstr)         Find a wide string in another wide string

> 找到一个宽字符串中的另一个宽字符串（wcsstr()）


  [`wcstod()`](wchar.html#man-wcstod)         Convert a wide string to a `double`

> `wcstod()`将宽字符串转换为`double`类型。


  [`wcstof()`](wchar.html#man-wcstod)         Convert a wide string to a `float`

> `wcstof()` (wchar.html#man-wcstod) 将宽字符串转换为 `float` 类型。

  [`wcstok()`](wchar.html#man-wcstok)         Tokenize a wide string


  [`wcstold()`](wchar.html#man-wcstod)        Convert a wide string to a `long double`

> wcstold() 将宽字符串转换为长双精度浮点数。


  [`wcstoll()`](wchar.html#man-wcstol)        Convert a wide string to a `long long`

> `wcstoll()`将宽字符串转换为`long long`类型。


  [`wcstol()`](wchar.html#man-wcstol)         Convert a wide string to a `long`

> wcstol() 将宽字符串转换为长整型。


  [`wcstoull()`](wchar.html#man-wcstol)       Convert a wide string to an `unsigned long long`

> `wcstoull()`（[wchar.html#man-wcstol](wchar.html#man-wcstol)）将宽字符串转换为无符号长长整型。


  [`wcstoul()`](wchar.html#man-wcstol)        Convert a wide string to an `unsigned long`

> `wcstoul()`（[wchar.html#man-wcstol](wchar.html#man-wcstol)）将宽字符串转换为无符号长整型。


  [`wcsxfrm()`](wchar.html#man-wcsxfrm)       Transform a wide string for comparing based on locale

> `wcsxfrm()`根据区域设置转换宽字符串以进行比较


  [`wctob()`](wchar.html#man-btowc)           Convert a wide character to a single byte character

> [`wctob()`](wchar.html#man-btowc)将宽字符转换为单字节字符


  [`wctombr()`](wchar.html#man-wcrtomb)       Convert wide to multibyte characters restartably

> [`wctomb()`](wchar.html#man-wcrtomb) 可重新启动地将宽字符转换为多字节字符。


  [`wmemcmp()`](wchar.html#man-wcscmp)        Compare wide characters in memory

> 比较内存中的宽字符（wmemcmp()）

  [`wmemcpy()`](wchar.html#man-wmemcpy)       Copy wide character memory


  [`wmemmove()`](wchar.html#man-wmemcpy)      Copy wide character memory, potentially overlapping

> wmemmove()（wchar.html#man-wmemcpy）复制宽字符内存，可能会发生重叠

  [`wprintf()`](wchar.html#man-wprintf)       Formatted wide output

  [`wscanf()`](wchar.html#man-wscanf)         Formatted wide input

  ---------------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------------
简体中文


These are the wide character variants of the functions found in [`<stdio.h>`](stdio.html#stdio).

> 这些是在[`<stdio.h>`](stdio.html#stdio)中发现的函数的宽字符变体。


Remember that you can't mix-and-match multibyte output functions (like [`printf()`](stdio.html#man-printf)) with wide character output functions (like [`wprintf()`](wchar.html#man-wprintf)). The output stream has an *orientation* to either multibyte or wide that gets set on the first I/O call to that stream. (Or it can be set with [`fwide()`](wchar.html#man-fwide).)

> 记住，你不能混合使用多字节输出函数（如[`printf()`](stdio.html#man-printf))和宽字符输出函数（如[`wprintf()`](wchar.html#man-wprintf))。输出流的*方向*被设置为多字节或宽字符，并在第一次I/O调用该流时设置。（或者可以使用[`fwide()`](wchar.html#man-fwide)设置。）

So choose one or the other and stick with it.


And you can specify wide character constants and string literals by prefixing `L` to the front of it:

> 你可以通过在前面加上`L`来指定宽字符常量和字符串文字：

::: {#cb810 .sourceCode}
``` {.sourceCode .c}
wchar_t *s = L"Hello, world!";
wchar_t c = L'B';
```
:::


This header also introduces a type `wint_t` that is used by the character I/O functions. It's a type that can hold any single wide character, but *also* the macro `WEOF` to indicate wide end-of-file.

> 这个头文件还引入了一种类型`wint_t`，它被字符I/O函数使用。它是一种可以容纳任何单个宽字符的类型，但也可以使用宏`WEOF`来表示宽字符的文件结束。

## [30.1]{.header-section-number} Restartable Functions {#restartable-functions number="30.1"}


Finally, a note on the "restartable" functions that are included here. When conversion is happening, some encodings require C to keep track of some *state* about the progress of the conversion so far.

> 最后，关于包含在这里的“可重启”功能的注意事项。当转换发生时，某些编码需要C跟踪有关转换进度的一些*状态*。


For a lot of the functions, C uses an internal variable for the state that is shared between function calls. The problem is if you're writing multithreaded code, this state might get trampled by other threads.

> 对于许多函数，C使用内部变量来共享函数调用之间的状态。问题是，如果您正在编写多线程代码，此状态可能会被其他线程破坏。


To avoid this, each thread needs to maintain its own state in a variable of the opaque type `mbstate_t`. And the "restartable" functions allow you to pass in this state so that each thread can use their own.

> 为了避免这种情况，每个线程都需要在不透明类型的变量中维护自己的状态。“可重新启动”的函数允许您传入此状态，以便每个线程都可以使用自己的状态。

------------------------------------------------------------------------

## [30.2]{.header-section-number} `wprintf()`, `fwprintf()`, `swprintf()` {#man-wprintf number="30.2"}

Formatted output with a wide string

### Synopsis {#synopsis-235 .unnumbered .unlisted}

::: {#cb811 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>   // For fwprintf()
#include <wchar.h>

int wprintf(const wchar_t * restrict format, ...);

int fwprintf(FILE * restrict stream, const wchar_t * restrict format, ...);

int swprintf(wchar_t * restrict s, size_t n,
             const wchar_t * restrict format, ...);
```
:::

### Description {#description-235 .unnumbered .unlisted}


These are the wide versions of [`printf()`](stdio.html#man-printf), [`fprintf()](#man-printf), and [`sprintf()\`](stdio.html#man-printf).

> 这些是[`printf()`](stdio.html#man-printf)、[`fprintf()`](#man-printf)和[`sprintf()`](stdio.html#man-printf)的宽版本。

See those pages for exact substantial usage.


These are the same except the `format` string is a wide character string instead of a multibyte string.

> 这些都是一样的，只是`format`字符串是宽字符串而不是多字节字符串。


And that `swprintf()` is analogous to `snprintf()` in that they both take the size of the destination array as an argument.

> 而且`swprintf()`与`snprintf()`类似，它们都将目标数组的大小作为参数。


And one more thing: the precision specified for a `%s` specifier corresponds to the number of wide characters printed, not the number of bytes. If you know of other difference, let me know.

> 另外一件事：`%s`指定符所指定的精度对应于打印的宽字符数，而不是字节数。如果你知道其他差异，请告诉我。

### Return Value {#return-value-233 .unnumbered .unlisted}


Returns the number of wide characters outputted, or `-1` if there's an error.

> 返回输出的宽字符数，如果出错则返回-1。

### Example {#example-237 .unnumbered .unlisted}

::: {#cb812 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

int main(void)
{
    char *mbs = "multibyte";
    wchar_t *ws = L"wide";

    wprintf(L"We're all wide for %s and %ls!\n", mbs, ws);

    double pi = 3.14159265358979;
    wprintf(L"pi = %f\n", pi);
}
```
:::

Output:

::: {#cb813 .sourceCode}
``` {.sourceCode .default}
We're all wide for multibyte and wide!
pi = 3.141593
```
:::

### See Also {#see-also-223 .unnumbered .unlisted}


[`printf()`](stdio.html#man-printf), [`vwprintf()`](wchar.html#man-vwprintf)

> [printf()](stdio.html#man-printf), [vwprintf()](wchar.html#man-vwprintf)

------------------------------------------------------------------------

## [30.3]{.header-section-number} `wscanf()` `fwscanf()` `swscanf()` {#man-wscanf number="30.3"}

Scan a wide stream or wide string for formatted input

### Synopsis {#synopsis-236 .unnumbered .unlisted}

::: {#cb814 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>  // for fwscanf()
#include <wchar.h>

int wscanf(const wchar_t * restrict format, ...);

int fwscanf(FILE * restrict stream, const wchar_t * restrict format, ...);

int swscanf(const wchar_t * restrict s, const wchar_t * restrict format, ...);
```
:::

### Description {#description-236 .unnumbered .unlisted}


These are the wide variants of [`scanf()`](stdio.html#man-scanf), [`fscanf()`](stdio.html#man-scanf), and [`sscanf()`](stdio.html#man-scanf).

> 这些是[`scanf()`](stdio.html#man-scanf)、[`fscanf()`](stdio.html#man-scanf)和[`sscanf()`](stdio.html#man-scanf)的广泛变体。

See the [`scanf()`](stdio.html#man-scanf) page for all the details.

### Return Value {#return-value-234 .unnumbered .unlisted}


Returns the number of items successfully scanned, or `EOF` on some kind of input failure.

> 返回成功扫描的项目数量，或者在某种输入失败时返回`EOF`。

### Example {#example-238 .unnumbered .unlisted}

::: {#cb815 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

int main(void)
{
    int quantity;
    wchar_t item[100];

    wprintf(L"Enter \"quantity: item\"\n");
    
    if (wscanf(L"%d:%99ls", &quantity, item) != 2)
        wprintf(L"Malformed input!\n");
    else
        wprintf(L"You entered: %d %ls\n", quantity, item);
}
```
:::

Output (input of `12: apples`):

::: {#cb816 .sourceCode}
``` {.sourceCode .default}
Enter "quantity: item"
12: apples
You entered: 12 apples
```
:::

### See Also {#see-also-224 .unnumbered .unlisted}

[`scanf()`](stdio.html#man-scanf), [`vwscanf()`](wchar.html#man-vwscanf)

------------------------------------------------------------------------

## [30.4]{.header-section-number} `vwprintf()` `vfwprintf()` `vswprintf()` {#man-vwprintf number="30.4"}

`wprintf()` variants using variable argument lists (`va_list`)

### Synopsis {#synopsis-237 .unnumbered .unlisted}

::: {#cb817 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>   // For vfwprintf()
#include <stdarg.h>
#include <wchar.h>

int vwprintf(const wchar_t * restrict format, va_list arg);

int vswprintf(wchar_t * restrict s, size_t n,
              const wchar_t * restrict format, va_list arg); 

int vfwprintf(FILE * restrict stream, const wchar_t * restrict format,
              va_list arg);
```
:::

### Description {#description-237 .unnumbered .unlisted}


These functions are the wide character variants of the [`vprintf()`](stdio.html#man-vprintf), functions. You can [refer to that reference page](stdio.html#man-vprintf) for more details.

> 这些函数是[`vprintf()`](stdio.html#man-vprintf)函数的宽字符变体。您可以参考[该参考页面](stdio.html#man-vprintf)了解更多细节。

### Return Value {#return-value-235 .unnumbered .unlisted}


Returns the number of wide characters stored, or a negative value on error.

> 返回存储的宽字符数量，出错时返回负值。

### Example {#example-239 .unnumbered .unlisted}


In this example, we make our own version of `wprintf()` called `wlogger()` that timestamps output. Notice how the calls to `wlogger()` have all the bells and whistles of `wprintf()`.

> 在这个例子中，我们创建了一个自己版本的`wprintf()`，叫做`wlogger()`，它可以对输出进行时间戳标记。注意，调用`wlogger()`的方式和`wprintf()`一样具有各种功能。

::: {#cb818 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdarg.h>
#include <wchar.h>
#include <time.h>

int wlogger(wchar_t *format, ...)
{
    va_list va;
    time_t now_secs = time(NULL);
    struct tm *now = gmtime(&now_secs);

    // Output timestamp in format "YYYY-MM-DD hh:mm:ss : "
    wprintf(L"%04d-%02d-%02d %02d:%02d:%02d : ",
        now->tm_year + 1900, now->tm_mon + 1, now->tm_mday,
        now->tm_hour, now->tm_min, now->tm_sec);

    va_start(va, format);
    int result = vwprintf(format, va);
    va_end(va);

    wprintf(L"\n");

    return result;
}

int main(void)
{
    int x = 12;
    float y = 3.2;

    wlogger(L"Hello!");
    wlogger(L"x = %d and y = %.2f", x, y);
}
```
:::

Output:

::: {#cb819 .sourceCode}
``` {.sourceCode .default}
2021-03-30 04:25:49 : Hello!
2021-03-30 04:25:49 : x = 12 and y = 3.20
```
:::

### See Also {#see-also-225 .unnumbered .unlisted}


[`printf()`](stdio.html#man-printf), [`vprintf()`](stdio.html#man-vprintf)

> [`printf()`](stdio.html#man-printf)，[`vprintf()`](stdio.html#man-vprintf)

------------------------------------------------------------------------

## [30.5]{.header-section-number} `vwscanf()`, `vfwscanf()`, `vswscanf()` {#man-vwscanf number="30.5"}

`wscanf()` variants using variable argument lists (`va_list`)

### Synopsis {#synopsis-238 .unnumbered .unlisted}

::: {#cb820 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>   // For vfwscanf()
#include <stdarg.h>
#include <wchar.h>

int vwscanf(const wchar_t * restrict format, va_list arg);

int vfwscanf(FILE * restrict stream, const wchar_t * restrict format,
             va_list arg); 

int vswscanf(const wchar_t * restrict s, const wchar_t * restrict format,
             va_list arg);
```
:::

### Description {#description-238 .unnumbered .unlisted}


These are the wide counterparts to the [`vscanf()`](stdio.html#man-vscanf) collection of functions. See their [reference page for details](stdio.html#man-vscanf).

> 这些是[`vscanf()`](stdio.html#man-vscanf)函数集的宽版本。有关详细信息，请参阅其[参考页面](stdio.html#man-vscanf)。

### Return Value {#return-value-236 .unnumbered .unlisted}


Returns the number of items successfully scanned, or `EOF` on some kind of input failure.

> 返回成功扫描的项目数量，或者在某种输入失败时返回`EOF`。

### Example {#example-240 .unnumbered .unlisted}


I have to admit I was wracking my brain to think of when you'd ever want to use this. The best example I could find was [one on Stack Overflow](https://stackoverflow.com/questions/17017331/c99-vscanf-for-dummies/17018046#17018046)[^77^](footnotes.html#fn77){#fnref77 .footnote-ref role="doc-noteref"} that error-checks the return value from `scanf()` against the expected. A variant of that is shown below.

> 我不得不承认，我正在努力思考你什么时候会想要使用这个。我找到的最佳例子是[Stack Overflow上的一个](https://stackoverflow.com/questions/17017331/c99-vscanf-for-dummies/17018046#17018046)[^77^](footnotes.html#fn77){#fnref77 .footnote-ref role="doc-noteref"}，它可以检查`scanf()`的返回值与预期值之间的差异。下面展示了一个变体。

::: {#cb821 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdarg.h>
#include <wchar.h>
#include <assert.h>

int error_check_wscanf(int expected_count, wchar_t *format, ...)
{
    va_list va;

    va_start(va, format);
    int count = vwscanf(format, va);
    va_end(va);

    // This line will crash the program if the condition is false:
    assert(count == expected_count);

    return count;
}

int main(void)
{
    int a, b;
    float c;

    error_check_wscanf(3, L"%d, %d/%f", &a, &b, &c);
    error_check_wscanf(2, L"%d", &a);
}
```
:::

### See Also {#see-also-226 .unnumbered .unlisted}

[`wscanf()`](wchar.html#man-wscanf)

------------------------------------------------------------------------

## [30.6]{.header-section-number} `getwc()` `fgetwc()` `getwchar()` {#man-getwc number="30.6"}

Get a wide character from an input stream

### Synopsis {#synopsis-239 .unnumbered .unlisted}

::: {#cb822 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>   // For getwc() and fgetwc()
#include <wchar.h>

wint_t getwchar(void);

wint_t getwc(FILE *stream);

wint_t fgetwc(FILE *stream);
```
:::

### Description {#description-239 .unnumbered .unlisted}

These are the wide variants of [`fgetc()`](stdio.html#man-getc).

`fgetwc()` and `getwc()` are identical except that `getwc()` might be implemented as a macro and is allowed to evaluate `stream` multiple times.

`getwchar()` is identical to `getwc()` with `stream` set to `stdin`.


I don't know why you'd ever use `getwc()` instead of `fgetwc()`, but if anyone knows, drop me a line.

> 我不知道你为什么要用`getwc()`而不是`fgetwc()`，但如果有人知道，请给我留言。

### Return Value {#return-value-237 .unnumbered .unlisted}


Returns the next wide character in the input stream. Return `WEOF` on end-of-file or error.

> 返回输入流中的下一个宽字符。在文件结束或错误时返回WEOF。

If an I/O error occurs, the error flag is also set on the stream.

If an invalid byte sequence is encountered, `errno` is set to `ILSEQ`.

### Example {#example-241 .unnumbered .unlisted}


Reads all the characters from a file, outputting only the letter 'b's it finds in the file:

> 从文件中读取所有字符，只输出文件中找到的字母'b'。

::: {#cb823 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

int main(void)
{
    FILE *fp;
    wint_t c;

    fp = fopen("datafile.txt", "r"); // error check this!

    // this while-statement assigns into c, and then checks against EOF:

    while((c = fgetc(fp)) != WEOF) 
        if (c == L'b')
            fputwc(c, stdout);

    fclose(fp);
}
```
:::

### See Also {#see-also-227 .unnumbered .unlisted}


[`fputwc`](wchar.html#man-putwc), [`fgetws`](wchar.html#man-fgetws), [`errno`](errno.html#errno)

> [`fputwc`](wchar.html#man-putwc)：将宽字符写入文件流
[`fgetws`](wchar.html#man-fgetws)：从文件流中读取宽字符
[`errno`](errno.html#errno)：错误号

------------------------------------------------------------------------

## [30.7]{.header-section-number} `fgetws()` {#man-fgetws number="30.7"}

Read a wide string from a file

### Synopsis {#synopsis-240 .unnumbered .unlisted}

::: {#cb824 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <wchar.h>

wchar_t *fgetws(wchar_t * restrict s, int n, FILE * restrict stream);
```
:::

### Description {#description-240 .unnumbered .unlisted}


This is the wide version of [`fgets()`](stdio.html#man-gets). See [its reference page for details](stdio.html#man-gets).

> 这是[`fgets()`](stdio.html#man-gets)的宽版本。详情请参见[它的参考页面](stdio.html#man-gets)。

A wide `NUL` character is used to terminate the string.

### Return Value {#return-value-238 .unnumbered .unlisted}

Returns `s` on success, or a `NULL` pointer on end-of-file or error.

### Example {#example-242 .unnumbered .unlisted}


The following example reads lines from a file and prepends them with numbers:

> 以下示例从文件中读取行，并为它们添加数字前缀：

::: {#cb825 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

#define BUF_SIZE 1024

int main(void)
{
    FILE *fp;
    wchar_t buf[BUF_SIZE];

    fp = fopen("textfile.txt", "r"); // error check this!

    int line_count = 0;

    while ((fgetws(buf, BUF_SIZE, fp)) != NULL) 
        wprintf(L"%04d: %ls", ++line_count, buf);

    fclose(fp);
}
```
:::


Example output for a file with these lines in them (without the prepended numbers):

> 以下是文件中的示例输出（不带预先添加的数字）：

::: {#cb826 .sourceCode}
``` {.sourceCode .default}
0001: line 1
0002: line 2
0003: something
0004: line 4
```
:::

### See Also {#see-also-228 .unnumbered .unlisted}

[`fgetwc()`](wchar.html#man-getwc), [`fgets()`](stdio.html#man-gets)

------------------------------------------------------------------------

## [30.8]{.header-section-number} `putwchar()` `putwc()` `fputwc()` {#man-putwc number="30.8"}

Write a single wide character to the console or to a file

### Synopsis {#synopsis-241 .unnumbered .unlisted}

::: {#cb827 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>   // For putwc() and fputwc()
#include <wchar.h>

wint_t putwchar(wchar_t c);

wint_t putwc(wchar_t c, FILE *stream);

wint_t fputwc(wchar_t c, FILE *stream);
```
:::

### Description {#description-241 .unnumbered .unlisted}


These are the wide character equivalents to the ['fputc()'](stdio.html#man-putc) group of functions. You can find more information ['in that reference section'](stdio.html#man-putc).

> 这些是与['fputc()'](stdio.html#man-putc)组函数的宽字符等价物。您可以在['该参考部分'](stdio.html#man-putc)中找到更多信息。

`fputwc()` and `putwc()` are identical except that `putwc()` might be implemented as a macro and is allowed to evaluate `stream` multiple times.

`putwchar()` is identical to `putwc()` with `stream` set to `stdin`.


I don't know why you'd ever use `putwc()` instead of `fputwc()`, but if anyone knows, drop me a line.

> 我不知道你为什么要用`putwc()`而不是`fputwc()`，但如果有人知道，请给我留言。

### Return Value {#return-value-239 .unnumbered .unlisted}

Returns the wide character written, or `WEOF` on error.

If it's an I/O error, the error flag will be set for the stream.

If it's an encoding error, `errno` will be set to `EILSEQ`.

### Example {#example-243 .unnumbered .unlisted}


Read all characters from a file, outputting only the letter 'b's it finds in the file:

> 从文件中读取所有字符，只输出其中的字母'b'。

::: {#cb828 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

int main(void)
{
    FILE *fp;
    wint_t c;

    fp = fopen("datafile.txt", "r"); // error check this!

    // this while-statement assigns into c, and then checks against EOF:

    while((c = fgetc(fp)) != WEOF) 
        if (c == L'b')
            fputwc(c, stdout);

    fclose(fp);
}
```
:::

### See Also {#see-also-229 .unnumbered .unlisted}


[`fgetwc()`](wchar.html#man-getwc), [`fputc()`](stdio.html#man-putc), [`errno`](errno.html#errno)

> [`fgetwc()`](wchar.html#man-getwc)：取得宽字符
[`fputc()`](stdio.html#man-putc)：写入字符
[`errno`](errno.html#errno)：错误码

------------------------------------------------------------------------

## [30.9]{.header-section-number} `fputws()` {#man-fputws number="30.9"}

Write a wide string to a file

### Synopsis {#synopsis-242 .unnumbered .unlisted}

::: {#cb829 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <wchar.h>

int fputws(const wchar_t * restrict s, FILE * restrict stream);
```
:::

### Description {#description-242 .unnumbered .unlisted}

This is the wide version of [`fputs()`](stdio.html#man-puts).

Pass in a wide string and an output stream, and it will so be written.

### Return Value {#return-value-240 .unnumbered .unlisted}

Returns a non-negative value on success, or `EOF` on error.

### Example {#example-244 .unnumbered .unlisted}

::: {#cb830 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

int main(void)
{
    fputws(L"Hello, world!\n", stdout);
}
```
:::

### See Also {#see-also-230 .unnumbered .unlisted}

[`fputwc()`](wchar.html#man-putwc) [`fputs()`](stdio.html#man-puts)

------------------------------------------------------------------------

## [30.10]{.header-section-number} `fwide()` {#man-fwide number="30.10"}

Get or set the orientation of the stream

### Synopsis {#synopsis-243 .unnumbered .unlisted}

::: {#cb831 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <wchar.h>

int fwide(FILE *stream, int mode);
```
:::

### Description {#description-243 .unnumbered .unlisted}


Streams can be either wide-oriented (meaning the wide functions are in use) or byte-oriented (that the regular multibyte functions are in use). Or, before an orientation is chosen, unoriented.

> 流可以是宽定向的（意味着使用宽功能）或字节定向的（即使用常规多字节功能）。或者，在选择定向之前，是未定向的。

There are two ways to set the orientation of an unoriented stream:


-   Implicitly: just use a function like `printf()` (byte oriented) or `wprintf()` (wide oriented), and the orientation will be set.

> 可以使用像`printf()`（字节导向）或`wprintf()`（宽字符导向）这样的函数，它们会隐式地设置方向。

-   Explicitly: use this function to set it.


You can set the orientation for the stream by passing different numbers to `mode`:

> 你可以通过传递不同的数字到'mode'来设置流的方向：

  `mode`   Description
  -------- ------------------------------
  `0`      Do not alter the orientation
  `-1`     Set stream to byte-oriented
  `1`      Set stream to wide-oriented


(I said `-1` and `1` there, but really it could be any positive or negative number.)

> 我说了-1和1，但实际上可以是任何正负数。


Most people choose the wide or byte functions (`printf()` or `wprintf()`) and just start using them and never use `fwide()` to set the orientation.

> 大多数人选择宽字节函数（`printf()`或`wprintf()`），只是开始使用它们，而不使用`fwide()`来设置方向。


And once the orientation is set, you can't change it. So you can't use `fwide()` for that, either.

> 一旦定位被设置，你就无法更改它。因此，你也不能使用`fwide（）`来完成这一点。

So what can you use it for?


You can *test* to see what orientation a stream is in by passing `0` as the `mode` and checking the return value.

> 你可以通过将`0`作为`mode`并检查返回值来*测试*查看流的方向。

### Return Value {#return-value-241 .unnumbered .unlisted}

Returns greater than zero if the stream is wide-oriented.

Returns less than zero if the stream is byte-oriented.

Returns zero if the stream is unoriented.

### Example {#example-245 .unnumbered .unlisted}

Example setting to byte-oriented:

::: {#cb832 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

int main(void)
{
    printf("Hello world!\n");  // Implicitly set to byte

    int mode = fwide(stdout, 0);

    printf("Stream is %s-oriented\n", mode < 0? "byte": "wide");
}
```
:::

Output:

::: {#cb833 .sourceCode}
``` {.sourceCode .default}
Hello world!
Stream is byte-oriented
```
:::

Example setting to wide-oriented:

::: {#cb834 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wchar.h>

int main(void)
{
    wprintf(L"Hello world!\n");  // Implicitly set to wide

    int mode = fwide(stdout, 0);

    wprintf(L"Stream is %ls-oriented\n", mode < 0? L"byte": L"wide");
}
```
:::

Output:

::: {#cb835 .sourceCode}
``` {.sourceCode .default}
Hello world!
Stream is wide-oriented
```
:::

------------------------------------------------------------------------

## [30.11]{.header-section-number} `ungetwc()` {#man-ungetwc number="30.11"}

Pushes a wide character back into the input stream

### Synopsis {#synopsis-244 .unnumbered .unlisted}

::: {#cb836 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <wchar.h>

wint_t ungetwc(wint_t c, FILE *stream);
```
:::

### Description {#description-244 .unnumbered .unlisted}


This is the wide character variant of [`ungetc()`](stdio.html#man-ungetc).

> 这是[`ungetc()`](stdio.html#man-ungetc)的宽字符变体。


It performs the reverse operation of [`fgetwc()`](wchar.html#man-getwc), pushing a character back on the input stream.

> 它执行[`fgetwc()`](wchar.html#man-getwc)的反向操作，将一个字符推回输入流。


The spec guarantees you can do this one time in a row. You can probably do it more times, but it's up to the implementation. If you do too many calls without an intervening read, an error could be returned.

> 规格保证您可以连续一次性完成这项操作。您可能可以多次完成，但取决于实现。如果您在没有中间读取的情况下进行太多调用，可能会返回错误。


Setting the file position discards any characters pushed by `ungetwc()` without being subsequently read.

> 设置文件位置会丢弃由`ungetwc()`推送但尚未被读取的任何字符。

The end-of-file flag is cleared after a successful call.

### Return Value {#return-value-242 .unnumbered .unlisted}


Returns the value of the pushed character on success, or `WEOF` on failure.

> 如果成功，返回推入字符的值，如果失败，返回WEOF。

### Example {#example-246 .unnumbered .unlisted}


This example reads a piece of punctuation, then everything after it up to the next piece of punctuation. It returns the leading punctuation, and stores the rest in a string.

> 这个例子读取一段标点符号，然后读取它后面到下一个标点符号的所有内容。它会返回前面的标点符号，并把其余的内容存储在一个字符串中。

::: {#cb837 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <wctype.h>
#include <wchar.h>

wint_t read_punctstring(FILE *fp, wchar_t *s)
{
    wint_t origpunct, c;
    
    origpunct = fgetwc(fp);

    if (origpunct == WEOF)  // return EOF on end-of-file
        return WEOF;

    while (c = fgetwc(fp), !iswpunct(c) && c != WEOF)
        *s++ = c;  // save it in the string

    *s = L'\0'; // nul-terminate the string

    // if we read punctuation last, ungetc it so we can fgetc it next
    // time:
    if (iswpunct(c))
        ungetwc(c, fp);

    return origpunct;
}

int main(void)
{
    wchar_t s[128];
    wint_t c;

    while ((c = read_punctstring(stdin, s)) != WEOF) {
        wprintf(L"%lc: %ls\n", c, s);
    }
}
```
:::

Sample Input:

::: {#cb838 .sourceCode}
``` {.sourceCode .default}
!foo#bar*baz
```
:::

Sample output:

::: {#cb839 .sourceCode}
``` {.sourceCode .default}
!: foo
#: bar
*: baz
```
:::

### See Also {#see-also-231 .unnumbered .unlisted}

[`fgetwc()`](wchar.html#man-getwc), [`ungetc()`](stdio.html#man-ungetc)

------------------------------------------------------------------------

## [30.12]{.header-section-number} `wcstod()` `wcstof()` `wcstold()` {#man-wcstod number="30.12"}

Convert a wide string to a floating point number

### Synopsis {#synopsis-245 .unnumbered .unlisted}

::: {#cb840 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

double wcstod(const wchar_t * restrict nptr, wchar_t ** restrict endptr);

float wcstof(const wchar_t * restrict nptr, wchar_t ** restrict endptr);

long double wcstold(const wchar_t * restrict nptr, wchar_t ** restrict endptr);
```
:::

### Description {#description-245 .unnumbered .unlisted}


These are the wide counterparts to the [`strtod()`](stdlib.html#man-strtod) family of functions. See [their reference pages for details](stdlib.html#man-strtod).

> 这些是[`strtod()`](stdlib.html#man-strtod)系列函数的宽版本。详情请参见[它们的参考页面](stdlib.html#man-strtod)。

### Return Value {#return-value-243 .unnumbered .unlisted}

Returns the string converted to a floating point value.

Returns `0` if there's no valid number in the string.


On overflow, returns an apporpriately-signed `HUGE_VAL`, `HUGE_VALF`. or `HUGE_VALL` depending on the return type, and `errno` is set to `ERANGE`.

> 当溢出时，根据返回类型返回一个适当符号的`HUGE_VAL`、`HUGE_VALF`或`HUGE_VALL`，并将`errno`设置为`ERANGE`。


On underflow, returns a number no greater than the smallest normalized positive number, appropriately signed. The implemention *might* set `errno` to `ERANGE`.

> 在溢出时，返回一个不大于最小正常化数字的数字，并带有适当的符号。实现可能会将`errno`设置为`ERANGE`。

### Example {#example-247 .unnumbered .unlisted}

::: {#cb841 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t *inp = L"   123.4567beej";
    wchar_t *badchar;

    double val = wcstod(inp, &badchar);

    wprintf(L"Converted string to %f\n", val);
    wprintf(L"Encountered bad characters: %ls\n", badchar);

    val = wcstod(L"987.654321beej", NULL);
    wprintf(L"Ignoring bad chars: %f\n", val);

    val = wcstod(L"11.2233", &badchar);

    if (*badchar == L'\0')
        wprintf(L"No bad chars: %f\n", val);
    else
        wprintf(L"Found bad chars: %f, %ls\n", val, badchar);
}
```
:::

Output:

::: {#cb842 .sourceCode}
``` {.sourceCode .default}
Converted string to 123.456700
Encountered bad characters: beej
Ignoring bad chars: 987.654321
No bad chars: 11.223300
```
:::

### See Also {#see-also-232 .unnumbered .unlisted}


[`wcstol()`](wchar.html#man-wcstol), [`strtod()`](stdlib.html#man-strtod), [`errno`](errno.html#errno)

> [`wcstol()`](wchar.html#man-wcstol)：将宽字符串转换为长整型
[`strtod()`](stdlib.html#man-strtod)：将字符串转换为双精度浮点数
[`errno`](errno.html#errno)：错误码

------------------------------------------------------------------------

## [30.13]{.header-section-number} `wcstol()` `wcstoll()` `wcstoul()` `wcstoull()` {#man-wcstol number="30.13"}

Convert a wide string to an integer value

### Synopsis {#synopsis-246 .unnumbered .unlisted}

::: {#cb843 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

long int wcstol(const wchar_t * restrict nptr,
                wchar_t ** restrict endptr, int base);

long long int wcstoll(const wchar_t * restrict nptr,
                      wchar_t ** restrict endptr, int base);

unsigned long int wcstoul(const wchar_t * restrict nptr,
                          wchar_t ** restrict endptr, int base);

unsigned long long int wcstoull(const wchar_t * restrict nptr,
                                wchar_t ** restrict endptr, int base);
```
:::

### Description {#description-246 .unnumbered .unlisted}


These are the wide counterparts to the [`strtol()`](stdlib.html#man-strtol) family of functions, so see [their reference pages for the details](stdlib.html#man-strtol).

> 这些是[`strtol()`](stdlib.html#man-strtol)系列函数的宽字符版本，详情请参阅[它们的参考页面](stdlib.html#man-strtol)。

### Return Value {#return-value-244 .unnumbered .unlisted}

Returns the integer value of the string.

If nothing can be found, `0` is returned.


If the result is out of range, the value returned is one of `LONG_MIN`, `LONG_MAX`, `LLONG_MIN`, `LLONG_MAX`, `ULONG_MAX` or `ULLONG_MAX`, as appropriate. And `errno` is set to `ERANGE`.

> 如果结果超出范围，返回的值将是`LONG_MIN`、`LONG_MAX`、`LLONG_MIN`、`LLONG_MAX`、`ULONG_MAX`或`ULLONG_MAX`之一，具体取决于情况。`errno`被设置为`ERANGE`。

### Example {#example-248 .unnumbered .unlisted}

::: {#cb844 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    // All output in decimal (base 10)

    wprintf(L"%ld\n", wcstol(L"123", NULL, 0));     // 123
    wprintf(L"%ld\n", wcstol(L"123", NULL, 10));    // 123
    wprintf(L"%ld\n", wcstol(L"101010", NULL, 2));  // binary, 42
    wprintf(L"%ld\n", wcstol(L"123", NULL, 8));     // octal, 83
    wprintf(L"%ld\n", wcstol(L"123", NULL, 16));    // hex, 291

    wprintf(L"%ld\n", wcstol(L"0123", NULL, 0));    // octal, 83
    wprintf(L"%ld\n", wcstol(L"0x123", NULL, 0));   // hex, 291

    wchar_t *badchar;
    long int x = wcstol(L"   1234beej", &badchar, 0);

    wprintf(L"Value is %ld\n", x);                  // Value is 1234
    wprintf(L"Bad chars at \"%ls\"\n", badchar);    // Bad chars at "beej"
}
```
:::

Output:

::: {#cb845 .sourceCode}
``` {.sourceCode .default}
123
123
42
83
291
83
291
Value is 1234
Bad chars at "beej"
```
:::

### See Also {#see-also-233 .unnumbered .unlisted}


[`wcstod()`](wchar.html#man-wcstod), [`strtol()`](stdlib.html#man-strtol), [`errno`](errno.html#errno), [`wcstoimax()`](inttypes.html#man-wcstoimax), [`wcstoumax()`](inttypes.html#man-wcstoimax)

> [`wcstod()`](wchar.html#man-wcstod)：将宽字符串转换为双精度浮点数
[`strtol()`](stdlib.html#man-strtol)：将字符串转换为长整数
[`errno`](errno.html#errno)：错误号
[`wcstoimax()`](inttypes.html#man-wcstoimax)：将宽字符串转换为最大整数
[`wcstoumax()`](inttypes.html#man-wcstoimax)：将宽字符串转换为最大无符号整数

------------------------------------------------------------------------

## [30.14]{.header-section-number} `wcscpy()` `wcsncpy()` {#man-wcscpy number="30.14"}

Copy a wide string

### Synopsis {#synopsis-247 .unnumbered .unlisted}

::: {#cb846 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

wchar_t *wcscpy(wchar_t * restrict s1, const wchar_t * restrict s2);

wchar_t *wcsncpy(wchar_t * restrict s1,
                 const wchar_t * restrict s2, size_t n);
```
:::

### Description {#description-247 .unnumbered .unlisted}


These are the wide versions of [`strcpy()`](stringref.html#man-strcpy) and [`strncpy()`](stringref.html#man-strcpy).

> 这些是[`strcpy()`](stringref.html#man-strcpy)和[`strncpy()`](stringref.html#man-strcpy)的宽版本。


They'll copy a string up to a wide NUL. Or, in the case of the safer `wcsncpy()`, until then or until `n` wide characters are copied.

> 他们会复制一个字符串直到宽度为零的NUL。或者，在更安全的`wcsncpy()`的情况下，直到复制了n个宽字符。


If the string in `s1` is shorter than `n`, `wcsncpy()` will pad `s2` with wide NUL characters until the `n`th wide character is reached.

> 如果字符串s1的长度小于n，wcsncpy()会使用宽度为NUL的字符填充s2，直到达到第n个宽字符。


Even though `wcsncpy()` is safer because it will never overrun the end of `s2` (assuming you set `n` correctly), it's still unsafe a NUL is not found in `s1` in the first `n` characters. In that case, `s2` will not be NUL-terminated. Always make sure `n` is greater than the string length of `s1`!

> 尽管`wcsncpy()`更安全，因为只要正确设置`n`，它就永远不会超过`s2`的末尾，但如果在前`n`个字符中没有找到NUL，它仍然是不安全的。在这种情况下，`s2`将不会以NUL结尾。一定要确保`n`大于`s1`的字符串长度！

### Return Value {#return-value-245 .unnumbered .unlisted}

Returns `s1`.

### Example {#example-249 .unnumbered .unlisted}

::: {#cb847 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t *s1 = L"Hello!";
    wchar_t s2[10];

    wcsncpy(s2, s1, 10);

    wprintf(L"\"%ls\"\n", s2);  // "Hello!"
}
```
:::

### See Also {#see-also-234 .unnumbered .unlisted}


[`wmemcpy()`](wchar.html#man-wmemcpy), [`wmemmove()`](wchar.html#man-wmemcpy) [`strcpy()`](stringref.html#man-strcpy), [`strncpy()`](stringref.html#man-strcpy)

> [`wmemcpy()`](wchar.html#man-wmemcpy)：宽字符内存拷贝
[`wmemmove()`](wchar.html#man-wmemcpy)：宽字符内存移动
[`strcpy()`](stringref.html#man-strcpy)：字符串拷贝
[`strncpy()`](stringref.html#man-strcpy)：字符串拷贝（有限长度）

------------------------------------------------------------------------

## [30.15]{.header-section-number} `wmemcpy()` `wmemmove()` {#man-wmemcpy number="30.15"}

Copy wide characters

### Synopsis {#synopsis-248 .unnumbered .unlisted}

::: {#cb848 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

wchar_t *wmemcpy(wchar_t * restrict s1,
                 const wchar_t * restrict s2, size_t n);

wchar_t *wmemmove(wchar_t *s1, const wchar_t *s2, size_t n);
```
:::

### Description {#description-248 .unnumbered .unlisted}


These are the wide versions of [`memcpy()`](stringref.html#man-memcpy) and [`memmove()`](stringref.html#man-memcpy).

> 这些是[`memcpy()`](stringref.html#man-memcpy)和[`memmove()`](stringref.html#man-memcpy)的宽版本。

They copy `n` wide characters from `s2` to `s1`.


They're the same except that `wmemmove()` is guaranteed to work with overlapping memory regions, and `wmemcpy()` is not.

> 他们是相同的，只是`wmemmove()`保证可以在重叠的内存区域中工作，而`wmemcpy()`则不行。

### Return Value {#return-value-246 .unnumbered .unlisted}

Both functions return the pointer `s1`.

### Example {#example-250 .unnumbered .unlisted}

::: {#cb849 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t s[100] = L"Goats";
    wchar_t t[100];

    wmemcpy(t, s, 6);       // Copy non-overlapping memory

    wmemmove(s + 2, s, 6);  // Copy overlapping memory

    wprintf(L"s is \"%ls\"\n", s);
    wprintf(L"t is \"%ls\"\n", t);
}
```
:::

Output:

::: {#cb850 .sourceCode}
``` {.sourceCode .default}
s is "GoGoats"
t is "Goats"
```
:::

### See Also {#see-also-235 .unnumbered .unlisted}


[`wcscpy()`](wchar.html#man-wcscpy), [`wcsncpy()`](wchar.html#man-wcscpy), [`memcpy()`](stringref.html#man-memcpy), [`memmove()`](stringref.html#man-memcpy)

> wcscpy()：复制宽字符串
wcsncpy()：复制宽字符串的一部分
memcpy()：复制内存块
memmove()：移动内存块

------------------------------------------------------------------------

## [30.16]{.header-section-number} `wcscat()` `wcsncat()` {#man-wcscat number="30.16"}

Concatenate wide strings

### Synopsis {#synopsis-249 .unnumbered .unlisted}

::: {#cb851 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

wchar_t *wcscat(wchar_t * restrict s1, const wchar_t * restrict s2);

wchar_t *wcsncat(wchar_t * restrict s1,
                 const wchar_t * restrict s2, size_t n);
```
:::

### Description {#description-249 .unnumbered .unlisted}


These are the wide variants of [`strcat()`](stringref.html#man-strcat) and [`strncat()`](stringref.html#man-strcat).

> 这些是[`strcat()`](stringref.html#man-strcat)和[`strncat()`](stringref.html#man-strcat)的广泛变体。

They concatenate `s2` onto the end of `s1`.


They're the same except `wcsncat()` gives you the option to limit the number of wide characters appended.

> 他们是一样的，只是`wcsncat()`给你提供了限制追加宽字符数量的选项。


Note that `wcsncat()` always adds a NUL terminator to the end, even if `n` characters were appended. So be sure to leave room for that.

> 注意，`wcsncat()`函数总是在末尾添加一个NUL终止符，即使只添加了`n`个字符。因此，一定要留出足够的空间。

### Return Value {#return-value-247 .unnumbered .unlisted}

Both functions return the pointer `s1`.

### Example {#example-251 .unnumbered .unlisted}

::: {#cb852 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t dest[30] = L"Hello";
    wchar_t *src = L", World!";
    wchar_t numbers[] = L"12345678";

    wprintf(L"dest before strcat: \"%ls\"\n", dest); // "Hello"

    wcscat(dest, src);
    wprintf(L"dest after strcat:  \"%ls\"\n", dest); // "Hello, world!"

    wcsncat(dest, numbers, 3); // strcat first 3 chars of numbers
    wprintf(L"dest after strncat: \"%ls\"\n", dest); // "Hello, world!123"
}
```
:::

### See Also {#see-also-236 .unnumbered .unlisted}


[`strcat()`](stringref.html#man-strcat), [`strncat()`](stringref.html#man-strcat)

> [`strcat()`](stringref.html#man-strcat)：字符串连接函数，将源字符串添加到目标字符串的末尾。
[`strncat()`](stringref.html#man-strcat)：字符串连接函数，将源字符串的前n个字符添加到目标字符串的末尾。

------------------------------------------------------------------------

## [30.17]{.header-section-number} `wcscmp()`, `wcsncmp()`, `wmemcmp()` {#man-wcscmp number="30.17"}

Compare wide strings or memory

### Synopsis {#synopsis-250 .unnumbered .unlisted}

::: {#cb853 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

int wcscmp(const wchar_t *s1, const wchar_t *s2);

int wcsncmp(const wchar_t *s1, const wchar_t *s2, size_t n);

int wmemcmp(const wchar_t *s1, const wchar_t *s2, size_t n);
```
:::

### Description {#description-250 .unnumbered .unlisted}


These are the wide variants of [`memcmp()`](stringref.html#man-strcmp), [`strcmp()`](stringref.html#man-strcmp), and [`strncmp()`](stringref.html#man-strcmp).

> 这些是[`memcmp()`](stringref.html#man-strcmp)、[`strcmp()`](stringref.html#man-strcmp)和[`strncmp()`](stringref.html#man-strcmp)的广泛变体。

`wcscmp()` and `wcsncmp()` both compare strings until a NUL character.

`wcsncmp()` also has the additional restriction that it will only compare the first `n` characters.

`wmemcmp()` is like `wcsncmp()` except it won't stop at a NUL.


The comparison is done against the character value (which might (or might not) be its Unicode code point).

> 比较是根据字符值（可能（或可能不）是它的Unicode代码点）进行的。

### Return Value {#return-value-248 .unnumbered .unlisted}

Returns zero if both regions are equal.


Returns a negative number if the region pointed to by `s1` is less than `s2`.

> 如果指向`s1`的区域小于`s2`，则返回一个负数。


Returns a positive number if the region pointed to by `s1` is greater than `s2`.

> 如果指向`s1`的区域大于`s2`，则返回一个正数。

### Example {#example-252 .unnumbered .unlisted}

::: {#cb854 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t *s1 = L"Muffin";
    wchar_t *s2 = L"Muffin Sandwich";
    wchar_t *s3 = L"Muffin";

    wprintf(L"%d\n", wcscmp(L"Biscuits", L"Kittens")); // <0 since 'B' < 'K'
    wprintf(L"%d\n", wcscmp(L"Kittens", L"Biscuits")); // >0 since 'K' > 'B'

    if (wcscmp(s1, s2) == 0)
        wprintf(L"This won't get printed because the strings differ\n");

    if (wcscmp(s1, s3) == 0)
        wprintf(L"This will print because s1 and s3 are the same\n");

    // this is a little weird...but if the strings are the same, it'll
    // return zero, which can also be thought of as "false". Not-false
    // is "true", so (!wcscmp()) will be true if the strings are the
    // same. yes, it's odd, but you see this all the time in the wild
    // so you might as well get used to it:

    if (!wcscmp(s1, s3))
        wprintf(L"The strings are the same!\n");

    if (!wcsncmp(s1, s2, 6))
        wprintf(L"The first 6 characters of s1 and s2 are the same\n");
}
```
:::

Output:

::: {#cb855 .sourceCode}
``` {.sourceCode .default}
-1
1
This will print because s1 and s3 are the same
The strings are the same!
The first 6 characters of s1 and s2 are the same
```
:::

### See Also {#see-also-237 .unnumbered .unlisted}


[`wcscoll()`](wchar.html#man-wcscoll), [`memcmp()`](stringref.html#man-strcmp), [`strcmp()`](stringref.html#man-strcmp), [`strncmp()`](stringref.html#man-strcmp)

> [`wcscoll()`](wchar.html#man-wcscoll)：比较两个宽字符串
[`memcmp()`](stringref.html#man-strcmp)：比较两个内存块
[`strcmp()`](stringref.html#man-strcmp)：比较两个字符串
[`strncmp()`](stringref.html#man-strcmp)：比较两个字符串的前n个字符

------------------------------------------------------------------------

## [30.18]{.header-section-number} `wcscoll()` {#man-wcscoll number="30.18"}

Compare two wide strings accounting for locale

### Synopsis {#synopsis-251 .unnumbered .unlisted}

::: {#cb856 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

int wcscoll(const wchar_t *s1, const wchar_t *s2);
```
:::

### Description {#description-251 .unnumbered .unlisted}


This is the wide version of [`strcoll()`](stringref.html#man-strcoll). See [`that reference page`](stringref.html#man-strcoll) for details.

> 这是[`strcoll()`](stringref.html#man-strcoll)的宽版本。有关详细信息，请参阅[`该参考页面`](stringref.html#man-strcoll)。


This is slower than `wcscmp()`, so only use it if you need the locale-specific compare.

> 这比`wcscmp()`慢，所以只有在需要特定语言环境的比较时才使用它。

### Return Value {#return-value-249 .unnumbered .unlisted}

Returns zero if both regions are equal in this locale.


Returns a negative number if the region pointed to by `s1` is less than `s2` in this locale.

> 如果在本地区指向的区域s1小于s2，则返回负数。


Returns a positive number if the region pointed to by `s1` is greater than `s2` in this locale.

> 如果在这个区域中，`s1`指向的区域大于`s2`，则返回一个正数。

### Example {#example-253 .unnumbered .unlisted}

::: {#cb857 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <locale.h>

int main(void)
{
    setlocale(LC_ALL, "");

    // If your source character set doesn't support "é" in a string
    // you can replace it with `\u00e9`, the Unicode code point
    // for "é".

    wprintf(L"%d\n", wcscmp(L"é", L"f"));   // Reports é > f, yuck.
    wprintf(L"%d\n", wcscoll(L"é", L"f"));  // Reports é < f, yay!
}
```
:::

### See Also {#see-also-238 .unnumbered .unlisted}


[`wcscmp()`](wchar.html#man-wcscmp), [`wcsxfrm()`](wchar.html#man-wcsxfrm), [`strcoll()`](stringref.html#man-strcoll)

> [`wcscmp()`](wchar.html#man-wcscmp): 比较两个宽字符串
[`wcsxfrm()`](wchar.html#man-wcsxfrm): 将宽字符串转换为排序形式
[`strcoll()`](stringref.html#man-strcoll): 比较两个字符串，使用本地化字符排序规则

------------------------------------------------------------------------

## [30.19]{.header-section-number} `wcsxfrm()` {#man-wcsxfrm number="30.19"}

Transform a wide string for comparing based on locale

### Synopsis {#synopsis-252 .unnumbered .unlisted}

::: {#cb858 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t wcsxfrm(wchar_t * restrict s1,
               const wchar_t * restrict s2, size_t n);
```
:::

### Description {#description-252 .unnumbered .unlisted}


This is the wide variant of [`strxfrm()`](stringref.html#man-strxfrm). See [that reference page](stringref.html#man-strxfrm) for details.

> 这是[`strxfrm()`](stringref.html#man-strxfrm)的宽变体。详情请参阅[该参考页面](stringref.html#man-strxfrm)。

### Return Value {#return-value-250 .unnumbered .unlisted}

Returns the length of the transformed wide string in wide characters.


If the return value is greater than `n`, all bets are off for the result in `s1`.

> 如果返回值大于n，对s1的结果所有赌注都无效。

### Example {#example-254 .unnumbered .unlisted}

::: {#cb859 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <locale.h>
#include <stdlib.h>

// Transform a string for comparison, returning a malloc'd
// result
wchar_t *get_xfrm_str(wchar_t *s)
{
    int len = wcsxfrm(NULL, s, 0) + 1;
    wchar_t *d = malloc(len * sizeof(wchar_t));

    wcsxfrm(d, s, len);

    return d;
}

// Does half the work of a regular wcscoll() because the second
// string arrives already transformed.
int half_wcscoll(wchar_t *s1, wchar_t *s2_transformed)
{
    wchar_t *s1_transformed = get_xfrm_str(s1);

    int result = wcscmp(s1_transformed, s2_transformed);

    free(s1_transformed);

    return result;
}

int main(void)
{
    setlocale(LC_ALL, "");

    // Pre-transform the string to compare against
    wchar_t *s = get_xfrm_str(L"éfg");

    // Repeatedly compare against "éfg" 
    wprintf(L"%d\n", half_wcscoll(L"fgh", s));  // "fgh" > "éfg"
    wprintf(L"%d\n", half_wcscoll(L"àbc", s));  // "àbc" < "éfg"
    wprintf(L"%d\n", half_wcscoll(L"ĥij", s));  // "ĥij" > "éfg"
    
    free(s);
}
```
:::

Output:

::: {#cb860 .sourceCode}
``` {.sourceCode .default}
1
-1
1
```
:::

### See Also {#see-also-239 .unnumbered .unlisted}


[`wcscmp()`](wchar.html#man-wcscmp), [`wcscoll()`](wchar.html#man-wcscoll), [`strxfrm()`](stringref.html#man-strxfrm)

> [`wcscmp()`](wchar.html#man-wcscmp)：比较两个宽字符串
[`wcscoll()`](wchar.html#man-wcscoll)：比较两个宽字符串，并根据区域设置进行排序
[`strxfrm()`](stringref.html#man-strxfrm)：将字符串转换为可排序的形式

------------------------------------------------------------------------

## [30.20]{.header-section-number} `wcschr()` `wcsrchr()` {#man-wcschr number="30.20"}

Find a wide character in a wide string

### Synopsis {#synopsis-253 .unnumbered .unlisted}

::: {#cb861 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

wchar_t *wcschr(const wchar_t *s, wchar_t c);

wchar_t *wcsrchr(const wchar_t *s, wchar_t c);

wchar_t *wmemchr(const wchar_t *s, wchar_t c, size_t n);
```
:::

### Description {#description-253 .unnumbered .unlisted}


These are the wide equivalents to [`strchr()`](stringref.html#man-strchr), [`strrchr()`](stringref.html#man-strchr), and [`memchr()`](stringref.html#man-strchr).

> 这些是[`strchr()`](stringref.html#man-strchr)、[`strrchr()`](stringref.html#man-strchr)和[`memchr()`](stringref.html#man-strchr)的宽等效物。


They search for wide characters in a wide string from the front (`wcschr()`), the end (`wcsrchr()`) or for an arbitrary number of wide characters (`wmemchr()`).

> 他们从前面（`wcschr()`）、末尾（`wcsrchr()`）或任意多个宽字符（`wmemchr()`）中搜索宽字符串。

### Return Value {#return-value-251 .unnumbered .unlisted}


All three functions return a pointer to the wide character found, or `NULL` if the character, sadly, isn't found.

> 所有三个函数都会返回一个指向找到的宽字符的指针，如果没有找到这个字符，则返回`NULL`。

### Example {#example-255 .unnumbered .unlisted}

::: {#cb862 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    // "Hello, world!"
    //       ^  ^   ^
    //       A  B   C

    wchar_t *str = L"Hello, world!";
    wchar_t *p;

    p = wcschr(str, ',');       // p now points at position A
    p = wcsrchr(str, 'o');      // p now points at position B

    p = wmemchr(str, '!', 13);   // p now points at position C

    // repeatedly find all occurrences of the letter 'B'
    str = L"A BIG BROWN BAT BIT BEEJ";

    for(p = wcschr(str, 'B'); p != NULL; p = wcschr(p + 1, 'B')) {
        wprintf(L"Found a 'B' here: %ls\n", p);
    }
}
```
:::

Output:

::: {#cb863 .sourceCode}
``` {.sourceCode .default}
Found a 'B' here: BIG BROWN BAT BIT BEEJ
Found a 'B' here: BROWN BAT BIT BEEJ
Found a 'B' here: BAT BIT BEEJ
Found a 'B' here: BIT BEEJ
Found a 'B' here: BEEJ
```
:::

### See Also {#see-also-240 .unnumbered .unlisted}


[`strchr()`](stringref.html#man-strchr), [`strrchr()`](stringref.html#man-strchr), [`memchr()`](stringref.html#man-strchr)

> `strchr()`，`strrchr()`，`memchr()`

------------------------------------------------------------------------

## [30.21]{.header-section-number} `wcsspn()` `wcscspn()` {#man-wcsspn number="30.21"}


Return the length of a wide string consisting entirely of a set of wide characters, or of not a set of wide characters

> 返回由一组宽字符或者非宽字符组成的宽字符串的长度。

### Synopsis {#synopsis-254 .unnumbered .unlisted}

::: {#cb864 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t wcsspn(const wchar_t *s1, const wchar_t *s2);

size_t wcscspn(const wchar_t *s1, const wchar_t *s2);
```
:::

### Description {#description-254 .unnumbered .unlisted}


The are the wide character counterparts to \[`strspn()`\] (#man-strspn)and [`strcspn()`](stringref.html#man-strspn).

> 他们是\[`strspn()`\] (#man-strspn)和[`strcspn()`](stringref.html#man-strspn)的宽字符对应物。


They compute the length of the string pointed to by `s1` consisting entirely of the characters found in `s2`. Or, in the case of `wcscspn()`, the characters *not* found in `s2`.

> 他们计算由`s1`指向的字符串的长度，该字符串完全由`s2`中找到的字符组成。或者，在`wcscspn()`的情况下，是没有在`s2`中找到的字符。

### Return Value {#return-value-252 .unnumbered .unlisted}


The length of the string pointed to by `s1` consisting solely of the characters in `s2` (in the case of `wcsspn()`) or of the characters *not* in `s2` (in th ecase of `wcscspn()`).

> 指向s1的字符串的长度仅由s2中的字符组成（在wcsspn（）的情况下）或不在s2中的字符（在wcscspn（）的情况下）。

### Example {#example-256 .unnumbered .unlisted}

::: {#cb865 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t str1[] = L"a banana";
    wchar_t str2[] = L"the bolivian navy on maneuvers in the south pacific";
    int n;

    // how many letters in str1 until we reach something that's not a vowel?
    n = wcsspn(str1, L"aeiou");
    wprintf(L"%d\n", n);  // n == 1, just "a"

    // how many letters in str1 until we reach something that's not a, b,
    // or space?
    n = wcsspn(str1, L"ab ");
    wprintf(L"%d\n", n);  // n == 4, "a ba"

    // how many letters in str2 before we get a "y"?
    n = wcscspn(str2, L"y");
    wprintf(L"%d\n", n);  // n = 16, "the bolivian nav"
}
```
:::

### See Also {#see-also-241 .unnumbered .unlisted}


[`wcschr()`](wchar.html#man-wcschr), [`wcsrchr()`](wchar.html#man-wcschr), [`strspn()`](stringref.html#man-strspn)

> `wcschr()`：在宽字符串中查找字符
`wcsrchr()`：在宽字符串中查找最后一个字符
`strspn()`：计算字符串中连续字符的长度

------------------------------------------------------------------------

## [30.22]{.header-section-number} `wcspbrk()` {#man-wcspbrk number="30.22"}

Search a wide string for one of a set of wide characters

### Synopsis {#synopsis-255 .unnumbered .unlisted}

::: {#cb866 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

wchar_t *wcspbrk(const wchar_t *s1, const wchar_t *s2);
```
:::

### Description {#description-255 .unnumbered .unlisted}


This is the wide character variant of [`strpbrk()`](stringref.html#man-strpbrk).

> 这是[`strpbrk()`](stringref.html#man-strpbrk)的宽字符变体。


It finds the first occurrance of any of a set of wide characters in a wide string.

> 它在宽字符串中查找一组宽字符的第一次出现。

### Return Value {#return-value-253 .unnumbered .unlisted}


Returns a pointer to the first character in the string `s1` that exists in the string `s2`.

> 返回指向字符串`s1`中存在于字符串`s2`中的第一个字符的指针。

Or `NULL` if none of the characters in `s2` can be found in `s1`.

### Example {#example-257 .unnumbered .unlisted}

::: {#cb867 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    //  p points here after wcspbrk
    //                  v
    wchar_t *s1 = L"Hello, world!";
    wchar_t *s2 = L"dow!";  // Match any of these chars

    wchar_t *p = wcspbrk(s1, s2);  // p points to the o

    wprintf(L"%ls\n", p);  // "o, world!"
}
```
:::

### See Also {#see-also-242 .unnumbered .unlisted}


[`wcschr()`](wchar.html#man-wcschr), [`wmemchr()`](wchar.html#man-wcschr), [`strpbrk()`](stringref.html#man-strpbrk)

> `wcschr()`：在宽字符串中搜索字符
`wmemchr()`：在宽字符内存块中搜索字符
`strpbrk()`：在字符串中搜索指定字符集中的字符

------------------------------------------------------------------------

## [30.23]{.header-section-number} `wcsstr()` {#man-wcsstr number="30.23"}

Find a wide string in another wide string

### Synopsis {#synopsis-256 .unnumbered .unlisted}

::: {#cb868 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

wchar_t *wcsstr(const wchar_t *s1, const wchar_t *s2);
```
:::

### Description {#description-256 .unnumbered .unlisted}

This is the wide variant of [`strstr()`](stringref.html#man-strstr).

It locates a substring in a string.

### Return Value {#return-value-254 .unnumbered .unlisted}

Returns a pointer to the location in `s1` that contains `s2`.

Or `NULL` if `s2` cannot be found in `s1`.

### Example {#example-258 .unnumbered .unlisted}

::: {#cb869 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t *str = L"The quick brown fox jumped over the lazy dogs.";
    wchar_t *p;

    p = wcsstr(str, L"lazy");
    wprintf(L"%ls\n", p == NULL? L"null": p); // "lazy dogs."

    // p is NULL after this, since the string "wombat" isn't in str:
    p = wcsstr(str, L"wombat");
    wprintf(L"%ls\n", p == NULL? L"null": p); // "null"
}
```
:::

### See Also {#see-also-243 .unnumbered .unlisted}


[`wcschr()`](wchar.html#man-wcschr), [`wcsrchr()`](wchar.html#man-wcschr), [`wcsspn()`](wchar.html#man-wcsspn), [`wcscspn()`](wchar.html#man-wcsspn), [`strstr()`](stringref.html#man-strstr)

> [`wcschr()`](wchar.html#man-wcschr)：在宽字符串中查找字符
[`wcsrchr()`](wchar.html#man-wcschr)：在宽字符串中查找最后一个字符
[`wcsspn()`](wchar.html#man-wcsspn)：计算宽字符串中连续的字符数
[`wcscspn()`](wchar.html#man-wcsspn)：计算宽字符串中不包含指定字符的字符数
[`strstr()`](stringref.html#man-strstr)：在字符串中查找子串

------------------------------------------------------------------------

## [30.24]{.header-section-number} `wcstok()` {#man-wcstok number="30.24"}

Tokenize a wide string

### Synopsis {#synopsis-257 .unnumbered .unlisted}

::: {#cb870 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>
wchar_t *wcstok(wchar_t * restrict s1, const wchar_t * restrict s2,
                wchar_t ** restrict ptr); 
```
:::

### Description {#description-257 .unnumbered .unlisted}

This is the wide version of [`strtok()`](stringref.html#man-strtok).


And, like that one, it modifies the string `s1`. So make a copy of it first if you want to preserve the original.

> 如果你想保留原始字符串，那么首先要先复制一份，就像那个一样，它会修改字符串`s1`。


One key difference is that `wcstok()` can be threadsafe because you pass in the pointer `ptr` to the current state of the transformation. This gets initializers for you when `s1` is initially passed in as non-`NULL`. (Subsequent calls with a `NULL` `s1` cause the state to update.)

> 一个关键的不同之处是，wcstok（）可以是线程安全的，因为您传递指向当前转换状态的指针ptr。当s1最初传入为非NULL时，它会为您初始化。（随后使用NULL s1调用会导致状态更新。）

### Return Value {#return-value-255 .unnumbered .unlisted}

### Example {#example-259 .unnumbered .unlisted}

::: {#cb871 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    // break up the string into a series of space or
    // punctuation-separated words
    wchar_t str[] = L"Where is my bacon, dude?";
    wchar_t *token;
    wchar_t *state;

    // Note that the following if-do-while construct is very very
    // very very very common to see when using strtok().

    // grab the first token (making sure there is a first token!)
    if ((token = wcstok(str, L".,?! ", &state)) != NULL) {
        do {
            wprintf(L"Word: \"%ls\"\n", token);

            // now, the while continuation condition grabs the
            // next token (by passing NULL as the first param)
            // and continues if the token's not NULL:
        } while ((token = wcstok(NULL, L".,?! ", &state)) != NULL);
    }
}
```
:::

Output:

::: {#cb872 .sourceCode}
``` {.sourceCode .default}
Word: "Where"
Word: "is"
Word: "my"
Word: "bacon"
Word: "dude"
```
:::

### See Also {#see-also-244 .unnumbered .unlisted}

[`strtok()`](stringref.html#man-strtok)

------------------------------------------------------------------------

## [30.25]{.header-section-number} `wcslen()` {#man-wcslen number="30.25"}

Returns the length of a wide string

### Synopsis {#synopsis-258 .unnumbered .unlisted}

::: {#cb873 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t wcslen(const wchar_t *s);
```
:::

### Description {#description-258 .unnumbered .unlisted}

This is the wide counterpart to [`strlen()`](stringref.html#man-strlen).

### Return Value {#return-value-256 .unnumbered .unlisted}

Returns the number of wide characters before the wide NUL terminator.

### Example {#example-260 .unnumbered .unlisted}

::: {#cb874 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wchar_t *s = L"Hello, world!"; // 13 characters

    // prints "The string is 13 characters long.":

    wprintf(L"The string is %zu characters long.\n", wcslen(s));
}
```
:::

### See Also {#see-also-245 .unnumbered .unlisted}

[`strlen()`](stringref.html#man-strlen)

------------------------------------------------------------------------

## [30.26]{.header-section-number} `wcsftime()` {#man-wcsftime number="30.26"}

Formatted date and time output

### Synopsis {#synopsis-259 .unnumbered .unlisted}

::: {#cb875 .sourceCode}
``` {.sourceCode .c}
#include <time.h>
#include <wchar.h>

size_t wcsftime(wchar_t * restrict s, size_t maxsize,
                const wchar_t * restrict format,
                const struct tm * restrict timeptr);
```
:::

### Description {#description-259 .unnumbered .unlisted}


This is the wide equivalent to [`strftime()`](time.html#man-strftime). See that reference page for details.

> 这是[`strftime()`](time.html#man-strftime)的宽泛等价物。有关详细信息，请参阅该参考页面。

`maxsize` here refers to the maximum number of wide characters that can be in the result string.

### Return Value {#return-value-257 .unnumbered .unlisted}

If successful, returns the number of wide characters written.


If not successful because the result couldn't fit in the space alloted, `0` is returned and the contents of the string could be anything.

> 如果由于结果无法放入分配的空间而未能成功，则返回`0`，字符串的内容可以是任何内容。

### Example {#example-261 .unnumbered .unlisted}

::: {#cb876 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>
#include <time.h>

#define BUFSIZE 128

int main(void)
{
    wchar_t s[BUFSIZE];
    time_t now = time(NULL);

    // %c: print date as per current locale
    wcsftime(s, BUFSIZE, L"%c", localtime(&now));
    wprintf(L"%ls\n", s);   // Sun Feb 28 22:29:00 2021

    // %A: full weekday name
    // %B: full month name
    // %d: day of the month
    wcsftime(s, BUFSIZE, L"%A, %B %d", localtime(&now));
    wprintf(L"%ls\n", s);   // Sunday, February 28

    // %I: hour (12 hour clock)
    // %M: minute
    // %S: second
    // %p: AM or PM
    wcsftime(s, BUFSIZE, L"It's %I:%M:%S %p", localtime(&now));
    wprintf(L"%ls\n", s);   // It's 10:29:00 PM

    // %F: ISO 8601 yyyy-mm-dd
    // %T: ISO 8601 hh:mm:ss
    // %z: ISO 8601 time zone offset
    wcsftime(s, BUFSIZE, L"ISO 8601: %FT%T%z", localtime(&now));
    wprintf(L"%ls\n", s);   // ISO 8601: 2021-02-28T22:29:00-0800
}
```
:::

### See Also {#see-also-246 .unnumbered .unlisted}

[`strftime()`](time.html#man-strftime)

------------------------------------------------------------------------

## [30.27]{.header-section-number} `btowc()` `wctob()` {#man-btowc number="30.27"}

Convert a single byte character to a wide character

### Synopsis {#synopsis-260 .unnumbered .unlisted}

::: {#cb877 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

wint_t btowc(int c);

int wctob(wint_t c);
```
:::

### Description {#description-260 .unnumbered .unlisted}


These functions convert between single byte characters and wide characters, and vice-versa.

> 这些函数可以在单字节字符和宽字符之间进行转换，反之亦然。


Even though `int`s are involved, don't let this mislead you; they're effectively converted to `unsigned char`s internally.

> 即使涉及到`int`，也不要被误导；它们在内部被有效地转换为`unsigned char`。


The characters in the basic character set are guaranteed to be a single byte.

> 字符集中的字符保证只有一个字节。

### Return Value {#return-value-258 .unnumbered .unlisted}

`btowc()` returns the single-byte character as a wide character. Returns `WEOF` if `EOF` is passed in, or if the byte doesn't correspond to a valid wide character.

`wctob()` returns the wide character as a single-byte character. Returns `EOF` if `WEOF` is passed in, or if the wide character doesn't correspond to a value single-byte character.


See [`mbtowc()`](stdlib.html#man-mbtowc) and [`wctomb()`](stdlib.html#man-wctomb) for multibyte to wide character conversion.

> 查看[`mbtowc()`](stdlib.html#man-mbtowc)和[`wctomb()`](stdlib.html#man-wctomb)以实现多字节到宽字符的转换。

### Example {#example-262 .unnumbered .unlisted}

::: {#cb878 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <wchar.h>

int main(void)
{
    wint_t wc = btowc('B');    // Convert single byte to wide char

    wprintf(L"Wide character: %lc\n", wc);

    unsigned char c = wctob(wc);  // Convert back to single byte

    wprintf(L"Single-byte character: %c\n", c);
}
```
:::

Output:

::: {#cb879 .sourceCode}
``` {.sourceCode .default}
Wide character: B
Single-byte character: B
```
:::

### See Also {#see-also-247 .unnumbered .unlisted}


[`mbtowc()`](stdlib.html#man-mbtowc), [`wctomb()`](stdlib.html#man-wctomb)

> [mbtowc()](stdlib.html#man-mbtowc)，[wctomb()](stdlib.html#man-wctomb)

------------------------------------------------------------------------

## [30.28]{.header-section-number} `mbsinit()` {#man-mbsinit number="30.28"}

Test if an `mbstate_t` is in the initial conversion state

### Synopsis {#synopsis-261 .unnumbered .unlisted}

::: {#cb880 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

int mbsinit(const mbstate_t *ps);
```
:::

### Description {#description-261 .unnumbered .unlisted}


For a given conversion state in a `mbstate_t` variable, this function determines if it's in the initial conversion state.

> 对于`mbstate_t`变量中的给定转换状态，此函数确定它是否处于初始转换状态。

### Return Value {#return-value-259 .unnumbered .unlisted}


Returns non-zero if the value pointed to by `ps` is in the initial conversion state, or if `ps` is `NULL`.

> 如果指针ps指向的值处于初始转换状态，或者ps为NULL，则返回非零值。


Returns `0` if the value pointed to by `ps` is **not** in the initial conversion state.

> 如果指向ps的值不在初始转换状态中，则返回`0`。

### Example {#example-263 .unnumbered .unlisted}


For me, this example doesn't do anything exciting, saying that the `mbstate_t` variable is always in the initial state. Yay.

> 对我来说，这个例子没有做任何令人兴奋的事情，只是说`mbstate_t`变量总是处于初始状态。太棒了！


But if have a stateful encoding like 2022-JP, try messing around with this to see if you can get into an intermediate state.

> 如果有一个有状态的编码，比如2022-JP，试着摆弄一下看看能否进入一个中间状态。


This program has a bit of code at the top that reports if your locale's encoding requires any state.

> 这个程序在顶部有一段代码，用于报告你的本地编码是否需要任何状态。

::: {#cb881 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <locale.h>   // For setlocale()
#include <string.h>   // For memset()
#include <stdlib.h>   // For mbtowc()
#include <wchar.h>

int main(void)
{
    mbstate_t state;
    wchar_t wc[128];

    setlocale(LC_ALL, "");

    int is_state_dependent = mbtowc(NULL, NULL, 0);

    wprintf(L"Is encoding state dependent? %d\n", is_state_dependent);

    memset(&state, 0, sizeof state);  // Set to initial state

    wprintf(L"In initial conversion state? %d\n", mbsinit(&state));

    mbrtowc(wc, "B", 5, &state);

    wprintf(L"In initial conversion state? %d\n", mbsinit(&state));
}
```
:::

### See Also {#see-also-248 .unnumbered .unlisted}


[`mbtowc()`](stdlib.html#man-mbtowc), [`wctomb()`](stdlib.html#man-wctomb), [`mbrtowc()`](wchar.html#man-mbrtowc), [`wcrtomb()`](wchar.html#man-wcrtomb)

> [`mbtowc()`](stdlib.html#man-mbtowc)：将多字节编码转换为宽字符
[`wctomb()`](stdlib.html#man-wctomb)：将宽字符转换为多字节编码
[`mbrtowc()`](wchar.html#man-mbrtowc)：将多字节序列转换为宽字符
[`wcrtomb()`](wchar.html#man-wcrtomb)：将宽字符转换为多字节序列

------------------------------------------------------------------------

## [30.29]{.header-section-number} `mbrlen()` {#man-mbrlen number="30.29"}

Compute the number of bytes in a multibyte character, restartably

### Synopsis {#synopsis-262 .unnumbered .unlisted}

::: {#cb882 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t mbrlen(const char * restrict s, size_t n, mbstate_t * restrict ps);
```
:::

### Description {#description-262 .unnumbered .unlisted}

This is the restartable version of [`mblen()`](stdlib.html#man-mblen).


It inspects at most `n` bytes of the string `s` to see how many bytes in this character.

> 它最多检查字符串`s`中的`n`个字节，以查看该字符中有多少个字节。

The conversion state is stored in `ps`.


This function doesn't have the functionality of `mblen()` that allowed you to query if this character encoding was stateful and to reset the internal state.

> 这个函数没有`mblen（）`的功能，它允许您查询此字符编码是否是有状态的，以及重置内部状态。

### Return Value {#return-value-260 .unnumbered .unlisted}

Returns the number of bytes required for this multibyte character.


Returns `(size_t)(-1)` if the data in `s` is not a valid multibyte character.

> 如果s中的数据不是有效的多字节字符，则返回（size_t）（-1）。


Returns `(size_t)(-2)` if the data is `s` is a valid but not complete multibyte character.

> 如果数据`s`是有效但不完整的多字节字符，则返回`（size_t）（-2）`。

### Example {#example-264 .unnumbered .unlisted}


If your character set doesn't support the Euro symbol "€", substitute the Unicode escape sequence `\u20ac`, below.

> 如果您的字符集不支持欧元符号“€”，请在下面替换为Unicode转义序列“\u20ac”。

::: {#cb883 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <locale.h>   // For setlocale()
#include <string.h>   // For memset()
#include <wchar.h>

int main(void)
{
    mbstate_t state;
    int len;

    setlocale(LC_ALL, "");

    memset(&state, 0, sizeof state);  // Set to initial state

    len = mbrlen("B", 5, &state);

    wprintf(L"Length of 'B' is %d byte(s)\n", len);

    len = mbrlen("€", 5, &state);

    wprintf(L"Length of '€' is %d byte(s)\n", len);
}
```
:::

Output:

::: {#cb884 .sourceCode}
``` {.sourceCode .default}
Length of 'B' is 1 byte(s)
Length of '€' is 3 byte(s)
```
:::

### See Also {#see-also-249 .unnumbered .unlisted}

[`mblen()`](stdlib.html#man-mblen)

------------------------------------------------------------------------

## [30.30]{.header-section-number} `mbrtowc()` {#man-mbrtowc number="30.30"}

Convert multibyte to wide characters restartably

### Synopsis {#synopsis-263 .unnumbered .unlisted}

::: {#cb885 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t mbrtowc(wchar_t * restrict pwc, const char * restrict s,
               size_t n, mbstate_t * restrict ps);
```
:::

### Description {#description-263 .unnumbered .unlisted}


This is the restartable counterpart to [`mbtowc()`](stdlib.html#man-mbtowc).

> 这是[`mbtowc()`](stdlib.html#man-mbtowc)的可重新启动对应物。


It converts individual characters from multibyte to wide, tracking the conversion state in the variable pointed to by `ps`.

> 它将多字节的单个字符转换为宽字符，并将转换状态跟踪到由`ps`指向的变量中。

At most `n` bytes are inspected for conversion to a wide character.


These two variants are identical and cause the state pointed to by `ps` to be set to the initial conversion state:

> 这两种变体是相同的，会导致`ps`指向的状态被设置为初始转换状态：

::: {#cb886 .sourceCode}
``` {.sourceCode .c}
mbrtowc(NULL, NULL, 0, &state);
mbrtowc(NULL, "", 1, &state);
```
:::


Also, if you're just interested in the length in bytes of the multibyte character, you can pass `NULL` for `pwc` and nothing will be stored for the wide character:

> 如果您只对多字节字符的长度（以字节为单位）感兴趣，可以将`NULL`传递给`pwc`，宽字符将不会存储任何内容。

::: {#cb887 .sourceCode}
``` {.sourceCode .c}
int len = mbrtowc(NULL, "€", 5, &state);
```
:::


This function doesn't have the functionality of `mbtowc()` that allowed you to query if this character encoding was stateful and to reset the internal state.

> 这个函数没有`mbtowc()`的功能，它允许你查询这种字符编码是否是有状态的，以及重置内部状态。

### Return Value {#return-value-261 .unnumbered .unlisted}


On success, returns a positive number corresponding to the number of bytes in the multibyte character.

> 如果成功，返回一个正数，对应于多字节字符中的字节数。

Returns `0` if the character encoded is a wide NUL character.


Returns `(size_t)(-1)` if the data in `s` is not a valid multibyte character.

> 如果s中的数据不是有效的多字节字符，则返回（size_t）（-1）。


Returns `(size_t)(-2)` if the data is `s` is a valid but not complete multibyte character.

> 如果数据`s`是有效但不完整的多字节字符，则返回（size_t）（-2）。

### Example {#example-265 .unnumbered .unlisted}


If your character set doesn't support the Euro symbol "€", substitute the Unicode escape sequence `\u20ac`, below.

> 如果您的字符集不支持欧元符号"€"，请在下面替换为Unicode转义序列\u20ac。

::: {#cb888 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <string.h>  // For memset()
#include <stdlib.h>  // For mbtowc()
#include <locale.h>  // For setlocale()
#include <wchar.h>

int main(void)
{
    mbstate_t state;

    memset(&state, 0, sizeof state);

    setlocale(LC_ALL, "");

    wprintf(L"State dependency: %d\n", mbtowc(NULL, NULL, 0));

    wchar_t wc;
    int bytes;

    bytes = mbrtowc(&wc, "€", 5, &state);

    wprintf(L"L'%lc' takes %d bytes as multibyte char '€'\n", wc, bytes);
}
```
:::

Output on my system:

::: {#cb889 .sourceCode}
``` {.sourceCode .default}
State dependency: 0
L'€' takes 3 bytes as multibyte char '€'
```
:::

### See Also {#see-also-250 .unnumbered .unlisted}


[`mbtowc()`](stdlib.html#man-mbtowc), [`wcrtomb()`](wchar.html#man-wcrtomb)

> [mbtowc()](stdlib.html#man-mbtowc)，[wcrtomb()](wchar.html#man-wcrtomb)

------------------------------------------------------------------------

## [30.31]{.header-section-number} `wcrtomb()` {#man-wcrtomb number="30.31"}

Convert wide to multibyte characters restartably

### Synopsis {#synopsis-264 .unnumbered .unlisted}

::: {#cb890 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t wcrtomb(char * restrict s, wchar_t wc, mbstate_t * restrict ps);
```
:::

### Description {#description-264 .unnumbered .unlisted}


This is the restartable counterpart to [`wctomb()`](stdlib.html#man-wctomb).

> 这是[`wctomb()`](stdlib.html#man-wctomb)的可重新启动对应物。


It converts individual characters from wide to multibyte, tracking the conversion state in the variable pointed to by `ps`.

> 它将单个字符从宽字节转换为多字节，并将转换状态跟踪到由`ps`指向的变量中。


The destination array `s` should be at least `MB_CUR_MAX`[^78^](footnotes.html#fn78){#fnref78 .footnote-ref role="doc-noteref"} bytes in size---you won't get anything bigger back from this function.

> 目标数组`s`的大小至少应为`MB_CUR_MAX`[^78^]（脚注.html#fn78）{#fnref78 .footnote-ref role="doc-noteref"}字节，否则该函数不会返回更大的值。

Note that the values in this result array won't be NUL-terminated.


If you pass a wide NUL character in, the result will contain any bytes needed to restore the conversion state to its initial state followed by a NUL character, and the state pointed to by `ps` will be reset to its initial state:

> 如果你传入一个宽NUL字符，结果将包含任何字节，以恢复转换状态到其初始状态，后跟一个NUL字符，并且`ps`指向的状态将重置为其初始状态：

::: {#cb891 .sourceCode}
``` {.sourceCode .c}
// Reset state
wcrtomb(mb, L'\0', &state)
```
:::


If you don't care about the results (i.e. you're just interested in resetting the state or getting the return value), you can do this by passing `NULL` for `s`:

> 如果你不在乎结果（即只对重置状态或获取返回值感兴趣），可以将`NULL`传递给`s`来实现：

::: {#cb892 .sourceCode}
``` {.sourceCode .c}
wcrtomb(NULL, L'\0', &state);                // Reset state

int byte_count = wctomb(NULL, "X", &state);  // Count bytes in 'X'
```
:::


This function doesn't have the functionality of `wctomb()` that allowed you to query if this character encoding was stateful and to reset the internal state.

> 这个函数没有`wctomb()`的功能，该功能允许查询此字符编码是否是有状态的，以及重置内部状态。

### Return Value {#return-value-262 .unnumbered .unlisted}


On success, returns the number of bytes needed to encode this wide character in the current locale.

> 在成功的情况下，返回在当前语言环境中编码此宽字符所需的字节数。


If the input is an invalid wide character, `errno` will be set to `EILSEQ` and the function returns `(size_t)(-1)`. If this happens, all bets are off for the conversion state, so you might as well reset it.

> 如果输入是无效的宽字符，`errno`将被设置为`EILSEQ`，函数返回`(size_t)(-1)`。如果发生这种情况，转换状态的所有赌注都会失去，因此您最好将其重置。

### Example {#example-266 .unnumbered .unlisted}


If your character set doesn't support the Euro symbol "€", substitute the Unicode escape sequence `\u20ac`, below.

> 如果您的字符集不支持欧元符号“€”，请在下面替换为Unicode转义序列“\u20ac”。

::: {#cb893 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <string.h>  // For memset()
#include <stdlib.h>  // For mbtowc()
#include <locale.h>  // For setlocale()
#include <wchar.h>

int main(void)
{
    mbstate_t state;

    memset(&state, 0, sizeof state);

    setlocale(LC_ALL, "");

    wprintf(L"State dependency: %d\n", mbtowc(NULL, NULL, 0));

    char mb[10] = {0};
    int bytes = wcrtomb(mb, L'€', &state);

    wprintf(L"L'€' takes %d bytes as multibyte char '%s'\n", bytes, mb);
}
```
:::

### See Also {#see-also-251 .unnumbered .unlisted}


[`mbrtowc()`](wchar.html#man-mbrtowc), [`wctomb()`](stdlib.html#man-wctomb), [`errno`](errno.html#errno)

> [`mbrtowc()`](wchar.html#man-mbrtowc)：多字节字符转换为宽字符
[`wctomb()`](stdlib.html#man-wctomb)：宽字符转换为多字节字符
[`errno`](errno.html#errno)：错误号

------------------------------------------------------------------------

## [30.32]{.header-section-number} `mbsrtowcs()` {#man-mbsrtowcs number="30.32"}

Convert a multibyte string to a wide character string restartably

### Synopsis {#synopsis-265 .unnumbered .unlisted}

::: {#cb894 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t mbsrtowcs(wchar_t * restrict dst, const char ** restrict src,
                 size_t len, mbstate_t * restrict ps);
```
:::

### Description {#description-265 .unnumbered .unlisted}


This is the restartable version of [`mbstowcs()`](stdlib.html#man-mbstowcs).

> 这是[`mbstowcs()`](stdlib.html#man-mbstowcs)的可重新启动版本。

It converts a multibyte string to a wide character string.


The result is put in the buffer pointed to by `dst`, and the pointer `src` is updated to indicate how much of the string was consumed (unless `dst` is `NULL`).

> 结果存放在指针`dst`指向的缓冲区中，指针`src`更新以指示字符串中被消耗了多少（除非`dst`为`NULL`）。

At most `len` wide characters will be stored.


This also takes a pointer to its own `mbstate_t` variable in `ps` for holding the conversion state.

> 这也需要一个指针指向它自己的`mbstate_t`变量，用于保存转换状态。


You can set `dst` to `NULL` if you only care about the return value. This could be useful for getting the number of characters in a multibyte string.

> 你可以将`dst`设置为`NULL`，如果你只关心返回值的话。这可能对获取多字节字符串中字符的数量很有用。


In the normal case, the `src` string will be consumed up to the NUL character, and the results will be stored in the `dst` buffer, including the wide NUL character. In this case, the pointer pointed to by `src` will be set to `NULL`. And the conversion state will be set to the initial conversion state.

> 在正常情况下，`src`字符串将被消耗到NUL字符，结果将被存储在`dst`缓冲区中，包括宽NUL字符。在这种情况下，指向`src`的指针将被设置为`NULL`。转换状态将被设置为初始转换状态。


If things go wrong because the source string isn't a valid sequence of characters, conversion will stop and the pointer pointed to by `src` will be set to the address just after the last successfully-translated multibyte character.

> 如果源字符串不是有效的字符序列，事情会出错，转换将停止，`src`指向的指针将被设置为最后一个成功转换的多字节字符的地址之后。

### Return Value {#return-value-263 .unnumbered .unlisted}


If successful, returns the number of characters converted, not including any NUL terminator.

> 如果成功，返回转换的字符数，不包括任何NUL终止符。


If the multibyte sequence is invalid, the function returns `(size_t)(-1)` and `errno` is set to `EILSEQ`.

> 如果多字节序列无效，函数会返回`(size_t)(-1)`，而`errno`被设置为`EILSEQ`。

### Example {#example-267 .unnumbered .unlisted}

Here we'll convert the string "€5 ± π" into a wide character string:

::: {#cb895 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <locale.h>  // For setlocale()
#include <string.h>  // For memset()
#include <wchar.h>

#define WIDE_STR_SIZE 10

int main(void)
{
    const char *mbs = "€5 ± π";  // That's the exact price range

    wchar_t wcs[WIDE_STR_SIZE];

    setlocale(LC_ALL, "");
    
    mbstate_t state;
    memset(&state, 0, sizeof state);

    size_t count = mbsrtowcs(wcs, &mbs, WIDE_STR_SIZE, &state);

    wprintf(L"Wide string L\"%ls\" is %d characters\n", wcs, count);
}
```
:::

Output:

::: {#cb896 .sourceCode}
``` {.sourceCode .default}
Wide string L"€5 ± π" is 6 characters
```
:::


Here's another example of using `mbsrtowcs()` to get the length in characters of a multibyte string even if the string is full of multibyte characters. This is in contrast to `strlen()`, which returns the total number of bytes in the string.

> 这是另一个使用`mbsrtowcs()`来获取多字节字符串的字符长度（即使字符串中充满了多字节字符）的例子。这与`strlen()`返回字符串中字节总数形成对比。

::: {#cb897 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>   // For printf()
#include <locale.h>  // For setlocale()

#include <string.h>  // For memset()
#include <stdint.h>  // For SIZE_MAX
#include <wchar.h>

size_t mbstrlen(const char *mbs)
{
    mbstate_t state;

    memset(&state, 0, sizeof state);

    return mbsrtowcs(NULL, &mbs, SIZE_MAX, &state);
}

int main(void)
{
    setlocale(LC_ALL, "");
    
    char *mbs = "€5 ± π";  // That's the exact price range

    printf("\"%s\" is %zu characters...\n", mbs, mbstrlen(mbs)); 
    printf("but it's %zu bytes!\n", strlen(mbs));
}
```
:::

Output on my system:

::: {#cb898 .sourceCode}
``` {.sourceCode .default}
"€5 ± π" is 6 characters...
but it's 10 bytes!
```
:::

### See Also {#see-also-252 .unnumbered .unlisted}


[`mbrtowc()`](wchar.html#man-mbrtowc), [`mbstowcs()`](stdlib.html#man-mbstowcs), [`wcsrtombs()`](wchar.html#man-wcsrtombs), [`strlen()`](stringref.html#man-strlen), [`errno`](errno.html#errno)

> [mbrtowc()](wchar.html#man-mbrtowc)：将多字节字符转换为宽字符
[mbstowcs()](stdlib.html#man-mbstowcs)：将多字节字符串转换为宽字符串
[wcsrtombs()](wchar.html#man-wcsrtombs)：将宽字符串转换为多字节字符串
[strlen()](stringref.html#man-strlen)：计算字符串长度
[errno](errno.html#errno)：错误号

------------------------------------------------------------------------

## [30.33]{.header-section-number} `wcsrtombs()` {#man-wcsrtombs number="30.33"}

Convert a wide character string to a multibyte string restartably

### Synopsis {#synopsis-266 .unnumbered .unlisted}

::: {#cb899 .sourceCode}
``` {.sourceCode .c}
#include <wchar.h>

size_t wcsrtombs(char * restrict dst, const wchar_t ** restrict src,
                 size_t len, mbstate_t * restrict ps);
```
:::

### Description {#description-266 .unnumbered .unlisted}


If you have a wide character string, you can convert it to a multibyte character string in the current locale using this function.

> 如果您有一个宽字符串，您可以使用此函数将其转换为当前区域设置中的多字节字符串。


At most `len` bytes of data will be stored in the buffer pointed to by `dst`. Conversion will stop just after the NUL terminator is copied, or `len` bytes get copied, or some other error occurs.

> 最多会将`len`字节的数据存储到指向`dst`的缓冲区中。转换将在复制NUL终止符之后立即停止，或者复制`len`字节之后立即停止，或者发生其他错误时立即停止。


If `dst` is a `NULL` pointer, no result is stored. You might do this if you're just interested in the return value (nominally the number of bytes this would use in a multibyte string, not including the NUL terminator).

> 如果`dst`是一个`NULL`指针，则不会存储结果。如果只对返回值感兴趣（通常是多字节字符串中使用的字节数，不包括NUL终止符），可以这样做。


If `dst` is not a `NULL` pointer, the pointer pointed to by `src` will get modified to indicate how much of the data was copied. If it contains `NULL` at the end, it means everything went well. In this case, the state `ps` will be set to the initial conversion state.

> 如果`dst`不是一个`NULL`指针，`src`指向的指针将被修改以指示复制了多少数据。如果它在末尾包含`NULL`，则意味着一切正常。在这种情况下，状态`ps`将被设置为初始转换状态。


If `len` was reached or an error occurred, it'll point one address past `dst+len`.

> 如果`len`已达到或发生错误，它将指向`dst+len`之后的一个地址。

### Return Value {#return-value-264 .unnumbered .unlisted}


If everything goes well, returns the number of bytes needed for the multibyte string, not counting the NUL terminator.

> 如果一切顺利，返回多字节字符串所需的字节数，不计算NUL终止符。


If any character in the string doesn't correspond to a valid multibyte character in the currently locale, it returns `(size_t)(-1)` and `EILSEQ` is stored in `errno`.

> 如果字符串中的任何字符与当前语言环境中的有效多字节字符不匹配，则返回`(size_t)(-1)`，并将`EILSEQ`存储在`errno`中。

### Example {#example-268 .unnumbered .unlisted}


Here we'll convert the wide string "€5 ± π" into a multibyte character string:

> 在这里，我们将宽字符串“€5 ± π”转换为多字节字符串：

::: {#cb900 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <locale.h>  // For setlocale()
#include <string.h>  // For memset()
#include <wchar.h>

#define MB_STR_SIZE 20

int main(void)
{
    const wchar_t *wcs = L"€5 ± π";  // That's the exact price range

    char mbs[MB_STR_SIZE];

    setlocale(LC_ALL, "");
    
    mbstate_t state;
    memset(&state, 0, sizeof state);

    size_t count = wcsrtombs(mbs, &wcs, MB_STR_SIZE, &state);

    wprintf(L"Multibyte string \"%s\" is %d bytes\n", mbs, count);
}
```
:::


Here's another example helper function that `malloc()`s just enough memory to hold the converted string, then returns the result. (Which must later be freed, of course, to prevent leaking memory.)

> 这里是另一个示例辅助函数，它使用`malloc()`分配足够的内存来容纳转换后的字符串，然后返回结果（当然，必须稍后释放，以防止泄漏内存）。

::: {#cb901 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdlib.h>  // For malloc()
#include <locale.h>  // For setlocale()
#include <string.h>  // For memset()
#include <stdint.h>  // For SIZE_MAX
#include <wchar.h>

char *get_mb_string(const wchar_t *wcs)
{
    setlocale(LC_ALL, "");

    mbstate_t state;
    memset(&state, 0, sizeof state);

    // Need a copy of this because wcsrtombs changes it
    const wchar_t *p = wcs;

    // Compute the number of bytes needed to hold the result
    size_t bytes_needed = wcsrtombs(NULL, &p, SIZE_MAX, &state);

    // If we didn't get a good full conversion, forget it
    if (bytes_needed == (size_t)(-1))
        return NULL;

    // Allocate space for result
    char *mbs = malloc(bytes_needed + 1);  // +1 for NUL terminator

    // Set conversion state to initial state
    memset(&state, 0, sizeof state);

    // Convert and store result
    wcsrtombs(mbs, &wcs, bytes_needed + 1, &state);

    // Make sure things went well
    if (wcs != NULL) {
        free(mbs);
        return NULL;
    }

    // Success!
    return mbs;
}

int main(void)
{
    char *mbs = get_mb_string(L"€5 ± π");

    wprintf(L"Multibyte result: \"%s\"\n", mbs);

    free(mbs);
}
```
:::

### See Also {#see-also-253 .unnumbered .unlisted}


[`wcrtomb()`](wchar.html#man-wcrtomb), [`wcstombs()`](stdlib.html#man-wcstombs), [`mbsrtowcs()`](wchar.html#man-mbsrtowcs), [`errno`](errno.html#errno)

> [`wcrtomb()`](wchar.html#man-wcrtomb)：将宽字符转换为多字节字符
[`wcstombs()`](stdlib.html#man-wcstombs)：将宽字符串转换为多字节字符串
[`mbsrtowcs()`](wchar.html#man-mbsrtowcs)：将多字节字符串转换为宽字符串
[`errno`](errno.html#errno)：错误号

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](uchar.html) \| [Contents](index.html) \| [Next](wctype.html)
:::
