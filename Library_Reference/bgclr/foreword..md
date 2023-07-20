---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](index.html) \| [Contents](index.html) \| [Next](the-c-language.html)
:::

------------------------------------------------------------------------

# [1]{.header-section-number} Foreword {#foreword number="1"}

The door slowly creaks open revealing a long hall with dusty stacks of books of lore...

I admit, maybe not that.

But you have found the Library Reference portion of Beej's Guide to C!

This isn't a tutorial, but rather is a comprehensive set of manual pages (or *man pages* as Unix hackers like to say) that define *every* function in the C Standard Library, complete with examples.

> *"This book, sir, contains every word in our beloved language."*\
> *"Every single one, sir?"*\
> *"Every single one, sir!"*\
> *"Ah, well in that case, sir, I hope you will not object if I also offer the doctor my most enthusiastic contrafribularities."*
>
> --Blackadder toying with Dr. Samuel Johnson

There are, in fact, a number of functions left out of this guide, most notably all the optional "safe" functions (with a `_s` suffix).

But everything you're likely to want is definitely covered in here. With examples.

Probably.

## [1.1]{.header-section-number} Audience {#audience number="1.1"}

This guide is for people who are at least modestly proficient in C.

If you are not one of those people and wish to become one of those people, I can wholeheartedly recommend with zero bias the book [*Beej's Guide to C Programming*](https://beej.us/guide/bgc/)[^1^](footnotes.html#fn1){#fnref1 .footnote-ref role="doc-noteref"}, freely available wherever the Internet is sold.

## [1.2]{.header-section-number} How to Read This Book {#how-to-read-this-book number="1.2"}

Use the contents or index to find the function or category you're after.

Then grab a bowl of your favorite cereal and devour the delicious, delicious verbiage.

## [1.3]{.header-section-number} Platform and Compiler {#platform-and-compiler number="1.3"}

I'll try to stick to Plain Ol'-Fashioned [ISO-standard C](https://en.wikipedia.org/wiki/ANSI_C)[^2^](footnotes.html#fn2){#fnref2 .footnote-ref role="doc-noteref"}. Well, for the most part. Here and there I might go crazy and start talking about [POSIX](https://en.wikipedia.org/wiki/POSIX)[^3^](footnotes.html#fn3){#fnref3 .footnote-ref role="doc-noteref"} or something, but we'll see.

**Unix** users (e.g. Linux, BSD, etc.) try running `cc` or `gcc` from the command line--you might already have a compiler installed. If you don't, search your distribution for installing `gcc` or `clang`.

**Windows** users should check out [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/)[^4^](footnotes.html#fn4){#fnref4 .footnote-ref role="doc-noteref"}. Or, if you're looking for a more Unix-like experience (recommended!), install [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)[^5^](footnotes.html#fn5){#fnref5 .footnote-ref role="doc-noteref"} and `gcc`.

**Mac** users will want to install [XCode](https://developer.apple.com/xcode/)[^6^](footnotes.html#fn6){#fnref6 .footnote-ref role="doc-noteref"}, and in particular the command line tools.

There are a lot of compilers out there, and virtually all of them will work for this book. And a C++ compiler will compile a lot of (but not all!) C code. Best use a proper C compiler if you can.

## [1.4]{.header-section-number} Official Homepage {#official-homepage number="1.4"}

This official location of this document is [`https://beej.us/guide/bgclr/`](https://beej.us/guide/bgclr/)[^7^](footnotes.html#fn7){#fnref7 .footnote-ref role="doc-noteref"}. There used to be a note here about migrating off Chico State's computers (my alma mater), but that's something that happened roughly a zillion years ago and the wording remained here only because it was copied over from the Network Guide, \[*breath*\] which I apparently haven't read in its entirety for quite some time.

The End.

## [1.5]{.header-section-number} Email Policy {#email-policy number="1.5"}

I'm generally available to help out with email questions so feel free to write in, but I can't guarantee a response. I lead a pretty busy life and there are times when I just can't answer a question you have. When that's the case, I usually just delete the message. It's nothing personal; I just won't ever have the time to give the detailed answer you require.

As a rule, the more complex the question, the less likely I am to respond. If you can narrow down your question before mailing it and be sure to include any pertinent information (like platform, compiler, error messages you're getting, and anything else you think might help me troubleshoot), you're much more likely to get a response.

If you don't get a response, hack on it some more, try to find the answer, and if it's still elusive, then write me again with the information you've found and hopefully it will be enough for me to help out.

Now that I've badgered you about how to write and not write me, I'd just like to let you know that I *fully* appreciate all the praise the guide has received over the years. It's a real morale boost, and it gladdens me to hear that it is being used for good! `:-)` Thank you!

## [1.6]{.header-section-number} Mirroring {#mirroring number="1.6"}

You are more than welcome to mirror this site, whether publicly or privately. If you publicly mirror the site and want me to link to it from the main page, drop me a line at [`beej@beej.us`](mailto:beej@beej.us).

## [1.7]{.header-section-number} Note for Translators {#note-for-translators number="1.7"}

If you want to translate the guide into another language, write me at [`beej@beej.us`](beej@beej.us) and I'll link to your translation from the main page. Feel free to add your name and contact info to the translation.

Please note the license restrictions in the Copyright and Distribution section, below.

## [1.8]{.header-section-number} Copyright and Distribution {#copyright-and-distribution number="1.8"}

Beej's Guide to C Programming--Library Reference is Copyright © 2021 Brian "Beej Jorgensen" Hall.

With specific exceptions for source code and translations, below, this work is licensed under the Creative Commons Attribution-Noncommercial-No Derivative Works 3.0 License. To view a copy of this license, visit [`https://creativecommons.org/licenses/by-nc-nd/3.0/`](https://creativecommons.org/licenses/by-nc-nd/3.0/) or send a letter to Creative Commons, 171 Second Street, Suite 300, San Francisco, California, 94105, USA.

One specific exception to the "No Derivative Works" portion of the license is as follows: this guide may be freely translated into any language, provided the translation is accurate, and the guide is reprinted in its entirety. The same license restrictions apply to the translation as to the original guide. The translation may also include the name and contact information for the translator.

The C source code presented in this document is hereby granted to the public domain, and is completely free of any license restriction.

Educators are freely encouraged to recommend or supply copies of this guide to their students.

Contact [`beej@beej.us`](beej@beej.us) for more information.

## [1.9]{.header-section-number} Dedication {#dedication number="1.9"}

The hardest things about writing these guides are:

-   Learning the material in enough detail to be able to explain it
-   Figuring out the best way to explain it clearly, a seemingly-endless iterative process
-   Putting myself out there as a so-called *authority*, when really I'm just a regular human trying to make sense of it all, just like everyone else
-   Keeping at it when so many other things draw my attention

A lot of people have helped me through this process, and I want to acknowledge those who have made this book possible.

-   Everyone on the Internet who decided to help share their knowledge in one form or another. The free sharing of instructive information is what makes the Internet the great place that it is.
-   The volunteers at [cppreference.com](https://en.cppreference.com/)[^8^](footnotes.html#fn8){#fnref8 .footnote-ref role="doc-noteref"} who provide the bridge that leads from the spec to the real world.
-   The helpful and knowledgeable folks on [comp.lang.c](https://groups.google.com/g/comp.lang.c)[^9^](footnotes.html#fn9){#fnref9 .footnote-ref role="doc-noteref"} and [r/C_Programming](https://www.reddit.com/r/C_Programming/)[^10^](footnotes.html#fn10){#fnref10 .footnote-ref role="doc-noteref"} who got me through the tougher parts of the language.
-   Everyone who submitted corrections and pull-requests on everything from misleading instructions to typos.

Thank you! ♥

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](index.html) \| [Contents](index.html) \| [Next](the-c-language.html)
:::
