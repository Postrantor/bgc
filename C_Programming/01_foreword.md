
# [1] Foreword {#foreword number="1"}

> _C is not a big language, and it is not well served by a big book._
>
> --Brian W. Kernighan, Dennis M. Ritchie

No point in wasting words here, folks, let's jump straight into the C code:

> 没有必要在这里浪费话语，伙计们，让我们直接跳到 C 代码：

::: {#cb1 .sourceCode}

```c
E((ck?main((z?(stat(M,&t)?P+=a+'{'?0:3:
execv(M,k),a=G,i=P,y=G&255,
sprintf(Q,y/'@'-3?A(*L(V(%d+%d)+%d,0)
```

:::

And they lived happily ever after. The End.

What's this? You say something's still not clear about this whole C programming language thing?

> 这是什么？你说关于这个 C 编程语言的事情还不清楚？

Well, to be quite honest, I'm not even sure what the above code does. It's a snippet from one of the entries in the 2001 [International Obfuscated C Code Contest](https://www.ioccc.org/)[^1^], a wonderful competition wherein the entrants attempt to write the most unreadable C code possible, with often surprising results.

> 嗯，老实说，我甚至不确定上面的代码是做什么的。这是 2001 年[国际 C 代码混淆比赛](https://www.ioccc.org/)[^1^]中的一个条目的片段，这是一个很棒的比赛，参赛者试图编写尽可能不可读的 C 代码，结果常常令人惊讶。

The bad news is that if you're a beginner in this whole thing, all C code you see probably looks obfuscated! The good news is, it's not going to be that way for long.

> 坏消息是，如果你是这一切的新手，你看到的所有 C 代码可能看起来很晦涩难懂！好消息是，这种情况不会持续太久。

What we'll try to do over the course of this guide is lead you from complete and utter sheer lost confusion on to the sort of enlightened bliss that can only be obtained through pure C programming. Right on.

> 我们在本指南中将尝试做的是，带领你从完全迷失的混乱中走向只能通过纯 C 编程获得的开明的幸福。就是这样。

In the old days, C was a simpler language. A good number of the features contained in this book and a _lot_ of the features in the Library Reference volume didn't exist when K&R wrote the famous second edition of their book in 1988. Nevertheless, the language remains small at its core, and I hope I've presented it here in a way that starts with that simple core and builds outward.

> 在过去，C 是一种更简单的语言。本书中包含的许多功能以及库参考手册中的大量功能在 1988 年 K＆R 写下着名的第二版书籍时都不存在。尽管如此，该语言在其核心处仍然很小，我希望我在这里以一种从简单的核心开始并向外构建的方式呈现它。

And that's my excuse for writing such a hilariously large book for such a small, concise language.

> 这就是我为什么要为如此简洁的语言写一本如此巨大又滑稽的书的借口。

## [1.1] Audience {#audience number="1.1"}

This guide assumes that you've already got some programming knowledge under your belt from another language, such as [Python](https://en.wikipedia.org/wiki/Python_(programming_language))[^2^], [JavaScript](https://en.wikipedia.org/wiki/JavaScript)[^3^], [Java](https://en.wikipedia.org/wiki/Java_(programming_language))[^4^], [Rust](https://en.wikipedia.org/wiki/Rust_(programming_language))[^5^], [Go](https://en.wikipedia.org/wiki/Go_(programming_language))[^6^], [Swift](https://en.wikipedia.org/wiki/Swift_(programming_language))[^7^], etc. ([Objective-C](https://en.wikipedia.org/wiki/Objective-C)[^8^] devs will have a particularly easy time of it!)

> 本指南假定你已经从另一种语言，如 [Python](https://en.wikipedia.org/wiki/Python_(programming_language))[^2^], [JavaScript](https://en.wikipedia.org/wiki/JavaScript)[^3^], [Java](https://en.wikipedia.org/wiki/Java_(programming_language))[^4^], [Rust](https://en.wikipedia.org/wiki/Rust_(programming_language))[^5^], [Go](https://en.wikipedia.org/wiki/Go_(programming_language))[^6^], [Swift](https://en.wikipedia.org/wiki/Swift_(programming_language))[^7^]等中获得了一些编程知识([Objective-C](https://en.wikipedia.org/wiki/Objective-C)[^8^]开发人员将特别容易！)。

We're going to assume you know what variables are, what loops do, how functions work, and so on.

> 我们假设你知道变量是什么，循环做什么，函数是如何工作的等等。

If that's not you for whatever reason the best I can hope to provide is some honest entertainment for your reading pleasure. The only thing I can reasonably promise is that this guide won't end on a cliffhanger... or _will_ it?

> 如果不是你的原因，我最多能提供的就是一些诚实的娱乐，以供你阅读。我唯一可以合理承诺的是，这份指南不会以悬念结尾...还是会？

## [1.2] How to Read This Book {#how-to-read-this-book number="1.2"}

The guide is in two volumes, and this is the first: the tutorial volume!

The second volume is the [library reference](https://beej.us/guide/bgclr/)[^9^], and it's far more reference than tutorial.

> 第二卷是[图书馆参考](https://beej.us/guide/bgclr/)[^9^], 它比教程更具参考价值。

If you're new, go through the tutorial part in order, generally. The higher you get in chapters, the less important it is to go in order.

> 如果你是新手，一般来说，要按照教程部分的顺序进行操作。随着章节的增加，按照顺序操作的重要性就会降低。

And no matter your skill level, the reference part is there with complete examples of the standard library function calls to help refresh your memory whenever needed. Good for reading over a bowl of cereal or other time.

> 无论您的技能水平如何，参考部分都提供了标准库函数调用的完整示例，以帮助您在需要时重新清晰记忆。很适合在吃麦片或其他时间阅读。

Finally, glancing at the index (if you're reading the print version), the reference section entries are italicized.

> 最后，如果你正在阅读印刷版本，瞥一眼索引，参考节条目用斜体字。

## [1.3] Platform and Compiler {#platform-and-compiler number="1.3"}

I'll try to stick to Plain Ol'-Fashioned [ISO-standard C](https://en.wikipedia.org/wiki/ANSI_C)[^10^]. Well, for the most part. Here and there I might go crazy and start talking about [POSIX](https://en.wikipedia.org/wiki/POSIX)[^11^] or something, but we'll see.

> 我会尽量只使用普通的 ISO 标准 C(参见维基百科：ANSI C)。大部分时候是这样，但有时候我可能会疯狂一点，开始谈论 POSIX(参见维基百科：POSIX)或其他的东西，但我们拭目以待。

**Unix** users (e.g. Linux, BSD, etc.) try running `cc` or `gcc` from the command line--you might already have a compiler installed. If you don't, search your distribution for installing `gcc` or `clang`.

> **Unix** 用户(例如 Linux、BSD 等)可以尝试从命令行运行 `cc` 或 `gcc`--您可能已经安装了编译器。如果没有，请在您的发行版中搜索安装 `gcc` 或 `clang`。

**Windows** users should check out [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/)[^12^]. Or, if you're looking for a more Unix-like experience (recommended!), install [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)[^13^] and `gcc`.

> Windows 用户应该查看 [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/)[^12^]。或者，如果您正在寻找更类 Unix 的体验(推荐！)，安装 [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)[^13^]和 `gcc`。

**Mac** users will want to install [XCode](https://developer.apple.com/xcode/)[^14^], and in particular the command line tools.

> **Mac** 用户需要安装 [XCode](https://developer.apple.com/xcode/)[^14^]，尤其是命令行工具。

There are a lot of compilers out there, and virtually all of them will work for this book. And a C++ compiler will compile a lot of (but not all!) C code. Best use a proper C compiler if you can.

> 有很多编译器可供选择，几乎所有的编译器都可以用于本书。C++ 编译器可以编译很多(但不是全部！)C 代码。如果可以的话，最好使用一个正确的 C 编译器。

## [1.4] Official Homepage {#official-homepage number="1.4"}

This official location of this document is [https://beej.us/guide/bgc/](https://beej.us/guide/bgc/)[^15^]. Maybe this'll change in the future, but it's more likely that all the other guides are migrated off Chico State computers.

> 这份文件的官方位置是 [https://beej.us/guide/bgc/](https://beej.us/guide/bgc/)[^15^]。也许这会在未来改变，但更有可能的是，所有其他指南都会迁移到 Chico State 计算机上。

## [1.5] Email Policy {#email-policy number="1.5"}

I'm generally available to help out with email questions so feel free to write in, but I can't guarantee a response. I lead a pretty busy life and there are times when I just can't answer a question you have. When that's the case, I usually just delete the message. It's nothing personal; I just won't ever have the time to give the detailed answer you require.

> 一般来说，我可以帮助处理电子邮件问题，所以随时可以写信给我，但我不能保证一定会有回复。我的生活很忙碌，有时候我就是无法回答你的问题。在这种情况下，我通常会直接删除邮件。这不是个人原因，只是我没有时间给出你所需要的详细答案。

As a rule, the more complex the question, the less likely I am to respond. If you can narrow down your question before mailing it and be sure to include any pertinent information (like platform, compiler, error messages you're getting, and anything else you think might help me troubleshoot), you're much more likely to get a response.

> 一般来说，问题越复杂，我回答的可能性就越小。如果你在发邮件之前能够缩小问题的范围，并确保包括所有相关信息(比如平台、编译器、错误信息以及你认为可能有助于我调试的其他任何信息)，你更有可能得到回复。

If you don't get a response, hack on it some more, try to find the answer, and if it's still elusive, then write me again with the information you've found and hopefully it will be enough for me to help out.

> 如果您没有得到回复，请继续努力，尝试找到答案，如果仍然无法解决，请再次给我发送您找到的信息，希望这些信息足以帮助我。

Now that I've badgered you about how to write and not write me, I'd just like to let you know that I _fully_ appreciate all the praise the guide has received over the years. It's a real morale boost, and it gladdens me to hear that it is being used for good! `:-)` Thank you!

> 现在我已经向你们唠叨了关于如何写信给我，我只想让你们知道，我完全欣赏这本指南多年来所获得的赞誉。这是一种真正的士气提振，听到它被用于善良的事情，我感到高兴！:-) 谢谢！

## [1.6] Mirroring {#mirroring number="1.6"}

You are more than welcome to mirror this site, whether publicly or privately. If you publicly mirror the site and want me to link to it from the main page, drop me a line at [`beej@beej.us`](mailto:beej@beej.us).

> 您可以公开或私下镜像本站，欢迎您的加入。如果您公开镜像本站，并希望我在主页上为您链接，请发送邮件至[`beej@beej.us`](mailto:beej@beej.us)。

## [1.7] Note for Translators {#note-for-translators number="1.7"}

If you want to translate the guide into another language, write me at [`beej@beej.us`](beej@beej.us) and I'll link to your translation from the main page. Feel free to add your name and contact info to the translation.

> 如果您想将指南翻译成另一种语言，请给我发邮件至[`beej@beej.us`](beej@beej.us)，我会在主页上链接到您的翻译。您可以在翻译中添加您的名字和联系信息。

Please note the license restrictions in the Copyright and Distribution section, below.

> 请注意下面版权和发行部分的许可限制。

## [1.8] Copyright and Distribution {#copyright-and-distribution number="1.8"}

Beej's Guide to C is Copyright © 2021 Brian "Beej Jorgensen" Hall.

With specific exceptions for source code and translations, below, this work is licensed under the Creative Commons Attribution-Noncommercial-No Derivative Works 3.0 License. To view a copy of this license, visit [`https://creativecommons.org/licenses/by-nc-nd/3.0/`](https://creativecommons.org/licenses/by-nc-nd/3.0/) or send a letter to Creative Commons, 171 Second Street, Suite 300, San Francisco, California, 94105, USA.

> 除源代码和翻译外，本作品根据知识共享署名-非商业性使用-禁止演绎 3.0 许可协议授权。要查看此许可协议的副本，请访问 [https://creativecommons.org/licenses/by-nc-nd/3.0/](https://creativecommons.org/licenses/by-nc-nd/3.0/) 或发送信函至知识共享，地址为：171 Second Street, Suite 300, San Francisco, California, 94105, USA.

One specific exception to the "No Derivative Works" portion of the license is as follows: this guide may be freely translated into any language, provided the translation is accurate, and the guide is reprinted in its entirety. The same license restrictions apply to the translation as to the original guide. The translation may also include the name and contact information for the translator.

> 例外情况：本指南可被自由翻译成任何语言，只要翻译准确，并且指南被完整地重印。对翻译的许可限制与原指南相同。翻译也可以包括翻译者的姓名和联系信息。

The C source code presented in this document is hereby granted to the public domain, and is completely free of any license restriction.

> 本文档中提供的 C 源代码特此授予公共领域，完全免于任何许可限制。

Educators are freely encouraged to recommend or supply copies of this guide to their students.

> 教育工作者可自由推荐或提供本指南的副本给他们的学生。

Contact [`beej@beej.us`](beej@beej.us) for more information.

## [1.9] Dedication {#dedication number="1.9"}

The hardest things about writing these guides are:

- Learning the material in enough detail to be able to explain it
- Figuring out the best way to explain it clearly, a seemingly-endless iterative process
- Putting myself out there as a so-called _authority_, when really I'm just a regular human trying to make sense of it all, just like everyone else

> 我自称是一个权威，其实我只是一个和其他人一样，努力理解这一切的普通人。

- Keeping at it when so many other things draw my attention

A lot of people have helped me through this process, and I want to acknowledge those who have made this book possible.

> 许多人在这个过程中帮助了我，我要感谢那些使这本书成为可能的人。

- Everyone on the Internet who decided to help share their knowledge in one form or another. The free sharing of instructive information is what makes the Internet the great place that it is.

> 所有在互联网上决定帮助分享他们的知识以某种形式或另一种形式的人。免费分享指导信息是使互联网成为伟大的地方的原因。

- The volunteers at [cppreference.com](https://en.cppreference.com/)[^16^] who provide the bridge that leads from the spec to the real world.

> 志愿者们在 cppreference.com 上提供了一座桥梁，将规范与现实世界联系起来。

- The helpful and knowledgeable folks on [comp.lang.c](https://groups.google.com/g/comp.lang.c)[^17^] and [r/C_Programming](https://www.reddit.com/r/C_Programming/)[^18^] who got me through the tougher parts of the language.

> 人们在 [comp.lang.c](https://groups.google.com/g/comp.lang.c)[^17^]和 [r/C_Programming](https://www.reddit.com/r/C_Programming/)[^18^]上提供的有用和知识渊博的帮助让我完成了语言的更困难的部分。

- Everyone who submitted corrections and pull-requests on everything from misleading instructions to typos.

> 所有提交了纠正和拉取请求的人，从误导性指令到拼写错误，都有所帮助。

Thank you! ♥
