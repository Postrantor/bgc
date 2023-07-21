---
tip: translate by openai@2023-07-20 23:03:22
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](ctype.html) \| [Contents](index.html) \| [Next](fenv.html)
:::

------------------------------------------------------------------------

# [6]{.header-section-number} `<errno.h>` Error Information {#errno number="6"}

  Variable                          Description
  --------------------------------- -----------------------------------------

  [`errno`](errno.html#man-errno)   Holds the error status of the last call

> `errno`保存了上一次调用的错误状态


This header defines a single variable[^15^](footnotes.html#fn15){#fnref15 .footnote-ref role="doc-noteref"}, `errno`, that can be checked to see if an error has occurred.

> 这个头文件定义了一个变量errno，可以检查是否发生了错误。

`errno` is set to `0` on startup, but no library function sets it to `0`. If you're going to use solely it to check for errors, set it to `0` before the call and then check it after. Not only that, but if there's no error, all library functions will leave the value of `errno` unchanged.


Often, though, you'll get some error indication from the function you're calling then check `errno` to see what went wrong.

> 通常情况下，您会从调用的函数中得到一些错误指示，然后检查`errno`以查看发生了什么错误。


This is commonly used in conjunction with [`perror()`](stdio.html#man-perror) to get a human-readable error message that corresponds to the specific error.

> 这通常与[`perror()`](stdio.html#man-perror)一起使用，以获得与特定错误相对应的可读性错误消息。


Important Safety Tip: You should never make your own variable called `errno`---that's undefined behavior.

> 重要安全提示：你永远不应该自己创建一个叫做“errno”的变量——那是未定义的行为。


Note that the C Spec defines less than a handful of values `errno` can take on. [Unix defines a bunch more](https://man.archlinux.org/man/errno.3.en)[^16^](footnotes.html#fn16){#fnref16 .footnote-ref role="doc-noteref"}, [as does Windows](https://docs.microsoft.com/en-us/cpp/c-runtime-library/errno-constants?view=msvc-160)[^17^](footnotes.html#fn17){#fnref17 .footnote-ref role="doc-noteref"}.

> 注意，C语言规范定义的`errno`可以接受的值不到一把。[Unix定义了更多](https://man.archlinux.org/man/errno.3.en)[^16^](footnotes.html#fn16){#fnref16 .footnote-ref role="doc-noteref"}，[Windows也是如此](https://docs.microsoft.com/en-us/cpp/c-runtime-library/errno-constants?view=msvc-160)[^17^](footnotes.html#fn17){#fnref17 .footnote-ref role="doc-noteref"}。

------------------------------------------------------------------------

## [6.1]{.header-section-number} `errno` {#man-errno number="6.1"}

Holds the error status of the last call

### Synopsis {#synopsis-39 .unnumbered .unlisted}

::: {#cb180 .sourceCode}
``` {.sourceCode .c}
errno   // Type is undefined, but it's assignable
```
:::

### Description {#description-39 .unnumbered .unlisted}


Indicates the error status of the last call (note that not all calls will set this value).

> 指示最后一次调用的错误状态（注意，并非所有调用都会设置此值）。

  Value      Description
  ---------- --------------------------------------------
  `0`        No error
  `EDOM`     Domain error (from math)
  `EILSEQ`   Encoding error (from character conversion)
  `ERANGE`   Range error (from math)


If you're doing a number of math functions, you might come across `EDOM` or `ERANGE`.

> 如果你正在做一些数学函数，你可能会遇到`EDOM`或`ERANGE`。


With multibyte/wide character conversion functions, you might see `EILSEQ`.

> 使用多字节/宽字符转换功能时，您可能会看到“EILSEQ”。


And your system might define any other number of values that `errno` could be set to, all of which will begin with the letter `E`.

> 系统可能定义任何数量的errno值，所有这些值都将以字母E开头。


Fun Fact: you can use `EDOM`, `EILSEQ`, and `ERANGE` with preprocessor directives such as `#ifdef`. But, frankly, I'm not sure why you'd do that other than to test their existence.

> 趣味事实：您可以使用`EDOM`，`EILSEQ`和`ERANGE`与预处理指令（如`#ifdef`）一起使用。但是，坦率地说，除了测试它们的存在之外，我不确定您为什么要这样做。

### Example {#example-39 .unnumbered .unlisted}


The following prints an error message, since passing `2.0` to `acos()` is outside the function's domain.

> 以下打印出一条错误消息，因为将`2.0`传递给`acos()`超出了函数的域。

::: {#cb181 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <errno.h>

int main(void)
{
    double x;

    errno = 0;       // Make sure this is clear before the call

    x = acos(2.0);   // Invalid argument to acos()

    if (errno == EDOM)
        perror("acos");
    else
        printf("Answer is %f\n", x);

    return 0;
}
```
:::

Output:

::: {#cb182 .sourceCode}
``` {.sourceCode .default}
acos: Numerical argument out of domain
```
:::


The following prints an error message (on my system), since passing `1e+30` to `exp()` produces a result that's outside the range of a `double`.

> 以下会打印一条错误消息（在我的系统上），因为将`1e+30`传递给`exp()`会产生超出`double`范围的结果。

::: {#cb183 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <math.h>
#include <errno.h>

int main(void)
{
    double x;

    errno = 0;       // Make sure this is clear before the call

    x = exp(1e+30);  // Pass in some too-huge number

    if (errno == ERANGE)
        perror("exp");
    else
        printf("Answer is %f\n", x);

    return 0;
}
```
:::

Output:

::: {#cb184 .sourceCode}
``` {.sourceCode .default}
exp: Numerical result out of range
```
:::


This example tries to convert an invalid character into a wide character, failing. This sets `errno` to `EILSEQ`. We then use `perror()` to print an error message.

> 这个例子试图将一个无效字符转换为宽字符，但失败了。这会将`errno`设置为`EILSEQ`。然后我们使用`perror()`来打印错误消息。

::: {#cb185 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>
#include <wchar.h>
#include <errno.h>
#include <locale.h>

int main(void)
{
    setlocale(LC_ALL, "");

    char *bad_str = "\xff";  // Probably invalid char in this locale
    wchar_t wc;
    size_t result;
    mbstate_t ps;

    memset(&ps, 0, sizeof ps);

    result = mbrtowc(&wc, bad_str, 1, &ps);

    if (result == (size_t)(-1))
        perror("mbrtowc");  // mbrtowc: Illegal byte sequence
    else
        printf("Converted to L'%lc'\n", wc);

    return 0;
}
```
:::

Output:

::: {#cb186 .sourceCode}
``` {.sourceCode .default}
mbrtowc: Invalid or incomplete multibyte or wide character
```
:::

### See Also {#see-also-36 .unnumbered .unlisted}


[`perror()`](stdio.html#man-perror), [`mbrtoc16()`](uchar.html#man-mbrtoc16), [`c16rtomb()`](uchar.html#man-c16rtomb), [`mbrtoc32()`](uchar.html#man-mbrtoc16), [`c32rtomb()`](uchar.html#man-c16rtomb), [`fgetwc()`](wchar.html#man-getwc), [`fputwc()`](wchar.html#man-putwc), [`mbrtowc()`](wchar.html#man-mbrtowc), [`wcrtomb()`](wchar.html#man-wcrtomb), [`mbsrtowcs()`](wchar.html#man-mbsrtowcs), [`wcsrtombs()`](wchar.html#man-wcsrtombs), [`<math.h>`](math.html#math),

> [perror()](stdio.html#man-perror)：显示最近一次系统调用的错误信息
[mbrtoc16()](uchar.html#man-mbrtoc16)：将多字节字符转换为UTF-16编码
[c16rtomb()](uchar.html#man-c16rtomb)：将UTF-16编码转换为多字节字符
[mbrtoc32()](uchar.html#man-mbrtoc16)：将多字节字符转换为UTF-32编码
[c32rtomb()](uchar.html#man-c16rtomb)：将UTF-32编码转换为多字节字符
[fgetwc()](wchar.html#man-getwc)：从文件中读取宽字符
[fputwc()](wchar.html#man-putwc)：将宽字符写入文件
[mbrtowc()](wchar.html#man-mbrtowc)：将多字节字符转换为宽字符
[wcrtomb()](wchar.html#man-wcrtomb)：将宽字符转换为多字节字符
[mbsrtowcs()](wchar.html#man-mbsrtowcs)：将多字节字符串转换为宽字符串
[wcsrtombs()](wchar.html#man-wcsrtombs)：将宽字符串转换为多字节字符串
[<math.h>](math.html#math)：数学函数头文件

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](ctype.html) \| [Contents](index.html) \| [Next](fenv.html)
:::
