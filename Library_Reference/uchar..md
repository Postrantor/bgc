---
tip: translate by openai@2023-07-21 09:20:04
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](time.html) \| [Contents](index.html) \| [Next](wchar.html)
:::

------------------------------------------------------------------------

# [29]{.header-section-number} `<uchar.h>` Unicode utility functions {#uchar number="29"}

  ---------------------------------------------------------------------------------------------
  Function                                  Description
  ----------------------------------------- ---------------------------------------------------

  [`c16rtomb()`](uchar.html#man-c16rtomb)   Convert a `char16_t` to a multibyte character

> `c16rtomb()` 将 `char16_t` 转换为多字节字符。


  [`c32rtomb()`](uchar.html#man-c16rtomb)   Convert a `char32_t` to a multibyte character

> c32rtomb() 将 char32_t 转换为多字节字符。


  [`mbrtoc16()`](uchar.html#man-mbrtoc16)   Convert a multibyte character to a `char16_t`

> `mbrtoc16()` 将多字节字符转换为 `char16_t`。


  [`mbrtoc32()`](uchar.html#man-mbrtoc16)   Convert a multibyte character to a `char32_t`

> mbrtoc32()将多字节字符转换为char32_t
  ---------------------------------------------------------------------------------------------


These functions are *restartable*, meaning multiple threads can safely call them at once. They handle this by having their own conversion state variable (of type `mbstate_t`) per call.

> 这些函数是可重启的，意味着多个线程可以安全地同时调用它们。它们通过每次调用都有自己的转换状态变量（类型为mbstate_t）来处理这一点。

## [29.1]{.header-section-number} Types {#types number="29.1"}

This header file defines four types.


  -----------------------------------------------------------------------------------------------------------------------

> -----------------------------------------------------------------------------------------------------------------------
无可奉告
  Type           Description

  -------------- --------------------------------------------------------------------------------------------------------

> -------------- --------------------------------------------------------------------------------------------------------
简体中文：-------------- --------------------------------------------------------------------------------------------------------
  `char16_t`     Type to hold 16-bit characters

  `char32_t`     Type to hold 32-bit characters


  `mbstate_t`    Holds the conversion state for restartable funcitons (also defined in [`<wchar.h>`](wchar.html#wchar))

> `mbstate_t`：用于重新启动功能的转换状态（也定义在[`<wchar.h>`](wchar.html#wchar)中）


  `size_t`       To hold various counts (also defined in [`<stddef.h>`](stddef.html#stddef))

> `size_t` 用于保存各种计数（也定义在[`<stddef.h>`](stddef.html#stddef)中）

  -----------------------------------------------------------------------------------------------------------------------

> -----------------------------------------------------------------------------------------------------------------------
无可奉告


String literals for the character types are `u` for `char16_t` and `U` for `char32_t`.

> 字符类型的字符串文字采用`u`表示`char16_t`，`U`表示`char32_t`。

::: {#cb798 .sourceCode}
``` {.sourceCode .c}
char16_t *str1 = u"Hello, world!";
char32_t *str2 = U"Hello, world!";

char16_t *chr1 = u'A';
char32_t *chr2 = U'B';
```
:::


Note that `char16_t` and `char32_t` *might* contain Unicode. Or not. If `__STDC_UTF_16__` or `__STDC_UTF_32__` is defined as `1`, then `char16_t` and `char32_t` use Unicode, respectively. Otherwise they don't and the actual value stored depend on the locale. And if you're not using Unicode, you have my commiserations.

> 注意，`char16_t`和`char32_t`可能包含Unicode。也可能不包含。如果`__STDC_UTF_16__`或`__STDC_UTF_32__`定义为`1`，那么`char16_t`和`char32_t`分别使用Unicode。否则它们不使用，实际存储的值取决于区域设置。如果您不使用Unicode，我表示慰问。

## [29.2]{.header-section-number} OS X issue {#os-x-issue number="29.2"}


This header file doesn't exist on OS X---bummer. If you just want the types, you can:

> 这个头文件在OS X上不存在---太糟糕了。如果你只想要类型，你可以：

::: {#cb799 .sourceCode}
``` {.sourceCode .c}
#include <stdint.h>

typedef int_least16_t char16_t;
typedef int_least32_t char32_t;
```
:::

But if you also want the functions, that's all on you.

------------------------------------------------------------------------

## [29.3]{.header-section-number} `mbrtoc16()` `mbrtoc32()` {#man-mbrtoc16 number="29.3"}

Convert a multibyte character to a `char16_t` or `char32_t` restartably

### Synopsis {#synopsis-233 .unnumbered .unlisted}

::: {#cb800 .sourceCode}
``` {.sourceCode .c}
#include <uchar.h>

size_t mbrtoc16(char16_t * restrict pc16, const char * restrict s, size_t n,
                mbstate_t * restrict ps);

size_t mbrtoc32(char32_t * restrict pc32, const char * restrict s, size_t n,
                mbstate_t * restrict ps);
```
:::

### Description {#description-233 .unnumbered .unlisted}


Given a source string `s` and a destination buffer `pc16` (or `pc32` for `mbrtoc32()`), convert the first character of the source to `char16_t`s (or `char32_t`s for `mbrtoc32()`).

> 给定源字符串`s`和目标缓冲区`pc16`（或`mbrtoc32()`的`pc32`），将源的第一个字符转换为`char16_t`（或`mbrtoc32()`的`char32_t`）。


Basically you have a regular character and you want it as `char16_t` or `char32_t`. Use these functions to do it. Note that only one character is converted no matter how many characters in `s`.

> 基本上，您有一个普通字符，并希望将其转换为`char16_t`或`char32_t`。使用这些函数来完成。请注意，无论`s`中有多少字符，只转换一个字符。


As the functions scan `s`, you don't want them to overrun the end. So you pass in `n` as the maximum number of bytes to inspect. The functions will quit after that many bytes or when they have a complete multibyte character, whichever comes first.

> 当函数扫描's时，你不希望它们越过结尾。因此，您将n作为要检查的最大字节数传入。函数将在达到该字节数或完成多字节字符之后退出，以先到者为准。


Since they're restartable, pass in a conversion state variable for the functions to do their work.

> 由于它们可以重新启动，因此为函数提供转换状态变量以完成其工作。

And the result will be placed in `pc16` (or `pc32` for `mbrtoc32()`).

### Return Value {#return-value-231 .unnumbered .unlisted}


When successful this function returns a number between `1` and `n` inclusive representing the number of bytes that made up the multibyte character.

> 当成功时，此函数返回一个介于1和n之间的数字，表示构成多字节字符的字节数。


Or, also in the success category, they can return `0` if the source character is the NUL character (value `0`).

> 或者，如果源字符是空字符（值为0），也可以在成功类别中返回0。


When not entirely successful, they can return a variety of codes. These are all of type `size_t`, but negative values cast to that type.

> 如果不能完全成功，它们可以返回各种代码。这些都是`size_t`类型，但负值被转换为该类型。


  ------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------
简化中文
  Return Value     Description

  ---------------- -------------------------------------------------------------------------------------------

> ---------------- -------------------------------------------------------------------------------------------
空白

  `(size_t)(-1)`   Encoding error---this isn't a valid sequence of bytes. `errno` is set to `EILSEQ`.

> 编码错误---这不是一个有效的字节序列。`errno`被设置为`EILSEQ`。


  `(size_t)(-2)`   `n` bytes were examined and were a *partial* valid character, but not a complete one.

> 已检查了 (size_t)(-2) 字节，它们是部分有效字符，但不是完整字符。


  `(size_t)(-3)`   A subsequent value of a character that can't be represented as a single value. See below.

> (size_t)(-3)：无法用单个值表示的后续字符的值。详见下文。

  ------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------
简化中文


Case `(size_t)(-3)` is an odd one. Basically there are some characters that can't be represented with 16 bits and so can't be stored in a `char16_t`. These characters are store in something called (in the Unicode world) *surrogate pairs*. That is, there are *two* 16-bit values back to back that represent a larger Unicode value.

> 这种情况(size_t)(-3)很特殊。有一些字符无法用16位表示，因此无法存储在char16_t中。这些字符在Unicode世界中被称为*替代对*。也就是说，有*两个*16位值连续表示更大的Unicode值。


For example, if you want to read the Unicode character `\U0001fbc5` (which is a [stick figure](https://en.wikipedia.org/wiki/Symbols_for_Legacy_Computing)[^76^](footnotes.html#fn76){#fnref76 .footnote-ref role="doc-noteref"}---I'm just not putting it in the text because my font doesn't render it) that's more than 16 bits. But each call to `mbrtoc16()` only returns a single `char16_t`!

> 如果你想读取Unicode字符\U0001fbc5（这是一个[插图](https://en.wikipedia.org/wiki/Symbols_for_Legacy_Computing)[^76^](footnotes.html#fn76){#fnref76 .footnote-ref role="doc-noteref"}，但我的字体不支持它），它的位数超过16位。但每次调用`mbrtoc16()`只会返回一个`char16_t`！


So subsequent calls to `mbrtoc16()` resolves the *next* value in the surrogate pair and returns `(size_t)(-3)` to let you know this has happened.

> 因此，随后对`mbrtoc16（）`的调用将解析替代对中的下一个值，并返回`（size_t）（-3）`以提醒您发生了这种情况。


You can also pass `NULL` for `pc16` or `pc32`. This will cause no result to be stored, but you can use it if you're only interested in the return value from the functions.

> 你也可以将`NULL`传递给`pc16`或`pc32`。这将导致不存储任何结果，但如果你只对函数的返回值感兴趣，你可以使用它。

Finally, if you pass `NULL` for `s`, the call is equivalent to:

::: {#cb801 .sourceCode}
``` {.sourceCode .c}
mbrtoc16(NULL, "", 1, ps)
```
:::


Since the character is a NUL in that case, this has the effect of setting the state in `ps` to the initial conversion state.

> 在这种情况下，由于字符是NUL，因此这会使`ps`的状态设置为初始转换状态。

### Example {#example-235 .unnumbered .unlisted}


Normal use case example where we get the first two character values from the multibyte string `"€Zillion"`:

> 一般使用案例，我们从多字节字符串"€Zillion"中获取前两个字符值：

::: {#cb802 .sourceCode}
``` {.sourceCode .c}
#include <uchar.h>
#include <stdio.h>   // for printf()
#include <locale.h>  // for setlocale()
#include <string.h>  // for memset()

int main(void)
{
    char *s = "\u20acZillion";  // 20ac is "€"
    char16_t pc16;
    size_t r;
    mbstate_t mbs;

    setlocale(LC_ALL, "");
    memset(&mbs, 0, sizeof mbs);

    // Examine the next 8 bytes to see if there's a character in there
    r = mbrtoc16(&pc16, s, 8, &mbs);

    printf("%zu\n", r);     // Prints a value >= 1 (3 in UTF-8 locale)
    printf("%#x\n", pc16);  // Prints 0x20ac for "€"

    s += r;  // Move to next character

    // Examine the next 8 bytes to see if there's a character in there
    r = mbrtoc16(&pc16, s, 8, &mbs);

    printf("%zu\n", r);     // Prints 1
    printf("%#x\n", pc16);  // Prints 0x5a for "Z"
}
```
:::


Example with a surrogate pair. In this case we read plenty to get the entire character, but the result must be stored in two `char16_t`s, requiring two calls to get them both.

> 例子中使用了一个替代对。在这种情况下，我们需要读取大量内容来获得整个字符，但结果必须存储在两个`char16_t`中，需要两次调用才能获得它们。

::: {#cb803 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <uchar.h>
#include <stdio.h>   // for printf()
#include <string.h>  // for memset()
#include <locale.h>  // for setlocale()

int main(void)
{
    char *s = "\U0001fbc5*";   // Stick figure glyph, more than 16 bits
    char16_t pc16;
    mbstate_t mbs;
    size_t r;

    setlocale(LC_ALL, "");
    memset(&mbs, 0, sizeof mbs);

    r = mbrtoc16(&pc16, s, 8, &mbs);

    printf("%zd\n", r);     // r is 4 bytes in UTF-8 locale
    printf("%#x\n", pc16);  // First value of surrogate pair

    s += r;  // Move to next character

    r = mbrtoc16(&pc16, s, 8, &mbs);

    printf("%zd\n", r);     // r is (size_t)(-3) here to indicate...
    printf("%#x\n", pc16);  // ...Second value of surrogate pair

    // Since r is -3, it means we're still processing the same
    // character, so DON'T move to the next character this time
    //s += r;  // Commented out

    r = mbrtoc16(&pc16, s, 8, &mbs);

    printf("%zd\n", r);     // 1 byte for "*"
    printf("%#x\n", pc16);  // 0x2a for "*"
}
```
:::


Output on my system, indicating the first character is represented by the pair `(0xd83e, 0xdfc5)` and the second character is represented by `0x2a`:

> 在我的系统上的输出，表明第一个字符由（0xd83e，0xdfc5）对表示，第二个字符由0x2a表示：

::: {#cb804 .sourceCode}
``` {.sourceCode .default}
4
0xd83e
-3
0xdfc5
1
0x2a
```
:::

### See Also {#see-also-221 .unnumbered .unlisted}


[`c16rtomb()`](uchar.html#man-c16rtomb), [`c32rtomb()`](uchar.html#man-c16rtomb)

> c16rtomb()、c32rtomb()

------------------------------------------------------------------------

## [29.4]{.header-section-number} `c16rtomb()` `c32rtomb()` {#man-c16rtomb number="29.4"}

Convert a `char16_t` or `char32_t` to a multibyte character restartably

### Synopsis {#synopsis-234 .unnumbered .unlisted}

::: {#cb805 .sourceCode}
``` {.sourceCode .c}
#include <uchar.h>

size_t c16rtomb(char * restrict s, char16_t c16, mbstate_t * restrict ps);

size_t c32rtomb(char * restrict s, char32_t c32, mbstate_t * restrict ps);
```
:::

### Description {#description-234 .unnumbered .unlisted}


If you have a character in a `char16_t` or `char32_t`, use these functions to convert them into a multibyte character.

> 如果你有一个`char16_t`或`char32_t`中的字符，请使用这些函数将它们转换为多字节字符。


These functions figure out how many bytes are needed for the multibyte character in the current locale and stores them in the buffer pointed to by `s`.

> 这些函数计算出当前区域设置中多字节字符所需的字节数，并将其存储在指向`s`的缓冲区中。


But how big to make that buffer? Luckily there is a macro to help: it needs be no larger than `MB_CUR_MAX`.

> 但是要多大的缓冲区呢？幸运的是有一个宏可以帮助：它不能大于“MB_CUR_MAX”。

As a special case, if `s` is `NULL`, it's the same as calling

::: {#cb806 .sourceCode}
``` {.sourceCode .c}
c16rtomb(buf, L'\0', ps);  // or...
c32rtomb(buf, L'\0', ps);
```
:::


where `buf` is a buffer maintained by the system that you don't have access to.

> 在这里，`buf`是一个由系统维护的缓冲区，你无法访问。

This has the effect of setting the `ps` state to the initial state.


Finally for surrogate pairs (where the character has been split into two `char16_t`s), you call this once with the first of the pair---at this point, the function will return `0`. Then you call it again with the second of the pair, and the function will return the number of bytes and store the result in the array `s`.

> 最后，对于代理对（字符被分割成两个char16_t），你先调用第一个字符，此时函数会返回0。然后你再调用第二个字符，函数会返回字节数并将结果存储在数组s中。

### Return Value {#return-value-232 .unnumbered .unlisted}

Returns the number of bytes stored in the array pointed to by `s`.


Returns 0 if processing is not yet complete for the current character, as in the case of surrogate pairs.

> 如果对于当前字符的处理尚未完成，则返回0，例如对于替代对的情况。


If there is an encoding error, the functions return `(size_t)(-1)` and `errno` is set to `EILSEQ`.

> 如果有编码错误，函数会返回`(size_t)(-1)`，并且将`errno`设置为`EILSEQ`。

### Example {#example-236 .unnumbered .unlisted}

::: {#cb807 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <uchar.h>
#include <stdlib.h>  // for MB_CUR_MAX
#include <stdio.h>   // for printf()
#include <string.h>  // for memset()
#include <locale.h>  // for setlocale()

int main(void)
{
    char16_t c16 = 0x20ac;  // Unicode for Euro symbol
    char dest[MB_CUR_MAX];
    size_t r;
    mbstate_t mbs;

    setlocale(LC_ALL, "");
    memset(&mbs, 0, sizeof mbs);  // Reset conversion state

    // Convert
    r = c16rtomb(dest, c16, &mbs);

    printf("r == %zd\n", r);  // r == 3 on my system

    // And this should print a Euro symbol
    printf("dest == \"%s\"\n", dest);
}
```
:::

Output on my system:

::: {#cb808 .sourceCode}
``` {.sourceCode .default}
r == 3
dest == "€"
```
:::


This is a more complex example that converts a large-valued character in a multibyte string into a surrogate pair (as in the `mbrtoc16()` example, above) and then converts it back again into a multibyte string to print.

> 这是一个更复杂的例子，它将多字节字符串中的大值字符转换为代理对（如上面的`mbrtoc16()`示例），然后再将其转换回多字节字符串以进行打印。

::: {#cb809 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <uchar.h>
#include <stdlib.h>  // for MB_CUR_MAX
#include <stdio.h>   // for printf()
#include <string.h>  // for memset()
#include <locale.h>  // for setlocale()

int main(void)
{
    char *src = "\U0001fbc5*";   // Stick figure glyph, more than 16 bits
    char dest[MB_CUR_MAX];
    char16_t surrogate0, surrogate1;
    mbstate_t mbs;
    size_t r;

    setlocale(LC_ALL, "");
    memset(&mbs, 0, sizeof mbs);  // Reset conversion state

    // Get first surrogate character
    r = mbrtoc16(&surrogate0, src, 8, &mbs);

    // Get next surrogate character
    src += r;  // Move to next character
    r = mbrtoc16(&surrogate1, src, 8, &mbs);

    printf("Surrogate pair: %#x, %#x\n", surrogate0, surrogate1);

    // Now reverse it
    memset(&mbs, 0, sizeof mbs);  // Reset conversion state

    // Process first surrogate character
    r = c16rtomb(dest, surrogate0, &mbs);

    // r should be 0 at this point, because the character hasn't been
    // processed yet. And dest won't have anything useful... yet!
    printf("r == %zd\n", r);   // r == 0

    // Process second surrogate character
    r = c16rtomb(dest, surrogate1, &mbs);

    // Now we should be in business. r should have the number of
    // bytes, and dest should hold the character.
    printf("r == %zd\n", r);  // r == 4 on my system

    // And this should print a stick figure, if your font supports it
    printf("dest == \"%s\"\n", dest);
}
```
:::

### See Also {#see-also-222 .unnumbered .unlisted}


[`mbrtoc16()`](uchar.html#man-mbrtoc16), [`mbrtoc32()`](uchar.html#man-mbrtoc16)

> [`mbrtoc16()`](uchar.html#man-mbrtoc16)，[`mbrtoc32()`](uchar.html#man-mbrtoc16)：将多字节字符转换为 UTF-16 或 UTF-32 字符。

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](time.html) \| [Contents](index.html) \| [Next](wchar.html)
:::
