---
tip: translate by openai@2023-07-20 18:22:19
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}

[Prev](index.html) \| [Contents](index.html) \| [Next](the-c-language.html)

> [上一页](index.html) \| [目录](index.html) \| [下一页](the-c-language.html)
:::

------------------------------------------------------------------------

# [1]{.header-section-number} Foreword {#foreword number="1"}


The door slowly creaks open revealing a long hall with dusty stacks of books of lore...

> 门缓缓地吱吱作响，露出一条满是灰尘的书籍传说的长廊...

I admit, maybe not that.

But you have found the Library Reference portion of Beej's Guide to C!


This isn't a tutorial, but rather is a comprehensive set of manual pages (or *man pages* as Unix hackers like to say) that define *every* function in the C Standard Library, complete with examples.

> 这不是一个教程，而是一组完整的手册页（或者Unix黑客喜欢说的*man页*），它们定义了C标准库中的每个函数，并附有示例。

> *"This book, sir, contains every word in our beloved language."*\
> *"Every single one, sir?"*\
> *"Every single one, sir!"*\
> *"Ah, well in that case, sir, I hope you will not object if I also offer the doctor my most enthusiastic contrafribularities."*
>
> --Blackadder toying with Dr. Samuel Johnson


There are, in fact, a number of functions left out of this guide, most notably all the optional "safe" functions (with a `_s` suffix).

> 实际上，本指南中有许多功能没有提及，尤其是所有可选的“安全”函数（带有`_s`后缀）。


But everything you're likely to want is definitely covered in here. With examples.

> 但是你可能想要的一切都在这里有所涵盖，并且有示例。

Probably.

## [1.1]{.header-section-number} Audience {#audience number="1.1"}

This guide is for people who are at least modestly proficient in C.


