---
tip: translate by openai@2023-07-20 19:10:14
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](signal.html) \| [Contents](index.html) \| [Next](stdarg.html)
:::

------------------------------------------------------------------------

# [16]{.header-section-number} `<stdalign.h>` Macros for Alignment {#stdalign number="16"}


If you're coding up something low-level like a memory allocator that interfaces with your OS, you might need this header file. But most C devs go their careers without using it.

> 如果你正在编写一些低级别的东西，比如与操作系统交互的内存分配器，你可能需要这个头文件。但大多数C开发人员在他们的职业生涯中都没有使用它。


[*Alignment*](https://en.wikipedia.org/wiki/Data_structure_alignment)[^37^](footnotes.html#fn37){#fnref37 .footnote-ref role="doc-noteref"} is all about multiples of addresses on which objects can be stored. Can you store this at any address? Or must it be a starting address that's divisible by 2? Or 8? Or 16?

> [对齐](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%AF%B9%E9%BD%90)[^37^](footnotes.html#fn37){#fnref37 .footnote-ref role="doc-noteref"} 是关于存储对象的多个地址的一切。你可以在任何地址存储它吗？还是必须是一个可以被2整除的起始地址？或8？或16？

  Name                                       Description
  ------------------------------------------ ------------------------------------------

  [`alignas()`](stdalign.html#man-alignas)   Specify alignment, expands to `_Alignas`

> [`alignas()`](stdalign.html#man-alignas)：指定对齐，展开为`_Alignas`

  [`alignof()`](stdalign.html#man-alignof)   Get alignment, expands to `_Alignof`

> `alignof()`获取对齐，展开为`_Alignof`

These two additional macros are defined to be `1`:

::: {#cb409 .sourceCode}
``` {.sourceCode .c}
__alignas_is_defined
__alignof_is_defined
```
:::


Quick note: alignments greater than that of `max_align_t` are known as *overalignments* and are implementation-defined.

> 快速提示：大于`max_align_t`的对齐称为*超对齐*，具体实现取决于实现者。

## [16.1]{.header-section-number} `alignas()` `_Alignas()` {#man-alignas number="16.1"}

Force a variable to have a certain alignment

### Synopsis {#synopsis-116 .unnumbered .unlisted}

::: {#cb410 .sourceCode}
``` {.sourceCode .c}
#include <stdalign.h>

alignas(type-name)
alignas(constant-expression)
```
:::

::: {#cb411 .sourceCode}
``` {.sourceCode .c}
_Alignas(type-name)
_Alignas(constant-expression)
```
:::

### Description {#description-116 .unnumbered .unlisted}


Use this *alignment specifier* to force the alignment of particular variables. For instance, we can declare `c` to be `char`, but aligned as if it were an `int`:

> 使用这个对齐规范来强制特定变量的对齐。例如，我们可以声明`c`为`char`，但是对齐方式像`int`一样：

::: {#cb412 .sourceCode}
``` {.sourceCode .c}
char alignas(int) c;
```
:::


You can put a constant integer expression in there, as well. The compiler will probably impose limits on what these values can be. Small powers of 2 (1, 2, 4, 8, and 16) are generally safe bets.

> 你也可以在里面放入一个常整数表达式。编译器可能会对这些值施加限制。2的小次幂（1，2，4，8和16）通常是安全的。

::: {#cb413 .sourceCode}
``` {.sourceCode .c}
char alignas(8) c;   // align on 8-byte boundaries
```
:::


For convenience, you can also specify `0` if you want the default alignment (as if you hadn't said `alignas()` at all):

> 为了方便起见，如果您不想使用`alignas()`，您也可以指定`0`以使用默认对齐方式。

::: {#cb414 .sourceCode}
``` {.sourceCode .c}
char alignas(0) c;   // use default alignment for this type
```
:::

### Example {#example-116 .unnumbered .unlisted}

::: {#cb415 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdalign.h>
#include <stdio.h>     // for printf()
#include <stddef.h>    // for max_align_t

int main(void)
{
    int i, j;
    char alignas(max_align_t) a, b;
    char alignas(int) c, d;
    char e, f;

    printf("i: %p\n", (void *)&i);
    printf("j: %p\n\n", (void *)&j);
    printf("a: %p\n", (void *)&a);
    printf("b: %p\n\n", (void *)&b);
    printf("c: %p\n", (void *)&c);
    printf("d: %p\n\n", (void *)&d);
    printf("e: %p\n", (void *)&e);
    printf("f: %p\n", (void *)&f);
}
```
:::


Output on my system follows. Notice the difference between the pairs of values.

> 系统输出如下，注意两个值之间的区别。

-   `i` and `j`, both `int`s, are aligned on 4-byte boundaries.

-   `a` and `b` have been forced to the boundary of the type `max_align_t`, which is every 16 bytes on my system.

> a和b被强制调整到max_align_t类型的边界，在我的系统中每16个字节。

-   `c` and `d` have been forced to the same alignment as `int`, which is 4 bytes, just like with `i` and `j`.

> c和d被迫与int一样，占用4个字节，就像i和j一样。

-   `e` and `f` do not have an alignment specified, so they were stored with their default alignment of 1 byte.

> `e`和`f`没有指定对齐方式，因此它们以默认的1字节对齐方式存储。

::: {#cb416 .sourceCode}
``` {.sourceCode .default}
i: 0x7ffee7dfb4cc    <-- difference of 4 bytes
j: 0x7ffee7dfb4c8

a: 0x7ffee7dfb4c0    <-- difference of 16 bytes
b: 0x7ffee7dfb4b0

c: 0x7ffee7dfb4ac    <-- difference of 4 bytes
d: 0x7ffee7dfb4a8

e: 0x7ffee7dfb4a7    <-- difference of 1 byte
f: 0x7ffee7dfb4a6
```
:::

### See Also {#see-also-109 .unnumbered .unlisted}


[`alignof`](stdalign.html#man-alignof), [`max_align_t`](stddef.html#man-max_align_t)

> [`alignof`](stdalign.html#man-alignof)：取得对象的对齐值
[`max_align_t`](stddef.html#man-max_align_t)：最大可对齐类型

------------------------------------------------------------------------

## [16.2]{.header-section-number} `alignof()` `_Alignof()` {#man-alignof number="16.2"}

Get the alignment of a type

### Synopsis {#synopsis-117 .unnumbered .unlisted}

::: {#cb417 .sourceCode}
``` {.sourceCode .c}
#include <stdalign.h>

alignof(type-name)
```
:::

::: {#cb418 .sourceCode}
``` {.sourceCode .c}
_Alignof(type-name)
```
:::

### Description {#description-117 .unnumbered .unlisted}


This evaluates to a value of type `size_t` that gives the alignment of a particular type on your system.

> 这会评估一个值，类型为`size_t`，它可以给出系统中特定类型的对齐方式。

### Return Value {#return-value-115 .unnumbered .unlisted}


Returns the alignment value, i.e. the address of the beginning of the given type of object must begin on an address boundary divisible by this number.

> 返回对齐值，即给定类型对象的开始地址必须以能被此数整除的地址边界开始。

### Example {#example-117 .unnumbered .unlisted}

Print out the alignments of a variety of different types.

::: {#cb419 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdalign.h>
#include <stdio.h>     // for printf()
#include <stddef.h>    // for max_align_t

struct t {
    int a;
    char b;
    float c;
};

int main(void)
{
    printf("char       : %zu\n", alignof(char));
    printf("short      : %zu\n", alignof(short));
    printf("int        : %zu\n", alignof(int));
    printf("long       : %zu\n", alignof(long));
    printf("long long  : %zu\n", alignof(long long));
    printf("double     : %zu\n", alignof(double));
    printf("long double: %zu\n", alignof(long double));
    printf("struct t   : %zu\n", alignof(struct t));
    printf("max_align_t: %zu\n", alignof(max_align_t));
}
```
:::

Output on my system:

::: {#cb420 .sourceCode}
``` {.sourceCode .default}
char       : 1
short      : 2
int        : 4
long       : 8
long long  : 8
double     : 8
long double: 16
struct t   : 16
max_align_t: 16
```
:::

### See Also {#see-also-110 .unnumbered .unlisted}


[`alignas`](stdalign.html#man-alignas), [`max_align_t`](stddef.html#man-max_align_t)

> [`alignas`](stdalign.html#man-alignas)：对齐
[`max_align_t`](stddef.html#man-max_align_t)：最大对齐类型

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](signal.html) \| [Contents](index.html) \| [Next](stdarg.html)
:::
