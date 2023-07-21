---
tip: translate by openai@2023-07-21 08:39:42
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](stdint.html) \| [Contents](index.html) \| [Next](stdlib.html)
:::

------------------------------------------------------------------------

# [22]{.header-section-number} `<stdio.h>` Standard I/O Library {#stdio number="22"}


  ------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。
  Function                                  Description

  ----------------------------------------- ------------------------------------------------------------

> ----------------------------------------- ------------------------------------------------------------
简体中文：
----------------------------------------- ------------------------------------------------------------

  [`clearerr()`](stdio.html#man-feof)       Clear the `feof` and `ferror` status flags

> clearerr()（stdio.html#man-feof）清除feof和ferror状态标志

  [`fclose()`](stdio.html#man-fclose)       Close an open file


  [`feof()`](stdio.html#man-feof)           Return the file end-of-file status

> feof() 返回文件结束状态

  [`ferror()`](stdio.html#man-feof)         Return the file error status


  [`fflush()`](stdio.html#man-fflush)       Flush all buffered output to a file

> `fflush()`（stdio.html#man-fflush）将所有缓冲输出刷新到文件。

  [`fgetc()`](stdio.html#man-getc)          Read a character in a file

  [`fgetpos()`](stdio.html#man-fgetpos)     Get the file I/O position

  [`fgets()`](stdio.html#man-gets)          Read a line from a file

  [`fopen()`](stdio.html#man-fopen)         Open a file


  [`fprintf()`](stdio.html#man-printf)      Print formatted output to a file

> `fprintf()`（[stdio.html#man-printf](stdio.html#man-printf)）打印格式化输出到文件

  [`fputc()`](stdio.html#man-putc)          Print a character to a file

  [`fputs()`](stdio.html#man-puts)          Print a string to a file

  [`fread()`](stdio.html#man-fread)         Read binary data from a file


  [`freopen()`](stdio.html#man-freopen)     Change file associated with a stream

> 改变与流相关的文件，使用freopen()函数


  [`fscanf()`](stdio.html#man-scanf)        Read formatted input from a file

> `fscanf()`（stdio.html#man-scanf）从文件中读取格式化的输入

  [`fseek()`](stdio.html#man-fseek)         Set the file I/O position

  [`fsetpos()`](stdio.html#man-fgetpos)     Set the file I/O position

  [`ftell()`](stdio.html#man-ftell)         Get the file I/O position

  [`fwrite()`](stdio.html#man-fwrite)       Write binary data to a file

  [`getc()`](stdio.html#man-getc)           Get a character from `stdin`

  [`getchar()`](stdio.html#man-getc)        Get a character from `stdin`


  [`gets()`](stdio.html#man-gets)           Get a string from `stdin` (removed in C11)

> `gets()`（参见stdio.html#man-gets）从`stdin`获取一个字符串（C11中已移除）


  [`perror()`](stdio.html#man-perror)       Print a human-formatted error message

> perror() 函数打印出一条人类可读的错误消息。


  [`printf()`](stdio.html#man-printf)       Print formatted output to `stdout`

> `printf()`（[stdio.html#man-printf](stdio.html#man-printf)）打印格式化输出到`stdout`

  [`putc()`](stdio.html#man-putc)           Print a character to `stdout`

  [`putchar()`](stdio.html#man-putc)        Print a character to `stdout`

  [`puts()`](stdio.html#man-puts)           Print a string to `stdout`

  [`remove()`](stdio.html#man-remove)       Delete a file from disk

  [`rename()`](stdio.html#man-rename)       Rename or move a file on disk


  [`rewind()`](stdio.html#man-fseek)        Set the I/O position to the beginning of a file

> `rewind()`（[`stdio.html#man-fseek`](stdio.html#man-fseek)）设置I/O位置到文件开头。


  [`scanf()`](stdio.html#man-scanf)         Read formatted input from `stdin`

> `scanf()`从`stdin`读取格式化输入


  [`setbuf()`](stdio.html#man-setbuf)       Configure buffering for I/O operations

> 设置I/O操作的缓冲区


  [`setvbuf()`](stdio.html#man-setbuf)      Configure buffering for I/O operations

> 设置I/O操作的缓冲区


  [`snprintf()`](stdio.html#man-printf)     Print length-limited formatted output to a string

> `snprintf()`（[stdio.html#man-printf](stdio.html#man-printf)）打印有限长度格式化输出到字符串。


  [`sprintf()`](stdio.html#man-printf)      Print formatted output to a string

> 使用格式化输出将字符串打印到一个字符串中。


  [`sscanf()`](stdio.html#man-scanf)        Read formatted input from a string

> `sscanf()`（stdio.html#man-scanf）从字符串中读取格式化输入

  [`tmpfile()`](stdio.html#man-tmpfile)     Create a temporary file


  [`tmpnam()`](stdio.html#man-tmpnam)       Generate a unique name for a temporary file

> tmpnam()函数可以生成一个临时文件的唯一名称。


  [`ungetc()`](stdio.html#man-ungetc)       Push a character back on the input stream

> `ungetc()`（[stdio.html#man-ungetc](stdio.html#man-ungetc)）将一个字符推回输入流。


  [`vfprintf()`](stdio.html#man-vprintf)    Variadic print formatted output to a file

> [`vfprintf()`](stdio.html#man-vprintf)：向文件输出可变参数格式化的输出。


  [`vfscanf()`](stdio.html#man-vscanf)      Variadic read formatted input from a file

> `vfscanf()`（[stdio.html#man-vscanf](stdio.html#man-vscanf)）：从文件中读取可变参数格式化的输入。


  [`vprintf()`](stdio.html#man-vprintf)     Variadic print formatted output to `stdout`

> `vprintf()`（[stdio.html#man-vprintf](stdio.html#man-vprintf)）：根据格式将变参输出到`stdout`


  [`vscanf()`](stdio.html#man-vscanf)       Variadic read formatted input from `stdin`

> vscanf()：从stdin读取带变参格式的输入


  [`vsnprintf()`](stdio.html#man-vprintf)   Variadic length-limited print formatted output to a string

> vsnprintf()：使用可变参数格式化输出到字符串，限制长度。


  [`vsprintf()`](stdio.html#man-vprintf)    Variadic print formatted output to a string

> `vsprintf()`（[stdio.html#man-vprintf](stdio.html#man-vprintf)）：根据格式将可变参数的输出打印到字符串中。


  [`vsscanf()`](stdio.html#man-vscanf)      Variadic read formatted input to a string

> [`vsscanf()`](stdio.html#man-vscanf)：可变参数的格式化输入读取到字符串。

  ------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。


The most basic of all libraries in the whole of the standard C library is the standard I/O library. It's used for reading from and writing to files. I can see you're very excited about this.

> 最基本的标准C库是标准I/O库。它用于读取和写入文件。我可以看到你对此非常兴奋。


So I'll continue. It's also used for reading and writing to the console, as we've already often seen with the `printf()` function.

> 所以我们继续吧。它也用于读取和写入控制台，正如我们经常看到的`printf()`函数一样。


(A little secret here---many many things in various operating systems are secretly files deep down, and the console is no exception. "*Everything in Unix is a file!*" `:-)`)

> 这里有一个小秘密---许多许多的东西在各种操作系统中都是深藏不露的文件，控制台也不例外。“Unix 中的一切都是文件！”


You'll probably want some prototypes of the functions you can use, right? To get your grubby little mittens on those, you'll want to include `stdio.h`.

> 你可能想要一些可以使用的函数原型，对吗？要获取这些，你需要包含`stdio.h`。


Anyway, so we can do all kinds of cool stuff in terms of file I/O. LIE DETECTED. Ok, ok. We can do all kinds of stuff in terms of file I/O. Basically, the strategy is this:

> 不管怎样，我们可以在文件I/O方面做各种酷炫的事情。检测到谎言。好吧，好吧。我们可以在文件I/O方面做各种事情。基本上，策略是这样的：


1.  Use `fopen()` to get a pointer to a file structure of type `FILE*`. This pointer is what you'll be passing to many of the other file I/O calls.

> 使用`fopen()`获取一个类型为`FILE*`的文件结构的指针。这个指针将传递给其他文件I/O调用。


2.  Use some of the other file calls, like `fscanf()`, `fgets()`, `fprintf()`, or etc. using the `FILE*` returned from `fopen()`.

> 使用`fopen()`返回的`FILE*`，使用其他文件调用，如`fscanf()`、`fgets()`、`fprintf()`等。


3.  When done, call `fclose()` with the `FILE*`. This let's the operating system know that you're truly done with the file, no take-backs.

> 完成后，使用`FILE*`调用`fclose()`。这样操作系统就知道您真的完成了文件，不能撤销。


What's in the `FILE*`? Well, as you might guess, it points to a `struct` that contains all kinds of information about the current read and write position in the file, how the file was opened, and other stuff like that. But, honestly, who cares. No one, that's who. The `FILE` structure is *opaque* to you as a programmer; that is, you don't need to know what's in it, and you don't even *want* to know what's in it. You just pass it to the other standard I/O functions and they know what to do.

> 你在`FILE*`里有什么？嗯，正如你所猜想的，它指向一个`struct`，其中包含有关当前文件读写位置、文件如何打开以及其他一些信息的所有信息。但是，老实说，谁会在乎呢？没有人，就是这样。`FILE`结构对你来说是*不透明*的；也就是说，你不需要知道里面有什么，甚至你也不想知道里面有什么。你只需要将它传递给其他标准I/O函数，它们就知道该怎么做了。


This is actually pretty important: try to not muck around in the `FILE` structure. It's not even the same from system to system, and you'll end up writing some really non-portable code.

> 这其实很重要：尽量不要在`FILE`结构中乱搞。它甚至在不同的系统中都不一样，你最终会编写一些不可移植的代码。


One more thing to mention about the standard I/O library: a lot of the functions that operate on files use an "f" prefix on the function name. The same function that is operating on the console will leave the "f" off. For instance, if you want to print to the console, you use `printf()`, but if you want to print to a file, use `fprintf()`, see?

> 关于标准I/O库还有一件事要提一下：很多操作文件的函数名前面都会有一个“f”前缀。操作控制台的函数则不带“f”前缀。比如，如果你想在控制台输出，就使用`printf()`，而如果你想输出到文件，就使用`fprintf()`，明白了吗？


Wait a moment! If writing to the console is, deep down, just like writing to a file, since everything in Unix is a file, why are there two functions? Answer: it's more convenient. But, more importantly, is there a `FILE*` associated with the console that you can use? Answer: YES!

> 等一下！如果写入控制台就像写入文件一样，因为Unix中的一切都是文件，为什么会有两个函数？答案：这更方便。但更重要的是，控制台是否有一个可以使用的`FILE*`？答案：是的！


There are, in fact, *three* (count 'em!) special `FILE*`s you have at your disposal merely for just including `stdio.h`. There is one for input, and two for output.

> 实际上，只要包含`stdio.h`，你就可以拥有三个（数一数！）特殊的`FILE*`。其中一个是用于输入，另外两个是用于输出。


That hardly seems fair---why does output get two files, and input only get one?

> 这似乎不太公平---为什么输出有两个文件，而输入只有一个文件？

That's jumping the gun a bit---let's just look at them:

  -------------------------------------------------------------------------------------
  Stream                              Description
  ----------------------------------- -------------------------------------------------
  `stdin`                             Input from the console.

  `stdout`                            Output to the console.


  `stderr`                            Output to the console on the error file stream.

> 输出到错误文件流上的控制台。
  -------------------------------------------------------------------------------------


So standard input (`stdin`) is by default just what you type at the keyboard. You can use that in `fscanf()` if you want, just like this:

> 标准输入（`stdin`）默认只是你在键盘上输入的内容。如果你想用`fscanf()`，可以这样：

::: {#cb491 .sourceCode}
``` {.sourceCode .c}
/* this line: */
scanf("%d", &x);

/* is just like this line: */
fscanf(stdin, "%d", &x);
```
:::

And `stdout` works the same way:

::: {#cb492 .sourceCode}
``` {.sourceCode .c}
printf("Hello, world!\n");
fprintf(stdout, "Hello, world!\n"); /* same as previous line! */
```
:::


So what is this `stderr` thing? What happens when you output to that? Well, generally it goes to the console just like `stdout`, but people use it for error messages, specifically. Why? On many systems you can redirect the output from the program into a file from the command line...and sometimes you're interested in getting just the error output. So if the program is good and writes all its errors to `stderr`, a user can redirect just `stderr` into a file, and just see that. It's just a nice thing you, as a programmer, can do.

> 那么这个`stderr`是什么？当你输出到它时会发生什么？通常它会像`stdout`一样输出到控制台，但人们会用它来输出错误信息。为什么？在许多系统中，你可以从命令行将程序的输出重定向到文件中...有时你只想获取错误输出。因此，如果程序很好，并将所有错误写入`stderr`，用户可以将`stderr`重定向到文件中，只看到错误信息。这对你作为程序员来说是一件很好的事情。


Finally, a lot of these functions return `int` where you might expect `char`. This is because the function can return a character *or* end-of-file (`EOF`), and `EOF` is potentially an integer. If you don't get `EOF` as a return value, you can safely store the result in a `char`.

> 最后，许多这些函数会返回一个`int`，而不是你期望的`char`。这是因为该函数可以返回一个字符*或*文件结束（`EOF`），而`EOF`可能是一个整数。如果您没有获得`EOF`作为返回值，您可以安全地将结果存储在`char`中。

------------------------------------------------------------------------

## [22.1]{.header-section-number} `remove()` {#man-remove number="22.1"}

Delete a file

### Synopsis {#synopsis-135 .unnumbered .unlisted}

::: {#cb493 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int remove(const char *filename); 
```
:::

### Description {#description-135 .unnumbered .unlisted}


Removes the specified file from the filesystem. It just deletes it. Nothing magical. Simply call this function and sacrifice a small chicken and the requested file will be deleted.

> 从文件系统中删除指定的文件。它只是删除它。没有什么神奇的。只需调用此函数，牺牲一只小鸡，所请求的文件就会被删除。

### Return Value {#return-value-133 .unnumbered .unlisted}

Returns zero on success, and `-1` on error, setting `errno`.

### Example {#example-136 .unnumbered .unlisted}

::: {#cb494 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    char *filename = "evidence.txt";

    remove(filename);
}
```
:::

### See Also {#see-also-127 .unnumbered .unlisted}

[`rename()`](stdio.html#man-rename)

------------------------------------------------------------------------

## [22.2]{.header-section-number} `rename()` {#man-rename number="22.2"}

Renames a file and optionally moves it to a new location

### Synopsis {#synopsis-136 .unnumbered .unlisted}

::: {#cb495 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int rename(const char *old, const char *new);
```
:::

### Description {#description-136 .unnumbered .unlisted}


Renames the file `old` to name `new`. Use this function if you're tired of the old name of the file, and you are ready for a change. Sometimes simply renaming your files makes them feel new again, and could save you money over just getting all new files!

> 将文件`old`重命名为`new`。如果你厌倦了文件的旧名称，并准备更改，可以使用此功能。有时，只需重命名文件就可以使它们重新焕发新生，并可以节省购买全新文件的费用！


One other cool thing you can do with this function is actually move a file from one directory to another by specifying a different path for the new name.

> 你可以用这个函数做另一件很酷的事情，就是通过指定不同的路径来将文件从一个目录移动到另一个目录。

### Return Value {#return-value-134 .unnumbered .unlisted}

Returns zero on success, and `-1` on error, setting `errno`.

### Example {#example-137 .unnumbered .unlisted}

::: {#cb496 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    // Rename a file
    rename("foo", "bar");

    // Rename and move to another directory:
    rename("/home/beej/evidence.txt", "/tmp/nothing.txt");
}
```
:::

### See Also {#see-also-128 .unnumbered .unlisted}

[`remove()`](stdio.html#man-remove)

------------------------------------------------------------------------

## [22.3]{.header-section-number} `tmpfile()` {#man-tmpfile number="22.3"}

Create a temporary file

### Synopsis {#synopsis-137 .unnumbered .unlisted}

::: {#cb497 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

FILE *tmpfile(void);
```
:::

### Description {#description-137 .unnumbered .unlisted}


This is a nifty little function that will create and open a temporary file for you, and will return a `FILE*` to it that you can use. The file is opened with mode "`r+b`", so it's suitable for reading, writing, and binary data.

> 这是一个非常棒的小功能，它可以为您创建和打开一个临时文件，并返回一个`FILE*`，您可以使用它。该文件以“`r+b`”模式打开，因此适合读取，写入和二进制数据。


By using a little magic, the temp file is automatically deleted when it is `close()`'d or when your program exits. (Specifically, in Unix terms, `tmpfile()` [*unlinks*](https://man.archlinux.org/man/unlinkat.2.en#DESCRIPTION)[^46^](footnotes.html#fn46){#fnref46 .footnote-ref role="doc-noteref"} the file right after it opens it. This means that it's primed to be deleted from disk, but still exists because your process still has it open. As soon as your process exits, all open files are closed, and the temp file vanishes into the ether.)

> 使用一点魔法，当调用`close()`或程序退出时，临时文件会自动删除。（更具体地说，在Unix系统中，`tmpfile()`会在打开文件后立即[解除链接](https://man.archlinux.org/man/unlinkat.2.en#DESCRIPTION)。这意味着它已经准备好从磁盘中删除，但仍然存在，因为你的进程仍然打开着它。一旦你的进程退出，所有打开的文件都会关闭，临时文件就会消失。）

### Return Value {#return-value-135 .unnumbered .unlisted}

This function returns an open `FILE*` on success, or `NULL` on failure.

### Example {#example-138 .unnumbered .unlisted}

::: {#cb498 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *temp;
    char s[128];

    temp = tmpfile();

    fprintf(temp, "What is the frequency, Alexander?\n");

    rewind(temp); // back to the beginning

    fscanf(temp, "%s", s); // read it back out

    fclose(temp); // close (and magically delete)
}
```
:::

### See Also {#see-also-129 .unnumbered .unlisted}


[`fopen()`](stdio.html#man-fopen), [`fclose()`](stdio.html#man-fclose), [`tmpnam()`](stdio.html#man-tmpnam)

> [`fopen()`](stdio.html#man-fopen)：打开文件
[`fclose()`](stdio.html#man-fclose)：关闭文件
[`tmpnam()`](stdio.html#man-tmpnam)：生成临时文件名

------------------------------------------------------------------------

## [22.4]{.header-section-number} `tmpnam()` {#man-tmpnam number="22.4"}

Generate a unique name for a temporary file

### Synopsis {#synopsis-138 .unnumbered .unlisted}

::: {#cb499 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

char *tmpnam(char *s);
```
:::

### Description {#description-138 .unnumbered .unlisted}


This function takes a good hard look at the existing files on your system, and comes up with a unique name for a new file that is suitable for temporary file usage.

> 这个功能会仔细检查您系统中现有的文件，并为新文件找出一个适合用于临时文件使用的独特名称。


Let's say you have a program that needs to store off some data for a short time so you create a temporary file for the data, to be deleted when the program is done running. Now imagine that you called this file `foo.txt`. This is all well and good, except what if a user already has a file called `foo.txt` in the directory that you ran your program from? You'd overwrite their file, and they'd be unhappy and stalk you forever. And you wouldn't want that, now would you?

> 假设你有一个程序需要短暂存储一些数据，所以你为这些数据创建了一个临时文件，在程序运行完毕后会被删除。现在想象一下，你给这个文件取名叫`foo.txt`。这样做没有问题，但如果用户在你运行程序的目录中已经有一个叫`foo.txt`的文件呢？你会覆盖他们的文件，他们会不开心并且永远跟踪你。你不想这样，对吗？


Ok, so you get wise, and you decide to put the file in `/tmp` so that it won't overwrite any important content. But wait! What if some other user is running your program at the same time and they both want to use that filename? Or what if some other program has already created that file?

> 好的，所以你变得聪明，你决定把文件放在`/tmp`里，这样就不会覆盖任何重要内容。但是等等！如果另一个用户也在同时运行你的程序，他们都想使用那个文件名呢？或者，如果另一个程序已经创建了该文件呢？


See, all of these scary problems can be completely avoided if you just use `tmpnam()` to get a safe-ready-to-use filename.

> 看，如果你只使用`tmpnam()`来获取一个安全可用的文件名，所有这些可怕的问题都可以完全避免。


So how do you use it? There are two amazing ways. One, you can declare an array (or `malloc()` it---whatever) that is big enough to hold the temporary file name. How big is that? Fortunately there has been a macro defined for you, `L_tmpnam`, which is how big the array must be.

> 那么你怎么使用它呢？有两种令人惊叹的方法。一种是声明一个足够大的数组（或者`malloc()`它---随便）来容纳临时文件名。它有多大？幸运的是，已经为你定义了一个宏`L_tmpnam`，它指定了数组的大小。


And the second way: just pass `NULL` for the filename. `tmpnam()` will store the temporary name in a static array and return a pointer to that. Subsequent calls with a `NULL` argument will overwrite the static array, so be sure you're done using it before you call `tmpnam()` again.

> 第二种方法：将文件名传递为`NULL`。`tmpnam()`将把临时名称存储在一个静态数组中，并返回一个指向该数组的指针。将`NULL`作为参数的后续调用将覆盖静态数组，因此在再次调用`tmpnam()`之前，请确保您已经完成使用它。


Again, this function just makes a file name for you. It's up to you to later `fopen()` the file and use it.

> 再次，此功能只是为您创建一个文件名。之后由您自行使用`fopen()`打开文件。


One more note: some compilers warn against using `tmpnam()` since some systems have better functions (like the Unix function `mkstemp()`.) You might want to check your local documentation to see if there's a better option. Linux documentation goes so far as to say, "Never use this function. Use `mkstemp()` instead."

> 再提一句：一些编译器会警告不要使用`tmpnam()`，因为一些系统有更好的函数（比如Unix函数`mkstemp()`）。您可能需要检查您的本地文档，看看是否有更好的选择。Linux文档甚至进一步表示：“永远不要使用此函数。使用`mkstemp()`代替。”


I, however, am going to be a jerk and not talk about [`mkstemp()`](https://man.archlinux.org/man/mkstemp.3.en)[^47^](footnotes.html#fn47){#fnref47 .footnote-ref role="doc-noteref"} because it's not in the standard I'm writing about. Nyaah.

> 我不过是想做个混蛋，不谈论[`mkstemp()`](https://man.archlinux.org/man/mkstemp.3.en)[^47^](footnotes.html#fn47){#fnref47 .footnote-ref role="doc-noteref"}，因为它不在我正在写的标准里。嘤嘤嘤。


The macro `TMP_MAX` holds the number of unique filenames that can be generated by `tmpnam()`. Ironically, it is the *minimum* number of such filenames.

> `TMP_MAX` 宏保存了 `tmpnam()` 可以生成的唯一文件名的数量。讽刺的是，它是这类文件名的*最小*数量。

### Return Value {#return-value-136 .unnumbered .unlisted}


Returns a pointer to the temporary file name. This is either a pointer to the string you passed in, or a pointer to internal static storage if you passed in `NULL`. On error (like it can't find any temporary name that is unique), `tmpnam()` returns `NULL`.

> `tmpnam()`返回一个指向临时文件名的指针。如果你传入的是指针，它就是指向你传入的字符串；如果你传入的是`NULL`，它就是指向内部静态存储。如果无法找到唯一的临时名称，`tmpnam()`就会返回`NULL`。

### Example {#example-139 .unnumbered .unlisted}

::: {#cb500 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    char filename[L_tmpnam];
    char *another_filename;

    if (tmpnam(filename) != NULL)
        printf("We got a temp file name: \"%s\"\n", filename);
    else
        printf("Something went wrong, and we got nothing!\n");

    another_filename = tmpnam(NULL);

    printf("We got another temp file name: \"%s\"\n", another_filename);
    printf("And we didn't error check it because we're too lazy!\n");
}
```
:::

On my Linux system, this generates the following output:

    We got a temp file name: "/tmp/filew9PMuZ"
    We got another temp file name: "/tmp/fileOwrgPO"
    And we didn't error check it because we're too lazy!

### See Also {#see-also-130 .unnumbered .unlisted}

[`fopen()`](stdio.html#man-fopen), [`tmpfile()`](stdio.html#man-tmpfile)

------------------------------------------------------------------------

## [22.5]{.header-section-number} `fclose()` {#man-fclose number="22.5"}


The opposite of `fopen()`---closes a file when you're done with it so that it frees system resources

> `fopen()` 的反义词——在完成使用文件后关闭它，以释放系统资源。

### Synopsis {#synopsis-139 .unnumbered .unlisted}

::: {#cb502 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int fclose(FILE *stream);
```
:::

### Description {#description-139 .unnumbered .unlisted}


When you open a file, the system sets aside some resources to maintain information about that open file. Usually it can only open so many files at once. In any case, the Right Thing to do is to close your files when you're done using them so that the system resources are freed.

> 当你打开一个文件时，系统会把一些资源拿出来维护有关打开文件的信息。通常，它一次只能打开这么多文件。无论如何，正确的做法是在使用完文件后将其关闭，以便释放系统资源。


Also, you might not find that all the information that you've written to the file has actually been written to disk until the file is closed. (You can force this with a call to `fflush()`.)

> 此外，您可能会发现，在文件关闭之前，您写入文件的所有信息并不一定会被写入磁盘。（您可以通过调用`fflush（）`来强制执行此操作。）


When your program exits normally, it closes all open files for you. Lots of times, though, you'll have a long-running program, and it'd be better to close the files before then. In any case, not closing a file you've opened makes you look bad. So, remember to `fclose()` your file when you're done with it!

> 当你的程序正常退出时，它会为你关闭所有打开的文件。不过，很多时候，你会有一个长时间运行的程序，在那之前关闭文件会更好。无论如何，如果没有关闭你打开的文件，你看起来都不怎么样。所以，记住在你完成操作后使用`fclose()`关闭文件！

### Return Value {#return-value-137 .unnumbered .unlisted}


On success, `0` is returned. Typically no one checks for this. On error `EOF` is returned. Typically no one checks for this, either.

> 如果成功，会返回`0`，通常没有人会检查这个。如果出错，会返回`EOF`，通常也没有人会检查这个。

### Example {#example-140 .unnumbered .unlisted}

::: {#cb503 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *fp;

    fp = fopen("spoon.txt", "r");

    if (fp == NULL) {
        printf("Error opening file\n");
    } else {
        printf("Opened file just fine!\n");
        fclose(fp);  // All done!
    }
}
```
:::

### See Also {#see-also-131 .unnumbered .unlisted}

[`fopen()`](stdio.html#man-fopen)

------------------------------------------------------------------------

## [22.6]{.header-section-number} `fflush()` {#man-fflush number="22.6"}

Process all buffered I/O for a stream right now

### Synopsis {#synopsis-140 .unnumbered .unlisted}

::: {#cb504 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int fflush(FILE *stream);
```
:::

### Description {#description-140 .unnumbered .unlisted}


When you do standard I/O, as mentioned in the section on the [`setvbuf()`](stdio.html#man-setbuf) function, it is usually stored in a buffer until a line has been entered or the buffer is full or the file is closed. Sometimes, though, you really want the output to happen *right this second*, and not wait around in the buffer. You can force this to happen by calling `fflush()`.

> 当你使用标准I/O时，正如在[`setvbuf()`](stdio.html#man-setbuf)函数部分所提到的，它通常会存储在缓冲区中，直到输入一行或缓冲区已满或文件已关闭。有时，你真的希望输出立即发生，而不是等待在缓冲区中。你可以通过调用`fflush()`来强制实现这一点。


The advantage to buffering is that the OS doesn't need to hit the disk every time you call `fprintf()`. The disadvantage is that if you look at the file on the disk after the `fprintf()` call, it might not have actually been written to yet. ("I called `fputs()`, but the file is still zero bytes long! Why?!") In virtually all circumstances, the advantages of buffering outweigh the disadvantages; for those other circumstances, however, use `fflush()`.

> 缓冲的优势是操作系统不需要每次调用`fprintf()`时都访问磁盘。缺点是，如果在调用`fprintf()`之后查看磁盘上的文件，它可能尚未写入。（“我调用了`fputs()`，但文件仍然是零字节长！为什么？”）几乎所有情况下，缓冲的优势都大于缺点；对于其他情况，请使用`fflush()`。


Note that `fflush()` is only designed to work on output streams according to the spec. What will happen if you try it on an input stream? Use your spooky voice: *who knooooows!*

> 注意，根据规范，`fflush（）`只设计用于输出流。如果尝试在输入流上使用它会发生什么？用你那鬼魂般的声音说：*谁知道呢！*

### Return Value {#return-value-138 .unnumbered .unlisted}


On success, `fflush()` returns zero. If there's an error, it returns `EOF` and sets the error condition for the stream (see [`ferror()`](stdio.html#man-feof).)

> 如果成功，`fflush()`函数会返回零。如果发生错误，它会返回`EOF`并且为流设置错误状态（参见[`ferror()`](stdio.html#man-feof)）。

### Example {#example-141 .unnumbered .unlisted}


In this example, we're going to use the carriage return, which is `'\r'`. This is like newline (`'\n'`), except that it doesn't move to the next line. It just returns to the front of the current line.

> 在这个例子中，我们将使用回车，它是'\r'。这就像换行（'\n'），但它不会移动到下一行。它只是返回到当前行的开头。


What we're going to do is a little text-based status bar like so many command line programs implement. It'll do a countdown from 10 to 0 printing over itself on the same line.

> 我们要做的是一个像许多命令行程序实现的基于文本的状态栏。它将从10开始倒计时到0，在同一行上覆盖自身打印。


What is the catch and what does this have to do with `fflush()`? The catch is that the terminal is most likely "line buffered" (see the section on [`setvbuf()`](stdio.html#man-setbuf) for more info), meaning that it won't actually display anything until it prints a newline. But we're not printing newlines; we're just printing carriage returns, so we need a way to force the output to occur even though we're on the same line. Yes, it's `fflush()!`

> 抓住什么？这和`fflush()`有什么关系？抓住的是终端很可能是“行缓冲”（参见[`setvbuf()`](stdio.html#man-setbuf)部分以获取更多信息），这意味着它不会实际显示任何东西，直到它打印一个换行符。但是我们没有打印换行符；我们只是打印回车，所以我们需要一种方法来强制输出发生，即使我们在同一行。是的，它是`fflush()！`

::: {#cb505 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <threads.h>

void sleep_seconds(int s)
{
    thrd_sleep(&(struct timespec){.tv_sec=s}, NULL);
}

int main(void)
{
    int count;

    for(count = 10; count >= 0; count--) {
        printf("\rSeconds until launch: ");  // lead with a CR
        if (count > 0)
            printf("%2d", count);
        else
            printf("blastoff!\n");

        // force output now!!
        fflush(stdout);

        sleep_seconds(1);
    }
}
```
:::

### See Also {#see-also-132 .unnumbered .unlisted}

[`setbuf()`](stdio.html#man-setbuf), [`setvbuf()`](stdio.html#man-setbuf)

------------------------------------------------------------------------

## [22.7]{.header-section-number} `fopen()` {#man-fopen number="22.7"}

Opens a file for reading or writing

### Synopsis {#synopsis-141 .unnumbered .unlisted}

::: {#cb506 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

FILE *fopen(const char *path, const char *mode);
```
:::

### Description {#description-141 .unnumbered .unlisted}

The `fopen()` opens a file for reading or writing.


Parameter `path` can be a relative or fully-qualified path and file name to the file in question.

> 参数`path`可以是指向问题文件的相对路径或完全限定路径和文件名。


Parameter `mode` tells `fopen()` how to open the file (reading, writing, or both), and whether or not it's a binary file. Possible modes are:

> 参数`mode`告诉`fopen()`如何打开文件（读取、写入或同时进行），以及它是否是二进制文件。可能的模式有：


  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无论如何，我们都必须努力前行。
  Mode                                Description

  ----------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ----------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
简体中文：----------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

  `r`                                 Open the file for reading (read-only).

> 打开文件进行只读读取。


  `w`                                 Open the file for writing (write-only). The file is created if it doesn't exist.

> 打开文件进行写入（只写）。如果文件不存在，则会创建它。


  `r+`                                Open the file for reading and writing. The file has to already exist.

> 打开文件进行读写。文件必须已经存在。


  `w+`                                Open the file for writing and reading. The file is created if it doesn't already exist.

> 打开文件进行读写。如果文件不存在，则会创建文件。


  `a`                                 Open the file for append. This is just like opening a file for writing, but it positions the file pointer at the end of the file, so the next write appends to the end. The file is created if it doesn't exist.

> 打开文件以追加内容。这就像打开文件以进行写入，但它将文件指针定位在文件末尾，因此下一次写入将追加到末尾。如果文件不存在，则会创建文件。


  `a+`                                Open the file for reading and appending. The file is created if it doesn't exist.

> 打开文件进行读取和追加。如果文件不存在，则创建文件。

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无论如何，我们都必须努力。


Any of the modes can have the letter "`b`" appended to the end, as is "`wb`" ("write binary"), to signify that the file in question is a *binary* file. ("Binary" in this case generally means that the file contains non-alphanumeric characters that look like garbage to human eyes.) Many systems (like Unix) don't differentiate between binary and non-binary files, so the "`b`" is extraneous. But if your data is binary, it doesn't hurt to throw the "`b`" in there, and it might help someone who is trying to port your code to another system.

> 任何模式都可以在末尾添加字母“b”，就像“wb”（“写入二进制”）一样，以表明所涉及的文件是一个*二进制*文件。 （在这种情况下，“二进制”通常意味着文件包含对人类眼睛看起来像垃圾的非字母数字字符。）许多系统（如Unix）不区分二进制文件和非二进制文件，因此“b”是多余的。但是，如果您的数据是二进制的，将“b”放在那里并不会有害，并且可能有助于某人试图将您的代码移植到另一个系统。


The macro `FOPEN_MAX` tells you how many streams (at least) you can have open at once.

> `FOPEN_MAX`宏告诉你一次可以打开多少个流（至少）。


The macro `FILENAME_MAX` tells you what the longest valid filename can be. Don't go crazy, now.

> `FILENAME_MAX` 宏告诉你最长的有效文件名是多少。不要太疯狂了。

### Return Value {#return-value-139 .unnumbered .unlisted}

`fopen()` returns a `FILE*` that can be used in subsequent file-related calls.


If something goes wrong (e.g. you tried to open a file for read that didn't exist), `fopen()` will return `NULL`.

> 如果出现问题（例如，您试图打开一个不存在的文件进行读取），`fopen()` 将返回 `NULL`。

### Example {#example-142 .unnumbered .unlisted}

::: {#cb507 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *fp;

    fp = fopen("spoon.txt", "r");

    if (fp == NULL) {
        printf("Error opening file\n");
    } else {
        printf("Opened file just fine!\n");
        fclose(fp);  // All done!
    }
}
```
:::

### See Also {#see-also-133 .unnumbered .unlisted}


[`fclose()`](stdio.html#man-fclose), [`freopen()`](stdio.html#man-freopen)

> [`fclose()`](stdio.html#man-fclose)：关闭文件
[`freopen()`](stdio.html#man-freopen)：重新打开文件

------------------------------------------------------------------------

## [22.8]{.header-section-number} `freopen()` {#man-freopen number="22.8"}

Reopen an existing `FILE*`, associating it with a new path

### Synopsis {#synopsis-142 .unnumbered .unlisted}

::: {#cb508 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

FILE *freopen(const char *filename, const char *mode, FILE *stream);
```
:::

### Description {#description-142 .unnumbered .unlisted}


Let's say you have an existing `FILE*` stream that's already open, but you want it to suddenly use a different file than the one it's using. You can use `freopen()` to "re-open" the stream with a new file.

> 如果你有一个已经打开的`FILE*`流，但你想让它突然使用一个不同的文件，你可以使用`freopen()`来“重新打开”流，以使用一个新文件。


Why on Earth would you ever want to do that? Well, the most common reason would be if you had a program that normally would read from `stdin`, but instead you wanted it to read from a file. Instead of changing all your `scanf()`s to `fscanf()`s, you could simply reopen `stdin` on the file you wanted to read from.

> 为什么你会想要做这件事？最常见的原因是，如果你有一个程序通常从`stdin`读取，但你想让它从文件中读取。你可以不用把所有的`scanf()`改成`fscanf()`，而是简单地重新打开你想要读取的文件的`stdin`。


Another usage that is allowed on some systems is that you can pass `NULL` for `filename`, and specify a new `mode` for `stream`. So you could change a file from "`r+`" (read and write) to just "`r`" (read), for instance. It's implementation dependent which modes can be changed.

> 在某些系统中允许的另一种用法是，您可以为`filename`传递`NULL`，并为`stream`指定新的`mode`。因此，您可以将文件从“`r+`”（读写）更改为仅“`r`”（只读）。可以更改哪些模式取决于实现。


When you call `freopen()`, the old `stream` is closed. Otherwise, the function behaves just like the standard `fopen()`.

> 当你调用`freopen()`时，旧的流将被关闭。否则，该函数的行为就和标准的`fopen()`一样。

### Return Value {#return-value-140 .unnumbered .unlisted}

`freopen()` returns `stream` if all goes well.


If something goes wrong (e.g. you tried to open a file for read that didn't exist), `freopen()` will return `NULL`.

> 如果出现问题（例如尝试打开一个不存在的文件进行读取），`freopen()`将返回`NULL`。

### Example {#example-143 .unnumbered .unlisted}

::: {#cb509 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    int i, i2;

    scanf("%d", &i); // read i from stdin

    // now change stdin to refer to a file instead of the keyboard
    freopen("someints.txt", "r", stdin);

    scanf("%d", &i2); // now this reads from the file "someints.txt"

    printf("Hello, world!\n"); // print to the screen

    // change stdout to go to a file instead of the terminal:
    freopen("output.txt", "w", stdout);

    printf("This goes to the file \"output.txt\"\n");

    // this is allowed on some systems--you can change the mode of a file:
    freopen(NULL, "wb", stdout); // change to "wb" instead of "w"
}
```
:::

### See Also {#see-also-134 .unnumbered .unlisted}

[`fclose()`](stdio.html#man-fclose), [`fopen()`](stdio.html#man-fopen)

------------------------------------------------------------------------

## [22.9]{.header-section-number} `setbuf()`, `setvbuf()` {#man-setbuf number="22.9"}

Configure buffering for standard I/O operations

### Synopsis {#synopsis-143 .unnumbered .unlisted}

::: {#cb510 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

void setbuf(FILE *stream, char *buf);

int setvbuf(FILE *stream, char *buf, int mode, size_t size);
```
:::

### Description {#description-143 .unnumbered .unlisted}


Now brace yourself because this might come as a bit of a surprise to you: when you `printf()` or `fprintf()` or use any I/O functions like that, *it does not normally work immediately*. For the sake of efficiency, and to irritate you, the I/O on a `FILE*` stream is buffered away safely until certain conditions are met, and only then is the actual I/O performed. The functions `setbuf()` and `setvbuf()` allow you to change those conditions and the buffering behavior.

> 现在准备好，因为这可能会让你有点惊讶：当你使用`printf()`或`fprintf()`或类似的I/O函数时，*通常不会立即起作用*。为了效率，并且为了让你感到恼火，`FILE*`流上的I/O会被安全地缓冲起来，直到满足某些条件，然后才会执行实际的I/O操作。函数`setbuf()`和`setvbuf()`允许您更改这些条件和缓冲行为。


So what are the different buffering behaviors? The biggest is called "full buffering", wherein all I/O is stored in a big buffer until it is full, and then it is dumped out to disk (or whatever the file is). The next biggest is called "line buffering"; with line buffering, I/O is stored up a line at a time (until a newline (`'\n'`) character is encountered) and then that line is processed. Finally, we have "unbuffered", which means I/O is processed immediately with every standard I/O call.

> 有哪些不同的缓冲行为？最大的一种叫做“完全缓冲”，在这种情况下，所有的I/O都存储在一个大的缓冲区中，直到它满了，然后才被转储到磁盘（或者是文件）上。接下来最大的一种叫做“行缓冲”；使用行缓冲，I/O会一行一行地存储（直到遇到换行符（'\n'）），然后处理这一行。最后，我们有“无缓冲”，这意味着每次标准I/O调用都会立即处理I/O。


You might have seen and wondered why you could call `putchar()` time and time again and not see any output until you called `putchar('\n')`; that's right---`stdout` is line-buffered!

> 你可能已经看到了，并且想知道为什么你可以一次又一次地调用`putchar()`而不会看到任何输出，直到你调用`putchar('\n')`;没错---`stdout`是行缓冲的！


Since `setbuf()` is just a simplified version of `setvbuf()`, we'll talk about `setvbuf()` first.

> 由于`setbuf()`只是`setvbuf()`的简化版本，我们首先讨论`setvbuf()`。


The `stream` is the `FILE*` you wish to modify. The standard says you *must* make your call to `setvbuf()` *before* any I/O operation is performed on the stream, or else by then it might be too late.

> 流是您希望修改的`FILE*`。标准规定，您必须在对流进行任何I/O操作之前调用`setvbuf()`，否则可能为时已晚。


The next argument, `buf` allows you to make your own buffer space (using [`malloc()`](stdlib.html#man-malloc) or just a `char` array) to use for buffering. If you don't care to do this, just set `buf` to `NULL`.

> 下一个参数`buf`允许您创建自己的缓冲空间（使用[`malloc()`](stdlib.html#man-malloc)或仅使用`char`数组）来用于缓冲。如果您不想这样做，只需将`buf`设置为`NULL`。


Now we get to the real meat of the function: `mode` allows you to choose what kind of buffering you want to use on this `stream`. Set it to one of the following:

> 现在我们来到函数的真正要点：`mode`允许您选择要在此`stream`上使用的缓冲类型。将其设置为以下之一：

  Mode       Description
  ---------- ----------------------------------
  `_IOFBF`   `stream` will be fully buffered.
  `_IOLBF`   `stream` will be line buffered.
  `_IONBF`   `stream` will be unbuffered.


Finally, the `size` argument is the size of the array you passed in for `buf`...unless you passed `NULL` for `buf`, in which case it will resize the existing buffer to the size you specify.

> 最后，`size`参数是您为`buf`传入的数组的大小...除非您为`buf`传入`NULL`，在这种情况下，它将重新调整现有缓冲区的大小为您指定的大小。


Now what about this lesser function `setbuf()`? It's just like calling `setvbuf()` with some specific parameters, except `setbuf()` doesn't return a value. The following example shows the equivalency:

> 现在关于这个较小的函数'setbuf()'又怎么样？它就像调用'setvbuf()'，只是使用一些特定的参数，但'setbuf()'不会返回值。以下示例显示了等价性：

::: {#cb511 .sourceCode}
``` {.sourceCode .c}
// these are the same:
setbuf(stream, buf);
setvbuf(stream, buf, _IOFBF, BUFSIZ); // fully buffered

// and these are the same:
setbuf(stream, NULL);
setvbuf(stream, NULL, _IONBF, BUFSIZ); // unbuffered
```
:::

### Return Value {#return-value-141 .unnumbered .unlisted}

`setvbuf()` returns zero on success, and nonzero on failure. `setbuf()` has no return value.

### Example {#example-144 .unnumbered .unlisted}

::: {#cb512 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char lineBuf[1024];

    fp = fopen("somefile.txt", "w");
    setvbuf(fp, lineBuf, _IOLBF, 1024);  // set to line buffering
    fprintf(fp, "You won't see this in the file yet. ");
    fprintf(fp, "But now you will because of this newline.\n");
    fclose(fp);

    fp = fopen("anotherfile.txt", "w");
    setbuf(fp, NULL); // set to unbuffered
    fprintf(fp, "You will see this in the file now.");
    fclose(fp);
}
```
:::

### See Also {#see-also-135 .unnumbered .unlisted}

[`fflush()`](stdio.html#man-fflush)

------------------------------------------------------------------------

## [22.10]{.header-section-number} `printf()`, `fprintf()`, `sprintf()`, `snprintf()` {#man-printf number="22.10"}

Print a formatted string to the console or to a file

### Synopsis {#synopsis-144 .unnumbered .unlisted}

::: {#cb513 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int printf(const char *format, ...);

int fprintf(FILE *stream, const char *format, ...);

int sprintf(char * restrict s, const char * restrict format, ...);

int snprintf(char * restrict s, size_t n, const char * restrict format, ...);
```
:::

### Description {#description-144 .unnumbered .unlisted}

These functions print formatted output to a variety of destinations.

  Function       Output Destination
  -------------- --------------------------------------------------
  `printf()`     Print to console (screen by default, typically).
  `fprintf()`    Print to a file.
  `sprintf()`    Print to a string.
  `snprintf()`   Print to a string (safely).


The only differences between these is are the leading parameters that you pass to them before the `format` string.

> 这些唯一的区别就是在`format`字符串之前传递给它们的领先参数。

  Function       What you pass before `format`
  -------------- -----------------------------------------------------------
  `printf()`     Nothing comes before `format`.
  `fprintf()`    Pass a `FILE*`.
  `sprintf()`    Pass a `char*` to a buffer to print into.

  `snprintf()`   Pass a `char*` to the buffer and a maximum buffer length.

> `snprintf()` 向缓冲区传递一个`char*`和最大缓冲区长度。


The `printf()` function is legendary as being one of the most flexible outputting systems ever devised. It can also get a bit freaky here or there, most notably in the `format` string. We'll take it a step at a time here.

> `printf()` 函数以其最灵活的输出系统而闻名，它在`格式`字符串中也可能有一些奇怪的表现。我们将一步一步地来看它。


The easiest way to look at the format string is that it will print everything in the string as-is, *unless* a character has a percent sign (`%`) in front of it. That's when the magic happens: the next argument in the `printf()` argument list is printed in the way described by the percent code. These percent codes are called *format specifiers*.

> 最简单的看格式字符串的方法是，除非字符前面有百分号（`%`），否则它将把字符串中的所有内容都原样打印出来。这就是魔法发生的地方：`printf（）`参数列表中的下一个参数按照百分比代码描述的方式打印出来。这些百分比代码称为*格式说明符*。

Here are the most common format specifiers.


  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告
   Specifier  Description

  ----------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ----------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
没有翻译内容
     `%d`     Print the next argument as a signed decimal number, like `3490`. The argument printed this way should be an `int`, or something that gets promoted to `int`.

     `%f`     Print the next argument as a signed floating point number, like `3.14159`. The argument printed this way should be a `double`, or something that gets promoted to a `double`.

     `%c`     Print the next argument as a character, like `'B'`. The argument printed this way should be a `char` variant.

     `%s`     Print the next argument as a string, like `"Did you remember your mittens?"`. The argument printed this way should be a `char*` or `char[]`.

     `%%`     No arguments are converted, and a plain old run-of-the-mill percent sign is printed. This is how you print a '%' using `printf()`.

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告


So those are the basics. I'll give you some more of the format specifiers in a bit, but let's get some more breadth before then. There's actually a lot more that you can specify in there after the percent sign.

> 这就是基础。我会稍后给你提供更多的格式规范，但在此之前，让我们先拓宽一下视野。实际上，在百分号之后，你可以指定更多内容。


For one thing, you can put a field width in there---this is a number that tells `printf()` how many spaces to put on one side or the other of the value you're printing. That helps you line things up in nice columns. If the number is negative, the result becomes left-justified instead of right-justified. Example:

> 你可以在里面放置一个字段宽度---这是一个数字，告诉`printf()`在要打印的值的一边或另一边要放置多少空格。这有助于你将事物排列成漂亮的列。如果数字是负数，结果将变成左对齐而不是右对齐。例子：

::: {#cb514 .sourceCode}
``` {.sourceCode .c}
printf("%10d", x);  /* prints X on the right side of the 10-space field */
printf("%-10d", x); /* prints X on the left side of the 10-space field */
```
:::


If you don't know the field width in advance, you can use a little kung-foo to get it from the argument list just before the argument itself. Do this by placing your seat and tray tables in the fully upright position. The seatbelt is fastened by placing the---**cough**. I seem to have been doing way too much flying lately. Ignoring that useless fact completely, you can specify a dynamic field width by putting a `*` in for the width. If you are not willing or able to perform this task, please notify a flight attendant and we will reseat you.

> 如果您事先不知道字段宽度，您可以使用一点功夫从参数列表中获取它，就在参数本身之前。要做到这一点，请将您的座位和托盘桌放置在完全直立的位置。安全带是通过放置---**咳嗽**来系上的。我似乎最近飞行太多了。完全忽略这个无用的事实，您可以通过在宽度处放置一个`*`来指定动态字段宽度。如果您不愿意或不能执行此任务，请通知乘务员，我们将为您重新安排座位。

::: {#cb515 .sourceCode}
``` {.sourceCode .c}
int width = 12;
int value = 3490;

printf("%*d\n", width, value);
```
:::


You can also put a "0" in front of the number if you want it to be padded with zeros:

> 你也可以在数字前面加上一个"0"，如果你想用零来填充的话：

::: {#cb516 .sourceCode}
``` {.sourceCode .c}
int x = 17;
printf("%05d", x);  /* "00017" */
```
:::


When it comes to floating point, you can also specify how many decimal places to print by making a field width of the form "`x.y`" where `x` is the field width (you can leave this off if you want it to be just wide enough) and `y` is the number of digits past the decimal point to print:

> 当涉及到浮点数时，您还可以通过制作形式为“x.y”的字段宽度来指定要打印的小数位数，其中x是字段宽度（如果您希望它足够宽，则可以省略），y是小数点后要打印的位数：

::: {#cb517 .sourceCode}
``` {.sourceCode .c}
float f = 3.1415926535;

printf("%.2f", f);  /* "3.14" */
printf("%7.3f", f); /* "  3.141" <-- 7 spaces across */
```
:::


Ok, those above are definitely the most common uses of `printf()`, but let's get *total coverage*.

> 好的，上面绝对是`printf()`最常见的用法，但让我们达到*完全覆盖*。

#### [22.10.0.1]{.header-section-number} Format Specifier Layout {#format-specifier-layout number="22.10.0.1"}


Technically, the layout of the format specifier is these things in this order:

> 技术上，格式说明符的布局是按照这些顺序排列的：

1.  `%`, followed by...
2.  Optional: zero or more flags, left justify, leading zeros, etc.
3.  Optional: Field width, how wide the output field should be.
4.  Optional: Precision, or how many decimal places to print.

5.  Optional: Length modifier, for printing things bigger than `int` or `double`.

> 可选：长度修饰符，用于打印大于`int`或`double`的东西。
6.  Conversion specifier, like `d`, `f`, etc.

In short, the whole format specifier is laid out like this:

    %[flags][fieldwidth][.precision][lengthmodifier]conversionspecifier

What could be easier?

#### [22.10.0.2]{.header-section-number} Conversion Specifiers {#conversion-specifiers number="22.10.0.2"}


Let's talk conversion specifiers first. Each of the following specifies what type it can print, but it can also print anything that gets promoted to that type. For example, `%d` can print `int`, `short`, and `char`.

> 让我们先谈谈转换说明符。每个以下说明符都指定了它可以打印的类型，但它也可以打印任何被提升到该类型的内容。例如，`％d`可以打印`int`，`short`和`char`。


  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。
   Conversion Specifier  Description

  ---------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ---------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
空白
           `d`           Print an `int` argument as a decimal number.

           `i`           Identical to `d`.

           `o`           Print an `unsigned int` in octal (base 8).

           `u`           Print an `unsigned int` in decimal.

           `x`           Print an `unsigned int` in hexadecimal with lowercase letters.

           `X`           Print an `unsigned int` in hexadecimal with uppercase letters.

           `f`           Print a `double` in decimal notation. Infinity is printed as `infinity` or `inf`, and NaN is printed as `nan`, any of which could have a leading minus sign.

           `F`           Same as `f`, except it prints out `INFINITY`, `INF`, or `NAN` in all caps.

           `e`           Print a number in scientific notation, e.g. `1.234e56`. Does infinity and NaN like `f`.

           `E`           Just like `e`, except prints the exponent `E` (and infinity and NaN) in uppercase.

           `g`           Print small numbers like `f` and large numbers like `e`. See note below.

           `G`           Print small numbers like `F` and large numbers like `E`. See note below.

           `a`           Print a `double` in hexadecimal form `0xh.hhhhpd` where `h` is a lowercase hex digit and `d` is a decimal exponent of 2. Infinity and NaN in the form of `f`. More below.

           `A`           Like `a` except everything's uppercase.

           `c`           Convert `int` argument to `unsigned char` and print as a character.

           `s`           Print a string starting at the given `char*`.

           `p`           Print a `void*` out as a number, probably the numeric address, possibly in hex.

           `n`           Store the number of characters written so far in the given `int*`. Doesn't print anything. See below.

           `%`           Print a literal percent sign.

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无论如何，我们都会努力。

##### [22.10.0.2.1]{.header-section-number} Note on `%a` and `%A` {#note-on-a-and-a number="22.10.0.2.1"}


When printing floating point numbers in hex form, there is one number before the decimal point, and the rest of are out to the precision.

> 当以十六进制形式打印浮点数时，小数点前有一个数字，其余的数字精确到小数点后。

::: {#cb519 .sourceCode}
``` {.sourceCode .c}
double pi = 3.14159265358979;

printf("%.3a\n", pi);  // 0x1.922p+1
```
:::


C can choose the leading number in such a way to ensure subsequent digits align to 4-bit boundaries.

> C 可以选择首位数字，以确保后续数字与 4 位边界对齐。


If the precision is left out and the macro `FLT_RADIX` is a power of 2, enough precision is used to represent the number exactly. If `FLT_RADIX` is not a power of two, enough precision is used to be able to tell any two floating values apart.

> 如果没有指定精度，而且宏`FLT_RADIX`是2的幂，那么使用足够的精度就可以精确表示数字。如果`FLT_RADIX`不是2的幂，那么使用足够的精度就可以区分任何两个浮点值。


If the precision is `0` and the `#` flag isn't specified, the decimal point is omitted.

> 如果精度为0且未指定#标志，则省略小数点。

##### [22.10.0.2.2]{.header-section-number} Note on `%g` and `%G` {#note-on-g-and-g number="22.10.0.2.2"}


The gist of this is to use scientific notation when the number gets too "extreme", and regular decimal notation otherwise.

> 这个要点是，当数字变得太“极端”时使用科学记数法，否则使用常规小数记数法。


The exact behavior for whether these print as `%f` or `%e` depends on a number of factors:

> 表示为`%f`还是`%e`的确切行为取决于多种因素。


If the number's exponent is greater than or equal to -4 **and** the precision is greater than the exponent, we use `%f`. In this case, the precision is converted according to [\\(p=p-(x+1)\\)]{.math .inline}, where [\\(p\\)]{.math .inline} is the specified precision and [\\(x\\)]{.math .inline} is the exponent.

> 如果数字的指数大于或等于-4且精度大于指数，我们使用`%f`。在这种情况下，精度将按照[\\(p=p-(x+1)\\)]{.math .inline}转换，其中[\\(p\\)]{.math .inline}是指定的精度，[\\(x\\)]{.math .inline}是指数。


Otherwise we use `%e`, and the precision becomes [\\(p-1\\)]{.math .inline}.

> 否则，我们使用`％e`，精度变成[\（p-1\）]{.math .inline}。


Trailing zeros in the decimal portion are removed. And if there are none left, the decimal point is removed, too. All this unless the `#` flag is specified.

> 小数部分的尾随零会被去除。如果没有剩余的零，小数点也会被去除。除非指定了“#”标志，否则都会这样处理。

##### [22.10.0.2.3]{.header-section-number} Note on `%n` {#note-on-n number="22.10.0.2.3"}


This specifier is cool and different, and rarely needed. It doesn't actually print anything, but stores the number of characters printed so far in the next pointer argument in the list.

> 这个指定符很酷而且不同，很少需要使用。它实际上不会打印任何东西，而是将到目前为止打印的字符数存储在列表中的下一个指针参数中。

::: {#cb520 .sourceCode}
``` {.sourceCode .c}
int numChars;
float a = 3.14159;
int b = 3490;

printf("%f %d%n\n", a, b, &numChars);
printf("The above line contains %d characters.\n", numChars);
```
:::


The above example will print out the values of `a` and `b`, and then store the number of characters printed so far into the variable `numChars`. The next call to `printf()` prints out that result.

> 上面的例子会打印出`a`和`b`的值，然后将打印出的字符数存储在变量`numChars`中。下一次调用`printf()`会打印出这个结果。

::: {#cb521 .sourceCode}
``` {.sourceCode .default}
3.141590 3490
The above line contains 13 characters
```
:::

#### [22.10.0.3]{.header-section-number} Length Modifiers {#length-modifiers number="22.10.0.3"}


You can stick a *length* modifier in front of each of the conversion specifiers, if you want. most of those format specifiers work on `int` or `double` types, but what if you want larger or smaller types? That's what these are good for.

> 你可以在每个转换说明符前面添加一个*长度*修饰符，如果你想的话。大多数格式说明符适用于`int`或`double`类型，但如果你想要更大或更小的类型呢？这些就是它们的用处。

你可以在每个转换说明符前面加上一个*长度*修饰符，如果你想的话。大多数格式说明符适用于`int`或`double`类型，但如果你想要更大或更小的类型呢？这些就是它们的用武之地。

For example, you could print out a long long int with the `ll` modifier:

::: {#cb522 .sourceCode}
``` {.sourceCode .c}
long long int x = 3490;

printf("%lld\n", x);  // 3490
```
:::


  -------------------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告
   Length Modifier            Conversion Specifier           Description

  ----------------- ---------------------------------------- --------------------------------------------------------------------------------------

> ----------------- ---------------------------------------- --------------------------------------------------------------------------------------
无
        `hh`              `d`, `i`, `o`, `u`, `x`, `X`       Convert argument to `char` (signed or unsigned as appropriate) before printing.

         `h`              `d`, `i`, `o`, `u`, `x`, `X`       Convert argument to `short int` (signed or unsigned as appropriate) before printing.

         `l`              `d`, `i`, `o`, `u`, `x`, `X`       Argument is a `long int` (signed or unsigned as appropriate).

        `ll`              `d`, `i`, `o`, `u`, `x`, `X`       Argument is a `long long int` (signed or unsigned as appropriate).

         `j`              `d`, `i`, `o`, `u`, `x`, `X`       Argument is a `intmax_t` or `uintmax_t` (as appropriate).

         `z`              `d`, `i`, `o`, `u`, `x`, `X`       Argument is a `size_t`.

         `t`              `d`, `i`, `o`, `u`, `x`, `X`       Argument is a `ptrdiff_t`.

         `L`         `a`, `A`, `e`, `E`, `f`, `F`, `g`, `G`  Argument is a `long double`.

         `l`                          `c`                    Argument is in a `wint_t`, a wide character.

         `l`                          `s`                    Argument is in a `wchar_t*`, a wide character string.

        `hh`                          `n`                    Store result in `signed char*` argument.

         `h`                          `n`                    Store result in `short int*` argument.

         `l`                          `n`                    Store result in `long int*` argument.

        `ll`                          `n`                    Store result in `long long int*` argument.

         `j`                          `n`                    Store result in `intmax_t*` argument.

         `z`                          `n`                    Store result in `size_t*` argument.

         `t`                          `n`                    Store result in `ptrdiff_t*` argument.

  -------------------------------------------------------------------------------------------------------------------------------------------------

> -------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告

#### [22.10.0.4]{.header-section-number} Precision {#precision number="22.10.0.4"}


In front of the length modifier, you can put a precision, which generally means how many decimal places you want on your floating point numbers.

> 在长度修饰符之前，您可以指定一个精度，通常意味着您希望浮点数的小数位数。


To do this, you put a decimal point (`.`) and the decimal places afterward.

> 要做到这一点，你需要放置一个小数点（`.`），然后是小数位。

For example, we could print π rounded to two decimal places like this:

::: {#cb523 .sourceCode}
``` {.sourceCode .c}
double pi = 3.14159265358979;

printf("%.2f\n", pi);  // 3.14
```
:::


  ---------------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------------
简化中文
       Conversion Specifier      Precision Value Meaning

  ------------------------------ --------------------------------------------------------------------------------

> ------------------------------ --------------------------------------------------------------------------------
简体中文：
------------------------------ --------------------------------------------------------------------------------

   `d`, `i`, `o`, `u`, `x`, `X`  For integer types, minimum number of digits (will pad with leading zeros)

> 对于整数类型，最少位数（将用前导零填充）：d、i、o、u、x、X


   `a`, `e`, `f`, `A`, `E`, `F`  For floating types, the precision is the number of digits past the decimal.

> 对于浮点类型，精度是小数点后的位数。

             `g`, `G`            For floating types, the precision is the number of significant digits printed.

               `s`               The maximum number of bytes (not multibyte characters!) to be written.

  ---------------------------------------------------------------------------------------------------------------

> ---------------------------------------------------------------------------------------------------------------
无论如何，我们都要努力。


If no number is specified in the precision after the decimal point, the precision is zero.

> 如果小数点后没有指定精度，则精度为零。


If an `*` is specified after the decimal, something amazing happens! It means the `int` argument to `printf()` before the number to be printed holds the precision. You can use this if you don't know the precision at compile time.

> 如果在小数后面指定一个`*`，就会发生一些神奇的事情！这意味着`printf（）`之前的`int`参数保存了精度。如果你在编译时不知道精度，可以使用它。

::: {#cb524 .sourceCode}
``` {.sourceCode .c}
int precision;
double pi = 3.14159265358979;

printf("Enter precision: "); fflush(stdout);
scanf("%d", &precision);

printf("%.*f\n", precision, pi);
```
:::

Which gives:

::: {#cb525 .sourceCode}
``` {.sourceCode .default}
Enter precision: 4
3.1416
```
:::

#### [22.10.0.5]{.header-section-number} Field Width {#field-width number="22.10.0.5"}


In front of the optional precision, you can indicate a field width. This is a decimal number that indicates how wide the region should be in which the argument is printed. The region is padding with leading (or trailing) spaces to make sure it's wide enough.

> 在可选精度之前，您可以指定一个字段宽度。这是一个十进制数，指示应该有多宽的区域来打印参数。该区域使用前导（或尾随）空格填充，以确保它足够宽。


If the field width specified is too small to hold the output, it is ignored.

> 如果指定的字段宽度太小而无法容纳输出，则会被忽略。


As a preview, you can give a negative field width to justify the item the other direction.

> 作为预览，您可以给出负的字段宽度以使项目向另一个方向对齐。


So let's print a number in a field of width 10. We'll put some angle brackets around it so we can see the padding spaces in the output.

> 让我们在一个宽度为10的字段中打印一个数字。 我们会在它周围放一些角括号，这样我们就可以看到输出中的填充空格。

::: {#cb526 .sourceCode}
``` {.sourceCode .c}
printf("<<%10d>>\n", 3490);   // right justified
printf("<<%-10d>>\n", 3490);  // left justified
```
:::

::: {#cb527 .sourceCode}
``` {.sourceCode .default}
<<      3490>>
<<3490      >>
```
:::

Like with the precision, you can use an asterisk (`*`) as the field width

::: {#cb528 .sourceCode}
``` {.sourceCode .c}
int field_width;
int val = 3490;

printf("Enter field_width: "); fflush(stdout);
scanf("%d", &field_width);

printf("<<%*d>>\n", field_width, val);
```
:::

#### [22.10.0.6]{.header-section-number} Flags {#flags number="22.10.0.6"}


Before the field width, you can put some optional flags that further control the output of the subsequent fields. We just saw that the `-` flag can be used to left- or right-justify fields. But there are plenty more!

> 在字段宽度之前，您可以放置一些可选标志，以进一步控制随后字段的输出。我们刚刚看到，`-`标志可用于左对齐或右对齐字段。但是还有很多！

  ------------------------------------------------------------------------------------------
     Flag     Description
  ----------- ------------------------------------------------------------------------------
      `-`     For a field width, left justify in the field (right is default).

      `+`     If the number is signed, always prefix a `+` or `-` on the front.


   \[SPACE\]  If the number is signed, prefix a space for positive, or a `-` for negative.

> 如果数字有符号，正数前面加一个空格，负数前面加一个“-”号。

      `0`     Pad the right-justified field with leading zeros instead of leading spaces.

      `#`     Print using an alternate form. See below.
  ------------------------------------------------------------------------------------------


For example, we could pad a hexadecimal number with leading zeros to a field width of 8 with:

> 例如，我们可以使用前导零将十六进制数填充到8位宽度：

::: {#cb529 .sourceCode}
``` {.sourceCode .c}
printf("%08x\n", 0x1234);  // 00001234
```
:::

The `#` "alternate form" result depends on the conversion specifier.


  ------------------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------------------
简化中文
   Conversion Specifier  Alternate Form (`#`) Meaning

  ---------------------- -------------------------------------------------------------------------------------------------

> ---------------------- -------------------------------------------------------------------------------------------------
无
           `o`           Increase precision of a non-zero number just enough to get one leading `0` on the octal number.

           `x`           Prefix a non-zero number with `0x`.

           `X`           Same as `x`, except capital `0X`.

      `a`, `e`, `f`      Always print a decimal point, even if nothing follows it.

      `A`, `E`, `F`      Identical to `a`, `e`, `f`.

         `g`, `G`        Always print a decimal point, even if nothing follows it, and keep trailing zeros.

  ------------------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------------------
简化中文

#### [22.10.0.7]{.header-section-number} `sprintf()` and `snprintf()` Details {#sprintf-and-snprintf-details number="22.10.0.7"}


Both `sprintf()` and `snprintf()` have the quality that if you pass in `NULL` as the buffer, nothing is written---but you can still check the return value to see how many characters *would* have been written.

> 两个函数`sprintf()`和`snprintf()`都有一个特性，如果你传入`NULL`作为缓冲区，则不会写入任何内容，但你仍然可以检查返回值，以查看有多少字符*将*被写入。

`snprintf()` **always** terminates the string with a `NUL` character. So if you try to write out more than the maximum specified characters, the universe ends.


Just kidding. If you do, `snprintf()` will write [\\(n-1\\)]{.math .inline} characters so that it has enough room to write the terminator at the end.

> 只是开玩笑。如果你这样做，`snprintf()` 将写入[\\(n-1\\)]{.math .inline}个字符，以便有足够的空间在末尾写入终止符。

### Return Value {#return-value-142 .unnumbered .unlisted}


Returns the number of characters outputted, or a negative number on error.

> 返回输出的字符数，如果出错则返回负数。

### Example {#example-145 .unnumbered .unlisted}

::: {#cb530 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    int a = 100;
    float b = 2.717;
    char *c = "beej!";
    char d = 'X';
    int e = 5;

    printf("%d\n", a); /* "100"      */
    printf("%f\n", b); /* "2.717000" */
    printf("%s\n", c); /* "beej!"    */
    printf("%c\n", d); /* "X"        */
    printf("110%%\n"); /* "110%"     */

    printf("%10d\n", a);   /* "       100" */
    printf("%-10d\n", a);  /* "100       " */
    printf("%*d\n", e, a); /* "  100"      */
    printf("%.2f\n", b);   /* "2.72"       */

    printf("%hhd\n", d); /* "88" <-- ASCII code for 'X' */

    printf("%5d %5.2f %c\n", a, b, d); /* "  100  2.72 X" */
}
```
:::

### See Also {#see-also-136 .unnumbered .unlisted}


[`sprintf()`](stdio.html#man-printf), [`vprintf()`](stdio.html#man-vprintf)

> sprintf()，vprintf()

------------------------------------------------------------------------

## [22.11]{.header-section-number} `scanf()`, `fscanf()`, `sscanf()` {#man-scanf number="22.11"}


Read formatted string, character, or numeric data from the console or from a file

> 从控制台或文件中读取格式化的字符串、字符或数字数据

### Synopsis {#synopsis-145 .unnumbered .unlisted}

::: {#cb531 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int scanf(const char *format, ...);

int fscanf(FILE *stream, const char *format, ...);

int sscanf(const char * restrict s, const char * restrict format, ...);
```
:::

### Description {#description-145 .unnumbered .unlisted}

These functions read formatted output from a variety of sources.

  Function     Input Source
  ------------ ---------------------------------------------------------
  `scanf()`    Read from the console (keyboard by default, typically).
  `fscanf()`   Read from a file.
  `sscanf()`   Read from a string.


The only differences between these is are the leading parameters that you pass to them before the `format` string.

> 这些之间唯一的区别就是在`format`字符串之前传递给它们的领先参数。

  Function     What you pass before `format`
  ------------ ------------------------------------------
  `scanf()`    Nothing comes before `format`.
  `fscanf()`   Pass a `FILE*`.
  `sscanf()`   Pass a `char*` to a buffer to read from.


The `scanf()` family of functions reads data from the console or from a `FILE` stream, parses it, and stores the results away in variables you provide in the argument list.

> `scanf()`系列函数从控制台或`FILE`流中读取数据，对其进行解析，并将结果存储在参数列表中提供的变量中。


The format string is very similar to that in `printf()` in that you can tell it to read a `"%d"`, for instance for an `int`. But it also has additional capabilities, most notably that it can eat up other characters in the input that you specify in the format string.

> 格式字符串与`printf()`非常相似，比如你可以指定一个`"%d"`来读取一个`int`。但它还有其他的能力，最显著的是它可以消耗掉输入中你在格式字符串中指定的其他字符。


But let's start simple, and look at the most basic usage first before plunging into the depths of the function. We'll start by reading an `int` from the keyboard:

> 让我们先简单点，先看最基本的用法，然后再深入研究函数。我们先从键盘读取一个`int`开始：

::: {#cb532 .sourceCode}
``` {.sourceCode .c}
int a;

scanf("%d", &a);
```
:::

`scanf()` obviously needs a pointer to the variable if it is going to change the variable itself, so we use the address-of operator to get the pointer.


In this case, `scanf()` walks down the format string, finds a "`%d`", and then knows it needs to read an integer and store it in the next variable in the argument list, `a`.

> 在这种情况下，`scanf()`会遍历格式字符串，找到一个"`%d`"，然后知道需要读取一个整数并将其存储在参数列表中的下一个变量`a`中。


Here are some of the other format specifiers you can put in the format string:

> 这里有一些其他的格式说明符，你可以放入格式字符串中：


  ------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------
简体中文
  Format Specifier                    Description

  ----------------------------------- ------------------------------------------------------------------------

> ----------------------------------- ------------------------------------------------------------------------
简体中文：
----------------------------------- ------------------------------------------------------------------------

  `%d`                                Reads an integer to be stored in an `int`. This integer can be signed.

> `%d` 读取一个整数，存储在`int`中。这个整数可以带符号。


  `%u`                                Reads an integer to be stored in an `unsigned int`.

> 读取一个整数存储在一个无符号整型中。


  `%f`                                Reads a floating point number, to be stored in a `float`.

> 读取一个浮点数，存储在一个`float`中。


  `%s`                                Reads a string up to the first whitespace character.

> 读取字符串直到遇到第一个空白字符。

  `%c`                                Reads a `char`.

  ------------------------------------------------------------------------------------------------------------

> ------------------------------------------------------------------------------------------------------------
简体中文

And that's the end of the story!


Ha! Just kidding. If you've just arrived from the `printf()` page, you know there's a near-infinite amount of additional material.

> 哈！只是开玩笑。如果你刚从`printf()`页面到来，你就知道还有几乎无限多的附加材料。

#### [22.11.0.1]{.header-section-number} Consuming Other Characters {#consuming-other-characters number="22.11.0.1"}

`scanf()` will move along the format string matching any characters you include.

For example, you could read a hyphenated date like so:

::: {#cb533 .sourceCode}
``` {.sourceCode .c}
scanf("%u-%u-%u", &yyyy, &mm, &dd);
```
:::


In that case, `scanf()` will attempt to consume an unsigned decimal number, then a hyphen, then another unsigned number, then another hypen, then another unsigned number.

> 在这种情况下，`scanf（）`将尝试消耗一个无符号十进制数，然后是一个连字符，然后是另一个无符号数，然后是另一个连字符，然后是另一个无符号数。


If it fails to match at any point (e.g. the user entered "foo"), `scanf()` will bail without consuming the offending characters.

> 如果在任何一点上无法匹配（例如用户输入“foo”），`scanf()`将不会消耗有害字符而退出。


And it will return the number of variables successfully converted. In the example above, if the user entered a valid string, `scanf()` would return `3`, one for each variable successfully read.

> 如果用户输入了有效的字符串，`scanf()`将返回`3`，每个变量成功读取一个。

#### [22.11.0.2]{.header-section-number} Problems with `scanf()` {#problems-with-scanf number="22.11.0.2"}


I (and the C FAQ and a lot of people) recommend *against* using `scanf()` to read directly from the keyboard. It's too easy for it to stop consuming characters when the user enters some bad data.

> 我（以及C FAQ和许多人）建议不要使用`scanf()`直接从键盘读取数据。当用户输入错误数据时，它很容易停止消费字符。


If you have data in a file and you're confident it's in good shape, `fscanf()` can be really useful.

> 如果你的文件中有数据，而且你确信它的格式很好，那么`fscanf()`就会非常有用。


But in the case of the keyboard or file, you can always use `fgets()` to read a complete line into a buffer, and then use `sscanf()` to scan things out of the buffer. This gives you the best of both worlds.

> 在键盘或文件的情况下，你可以使用`fgets()`将一整行读取到缓冲区中，然后使用`sscanf()`从缓冲区中提取出东西。这样你就可以兼得两全。

#### [22.11.0.3]{.header-section-number} Problems with `sscanf()` {#problems-with-sscanf number="22.11.0.3"}


A while back, a third-party programmer rose to fame for figuring out [how to cut *GTA Online* load times by 70%](https://nee.lv/2021/02/28/How-I-cut-GTA-Online-loading-times-by-70/)[^48^](footnotes.html#fn48){#fnref48 .footnote-ref role="doc-noteref"}.

> 不久前，一位第三方程序员因弄清楚[如何将*GTA Online*加载时间减少70％](https://nee.lv/2021/02/28/How-I-cut-GTA-Online-loading-times-by-70/)[^48^](footnotes.html#fn48){#fnref48 .footnote-ref role="doc-noteref"}而声名鹊起。


What they'd discovered was that the implementation of `sscanf()` first effectively calls `strlen()`... so even if you're just using `sscanf()` to peel the first few characters off the string, it still runs all the way out to the end of the string first.

> 他们发现，实现`sscanf()`首先有效地调用`strlen()`...因此，即使您只使用`sscanf()`来剥离字符串的前几个字符，它仍然会首先运行到字符串的末尾。


On small strings, no big deal, but on large strings with repeated calls (which is what was happening in *GTA*) it got *sloooooooooowwwww*...

> 在小字符串上没什么大不了的，但是在大字符串上，重复调用（就像GTA中发生的那样）就会变得*非常慢*...


So if you're just converting a string to a number, consider [`atoi()`](stdlib.html#man-atoi), [`atof()`](stdlib.html#man-atof), or the [`strtol()`](stdlib.html#man-strtol) and [`strtod()`](stdlib.html#man-strtod) families of functions, instead.

> 如果你只是要把一个字符串转换成数字，可以考虑使用atoi()、atof()或strtol()和strtod()系列函数。


(The programmer [collected a \$10,000 bug bounty](https://www.polygon.com/2021/3/16/22334214/gta-online-loading-times-t0st-update-bug-bounty) for the effort.)

> 程序员因为这项努力获得了1万美元的错误赏金（参见https://www.polygon.com/2021/3/16/22334214/gta-online-loading-times-t0st-update-bug-bounty）。

#### [22.11.0.4]{.header-section-number} The Deep Details {#the-deep-details number="22.11.0.4"}

Let's check out what a `scanf()`


And here are some more codes, except these don't tend to be used as often. You, of course, may use them as often as you wish!

> 这里还有一些代码，不过这些代码不太常用。当然，你可以随意使用它们！


First, the format string. Like we mentioned, it can hold ordinary characters as well as `%` format specifiers. And whitespace characters.

> 首先，格式字符串。正如我们提到的，它可以容纳普通字符以及`％`格式说明符。还有空白字符。


Whitespace characters have a special role: a whitespace character will cause `scanf()` to consume as many whitespace characters as it can up to the next non-whitespace character. You can use this to ignore all leading or trailing whitespace.

> 空白字符具有特殊作用：空白字符会导致`scanf（）`消耗尽可能多的空白字符，直到下一个非空白字符。您可以使用它来忽略所有前导或尾随空白字符。


Also, all format specifiers except for `s`, `c`, and `[` automatically consume leading whitespace.

> 除了`s`、`c`和`[`以外，所有格式说明符都会自动消耗开头的空白符。


But I know what you're thinking: the meat of this function is in the format specifiers. What do those look like?

> 但我知道你在想什么：这个函数的核心在于格式指定符。它们看起来像什么？

These consist of the following, in sequence:

1.  A `%` sign
2.  Optional: an `*` to suppress assignment---more later
3.  Optional: a field width---max characters to read
4.  Optional: length modifier, for specifying longer or shorter types
5.  A conversion specifier, like `d` or `f` indicating the type to read

#### [22.11.0.5]{.header-section-number} The Conversion Specifier {#the-conversion-specifier number="22.11.0.5"}

Let's start with the best and last: the *conversion specifier*.


This is the part of the format specifier that tells us what type of variable `scanf()` should be reading into, like `%d` or `%f`.

> 这是格式说明符的一部分，它告诉我们`scanf()`应该读入什么类型的变量，比如`%d`或`%f`。


  ----------------------------------------------------------------------------------------------------------------------

> ----------------------------------------------------------------------------------------------------------------------
无论如何，我们都要努力前行。
   Conversion Specifier  Description

  ---------------------- -----------------------------------------------------------------------------------------------

> ---------------------- -----------------------------------------------------------------------------------------------
空白
           `d`           Matches a decimal `int`. Can have a leading sign.

           `i`           Like `d`, except will handle it if you put a leading `0x` (hex) or `0` (octal) on the number.

           `o`           Matches an octal (base 8) `unsigned int`. Leading zeros are ignored.

           `u`           Matches a decimal `unsigned int`.

           `x`           Matches a hex (base 16) `unsigned int`.

           `f`           Match a floating point number (or scientific notation, or anything `strtod()` can handle).

           `c`           Match a `char`, or mutiple `char`s if a field width is given.

           `s`           Match a sequence of non-whitespace `char`s.

           `[`           Match a sequence of characters from a set. The set ends with `]`. More below.

           `p`           Match a pointer, the opposite of `%p` for `printf()`.

           `n`           Store the number of characters written so far in the given `int*`. Doesn't consume anything.

           `%`           Match a literal percent sign.

  ----------------------------------------------------------------------------------------------------------------------

> ----------------------------------------------------------------------------------------------------------------------
无论如何，请帮助我翻译。


All of the following are equivalent to the `f` specifier: `a`, `e`, `g`, `A`, `E`, `F`, `G`.

> 所有以下等价于`f`规范：`a`、`e`、`g`、`A`、`E`、`F`、`G`。

And capital `X` is equivalent to lowercase `x`.

##### [22.11.0.5.1]{.header-section-number} The Scanset `%[]` Conversion Specifier {#the-scanset-conversion-specifier number="22.11.0.5.1"}


This is about the weirdest format specifier there is. It allows you to specify a set of characters (the *scanset*) to be stored away (likely in an array of `char`s). Conversion stops when a character that is not in the set is matched.

> 这可能是最奇怪的格式指示符了。它允许您指定一组字符（*scanset*）存储（可能是`char`数组）。当匹配到不在集合中的字符时，转换将停止。


For example, `%[0-9]` means "match all numbers zero through nine." And `%[AD-G34]` means "match A, D through G, 3, or 4".

> 例如，`％[0-9]`意味着“匹配零到九的所有数字”。而`％[AD-G34]`意味着“匹配A，D到G，3或4”。


Now, to convolute matters, you can tell `scanf()` to match characters that are *not* in the set by putting a caret (`^`) directly after the `%[` and following it with the set, like this: `%[^A-C]`, which means "match all characters that are *not* A through C."

> 现在，为了使事情复杂化，你可以告诉`scanf（）`通过在`％[`之后直接放置插入号（`^`）并在其后跟随集合来匹配不在集合中的字符，例如：`％[^A-C]`，这意味着“匹配所有不在A到C之间的字符”。


To match a close square bracket, make it the first character in the set, like this: `%[]A-C]` or `%[^]A-C]`. (I added the "`A-C`" just so it was clear that the "`]`" was first in the set.)

> 要匹配一个闭合的方括号，请将其作为集合中的第一个字符，如：`%[]A-C]` 或 `%[^]A-C]`（我只是为了清楚地表明“]”是集合中的第一个字符而添加了“A-C”）。


To match a hyphen, make it the last character in the set, e.g. to match A-through-C or hyphen: `%[A-C-]`.

> 要匹配破折号，将它作为集合中的最后一个字符，例如：要匹配A-C或破折号：`%[A-C-]`。


So if we wanted to match all letters *except* "%", "\^", "\]", "B", "C", "D", "E", and "-", we could use this format string: `%[^]%^B-E-]`.

> 如果我们想匹配除了"％"、"\^"、"\]"、"B"、"C"、"D"、"E"和"-"之外的所有字母，我们可以使用这个格式字符串：%[^]%^B-E-]。


Got it? Now we can go onto the next func---no wait! There's more! Yes, still more to know about `scanf()`. Does it never end? Try to imagine how I feel writing about it!

> 明白了吗？现在我们可以继续下一个功能了---等等！还有更多！是的，关于`scanf()`还有更多要知道。它永远不会结束吗？试着想象我写关于它的感受！

#### [22.11.0.6]{.header-section-number} The Length Modifier {#the-length-modifier number="22.11.0.6"}


So you know that "`%d`" stores into an `int`. But how do you store into a `long`, `short`, or `double`?

> 所以你知道"%d"存储到一个int中。但是如何存储到一个long、short或double中呢？


Well, like in `printf()`, you can add a modifier before the type specifier to tell `scanf()` that you have a longer or shorter type. The following is a table of the possible modifiers:

> 嗯，就像在`printf()`中一样，你可以在类型说明符之前添加一个修饰符，以告诉`scanf()`你有一个更长或更短的类型。以下是可能的修饰符的表格：


  ----------------------------------------------------------------------------------------------------------------------------------------------

> ----------------------------------------------------------------------------------------------------------------------------------------------
简体中文
   Length Modifier            Conversion Specifier           Description

  ----------------- ---------------------------------------- -----------------------------------------------------------------------------------

> ----------------- ---------------------------------------- -----------------------------------------------------------------------------------
没有可翻译的内容
        `hh`              `d`, `i`, `o`, `u`, `x`, `X`       Convert input to `char` (signed or unsigned as appropriate) before printing.

         `h`              `d`, `i`, `o`, `u`, `x`, `X`       Convert input to `short int` (signed or unsigned as appropriate) before printing.

         `l`              `d`, `i`, `o`, `u`, `x`, `X`       Convert input to `long int` (signed or unsigned as appropriate).

        `ll`              `d`, `i`, `o`, `u`, `x`, `X`       Convert input to `long long int` (signed or unsigned as appropriate).

         `j`              `d`, `i`, `o`, `u`, `x`, `X`       Convert input to `intmax_t` or `uintmax_t` (as appropriate).

         `z`              `d`, `i`, `o`, `u`, `x`, `X`       Convert input to `size_t`.

         `t`              `d`, `i`, `o`, `u`, `x`, `X`       Convert input to `ptrdiff_t`.

         `L`         `a`, `A`, `e`, `E`, `f`, `F`, `g`, `G`  Convert input to `long double`.

         `l`                      `c`,`s`,`[`                Convert input to `wchar_t`, a wide character.

         `l`                          `s`                    Argument is in a `wchar_t*`, a wide character string.

        `hh`                          `n`                    Store result in `signed char*` argument.

         `h`                          `n`                    Store result in `short int*` argument.

         `l`                          `n`                    Store result in `long int*` argument.

        `ll`                          `n`                    Store result in `long long int*` argument.

         `j`                          `n`                    Store result in `intmax_t*` argument.

         `z`                          `n`                    Store result in `size_t*` argument.

         `t`                          `n`                    Store result in `ptrdiff_t*` argument.

  ----------------------------------------------------------------------------------------------------------------------------------------------

> ----------------------------------------------------------------------------------------------------------------------------------------------
简体中文

#### [22.11.0.7]{.header-section-number} Field Widths {#field-widths number="22.11.0.7"}


The field width generally allows you to specify a maximum number of characters to consume. If the thing you're trying to match is shorter than the field width, that input will stop being processed before the field width is reached.

> 通常，字段宽度允许您指定要消耗的最大字符数。如果要匹配的内容比字段宽度短，则在达到字段宽度之前，输入将停止处理。


So a string will stop being consumed when whitespace is found, even if fewer than the field width characters are matched.

> 当发现空白字符时，即使匹配的字符数少于字段宽度，字符串也会停止被消耗。


And a float will stop being consumed at the end of the number, even if fewer characters than the field width are matched.

> 当数字结束时，即使匹配的字符数少于字段宽度，浮点数也不会被消耗。


But `%c` is an interesting one---it doesn't stop consuming characters on anything. So it'll go exactly to the field width. (Or 1 character if no field width is given.)

> 但是`%c`是一个有趣的，它不会停止消耗字符。因此它将完全按照字段宽度（如果没有指定字段宽度，则为1个字符）。

#### [22.11.0.8]{.header-section-number} Skip Input with `*` {#skip-input-with number="22.11.0.8"}


If you put an `*` in the format specifier, it tells `scanf()` do to the conversion specified, but not store it anywhere. It simply discards the data as it reads it. This is what you use if you want `scanf()` to eat some data but you don't want to store it anywhere; you don't give `scanf()` an argument for this conversion.

> 如果在格式说明符中放置一个`*`，它会告诉`scanf()`执行指定的转换，但不将其存储在任何地方。它只是在读取数据时将其丢弃。如果您想让`scanf()`吃掉一些数据，但又不想将其存储在任何地方，您就可以使用此转换，而不给`scanf()`提供任何参数。

::: {#cb534 .sourceCode}
``` {.sourceCode .c}
// Read 3 ints, but discard the middle one
scanf("%d %*d %d", &int1, &int3);
```
:::

### Return Value {#return-value-143 .unnumbered .unlisted}

`scanf()` returns the number of items assigned into variables. Since assignment into variables stops when given invalid input for a certain format specifier, this can tell you if you've input all your data correctly.

Also, `scanf()` returns `EOF` on end-of-file.

### Example {#example-146 .unnumbered .unlisted}

::: {#cb535 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    int a;
    long int b;
    unsigned int c;
    float d;
    double e;
    long double f;
    char s[100];

    scanf("%d", &a);  // store an int
    scanf(" %d", &a); // eat any whitespace, then store an int
    scanf("%s", s); // store a string
    scanf("%Lf", &f); // store a long double

    // store an unsigned, read all whitespace, then store a long int:
    scanf("%u %ld", &c, &b);

    // store an int, read whitespace, read "blendo", read whitespace,
    // and store a float:
    scanf("%d blendo %f", &a, &d);

    // read all whitespace, then store all characters up to a newline
    scanf(" %[^\n]", s);

    // store a float, read (and ignore) an int, then store a double:
    scanf("%f %*d %lf", &d, &e);

    // store 10 characters:
    scanf("%10c", s);
}
```
:::

### See Also {#see-also-137 .unnumbered .unlisted}


[`sscanf()`](stdio.html#man-scanf), [`vscanf()`](stdio.html#man-vscanf), [`vsscanf()`](stdio.html#man-vscanf), [`vfscanf()`](stdio.html#man-vscanf)

> `sscanf()`、`vscanf()`、`vsscanf()`、`vfscanf()`

------------------------------------------------------------------------

## [22.12]{.header-section-number} `vprintf()`, `vfprintf()`, `vsprintf()`, `vsnprintf()` {#man-vprintf number="22.12"}

`printf()` variants using variable argument lists (`va_list`)

### Synopsis {#synopsis-146 .unnumbered .unlisted}

::: {#cb536 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <stdarg.h>

int vprintf(const char * restrict format, va_list arg);

int vfprintf(FILE * restrict stream, const char * restrict format,
             va_list arg);

int vsprintf(char * restrict s, const char * restrict format, va_list arg);

int vsnprintf(char * restrict s, size_t n, const char * restrict format,
              va_list arg);
```
:::

### Description {#description-146 .unnumbered .unlisted}


These are just like the `printf()` variants except instead of taking an actual variable number of arguments, they take a fixed number---the last of which is a `va_list` that refers to the variable arguments.

> 这些就像`printf()`变体一样，只是它们不是采用实际的可变参数，而是采用固定数量的参数——其中最后一个是指向可变参数的`va_list`。


Like with `printf()`, the different variants send output different places.

> 就像`printf()`一样，不同的变体会将输出发送到不同的地方。

  Function        Output Destination
  --------------- --------------------------------------------------
  `vprintf()`     Print to console (screen by default, typically).
  `vfprintf()`    Print to a file.
  `vsprintf()`    Print to a string.
  `vsnprintf()`   Print to a string (safely).


Both `vsprintf()` and `vsnprintf()` have the quality that if you pass in `NULL` as the buffer, nothing is written---but you can still check the return value to see how many characters *would* have been written.

> 两个函数`vsprintf()`和`vsnprintf()`都有一个特性：如果你传入`NULL`作为缓冲区，什么都不会被写入，但是你仍然可以检查返回值来看本来会被写入多少字符。


If you try to write out more than the maximum number of characters, `vsnprintf()` will graciously write only [\\(n-1\\)]{.math .inline} characters so that it has enough room to write the terminator at the end.

> 如果你试图写出超过最大字符数的内容，`vsnprintf()` 会慷慨地只写出 [\\(n-1\\)]{.math .inline} 个字符，以便有足够的空间在末尾写入终止符。


As for why in the heck would you ever want to do this, the most common reason is to create your own specialized versions of `printf()`-type functions, piggybacking on all that `printf()` functionality goodness.

> 至于为什么你要这么做，最常见的原因是创建自己的专用版本的`printf()`类型函数，利用`printf()`功能的优点。

See the example for an example, predictably.

### Return Value {#return-value-144 .unnumbered .unlisted}

`vprintf()` and `vfprintf()` return the number of characters printed, or a negative value on error.

`vsprintf()` returns the number of characters printed to the buffer, not counting the NUL terminator, or a negative value if an error occurred.

`vnsprintf()` returns the number of characters printed to the buffer. Or the number that *would* have been printed if the buffer had been large enough.

### Example {#example-147 .unnumbered .unlisted}


In this example, we make our own version of `printf()` called `logger()` that timestamps output. Notice how the calls to `logger()` have all the bells and whistles of `printf()`.

> 在这个例子中，我们创建了自己版本的`printf()`，叫做`logger()`，它可以对输出进行时间戳标记。注意，对`logger()`的调用具有`printf()`的所有功能。

::: {#cb537 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdarg.h>
#include <time.h>

int logger(char *format, ...)
{
    va_list va;
    time_t now_secs = time(NULL);
    struct tm *now = gmtime(&now_secs);

    // Output timestamp in format "YYYY-MM-DD hh:mm:ss : "
    printf("%04d-%02d-%02d %02d:%02d:%02d : ",
        now->tm_year + 1900, now->tm_mon + 1, now->tm_mday,
        now->tm_hour, now->tm_min, now->tm_sec);

    va_start(va, format);
    int result = vprintf(format, va);
    va_end(va);

    printf("\n");

    return result;
}

int main(void)
{
    int x = 12;
    float y = 3.2;

    logger("Hello!");
    logger("x = %d and y = %.2f", x, y);
}
```
:::

Output:

::: {#cb538 .sourceCode}
``` {.sourceCode .default}
2021-03-30 04:25:49 : Hello!
2021-03-30 04:25:49 : x = 12 and y = 3.20
```
:::

### See Also {#see-also-138 .unnumbered .unlisted}

[`printf()`](stdio.html#man-printf)

------------------------------------------------------------------------

## [22.13]{.header-section-number} `vscanf()`, `vfscanf()`, `vsscanf()` {#man-vscanf number="22.13"}

`scanf()` variants using variable argument lists (`va_list`)

### Synopsis {#synopsis-147 .unnumbered .unlisted}

::: {#cb539 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <stdarg.h>

int vscanf(const char * restrict format, va_list arg);

int vfscanf(FILE * restrict stream, const char * restrict format,
            va_list arg);

int vsscanf(const char * restrict s, const char * restrict format,
            va_list arg);
```
:::

### Description {#description-147 .unnumbered .unlisted}


These are just like the `scanf()` variants except instead of taking an actual variable number of arguments, they take a fixed number---the last of which is a `va_list` that refers to the variable arguments.

> 这些就像`scanf()`变体一样，只是它们不是采用实际的可变参数，而是采用固定数量的参数，其中最后一个是指向可变参数的`va_list`。

  Function      Input Source
  ------------- ---------------------------------------------------------
  `vscanf()`    Read from the console (keyboard by default, typically).
  `vfscanf()`   Read from a file.
  `vsscanf()`   Read from a string.


Like with the `vprintf()` functions, this would be a good way to add additional functionality that took advantage of the power `scanf()` has to offer.

> 就像`vprintf()`函数一样，这是一种利用`scanf()`的强大功能来添加附加功能的好方法。

### Return Value {#return-value-145 .unnumbered .unlisted}


Returns the number of items successfully scanned, or `EOF` on end-of-file or error.

> 返回成功扫描的项目数量，或者在文件结尾或错误时返回`EOF`。

### Example {#example-148 .unnumbered .unlisted}


I have to admit I was wracking my brain to think of when you'd ever want to use this. The best example I could find was [one on Stack Overflow](https://stackoverflow.com/questions/17017331/c99-vscanf-for-dummies/17018046#17018046)[^49^](footnotes.html#fn49){#fnref49 .footnote-ref role="doc-noteref"} that error-checks the return value from `scanf()` against the expected. A variant of that is shown below.

> 我不得不承认，我正在努力思考你何时会想要使用这个。我找到的最好的例子是[一个在Stack Overflow上的](https://stackoverflow.com/questions/17017331/c99-vscanf-for-dummies/17018046#17018046)[^49^](footnotes.html#fn49){#fnref49 .footnote-ref role="doc-noteref"}，用于检查`scanf()`的返回值与预期值是否相符。下面是一个变体。

::: {#cb540 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdarg.h>
#include <assert.h>

int error_check_scanf(int expected_count, char *format, ...)
{
    va_list va;

    va_start(va, format);
    int count = vscanf(format, va);
    va_end(va);

    // This line will crash the program if the condition is false:
    assert(count == expected_count);

    return count;
}

int main(void)
{
    int a, b;
    float c;

    error_check_scanf(3, "%d, %d/%f", &a, &b, &c);
    error_check_scanf(2, "%d", &a);
}
```
:::

### See Also {#see-also-139 .unnumbered .unlisted}

[`scanf()`](stdio.html#man-scanf)

------------------------------------------------------------------------

## [22.14]{.header-section-number} `getc()`, `fgetc()`, `getchar()` {#man-getc number="22.14"}

Get a single character from the console or from a file

### Synopsis {#synopsis-148 .unnumbered .unlisted}

::: {#cb541 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int getc(FILE *stream);

int fgetc(FILE *stream);

int getchar(void);
```
:::

### Description {#description-148 .unnumbered .unlisted}


All of these functions in one way or another, read a single character from the console or from a `FILE`. The differences are fairly minor, and here are the descriptions:

> 所有这些功能都以某种方式从控制台或`FILE`中读取单个字符。 差异相当小，以下是描述：

`getc()` returns a character from the specified `FILE`. From a usage standpoint, it's equivalent to the same `fgetc()` call, and `fgetc()` is a little more common to see. Only the implementation of the two functions differs.

`fgetc()` returns a character from the specified `FILE`. From a usage standpoint, it's equivalent to the same `getc()` call, except that `fgetc()` is a little more common to see. Only the implementation of the two functions differs.

Yes, I cheated and used cut-n-paste to do that last paragraph.

`getchar()` returns a character from `stdin`. In fact, it's the same as calling `getc(stdin)`.

### Return Value {#return-value-146 .unnumbered .unlisted}


All three functions return the `unsigned char` that they read, except it's cast to an `int`.

> 所有三个函数都会返回它们读取的`unsigned char`，但是会被转换为`int`。


If end-of-file or an error is encountered, all three functions return `EOF`.

> 如果遇到文件结尾或错误，这三个函数都会返回“EOF”。

### Example {#example-149 .unnumbered .unlisted}


This example reads all the characters from a file, outputting only the letter 'b's it finds..

> 这个例子从文件中读取所有字符，只输出找到的字母'b'。

::: {#cb542 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *fp;
    int c;

    fp = fopen("spoon.txt", "r"); // error check this!

    // this while-statement assigns into c, and then checks against EOF:

    while((c = fgetc(fp)) != EOF) {
        if (c == 'b') {
            putchar(c);
        }
    }

    putchar('\n');

    fclose(fp);
}
```
:::

### See Also {#see-also-140 .unnumbered .unlisted}

------------------------------------------------------------------------

## [22.15]{.header-section-number} `gets()`, `fgets()` {#man-gets number="22.15"}

Read a string from console or file

### Synopsis {#synopsis-149 .unnumbered .unlisted}

::: {#cb543 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

char *fgets(char *s, int size, FILE *stream);
char *gets(char *s);
```
:::

### Description {#description-149 .unnumbered .unlisted}


These are functions that will retrieve a newline-terminated string from the console or a file. In other normal words, it reads a line of text. The behavior is slightly different, and, as such, so is the usage. For instance, here is the usage of `gets()`:

> 这些是从控制台或文件中检索换行终止字符串的函数。换句话说，它读取一行文本。行为略有不同，因此使用方式也不同。例如，这是`gets()`的用法：


Don't use `gets()`. In fact, as of C11, it ceases to exist! This is one of the rare cases of a function being *removed* from the standard.

> 不要使用`gets()`。事实上，自C11以来，它已经不复存在了！这是一个罕见的函数从标准中被*移除*的情况。


Admittedly, rationale would be useful, yes? For one thing, `gets()` doesn't allow you to specify the length of the buffer to store the string in. This would allow people to keep entering data past the end of your buffer, and believe me, this would be Bad News.

> 承认，理性会很有用，是吗？首先，`gets()`不允许你指定用于存储字符串的缓冲区的长度。这将允许人们输入超出缓冲区结尾的数据，相信我，这将是坏消息。


And that's what the `size` parameter in `fgets()` is for. `fgets()` will read at most `size-1` characters and then stick a `NUL` terminator on after that.

> 这就是`fgets()`中的`size`参数的用处。`fgets()`最多会读取`size-1`个字符，然后在末尾添加一个`NUL`终止符。


I was going to add another reason, but that's basically the primary and only reason not to use `gets()`. As you might suspect, `fgets()` allows you to specify a maximum string length.

> 我本打算再加一个原因，但这基本上是不使用`gets()`的主要唯一原因。正如你可能猜到的，`fgets()`允许您指定最大字符串长度。


One difference here between the two functions: `gets()` will devour and throw away the newline at the end of the line, while `fgets()` will store it at the end of your string (space permitting).

> 这里两个函数的一个区别是：`gets()`会吞掉行尾的换行符，而`fgets()`会将它存储在字符串的末尾（如果有足够的空间的话）。


Here's an example of using `fgets()` from the console, making it behave more like `gets()` (with the exception of the newline inclusion):

> 这里是一个使用`fgets()`从控制台输入，使其表现得更像`gets()`（除了包括换行符）的例子：

::: {#cb544 .sourceCode}
``` {.sourceCode .c}
char s[100];
gets(s);  // don't use this--read a line (from stdin)
fgets(s, sizeof(s), stdin); // read a line from stdin
```
:::


In this case, the `sizeof()` operator gives us the total size of the array in bytes, and since a `char` is a byte, it conveniently gives us the total size of the array.

> 在这种情况下，`sizeof()` 运算符给我们数组的总大小，以字节为单位，而由于`char`是一个字节，它方便地给我们提供了数组的总大小。


Of course, like I keep saying, the string returned from `fgets()` probably has a newline at the end that you might not want. You can write a short function to chop the newline off---in fact, let's just roll that into our own version of `gets()`

> 当然，正如我一直在说的，从`fgets()`返回的字符串可能在末尾有一个换行符，你可能不想要它。你可以编写一个简短的函数来删除换行符——事实上，让我们把它放入我们自己版本的`gets()`中吧。

::: {#cb545 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <string.h>

char *ngets(char *s, int size)
{
    char *rv = fgets(s, size, stdin);

    if (rv == NULL)
        return NULL;

    char *p = strchr(s, '\n');  // Find a newline

    if (p != NULL)  // if there's a newline
        *p = '\0';  // truncate the string there

    return s;
}
```
:::


So, in summary, use `fgets()` to read a line of text from the keyboard or a file, and don't use `gets()`.

> 总之，使用`fgets()`从键盘或文件读取一行文本，不要使用`gets()`。

### Return Value {#return-value-147 .unnumbered .unlisted}

Both `gets()` and `fgets()` return a pointer to the string passed.

On error or end-of-file, the functions return `NULL`.

### Example {#example-150 .unnumbered .unlisted}

::: {#cb546 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char s[100];

    gets(s); // read from standard input (don't use this--use fgets()!)

    fgets(s, sizeof s, stdin); // read 100 bytes from standard input

    fp = fopen("spoon.txt", "r"); // (you should error-check this)
    fgets(s, 100, fp); // read 100 bytes from the file datafile.dat
    fclose(fp);

    fgets(s, 20, stdin); // read a maximum of 20 bytes from stdin
}
```
:::

### See Also {#see-also-141 .unnumbered .unlisted}


[`getc()`](stdio.html#man-getc), [`fgetc()`](stdio.html#man-getc), [`getchar()`](stdio.html#man-getc), [`puts()`](stdio.html#man-puts), [`fputs()`](stdio.html#man-puts), [`ungetc()`](stdio.html#man-ungetc)

> [`getc()`](stdio.html#man-getc)：从文件中读取一个字符
[`fgetc()`](stdio.html#man-getc)：从文件流中读取一个字符
[`getchar()`](stdio.html#man-getc)：从标准输入中读取一个字符
[`puts()`](stdio.html#man-puts)：将字符串写入标准输出
[`fputs()`](stdio.html#man-puts)：将字符串写入文件流
[`ungetc()`](stdio.html#man-ungetc)：将字符放回文件缓冲区

------------------------------------------------------------------------

## [22.16]{.header-section-number} `putc()`, `fputc()`, `putchar()` {#man-putc number="22.16"}

Write a single character to the console or to a file

### Synopsis {#synopsis-150 .unnumbered .unlisted}

::: {#cb547 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int putc(int c, FILE *stream);

int fputc(int c, FILE *stream);

int putchar(int c);
```
:::

### Description {#description-150 .unnumbered .unlisted}


All three functions output a single character, either to the console or to a `FILE`.

> 所有三个函数都会输出一个字符，可以是到控制台或者是到一个文件中。

`putc()` takes a character argument, and outputs it to the specified `FILE`. `fputc()` does exactly the same thing, and differs from `putc()` in implementation only. Most people use `fputc()`.

`putchar()` writes the character to the console, and is the same as calling `putc(c, stdout)`.

### Return Value {#return-value-148 .unnumbered .unlisted}


All three functions return the character written on success, or `EOF` on error.

> 所有三个函数在成功时返回写入的字符，在出错时返回`EOF`。

### Example {#example-151 .unnumbered .unlisted}

Print the alphabet:

::: {#cb548 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    char i;

    for(i = 'A'; i <= 'Z'; i++)
        putchar(i);

    putchar('\n'); // put a newline at the end to make it pretty
}
```
:::

### See Also {#see-also-142 .unnumbered .unlisted}

------------------------------------------------------------------------

## [22.17]{.header-section-number} `puts()`, `fputs()` {#man-puts number="22.17"}

Write a string to the console or to a file

### Synopsis {#synopsis-151 .unnumbered .unlisted}

::: {#cb549 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int puts(const char *s);

int fputs(const char *s, FILE *stream);
```
:::

### Description {#description-151 .unnumbered .unlisted}


Both these functions output a NUL-terminated string. `puts()` outputs to the console, while `fputs()` allows you to specify the file for output.

> 两个函数都会输出一个以NUL结尾的字符串。`puts()`会输出到控制台，而`fputs()`则允许您指定输出文件。

### Return Value {#return-value-149 .unnumbered .unlisted}

Both functions return non-negative on success, or `EOF` on error.

### Example {#example-152 .unnumbered .unlisted}

Read strings from the console and save them in a file:

::: {#cb550 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char s[100];

    fp = fopen("somefile.txt", "w"); // error check this!

    while(fgets(s, sizeof(s), stdin) != NULL) { // read a string
        fputs(s, fp);  // write it to the file we opened
    }

    fclose(fp);
}
```
:::

### See Also {#see-also-143 .unnumbered .unlisted}

------------------------------------------------------------------------

## [22.18]{.header-section-number} `ungetc()` {#man-ungetc number="22.18"}

Pushes a character back into the input stream

### Synopsis {#synopsis-152 .unnumbered .unlisted}

::: {#cb551 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int ungetc(int c, FILE *stream);
```
:::

### Description {#description-152 .unnumbered .unlisted}


You know how `getc()` reads the next character from a file stream? Well, this is the opposite of that---it pushes a character back into the file stream so that it will show up again on the very next read from the stream, as if you'd never gotten it from `getc()` in the first place.

> 你知道`getc()`是如何从文件流中读取下一个字符的吗？好吧，这正好相反---它将一个字符推回文件流，以便它将在下一次从流中读取时再次出现，就好像你从`getc()`中从未获得它一样。


Why, in the name of all that is holy would you want to do that? Perhaps you have a stream of data that you're reading a character at a time, and you won't know to stop reading until you get a certain character, but you want to be able to read that character again later. You can read the character, see that it's what you're supposed to stop on, and then `ungetc()` it so it'll show up on the next read.

> 为什么你要这么做？也许你正在一次读取一个字符的数据流，你不知道何时停止读取，直到你得到一个特定的字符。但你想稍后再读取这个字符。你可以读取这个字符，看到它是你应该停止的位置，然后使用`ungetc()`，这样它就会在下次读取时显示出来。

Yeah, that doesn't happen very often, but there we are.


Here's the catch: the standard only guarantees that you'll be able to push back *one character*. Some implementations might allow you to push back more, but there's really no way to tell and still be portable.

> 这里是抓手：标准只保证你可以推回一个字符。一些实现可能允许你推回更多，但是要想保持可移植性，真的没有办法知道。

### Return Value {#return-value-150 .unnumbered .unlisted}


On success, `ungetc()` returns the character you passed to it. On failure, it returns `EOF`.

> 如果成功，`ungetc()`会返回你传入它的字符。如果失败，它会返回`EOF`。

### Example {#example-153 .unnumbered .unlisted}


This example reads a piece of punctuation, then everything after it up to the next piece of punctuation. It returns the leading punctuation, and stores the rest in a string.

> 这个例子读取一段标点符号，然后读取直到下一个标点符号的所有内容。它会返回前导标点符号，并将剩余的内容存储在一个字符串中。

::: {#cb552 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <ctype.h>

int read_punctstring(FILE *fp, char *s)
{
    int origpunct, c;
    
    origpunct = fgetc(fp);

    if (origpunct == EOF)  // return EOF on end-of-file
        return EOF;

    while (c = fgetc(fp), !ispunct(c) && c != EOF)
        *s++ = c;  // save it in the string

    *s = '\0'; // nul-terminate the string

    // if we read punctuation last, ungetc it so we can fgetc it next
    // time:
    if (ispunct(c))
        ungetc(c, fp);

    return origpunct;
}

int main(void)
{
    char s[128];
    char c;

    while((c = read_punctstring(stdin, s)) != EOF) {
        printf("%c: %s\n", c, s);
    }
}
```
:::

Sample Input:

::: {#cb553 .sourceCode}
``` {.sourceCode .default}
!foo#bar*baz
```
:::

Sample output:

::: {#cb554 .sourceCode}
``` {.sourceCode .default}
!: foo
#: bar
*: baz
```
:::

### See Also {#see-also-144 .unnumbered .unlisted}

[`fgetc()`](stdio.html#man-getc)

------------------------------------------------------------------------

## [22.19]{.header-section-number} `fread()` {#man-fread number="22.19"}

Read binary data from a file

### Synopsis {#synopsis-153 .unnumbered .unlisted}

::: {#cb555 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

size_t fread(void *p, size_t size, size_t nmemb, FILE *stream);
```
:::

### Description {#description-153 .unnumbered .unlisted}


You might remember that you can call [`fopen()`](stdio.html#man-fopen) with the "`b`" flag in the open mode string to open the file in "binary" mode. Files open in not-binary (ASCII or text mode) can be read using standard character-oriented calls like [`fgetc()`](stdio.html#man-getc) or [`fgets()`](stdio.html#man-gets). Files open in binary mode are typically read using the `fread()` function.

> 你可能记得可以使用“b”标志在打开模式字符串中调用fopen（）以二进制模式打开文件。 使用标准字符导向调用（例如fgetc（）或fgets（））可以读取未二进制（ASCII或文本模式）的文件。 通常使用fread（）函数读取以二进制模式打开的文件。


All this function does is says, "Hey, read this many things where each thing is a certain number of bytes, and store the whole mess of them in memory starting at this pointer."

> 所有这个函数做的就是说，“嘿，读取这么多个东西，每个东西是一定字节数，然后把整个东西存储在从这个指针开始的内存中。”


This can be very useful, believe me, when you want to do something like store 20 `int`s in a file.

> 这可能会非常有用，相信我，当你想要像存储20个int一样做某事时。


But wait---can't you use [`fprintf()`](stdio.html#man-printf) with the "`%d`" format specifier to save the `int`s to a text file and store them that way? Yes, sure. That has the advantage that a human can open the file and read the numbers. It has the disadvantage that it's slower to convert the numbers from `int`s to text and that the numbers are likely to take more space in the file. (Remember, an `int` is likely 4 bytes, but the string "12345678" is 8 bytes.)

> 但是等等---你不能用“％d”格式说明符使用fprintf（）将int保存到文本文件中并以此方式存储它们吗？是的，当然可以。这具有优势，人类可以打开文件并读取数字。它的缺点是将数字从int转换为文本的速度较慢，并且数字在文件中可能需要更多的空间。 （记住，int可能是4个字节，但字符串“12345678”是8个字节。）


So storing the binary data can certainly be more compact and faster to read.

> 存储二进制数据当然更加紧凑和快速读取。

### Return Value {#return-value-151 .unnumbered .unlisted}


This function returns the number of items successfully read. If all requested items are read, the return value will be equal to that of the parameter `nmemb`. If EOF occurs, the return value will be zero.

> 这个函数返回成功读取的项目数量。如果所有请求的项目都被读取，返回值将等于参数`nmemb`的值。如果发生EOF，返回值将为零。


To make you confused, it will also return zero if there's an error. You can use the functions [`feof()`](stdio.html#man-feof) or [`ferror()`](stdio.html#man-feof) to tell which one really happened.

> 为了让你感到困惑，如果发生错误，它也会返回零。您可以使用函数[`feof（）`](stdio.html#man-feof)或[`ferror（）`](stdio.html#man-feof)来告诉哪一个真的发生了。

### Example {#example-154 .unnumbered .unlisted}

Read 10 numbers from a file and store them in an array:

::: {#cb556 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    int i;
    int n[10]
    FILE *fp;

    fp = fopen("numbers.dat", "rb");
    fread(n, sizeof(int), 10, fp);  // read 10 ints
    fclose(fp);

    // print them out:
    for(i = 0; i < 10; i++)
        printf("n[%d] == %d\n", i, n[i]);
}
```
:::

### See Also {#see-also-145 .unnumbered .unlisted}


[`fopen()`](stdio.html#man-fopen), [`fwrite()`](stdio.html#man-fwrite), [`feof()`](stdio.html#man-feof), [`ferror()`](stdio.html#man-feof)

> [`fopen()`](stdio.html#man-fopen)：打开文件
[`fwrite()`](stdio.html#man-fwrite)：写入文件
[`feof()`](stdio.html#man-feof)：检测文件结尾
[`ferror()`](stdio.html#man-feof)：检测文件错误

------------------------------------------------------------------------

## [22.20]{.header-section-number} `fwrite()` {#man-fwrite number="22.20"}

Write binary data to a file

### Synopsis {#synopsis-154 .unnumbered .unlisted}

::: {#cb557 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

size_t fwrite(const void *p, size_t size, size_t nmemb, FILE *stream);
```
:::

### Description {#description-154 .unnumbered .unlisted}


This is the counterpart to the [`fread()`](stdio.html#man-fread) function. It writes blocks of binary data to disk. For a description of what this means, see the entry for [`fread()`](stdio.html#man-fread).

> 这是[`fread()`](stdio.html#man-fread)函数的对应物。它将二进制数据块写入磁盘。要了解其含义，请参阅[`fread()`](stdio.html#man-fread)的条目。

### Return Value {#return-value-152 .unnumbered .unlisted}

`fwrite()` returns the number of items successfully written, which should hopefully be `nmemb` that you passed in. It'll return zero on error.

### Example {#example-155 .unnumbered .unlisted}

Save 10 random numbers to a file:

::: {#cb558 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int i;
    int n[10];
    FILE *fp;

    // populate the array with random numbers:
    for(i = 0; i < 10; i++) {
        n[i] = rand();
        printf("n[%d] = %d\n", i, n[i]);
    }

    // save the random numbers (10 ints) to the file
    fp = fopen("numbers.dat", "wb");
    fwrite(n, sizeof(int), 10, fp); // write 10 ints
    fclose(fp);
}
```
:::

### See Also {#see-also-146 .unnumbered .unlisted}

[`fopen()`](stdio.html#man-fopen), [`fread()`](stdio.html#man-fread)

------------------------------------------------------------------------

## [22.21]{.header-section-number} `fgetpos()`, `fsetpos()` {#man-fgetpos number="22.21"}


Get the current position in a file, or set the current position in a file. Just like `ftell()` and `fseek()` for most systems

> 获取文件中的当前位置，或者设置文件中的当前位置。就像大多数系统中的`ftell()`和`fseek()`一样。

### Synopsis {#synopsis-155 .unnumbered .unlisted}

::: {#cb559 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int fgetpos(FILE *stream, fpos_t *pos);

int fsetpos(FILE *stream, fpos_t *pos);
```
:::

### Description {#description-155 .unnumbered .unlisted}


These functions are just like `ftell()` and `fseek()`, except instead of counting in bytes, they use an *opaque* data structure to hold positional information about the file. (Opaque, in this case, means you're not supposed to know what the data type is made up of.)

> 这些函数就像`ftell()`和`fseek()`一样，只不过它们不是以字节计数，而是使用一种*不透明*的数据结构来保存文件的位置信息（在这种情况下，不透明意味着你不应该知道数据类型是由什么组成的）。


On virtually every system (and certainly every system that I know of), people don't use these functions, using `ftell()` and `fseek()` instead. These functions exist just in case your system can't remember file positions as a simple byte offset.

> 几乎在每一个系统（当然，我所知道的每一个系统）上，人们不使用这些函数，而是使用`ftell()`和`fseek()`代替。这些函数只是为了防止你的系统无法将文件位置记录为简单的字节偏移量。


Since the `pos` variable is opaque, you have to assign to it using the `fgetpos()` call itself. Then you save the value for later and use it to reset the position using `fsetpos()`.

> 由于`pos`变量不透明，您必须使用`fgetpos()`调用本身来对其进行赋值。然后您将该值保存以备以后使用，并使用`fsetpos()`将其重置。

### Return Value {#return-value-153 .unnumbered .unlisted}

Both functions return zero on success, and `-1` on error.

### Example {#example-156 .unnumbered .unlisted}

::: {#cb560 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    char s[100];
    fpos_t pos;
    FILE *fp;

    fp = fopen("spoon.txt", "r");

    fgets(s, sizeof(s), fp); // read a line from the file
    printf("%s", s);

    fgetpos(fp, &pos);   // save the position after the read

    fgets(s, sizeof(s), fp); // read another line from the file
    printf("%s", s);

    fsetpos(fp, &pos);   // now restore the position to where we saved

    fgets(s, sizeof(s), fp); // read the earlier line again
    printf("%s", s);

    fclose(fp);
}
```
:::

### See Also {#see-also-147 .unnumbered .unlisted}


[`fseek()`](stdio.html#man-fseek), [`ftell()`](stdio.html#man-ftell), [`rewind()`](stdio.html#man-fseek)

> [`fseek()`](stdio.html#man-fseek)：fseek()，
[`ftell()`](stdio.html#man-ftell)：ftell()，
[`rewind()`](stdio.html#man-fseek)：重置文件指针。

------------------------------------------------------------------------

## [22.22]{.header-section-number} `fseek()`, `rewind()` {#man-fseek number="22.22"}

Position the file pointer in anticipition of the next read or write

### Synopsis {#synopsis-156 .unnumbered .unlisted}

::: {#cb561 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int fseek(FILE *stream, long offset, int whence);

void rewind(FILE *stream);
```
:::

### Description {#description-156 .unnumbered .unlisted}


When doing reads and writes to a file, the OS keeps track of where you are in the file using a counter generically known as the file pointer. You can reposition the file pointer to a different point in the file using the `fseek()` call. Think of it as a way to randomly access you file.

> 当对文件进行读写时，操作系统会使用一个通用称为文件指针的计数器来跟踪你在文件中的位置。您可以使用`fseek（）`调用将文件指针重新定位到文件的不同位置。把它想象成一种随机访问您的文件的方式。


The first argument is the file in question, obviously. `offset` argument is the position that you want to seek to, and `whence` is what that offset is relative to.

> 第一个参数显然是有问题的文件。`offset`参数是您要寻求的位置，而`whence`是该偏移量相对于什么。


Of course, you probably like to think of the offset as being from the beginning of the file. I mean, "Seek to position 3490, that should be 3490 bytes from the beginning of the file." Well, it *can* be, but it doesn't have to be. Imagine the power you're wielding here. Try to command your enthusiasm.

> 当然，你可能喜欢把偏移量视为从文件开头开始的。我的意思是，“定位到位置3490，这应该是从文件开头开始的3490字节。”好吧，它*可以*是，但不一定是。想象一下你正在掌握的力量。试着去指挥你的热情。

You can set the value of `whence` to one of three things:


  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告。
  `whence`     Description

  ------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
没有可翻译的内容

  `SEEK_SET`   `offset` is relative to the beginning of the file. This is probably what you had in mind anyway, and is the most commonly used value for `whence`.

> `SEEK_SET` 偏移量是相对于文件开头的。 这可能是您想要的，也是`whence`最常用的值。


  `SEEK_CUR`   `offset` is relative to the current file pointer position. So, in effect, you can say, "Move to my current position plus 30 bytes," or, "move to my current position minus 20 bytes."

> `SEEK_CUR` `偏移量`是相对于当前文件指针位置的。因此，实际上，你可以说：“移动到我当前位置加上30个字节”，或者“移动到我当前位置减去20个字节”。


  `SEEK_END`   `offset` is relative to the end of the file. Just like `SEEK_SET` except from the other end of the file. Be sure to use negative values for `offset` if you want to back up from the end of the file, instead of going past the end into oblivion.

> `SEEK_END` `offset` 相对于文件的末尾。就像 `SEEK_SET` 一样，只是从文件的另一端开始。如果你想从文件末尾向后退，而不是超出文件末尾，请确保使用负值作为 `offset`。

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
无可奉告。


Speaking of seeking off the end of the file, can you do it? Sure thing. In fact, you can seek way off the end and then write a character; the file will be expanded to a size big enough to hold a bunch of zeros way out to that character.

> 谈到寻找文件末尾，你能做到吗？当然可以。事实上，你可以寻找很远的末尾，然后写入一个字符；文件将被扩展到足够大的尺寸，可以在那个字符处容纳大量的零。


Now that the complicated function is out of the way, what's this `rewind()` that I briefly mentioned? It repositions the file pointer at the beginning of the file:

> 现在复杂的函数已经完成，我简要提到的`rewind()`又是什么呢？它将文件指针重新定位到文件的开头。

::: {#cb562 .sourceCode}
``` {.sourceCode .c}
fseek(fp, 0, SEEK_SET); // same as rewind()
rewind(fp);             // same as fseek(fp, 0, SEEK_SET)
```
:::

### Return Value {#return-value-154 .unnumbered .unlisted}

For `fseek()`, on success zero is returned; `-1` is returned on failure.

The call to `rewind()` never fails.

### Example {#example-157 .unnumbered .unlisted}

::: {#cb563 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    FILE *fp;

    fp = fopen("spoon.txt", "r");

    fseek(fp, 100, SEEK_SET); // seek to the 100th byte of the file
    printf("100: %c\n", fgetc(fp));

    fseek(fp, -31, SEEK_CUR); // seek backward 30 bytes from the current pos
    printf("31 back: %c\n", fgetc(fp));

    fseek(fp, -12, SEEK_END); // seek to the 10th byte before the end of file
    printf("12 from end: %c\n", fgetc(fp));

    fseek(fp, 0, SEEK_SET);   // seek to the beginning of the file
    rewind(fp);               // seek to the beginning of the file, too
    printf("Beginning: %c\n", fgetc(fp));

    fclose(fp);
}
```
:::

### See Also {#see-also-148 .unnumbered .unlisted}


[`ftell()`](stdio.html#man-ftell), [`fgetpos()`](stdio.html#man-fgetpos), [`fsetpos()`](stdio.html#man-fgetpos)

> [`ftell()`](stdio.html#man-ftell)：取得文件指针的当前位置
[`fgetpos()`](stdio.html#man-fgetpos)：取得文件指针的当前位置，并将其存储在指定的缓冲区中
[`fsetpos()`](stdio.html#man-fgetpos)：将文件指针设置到指定的缓冲区中存储的位置

------------------------------------------------------------------------

## [22.23]{.header-section-number} `ftell()` {#man-ftell number="22.23"}

Tells you where a particular file is about to read from or write to

### Synopsis {#synopsis-157 .unnumbered .unlisted}

::: {#cb564 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

long ftell(FILE *stream);
```
:::

### Description {#description-157 .unnumbered .unlisted}


This function is the opposite of [`fseek()`](stdio.html#man-fseek). It tells you where in the file the next file operation will occur relative to the beginning of the file.

> 这个函数是[`fseek()`](stdio.html#man-fseek)的反函数。它告诉你下一个文件操作相对于文件开头的位置。


It's useful if you want to remember where you are in the file, `fseek()` somewhere else, and then come back later. You can take the return value from `ftell()` and feed it back into `fseek()` (with `whence` parameter set to `SEEK_SET`) when you want to return to your previous position.

> 如果你想记住文件中的位置，使用`fseek()`在其他位置移动，然后稍后再返回，可以使用`ftell()`获取返回值，并将其传递给`fseek()`（将`whence`参数设置为`SEEK_SET`），以便返回到先前的位置。

### Return Value {#return-value-155 .unnumbered .unlisted}

Returns the current offset in the file, or `-1` on error.

### Example {#example-158 .unnumbered .unlisted}

::: {#cb565 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    char c[6];
    FILE *fp;

    fp = fopen("spoon.txt", "r");

    long pos;

    // seek ahead 10 bytes:
    fseek(fp, 10, SEEK_SET);

    // store the current position in variable "pos":
    pos = ftell(fp);

    // Read some bytes
    fread(c, sizeof c  - 1, 1, fp);
    c[5] = '\0';
    printf("Read: \"%s\"\n", c);

    // and return to the starting position, stored in "pos":
    fseek(fp, pos, SEEK_SET);

    // Read the same bytes again
    fread(c, sizeof c  - 1, 1, fp);
    c[5] = '\0';
    printf("Read: \"%s\"\n", c);

    fclose(fp);
}
```
:::

### See Also {#see-also-149 .unnumbered .unlisted}


[`fseek()`](stdio.html#man-fseek), [`rewind()`](stdio.html#man-fseek), [`fgetpos()`](stdio.html#man-fgetpos), [`fsetpos()`](stdio.html#man-fgetpos)

> [`fseek()`](stdio.html#man-fseek)：设置文件指针位置
[`rewind()`](stdio.html#man-fseek)：将文件指针重新定位到文件的开头
[`fgetpos()`](stdio.html#man-fgetpos)：获取文件指针的当前位置
[`fsetpos()`](stdio.html#man-fgetpos)：设置文件指针的位置

------------------------------------------------------------------------

## [22.24]{.header-section-number} `feof()`, `ferror()`, `clearerr()` {#man-feof number="22.24"}

Determine if a file has reached end-of-file or if an error has occurred

### Synopsis {#synopsis-158 .unnumbered .unlisted}

::: {#cb566 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>

int feof(FILE *stream);

int ferror(FILE *stream);

void clearerr(FILE *stream);
```
:::

### Description {#description-158 .unnumbered .unlisted}


Each `FILE*` that you use to read and write data from and to a file contains flags that the system sets when certain events occur. If you get an error, it sets the error flag; if you reach the end of the file during a read, it sets the EOF flag. Pretty simple really.

> 每一个你用来读写文件的`FILE*`都包含系统在某些事件发生时设置的标志。如果你遇到错误，它会设置错误标志；如果你在读取时到达文件末尾，它会设置EOF标志。很简单。


The functions `feof()` and `ferror()` give you a simple way to test these flags: they'll return non-zero (true) if they're set.

> 这些函数`feof()`和`ferror()`提供了一种简单的方法来测试这些标志：如果它们被设置，它们将返回非零（真）值。


Once the flags are set for a particular stream, they stay that way until you call `clearerr()` to clear them.

> 一旦为特定流设置了标志，它们会一直保持这种状态，直到调用`clearerr()`来清除它们。

### Return Value {#return-value-156 .unnumbered .unlisted}

`feof()` and `ferror()` return non-zero (true) if the file has reached EOF or there has been an error, respectively.

### Example {#example-159 .unnumbered .unlisted}

Read binary data, checking for EOF or error:

::: {#cb567 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

int main(void)
{
    int a;
    FILE *fp;

    fp = fopen("numbers.dat", "r");

    // read single ints at a time, stopping on EOF or error:

    while(fread(&a, sizeof(int), 1, fp), !feof(fp) && !ferror(fp)) {
        printf("Read %d\n", a);
    }

    if (feof(fp))
        printf("End of file was reached.\n");

    if (ferror(fp))
        printf("An error occurred.\n");

    fclose(fp);
}
```
:::

### See Also {#see-also-150 .unnumbered .unlisted}

[`fopen()`](stdio.html#man-fopen), [`fread()`](stdio.html#man-fread)

------------------------------------------------------------------------

## [22.25]{.header-section-number} `perror()` {#man-perror number="22.25"}

Print the last error message to `stderr`

### Synopsis {#synopsis-159 .unnumbered .unlisted}

::: {#cb568 .sourceCode}
``` {.sourceCode .c}
#include <stdio.h>
#include <errno.h>  // only if you want to directly use the "errno" var

void perror(const char *s);
```
:::

### Description {#description-159 .unnumbered .unlisted}


Many functions, when they encounter an error condition for whatever reason, will set a global variable called `errno` (in `<errno.h>`) for you. `errno` is just an interger representing a unique error.

> 许多函数在遇到任何原因的错误条件时，会为您设置一个名为`errno`（在`<errno.h>`中）的全局变量。 `errno`只是一个表示唯一错误的整数。


But to you, the user, some number isn't generally very useful. For this reason, you can call `perror()` after an error occurs to print what error has actually happened in a nice human-readable string.

> 但是对于您这个用户来说，一些数字通常没有太大用处。因此，在发生错误后，您可以调用`perror()`来打印出实际发生的错误，以便以人类可读的字符串形式显示。


And to help you along, you can pass a parameter, `s`, that will be prepended to the error string for you.

> 为了帮助您，您可以传递一个参数's'，它将被附加到错误字符串中。


One more clever trick you can do is check the value of the `errno` (you have to include `errno.h` to see it) for specific errors and have your code do different things. Perhaps you want to ignore certain errors but not others, for instance.

> 你可以做的另一个聪明的把戏是检查`errno`的值（你必须包含`errno.h`才能看到它）以检测特定的错误，并让你的代码做出不同的反应。也许你想忽略某些错误而不忽略其他错误。


The standard only defines three values for `errno`, but your system undoubtedly defines more. The three that are defined are:

> 标准只定义了三个errno值，但你的系统无疑定义了更多。定义的三个值是：

  `errno`    Description
  ---------- -----------------------------------------------------------
  `EDOM`     Math operation outside domain.
  `EILSEQ`   Invalid sequence in multibyte to wide character encoding.
  `ERANGE`   Result of operation doesn't fit in specified type.


The catch is that different systems define different values for `errno`, so it's not very portable beyond the above 3. The good news is that at least the values are *largely* portable between Unix-like systems, at least.

> 捕获的是，不同的系统为`errno`定义了不同的值，因此它不太适用于上述3个以上的系统。好消息是，至少Unix类系统之间的值是*大致*可移植的。

### Return Value {#return-value-157 .unnumbered .unlisted}

Returns nothing at all! Sorry!

### Example {#example-160 .unnumbered .unlisted}


[`fseek()`](stdio.html#man-fseek) returns `-1` on error, and sets `errno`, so let's use it. Seeking on `stdin` makes no sense, so it should generate an error:

> `fseek()`函数在出错时返回-1，并设置`errno`，因此我们可以使用它。 对`stdin`进行搜索毫无意义，因此它应该产生一个错误：

::: {#cb569 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>
#include <errno.h> // must include this to see "errno" in this example

int main(void)
{
    if (fseek(stdin, 10L, SEEK_SET) < 0)
        perror("fseek");

    fclose(stdin); // stop using this stream

    if (fseek(stdin, 20L, SEEK_CUR) < 0) {

        // specifically check errno to see what kind of
        // error happened...this works on Linux, but your
        // mileage may vary on other systems!

        if (errno == EBADF) {
            perror("fseek again, EBADF");
        } else {
            perror("fseek again");
        }
    }
}
```
:::

And the output is:

::: {#cb570 .sourceCode}
``` {.sourceCode .default}
fseek: Illegal seek
fseek again, EBADF: Bad file descriptor
```
:::

### See Also {#see-also-151 .unnumbered .unlisted}


[`feof()`](stdio.html#man-feof), [`ferror()`](stdio.html#man-feof), [`strerror()`](stringref.html#man-strerror)

> [`feof()`](stdio.html#man-feof)：检查文件指针是否已到达文件末尾
[`ferror()`](stdio.html#man-feof)：检查文件指针是否发生错误
[`strerror()`](stringref.html#man-strerror)：返回指定错误码的错误消息字符串

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](stdint.html) \| [Contents](index.html) \| [Next](stdlib.html)
:::
