---
tip: translate by openai@2023-07-21 12:48:20
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdnoreturn.html) \| [Contents](index.html) \| [Next](tgmath.html)
:::

------------------------------------------------------------------------

# [25]{.header-section-number} `<string.h>` String Manipulation {#stringref number="25"}


  --------------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。
  Function                                      Description

  --------------------------------------------- ----------------------------------------------------------------

> --------------------------------------------- ----------------------------------------------------------------
简体中文：
--------------------------------------------- ----------------------------------------------------------------

  [`memchr()`](stringref.html#man-strchr)       Find the first occurrence of a character in memory.

> 找到内存中第一次出现的字符。


  [`memcmp()`](stringref.html#man-strcmp)       Compare two regions of memory.

> `memcmp()`比较两个内存区域。


  [`memcpy()`](stringref.html#man-memcpy)       Copy a region of memory to another.

> `memcpy()`将一块内存区域复制到另一块内存区域。


  [`memmove()`](stringref.html#man-memcpy)      Move a (potentially overlapping) region of memory.

> memmove()（参见stringref.html#man-memcpy）移动一块（可能重叠的）内存区域。


  [`memset()`](stringref.html#man-memset)       Set a region of memory to a value.

> 设置内存区域的值。


  [`strcat()`](stringref.html#man-strcat)       Concatenate (join) two strings together.

> `strcat()`：将两个字符串连接在一起。


  [`strchr()`](stringref.html#man-strchr)       Find the first occurrence of a character in a string.

> `strchr()` 找到字符串中第一次出现的字符。

  [`strcmp()`](stringref.html#man-strcmp)       Compare two strings.


  [`strcoll()`](stringref.html#man-strcoll)     Compare two strings accounting for locale.

> [`strcoll()`](stringref.html#man-strcoll) 根据语言环境比较两个字符串。

  [`strcpy()`](stringref.html#man-strcpy)       Copy a string.


  [`strcspn()`](stringref.html#man-strspn)      Find length of a string not consisting of a set of characters.

> 找到不包含一组字符的字符串的长度。


  [`strerror()`](stringref.html#man-strerror)   Return a human-readable error message for a given code.

> `strerror()`返回给定代码的可读错误消息。


  [`strlen()`](stringref.html#man-strlen)       Return the length of a string.

> `strlen()` 返回字符串的长度。


  [`strncat()`](stringref.html#man-strcat)      Concatenate (join) two strings, length-limited.

> `strncat()`：有长度限制的连接两个字符串。


  [`strncmp()`](stringref.html#man-strcmp)      Compare two strings, length-limited.

> [`strncmp()`](stringref.html#man-strcmp)比较两个字符串，长度有限。


  [`strncpy()`](stringref.html#man-strcpy)      Copy two strings, length-limited.

> `strncpy()`：有长度限制的复制两个字符串。


  [`strpbrk()`](stringref.html#man-strpbrk)     Search a string for one of a set of character.

> `strpbrk()`（stringref.html#man-strpbrk）搜索一个字符串中是否包含一组字符中的任意一个。


  [`strrchr()`](stringref.html#man-strchr)      Find the last occurrence of a character in a string.

> 找到字符串中最后一次出现的字符。


  [`strspn()`](stringref.html#man-strspn)       Find length of a string consisting of a set of characters.

> `strspn()`函数可以查找由一组字符组成的字符串的长度。


  [`strstr()`](stringref.html#man-strstr)       Find a substring in a string.

> `strstr()`（[stringref.html#man-strstr](stringref.html#man-strstr)）：在字符串中查找子串。

  [`strtok()`](stringref.html#man-strtok)       Tokenize a string.


  [`strxfrm()`](stringref.html#man-strxfrm)     Prepare a string for comparison as if by `strcoll()`.

> strxfrm()（stringref.html#man-strxfrm）准备一个字符串，就像使用strcoll()一样进行比较。

  --------------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------------
无论如何，我们都要努力。


As has been mentioned earlier in the guide, a string in C is a sequence of bytes in memory, terminated by a NUL character ('`\0`'). The NUL at the end is important, since it lets all these string functions (and `printf()` and `puts()` and everything else that deals with a string) know where the end of the string actually is.

> 正如本指南之前提到的，C中的字符串是一个由NUL字符（'\0'）结尾的字节序列。NUL字符在末尾非常重要，因为它让所有这些字符串函数（以及printf（）、puts（）和其他处理字符串的函数）知道字符串的结束位置。


Fortunately, when you operate on a string using one of these many functions available to you, they add the NUL terminator on for you, so you actually rarely have to keep track of it yourself. (Sometimes you do, especially if you're building a string from scratch a character at a time or something.)

> 幸运的是，当你使用其中一个可用的函数操作字符串时，它们会为你添加NUL终止符，所以你实际上很少需要自己跟踪它。 （有时你需要，特别是如果你一次一个字符地从头开始构建字符串的话。）


In this section you'll find functions for pulling substrings out of strings, concatenating strings together, getting the length of a string, and so forth and so on.

> 在这一部分，你会发现一些函数，可以从字符串中提取子字符串，拼接字符串，获取字符串的长度，等等。

------------------------------------------------------------------------

## [25.1]{.header-section-number} `memcpy()`, `memmove()` {#man-memcpy number="25.1"}

Copy bytes of memory from one location to another

### Synopsis {#synopsis-184 .unnumbered .unlisted}

::: {#cb646 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

void *memcpy(void * restrict s1, const void * restrict s2, size_t n);

void *memmove(void *s1, const void *s2, size_t n);
```
:::

### Description {#description-184 .unnumbered .unlisted}


These functions copy memory---as many bytes as you want! From source to destination!

> 这些函数可以复制内存---您想要多少字节都可以！从源头到目的地！


The main difference between the two is that `memcpy()` cannot safely copy overlapping memory regions, whereas `memmove()` can.

> 两者之间的主要区别是`memcpy()`不能安全地复制重叠的内存区域，而`memmove()`可以。


On the one hand, I'm not sure why you'd want to ever use `memcpy()` instead of `memmove()`, but I'll bet it's possibly more performant.

> 一方面，我不确定你为什么要使用memcpy()而不是memmove()，但我敢打赌它可能更有效率。


The parameters are in a particular order: destination first, then source. I remember this order because it behaves like an "`=`" assignment: the destination is on the left.

> 参数按特定顺序排列：先是目的地，然后是源。我记住了这个顺序，因为它的行为就像一个“=”赋值：目的地在左边。

### Return Value {#return-value-182 .unnumbered .unlisted}


Both functions return whatever you passed in for parameter `s1` for your convenience.

> 两个函数都会为了方便您而将您传入的`s1`参数原样返回。

### Example {#example-185 .unnumbered .unlisted}

::: {#cb647 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <string.h>

int main(void)
{
    char s[100] = "Goats";
    char t[100];

    memcpy(t, s, 6);       // Copy non-overlapping memory

    memmove(s + 2, s, 6);  // Copy overlapping memory
}
```
:::

### See Also {#see-also-174 .unnumbered .unlisted}


[`strcpy()`](stringref.html#man-strcpy), [`strncpy()`](stringref.html#man-strcpy)

> `strcpy()`，`strncpy()`

------------------------------------------------------------------------

## [25.2]{.header-section-number} `strcpy()`, `strncpy()` {#man-strcpy number="25.2"}

Copy a string

### Synopsis {#synopsis-185 .unnumbered .unlisted}

::: {#cb648 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

char *strcpy(char *dest, char *src);

char *strncpy(char *dest, char *src, size_t n);
```
:::

### Description {#description-185 .unnumbered .unlisted}


These functions copy a string from one address to another, stopping at the NUL terminator on the `src`string.

> 这些函数会从一个地址复制一个字符串到另一个地址，在`src`字符串的空字符终止符处停止。

`strncpy()` is just like `strcpy()`, except only the first `n` characters are actually copied. Beware that if you hit the limit, `n` before you get a NUL terminator on the `src` string, your `dest` string won't be NUL-terminated. Beware! BEWARE!


(If the `src` string has fewer than `n` characters, it works just like `strcpy()`.)

> 如果'src'字符串的长度小于n，它的工作方式就和strcpy()一样。


You can terminate the string yourself by sticking the `'\0'` in there yourself:

> 你可以自己在里面放置'\0'来终止字符串。

::: {#cb649 .sourceCode}
``` {.sourceCode .c}
char s[10];
char foo = "My hovercraft is full of eels."; // more than 10 chars

strncpy(s, foo, 9); // only copy 9 chars into positions 0-8
s[9] = '\0';        // position 9 gets the terminator
```
:::

### Return Value {#return-value-183 .unnumbered .unlisted}

Both functions return `dest` for your convenience, at no extra charge.

### Example {#example-186 .unnumbered .unlisted}

::: {#cb650 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <string.h>

int main(void)
{
    char *src = "hockey hockey hockey hockey hockey hockey hockey hockey";
    char dest[20];

    int len;

    strcpy(dest, "I like "); // dest is now "I like "

    len = strlen(dest);

    // tricky, but let's use some pointer arithmetic and math to append
    // as much of src as possible onto the end of dest, -1 on the length to
    // leave room for the terminator:
    strncpy(dest+len, src, sizeof(dest)-len-1);

    // remember that sizeof() returns the size of the array in bytes
    // and a char is a byte:
    dest[sizeof(dest)-1] = '\0'; // terminate

    // dest is now:       v null terminator
    // I like hockey hocke 
    // 01234567890123456789012345
}
```
:::

### See Also {#see-also-175 .unnumbered .unlisted}


[`memcpy()`](stringref.html#man-memcpy), [`strcat()`](stringref.html#man-strcat), [`strncat()`](stringref.html#man-strcat)

> [`memcpy()`](stringref.html#man-memcpy)：复制内存块
[`strcat()`](stringref.html#man-strcat)：连接字符串
[`strncat()`](stringref.html#man-strcat)：连接指定长度的字符串

------------------------------------------------------------------------

## [25.3]{.header-section-number} `strcat()`, `strncat()` {#man-strcat number="25.3"}

Concatenate two strings into a single string

### Synopsis {#synopsis-186 .unnumbered .unlisted}

::: {#cb651 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

int strcat(const char *dest, const char *src);

int strncat(const char *dest, const char *src, size_t n);
```
:::

### Description {#description-186 .unnumbered .unlisted}


"Concatenate", for those not in the know, means to "stick together". These functions take two strings, and stick them together, storing the result in the first string.

> "Concatenate"，对于那些不了解的人来说，意味着"拼接"。这些函数接受两个字符串，并将它们拼接在一起，将结果存储在第一个字符串中。


These functions don't take the size of the first string into account when it does the concatenation. What this means in practical terms is that you can try to stick a 2 megabyte string into a 10 byte space. This will lead to unintended consequences, unless you intended to lead to unintended consequences, in which case it will lead to intended unintended consequences.

> 这些函数在进行连接时不考虑第一个字符串的大小。这在实际中意味着你可以尝试将2MB的字符串放入10字节的空间中。除非你有意导致意外后果，否则这将导致意外的后果，在这种情况下，它将导致有意的意外后果。

Technical banter aside, your boss and/or professor will be irate.


If you want to make sure you don't overrun the first string, be sure to check the lengths of the strings first and use some highly technical subtraction to make sure things fit.

> 如果你想确保不超过第一个字符串，请先检查字符串的长度，并使用一些高级技术的减法来确保每件事都能放得下。


You can actually only concatenate the first `n` characters of the second string by using `strncat()` and specifying the maximum number of characters to copy.

> 你可以通过使用`strncat()`并指定要复制的最大字符数，只连接第二个字符串的前`n`个字符。

### Return Value {#return-value-184 .unnumbered .unlisted}


Both functions return a pointer to the destination string, like most of the string-oriented functions.

> 两个函数都会返回一个指向目标字符串的指针，就像大多数字符串相关函数一样。

### Example {#example-187 .unnumbered .unlisted}

::: {#cb652 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    char dest[30] = "Hello";
    char *src = ", World!";
    char numbers[] = "12345678";

    printf("dest before strcat: \"%s\"\n", dest); // "Hello"

    strcat(dest, src);
    printf("dest after strcat:  \"%s\"\n", dest); // "Hello, world!"

    strncat(dest, numbers, 3); // strcat first 3 chars of numbers
    printf("dest after strncat: \"%s\"\n", dest); // "Hello, world!123"
}
```
:::


Notice I mixed and matched pointer and array notation there with `src` and `numbers`; this is just fine with string functions.

> 注意我在`src`和`numbers`之间混合使用了指针和数组表示法；这对字符串函数来说是完全正常的。

### See Also {#see-also-176 .unnumbered .unlisted}

[`strlen()`](stringref.html#man-strlen)

------------------------------------------------------------------------

## [25.4]{.header-section-number} `strcmp()`, `strncmp()`, `memcmp()` {#man-strcmp number="25.4"}

Compare two strings or memory regions and return a difference

### Synopsis {#synopsis-187 .unnumbered .unlisted}

::: {#cb653 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

int strcmp(const char *s1, const char *s2);

int strncmp(const char *s1, const char *s2, size_t n);

int memcmp(const void *s1, const void *s2, size_t n);
```
:::

### Description {#description-187 .unnumbered .unlisted}

All these functions compare chunks of bytes in memory.

`strcmp()` and `strncmp()` operate on NUL-terminated strings, whereas `memcmp()` will compare the number of bytes you specify, brazenly ignoring any NUL characters it finds along the way.

`strcmp()` compares the entire string down to the end, while `strncmp()` only compares the first `n` characters of the strings.


It's a little funky what they return. Basically it's a difference of the strings, so if the strings are the same, it'll return zero (since the difference is zero). It'll return non-zero if the strings differ; basically it will find the first mismatched character and return less-than zero if that character in `s1` is less than the corresponding character in `s2`. It'll return greater-than zero if that character in `s1` is greater than that in `s2`.

> 它们返回的有点古怪。基本上它是字符串之间的差异，所以如果字符串相同，它会返回零（因为差异为零）。如果字符串不同，它会返回非零值；基本上它会找到第一个不匹配的字符，如果`s1`中的字符小于`s2`中的对应字符，则返回小于零的值。如果`s1`中的字符大于`s2`中的字符，则返回大于零的值。


So if they return `0`, the comparison was equal (i.e. the difference was `0`.)

> 如果它们返回“0”，则比较相等（即差异为“0”）。


These functions can be used as comparison functions for [`qsort()`](stdlib.html#man-qsort) if you have an array of `char*`s you want to sort.

> 这些函数可以用作[`qsort()`](stdlib.html#man-qsort)的比较函数，如果你有一个`char*`数组要排序。

### Return Value {#return-value-185 .unnumbered .unlisted}


Returns zero if the strings or memory are the same, less-than zero if the first different character in `s1` is less than that in `s2`, or greater-than zero if the first difference character in `s1` is greater than than in `s2`.

> 如果字符串或内存相同，则返回零；如果s1中的第一个不同字符小于s2中的第一个不同字符，则返回小于零的值；如果s1中的第一个不同字符大于s2中的第一个不同字符，则返回大于零的值。

### Example {#example-188 .unnumbered .unlisted}

::: {#cb654 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *s1 = "Muffin";
    char *s2 = "Muffin Sandwich";
    char *s3 = "Muffin";

    int r1 = strcmp("Biscuits", "Kittens");
    printf("%d\n", r1); // prints < 0 since 'B' < 'K'

    int r2 = strcmp("Kittens", "Biscuits");
    printf("%d\n", r2); // prints > 0 since 'K' > 'B'

    if (strcmp(s1, s2) == 0)
        printf("This won't get printed because the strings differ\n");

    if (strcmp(s1, s3) == 0)
        printf("This will print because s1 and s3 are the same\n");

    // this is a little weird...but if the strings are the same, it'll
    // return zero, which can also be thought of as "false". Not-false
    // is "true", so (!strcmp()) will be true if the strings are the
    // same. yes, it's odd, but you see this all the time in the wild
    // so you might as well get used to it:

    if (!strcmp(s1, s3))
        printf("The strings are the same!\n");

    if (!strncmp(s1, s2, 6))
        printf("The first 6 characters of s1 and s2 are the same\n");
}
```
:::

### See Also {#see-also-177 .unnumbered .unlisted}


[`memcmp()`](stringref.html#man-strcmp), [`qsort()`](stdlib.html#man-qsort)

> `memcmp()`：比较内存块；`qsort()`：快速排序。

------------------------------------------------------------------------

## [25.5]{.header-section-number} `strcoll()` {#man-strcoll number="25.5"}

Compare two strings accounting for locale

### Synopsis {#synopsis-188 .unnumbered .unlisted}

::: {#cb655 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

int strcoll(const char *s1, const char *s2);
```
:::

### Description {#description-188 .unnumbered .unlisted}


This is basically `strcmp()`, except that it handles accented characters better depending on the locale.

> 这基本上就是`strcmp()`，只是它根据区域设置更好地处理带有重音符号的字符。


For example, my `strcmp()` reports that the character "é" (with accent) is greater than "f". But that's hardly useful for alphabetizing.

> 例如，我的`strcmp()`报告说带有重音的字符"é"比"f"大。但这对于字母排序来说几乎没有用处。


By setting the `LC_COLLATE` locale value (either by name or via `LC_ALL`), you can have `strcoll()` sort in a way that's more meaningful by the current locale. For example, by having "é" appear sanely *before* "f".

> 通过设置`LC_COLLATE`区域设置值（通过名称或`LC_ALL`），您可以通过当前区域设置让`strcoll()`排序更有意义。例如，让“é”出现在“f”之前。


It's also a lot slower than `strcmp()` so use it only if you have to. See [`strxfrm()`](stringref.html#man-strxfrm) for a potential speedup.

> 它比`strcmp()`慢得多，所以只有在必须的情况下才使用它。可以参考[`strxfrm()`](stringref.html#man-strxfrm)来提高速度。

### Return Value {#return-value-186 .unnumbered .unlisted}


Like the other string comparison functions, `strcoll()` returns a negative value if `s1` is less than `s2`, or a positive value if `s1` is greater than `s2`. Or `0` if they are equal.

> 像其他字符串比较函数一样，如果s1小于s2，`strcoll()`会返回一个负值，如果s1大于s2，则会返回一个正值。如果它们相等，则返回0。

### Example {#example-189 .unnumbered .unlisted}

::: {#cb656 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>
#include <locale.h>

int main(void)
{
    setlocale(LC_ALL, "");

    // If your source character set doesn't support "é" in a string
    // you can replace it with `\u00e9`, the Unicode code point
    // for "é".

    printf("%d\n", strcmp("é", "f"));   // Reports é > f, yuck.
    printf("%d\n", strcoll("é", "f"));  // Reports é < f, yay!
}
```
:::

### See Also {#see-also-178 .unnumbered .unlisted}

[`strcmp()`](stringref.html#man-strcmp)

------------------------------------------------------------------------

## [25.6]{.header-section-number} `strxfrm()` {#man-strxfrm number="25.6"}

Transform a string for comparing based on locale

### Synopsis {#synopsis-189 .unnumbered .unlisted}

::: {#cb657 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

size_t strxfrm(char * restrict s1, const char * restrict s2, size_t n);
```
:::

### Description {#description-189 .unnumbered .unlisted}

This is a strange little function, so bear with me.


Firstly, if you haven't done so, get familiar with [`strcoll()`](stringref.html#man-strcoll) because this is closely related to that.

> 首先，如果你还没有这样做，请熟悉[`strcoll()`](stringref.html#man-strcoll)，因为它与此密切相关。


OK! Now that you're back, you can think of `strxfrm()` as the first part of the `strcoll()` internals. Basically, `strcoll()` has to transform a string into a form that can be compared with `strcmp()`. And it does this with `strxfrm()` for both strings every time you call it.

> 好的！现在你回来了，你可以把strxfrm()看作strcoll()内部的第一部分。基本上，strcoll()必须将字符串转换为可以与strcmp()比较的形式。每次调用它时，它都会使用strxfrm()来对两个字符串进行转换。

`strxform()` takes string `s2` and transforms it (readies it for `strcmp()`) storing the result in `s1`. It writes no more than `n` bytes, protecting us from terrible buffer overflows.


But hang on---there's another mode! If you pass `NULL` for `s1` and `0` for `n`, it will return the number of bytes that the transformed string *would have* used[^64^](footnotes.html#fn64){#fnref64 .footnote-ref role="doc-noteref"}. This is useful if you need to allocate some space to hold the transformed string before you `strcmp()` it against another.

> 但是等等---还有另一种模式！如果您将`NULL`传递给`s1`和`0`传递给`n`，它将返回转换后的字符串*将使用*的字节数[^64^]（脚注。HTML＃fn64）{＃fnref64 .footnote-ref role =“doc-noteref”}。如果您需要分配一些空间来保存转换后的字符串，然后再`strcmp()`它与另一个，这是有用的。


What I'm getting at, not to be too blunt, is that `strcoll()` is slow compared to `strcmp()`. It does a lot of extra work running `strxfrm()` on all its strings.

> 我想说的是，与`strcmp()`相比，`strcoll()`速度慢。它还要运行`strxfrm()`来处理所有字符串，这是一项额外的工作。

In fact, we can see how it works by writing our own like this:

::: {#cb658 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
int my_strcoll(char *s1, char *s2)
{
    // Use n = 0 to just get the lengths of the transformed strings
    int len1 = strxfrm(NULL, s1, 0) + 1;
    int len2 = strxfrm(NULL, s2, 0) + 1;

    // Allocate enough room for each
    char *d1 = malloc(len1);
    char *d2 = malloc(len2);

    // Transform the strings for comparison
    strxfrm(d1, s1, len1);
    strxfrm(d2, s2, len2);

    // Compare the transformed strings
    int result = strcmp(d1, d2);

    // Free up the transformed strings
    free(d2);
    free(d1);

    return result;
}
```
:::


You see on lines 12, 13, and 16, above how we transform the two input strings and then call `strcmp()` on the result.

> 你可以在上面的12、13和16行看到，我们如何转换两个输入字符串，然后在结果上调用`strcmp()`。


So why do we have this function? Can't we just call `strcoll()` and be done with it?

> 为什么我们要有这个函数？我们不能只调用`strcoll()`就完事了吗？


The idea is that if you have one string that you're going to be comparing against a whole lot of other ones, maybe you just want to transform that string one time, then use the faster `strcmp()` saving yourself a bunch of the work we had to do in the function, above.

> 这个想法是，如果你有一个字符串要与很多其他字符串进行比较，也许你只想对该字符串进行一次转换，然后使用更快的`strcmp()`，从而节省我们在上面函数中所做的大量工作。

We'll do that in the example.

### Return Value {#return-value-187 .unnumbered .unlisted}


Returns the number of bytes in the transformed sequence. If the value is greater than `n`, the results in `s1` are meaningless.

> 返回转换序列中的字节数。如果值大于`n`，`s1`中的结果将毫无意义。

### Example {#example-190 .unnumbered .unlisted}

::: {#cb659 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>
#include <locale.h>
#include <stdlib.h>

// Transform a string for comparison, returning a malloc'd
// result
char *get_xfrm_str(char *s)
{
    int len = strxfrm(NULL, s, 0) + 1;
    char *d = malloc(len);

    strxfrm(d, s, len);

    return d;
}

// Does half the work of a regular strcoll() because the second
// string arrives already transformed.
int half_strcoll(char *s1, char *s2_transformed)
{
    char *s1_transformed = get_xfrm_str(s1);

    int result = strcmp(s1_transformed, s2_transformed);

    free(s1_transformed);

    return result;
}

int main(void)
{
    setlocale(LC_ALL, "");

    // Pre-transform the string to compare against
    char *s = get_xfrm_str("éfg");

    // Repeatedly compare against "éfg" 
    printf("%d\n", half_strcoll("fgh", s));  // "fgh" > "éfg"
    printf("%d\n", half_strcoll("àbc", s));  // "àbc" < "éfg"
    printf("%d\n", half_strcoll("ĥij", s));  // "ĥij" > "éfg"
    
    free(s);
}
```
:::

### See Also {#see-also-179 .unnumbered .unlisted}

[`strcoll()`](stringref.html#man-strcoll)

------------------------------------------------------------------------

## [25.7]{.header-section-number} `strchr()`, `strrchr()`, `memchr()` {#man-strchr number="25.7"}

Find a character in a string

### Synopsis {#synopsis-190 .unnumbered .unlisted}

::: {#cb660 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

char *strchr(char *str, int c);

char *strrchr(char *str, int c);

void *memchr(const void *s, int c, size_t n);
```
:::

### Description {#description-190 .unnumbered .unlisted}


The functions `strchr()` and `strrchr` find the first or last occurrence of a letter in a string, respectively. (The extra "r" in `strrchr()` stands for "reverse"--it looks starting at the end of the string and working backward.) Each function returns a pointer to the char in question, or `NULL` if the letter isn't found in the string.

> `strchr()`和`strrchr()`函数分别用于在字符串中查找第一次或最后一次出现的字母。（`strrchr()`中多余的“r”代表“反向”——它从字符串的末尾开始向前搜索。）每个函数都会返回指向该字符的指针，如果字符不存在于字符串中，则返回`NULL`。

`memchr()` is similar, except that instead of stopping on the first NUL character, it continues searching for however many bytes you specify.

Quite straightforward.


One thing you can do if you want to find the next occurrence of the letter after finding the first, is call the function again with the previous return value plus one. (Remember pointer arithmetic?) Or minus one if you're looking in reverse. Don't accidentally go off the end of the string!

> 如果你想要在找到第一个字母后找到下一个出现的字母，你可以做的一件事是用前一个返回值加一再调用这个函数（记得指针算术吗？）或者减一如果你在反向查找。不要不小心超出字符串的结尾！

### Return Value {#return-value-188 .unnumbered .unlisted}


Returns a pointer to the occurrence of the letter in the string, or `NULL` if the letter is not found.

> 返回一个指向字符串中字母出现的位置的指针，如果没有找到字母则返回`NULL`。

### Example {#example-191 .unnumbered .unlisted}

::: {#cb661 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    // "Hello, world!"
    //       ^  ^   ^
    //       A  B   C

    char *str = "Hello, world!";
    char *p;

    p = strchr(str, ',');       // p now points at position A
    p = strrchr(str, 'o');      // p now points at position B

    p = memchr(str, '!', 13);   // p now points at position C

    // repeatedly find all occurrences of the letter 'B'
    str = "A BIG BROWN BAT BIT BEEJ";

    for(p = strchr(str, 'B'); p != NULL; p = strchr(p + 1, 'B')) {
        printf("Found a 'B' here: %s\n", p);
    }
}
```
:::

Output:

::: {#cb662 .sourceCode}
``` {.sourceCode .default}
Found a 'B' here: BIG BROWN BAT BIT BEEJ
Found a 'B' here: BROWN BAT BIT BEEJ
Found a 'B' here: BAT BIT BEEJ
Found a 'B' here: BIT BEEJ
Found a 'B' here: BEEJ
```
:::

------------------------------------------------------------------------

## [25.8]{.header-section-number} `strspn()`, `strcspn()` {#man-strspn number="25.8"}


Return the length of a string consisting entirely of a set of characters, or of not a set of characters

> 返回由一组字符或非一组字符组成的字符串的长度

### Synopsis {#synopsis-191 .unnumbered .unlisted}

::: {#cb663 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

size_t strspn(char *str, const char *accept);

size_t strcspn(char *str, const char *reject);
```
:::

### Description {#description-191 .unnumbered .unlisted}

`strspn()` will tell you the length of a string consisting entirely of the set of characters in `accept`. That is, it starts walking down `str` until it finds a character that is *not* in the set (that is, a character that is not to be accepted), and returns the length of the string so far.

`strcspn()` works much the same way, except that it walks down `str` until it finds a character in the `reject` set (that is, a character that is to be rejected.) It then returns the length of the string so far.

### Return Value {#return-value-189 .unnumbered .unlisted}


The length of the string consisting of all characters in `accept` (for `strspn()`), or the length of the string consisting of all characters except `reject` (for `strcspn()`).

> 字符串`accept`中所有字符的长度（用于`strspn()`），或者字符串中除`reject`以外的所有字符的长度（用于`strcspn()`）。

### Example {#example-192 .unnumbered .unlisted}

::: {#cb664 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    char str1[] = "a banana";
    char str2[] = "the bolivian navy on maenuvers in the south pacific";
    int n;

    // how many letters in str1 until we reach something that's not a vowel?
    n = strspn(str1, "aeiou");
    printf("%d\n", n);  // n == 1, just "a"

    // how many letters in str1 until we reach something that's not a, b,
    // or space?
    n = strspn(str1, "ab ");
    printf("%d\n", n);  // n == 4, "a ba"

    // how many letters in str2 before we get a "y"?
    n = strcspn(str2, "y");
    printf("%d\n", n);  // n = 16, "the bolivian nav"
}
```
:::

### See Also {#see-also-180 .unnumbered .unlisted}


[`strchr()`](stringref.html#man-strchr), [`strrchr()`](stringref.html#man-strchr)

> `strchr()`，`strrchr()`

------------------------------------------------------------------------

## [25.9]{.header-section-number} `strpbrk()` {#man-strpbrk number="25.9"}

Search a string for one of a set of characters

### Synopsis {#synopsis-192 .unnumbered .unlisted}

::: {#cb665 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

char *strpbrk(const char *s1, const char *s2);
```
:::

### Description {#description-192 .unnumbered .unlisted}


This function searches string `s1` for any of the characters that are found in string `s2`.

> 这个函数搜索字符串s1，看看它是否包含字符串s2中的任何字符。


It's just like how `strchr()` searches for a specific character in a string, except it will match *any* of the characters found in `s2`.

> 它就像`strchr()`在字符串中搜索特定字符一样，只是它会匹配`s2`中发现的任何字符。

Think of the power!

### Return Value {#return-value-190 .unnumbered .unlisted}


Returns a pointer to the first character matched in `s1`, or NULL if the string isn't found.

> 返回一个指向s1中第一个匹配字符的指针，如果字符串未找到，则返回NULL。

### Example {#example-193 .unnumbered .unlisted}

::: {#cb666 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    //  p points here after strpbrk
    //              v
    char *s1 = "Hello, world!";
    char *s2 = "dow!";  // Match any of these chars

    char *p = strpbrk(s1, s2);  // p points to the o

    printf("%s\n", p);  // "o, world!"
}
```
:::

### See Also {#see-also-181 .unnumbered .unlisted}


[`strchr()`](stringref.html#man-strchr), [`memchr()`](stringref.html#man-strchr)

> `strchr()`，`memchr()`

------------------------------------------------------------------------

## [25.10]{.header-section-number} `strstr()` {#man-strstr number="25.10"}

Find a string in another string

### Synopsis {#synopsis-193 .unnumbered .unlisted}

::: {#cb667 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

char *strstr(const char *str, const char *substr);
```
:::

### Description {#description-193 .unnumbered .unlisted}


Let's say you have a big long string, and you want to find a word, or whatever substring strikes your fancy, inside the first string. Then `strstr()` is for you! It'll return a pointer to the `substr` within the `str`!

> 如果你有一个很长的字符串，想要在其中找到一个单词或任何你喜欢的子字符串，那么`strstr()`就是你需要的！它将返回一个指向`str`中的`substr`的指针！

### Return Value {#return-value-191 .unnumbered .unlisted}


You get back a pointer to the occurrence of the `substr` inside the `str`, or `NULL` if the substring can't be found.

> 你会得到一个指向`str`中`substr`出现位置的指针，如果找不到子字符串，则返回`NULL`。

### Example {#example-194 .unnumbered .unlisted}

::: {#cb668 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *str = "The quick brown fox jumped over the lazy dogs.";
    char *p;

    p = strstr(str, "lazy");
    printf("%s\n", p == NULL? "null": p); // "lazy dogs."

    // p is NULL after this, since the string "wombat" isn't in str:
    p = strstr(str, "wombat");
    printf("%s\n", p == NULL? "null": p); // "null"
}
```
:::

### See Also {#see-also-182 .unnumbered .unlisted}


[`strchr()`](stringref.html#man-strchr), [`strrchr()`](stringref.html#man-strchr), [`strspn()`](stringref.html#man-strspn), [`strcspn()`](stringref.html#man-strspn)

> [`strchr()`](stringref.html#man-strchr)：在字符串中查找指定字符的位置
[`strrchr()`](stringref.html#man-strchr)：在字符串中查找指定字符的最后一次出现的位置
[`strspn()`](stringref.html#man-strspn)：计算字符串中连续字符的个数
[`strcspn()`](stringref.html#man-strspn)：计算字符串中不包含指定字符的连续字符的个数

------------------------------------------------------------------------

## [25.11]{.header-section-number} `strtok()` {#man-strtok number="25.11"}

Tokenize a string

### Synopsis {#synopsis-194 .unnumbered .unlisted}

::: {#cb669 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

char *strtok(char *str, const char *delim);
```
:::

### Description {#description-194 .unnumbered .unlisted}


If you have a string that has a bunch of separators in it, and you want to break that string up into individual pieces, this function can do it for you.

> 如果你有一个字符串，里面有很多分隔符，你想把它拆分成单独的部分，这个函数可以帮你实现。


The usage is a little bit weird, but at least whenever you see the function in the wild, it's consistently weird.

> 使用方法有点奇怪，但是每次你在野外看到这个函数时，它总是很奇怪的。


Basically, the first time you call it, you pass the string, `str` that you want to break up in as the first argument. For each subsequent call to get more tokens out of the string, you pass `NULL`. This is a little weird, but `strtok()` remembers the string you originally passed in, and continues to strip tokens off for you.

> 基本上，第一次调用它时，您将要分解的字符串`str`作为第一个参数传递。 对于获取更多令牌的每个后续调用，您将传递`NULL`。 这有点奇怪，但`strtok（）`记住您最初传入的字符串，并继续为您剥离令牌。


Note that it does this by actually putting a NUL terminator after the token, and then returning a pointer to the start of the token. So the original string you pass in is destroyed, as it were. If you need to preserve the string, be sure to pass a copy of it to `strtok()` so the original isn't destroyed.

> 注意，它是通过在令牌之后实际放置一个NUL终止符来实现的，然后返回一个指向令牌开头的指针。因此，您传入的原始字符串被破坏了。如果您需要保留字符串，请确保将其副本传递给`strtok()`，以免破坏原始字符串。

### Return Value {#return-value-192 .unnumbered .unlisted}

A pointer to the next token. If you're out of tokens, `NULL` is returned.

### Example {#example-195 .unnumbered .unlisted}

::: {#cb670 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    // break up the string into a series of space or
    // punctuation-separated words
    char str[] = "Where is my bacon, dude?";
    char *token;

    // Note that the following if-do-while construct is very very
    // very very very common to see when using strtok().

    // grab the first token (making sure there is a first token!)
    if ((token = strtok(str, ".,?! ")) != NULL) {
        do {
            printf("Word: \"%s\"\n", token);

            // now, the while continuation condition grabs the
            // next token (by passing NULL as the first param)
            // and continues if the token's not NULL:
        } while ((token = strtok(NULL, ".,?! ")) != NULL);
    }
}
```
:::

Output:

::: {#cb671 .sourceCode}
``` {.sourceCode .default}
Word: "Where"
Word: "is"
Word: "my"
Word: "bacon"
Word: "dude"
```
:::

### See Also {#see-also-183 .unnumbered .unlisted}


[`strchr()`](stringref.html#man-strchr), [`strrchr()`](stringref.html#man-strchr), [`strspn()`](stringref.html#man-strspn), [`strcspn()`](stringref.html#man-strspn)

> [`strchr()`](stringref.html#man-strchr)：在字符串中查找指定字符的第一次出现的位置
[`strrchr()`](stringref.html#man-strchr)：在字符串中查找指定字符的最后一次出现的位置
[`strspn()`](stringref.html#man-strspn)：计算字符串中连续的字符的个数
[`strcspn()`](stringref.html#man-strspn)：计算字符串中不连续的字符的个数

------------------------------------------------------------------------

## [25.12]{.header-section-number} `memset()` {#man-memset number="25.12"}

Set a region of memory to a certain value

### Synopsis {#synopsis-195 .unnumbered .unlisted}

::: {#cb672 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

void *memset(void *s, int c, size_t n);
```
:::

### Description {#description-195 .unnumbered .unlisted}


This function is what you use to set a region of memory to a particular value, namely `c` converted into `unsigned char`.

> 这个函数用来将一块内存区域设置为特定值，即将`c`转换为`unsigned char`。

The most common usage is to zero out an array or `struct`.

### Return Value {#return-value-193 .unnumbered .unlisted}

`memset()` returns whatever you passed in as `s` for happy convenience.

### Example {#example-196 .unnumbered .unlisted}

::: {#cb673 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    struct banana {
        float ripeness;
        char *peel_color;
        int grams;
    };

    struct banana b;

    memset(&b, 0, sizeof b);

    printf("%d\n", b.ripeness == 0.0);     // True
    printf("%d\n", b.peel_color == NULL);  // True
    printf("%d\n", b.grams == 0);          // True
}
```
:::

### See Also {#see-also-184 .unnumbered .unlisted}


[`memcpy()`](stringref.html#man-memcpy), [`memmove()`](stringref.html#man-memcpy)

> [`memcpy()`](stringref.html#man-memcpy)：复制内存块；[`memmove()`](stringref.html#man-memcpy)：移动内存块

------------------------------------------------------------------------

## [25.13]{.header-section-number} `strerror()` {#man-strerror number="25.13"}

Get a string version of an error number

### Synopsis {#synopsis-196 .unnumbered .unlisted}

::: {#cb674 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

char *strerror(int errnum);
```
:::

### Description {#description-196 .unnumbered .unlisted}


This function ties closely into `perror()` (which prints a human-readable error message corresponding to `errno`). But instead of printing, `strerror()` returns a pointer to the locale-specific error message string.

> 这个函数与`perror()`密切相关（它会打印与`errno`相对应的人类可读的错误消息）。但`strerror()`不是打印，而是返回一个指向本地化错误消息字符串的指针。


So if you ever need that string back for some reason (e.g. you're going to `fprintf()` it to a file or something), this function will give it to you. All you need to do is pass in `errno` as an argument. (Recall that `errno` gets set as an error status by a variety of functions.)

> 如果您因为某些原因需要这个字符串（例如您要使用`fprintf()`将其写入文件等），这个函数可以给您。您只需要将`errno`作为参数传入即可（请记住，`errno`可以由各种函数设置为错误状态）。


You can actually pass in any integer for `errnum` you want. The function will return *some* message, even if the number doesn't correspond to any known value for `errno`.

> 你实际上可以为`errnum`传入任何整数。即使该数字不对应于`errno`的任何已知值，该函数也会返回某些消息。


The values of `errno` and the strings returned by `strerror()` are system-dependent.

> `errno`的值和`strerror()`返回的字符串取决于系统。

### Return Value {#return-value-194 .unnumbered .unlisted}

A string error message corresponding to the given error number.

You are not allowed to modify the returned string.

### Example {#example-197 .unnumbered .unlisted}

::: {#cb675 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>
#include <errno.h>

int main(void)
{
    FILE *fp = fopen("NONEXISTENT_FILE.TXT", "r");

    if (fp == NULL) {
        char *errmsg = strerror(errno);
        printf("Error %d opening file: %s\n", errno, errmsg);
    }
}
```
:::

Output:

::: {#cb676 .sourceCode}
``` {.sourceCode .default}
Error 2 opening file: No such file or directory
```
:::

### See Also {#see-also-185 .unnumbered .unlisted}

[`perror()`](stdio.html#man-perror)

------------------------------------------------------------------------

## [25.14]{.header-section-number} `strlen()` {#man-strlen number="25.14"}

Returns the length of a string

### Synopsis {#synopsis-197 .unnumbered .unlisted}

::: {#cb677 .sourceCode}
``` {.sourceCode .c}
#include <string.h>

size_t strlen(const char *s);
```
:::

### Description {#description-197 .unnumbered .unlisted}


This function returns the length of the passed null-terminated string (not counting the NUL character at the end). It does this by walking down the string and counting the bytes until the NUL character, so it's a little time consuming. If you have to get the length of the same string repeatedly, save it off in a variable somewhere.

> 这个函数返回传入的以null结尾的字符串的长度（不计算末尾的NUL字符）。它通过遍历字符串并计算字节数来实现，因此会花费一些时间。如果你需要重复获取同一个字符串的长度，请将其保存在某个变量中。

### Return Value {#return-value-195 .unnumbered .unlisted}


Returns the number of bytes in the string. Note that this might be different than the number of characters in a multibyte string.

> 返回字符串中的字节数。请注意，这可能与多字节字符串中的字符数不同。

### Example {#example-198 .unnumbered .unlisted}

::: {#cb678 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *s = "Hello, world!"; // 13 characters

    // prints "The string is 13 characters long.":

    printf("The string is %zu characters long.\n", strlen(s));
}
```
:::

### See Also {#see-also-186 .unnumbered .unlisted}

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdnoreturn.html) \| [Contents](index.html) \| [Next](tgmath.html)
:::
