# [2] Hello, World! {#hello-world number="2"}

## [2.1] What to Expect from C {#what-to-expect-from-c number="2.1"}

> _"Where do these stairs go?"_ > _"They go up."_
> ---Ray Stantz and Peter Venkman, Ghostbusters

**C is a low-level language.**

It didn't use to be. Back in the day when people carved punch cards out of granite, C was an incredible way to be free of the drudgery of lower-level languages like [assembly](https://en.wikipedia.org/wiki/Assembly_language)[^19^].

> 以前不是这样的。 在人们用花岗岩刻出穿孔卡的日子里，C 语言是一种摆脱像汇编语言这样低级语言的苦役的不可思议的方式。

But now in these modern times, current-generation languages offer all kinds of features that didn't exist in 1972 when C was invented. This means C is a pretty basic language with not a lot of features. It can do _anything_, but it can make you work for it.

> 但是现在在这个现代时代，当前一代的语言提供了 1972 年 C 语言发明时不存在的各种功能。这意味着 C 是一种非常基础的语言，没有很多功能。它可以做任何事情，但是你需要付出努力才能实现。

So why would we even use it today?

- As a learning tool: not only is C a venerable piece of computing history, but it is connected to the [bare metal](https://en.wikipedia.org/wiki/Bare_machine)[^20^] in a way that present-day languages are not. When you learn C, you learn about how software interfaces with computer memory at a low level. There are no seatbelts. You'll write software that crashes, I assure you. And that's all part of the fun!

> 作为一种学习工具：C 不仅是一段古老的计算历史，而且它与裸机 [^20^]的连接方式，是当今语言所不具备的。当你学习 C 语言时，你会了解软件如何在低级别与计算机内存进行交互。这里没有安全带。我向你保证，你会编写出会崩溃的软件，而这也是有趣的一部分！

- As a useful tool: C still is used for certain applications, such as building [operating systems](https://en.wikipedia.org/wiki/Operating_system)[^21^] or in [embedded systems](https://en.wikipedia.org/wiki/Embedded_system)[^22^]. (Though the [Rust](https://en.wikipedia.org/wiki/Rust_(programming_language))[^23^] programming language is eyeing both these fields!)

> C 仍然被用于某些应用，如构建操作系统 [^21^]或嵌入式系统 [^22^]，作为一个有用的工具。(尽管 [Rust](https://en.wikipedia.org/wiki/Rust_(programming_language))[^23^]编程语言正在盯着这两个领域！)

If you're familiar with another language, a lot of things about C are easy. C inspired many other languages, and you'll see bits of it in Go, Rust, Swift, Python, JavaScript, Java, and all kinds of other languages. Those parts will be familiar.

> 如果你熟悉另一种语言，很多关于 C 的事情就会变得容易。C 启发了许多其他语言，你会在 Go、Rust、Swift、Python、JavaScript、Java 等各种语言中看到它的影子。这些部分你应该会熟悉。

The one thing about C that hangs people up is _pointers_. Virtually everything else is familiar, but pointers are the weird one. The concept behind pointers is likely one you already know, but C forces you to be explicit about it, using operators you've likely never seen before.

> C 的一件让人抓狂的事情就是指针。几乎其他的都很熟悉，但指针就是那个怪物。指针的概念可能你已经知道了，但 C 要求你必须明确表达，使用你以前从未见过的运算符。

It's especially insidious because once you [_grok_](https://en.wikipedia.org/wiki/Grok)[^24^] pointers, they're suddenly easy. But up until that moment, they're slippery eels.

> 它尤其阴险，因为一旦你理解指针，它们就变得很容易。但是在那一刻之前，它们就像滑溜的鳗鱼一样难以捉摸。

Everything else in C is just memorizing another way (or sometimes the same way!) of doing something you've done already. Pointers are the weird bit. And, arguably, even pointers are variations on a theme you're probably familiar with.

> 所有其他的 C 都只是记住另一种(有时是相同的方式！)去做你已经做过的事情。指针是奇怪的部分。而且，可以说，即使是指针也是你可能已经熟悉的主题的变化。

So get ready for a rollicking adventure as close to the core of the computer as you can get without assembly, in the most influential computer language of all time[^25^]. Hang on!

> 准备好迎接一段充满乐趣的冒险吧！这是一次可以让你接近计算机核心的冒险，而且使用的是史上最具影响力的计算机语言[^25^]。拭目以待吧！

## [2.2] Hello, World! {#hello-world-1 number="2.2"}

This is the canonical example of a C program. Everyone uses it. (Note that the numbers to the left are for reader reference only, and are not part of the source code.)

> 这是 C 程序的典型示例。每个人都在使用它。(注意，左侧的数字仅供读者参考，不是源代码的一部分。)

::: {#cb2 .sourceCode}

```c
/* Hello world program */

#include <stdio.h>

int main(void)
{
    printf("Hello, World!\n");  // Actually do the work here
}
```

:::

We're going to don our long-sleeved heavy-duty rubber gloves, grab a scalpel, and rip into this thing to see what makes it tick. So, scrub up, because here we go. Cutting very gently...

> 我们要穿上长袖重型橡胶手套，拿起一把手术刀，深入研究它到底是怎么回事。所以，洗洗手，因为我们要开始了。轻轻地切割...

Let's get the easy thing out of the way: anything between the digraphs `/*` and `*/` is a comment and will be completely ignored by the compiler. Same goes for anything on a line after a `//`. This allows you to leave messages to yourself and others, so that when you come back and read your code in the distant future, you'll know what the heck it was you were trying to do. Believe me, you will forget; it happens.

> 让我们先把容易的事情搞定：任何在双字符 `/*` 和 `*/` 之间的东西都是注释，编译器会完全忽略它们。在一行的 `//` 之后也是一样。这样可以给自己和其他人留言，这样当你在将来回来读你的代码时，你就知道你当时在试图做什么了。相信我，你会忘记的；这种事情经常发生。

Now, what is this `#include`? GROSS! Well, it tells the C Preprocessor to pull the contents of another file and insert it into the code right _there_.

> 现在，这是什么 `#include`？太糟糕了！嗯，它告诉 C 预处理器抓取另一个文件的内容，并将其插入到代码的那里。

Wait---what's a C Preprocessor? Good question. There are two stages[^26^] to compilation: the preprocessor and the compiler. Anything that starts with pound sign, or "octothorpe", (`#`) is something the preprocessor operates on before the compiler even gets started. Common _preprocessor directives_, as they're called, are `#include` and `#define`. More on that later.

> 等等---什么是 **C 预处理器**？好问题。编译有两个阶段：[^26^]预处理器和编译器。任何以井号开头，或者“八角”(`#`)开头的东西，都是在编译器开始之前由预处理器处理的东西。常见的 _预处理指令_，又称之为 `#include` 和 `#define`。稍后会讲到更多。

Before we go on, why would I even begin to bother pointing out that a pound sign is called an octothorpe? The answer is simple: I think the word octothorpe is so excellently funny, I have to gratuitously spread its name around whenever I get the opportunity. Octothorpe. Octothorpe, octothorpe, octothorpe.

> 在我们继续之前，为什么我要提出一个磅号被称为八角号？答案很简单：我认为八角号这个词非常有趣，每当我有机会时，我都要把它的名字传播出去。八角号。八角号，八角号，八角号。

So _anyway_. After the C preprocessor has finished preprocessing everything, the results are ready for the compiler to take them and produce [assembly code](https://en.wikipedia.org/wiki/Assembly_language)[^27^], [machine code](https://en.wikipedia.org/wiki/Machine_code)[^28^], or whatever it's about to do. Machine code is the "language" the CPU understands, and it can understand it _very rapidly_. This is one of the reasons C programs tend to be quick.

> 好吧。在预处理器完成预处理之后，结果就准备好了，编译器可以拿起它们并生成[汇编语言][^27^]、[机器码][^28^]或者它要做的任何事情。机器码是 CPU 理解的“语言”，它可以非常快速地理解它。这就是 C 程序通常很快的原因之一。

Don't worry about the technical details of compilation for now; just know that your source runs through the preprocessor, then the output of that runs through the compiler, then that produces an executable for you to run.

> 不用担心编译的技术细节，现在只需要知道你的源代码会先经过预处理器，然后输出会经过编译器，然后产生一个可以执行的程式给你。

What about the rest of the line? What's `<stdio.h>`? That is what is known as a _header file_. It's the dot-h at the end that gives it away. In fact it's the "Standard I/O" (`stdio`) header file that you will grow to know and love. It gives us access to a bunch of I/O functionality[^29^]. For our demo program, we're outputting the string "Hello, World!", so we in particular need access to the `printf()` function to do this. The `<stdio.h>` file gives us this access. Basically, if we tried to use `printf()` without `#include <stdio.h>`, the compiler would have complained to us about it.

> 其余的行呢？什么是 <stdio.h>？这就是所谓的头文件。它以.h 结尾，这就是它的特征。实际上，这是你将会熟悉和喜爱的“标准 I/O”(stdio)头文件。它给我们提供了大量的 I/O 功能[^29^]。对于我们的演示程序，我们需要输出字符串“Hello，World！”，因此我们特别需要访问 printf()函数来实现这一点。<stdio.h> 文件给了我们这种访问权限。基本上，如果我们试图在没有`#include <stdio.h>` 的情况下使用 printf()，编译器会向我们抱怨它。

How did I know I needed to `#include <stdio.h>` for `printf()`? Answer: it's in the documentation. If you're on a Unix system, `man 3 printf` and it'll tell you right at the top of the man page what header files are required. Or see the reference section in this book. `:-)`

> 我怎么知道我需要 `#include <stdio.h>` 才能使用 `printf()`？答案：**这在文档中有说明**。如果你使用的是 Unix 系统，可以输入 `man 3 printf`，它会在 man 页面的顶部告诉你需要包含哪些头文件。或者参考本书的参考资料部分。:-)

Holy moly. That was all to cover the first line! But, let's face it, it has been completely dissected. No mystery shall remain! So take a breather...look back over the sample code. Only a couple easy lines to go. Welcome back from your break! I know you didn't really take a break; I was just humoring you.

> 哇！我们已经彻底剖析了第一行！但是，让我们面对现实吧，没有任何神秘可言了！
> 所以休息一下...回顾一下样例代码。只剩下几行简单的代码了。
> 欢迎回来！我知道你没有真的休息；我只是在逗你玩。

The next line is `main()`. This is the definition of the function `main()`; everything between the squirrelly braces (`{` and `}`) is part of the function definition.

> 下一行是 `main()`。这是函数 `main()` 的定义；括号(`{` 和 `}`)之间的所有内容都是函数定义的一部分。

(How do you _call_ a different function, anyway? The answer lies in the `printf()` line, but we'll get to that in a minute.)

> 你怎么去调用一个不同的函数？答案就在 `printf()` 行里，不过我们稍后再来讨论这个问题。

Now, the main function is a special one in many ways, but one way stands above the rest: it is the function that will be called automatically when your program starts executing. Nothing of yours gets called before `main()`. In the case of our example, this works fine since all we want to do is print a line and exit.

> 现在，主函数在很多方面都是特殊的，但有一种方式高于其他方式：当你的程序开始执行时，它**将被自动调用**。在你的东西之前没有调用`main()`。在我们的例子中，这很好，因为我们要做的就是打印一行并退出。

Oh, that's another thing: once the program executes past the end of `main()`, down there at the closing squirrelly brace, the program will exit, and you'll be back at your command prompt.

> 哦，那又是另一件事：一旦程序在 `main()` 的末尾执行完毕，在那里的闭括号，程序将退出，你会回到你的命令提示符。

So now we know that that program has brought in a header file, `stdio.h`, and declared a `main()` function that will execute when the program is started. What are the goodies in `main()`?

> 现在我们知道这个程序已经引入了一个头文件 `stdio.h`，并声明了一个 `main()` 函数，当程序启动时将执行该函数。`main()` 里有什么精彩内容？

I am so happy you asked. Really! We only have the one goodie: a call to the function `printf()`. You can tell this is a function call and not a function definition in a number of ways, but one indicator is the lack of squirrelly braces after it. And you end the function call with a semicolon so the compiler knows it's the end of the expression. You'll be putting semicolons after almost everything, as you'll see.

> 我很高兴你问了。真的！我们只有一个好东西：**调用函数 `printf()`**。你可以通过多种方式来判断这是一个**函数调用而不是函数定义**，但一个指标是它后面没有多余的大括号。你要**用分号结束函数调用**，这样编译器就知道这是表达式的结尾了。你会发现**几乎每件事情都要加分号**。

You're passing one argument to the function `printf()`: a string to be printed when you call it. Oh, yeah---we're calling a function! We rock! Wait, wait---don't get cocky. What's that crazy `\n` at the end of the string? Well, most characters in the string will print out just like they are stored. But there are certain characters that you can't print on screen well that are embedded as two-character backslash codes. One of the most popular is `\n` (read "backslash-N" or simply "newline") that corresponds to the _newline_ character. This is the character that causes further printing to continue at the beginning of the next line instead of the current. It's like hitting return at the end of the line.

> 你正在给函数 `printf()` 传递一个参数：调用它时要打印的字符串。哦，是的——我们正在调用一个函数！我们太棒了！等等——不要太自负。字符串末尾的那个疯狂的 `\n` 是什么？嗯，大多数字符串中的字符都会按照它们存储的方式打印出来。但也有一些你无法在屏幕上打印的字符，它们以双字符反斜杠编码的形式嵌入。其中最常用的是 `\n`(读作“反斜杠-N”或简称“换行”)，它对应于 _换行_ 字符。这个字符会导致后续的打印继续在下一行的开头而不是当前行。就像在行末按下回车键一样。

So copy that code into a file called `hello.c` and build it. On a Unix-like platform (e.g. Linux, BSD, Mac, or WSL), from the command line you'll build with a command like so:

> 将该代码复制到一个叫做 `hello.c` 的文件中，然后进行构建。 在类 Unix 平台(例如 Linux，BSD，Mac 或 WSL)上，从命令行您将使用如下命令进行构建：

::: {#cb3 .sourceCode}

```zsh
gcc -o hello hello.c
```

:::

(This means "compile `hello.c`, and output an executable called `hello`".)

> 编译 `hello.c`，输出一个可执行文件叫做 `hello`。

After that's done, you should have a file called `hello` that you can run with this command:

> 完成之后，您应该有一个叫做 `hello` 的文件，您可以使用以下命令运行它：

::: {#cb4 .sourceCode}

```{.sourceCode .default}
./hello
```

:::

(The leading `./` tells the shell to "run from the current directory".)

And see what happens:

::: {#cb5 .sourceCode}

```{.sourceCode .default}
Hello, World!
```

:::

It's done and tested! Ship it!

## [2.3] Compilation Details {#compilation-details number="2.3"}

Let's talk a bit more about how to build C programs, and what happens behind the scenes there.

> 让我们谈谈如何构建 C 程序以及在其背后发生的事情。

Like other languages, C has _source code_. But, depending on what language you're coming from, you might never have had to _compile_ your source code into an _executable_.

> 像其他语言一样，C 有源代码。但是，根据你来自的语言，你可能从未必须将源代码编译成可执行文件。

Compilation is the process of taking your C source code and turning it into a program that your operating system can execute.

> 编译是将您的 C 源代码转换为操作系统可以执行的程序的过程。

JavaScript and Python devs aren't used to a separate compilation step at all--though behind the scenes it's happening! Python compiles your source code into something called _bytecode_ that the Python virtual machine can execute. Java devs are used to compilation, but that produces bytecode for the Java Virtual Machine.

> JavaScript 和 Python 开发人员根本不习惯独立的编译步骤--尽管在幕后它正在发生！Python 将您的源代码编译成称为_字节码_的东西，Python 虚拟机可以执行它。Java 开发人员习惯了编译，但这会为 Java 虚拟机生成字节码。

When compiling C, _machine code_ is generated. This is the 1s and 0s that can be executed directly and speedily by the CPU.

> 当编译 C 语言时，会生成_机器代码_。这是可以被 CPU 直接快速执行的 1 和 0。

> Languages that typically aren't compiled are called _interpreted_ languages. But as we mentioned with Java and Python, they also have a compilation step. And there's no rule saying that C can't be interpreted. (There are C interpreters out there!) In short, it's a bunch of gray areas. Compilation in general is just taking source code and turning it into another, more easily-executed form.

The C compiler is the program that does the compilation.

As we've already said, `gcc` is a compiler that's installed on a lot of [Unix-like operating systems](https://en.wikipedia.org/wiki/Unix)[^30^]. And it's commonly run from the command line in a terminal, but not always. You can run it from your IDE, as well.

> 我们已经说过，`GCC` 是一个安装在许多类 Unix 操作系统上的编译器。通常可以从终端的命令行运行它，但不是总是如此。您也可以从您的 IDE 中运行它。

So how do we do command line builds?

## [2.4] Building with `gcc` {#building-with-gcc number="2.4"}

If you have a source file called `hello.c` in the current directory, you can build that into a program called `hello` with this command typed in a terminal:

> 如果当前目录有一个叫做 `hello.c` 的源文件，你可以使用终端输入的这条命令把它编译成一个叫做 `hello` 的程序：

::: {#cb6 .sourceCode}

```zsh
gcc -o hello hello.c
```

:::

The `-o` means "output to this file"[^31^]. And there's `hello.c` at the end, the name of the file we want to compile.

> `-o` 意味着"输出到这个文件"[^31^]。最后有一个 `hello.c`，这是我们要编译的文件的名字。

If your source is broken up into multiple files, you can compile them all together (almost as if they were one file, but the rules are actually more complex than that) by putting all the `.c` files on the command line:

> 如果您的源代码分成多个文件，您可以将它们全部编译在一起(几乎就像是一个文件，但实际上规则比这更复杂)，只需将所有 `.c` 文件放在命令行上：

::: {#cb7 .sourceCode}

```zsh
gcc -o awesomegame ui.c characters.c npc.c items.c
```

:::

and they'll all get built together into a big executable.

That's enough to get started---later we'll talk details about multiple source files, object files, and all kinds of fun stuff.

> 够了，开始吧---稍后我们会讨论关于多个源文件、目标文件以及各种有趣的东西的细节。

## [2.5] Building with `clang` {#building-with-clang number="2.5"}

On Macs, the stock compiler isn't `gcc`---it's `clang`. But a wrapper is also installed so you can run `gcc` and have it still work.

> 在 Mac 上，默认的编译器不是 gcc，而是 clang。但是也安装了一个包装器，所以你可以运行 gcc，它仍然可以正常工作。

You can also install the `gcc` compiler proper through [Homebrew](https://formulae.brew.sh/formula/gcc)[^32^] or some other means.

> 你也可以通过 [Homebrew][^32^]或其他方式正确安装 `gcc` 编译器。

## [2.6] Building from IDEs {#building-from-ides number="2.6"}

If you're using an _Integrated Development Environment_ (IDE), you probably don't have to build from the command line.

> 如果你使用集成开发环境(IDE)，你可能不需要从命令行构建。

With Visual Studio, `CTRL-F7` will build, and `CTRL-F5` will run.

With VS Code, you can hit `F5` to run via the debugger. (You'll have to install the C/C++ Extension.)

> 使用 VS Code，您可以按下 `F5` 来通过调试器运行(您需要安装 C/C++ 扩展)。

With XCode, you can build with `COMMAND-B` and run with `COMMAND-R`. To get the command line tools, Google for "XCode command line tools" and you'll find instructions for installing them.

> 使用 XCode，您可以使用 `COMMAND-B` 构建，并使用 `COMMAND-R` 运行。要获取命令行工具，请在 Google 上搜索“XCode 命令行工具”，您将找到安装说明。

For getting started, I encourage you to also try to build from the command line---it's history!

> 为了开始，我鼓励你也尝试从命令行构建---这是历史！

## [2.7] C Versions {#c-versions number="2.7"}

C has come a long way over the years, and it had many named version numbers to describe which dialect of the language you're using.

> C 在过去的几年里取得了很大的进步，它有许多命名的版本号来描述您正在使用的语言方言。

These generally refer to the year of the specification.

The most famous are C89, C99, C11, and C2x. We'll focus on the latter in this book.

> 最着名的是 C89、C99、C11 和 C2x。我们将在本书中主要关注后者。

But here's a more complete table:

---

Version Description

---

K&R C 1978, the original. Named after Brian Kernighan and Dennis Ritchie. Ritchie designed and coded the language, and Kernighan co-authored the book on it. You rarely see original K&R code today. If you do, it'll look odd, like Middle English looks odd to modern English readers.

> 1978 年的 K&R C，最初的版本。以布莱恩·克尼根和丹尼斯·里奇的名字命名。里奇设计和编写了这门语言，克尼根共同撰写了有关它的书籍。如今，你很少能看到原始的 K&R 代码。如果你看到了，它会看起来很奇怪，就像中世纪英语对现代英语读者来说看起来很奇怪一样。

**C89**, ANSI C, C90 In 1989, the American National Standards Institute (ANSI) produced a C language specification that set the tone for C that persists to this day. A year later, the reins were handed to the International Organization for Standardization (ISO) that produced the identical C90.

> 1989 年，美国国家标准学会(ANSI)制定了一项 C 语言规范，为当今的 C 语言设定了基调。一年后，国际标准化组织(ISO)接管，制定了相同的 C90。

C95 A rarely-mentioned addition to C89 that included wide character support.

> C95 是 C89 的一个很少提及的补充，它包括对宽字符的支持。

**C99** The first big overhaul with lots of language additions. The thing most people remember is the addition of `//`-style comments. This is the most popular version of C in use as of this writing.

> **C99** 第一次大规模的改版，增加了许多语言特性。大多数人记得的是增加了 `//`-风格的注释。这是目前使用最广泛的 C 版本。

**C11** This major version update includes Unicode support and multi-threading. Be advised that if you start using these language features, you might be sacrificing portability with places that are stuck in C99 land. But, honestly, 1999 is getting to be a while back now.

> **C11** 这个主要版本更新**包括 Unicode 支持和多线程**。请注意，如果你开始使用这些语言特性，可能会牺牲可移植性，因为一些地方仍然停留在 C99 版本。但是，说实话，1999 年已经有一段时间了。

C17, C18 Bugfix update to C11. C17 seems to be the official name, but the publication was delayed until 2018. As far as I can tell, these two are interchangeable, with C17 being preferred.

> C17、C18 错误修复更新到 C11。C17 似乎是官方名称，但发布被推迟到 2018 年。据我所知，这两者是可以互换的，优先使用 C17。

## C2x What's coming next! Expected to eventually become C23.

You can force GCC to use one of these standards with the `-std=` command line argument. If you want it to be picky about the standard, add `-pedantic`.

> 你可以使用 `-std=` 命令行参数强制 GCC 使用其中一个标准。如果你希望它对标准挑剔，请添加 `-pedantic`。

For example:

::: {#cb8 .sourceCode}

```zsh
gcc -std=c11 -pedantic foo.c
```

:::

For this book, I compile programs for C2x with all warnings set:

::: {#cb9 .sourceCode}

```zsh
gcc -Wall -Wextra -std=c2x -pedantic foo.c
```

:::