If you are not one of those people and wish to become one of those people, I can wholeheartedly recommend with zero bias the book [*Beej's Guide to C Programming*](https://beej.us/guide/bgc/)[^1^](footnotes.html#fn1){#fnref1 .footnote-ref role="doc-noteref"}, freely available wherever the Internet is sold.

> 如果你不是其中的一员，而希望成为其中的一员，我可以完全推荐没有偏见的书籍《Beej's Guide to C Programming》，可以在任何互联网销售网站免费获取。

## [1.2]{.header-section-number} How to Read This Book {#how-to-read-this-book number="1.2"}

Use the contents or index to find the function or category you're after.


Then grab a bowl of your favorite cereal and devour the delicious, delicious verbiage.

> 接着拿一碗你最喜欢的谷物，享受美味的语言。

## [1.3]{.header-section-number} Platform and Compiler {#platform-and-compiler number="1.3"}


I'll try to stick to Plain Ol'-Fashioned [ISO-standard C](https://en.wikipedia.org/wiki/ANSI_C)[^2^](footnotes.html#fn2){#fnref2 .footnote-ref role="doc-noteref"}. Well, for the most part. Here and there I might go crazy and start talking about [POSIX](https://en.wikipedia.org/wiki/POSIX)[^3^](footnotes.html#fn3){#fnref3 .footnote-ref role="doc-noteref"} or something, but we'll see.

> 我会尽量使用普通的ISO标准C（https://en.wikipedia.org/wiki/ANSI_C）[^2^]（footnotes.html#fn2）{#fnref2 .footnote-ref role="doc-noteref"}。大部分时候是如此。有时候我可能会疯狂地开始谈论[POSIX](https://en.wikipedia.org/wiki/POSIX)[^3^]（footnotes.html#fn3）{#fnref3 .footnote-ref role="doc-noteref"}或其他东西，但我们拭目以待吧。


**Unix** users (e.g. Linux, BSD, etc.) try running `cc` or `gcc` from the command line--you might already have a compiler installed. If you don't, search your distribution for installing `gcc` or `clang`.

> **Unix** 用户（例如Linux、BSD等）可以从命令行运行`cc`或`gcc`--您可能已经安装了编译器。如果没有，请搜索您的发行版本以安装`gcc`或`clang`。


**Windows** users should check out [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/)[^4^](footnotes.html#fn4){#fnref4 .footnote-ref role="doc-noteref"}. Or, if you're looking for a more Unix-like experience (recommended!), install [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)[^5^](footnotes.html#fn5){#fnref5 .footnote-ref role="doc-noteref"} and `gcc`.

> Windows 用户应该查看[Visual Studio Community](https://visualstudio.microsoft.com/vs/community/)[^4^](footnotes.html#fn4){#fnref4 .footnote-ref role="doc-noteref"}。或者，如果您正在寻找更类Unix的体验（推荐！），请安装[WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)[^5^](footnotes.html#fn5){#fnref5 .footnote-ref role="doc-noteref"}和`gcc`。


**Mac** users will want to install [XCode](https://developer.apple.com/xcode/)[^6^](footnotes.html#fn6){#fnref6 .footnote-ref role="doc-noteref"}, and in particular the command line tools.

> **Mac** 用户需要安装[XCode](https://developer.apple.com/xcode/)[^6^](footnotes.html#fn6){#fnref6 .footnote-ref role="doc-noteref"}，特别是命令行工具。


There are a lot of compilers out there, and virtually all of them will work for this book. And a C++ compiler will compile a lot of (but not all!) C code. Best use a proper C compiler if you can.

> 在市面上有很多编译器，几乎所有的都可以用于本书。C++编译器可以编译很多（但不是全部！）C代码。如果可以的话，最好使用正确的C编译器。

## [1.4]{.header-section-number} Official Homepage {#official-homepage number="1.4"}


This official location of this document is [`https://beej.us/guide/bgclr/`](https://beej.us/guide/bgclr/)[^7^](footnotes.html#fn7){#fnref7 .footnote-ref role="doc-noteref"}. There used to be a note here about migrating off Chico State's computers (my alma mater), but that's something that happened roughly a zillion years ago and the wording remained here only because it was copied over from the Network Guide, \[*breath*\] which I apparently haven't read in its entirety for quite some time.

> 这份文件的官方位置是[https://beej.us/guide/bgclr/](https://beej.us/guide/bgclr/)[^7^](footnotes.html#fn7){#fnref7 .footnote-ref role="doc-noteref"}。过去这里有一个关于从我的母校Chico State的计算机迁移的注释，但那是大约一千年前发生的事情，而且这里的措辞仅仅是从网络指南中复制过来的，[*呼吸*] 显然我已经很长一段时间没有完整地阅读过它了。

The End.

## [1.5]{.header-section-number} Email Policy {#email-policy number="1.5"}


I'm generally available to help out with email questions so feel free to write in, but I can't guarantee a response. I lead a pretty busy life and there are times when I just can't answer a question you have. When that's the case, I usually just delete the message. It's nothing personal; I just won't ever have the time to give the detailed answer you require.

> 我通常可以帮助回答邮件问题，所以随时可以写信给我，但我不能保证一定会有回复。我的生活很忙碌，有时候我根本没时间回答你的问题。那种情况下，我通常会直接删除邮件。这没有什么个人意思，只是我根本没有时间给你更详细的回答。


As a rule, the more complex the question, the less likely I am to respond. If you can narrow down your question before mailing it and be sure to include any pertinent information (like platform, compiler, error messages you're getting, and anything else you think might help me troubleshoot), you're much more likely to get a response.

> 一般来说，问题越复杂，我回答的可能性就越低。如果你在发邮件之前能够缩小问题的范围，并确保包括所有相关信息（比如平台，编译器，错误信息以及你认为可能有助于我调试的其他任何信息），你更有可能得到回复。


If you don't get a response, hack on it some more, try to find the answer, and if it's still elusive, then write me again with the information you've found and hopefully it will be enough for me to help out.

> 如果你没有得到回复，请继续努力，尝试找到答案，如果仍然找不到，请再次给我写信，告诉我你已经发现的信息，希望这些信息足以帮助我。


Now that I've badgered you about how to write and not write me, I'd just like to let you know that I *fully* appreciate all the praise the guide has received over the years. It's a real morale boost, and it gladdens me to hear that it is being used for good! `:-)` Thank you!

> 现在我已经向你们唠叨了关于如何写信给我以及不要写信给我的事情，我只想让你们知道，我*完全*欣赏这本指南多年来获得的赞誉。这真是一种士气的提升，听到它被用于善良的事情，我也感到高兴！:-) 谢谢！

## [1.6]{.header-section-number} Mirroring {#mirroring number="1.6"}


You are more than welcome to mirror this site, whether publicly or privately. If you publicly mirror the site and want me to link to it from the main page, drop me a line at [`beej@beej.us`](mailto:beej@beej.us).

> 您可以自由地公开或私下镜像本站，您可以从主页上链接到它，请给我发送电子邮件至[`beej@beej.us`](mailto:beej@beej.us)。

## [1.7]{.header-section-number} Note for Translators {#note-for-translators number="1.7"}


If you want to translate the guide into another language, write me at [`beej@beej.us`](beej@beej.us) and I'll link to your translation from the main page. Feel free to add your name and contact info to the translation.

> 如果您想将指南翻译成另一种语言，请在[`beej@beej.us`](beej@beej.us)给我写信，我会在主页上链接到您的翻译。欢迎您在翻译中添加您的姓名和联系信息。


Please note the license restrictions in the Copyright and Distribution section, below.

> 请注意下面版权和发行部分的许可限制。

## [1.8]{.header-section-number} Copyright and Distribution {#copyright-and-distribution number="1.8"}


Beej's Guide to C Programming--Library Reference is Copyright © 2021 Brian "Beej Jorgensen" Hall.

> 《Beej的C编程指南--库参考》版权所有©2021 Brian "Beej Jorgensen" Hall.


With specific exceptions for source code and translations, below, this work is licensed under the Creative Commons Attribution-Noncommercial-No Derivative Works 3.0 License. To view a copy of this license, visit [`https://creativecommons.org/licenses/by-nc-nd/3.0/`](https://creativecommons.org/licenses/by-nc-nd/3.0/) or send a letter to Creative Commons, 171 Second Street, Suite 300, San Francisco, California, 94105, USA.

> 除源代码和翻译外，本作品根据知识共享署名-非商业性使用-禁止演绎 3.0 许可协议授权。查看此许可协议的副本，请访问[https://creativecommons.org/licenses/by-nc-nd/3.0/](https://creativecommons.org/licenses/by-nc-nd/3.0/) 或发送信件至知识共享，地址为：171 Second Street, Suite 300, San Francisco, California, 94105, USA.


One specific exception to the "No Derivative Works" portion of the license is as follows: this guide may be freely translated into any language, provided the translation is accurate, and the guide is reprinted in its entirety. The same license restrictions apply to the translation as to the original guide. The translation may also include the name and contact information for the translator.

> 例外情况：本指南可以被自由翻译成任何语言，只要翻译准确，并且指南完整地被重印。翻译也要遵守原指南的许可限制。翻译中也可以包括翻译者的姓名和联系方式。


The C source code presented in this document is hereby granted to the public domain, and is completely free of any license restriction.

> 本文档中所示的C源代码特此授予公共领域，完全免除任何许可限制。


Educators are freely encouraged to recommend or supply copies of this guide to their students.

> 教育工作者可以自由地鼓励推荐或提供本指南的副本给他们的学生。

Contact [`beej@beej.us`](beej@beej.us) for more information.

## [1.9]{.header-section-number} Dedication {#dedication number="1.9"}

The hardest things about writing these guides are:

-   Learning the material in enough detail to be able to explain it
-   Figuring out the best way to explain it clearly, a seemingly-endless iterative process

-   Putting myself out there as a so-called *authority*, when really I'm just a regular human trying to make sense of it all, just like everyone else

> 我把自己放在那里，作为一个所谓的权威，其实我只是一个普通的人，像其他人一样，努力去理解这一切。
-   Keeping at it when so many other things draw my attention


A lot of people have helped me through this process, and I want to acknowledge those who have made this book possible.

> 许多人在这个过程中帮助了我，我要感谢那些使这本书成为可能的人。


-   Everyone on the Internet who decided to help share their knowledge in one form or another. The free sharing of instructive information is what makes the Internet the great place that it is.

> 所有在互联网上决定帮助分享他们的知识以某种形式或另一种形式的人。免费分享指导信息是使互联网成为伟大之处的原因。

-   The volunteers at [cppreference.com](https://en.cppreference.com/)[^8^](footnotes.html#fn8){#fnref8 .footnote-ref role="doc-noteref"} who provide the bridge that leads from the spec to the real world.

> 志愿者们在cppreference.com上提供了一座桥梁，将规范与现实世界连接起来。

-   The helpful and knowledgeable folks on [comp.lang.c](https://groups.google.com/g/comp.lang.c)[^9^](footnotes.html#fn9){#fnref9 .footnote-ref role="doc-noteref"} and [r/C_Programming](https://www.reddit.com/r/C_Programming/)[^10^](footnotes.html#fn10){#fnref10 .footnote-ref role="doc-noteref"} who got me through the tougher parts of the language.

> 非常有帮助和知识渊博的[comp.lang.c](https://groups.google.com/g/comp.lang.c)[^9^](footnotes.html#fn9){#fnref9 .footnote-ref role="doc-noteref"}和[r/C_Programming](https://www.reddit.com/r/C_Programming/)[^10^](footnotes.html#fn10){#fnref10 .footnote-ref role="doc-noteref"}的人们帮助我完成了语言的更难部分。

-   Everyone who submitted corrections and pull-requests on everything from misleading instructions to typos.

> 所有提交了纠正和拉取请求的人，从误导性指令到拼写错误都有。

Thank you! ♥

------------------------------------------------------------------------

::: {style="text-align:center"}

[Prev](index.html) \| [Contents](index.html) \| [Next](the-c-language.html)

> [上一页](index.html) \| [目录](index.html) \| [下一页](the-c-language.html)
:::
