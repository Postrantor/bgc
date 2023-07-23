
# [4] Functions {#functions number="4"}

> _"Sir, not in an environment such as this. That's why I've also been programmed for over thirty secondary functions that---"_
>
> ---C3PO, before being rudely interrupted, reporting a now-unimpressive number of additional functions, _Star Wars_ script

Very much like other languages you're used to, C has the concept of _functions_.

> C 也像你熟悉的其他语言一样，拥有函数的概念。

Functions can accept a variety of _arguments_ and return a value. One important thing, though: the arguments and return value types are predeclared---because that's how C likes it!

> 函数可以接受各种参数，并返回一个值。重要的是：参数和返回值的类型是预先声明的，因为这是 C 喜欢的！

Let's take a look at a function. This is a function that takes an `int` as an argument, and returns an `int`.

> 让我们来看一下一个函数。这是一个接受 `int` 作为参数并返回 `int` 的函数。

::: {#cb58 .sourceCode}

```c
#include <stdio.h>

int plus_one(int n)  // The "definition"
{
    return n + 1;
}

```

:::

The `int` before the `plus_one` indicates the return type.

The `int n` indicates that this function takes one `int` argument, stored in _parameter_ `n`. A parameter is a special type of local variable into which the arguments are copied.

> `int n` 表示这个函数接受一个 `int` 参数，存储在参数 `n` 中。参数是一种特殊类型的局部变量，参数会被复制到其中。

I'm going to drive home the point that the arguments are copied into the parameters, here. Lots of things in C are easier to understand if you know that the parameter is a _copy_ of the argument, not the argument itself. More on that in a minute.

> 我要强调的是，参数是参数的副本，而不是参数本身。如果你知道参数是参数的副本，那么 C 中的许多事情就会变得更容易理解。再说一分钟。

Continuing the program down into `main()`, we can see the call to the function, where we assign the return value into local variable `j`:

> 继续程序到 `main()`，我们可以看到对函数的调用，在那里我们将返回值赋值给局部变量 `j`：

::: {#cb59 .sourceCode startfrom="8"}

```c
int main(void)
{
    int i = 10, j;

    j = plus_one(i);  // The "call"

    printf("i + 1 is %d\n", j);
}
```

:::

> Before I forget, notice that I defined the function before I used it. If I hadn't done that, the compiler wouldn't know about it yet when it compiles `main()` and it would have given an unknown function call error. There is a more proper way to do the above code with _function prototypes_, but we'll talk about that later.

Also notice that `main()` is a function!

It returns an `int`.

But what's this `void` thing? This is a keyword that's used to indicate that the function accepts no arguments.

> 但是这个 `void` 是什么？这是一个关键字，用来表示函数不接受任何参数。

You can also return `void` to indicate that you don't return a value:

::: {#cb60 .sourceCode}

```c
#include <stdio.h>

// This function takes no arguments and returns no value:

void hello(void)
{
    printf("Hello, world!\n");
}

int main(void)
{
    hello();  // Prints "Hello, world!"
}
```

:::

## [4.1] Passing by Value {#passvalue number="4.1"}

I'd mentioned earlier that when you pass an argument to a function, a copy of that argument gets made and stored in the corresponding parameter.

> 当你向函数传递一个参数时，会创建一个该参数的副本并存储在相应的参数中，我之前提到过这一点。

If the argument is a variable, a copy of the value of that variable gets made and stored in the parameter.

> 如果参数是一个变量，那么会复制该变量的值并存储在参数中。

More generally, the entire argument expression is evaluated and its value determined. That value is copied to the parameter.

> 整体而言，整个参数表达式都会被求值，并且确定其值。该值会被复制到参数中。

In any case, the value in the parameter is its own thing. It is independent of whatever values or variables you used as arguments when you made the function call.

> 反正，参数中的值是它自己的东西。它独立于你在调用函数时使用的任何值或变量。

So let's look at an example here. Study it and see if you can determine the output before running it:

> 让我们来看一个例子。研究它，看看你能否在运行前确定输出？

::: {#cb61 .sourceCode}

```c
#include <stdio.h>

void increment(int a)
{
    a++;
}

int main(void)
{
    int i = 10;

    increment(i);

    printf("i == %d\n", i);  // What does this print?
}
```

:::

At first glance, it looks like `i` is `10`, and we pass it to the function `increment()`. There the value gets incremented, so when we print it, it must be `11`, right?

> 一看起来，`i` 的值是 10，我们把它传递给函数 `increment()`。在那里，值会被增加，所以当我们打印它的时候，它应该是 11，对吗？

> _"Get used to disappointment."_
>
> ---Dread Pirate Roberts, _The Princess Bride_

But it's not `11`---it prints `10`! How?

It's all about the fact that the expressions you pass to functions get _copied_ onto their corresponding parameters. The parameter is a copy, not the original.

> 事实就是你传递给函数的表达式会被_复制_到它们对应的参数上。参数是一个副本，而不是原件。

So `i` is `10` out in `main()`. And we pass it to `increment()`. The corresponding parameter is called `a` in that function.

> 所以在 main()中 i 的值是 10，我们把它传给 increment()函数，在那个函数中对应的参数叫做 a。

And the copy happens, as if by assignment. Loosely, `a = i`. So at that point, `a` is `10`. And out in `main()`, `i` is also `10`.

> 当复制发生时，就好像是按照赋值来的。简单地说，`a = i`。所以在那一刻，`a` 等于 `10`。而在 `main()` 中，`i` 也是 `10`。

Then we increment `a` to `11`. But we're not touching `i` at all! It remains `10`.

> 然后我们将 a 增加到 11，但我们不会碰 i，它仍然是 10。

Finally, the function is complete. All its local variables are discarded (bye, `a`!) and we return to `main()`, where `i` is still `10`.

> 最后，函数完成了，它的所有局部变量都被丢弃了(再见，`a`！)，我们回到 `main()`，`i` 仍然是 `10`。

And we print it, getting `10`, and we're done.

This is why in the previous example with the `plus_one()` function, we `return` ed the locally modified value so that we could see it again in `main()`.

> 在前面的例子中，我们使用 `plus_one()` 函数，我们返回了本地修改的值，以便我们可以在 `main()` 中再次看到它。

Seems a little bit restrictive, huh? Like you can only get one piece of data back from a function, is what you're thinking. There is, however, another way to get data back; C folks call it _passing by reference_ and that's a story we'll tell another time.

> 看起来有点局限，对吗？就像你只能从函数获得一个数据，这是你的想法。但是，还有另一种方法可以获得数据；C 语言的人称之为“传值引用”，这是我们另一次讲述的故事。

But no fancy-schmancy name will distract you from the fact that _EVERYTHING_ you pass to a function _WITHOUT EXCEPTION_ is copied into its corresponding parameter, and the function operates on that local copy, _NO MATTER WHAT_. Remember that, even when we're talking about this so-called passing by reference.

> 但是，没有花哨的名字能够让你忘记这样一个事实：_无一例外_，你传递给函数的_所有_内容都会被复制到相应的参数中，函数也会对这个本地副本进行操作，_无论如何_。即使我们在谈论所谓的引用传递，也要记住这一点。

## [4.2] Function Prototypes {#prototypes number="4.2"}

So if you recall back in the ice age a few sections ago, I mentioned that you had to define the function before you used it, otherwise the compiler wouldn't know about it ahead of time, and would bomb out with an error.

> 如果你还记得几节课前的冰河时代，我提到你必须在使用函数之前定义它，否则编译器不会提前知道，会报出一个错误。

This isn't quite strictly true. You can notify the compiler in advance that you'll be using a function of a certain type that has a certain parameter list. That way the function can be defined anywhere (even in a different file), as long as the _function prototype_ has been declared before you call that function.

> 这并不完全正确。你可以提前通知编译器你将使用一个特定类型的函数，具有特定的参数列表。这样，只要在调用该函数之前声明了函数原型，就可以在任何地方定义该函数(甚至在不同的文件中)。

Fortunately, the function prototype is really quite easy. It's merely a copy of the first line of the function definition with a semicolon tacked on the end for good measure. For example, this code calls a function that is defined later, because a prototype has been declared first:

> 幸运的是，函数原型真的很简单。它只是函数定义的第一行的副本，并在末尾添加一个分号以示好意。例如，此代码调用后面定义的函数，因为已经声明了原型：

::: {#cb62 .sourceCode}

```c
#include <stdio.h>

int foo(void);  // This is the prototype!

int main(void)
{
    int i;

    // We can call foo() here before it's definition because the
    // prototype has already been declared, above!

    i = foo();

    printf("%d\n", i);  // 3490
}

int foo(void)  // This is the definition, just like the prototype!
{
    return 3490;
}
```

:::

If you don't declare your function before you use it (either with a prototype or its definition), you're performing something called an _implicit declaration_. This was allowed in the first C standard (C89), and that standard has rules about it, but is no longer allowed today. And there is no legitimate reason to rely on it in new code.

> 如果你在使用函数之前没有声明它(使用原型或定义)，你就在执行一种叫做隐式声明的操作。这在第一个 C 标准(C89)中是允许的，该标准有关于它的规则，但今天不再允许。在新代码中没有合法的理由依赖它。

You might notice something about the sample code we've been using... That is, we've been using the good old `printf()` function without defining it or declaring a prototype! How do we get away with this lawlessness? We don't, actually. There is a prototype; it's in that header file `stdio.h` that we included with `#include`, remember? So we're still legit, officer!

> 你可能会注意到我们一直在使用的样例代码...也就是说，我们一直在使用老牌的 `printf()` 函数，而没有定义它或声明原型！我们怎么能这样违法呢？其实不行的，这里有一个原型；它就在我们用 `#include` 引入的头文件 `stdio.h` 里，记得吗？所以我们仍然是合法的，警官！

## [4.3] Empty Parameter Lists {#empty-parameter-lists number="4.3"}

You might see these from time to time in older code, but you shouldn't ever code one up in new code. Always use `void` to indicate that a function takes no parameters. There's never[^43^] a reason to do this in modern code.

> 你可能会时不时地在旧代码中看到它们，但你永远不应该在新代码中编写它们。总是使用 `void` 来表示函数不带参数。在现代代码中，没有理由这样做。

If you're good at just remembering to put `void` in for empty parameter lists in functions and prototypes, you can skip the rest of this section.

> 如果你擅长记住在函数和原型中的空参数列表中放入 `void`，你可以跳过本节的其余内容。

There are two contexts for this:

- Omitting all parameters where the function is defined
- Omitting all parameters in a prototype

Let's look at a potential function definition first:

::: {#cb63 .sourceCode}

```c
void foo()  // Should really have a `void` in there
{
    printf("Hello, world!\n");
}
```

:::

While the spec spells out that the behavior in this instance is _as-if_ you'd indicated `void` (C11 §6.7.6.3¶14), the `void` type is there for a reason. Use it.

> 尽管规范中明确指出，在这种情况下的行为就像您指示 `void` 一样(C11 §6.7.6.3¶14)，但 `void` 类型是有原因的。请使用它。

But in the case of a function prototype, there is a _significant_ difference between using `void` and not:

> 但是在函数原型的情况下，使用 `void` 和不使用之间有_重大_的区别：

::: {#cb64 .sourceCode}

```c
void foo();
void foo(void);  // Not the same!
```

:::

Leaving `void` out of the prototype indicates to the compiler that there is no additional information about the parameters to the function. It effectively turns off all that type checking.

> 移除原型中的 `void` 表明编译器没有关于函数参数的额外信息。它有效地关闭了所有类型检查。

With a prototype **definitely** use `void` when you have an empty parameter list.

> 使用原型时，当参数列表为空时，**一定**要使用 `void`。

# [5] Pointers---Cower In Fear! {#pointers number="5"}

> _"How do you get to Carnegie Hall?"_ > _"Practice!"_
>
> ---20th-century joke of unknown origin

Pointers are one of the most feared things in the C language. In fact, they are the one thing that makes this language challenging at all. But why?

> 指针是 C 语言中最可怕的东西之一。事实上，它们是使这门语言具有挑战性的唯一东西。但是为什么呢？

Because they, quite honestly, can cause electric shocks to come up through the keyboard and physically _weld_ your arms permanently in place, cursing you to a life at the keyboard in this language from the 70s!

> 因为它们可以通过键盘产生电击，真的会将你的手臂永久地焊接在键盘上，将你困在 70 年代的这种语言下的键盘上！

Really? Well, not really. I'm just trying to set you up for success.

Depending on what language you came from, you might already understand the concept of _references_, where a variable refers to an object of some type.

> 取决于你来自哪种语言，你可能已经理解了引用的概念，其中一个变量指向某种类型的对象。

This is very much the same, except we have to be more explicit with C about when we're talking about the reference or the thing it refers to.

> 这是非常相似的，只是我们在和 C 语言谈论引用或其所指物时，必须更加明确。

## [5.1] Memory and Variables {#ptmem number="5.1"}

Computer memory holds data of all kinds, right? It'll hold `float` s, `int` s, or whatever you have. To make memory easy to cope with, each byte of memory is identified by an integer. These integers increase sequentially as you move up through memory[^44^]. You can think of it as a bunch of numbered boxes, where each box holds a byte[^45^] of data. Or like a big array where each element holds a byte, if you come from a language with arrays. The number that represents each box is called its _address_.

> 计算机内存可以存储各种数据，对吗？它可以存储 `float`、`int` 或者你想要的任何东西。为了让内存更容易处理，每个字节的内存都有一个整数来标识。随着你在内存中向上移动，这些整数会逐渐增加[^44^]。你可以把它想象成一堆有编号的盒子，每个盒子里装着一个字节的数据[^45^]。或者像一个大数组，如果你来自一种有数组的语言，每个元素里装着一个字节。表示每个盒子的数字叫做它的_地址_。

Now, not all data types use just a byte. For instance, an `int` is often four bytes, as is a `float`, but it really depends on the system. You can use the `sizeof` operator to determine how many bytes of memory a certain type uses.

> 现在，并不是所有的数据类型都只使用一个字节。例如，`int` 通常是四个字节，`float` 也是四个字节，但这实际上取决于系统。您可以使用 `sizeof` 运算符来确定某种类型使用多少字节的内存。

::: {#cb65 .sourceCode}

```c
// %zu is the format specifier for type size_t

printf("an int uses %zu bytes of memory\n", sizeof(int));

// That prints "4" for me, but can vary by system.
```

:::

> **Memory Fun Facts**: When you have a data type (like your typical `int`) that uses more than a byte of memory, the bytes that make up the data are always adjacent to one another in memory. Sometimes they're in the order that you expect, and sometimes they're not[^46^]. While C doesn't guarantee any particular memory order (it's platform-dependent), it's still generally possible to write code in a way that's platform-independent where you don't have to even consider these pesky byte orderings.

So _anyway_, if we can get on with it and get a drum roll and some foreboding music playing for the definition of a pointer, _a pointer is a variable that holds an address_. Imagine the classical score from 2001: A Space Odyssey at this point. Ba bum ba bum ba bum BAAAAH!

> 好吧，如果我们可以继续，并且有鼓声和一些不祥的音乐播放来定义指针，指针是一个存储地址的变量。想象一下 2001：太空奥德赛的古典配乐。Ba bum ba bum ba bum BAAAAH！

Ok, so maybe a bit overwrought here, yes? There's not a lot of mystery about pointers. They are the address of data. Just like an `int` variable can hold the value `12`, a pointer variable can hold the address of data.

> 好吧，也许有点夸张，是吗？关于指针没有太多的神秘。它们是数据的地址。就像一个 `int` 变量可以存储值 `12`，一个指针变量可以存储数据的地址。

This means that all these things mean the same thing, i.e. a number that represents a point in memory:

> 这意味着所有这些东西意味着同一件事，即代表内存中某个点的数字。

- Index into memory (if you're thinking of memory like a big array)
- Address
- Location

I'm going to use these interchangeably. And yes, I just threw _location_ in there because you can never have enough words that mean the same thing.

> 我会交替使用这些。而且，我刚刚加入了_位置_，因为你永远不会有太多意思相同的词。

And a pointer variable holds that address number. Just like a `float` variable might hold `3.14159`.

> 一个指针变量保存着那个地址号码，就像一个 `float` 变量可以保存 `3.14159` 一样。

Imagine you have a bunch of Post-it® notes all numbered in sequence with their address. (The first one is at index numbered `0`, the next at index `1`, and so on.)

> 想象你有一堆按顺序编号的 Post-it® 便签，(第一个编号为 `0`，接下来是 `1`，依此类推)。

In addition to the number representing their positions, you can also write another number of your choice on each. It could be the number of dogs you have. Or the number of moons around Mars...

> 除了代表它们位置的数字外，你还可以在每个上面写上另一个你喜欢的数字。它可以是你养的狗的数量，也可以是火星上的月亮数量...

...Or, _it could be the index of another Post-it note!_

If you have written the number of dogs you have, that's just a regular variable. But if you wrote the index of another Post-it in there, _that's a pointer_. It points to the other note!

> 如果你写下你有多少只狗，那只是一个普通的变量。但如果你在里面写下另一张便利贴的索引，那就是一个指针。它指向另一张笔记！

Another analogy might be with house addresses. You can have a house with certain qualities, yard, metal roof, solar, etc. Or you could have the address of that house. The address isn't the same as the house itself. One's a full-blown house, and the other is just a few lines of text. But the address of the house is a _pointer_ to that house. It's not the house itself, but it tells you where to find it.

> 另一个类比可能是房屋地址。你可以有一个具有某些特质的房子，院子，金属屋顶，太阳能等。或者你可以有这个房子的地址。地址不是房子本身。一个是完整的房子，另一个只是几行文本。但是房子的地址是一个_指针_到那个房子。它不是房子本身，但它告诉你在哪里找到它。

And we can do the same thing in the computer with data. You can have a data variable that's holding some value. And that value is in memory at some address. And you could have a different _pointer variable_ hold the address of that data variable.

> 我们可以在计算机中用数据做同样的事情。你可以有一个数据变量，它保存着一些值。这个值存储在某个地址的内存中。你可以有一个不同的指针变量来保存该数据变量的地址。

It's not the data variable itself, but, like with a house address, it tells us where to find it.

> 它不是数据变量本身，而是像房屋地址一样，它告诉我们在哪里找到它。

When we have that, we say we have a "pointer to" that data. And we can follow the pointer to access the data itself.

> 当我们拥有这个时，我们说我们拥有一个"指针"指向该数据。我们可以通过指针来访问数据本身。

(Though it doesn't seem particularly useful yet, this all becomes indispensable when used with function calls. Bear with me until we get there.)

> (虽然它看起来没有特别有用，但是当与函数调用一起使用时，这一切就变得不可或缺了。请耐心等待，直到我们到达那里。)

So if we have an `int`, say, and we want a pointer to it, what we want is some way to get the address of that `int`, right? After all, the pointer just holds the _address of_ the data. What operator do you suppose we'd use to find the _address of_ the `int`?

> 如果我们有一个 `int`，我们想要一个指向它的指针，我们想要的是一种获取该 `int` 地址的方法，对吧？毕竟，指针只是保存数据的地址。你认为我们应该使用什么运算符来找到 `int` 的地址？

Well, by a shocking surprise that must come as something of a shock to you, gentle reader, we use the `address-of` operator (which happens to be an ampersand: "`&`")to find the address of the data. Ampersand.

> 嗯，这可能会让你感到震惊，亲爱的读者，我们使用“地址符”(它恰好是一个“&”符号)来找到数据的地址。“&”符号。

So for a quick example, we'll introduce a new _format specifier_ for `printf()` so you can print a pointer. You know already how `%d` prints a decimal integer, yes? Well, `%p` prints a pointer. Now, this pointer is going to look like a garbage number (and it might be printed in hexadecimal[^47^] instead of decimal), but it is merely the index into memory the data is stored in. (Or the index into memory that the first byte of data is stored in, if the data is multi-byte.) In virtually all circumstances, including this one, the actual value of the number printed is unimportant to you, and I show it here only for demonstration of the `address-of` operator.

> 举个例子，我们来介绍一个新的 `printf()` 格式说明符，这样你就可以打印指针了。你已经知道 `％d` 打印十进制整数，对吗？好的，`％p` 打印指针。现在，这个指针看起来像一个垃圾数字(它可能以十六进制[^47^](＃fn47){＃fnref47 .footnote-ref role =“doc-noteref”}而不是十进制打印)，但它只是存储数据的内存索引。 (或者，如果数据是多字节的，则是存储第一个字节数据的内存索引。)在几乎所有情况下，包括这种情况，打印出的数字的实际值对你来说都是无关紧要的，我在这里只是为了演示“取地址”运算符。

::: {#cb66 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i = 10;

    printf("The value of i is %d\n", i);
    printf("And its address is %p\n", (void *)&i);

    // %p expects the argument to be a pointer to void
    // so we cast it to make the compiler happy.
}
```

:::

On my computer, this prints:

::: {#cb67 .sourceCode}

```{.sourceCode .default}
The value of i is 10
And its address is 0x7ffddf7072a4
```

:::

If you're curious, that hexadecimal number is 140,727,326,896,068 in decimal (base 10 just like Grandma used to use). That's the index into memory where the variable `i`'s data is stored. It's the address of `i`. It's the location of `i`. It's a pointer to `i`.

> 如果你感到好奇，那么十六进制数字 140,727,326,896,068 在十进制(就像祖母以前使用的那样)中是多少？那就是存储变量 `i` 数据的内存索引。这是 `i` 的地址。这是 `i` 的位置。这是一个指向 `i` 的指针。

It's a pointer because it lets you know where `i` is in memory. Like a home address written on a scrap of paper tells you where you can find a particular house, this number indicates to us where in memory we can find the value of `i`. It points to `i`.

> 它是一个指针，因为它可以告诉你 `i` 在内存中的位置。就像一张纸片上写着的家庭地址可以告诉你你可以找到一个特定的房子，这个数字向我们表明，在内存中我们可以找到 `i` 的值的位置。它指向 `i`。

Again, we don't really care what the address's exact number is, generally. We just care that it's a pointer to `i`.

> 再次，我们通常不太关心地址的确切数字是什么。我们只关心它是指向'i'的指针。

## [5.2] Pointer Types {#pttypes number="5.2"}

So... this is all well and good. You can now successfully take the address of a variable and print it on the screen. There's a little something for the ol' resume, right? Here's where you grab me by the scruff of the neck and ask politely what the frick pointers are good for.

> 好了，这一切都很好。现在你可以成功地获取一个变量的地址并将其打印在屏幕上。这对简历来说是一个小小的成就，对吧？现在你可以抓住我的脖子并礼貌地问问指针到底有什么用处。

Excellent question, and we'll get to that right after these messages from our sponsor.

> 优秀的问题，在我们的赞助商的消息之后，我们将立即解决。

> `ACME ROBOTIC HOUSING UNIT CLEANING SERVICES. YOUR HOMESTEAD WILL BE DRAMATICALLY IMPROVED OR YOU WILL BE TERMINATED. MESSAGE ENDS.`

Welcome back to another installment of Beej's Guide. When we met last we were talking about how to make use of pointers. Well, what we're going to do is store a pointer off in a variable so that we can use it later. You can identify the _pointer type_ because there's an asterisk (`*`) before the variable name and after its type:

> 欢迎回到 Beej 的指南的另一个分节。当我们上次见面时，我们正在讨论如何利用指针。好吧，我们要做的是将指针存储在变量中，以便以后使用它。您可以识别_指针类型_，因为变量名称前面和类型后面都有一个星号(`*`)：

::: {#cb68 .sourceCode}

```c
int main(void)
{
    int i;  // i's type is "int"
    int *p; // p's type is "pointer to an int", or "int-pointer"
}
```

:::

Hey, so we have here a variable that is a pointer type, and it can point to other `int` s. That is, it can hold the address of other `int` s. We know it points to `int` s, since it's of type `int*` (read "int-pointer").

> 嘿，我们有一个指针类型的变量，它可以指向其他的 int。也就是说，它可以保存其他 int 的地址。我们知道它指向 int，因为它的类型是 int*(读作“int-pointer”)。

When you do an assignment into a pointer variable, the type of the right hand side of the assignment has to be the same type as the pointer variable. Fortunately for us, when you take the `address-of` a variable, the resultant type is a pointer to that variable type, so assignments like the following are perfect:

> 当您将一个任务分配给指针变量时，赋值右侧的类型必须与指针变量的类型相同。 幸运的是，当您取得变量的“地址”时，所产生的类型是该变量类型的指针，因此以下赋值是完美的：

::: {#cb69 .sourceCode}

```c
int i;
int *p;  // p is a pointer, but is uninitialized and points to garbage

p = &i;  // p is assigned the address of i--p now "points to" i
```

:::

On the left of the assignment, we have a variable of type pointer-to-`int` (`int*`), and on the right side, we have expression of type pointer-to-`int` since `i` is an `int` (because address-of `int` gives you a pointer to `int`). The address of a thing can be stored in a pointer to that thing.

> 在赋值的左边，我们有一个指向 `int` 类型的变量(`int*`)，在右边，我们有一个指向 `int` 类型的表达式，因为 `i` 是一个 `int`(因为 `int` 的地址给你一个指向 `int` 的指针)。一个东西的地址可以存储在指向该东西的指针中。

Get it? I know it still doesn't quite make much sense since you haven't seen an actual use for the pointer variable, but we're taking small steps here so that no one gets lost. So now, let's introduce you to the anti-address-of operator. It's kind of like what `address-of` would be like in Bizarro World.

> 你明白了吗？我知道你还没有看到指针变量的实际用途，所以这里还不太容易理解，但我们现在只是一步一步地学习，以免有人跟不上。现在，让我们来介绍一下反地址运算符。它有点像比扎罗世界里的“地址”。

## [5.3] Dereferencing {#deref number="5.3"}

A pointer variable can be thought of as _referring_ to another variable by pointing to it. It's rare you'll hear anyone in C land talking about "referring" or "references", but I bring it up just so that the name of this operator will make a little more sense.

> 指针变量可以被认为是通过指向它来指向另一个变量。很少有人在 C 语言中谈论“引用”或“引用”，但我提出它只是为了让这个运算符的名字更有意义。

When you have a pointer to a variable (roughly "a reference to a variable"), you can use the original variable through the pointer by _dereferencing_ the pointer. (You can think of this as "de-pointering" the pointer, but no one ever says "de-pointering".)

> 当你有一个指向变量的指针(大致上是“对变量的引用”)时，你可以通过解引用指针来使用原始变量。(你可以把这想象成“取消指针”，但没有人会说“取消指针”。)

Back to our analogy, this is vaguely like looking at a home address and then going to that house.

> 回到我们的比喻，这就好比是看到一个家庭地址，然后去那个房子。

Now, what do I mean by "get access to the original variable"? Well, if you have a variable called `i`, and you have a pointer to `i` called `p`, you can use the dereferenced pointer `p` _exactly as if it were the original variable `i`_!

> 现在，我所说的“获取对原变量的访问”是什么意思？好吧，如果你有一个叫做 `i` 的变量，并且你有一个指向 `i` 的指针叫做 `p`，你可以像使用原始变量 `i` 一样使用解引用的指针 `p`！

You almost have enough knowledge to handle an example. The last tidbit you need to know is actually this: what is the dereference operator? It's actually called the _indirection operator_, because you're accessing values indirectly via the pointer. And it is the asterisk, again: `*`. Now, don't get this confused with the asterisk you used in the pointer declaration, earlier. They are the same character, but they have different meanings in different contexts[^48^].

> 你几乎已经拥有足够的知识来处理一个例子。你最后需要知道的小细节实际上是：什么是取消引用运算符？它实际上被称为_间接操作符_，因为你是通过指针间接访问值。它是星号，再次：`*`。现在，不要把这个星号与你之前在指针声明中使用的星号混淆了。它们是相同的字符，但是在不同的上下文中具有不同的含义[^48^]。

Here's a full-blown example:

::: {#cb70 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i;
    int *p;  // this is NOT a dereference--this is a type "int*"

    p = &i;  // p now points to i, p holds address of i

    i = 10;  // i is now 10
    *p = 20; // the thing p points to (namely i!) is now 20!!

    printf("i is %d\n", i);   // prints "20"
    printf("i is %d\n", *p);  // "20"! dereference-p is the same as i!
}
```

:::

Remember that `p` holds the address of `i`, as you can see where we did the assignment to `p` on line 8. What the indirection operator does is tells the computer to _use the object the pointer points to_ instead of using the pointer itself. In this way, we have turned `*p` into an alias of sorts for `i`.

> 记住，`p` 保存着 `i` 的地址，正如你在第 8 行看到的那样。间接操作符的作用是告诉计算机使用指针指向的对象，而不是使用指针本身。这样，我们就把 `*p` 变成了 `i` 的一种别名。

Great, but _why_? Why do any of this?

## [5.4] Passing Pointers as Arguments {#ptpass number="5.4"}

Right about now, you're thinking that you have an awful lot of knowledge about pointers, but absolutely zero application, right? I mean, what use is `*p` if you could just simply say `i` instead?

> 此时此刻，你可能觉得自己对指针有很多知识，但是没有实际应用，对吗？我的意思是，如果你可以只说 `i`，那么 `*p` 有什么用处呢？

Well, my friend, the real power of pointers comes into play when you start passing them to functions. Why is this a big deal? You might recall from before that you could pass all kinds of arguments to functions and they'd be dutifully copied into parameters, and then you could manipulate local copies of those variables from within the function, and then you could return a single value.

> 嗯，我的朋友，当你开始把指针传递给函数时，指针的真正功能才开始发挥作用。这有什么大不了的？你可能还记得，你可以把各种参数传递给函数，它们会被谨慎地复制到参数中，然后你可以在函数内部操纵这些变量的本地副本，然后你可以返回一个值。

简体中文：嗯，我的朋友，当你开始把指针传递给函数时，指针的真正功能才开始发挥作用。这有什么大不了的？你可能还记得，你可以把各种参数传递给函数，它们会被谨慎地复制到参数中，然后你可以在函数内部操纵这些变量的本地副本，然后你可以返回一个值。

What if you wanted to bring back more than one single piece of data from the function? I mean, you can only return one thing, right? What if I answered that question with another question? ...Er, two questions?

> 如果你想从函数中返回不止一个数据，怎么办？我的意思是，你只能返回一件事，对吗？如果我用另一个问题来回答这个问题会怎样？...嗯，两个问题？

What happens when you pass a pointer as an argument to a function? Does a copy of the pointer get put into its corresponding parameter? _You bet your sweet peas it does._ Remember how earlier I rambled on and on about how _EVERY SINGLE ARGUMENT_ gets copied into parameters and the function uses a copy of the argument? Well, the same is true here. The function will get a copy of the pointer.

> 当你把一个指针作为参数传递给一个函数时会发生什么？指针的副本会被拷贝到相应的参数中吗？当然会！记得我之前讲过的每一个参数都会被拷贝到参数中，函数使用参数的副本？同样的，这里也是如此。函数会得到指针的副本。

But, and this is the clever part: we will have set up the pointer in advance to point at a variable... and then the function can dereference its copy of the pointer to get back to the original variable! The function can't see the variable itself, but it can certainly dereference a pointer to that variable!

> 但是，这是聪明的一部分：我们将提前设置指针指向一个变量... 然后函数可以解引用它的指针副本以访问原始变量！函数看不到变量本身，但它可以解引用指向该变量的指针！

This is analogous to writing a home address on a piece of paper, and then copying that onto another piece of paper. You now have _two_ pointers to that house, and both are equally good at getting you to the house itself.

> 这类似于在一张纸上写下家庭地址，然后将其复制到另一张纸上。现在你有了_两_个指向那个房子的指针，它们都能让你到达那个房子。

In the case of a function call. one of the copies is stored in a pointer variable out in the calling scope, and the other is stored in a pointer variable that is the parameter of the function.

> 在函数调用的情况下，其中一个副本存储在调用范围外的指针变量中，另一个副本存储在作为函数参数的指针变量中。

Example! Let's revisit our old `increment()` function, but this time let's make it so that it actually increments the value out in the caller.

> 例子！让我们重新查看我们的旧 `increment()` 函数，但这次让它实际增加调用者中的值。

::: {#cb71 .sourceCode}

```c
#include <stdio.h>

void increment(int *p)  // note that it accepts a pointer to an int
{
    *p = *p + 1;        // add one to the thing p points to
}

int main(void)
{
    int i = 10;
    int *j = &i;  // note the address-of; turns it into a pointer to i

    printf("i is %d\n", i);        // prints "10"
    printf("i is also %d\n", *j);  // prints "10"

    increment(j);                  // j is an int*--to i

    printf("i is %d\n", i);        // prints "11"!
}
```

:::

Ok! There are a couple things to see here... not the least of which is that the `increment()` function takes an `int*` as an argument. We pass it an `int*` in the call by changing the `int` variable `i` to an `int*` using the `address-of` operator. (Remember, a pointer holds an address, so we make pointers to variables by running them through the `address-of` operator.)

> 好的！这里有几件事可以看到...其中最不可忽视的是 `increment()` 函数接受一个 `int*` 作为参数。我们在调用时通过使用 `地址运算符` 将 `int` 变量 `i` 改为 `int*` 来传递它。(记住，指针保存一个地址，所以我们可以通过 `地址运算符` 将变量转换为指针)。

The `increment()` function gets a copy of the pointer. Both the original pointer `j` (in `main()`) and the copy of that pointer `p` (the parameter in `increment()`) point to the same address, namely the one holding the value `i`. (Again, by analogy, like two pieces of paper with the same home address written on them.) Dereferencing either will allow you to modify the original variable `i`! The function can modify a variable in another scope! Rock on!

> `increment()` 函数获得指针的副本。原始指针 `j`(在 `main()` 中)和该指针 `p`(`increment()` 中的参数)的副本指向同一个地址，即存储值 `i` 的地址。(再次比喻，就像两张纸上写着相同家庭地址的纸。)解引用任何一个都可以修改原始变量 `i`！该函数可以修改另一个作用域中的变量！太棒了！

The above example is often more concisely written in the call just by using address-of right in the argument list:

> 以上的例子通常可以通过在参数列表中直接使用地址符号来更简洁地调用：

::: {#cb72 .sourceCode}

```c
printf("i is %d\n", i);  // prints "10"
increment(&i);
printf("i is %d\n", i);  // prints "11"!
```

:::

Pointer enthusiasts will recall from early on in the guide, we used a function to read from the keyboard, `scanf()`... and, although you might not have recognized it at the time, we used the `address-of` to pass a pointer to a value to `scanf()`. We had to pass a pointer, see, because `scanf()` reads from the keyboard (typically) and stores the result in a variable. The only way it can see that variable out in the calling function's scope is if we pass a pointer to that variable:

> 指针爱好者们会从本指南的早期记忆，我们使用一个函数来从键盘读取，`scanf()`...而且，尽管你可能当时没有认识到，我们使用 `地址` 来传递一个指针给 `scanf()`。我们必须传递一个指针，看到，因为 `scanf()` 从键盘(通常)读取并将结果存储在变量中。它只能看到调用函数作用域中的变量，如果我们传递一个指向该变量的指针：

::: {#cb73 .sourceCode}

```c
int i = 0;

scanf("%d", &i);         // pretend you typed "12"
printf("i is %d\n", i);  // prints "i is 12"
```

:::

See, `scanf()` dereferences the pointer we pass it in order to modify the variable it points to. And now you know why you have to put that pesky ampersand in there!

> 看，`scanf()` 解引用我们传递给它的指针，以便修改它指向的变量。现在你知道为什么你必须在那里放置那个讨厌的操作符号了！

## [5.5] The `NULL` Pointer {#the-null-pointer number="5.5"}

Any pointer variable of any pointer type can be set to a special value called `NULL`. This indicates that this pointer doesn't point to anything.

> 任何指针类型的指针变量都可以设置为一个特殊值，称为“NULL”。这表明该指针不指向任何内容。

::: {#cb74 .sourceCode}

```c
int *p;

p = NULL;
```

:::

Since it doesn't point to a value, dereferencing it is undefined behavior, and probably will result in a crash:

> 由于它不指向任何值，解引用它是未定义的行为，可能会导致崩溃：

::: {#cb75 .sourceCode}

```c
int *p = NULL;

*p = 12;  // CRASH or SOMETHING PROBABLY BAD. BEST AVOIDED.
```

:::

Despite being called [the billion dollar mistake by its creator](https://en.wikipedia.org/wiki/Null_pointer#History)[^49^], the `NULL` pointer is a good [sentinel value](https://en.wikipedia.org/wiki/Sentinel_value)[^50^] and general indicator that a pointer hasn't yet been initialized.

> 尽管它的创造者称之为“十亿美元的错误”，但 NULL 指针是一个很好的哨兵值和指示指针尚未初始化的一般指标。

(Of course, like other variables, the pointer points to garbage unless you explicitly assign it to point to an address or `NULL`.)

> 当然，像其他变量一样，指针除非你显式地将它指向一个地址或者 `NULL`，否则它指向的就是垃圾数据。

## [5.6] A Note on Declaring Pointers {#a-note-on-declaring-pointers number="5.6"}

The syntax for declaring a pointer can get a little weird. Let's look at this example:

> 声明指针的语法可能有点奇怪。让我们看看这个例子：

::: {#cb76 .sourceCode}

```c
int a;
int b;
```

:::

We can condense that into a single line, right?

::: {#cb77 .sourceCode}

```c
int a, b;  // Same thing
```

:::

So `a` and `b` are both `int` s. No problem.

But what about this?

::: {#cb78 .sourceCode}

```c
int a;
int *p;
```

:::

Can we make that into one line? We can. But where does the `*` go?

The rule is that the `*` goes in front of any variable that is a pointer type. That is. the `*` is _not_ part of the `int` in this example. it's a part of variable `p`.

> 规则是，任何指针类型的变量前面都要加上 `*` 号。也就是说，在这个例子中，`*` 不是 `int` 的一部分，而是变量 `p` 的一部分。

With that in mind, we can write this:

::: {#cb79 .sourceCode}

```c
int a, *p;  // Same thing
```

:::

It's important to note that the following line does _not_ declare two pointers:

> 重要的是要注意，下面这行代码并不声明两个指针。

::: {#cb80 .sourceCode}

```c
int *p, q;  // p is a pointer to an int; q is just an int.
```

:::

This can be particularly insidious-looking if the programmer writes this following (valid) line of code which is functionally identical to the one above.

> 这可能特别隐蔽，如果程序员编写了下面这行(有效的)代码，它在功能上与上面的代码完全相同。

::: {#cb81 .sourceCode}

```c
int* p, q;  // p is a pointer to an int; q is just an int.
```

:::

So take a look at this and determine which variables are pointers and which are not:

> 看看这个，确定哪些变量是指针，哪些不是？

::: {#cb82 .sourceCode}

```c
int *a, b, c, *d, e, *f, g, h, *i;
```

:::

I'll drop the answer in a footnote[^51^].

> 我会在脚注 [^51^]中放置答案。

## [5.7] `sizeof` and Pointers {#sizeof-and-pointers number="5.7"}

Just a little bit of syntax here that might be confusing and you might see from time to time.

> 只有一点点语法，可能会让你感到困惑，你可能会不时地看到它。

Recall that `sizeof` operates on the _type_ of the expression.

::: {#cb83 .sourceCode}

```c
int *p;

// Prints size of an 'int'
printf("%zu\n", sizeof(int));

// p is type 'int *', so prints size of 'int*'
printf("%zu\n", sizeof p);

// *p is type 'int', so prints size of 'int'
printf("%zu\n", sizeof *p);
```

:::

You might see code in the wild with that last `sizeof` in there. Just remember that `sizeof` is all about the type of the expression, not the variables in the expression themselves.

> 你可能会在野外看到有最后一个 `sizeof` 的代码。只要记住 `sizeof` 与表达式的类型有关，而不是表达式中的变量本身。

# [6] Arrays {#arrays number="6"}

> _"Should array indices start at 0 or 1? My compromise of 0.5 was rejected without, I thought, proper consideration."_
>
> ---Stan Kelly-Bootle, computer scientist

Luckily, C has arrays. I mean, I know it's considered a low-level language[^52^] but it does at least have the concept of arrays built-in. And since a great many languages drew inspiration from C's syntax, you're probably already familiar with using `[` and `]` for declaring and using arrays.

> 幸运的是，C 有数组。我的意思是，我知道它被认为是一种低级语言[^52^]，但它至少具有数组的概念。由于许多语言都从 C 的语法中获得灵感，您可能已经熟悉使用 `[` 和 `]` 来声明和使用数组了。

But C only _barely_ has arrays! As we'll find out later, arrays are just syntactic sugar in C---they're actually all pointers and stuff deep down. _Freak out!_ But for now, let's just use them as arrays. _Phew_.

> 但是 C 只是勉强有数组！稍后我们会发现，数组只是 C 中的语法糖——实际上它们在深层次上都是指针等等。太可怕了！但是现在，让我们把它们当做数组来使用吧。太好了。

## [6.1] Easy Example {#easy-example number="6.1"}

Let's just crank out an example:

::: {#cb84 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i;
    float f[4];  // Declare an array of 4 floats

    f[0] = 3.14159;  // Indexing starts at 0, of course.
    f[1] = 1.41421;
    f[2] = 1.61803;
    f[3] = 2.71828;

    // Print them all out:

    for (i = 0; i < 4; i++) {
        printf("%f\n", f[i]);
    }
}
```

:::

When you declare an array, you have to give it a size. And the size has to be fixed[^53^].

> 当你声明一个数组时，你必须给它一个固定的大小。

In the above example, we made an array of 4 `float` s. The value in the square brackets in the declaration lets us know that.

> 在上面的例子中，我们创建了一个由 4 个 `float` 组成的数组。声明中方括号中的值告诉我们这一点。

Later on in subsequent lines, we access the values in the array, setting them or getting them, again with square brackets.

> 在随后的行中，我们使用方括号来访问数组中的值，设置或获取它们。

Hopefully this looks familiar from languages you already know!

## [6.2] Getting the Length of an Array {#getting-the-length-of-an-array number="6.2"}

You can't...ish. C doesn't record this information[^54^]. You have to manage it separately in another variable.

> 你不能...。C 语言不会记录这些信息 [^54^]。你必须在另一个变量中单独管理它。

When I say "can't", I actually mean there are some circumstances when you _can_. There is a trick to get the number of elements in an array in the scope in which an array is declared. But, generally speaking, this won't work the way you want if you pass the array to a function[^55^].

> 当我说“不能”时，我实际上是指有些情况下你可以做到。在声明数组的范围内有一种技巧可以获取数组中的元素数量。但是，一般来说，如果你将数组传递给函数，这种方法不会按照你的期望工作 [^55^]。

Let's take a look at this trick. The basic idea is that you take the `sizeof` the array, and then divide that by the size of each element to get the length. For example, if an `int` is 4 bytes, and the array is 32 bytes long, there must be room for [\\(\\frac{32}{4}\\)]{.math .inline} or [\\(8\\)]{.math .inline} `int` s in there.

> 让我们来看看这个把戏。基本思想是你取得数组的 `sizeof`，然后除以每个元素的大小来获得长度。例如，如果 `int` 是 4 字节，数组长度是 32 字节，那里一定有[\\(\\frac{32}{4}\\)]{.math .inline}或[\\(8\\)]{.math .inline}个 `int` s。

::: {#cb85 .sourceCode}

```c
int x[12];  // 12 ints

printf("%zu\n", sizeof x);     // 48 total bytes
printf("%zu\n", sizeof(int));  // 4 bytes per int

printf("%zu\n", sizeof x / sizeof(int));  // 48/4 = 12 ints!
```

:::

If it's an array of `char` s, then `sizeof` the array _is_ the number of elements, since `sizeof(char)` is defined to be 1. For anything else, you have to divide by the size of each element.

> 如果是一个 `char` 数组，那么 `sizeof` 数组_就是_元素的数量，因为 `sizeof(char)` 被定义为 1。对于其他任何东西，你必须除以每个元素的大小。

But this trick only works in the scope in which the array was defined. If you pass the array to a function, it doesn't work. Even if you make it "big" in the function signature:

> 但是，这个技巧只适用于定义数组的范围。如果您将数组传递给函数，它就不起作用。即使在函数签名中将其“扩大”也是如此：

::: {#cb86 .sourceCode}

```c
void foo(int x[12])
{
    printf("%zu\n", sizeof x);     // 8?! What happened to 48?
    printf("%zu\n", sizeof(int));  // 4 bytes per int

    printf("%zu\n", sizeof x / sizeof(int));  // 8/4 = 2 ints?? WRONG.
}
```

:::

This is because when you "pass" arrays to functions, you're only passing a pointer to the first element, and that's what `sizeof` measures. More on this in the [Passing Single Dimensional Arrays to Functions](#passing1darrays) section, below.

> 因为当你把数组传递给函数时，你只传递了一个指向第一个元素的指针，而 `sizeof` 就是测量这个指针。更多内容请参考下面的[将单维数组传递给函数](#passing1darrays)部分。

One more thing you can do with `sizeof` and arrays is get the size of an array of a fixed number of elements without declaring the array. This is like how you can get the size of an `int` with `sizeof(int)`.

> 你可以使用 `sizeof` 和数组做的另一件事是获取固定元素数量的数组的大小，而无需声明数组。这就像你可以使用 `sizeof(int)` 获取 `int` 的大小一样。

For example, to see how many bytes would be needed for an array of 48 `double` s, you can do this:

> 例如，要查看需要多少字节用于一个 48 个 `double` 的数组，可以这样做：

::: {#cb87 .sourceCode}

```c
sizeof(double [48]);
```

:::

## [6.3] Array Initializers {#array-initializers number="6.3"}

You can initialize an array with constants ahead of time:

::: {#cb88 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i;
    int a[5] = {22, 37, 3490, 18, 95};  // Initialize with these values

    for (i = 0; i < 5; i++) {
        printf("%d\n", a[i]);
    }
}
```

:::

Catch: initializer values must be constant terms. Can't throw variables in there. Sorry, Illinois!

> 捕获：初始值必须是常量项。不能在里面扔变量。抱歉，伊利诺伊！

You should never have more items in your initializer than there is room for in the array, or the compiler will get cranky:

> 你的初始化器中的项目不应该超过数组中可容纳的空间，否则编译器会变得暴躁：

::: {#cb89 .sourceCode}

```zsh
foo.c: In function ‘main’:
foo.c:6:39: warning: excess elements in array initializer
    6 |     int a[5] = {22, 37, 3490, 18, 95, 999};
      |                                       ^~~
foo.c:6:39: note: (near initialization for ‘a’)
```

:::

But (fun fact!) you can have _fewer_ items in your initializer than there is room for in the array. The remaining elements in the array will be automatically initialized with zero. This is true in general for all types of array initializers: if you have an initializer, anything not explicitly set to a value will be set to zero.

> 但是(有趣的事实！)您可以在初始化器中拥有比数组中有更少的项目。数组中剩余的元素将自动初始化为零。对于所有类型的数组初始化器来说，这都是正确的：如果您有一个初始化器，任何未显式设置为值的内容都将被设置为零。

::: {#cb90 .sourceCode}

```c
int a[5] = {22, 37, 3490};

// is the same as:

int a[5] = {22, 37, 3490, 0, 0};
```

:::

It's a common shortcut to see this in an initializer when you want to set an entire array to zero:

> 这是一个常见的快捷方式，当你想将整个数组设置为零时，可以在初始化器中看到：

::: {#cb91 .sourceCode}

```c
int a[100] = {0};
```

:::

Which means, "Make the first element zero, and then automatically make the rest zero, as well."

> 将第一个元素置零，然后自动将其余元素也置零。

You can set specific array elements in the initializer, as well, by specifying an index for the value! When you do this, C will happily keep initializing subsequent values for you until the initializer runs out, filling everything else with `0`.

> 你也可以在初始化器中为特定的数组元素设置值，只需为该值指定一个索引即可！当你这样做时，C 会很乐意继续初始化后续值，直到初始化器用完，剩下的所有值都会被填充为“0”。

To do this, put the index in square brackets with an `=` after, and then set the value.

> 将索引放入方括号中，后面加上等号，然后设置值。

Here's an example where we build an array:

::: {#cb92 .sourceCode}

```c
int a[10] = {0, 11, 22, [5]=55, 66, 77};
```

:::

Because we listed index 5 as the start for `55`, the resulting data in the array is:

> 因为我们将索引 5 列为 `55` 的起点，数组中的结果是：

::: {#cb93 .sourceCode}

```{.sourceCode .default}
0 11 22 0 0 55 66 77 0 0
```

:::

You can put simple constant expressions in there, as well.

::: {#cb94 .sourceCode}

```c
#define COUNT 5

int a[COUNT] = {[COUNT-3]=3, 2, 1};
```

:::

which gives us:

::: {#cb95 .sourceCode}

```{.sourceCode .default}
0 0 3 2 1
```

:::

Lastly, you can also have C compute the size of the array from the initializer, just by leaving the size off:

> 最后，您还可以让 C 从初始值计算数组的大小，只需要省略大小即可：

::: {#cb96 .sourceCode}

```c
int a[3] = {22, 37, 3490};

// is the same as:

int a[] = {22, 37, 3490};  // Left the size off!
```

:::

## [6.4] Out of Bounds! {#out-of-bounds number="6.4"}

C doesn't stop you from accessing arrays out of bounds. It might not even warn you.

> C 不会阻止你访问超出边界的数组，甚至可能不会警告你。

Let's steal the example from above and keep printing off the end of the array. It only has 5 elements, but let's try to print 10 and see what happens:

> 让我们从上面偷窃一个例子，并继续打印数组的末尾。它只有 5 个元素，但让我们尝试打印 10 个，看看会发生什么：

::: {#cb97 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i;
    int a[5] = {22, 37, 3490, 18, 95};

    for (i = 0; i < 10; i++) {  // BAD NEWS: printing too many elements!
        printf("%d\n", a[i]);
    }
}
```

:::

Running it on my computer prints:

::: {#cb98 .sourceCode}

```{.sourceCode .default}
22
37
3490
18
95
32765
1847052032
1780534144
-56487472
21890
```

:::

Yikes! What's that? Well, turns out printing off the end of an array results in what C developers call _undefined behavior_. We'll talk more about this beast later, but for now it means, "You've done something bad, and anything could happen during your program run."

> 哎呀！那是什么？原来，打印数组末尾的结果会导致 C 开发人员所说的_未定义行为_。我们稍后会讨论更多关于这个怪物的事情，但是现在它的意思是：“你做了一些不好的事情，在程序运行期间任何事情都可能发生。”

And by anything, I mean typically things like finding zeroes, finding garbage numbers, or crashing. But really the C spec says in this circumstance the compiler is allowed to emit code that does _anything_[^56^].

> 而所谓的任何东西，通常指的是像寻找零点、寻找垃圾数字或崩溃等事情。但实际上，C 规范说，在这种情况下，编译器可以释放任何代码[^56^]。

Short version: don't do anything that causes undefined behavior. Ever[^57^].

> 不要做任何会导致未定义行为的事情。永远不要。

## [6.5] Multidimensional Arrays {#multidimensional-arrays number="6.5"}

You can add as many dimensions as you want to your arrays.

::: {#cb99 .sourceCode}

```c
int a[10];
int b[2][7];
int c[4][5][6];
```

:::

These are stored in memory in [row-major order](https://en.wikipedia.org/wiki/Row-_and_column-major_order)[^58^]. This means with a 2D array, the first index listed indicates the row, and the second the column.

> 这些存储在内存中是按[行优先顺序](https://en.wikipedia.org/wiki/Row-_and_column-major_order)[^58^]排列的。这意味着对于二维数组，第一个索引表示行，第二个索引表示列。

You can also use initializers on multidimensional arrays by nesting them:

::: {#cb100 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int row, col;

    int a[2][5] = {      // Initialize a 2D array
        {0, 1, 2, 3, 4},
        {5, 6, 7, 8, 9}
    };

    for (row = 0; row < 2; row++) {
        for (col = 0; col < 5; col++) {
            printf("(%d,%d) = %d\n", row, col, a[row][col]);
        }
    }
}
```

:::

For output of:

::: {#cb101 .sourceCode}

```{.sourceCode .default}
(0,0) = 0
(0,1) = 1
(0,2) = 2
(0,3) = 3
(0,4) = 4
(1,0) = 5
(1,1) = 6
(1,2) = 7
(1,3) = 8
(1,4) = 9
```

:::

And you can initialize with explicit indexes:

::: {#cb102 .sourceCode}

```c
// Make a 3x3 identity matrix

int a[3][3] = {[0][0]=1, [1][1]=1, [2][2]=1};
```

:::

which builds a 2D array like this:

::: {#cb103 .sourceCode}

```{.sourceCode .default}
1 0 0
0 1 0
0 0 1
```

:::

## [6.6] Arrays and Pointers {#arrays-and-pointers number="6.6"}

\[_Casually_\] So... I kinda might have mentioned up there that arrays were pointers, deep down? We should take a shallow dive into that now so that things aren't completely confusing. Later on, we'll look at what the real relationship between arrays and pointers is, but for now I just want to look at passing arrays to functions.

> [_随便_] 嗯... 我可能在上面提到过，数组其实是指针，现在我们来浅尝一下，免得大家完全搞不清楚。稍后，我们会看到数组和指针之间的真正关系，但现在我只想看看如何把数组传递给函数。

### [6.6.1] Getting a Pointer to an Array {#getting-a-pointer-to-an-array number="6.6.1"}

I want to tell you a secret. Generally speaking, when a C programmer talks about a pointer to an array, they're talking about a pointer _to the first element_ of the array[^59^].

> 我想告诉你一个秘密。一般来说，当 C 程序员谈论指向数组的指针时，他们指的是指向数组第一个元素的指针。

So let's get a pointer to the first element of an array.

::: {#cb104 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int a[5] = {11, 22, 33, 44, 55};
    int *p;

    p = &a[0];  // p points to the array
                // Well, to the first element, actually

    printf("%d\n", *p);  // Prints "11"
}
```

:::

This is so common to do in C that the language allows us a shorthand:

::: {#cb105 .sourceCode}

```c
p = &a[0];  // p points to the array

// is the same as:

p = a;      // p points to the array, but much nicer-looking!
```

:::

Just referring to the array name in isolation is the same as getting a pointer to the first element of the array! We're going to use this extensively in the upcoming examples.

> 只是提到数组名称本身就相当于获取数组第一个元素的指针！我们将在接下来的例子中大量使用它。

But hold on a second---isn't `p` an `int*`? And `*p` gives us `11`, same as `a[0]`? Yessss. You're starting to get a glimpse of how arrays and pointers are related in C.

> 等一下---`p` 不是一个 `int*` 吗？而 `*p` 给我们的是 `11`，跟 `a[0]` 一样吗？是的。你开始看到在 C 语言中，数组和指针是如何相关联的了。

### [6.6.2] Passing Single Dimensional Arrays to Functions {#passing1darrays number="6.6.2"}

Let's do an example with a single dimensional array. I'm going to write a couple functions that we can pass the array to that do different things.

> 让我们用一维数组做一个例子。我们可以传递数组给它们，它们可以做不同的事情。

Prepare for some mind-blowing function signatures!

::: {#cb106 .sourceCode}

```c
#include <stdio.h>

// Passing as a pointer to the first element
void times2(int *a, int len)
{
    for (int i = 0; i < len; i++)
        printf("%d\n", a[i] * 2);
}

// Same thing, but using array notation
void times3(int a[], int len)
{
    for (int i = 0; i < len; i++)
        printf("%d\n", a[i] * 3);
}

// Same thing, but using array notation with size
void times4(int a[5], int len)
{
    for (int i = 0; i < len; i++)
        printf("%d\n", a[i] * 4);
}

int main(void)
{
    int x[5] = {11, 22, 33, 44, 55};

    times2(x, 5);
    times3(x, 5);
    times4(x, 5);
}
```

:::

All those methods of listing the array as a parameter in the function are identical.

> 所有这些将数组列为函数参数的方法是相同的。

::: {#cb107 .sourceCode}

```c
void times2(int *a, int len)
void times3(int a[], int len)
void times4(int a[5], int len)
```

:::

In usage by C regulars, the first is the most common, by far.

And, in fact, in the latter situation, the compiler doesn't even care what number you pass in (other than it has to be greater than zero[^60^]). It doesn't enforce anything at all.

> 在后一种情况下，编译器甚至不关心你传入了什么数字(只要它大于零 [^60^])，它根本不会强制执行任何东西。

Now that I've said that, the size of the array in the function declaration actually _does_ matter when you're passing multidimensional arrays into functions, but let's come back to that.

> 现在我说了这些，当你传递多维数组到函数中时，函数声明中的数组大小实际上是很重要的，但让我们回到这个问题上来。

### [6.6.3] Changing Arrays in Functions {#changing-arrays-in-functions number="6.6.3"}

We've said that arrays are just pointers in disguise. This means that if you pass an array to a function, you're likely passing a pointer to the first element in the array.

> 我们说过数组只是伪装的指针。这意味着如果你把一个数组传递给一个函数，你可能会传递一个指向数组第一个元素的指针。

But if the function has a pointer to the data, it is able to manipulate that data! So changes that a function makes to an array will be visible back out in the caller.

> 但是，如果函数拥有指向数据的指针，它就能够操纵该数据！因此，函数对数组所做的更改将在调用者中可见。

Here's an example where we pass a pointer to an array to a function, the function manipulates the values in that array, and those changes are visible out in the caller.

> 这里有一个例子，我们将一个指向数组的指针传递给一个函数，该函数操纵该数组中的值，而这些变化在调用者处可见。

::: {#cb108 .sourceCode}

```c
#include <stdio.h>

void double_array(int *a, int len)
{
    // Multiply each element by 2
    //
    // This doubles the values in x in main() since x and a both point
    // to the same array in memory!

    for (int i = 0; i < len; i++)
        a[i] *= 2;
}

int main(void)
{
    int x[5] = {1, 2, 3, 4, 5};

    double_array(x, 5);

    for (int i = 0; i < 5; i++)
        printf("%d\n", x[i]);  // 2, 4, 6, 8, 10!
}
```

:::

Even though we passed the array in as parameter `a` which is type `int*`, look at how we access it using array notation with `a[i]`! Whaaaat. This is totally allowed.

> 即使我们以 `int *` 类型的数组 `a` 作为参数传入，看看我们如何使用数组符号 `a[i]` 来访问它！哇哦！这是完全允许的。

Later when we talk about the equivalence between arrays and pointers, we'll see how this makes a lot more sense. For now, it's enough to know that functions can make changes to arrays that are visible out in the caller.

> 稍后当我们讨论数组和指针之间的等价性时，我们会看到这有多么有意义。现在，只需要知道函数可以对数组进行更改，这些更改在调用者中是可见的。

### [6.6.4] Passing Multidimensional Arrays to Functions {#passing-multidimensional-arrays-to-functions number="6.6.4"}

The story changes a little when we're talking about multidimensional arrays. C needs to know all the dimensions (except the first one) so it has enough information to know where in memory to look to find a value.

> 故事在谈论多维数组时有些变化。C 需要知道所有的维度(除了第一个)，这样它就有足够的信息来知道在内存中去寻找一个值的位置。

Here's an example where we're explicit with all the dimensions:

::: {#cb109 .sourceCode}

```c
#include <stdio.h>

void print_2D_array(int a[2][3])
{
    for (int row = 0; row < 2; row++) {
        for (int col = 0; col < 3; col++)
            printf("%d ", a[row][col]);
        printf("\n");
    }
}

int main(void)
{
    int x[2][3] = {
        {1, 2, 3},
        {4, 5, 6}
    };

    print_2D_array(x);
}
```

:::

But in this case, these two[^61^] are equivalent:

> 在这种情况下，这两个是等价的：

::: {#cb110 .sourceCode}

```c
void print_2D_array(int a[2][3])
void print_2D_array(int a[][3])
```

:::

The compiler really only needs the second dimension so it can figure out how far in memory to skip for each increment of the first dimension. In general, it needs to know all the dimensions except the first one.

> 编译器只需要第二维度，以便了解每次增加第一维度时需要跳过多少内存。一般来说，它需要知道除第一维度之外的所有维度。

Also, remember that the compiler does minimal compile-time bounds checking (if you're lucky), and C does zero runtime checking of bounds. No seat belts! Don't crash by accessing array elements out of bounds!

> 也记住，编译器只做最少的编译时边界检查(如果你幸运的话)，而 C 语言不会在运行时对边界进行检查。没有安全带！不要通过访问越界的数组元素而崩溃！

# [7] Strings {#strings number="7"}

Finally! Strings! What could be simpler?

Well, turns out strings aren't actually strings in C. That's right! They're pointers! Of course they are!

> 哦，原来在 C 语言中字符串其实不是字符串。没错！它们是指针！当然是！

Much like arrays, strings in C _barely exist_.

But let's check it out---it's not really such a big deal.

## [7.1] String Literals {#string-literals number="7.1"}

Before we start, let's talk about string literals in C. These are sequences of characters in _double_ quotes (`"`). (Single quotes enclose characters, and are a different animal entirely.)

> 在我们开始之前，让我们谈谈 C 语言中的字符串文字。这些是用双引号(`"`)括起来的字符序列。(单引号括起来的是字符，它们是完全不同的东西。)

Examples:

::: {#cb111 .sourceCode}

```c
"Hello, world!\n"
"This is a test."
"When asked if this string had quotes in it, she replied, \"It does.\""
```

:::

The first one has a newline at the end---quite a common thing to see.

The last one has quotes embedded within it, but you see each is preceded by (we say "escaped by") a backslash (`\`) indicating that a literal quote belongs in the string at this point. This is how the C compiler can tell the difference between printing a double quote and the double quote at the end of the string.

> 最后一个有嵌入引号，但你会看到每个都被反斜杠(\)所前置(我们称之为“转义”)，表明在这一点上字符串中应该有一个字面上的引号。这就是 C 编译器如何区分打印双引号和字符串结尾的双引号的区别。

## [7.2] String Variables {#string-variables number="7.2"}

Now that we know how to make a string literal, let's assign it to a variable so we can do something with it.

> 现在我们知道如何创建字符串文字，让我们把它赋给一个变量，这样我们就可以用它做点什么了。

::: {#cb112 .sourceCode}

```c
char *s = "Hello, world!";
```

:::

Check out that type: pointer to a `char`. The string variable `s` is actually a pointer to the first character in that string, namely the `H`.

> 检查那种类型：指向字符的指针。字符串变量 `s` 实际上是指向该字符串中第一个字符的指针，即 `H`。

And we can print it with the `%s` (for "string") format specifier:

::: {#cb113 .sourceCode}

```c
char *s = "Hello, world!";

printf("%s\n", s);  // "Hello, world!"
```

:::

## [7.3] String Variables as Arrays {#string-variables-as-arrays number="7.3"}

Another option is this, nearly equivalent to the above `char*` usage:

::: {#cb114 .sourceCode}

```c
char s[14] = "Hello, world!";

// or, if we were properly lazy and have the compiler
// figure the length for us:

char s[] = "Hello, world!";
```

:::

This means you can use array notation to access characters in a string. Let's do exactly that to print all the characters in a string on the same line:

> 这意味着你可以使用数组符号来访问字符串中的字符。让我们确切地这样做，在同一行上打印出字符串中的所有字符：

::: {#cb115 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    char s[] = "Hello, world!";

    for (int i = 0; i < 13; i++)
        printf("%c\n", s[i]);
}
```

:::

Note that we're using the format specifier `%c` to print a single character.

> 注意我们使用格式说明符 `%c` 来打印单个字符。

Also, check this out. The program will still work fine if we change the definition of `s` to be a `char*` type:

> 也可以看看这个：如果我们把 `s` 的定义改为 `char*` 类型，程序仍然可以正常工作。

::: {#cb116 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    char *s = "Hello, world!";   // char* here

    for (int i = 0; i < 13; i++)
        printf("%c\n", s[i]);    // But still use arrays here...?
}
```

:::

And we still can use array notation to get the job done when printing it out! This is surprising, but is still only because we haven't talked about array/pointer equivalence yet. But this is yet another hint that arrays and pointers are the same thing, deep down.

> 我们仍然可以使用数组符号来完成打印任务！这令人惊讶，但仅仅是因为我们还没有讨论过数组/指针等价性。但这又是一个暗示，深层次上，数组和指针是同一回事。

## [7.4] String Initializers {#string-initializers number="7.4"}

We've already seen some examples with initializing string variables with string literals:

> 我们已经看到了一些使用字符串文字初始化字符串变量的例子：

::: {#cb117 .sourceCode}

```c
char *s = "Hello, world!";
char t[] = "Hello, again!";
```

:::

But these two are subtly different.

This one is a pointer to a string literal (i.e. a pointer to the first character in a string):

> 这是一个指向字符串文字(即指向字符串中第一个字符的指针)：

::: {#cb118 .sourceCode}

```c
char *s = "Hello, world!";
```

:::

If you try to mutate that string with this:

::: {#cb119 .sourceCode}

```c
char *s = "Hello, world!";

s[0] = 'z';  // BAD NEWS: tried to mutate a string literal!
```

:::

The behavior is undefined. Probably, depending on your system, a crash will result.

> 行为未定义。可能会根据您的系统导致崩溃。

But declaring it as an array is different. This one is a mutable _copy_ of the string that we can change at will:

> 但是把它声明为一个数组是不同的。这是一个可变的字符串副本，我们可以随意更改：

::: {#cb120 .sourceCode}

```c
char t[] = "Hello, again!";  // t is an array copy of the string
t[0] = 'z'; //  No problem

printf("%s\n", t);  // "zello, again!"
```

:::

So remember: if you have a pointer to a string literal, don't try to change it! And if you use a string in double quotes to initialize an array, that's not actually a string literal.

> 记住：如果你有一个指向字符串文字的指针，不要尝试改变它！如果你使用双引号中的字符串来初始化一个数组，那实际上不是一个字符串文字。

## [7.5] Getting String Length {#getting-string-length number="7.5"}

You can't, since C doesn't track it for you. And when I say "can't", I actually mean "can"[^62^]. There's a function in `<string.h>` called `strlen()` that can be used to compute the length of any string in bytes[^63^].

> 你不能，因为 C 不会为你跟踪它。当我说“不能”时，我实际上是说“可以”[^62^] (#fn62) {#fnref62 .footnote-ref role="doc-noteref"}。在 <string.h> 中有一个名为 strlen()的函数，可以用来计算任何字符串的字节数[^63^] (#fn63) {#fnref63 .footnote-ref role="doc-noteref"}。

::: {#cb121 .sourceCode}

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char *s = "Hello, world!";

    printf("The string is %zu bytes long.\n", strlen(s));
}
```

:::

The `strlen()` function returns type `size_t`, which is an integer type so you can use it for integer math. We print `size_t` with `%zu`.

> `strlen()` 函数返回类型 `size_t`，这是一种整数类型，因此您可以用它来进行整数运算。 我们使用 `%zu` 打印 `size_t`。

The above program prints:

::: {#cb122 .sourceCode}

```{.sourceCode .default}
The string is 13 bytes long.
```

:::

Great! So it _is_ possible to get the string length!

But... if C doesn't track the length of the string anywhere, how does it know how long the string is?

> 但是...如果 C 不跟踪字符串的长度，它怎么知道字符串有多长？

## [7.6] String Termination {#string-termination number="7.6"}

C does strings a little differently than many programming languages, and in fact differently than almost every modern programming language.

> C 对字符串的处理方式与许多编程语言不同，实际上也不同于几乎所有现代编程语言。

When you're making a new language, you have basically two options for storing a string in memory:

> 当你创建一种新的语言时，你基本上有两种选择来在内存中存储字符串：

1. Store the bytes of the string along with a number indicating the length of the string.

> 存储字符串的字节以及一个指示字符串长度的数字。

2. Store the bytes of the string, and mark the end of the string with a special byte called the _terminator_.

> 存储字符串的字节，并使用一个称为终止符的特殊字节来标记字符串的结尾。

If you want strings longer than 255 characters, option 1 requires at least two bytes to store the length. Whereas option 2 only requires one byte to terminate the string. So a bit of savings there.

> 如果你想要长度超过 255 个字符的字符串，选项 1 至少需要两个字节来存储长度。而选项 2 只需要一个字节来终止字符串，这样可以节省一点空间。

Of course, these days it seems ridiculous to worry about saving a byte (or 3---lots of languages will happily let you have strings that are 4 gigabytes in length). But back in the day, it was a bigger deal.

> 当然，现在担心节省一个字节(或 3 个字节——很多语言都可以让你使用 4GB 长度的字符串)似乎很可笑。但在过去，这是一个更大的问题。

So C took approach #2. In C, a "string" is defined by two basic characteristics:

> 所以 C 采取了第二种方法。在 C 中，一个“字符串”由两个基本特征定义：

- A pointer to the first character in the string.
- A zero-valued byte (or `NUL` character[^64^]) somewhere in memory after the pointer that indicates the end of the string.

> 一个值为零的字节(或称为“NUL”字符[^64^]<#fnref64>)存在于指示字符串结束的指针之后的内存中。

A `NUL` character can be written in C code as `\0`, though you don't often have to do this.

> 在 C 代码中可以用 `\0` 来表示 `NUL` 字符，尽管你不经常需要这么做。

When you include a string in double quotes in your code, the `NUL` character is automatically, implicitly included.

> 当你在代码中用双引号包裹一个字符串时，`NUL` 字符会自动隐式地被包含进去。

::: {#cb123 .sourceCode}

```c
char *s = "Hello!";  // Actually "Hello!\0" behind the scenes
```

:::

So with this in mind, let's write our own `strlen()` function that counts `char` s in a string until it finds a `NUL`.

> 鉴于此，让我们编写自己的 `strlen()` 函数，计算字符串中直到找到 `NUL` 为止的 `char` 数量。

The procedure is to look down the string for a single `NUL` character, counting as we go[^65^]:

> 过程是从字符串中查找单个 `NUL` 字符，并计数：

::: {#cb124 .sourceCode}

```c
int my_strlen(char *s)
{
    int count = 0;

    while (s[count] != '\0')  // Single quotes for single char
        count++;

    return count;
}
```

:::

And that's basically how the built-in `strlen()` gets the job done.

## [7.7] Copying a String {#copying-a-string number="7.7"}

You can't copy a string through the assignment operator (`=`). All that does is make a copy of the pointer to the first character... so you end up with two pointers to the same string:

> 你不能通过赋值运算符(“=”)复制一个字符串。这只会复制指向第一个字符的指针... 所以你最终得到两个指向同一个字符串的指针：

::: {#cb125 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    char s[] = "Hello, world!";
    char *t;

    // This makes a copy of the pointer, not a copy of the string!
    t = s;

    // We modify t
    t[0] = 'z';

    // But printing s shows the modification!
    // Because t and s point to the same string!

    printf("%s\n", s);  // "zello, world!"
}
```

:::

If you want to make a copy of a string, you have to copy it a byte at a time---but this is made easier with the `strcpy()` function[^66^].

> 如果你想复制一个字符串，你必须一次复制一个字节---但是使用 `strcpy()` 函数可以让这个过程变得更容易 [^66^]。

Before you copy the string, make sure you have room to copy it into, i.e. the destination array that's going to hold the characters needs to be at least as long as the string you're copying.

> 在复制字符串之前，请确保您有足够的空间将其复制到目标数组中，即要复制的字符串至少要和目标数组一样长。

::: {#cb126 .sourceCode}

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char s[] = "Hello, world!";
    char t[100];  // Each char is one byte, so plenty of room

    // This makes a copy of the string!
    strcpy(t, s);

    // We modify t
    t[0] = 'z';

    // And s remains unaffected because it's a different string
    printf("%s\n", s);  // "Hello, world!"

    // But t has been changed
    printf("%s\n", t);  // "zello, world!"
}
```

:::

Notice with `strcpy()`, the destination pointer is the first argument, and the source pointer is the second. A mnemonic I use to remember this is that it's the order you would have put `t` and `s` if an assignment `=` worked for strings, with the source on the right and the destination on the left.

> 注意使用 `strcpy()` 时，目标指针是第一个参数，源指针是第二个参数。我用来记住这一点的技巧是，如果字符串可以使用赋值 `=` 操作，那么源在右边，目标在左边，就是 `t` 和 `s` 的顺序。

# [8] Structs {#structs number="8"}

In C, we have something called a `struct`, which is a user-definable type that holds multiple pieces of data, potentially of different types.

> 在 C 语言中，我们有一种叫做 `struct` 的东西，它是一种用户可定义的类型，可以容纳多个不同类型的数据。

It's a convenient way to bundle multiple variables into a single one. This can be beneficial for passing variables to functions (so you just have to pass one instead of many), and useful for organizing data and making code more readable.

> 这是一种将多个变量捆绑到一个变量的方便方法。这对于将变量传递给函数(只需要传递一个而不是多个)是有益的，对于组织数据和使代码更具可读性也很有用。

If you've come from another language, you might be familiar with the idea of _classes_ and _objects_. These don't exist in C, natively[^67^]. You can think of a `struct` as a class with only data members, and no methods.

> 如果你来自另一种语言，你可能熟悉_类_和_对象_的概念。这些在 C 语言中本身不存在[^67^]。你可以把 `struct` 看作是一个只有数据成员，没有方法的类。

## [8.1] Declaring a Struct {#declaring-a-struct number="8.1"}

You can declare a `struct` in your code like so:

::: {#cb127 .sourceCode}

```c
struct car {
    char *name;
    float price;
    int speed;
};
```

:::

This is often done at the global scope outside any functions so that the `struct` is globally available.

> 这通常在全局作用域之外的任何函数中完成，以便 `struct` 可以全局使用。

When you do this, you're making a new _type_. The full type name is `struct car`. (Not just `car`---that won't work.)

> 当你这样做时，你正在创建一种新的类型。完整的类型名称是 `struct car`(不只是 `car`---这样不行)。

There aren't any variables of that type yet, but we can declare some:

::: {#cb128 .sourceCode}

```c
struct car saturn;  // Variable "saturn" of type "struct car"
```

:::

And now we have an uninitialized variable `saturn`[^68^] of type `struct car`.

> 现在我们有一个未初始化的变量 `saturn`(参见注释 68)，类型为 `struct car`。

We should initialize it! But how do we set the values of those individual fields?

> 我们应该初始化它！但是我们如何设置这些单独字段的值？

Like in many other languages that stole it from C, we're going to use the dot operator (`.`) to access the individual fields.

> 就像在许多从 C 偷来的其他语言中一样，我们将使用点运算子(`.`)来访问个别字段。

::: {#cb129 .sourceCode}

```c
saturn.name = "Saturn SL/2";
saturn.price = 15999.99;
saturn.speed = 175;

printf("Name:           %s\n", saturn.name);
printf("Price (USD):    %f\n", saturn.price);
printf("Top Speed (km): %d\n", saturn.speed);
```

:::

There on the first lines, we set the values in the `struct car`, and then in the next bit, we print those values out.

> 在第一行，我们在 `struct car` 中设置了值，然后在下一段中，我们打印出这些值。

## [8.2] Struct Initializers {#struct-initializers number="8.2"}

That example in the previous section was a little unwieldy. There must be a better way to initialize that `struct` variable!

> 上一节中的那个例子有点繁琐。一定有更好的方法来初始化那个 `struct` 变量！

You can do it with an initializer by putting values in for the fields _in the order they appear in the `struct`_ when you define the variable. (This won't work after the variable has been defined---it has to happen in the definition).

> 你可以通过在定义变量时为字段提供值(按照它们在结构中出现的顺序)来使用初始化程序(这在变量定义后不起作用---必须在定义时发生)。

::: {#cb130 .sourceCode}

```c
struct car {
    char *name;
    float price;
    int speed;
};

// Now with an initializer! Same field order as in the struct declaration:
struct car saturn = {"Saturn SL/2", 16000.99, 175};

printf("Name:      %s\n", saturn.name);
printf("Price:     %f\n", saturn.price);
printf("Top Speed: %d km\n", saturn.speed);
```

:::

The fact that the fields in the initializer need to be in the same order is a little freaky. If someone changes the order in `struct car`, it could break all the other code!

> 事实上，初始化程序中的字段需要按相同的顺序排列有点可怕。如果有人改变 `struct car` 中的顺序，可能会破坏所有其他代码！

We can be more specific with our initializers:

::: {#cb131 .sourceCode}

```c
struct car saturn = {.speed=175, .name="Saturn SL/2"};
```

:::

Now it's independent of the order in the `struct` declaration. Which is safer code, for sure.

> 现在它独立于结构声明中的顺序，这是更安全的代码。

Similar to array initializers, any missing field designators are initialized to zero (in this case, that would be `.price`, which I've omitted).

> 类似于数组初始化，任何缺失的字段指示符都会被初始化为零(在这种情况下，就是我省略的 `.price`)。

## [8.3] Passing Structs to Functions {#passing-structs-to-functions number="8.3"}

You can do a couple things to pass a `struct` to a function.

1. Pass the `struct`.
2. Pass a pointer to the `struct`.

Recall that when you pass something to a function, a _copy_ of that thing gets made for the function to operate on, whether it's a copy of a pointer, an `int`, a `struct`, or anything.

> 当你把某件事传递给一个函数时，会为该函数创建一个_副本_，无论它是指针的副本、`int` 的副本、`struct` 的副本还是其他任何东西的副本。

There are basically two cases when you'd want to pass a pointer to the `struct`:

> 基本上有两种情况你会想要传递一个指向结构体的指针：

1. You need the function to be able to make changes to the `struct` that was passed in, and have those changes show in the caller.

> 你需要这个函数能够对传入的 `struct` 进行修改，并且在调用者中看到这些修改。

2. The `struct` is somewhat large and it's more expensive to copy that onto the stack than it is to just copy a pointer[^69^].

> 结构体有点大，把它复制到堆栈比只复制一个指针要贵得多。

For those two reasons, it's far more common to pass a pointer to a `struct` to a function, though its by no means illegal to pass the `struct` itself.

> 由于这两个原因，传递指向结构体的指针到函数更为常见，尽管传递结构体本身并不违法。

Let's try passing in a pointer, making a function that will allow you to set the `.price` field of the `struct car`:

> 让我们尝试传入一个指针，创建一个函数，让你可以设置 `struct car` 的 `price` 字段：

::: {#cb132 .sourceCode}

```c
#include <stdio.h>

struct car {
    char *name;
    float price;
    int speed;
};

int main(void)
{
    struct car saturn = {.speed=175, .name="Saturn SL/2"};

    // Pass a pointer to this struct car, along with a new,
    // more realistic, price:
    set_price(&saturn, 799.99);

    printf("Price: %f\n", saturn.price);
}
```

:::

You should be able to come up with the function signature for `set_price()` just by looking at the types of the arguments we have there.

> 你应该能够仅仅通过查看参数的类型就能想出 `set_price()` 的函数签名。

`saturn` is a `struct car`, so `&saturn` must be the address of the `struct car`, AKA a pointer to a `struct car`, namely a `struct car*`.

And `799.99` is a `float`.

So the function declaration must look like this:

::: {#cb133 .sourceCode}

```c
void set_price(struct car *c, float new_price)
```

:::

We just need to write the body. One attempt might be:

::: {#cb134 .sourceCode}

```c
void set_price(struct car *c, float new_price) {
    c.price = new_price;  // ERROR!!
}
```

:::

That won't work because the dot operator only works on `struct` s... it doesn't work on _pointers_ to `struct` s.

> 那不行，因为点运算符只适用于 `struct`，不适用于 `struct` 的指针。

Ok, so we can dereference the `struct` to de-pointer it to get to the `struct` itself. Dereferencing a `struct car*` results in the `struct car` that the pointer points to, which we should be able to use the dot operator on:

> 好的，所以我们可以取消引用结构体以取消指针，以获得结构体本身。 取消引用 struct car *结果为指针指向的 struct car，我们应该能够使用点运算符：

::: {#cb135 .sourceCode}

```c
void set_price(struct car *c, float new_price) {
    (*c).price = new_price;  // Works, but is ugly and non-idiomatic :(
}
```

:::

And that works! But it's a little clunky to type all those parens and the asterisk. C has some syntactic sugar called the _arrow operator_ that helps with that.

> 而且这可以工作！但是要输入所有的括号和星号有点繁琐。C 有一些叫做箭头操作符的语法糖，可以帮助解决这个问题。

## [8.4] The Arrow Operator {#the-arrow-operator number="8.4"}

The arrow operator helps refer to fields in pointers to `struct` s.

::: {#cb136 .sourceCode}

```c
void set_price(struct car *c, float new_price) {
    // (*c).price = new_price;  // Works, but non-idiomatic :(
    //
    // The line above is 100% equivalent to the one below:

    c->price = new_price;  // That's the one!
}
```

:::

So when accessing fields, when do we use dot and when do we use arrow?

- If you have a `struct`, use dot (`.`).
- If you have a pointer to a `struct`, use arrow (`->`).

## [8.5] Copying and Returning `struct` s {#copying-and-returning-structs number="8.5"}

Here's an easy one for you!

Just assign from one to the other!

::: {#cb137 .sourceCode}

```c
struct car a, b;

b = a;  // Copy the struct
```

:::

And returning a `struct` (as opposed to a pointer to one) from a function also makes a similar copy to the receiving variable.

> 返回一个 `struct`(而不是指向它的指针)从一个函数也会给接收变量做一个类似的复制。

This is not a "deep copy"[^70^]. All fields are copied as-is, including pointers to things.

> 这不是一个“深拷贝”[^70^]。所有字段都是原样复制，包括指向物体的指针。

## [8.6] Comparing `struct` s {#comparing-structs number="8.6"}

There's only one safe way to do it: compare each field one at a time.

You might think you could use [`memcmp()`](https://beej.us/guide/bgclr/html/split/stringref.html#man-strcmp)[^71^], but that doesn't handle the case of the possible [padding bytes](#struct-padding-bytes) that might be in there.

> 你可能会认为可以使用 memcmp()，但这不能处理可能存在的填充字节的情况。

If you clear the `struct` to zero first with [`memset()`](https://beej.us/guide/bgclr/html/split/stringref.html#man-memset)[^72^], then it _might_ work, though there could be weird elements that [might not compare as you expect](https://stackoverflow.com/questions/141720/how-do-you-compare-structs-for-equality-in-c)[^73^].

> 如果你先用[`memset()`](https://beej.us/guide/bgclr/html/split/stringref.html#man-memset)[^72^]把 `struct` 清零，那么它_可能_会起作用，但也可能会有一些奇怪的元素[不能按你期望的方式比较](https://stackoverflow.com/questions/141720/how-do-you-compare-structs-for-equality-in-c)[^73^]。

# [9] File Input/Output {#file-inputoutput number="9"}

We've already seen a couple examples of I/O with `scanf()` and `printf()` for doing I/O at the console (screen/keyboard).

> 我们已经看到了使用 `scanf()` 和 `printf()` 在控制台(屏幕/键盘)进行 I/O 的几个例子。

But we'll push those concepts a little farther this chapter.

## [9.1] The `FILE*` Data Type {#the-file-data-type number="9.1"}

When we do any kind of I/O in C, we do so through a piece of data that you get in the form of a `FILE*` type. This `FILE*` holds all the information needed to communicate with the I/O subsystem about which file you have open, where you are in the file, and so on.

> 当我们在 C 中进行任何类型的 I/O 操作时，我们都会以 `FILE*` 类型的数据形式获取。这个 `FILE*` 保存着所有与 I/O 子系统通信所需的信息，比如您打开了哪个文件，您在文件中的位置等等。

The spec refers to these as _streams_, i.e. a stream of data from a file or from any source. I'm going to use "files" and "streams" interchangeably, but really you should think of a "file" as a special case of a "stream". There are other ways to stream data into a program than just reading from a file.

> 规范将这些称为_流_，即来自文件或任何来源的数据流。我将使用“文件”和“流”交替使用，但实际上您应该将“文件”视为“流”的特殊情况。除了从文件读取之外，还有其他方法将数据流入程序。

We'll see in a moment how to go from having a filename to getting an open `FILE*` for it, but first I want to mention three streams that are already open for you and ready for use.

> 我们马上就会看到如何从文件名获得一个打开的 `FILE*`，但首先我想提及三个已经为您打开并准备使用的流。

`FILE*` name Description

---

`stdin` Standard Input, generally the keyboard by default
`stdout` Standard Output, generally the screen by default
`stderr` Standard Error, generally the screen by default, as well

We've actually been using these implicitly already, it turns out. For example, these two calls are the same:

> 我们其实已经隐式地使用了这些，结果发现，这两个调用是一样的。

::: {#cb138 .sourceCode}

```c
printf("Hello, world!\n");
fprintf(stdout, "Hello, world!\n");  // printf to a file
```

:::

But more on that later.

Also you'll notice that both `stdout` and `stderr` go to the screen. While this seems at first either like an oversight or redundancy, it actually isn't. Typical operating systems allow you to _redirect_ the output of either of those into different files, and it can be convenient to be able to separate error messages from regular non-error output.

> 此外，您还会注意到 `stdout` 和 `stderr` 都会输出到屏幕上。虽然这似乎一开始是一个疏忽或冗余，但实际上并非如此。典型的操作系统允许您将这两者的输出重定向到不同的文件中，将错误消息与常规非错误输出分开可能会很方便。

For example, in a POSIX shell (like sh, ksh, bash, zsh, etc.) on a Unix-like system, we could run a program and send just the non-error (`stdout`) output to one file, and all the error (`stderr`) output to another file.

> 例如，在类 Unix 系统上的 POSIX shell(如 sh、ksh、bash、zsh 等)中，我们可以运行一个程序，将非错误(`stdout`)输出发送到一个文件，将所有错误(`stderr`)输出发送到另一个文件。

::: {#cb139 .sourceCode}

```zsh
./foo > output.txt 2> errors.txt   # This command is Unix-specific
```

:::

For this reason, you should send serious error messages to `stderr` instead of `stdout`.

> 因此，您应该将严重错误消息发送到 `stderr` 而不是 `stdout`。

More on how to do that later.

## [9.2] Reading Text Files {#reading-text-files number="9.2"}

Streams are largely categorized two different ways: _text_ and _binary_.

Text streams are allowed to do significant translation of the data, most notably translations of newlines to their different representations[^74^]. Text files are logically a sequence of _lines_ separated by newlines. To be portable, your input data should always end with a newline.

> 文本流允许对数据进行重要的翻译，尤其是对换行符的不同表示的翻译 [^74^]。文本文件逻辑上是由换行符分隔的_行_序列。为了可移植性，您的输入数据应始终以换行符结尾。

But the general rule is that if you're able to edit the file in a regular text editor, it's a text file. Otherwise, it's binary. More on binary later.

> 但是一般的规则是，如果你能够在常规文本编辑器中编辑文件，那么它就是文本文件。否则，它就是二进制文件。稍后会有更多关于二进制的内容。

So let's get to work---how do we open a file for reading, and pull data out of it?

> 让我们开始工作吧---我们怎样打开一个文件进行读取，并从中提取数据？

Let's create a file called `hello.txt` that has just this in it:

::: {#cb140 .sourceCode}

```{.sourceCode .default}
Hello, world!
```

:::

And let's write a program to open the file, read a character out of it, and then close the file when we're done. That's the game plan!

> 让我们编写一个程序来打开文件、从中读取一个字符，然后在完成时关闭文件。这就是计划！

::: {#cb141 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;                      // Variable to represent open file

    fp = fopen("hello.txt", "r");  // Open file for reading

    int c = fgetc(fp);             // Read a single character
    printf("%c\n", c);             // Print char to stdout

    fclose(fp);                    // Close the file when done
}
```

:::

See how when we opened the file with `fopen()`, it returned the `FILE*` to us so we could use it later.

> 看看当我们用 `fopen()` 打开文件时，它会返回一个 `FILE*` 给我们，以便我们稍后使用。

(I'm leaving it out for brevity, but `fopen()` will return `NULL` if something goes wrong, like file-not-found, so you should really error check it!)

> (为了简洁起见，我把它省略了，但是如果出现文件未找到等错误，`fopen()` 将会返回 `NULL`，所以你应该做错误检查！)

Also notice the `"r"` that we passed in---this means "open a text stream for reading". (There are various strings we can pass to `fopen()` with additional meaning, like writing, or appending, and so on.)

> 此外，注意我们传递的 `"r"`——这意味着“打开一个文本流以进行读取”。(我们可以传递给 `fopen()` 具有其他含义的各种字符串，例如写入或追加等。)

After that, we used the `fgetc()` function to get a character from the stream. You might be wondering why I've made `c` an `int` instead of a `char`---hold that thought!

> 接下来，我们使用 `fgetc()` 函数从流中获取一个字符。你可能想知道为什么我把 `c` 设置为 `int` 而不是 `char`——暂且把这个想法放在一边吧！

Finally, we close the stream when we're done with it. All streams are automatically closed when the program exits, but it's good form and good housekeeping to explicitly close any files yourself when done with them.

> 最后，当我们完成使用时，我们关闭流。当程序退出时，所有流都会自动关闭，但是明确关闭它们本身是一种良好的形式和良好的房屋管理。

The `FILE*` keeps track of our position in the file. So subsequent calls to `fgetc()` would get the next character in the file, and then the next, until the end.

> 文件指针 `FILE*` 记录我们在文件中的位置。因此，随后对 `fgetc()` 的调用将获取文件中的下一个字符，然后是下一个，直到结束。

But that sounds like a pain. Let's see if we can make it easier.

## [9.3] End of File: `EOF` {#end-of-file-eof number="9.3"}

There is a special character defined as a macro: `EOF`. This is what `fgetc()` will return when the end of the file has been reached and you've attempted to read another character.

> 有一个特殊字符被定义为宏：`EOF`。当文件结束，而你试图读取另一个字符时，`fgetc()` 将返回此值。

How about I share that Fun Fact™, now. Turns out `EOF` is the reason why `fgetc()` and functions like it return an `int` instead of a `char`. `EOF` isn't a character proper, and its value likely falls outside the range of `char`. Since `fgetc()` needs to be able to return any byte **and** `EOF`, it needs to be a wider type that can hold more values. so `int` it is. But unless you're comparing the returned value against `EOF`, you can know, deep down, it's a `char`.

> 怎么样，我现在分享一个有趣的事实 ™。原来 EOF 就是为什么 fgetc()和类似的函数返回 int 而不是 char 的原因。EOF 不是一个真正的字符，它的值可能超出 char 的范围。由于 fgetc()需要能够返回任何字节和 EOF，它需要一个更宽的类型来容纳更多的值。所以是 int。但是除非你把返回的值与 EOF 进行比较，否则你可以深知，它是一个 char。

All right! Back to reality! We can use this to read the whole file in a loop.

> 好的！回到现实！我们可以用这个在循环中读取整个文件。

::: {#cb142 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    int c;

    fp = fopen("hello.txt", "r");

    while ((c = fgetc(fp)) != EOF)
        printf("%c", c);

    fclose(fp);
}
```

:::

(If line 10 is too weird, just break it down starting with the innermost-nested parens. The first thing we do is assign the result of `fgetc()` into `c`, and _then_ we compare _that_ against `EOF`. We've just crammed it into a single line. This might look hard to read, but study it---it's idiomatic C.)

> 如果第 10 行太奇怪，可以从最里层的括号开始分解。我们首先要做的是将 `fgetc()` 的结果赋值给 `c`，然后将其与 `EOF` 进行比较。我们把它塞进了一行。这看起来可能很难读懂，但要仔细研究一下，这是 C 语言的惯用法。

And running this, we see:

::: {#cb143 .sourceCode}

```{.sourceCode .default}
Hello, world!
```

:::

But still, we're operating a character at a time, and lots of text files make more sense at the line level. Let's switch to that.

> 然而，我们仍然是一次操作一个字符，很多文本文件在行级别上更有意义。让我们切换到那个。

### [9.3.1] Reading a Line at a Time {#reading-a-line-at-a-time number="9.3.1"}

So how can we get an entire line at once? `fgets()` to the rescue! For arguments, it takes a pointer to a `char` buffer to hold bytes, a maximum number of bytes to read, and a `FILE*` to read from. It returns `NULL` on end-of-file or error. `fgets()` is even nice enough to NUL-terminate the string when its done[^75^].

> fgets() 可以拯救我们！它的参数是一个指向字符缓冲区的指针，用来存储字节，一个最大读取字节数，以及一个从中读取的 FILE*。当到达文件末尾或发生错误时，它会返回 NULL。fgets()甚至还会在完成时 NUL 终止字符串(NUL-terminate the string)。

Let's do a similar loop as before, except let's have a multiline file and read it in a line at a time.

> 让我们做一个类似的循环，就像之前一样，但让我们有一个多行文件，一次读取一行。

Here's a file `quote.txt`:

::: {#cb144 .sourceCode}

```{.sourceCode .default}
A wise man can learn more from
a foolish question than a fool
can learn from a wise answer.
                  --Bruce Lee
```

:::

And here's some code that reads that file a line at a time and prints out a line number before each one:

> 这里有一段代码，可以一行一行地读取文件，并在每一行前面打印出行号：

::: {#cb145 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char s[1024];  // Big enough for any line this program will encounter
    int linecount = 0;

    fp = fopen("quote.txt", "r");

    while (fgets(s, sizeof s, fp) != NULL)
        printf("%d: %s", ++linecount, s);

    fclose(fp);
}
```

:::

Which gives the output:

::: {#cb146 .sourceCode}

```{.sourceCode .default}
1: A wise man can learn more from
2: a foolish question than a fool
3: can learn from a wise answer.
4:                   --Bruce Lee
```

:::

## [9.4] Formatted Input {#formatted-input number="9.4"}

You know how you can get formatted output with `printf()` (and, thus, `fprintf()` like we'll see, below)?

> 你知道你可以使用 `printf()`(以及我们将在下面看到的 `fprintf()`)获得格式化的输出吗？

You can do the same thing with `fscanf()`.

Let's have a file with a series of data records in it. In this case, whales, with name, length in meters, and weight in tonnes. `whales.txt`:

> 让我们有一个文件，里面有一系列的数据记录。这里是鲸鱼，有名字、米数和吨数。`whales.txt`：

::: {#cb147 .sourceCode}

```{.sourceCode .default}
blue 29.9 173
right 20.7 135
gray 14.9 41
humpback 16.0 30
```

:::

Yes, we could read these with `fgets()` and then parse the string with `sscanf()` (and in some ways that's more resilient against corrupted files), but in this case, let's just use `fscanf()` and pull it in directly.

> 是的，我们可以使用 `fgets()` 读取这些，然后用 `sscanf()` 解析字符串(在某些情况下，这更能抵抗损坏的文件)，但是在这种情况下，让我们直接使用 `fscanf()` 把它拉进来。

The `fscanf()` function skips leading whitespace when reading, and returns `EOF` on end-of-file or error.

> `fscanf()` 函数在读取时会跳过前导空格，在文件结尾或发生错误时会返回 `EOF`。

::: {#cb148 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char name[1024];  // Big enough for any line this program will encounter
    float length;
    int mass;

    fp = fopen("whales.txt", "r");

    while (fscanf(fp, "%s %f %d", name, &length, &mass) != EOF)
        printf("%s whale, %d tonnes, %.1f meters\n", name, mass, length);

    fclose(fp);
}
```

:::

Which gives the result:

::: {#cb149 .sourceCode}

```{.sourceCode .default}
blue whale, 173 tonnes, 29.9 meters
right whale, 135 tonnes, 20.7 meters
gray whale, 41 tonnes, 14.9 meters
humpback whale, 30 tonnes, 16.0 meters
```

:::

## [9.5] Writing Text Files {#writing-text-files number="9.5"}

In much the same way we can use `fgetc()`, `fgets()`, and `fscanf()` to read text streams, we can use `fputc()`, `fputs()`, and `fprintf()` to write text streams.

> 同样的，我们可以使用 `fgetc()`，`fgets()` 和 `fscanf()` 来读取文本流，我们可以使用 `fputc()`，`fputs()` 和 `fprintf()` 来写入文本流。

To do so, we have to `fopen()` the file in write mode by passing `"w"` as the second argument. Opening an existing file in `"w"` mode will instantly truncate that file to 0 bytes for a full overwrite.

> 要做到这一点，我们必须通过将“w”作为第二个参数来以写模式打开文件 `fopen()`。 以“w”模式打开现有文件将立即将该文件截断为 0 字节以进行完全覆盖。

We'll put together a simple program that outputs a file `output.txt` using a variety of output functions.

> 我们将使用各种输出函数组装一个简单的程序，以输出一个名为 `output.txt` 的文件。

::: {#cb150 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    int x = 32;

    fp = fopen("output.txt", "w");

    fputc('B', fp);
    fputc('\n', fp);   // newline
    fprintf(fp, "x = %d\n", x);
    fputs("Hello, world!\n", fp);

    fclose(fp);
}
```

:::

And this produces a file, `output.txt`, with these contents:

::: {#cb151 .sourceCode}

```{.sourceCode .default}
B
x = 32
Hello, world!
```

:::

Fun fact: since `stdout` is a file, you could replace line 8 with:

::: {#cb152 .sourceCode}

```c
fp = stdout;
```

:::

and the program would have outputted to the console instead of to a file. Try it!

> 程序会输出到控制台而不是文件中。试试看！

## [9.6] Binary File I/O {#binary-file-io number="9.6"}

So far we've just been talking text files. But there's that other beast we mentioned early on called _binary_ files, or binary streams.

> 到目前为止，我们只讨论文本文件。但是我们早先提到的另一种叫做_二进制_文件或二进制流的东西。

These work very similarly to text files, except the I/O subsystem doesn't perform any translations on the data like it might with a text file. With binary files, you get a raw stream of bytes, and that's all.

> 这些工作与文本文件非常相似，只是 I / O 子系统不会对数据执行任何转换，就像它可能与文本文件一样。使用二进制文件，您将获得原始字节流，仅此而已。

The big difference in opening the file is that you have to add a `"b"` to the mode. That is, to read a binary file, open it in `"rb"` mode. To write a file, open it in `"wb"` mode.

> 打开文件的最大区别是你必须在模式中添加一个 `"b"`。也就是说，要读取二进制文件，请以 `"rb"` 模式打开它。要写入文件，请以 `"wb"` 模式打开它。

Because it's streams of bytes, and streams of bytes can contain NUL characters, and the NUL character is the end-of-string marker in C, it's rare that people use the `fprintf()`-and-friends functions to operate on binary files.

> 由于它是字节流，而字节流可以包含 NUL 字符，而 NUL 字符是 C 中的结束字符标记，因此人们很少使用 `fprintf()` 等函数来操作二进制文件。

Instead the most common functions are `fread()` and `fwrite()`. The functions read and write a specified number of bytes to the stream.

> 最常用的函数是 `fread()` 和 `fwrite()`。这些函数从流中读取和写入指定数量的字节。

To demo, we'll write a couple programs. One will write a sequence of byte values to disk all at once. And the second program will read a byte at a time and print them out[^76^].

> 为了演示，我们将编写几个程序。一个将一次性将一系列字节值写入磁盘，另一个程序将一次读取一个字节，并将其打印出来。

::: {#cb153 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    unsigned char bytes[6] = {5, 37, 0, 88, 255, 12};

    fp = fopen("output.bin", "wb");  // wb mode for "write binary"!

    // In the call to fwrite, the arguments are:
    //
    // * Pointer to data to write
    // * Size of each "piece" of data
    // * Count of each "piece" of data
    // * FILE*

    fwrite(bytes, sizeof(char), 6, fp);

    fclose(fp);
}
```

:::

Those two middle arguments to `fwrite()` are pretty odd. But basically what we want to tell the function is, "We have items that are _this_ big, and we want to write _that_ many of them." This makes it convenient if you have a record of a fixed length, and you have a bunch of them in an array. You can just tell it the size of one record and how many to write.

> 这两个中间参数对 `fwrite()` 来说真的有点奇怪。但基本上我们想告诉这个函数的是，“我们有_this_大小的项目，我们想写_that_多个。”如果你有一个固定长度的记录，并且你有一堆它们在数组中，这将很方便。你只需要告诉它一个记录的大小和要写多少个。

In the example above, we tell it each record is the size of a `char`, and we have 6 of them.

> 在上面的例子中，我们告诉它每条记录的大小是一个 `char`，我们有 6 个。

Running the program gives us a file `output.bin`, but opening it in a text editor doesn't show anything friendly! It's binary data---not text. And random binary data I just made up, at that!

> 运行程序会给我们一个文件 `output.bin`，但是在文本编辑器中打开它却没有任何友好的内容！这是二进制数据——而不是文本。而且是我刚刚编造出来的随机二进制数据！

If I run it through a [hex dump](https://en.wikipedia.org/wiki/Hex_dump)[^77^] program, we can see the output as bytes:

> 如果我将它通过十六进制转储程序运行，我们可以将输出作为字节查看：

::: {#cb154 .sourceCode}

```{.sourceCode .default}
05 25 00 58 ff 0c
```

:::

And those values in hex do match up to the values (in decimal) that we wrote out.

> 这些十六进制的值确实与我们写出的十进制值相匹配。

But now let's try to read them back in with a different program. This one will open the file for binary reading (`"rb"` mode) and will read the bytes one at a time in a loop.

> 现在让我们用另一个程序读取它们。这个程序将以二进制模式打开文件(“rb”模式)，并以循环的方式一次读取一个字节。

`fread()` has the neat feature where it returns the number of bytes read, or `0` on EOF. So we can loop until we see that, printing numbers as we go.

::: {#cb155 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    unsigned char c;

    fp = fopen("output.bin", "rb"); // rb for "read binary"!

    while (fread(&c, sizeof(char), 1, fp) > 0)
        printf("%d\n", c);
}
```

:::

And, running it, we see our original numbers!

::: {#cb156 .sourceCode}

```{.sourceCode .default}
5
37
0
88
255
12
```

:::

Woo hoo!

### [9.6.1] `struct` and Number Caveats {#struct-and-number-caveats number="9.6.1"}

As we saw in the `struct` s section, the compiler is free to add padding to a `struct` as it sees fit. And different compilers might do this differently. And the same compiler on different architectures could do it differently. And the same compiler on the same architectures could do it differently.

> 正如我们在“struct”部分所看到的，编译器可以根据自己的意愿为“struct”添加填充。不同的编译器可能会有不同的做法，同一个编译器在不同的架构上也可能会有不同的做法，甚至同一个编译器在同一个架构上也可能会有不同的做法。

What I'm getting at is this: it's not portable to just `fwrite()` an entire `struct` out to a file when you don't know where the padding will end up.

> 我的意思是：如果你不知道填充会放在哪里，只使用 `fwrite()` 将整个 `struct` 写入文件是不可移植的。

How do we fix this? Hold that thought---we'll look at some ways to do this after looking at another related problem.

> 我们怎么解决这个问题？先把这个想法放在一边---我们在研究另一个相关问题后再看看有什么办法可以解决这个问题。

Numbers!

Turns out all architectures don't represent numbers in memory the same way.

> 原来，所有的架构都不会以相同的方式在内存中表示数字。

Let's look at a simple `fwrite()` of a 2-byte number. We'll write it in hex so each byte is clear. The most significant byte will have the value `0x12` and the least significant will have the value `0x34`.

> 让我们来看一个简单的 2 字节数字的 fwrite()。我们将以十六进制的形式写入，以便每个字节都清晰可见。最高有效字节的值为 0x12，最低有效字节的值为 0x34。

::: {#cb157 .sourceCode}

```c
unsigned short v = 0x1234;  // Two bytes, 0x12 and 0x34

fwrite(&v, sizeof v, 1, fp);
```

:::

What ends up in the stream?

Well, it seems like it should be `0x12` followed by `0x34`, right?

But if I run this on my machine and hex dump the result, I get:

::: {#cb158 .sourceCode}

```{.sourceCode .default}
34 12
```

:::

They're reversed! What gives?

This has something to do with what's called the [_endianess_](https://en.wikipedia.org/wiki/Endianess)[^78^] of the architecture. Some write the most significant bytes first, and some the least significant bytes first.

> 这与所谓的[_endianess_](https://zh.wikipedia.org/wiki/%E5%AD%97%E8%8A%82%E5%BA%8F)[^78^]有关。有些会先写最重要的字节，有些会先写最不重要的字节。

This means that if you write a multibyte number out straight from memory, you can't do it in a portable way[^79^].

> 这意味着，如果你直接从内存中写出多字节数字，你就无法以一种可移植的方式来做到这一点[^79^]。

A similar problem exists with floating point. Most systems use the same format for their floating point numbers, but some do not. No guarantees!

> 相似的问题也存在于浮点数。大多数系统使用相同的格式来表示它们的浮点数，但有些系统并不这样做。没有保证！

So... how can we fix all these problems with numbers and `struct` s to get our data written in a portable way?

> 那么...我们如何用数字和 `struct` 来修复这些问题，以便以便把我们的数据以可移植的方式写入？

The summary is to _serialize_ the data, which is a general term that means to take all the data and write it out in a format that you control, that is well-known, and programmable to work the same way on all platforms.

> 概括而言，就是要对数据进行序列化，这是一个普遍的术语，意思是把所有的数据都写出来，以您控制的、众所周知的、可编程的格式，在所有平台上都能够以同样的方式工作。

As you might imagine, this is a solved problem. There are a bunch of serialization libraries you can take advantage of, such as Google's [_protocol buffers_](https://en.wikipedia.org/wiki/Protocol_buffers)[^80^], out there and ready to use. They will take care of all the gritty details for you, and even will allow data from your C programs to interoperate with other languages that support the same serialization methods.

> 可以想象，这是一个已经解决的问题。有很多序列化库可以供您使用，比如谷歌的[协议缓冲器](https://en.wikipedia.org/wiki/Protocol_buffers)[^80^]，它们可以帮助您处理所有细节，甚至可以让您的 C 程序与支持相同序列化方法的其他语言互操作。

Do yourself and everyone a favor! Serialize your binary data when you write it to a stream! This will keep things nice and portable, even if you transfer data files from one architecture to another.

> 请为自己和其他人做个好事！在将二进制数据写入流时，请将其序列化！这样即使您将数据文件从一个架构传输到另一个架构，也可以保持良好的可移植性。

# [10] `typedef`: Making New Types {#typedef-making-new-types number="10"}

Well, not so much making _new_ types as getting new names for existing types. Sounds kinda pointless on the surface, but we can really use this to make our code cleaner.

> 嗯，不是那么多创造新类型，而是为现有类型获得新的名称。表面上看起来似乎毫无意义，但我们可以用它来让我们的代码更加清晰。

## [10.1] `typedef` in Theory {#typedef-in-theory number="10.1"}

Basically, you take an existing type and you make an alias for it with `typedef`.

> 基本上，你可以使用 `typedef` 为现有类型创建一个别名。

Like this:

::: {#cb159 .sourceCode}

```c
typedef int antelope;  // Make "antelope" an alias for "int"

antelope x = 10;       // Type "antelope" is the same as type "int"
```

:::

You can take any existing type and do it. You can even make a number of types with a comma list:

> 你可以选择任何现有的类型并进行操作。你甚至可以使用逗号列表创建多种类型：

::: {#cb160 .sourceCode}

```c
typedef int antelope, bagel, mushroom;  // These are all "int"
```

:::

That's really useful, right? That you can type `mushroom` instead of `int`? You must be _super excited_ about this feature!

> 真的很有用，对吗？你可以用 `mushroom` 而不是 `int`？你一定对这个功能_超级兴奋_！

OK, Professor Sarcasm---we'll get to some more common applications of this in a moment.

> 好的，讽刺教授——我们马上就会看到这个的更多普通应用。

### [10.1.1] Scoping {#scoping number="10.1.1"}

`typedef` follows regular [scoping rules](#scope).

For this reason, it's quite common to find `typedef` at file scope ("global") so that all functions can use the new types at will.

> 因此，在文件范围(“全局”)中发现 `typedef` 是很常见的，这样所有函数都可以随意使用新类型。

## [10.2] `typedef` in Practice {#typedef-in-practice number="10.2"}

So renaming `int` to something else isn't that exciting. Let's see where `typedef` commonly makes an appearance.

> 所以把 `int` 改名可不是什么令人兴奋的事情。让我们看看 `typedef` 通常出现在哪里。

### [10.2.1] `typedef` and `struct` s {#typedef-struct number="10.2.1"}

Sometimes a `struct` will be `typedef`'d to a new name so you don't have to type the word `struct` over and over.

> 有时候会把 `struct` 类型定义为新的名字，这样就不用一遍又一遍地输入 `struct` 这个词了。

::: {#cb161 .sourceCode}

```c
struct animal {
    char *name;
    int leg_count, speed;
};

//  original name      new name
//            |         |
//            v         v
//      |-----------| |----|
typedef struct animal animal;

struct animal y;  // This works
animal z;         // This also works because "animal" is an alias
```

:::

Personally, I don't care for this practice. I like the clarity the code has when you add the word `struct` to the type; programmers know what they're getting. But it's really common so I'm including it here.

> 我个人不喜欢这种做法。当你在类型上添加单词“struct”时，代码具有清晰的特点，程序员知道他们得到了什么。但这种做法非常普遍，所以我在这里也包括它。

Now I want to run the exact same example in a way that you might commonly see. We're going to put the `struct animal` _in_ the `typedef`. You can mash it all together like this:

> 现在我想以一种你经常看到的方式运行相同的示例。我们将把 `struct animal` 放入 `typedef` 中。你可以将它们混合在一起，如下所示：

::: {#cb162 .sourceCode}

```c
//  original name
//            |
//            v
//      |-----------|
typedef struct animal {
    char *name;
    int leg_count, speed;
} animal;                         // <-- new name

struct animal y;  // This works
animal z;         // This also works because "animal" is an alias
```

:::

That's exactly the same as the previous example, just more concise.

But that's not all! There's another common shortcut that you might see in code using what are called _anonymous structures_[^81^]. It turns out you don't actually need to name the structure in a variety of places, and with `typedef` is one of them.

> 但这还不是全部！还有另一个常见的快捷方式，你可能会在使用所谓的_匿名结构_[^81^]中看到代码。事实证明，您实际上不需要在各种地方命名结构，而 `typedef` 就是其中之一。

Let's do the same example with an anonymous structure:

::: {#cb163 .sourceCode}

```c
//  Anonymous struct! It has no name!
//         |
//         v
//      |----|
typedef struct {
    char *name;
    int leg_count, speed;
} animal;                         // <-- new name

//struct animal y;  // ERROR: this no longer works--no such struct!
animal z;           // This works because "animal" is an alias
```

:::

As another example, we might find something like this:

::: {#cb164 .sourceCode}

```c
typedef struct {
    int x, y;
} point;

point p = {.x=20, .y=40};

printf("%d, %d\n", p.x, p.y);  // 20, 40
```

:::

### [10.2.2] `typedef` and Other Types {#typedef-and-other-types number="10.2.2"}

It's not that using `typedef` with a simple type like `int` is completely useless... it helps you abstract the types to make it easier to change them later.

> 使用 `typedef` 和简单类型如 `int` 并不完全没有用，它可以帮助抽象类型，以便以后更容易更改它们。

For example, if you have `float` all over your code in 100 zillion places, it's going to be painful to change them all to `double` if you find you have to do that later for some reason.

> 例如，如果你的代码中有 1000 万处都使用 `float`，如果以后出于某种原因你发现需要把它们都改成 `double`，那将会是一件痛苦的事情。

But if you prepared a little with:

::: {#cb165 .sourceCode}

```c
typedef float app_float;

// and

app_float f1, f2, f3;
```

:::

Then if later you want to change to another type, like `long double`, you just need to change the `typedef`:

> 然后，如果你想改变类型，比如 `long double`，你只需要改变 `typedef`：

::: {#cb166 .sourceCode}

```c
//        voila!
//      |---------|
typedef long double app_float;

// and no need to change this line:

app_float f1, f2, f3;  // Now these are all long doubles
```

:::

### [10.2.3] `typedef` and Pointers {#typedef-and-pointers number="10.2.3"}

You can make a type that is a pointer.

::: {#cb167 .sourceCode}

```c
typedef int *intptr;

int a = 10;
intptr x = &a;  // "intptr" is type "int*"
```

:::

I really don't like this practice. It hides the fact that `x` is a pointer type because you don't see a `*` in the declaration.

> 我真的不喜欢这种做法。它掩盖了 `x` 是指针类型的事实，因为在声明中你看不到 `*`。

IMHO, it's better to explicitly show that you're declaring a pointer type so that other devs can clearly see it and don't mistake `x` for having a non-pointer type.

> 我的个人看法，最好明确表明你声明的是一个指针类型，这样其他开发人员就可以清楚地看到它，而不会误以为 `x` 具有非指针类型。

But at last count, say, 832,007 people had a different opinion.

### [10.2.4] `typedef` and Capitalization {#typedef-and-capitalization number="10.2.4"}

I've seen all kinds of capitalization on `typedef`.

::: {#cb168 .sourceCode}

```c
typedef struct {
    int x, y;
} my_point;          // lower snake case

typedef struct {
    int x, y;
} MyPoint;          // CamelCase

typedef struct {
    int x, y;
} Mypoint;          // Leading uppercase

typedef struct {
    int x, y;
} MY_POINT;          // UPPER SNAKE CASE
```

:::

The C11 specification doesn't dictate one way or another, and shows examples in all uppercase and all lowercase.

> C11 规范没有明确规定，并且以全大写和全小写的形式给出了示例。

K&R2 uses leading uppercase predominantly, but show some examples in uppercase and snake case (with `_t`).

> K&R2 主要使用大写字母，但也有一些以大写字母和蛇形(带有 `_t`)的示例。

If you have a style guide in use, stick with it. If you don't, grab one and stick with it.

> 如果你有一个风格指南在使用，坚持使用它。如果没有，抓一个并坚持使用它。

## [10.3] Arrays and `typedef` {#arrays-and-typedef number="10.3"}

The syntax is a little weird, and this is rarely seen in my experience, but you can `typedef` an array of some number of items.

> 语法有点奇怪，我的经验中很少见到，但是你可以使用 `typedef` 定义一个数量可变的数组。

::: {#cb169 .sourceCode}

```c
// Make type five_ints an array of 5 ints
typedef int five_ints[5];

five_ints x = {11, 22, 33, 44, 55};
```

:::

I don't like it because it hides the array nature of the variable, but it's possible to do.

> 我不喜欢它，因为它隐藏了变量的数组本质，但还是可以做到的。

# [11] Pointers II: Arithmetic {#pointers2 number="11"}

Time to get more into it with a number of new pointer topics! If you're not up to speed with pointers, [check out the first section in the guide on the matter](#pointers).

> 是时候深入学习一些新的指针主题了！如果你对指针还不太熟悉，[请查看本指南中关于指针的第一部分](#pointers)。

## [11.1] Pointer Arithmetic {#pointer-arithmetic number="11.1"}

Turns out you can do math on pointers, notably addition and subtraction.

But what does it mean when you do that?

In short, if you have a pointer to a type, adding one to the pointer moves to the next item of that type directly after it in memory.

> 如果你有一个指向某种类型的指针，在内存中将其加一，可以直接移动到该类型的下一个项目。

It's **important** to remember that as we move pointers around and look at different places in memory, we need to make sure that we're always pointing to a valid place in memory before we dereference. If we're off in the weeds and we try to see what's there, the behavior is undefined and a crash is a common result.

> 记住，当我们移动指针并查看内存中的不同位置时，我们需要确保在解引用之前总是指向内存中的有效位置。如果我们走入歧途，试图看看那里有什么，行为是不确定的，崩溃是常见的结果。

This is a little chicken-and-eggy with [Array/Pointer Equivalence, below](#arraypointerequiv), but we're going to give it a shot, anyway.

> 这是一个有关数组/指针等价性的小鸡蛋，尽管如此，我们还是要尝试一下。

### [11.1.1] Adding to Pointers {#adding-to-pointers number="11.1.1"}

First, let's take an array of numbers.

::: {#cb170 .sourceCode}

```c
int a[5] = {11, 22, 33, 44, 55};
```

:::

Then let's get a pointer to the first element in that array:

::: {#cb171 .sourceCode}

```c
int a[5] = {11, 22, 33, 44, 55};

int *p = &a[0];  // Or "int *p = a;" works just as well
```

:::

Then let's print the value there by dereferencing the pointer:

::: {#cb172 .sourceCode}

```c
printf("%d\n", *p);  // Prints 11
```

:::

Now let's use pointer arithmetic to print the next element in the array, the one at index 1:

> 现在让我们使用指针算术来打印数组中的下一个元素，即索引为 1 的元素：

::: {#cb173 .sourceCode}

```c
printf("%d\n", *(p + 1));  // Prints 22!!
```

:::

What happened there? C knows that `p` is a pointer to an `int`. So it knows the `sizeof` an `int`[^82^] and it knows to skip that many bytes to get to the next `int` after the first one!

> 那里发生了什么？C 知道 `p` 是一个指向 `int` 的指针。因此它知道 `int` 的 `sizeof`[^82^]，它知道跳过多少字节才能获得第一个 `int` 之后的下一个 `int`！

In fact, the prior example could be written these two equivalent ways:

::: {#cb174 .sourceCode}

```c
printf("%d\n", *p);        // Prints 11
printf("%d\n", *(p + 0));  // Prints 11
```

:::

because adding `0` to a pointer results in the same pointer.

Let's think of the upshot here. We can iterate over elements of an array this way instead of using an array:

> 让我们来思考一下结果。我们可以用这种方式遍历数组的元素，而不是使用数组。

::: {#cb175 .sourceCode}

```c
int a[5] = {11, 22, 33, 44, 55};

int *p = &a[0];  // Or "int *p = a;" works just as well

for (int i = 0; i < 5; i++) {
    printf("%d\n", *(p + i));  // Same as p[i]!
}
```

:::

And that works the same as if we used array notation! Oooo! Getting closer to that array/pointer equivalence thing! More on this later in this chapter.

> 而这和我们使用数组表示法的效果是一样的！哦！我们越来越接近数组/指针的等价性了！本章后面会有更多内容。

But what's actually happening, here? How does it work?

Remember from early on that memory is like a big array, where a byte is stored at each array index?

> 记得从一开始记忆就像一个大阵列，每个阵列索引都会储存一个位元组吗？

And the array index into memory has a few names:

- Index into memory
- Location
- Address
- _Pointer!_

So a point is an index into memory, somewhere.

For a random example, say that a number 3490 was stored at address ("index") 23,237,489,202. If we have an `int` pointer to that 3490, that value of that pointer is 23,237,489,202... because the pointer is the memory address. Different words for the same thing.

> 例如，在地址(“索引”)23,237,489,202 存储了一个数字 3490。如果我们有一个指向 3490 的 `int` 指针，那么该指针的值就是 23,237,489,202...因为指针是内存地址。同一件事用不同的词语表达。

And now let's say we have another number, 4096, stored right after the 3490 at address 23,237,489,210 (8 higher than the 3490 because each `int` in this example is 8 bytes long).

> 现在让我们来说，我们在地址 23,237,489,210(比 3490 高 8 个字节，因为在这个例子中每个 `int` 是 8 个字节长)之后存储了另一个数字 4096。

If we add `1` to that pointer, it actually jumps ahead `sizeof(int)` bytes to the next `int`. It knows to jump that far ahead because it's an `int` pointer. If it were a `float` pointer, it'd jump `sizeof(float)` bytes ahead to get to the next float!

> 如果我们给这个指针加上 1，它实际上会跳过 sizeof(int)字节到下一个 int。它知道跳得那么远是因为它是一个 int 指针。如果它是一个 float 指针，它会跳过 sizeof(float)字节到下一个 float！

So you can look at the next `int`, by adding `1` to the pointer, the one after that by adding `2` to the pointer, and so on.

> 你可以通过给指针加 1 来查看下一个 `int`，给指针加 2 来查看其后的 `int`，以此类推。

### [11.1.2] Changing Pointers {#changing-pointers number="11.1.2"}

We saw how we could add an integer to a pointer in the previous section. This time, let's _modify the pointer, itself_.

> 在上一节中，我们看到了如何将整数添加到指针。这次，让我们修改指针本身。

You can just add (or subtract) integer values directly to (or from) any pointer!

> 你可以直接向任何指针添加(或减去)整数值！

Let's do that example again, except with a couple changes. First, I'm going to add a `999` to the end of our numbers to act as a sentinel value. This will let us know where the end of the data is.

> 让我们再做一次这个例子，但有几处改变。首先，我要在我们的数字末尾添加一个 `999` 作为哨兵值。这将让我们知道数据的结束位置。

::: {#cb176 .sourceCode}

```c
int a[] = {11, 22, 33, 44, 55, 999};  // Add 999 here as a sentinel

int *p = &a[0];  // p points to the 11
```

:::

And we also have `p` pointing to the element at index `0` of `a`, namely `11`, just like before.

> 我们还有一个 `p` 指向 `a` 中索引为 `0` 的元素，也就是 `11`，就像之前一样。

Now---let's start _incrementing_ `p` so that it points at subsequent elements of the array. We'll do this until `p` points to the `999`; that is, we'll do it until `*p == 999`:

> 现在，让我们开始递增 `p`，以便它指向数组的后续元素。 我们将这样做，直到 `p` 指向 `999`; 也就是说，我们将这样做，直到 `*p == 999`：

::: {#cb177 .sourceCode}

```c
while (*p != 999) {       // While the thing p points to isn't 999
    printf("%d\n", *p);   // Print it
    p++;                  // Move p to point to the next int!
}
```

:::

Pretty crazy, right?

When we give it a run, first `p` points to `11`. Then we increment `p`, and it points to `22`, and then again, it points to `33`. And so on, until it points to `999` and we quit.

> 当我们运行它时，首先 `p` 指向 `11`。然后我们增加 `p`，它指向 `22`，然后再次指向 `33`。等等，直到它指向 `999`，然后我们退出。

### [11.1.3] Subtracting Pointers {#subtracting-pointers number="11.1.3"}

You can subtract a value from a pointer to get to earlier address, as well, just like we were adding to them before.

> 你也可以从指针中减去一个值来访问更早的地址，就像我们之前对它们进行加法操作一样。

But we can also subtract two pointers to find the difference between them, e.g. we can calculate how many `int` s there are between two `int*` s. The catch is that this only works within a single array[^83^]---if the pointers point to anything else, you get undefined behavior.

> 但我们也可以通过减去两个指针来找出它们之间的差异，例如，我们可以计算两个 `int*` 之间有多少个 `int`。关键是，这只适用于单个数组[^83^]---如果指针指向其他任何内容，则会出现未定义的行为。

Remember how strings are `char*` s in C? Let's see if we can use this to write another variant of `strlen()` to compute the length of a string that utilizes pointer subtraction.

> 记得在 C 语言中字串是 `char*` 吗？让我们来看看我们是否可以使用这个来写另一个版本的 `strlen()` 来计算字串的长度，并使用指标相减法。

The idea is that if we have a pointer to the beginning of the string, we can find a pointer to the end of the string by scanning ahead for the `NUL` character.

> 如果我们有一个指向字符串开头的指针，我们可以通过扫描 `NUL` 字符来找到指向字符串结尾的指针。

And if we have a pointer to the beginning of the string, and we computed the pointer to the end of the string, we can just subtract the two pointers to come up with the length!

> 如果我们有一个指向字符串开头的指针，并且我们计算出指向字符串结尾的指针，我们可以通过相减两个指针来获得长度！

::: {#cb178 .sourceCode}

```c
#include <stdio.h>

int my_strlen(char *s)
{
    // Start scanning from the beginning of the string
    char *p = s;

    // Scan until we find the NUL character
    while (*p != '\0')
        p++;

    // Return the difference in pointers
    return p - s;
}

int main(void)
{
    printf("%d\n", my_strlen("Hello, world!"));  // Prints "13"
}
```

:::

Remember that you can only use pointer subtraction between two pointers that point to the same array!

> 记住，只有在指向同一个数组的两个指针之间才能使用指针减法！

## [11.2] Array/Pointer Equivalence {#arraypointerequiv number="11.2"}

We're finally ready to talk about this! We've seen plenty of examples of places where we've intermixed array notation, but let's give out the _fundamental formula of array/pointer equivalence_:

> 我们终于准备好谈论这个了！我们已经看到了很多混合数组符号的例子，但让我们给出数组/指针等价的基本公式：

::: {#cb179 .sourceCode}

```c
a[b] == *(a + b)
```

:::

Study that! Those are equivalent and can be used interchangeably!

I've oversimplified a bit, because in my above example `a` and `b` can both be expressions, and we might want a few more parentheses to force order of operations in case the expressions are complex.

> 我有点过于简化了，因为在我上面的例子中，`a` 和 `b` 都可以是表达式，如果表达式很复杂，我们可能需要更多的括号来强制操作顺序。

The spec is specific, as always, declaring (in C11 §6.5.2.1¶2):

> `E1[E2]` is identical to `(*((E1)+(E2)))`

but that's a little harder to grok. Just make sure you include parentheses if the expressions are complicated so all your math happens in the right order.

> 但这更难理解。如果表达式很复杂，一定要加上括号，这样才能确保数学运算按正确的顺序进行。

This means we can _decide_ if we're going to use array or pointer notation for any array or pointer (assuming it points to an element of an array).

> 这意味着我们可以决定是否使用数组或指针表示法来表示任何数组或指针(假设它指向数组的一个元素)。

Let's use an array and pointer with both array and pointer notation:

::: {#cb180 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int a[] = {11, 22, 33, 44, 55};

    int *p = a;  // p points to the first element of a, 11

    // Print all elements of the array a variety of ways:

    for (int i = 0; i < 5; i++)
        printf("%d\n", a[i]);      // Array notation with a

    for (int i = 0; i < 5; i++)
        printf("%d\n", p[i]);      // Array notation with p

    for (int i = 0; i < 5; i++)
        printf("%d\n", *(a + i));  // Pointer notation with a

    for (int i = 0; i < 5; i++)
        printf("%d\n", *(p + i));  // Pointer notation with p

    for (int i = 0; i < 5; i++)
        printf("%d\n", *(p++));    // Moving pointer p
        //printf("%d\n", *(a++));    // Moving array variable a--ERROR!
}
```

:::

So you can see that in general, if you have an array variable, you can use pointer or array notion to access elements. Same with a pointer variable.

> 你可以看到，一般来说，如果你有一个数组变量，你可以使用指针或数组概念来访问元素。同样适用于指针变量。

The one big difference is that you can _modify_ a pointer to point to a different address, but you can't do that with an array variable.

> 一个很大的不同是，你可以修改指针指向不同的地址，但是你不能这样做数组变量。

### [11.2.1] Array/Pointer Equivalence in Function Calls {#arraypointer-equivalence-in-function-calls number="11.2.1"}

This is where you'll encounter this concept the most, for sure.

If you have a function that takes a pointer argument, e.g.:

::: {#cb181 .sourceCode}

```c
int my_strlen(char *s)
```

:::

this means you can pass either an array or a pointer to this function and have it work!

> 这意味着你可以传入一个数组或指针给这个函数，它都能正常工作！

::: {#cb182 .sourceCode}

```c
char s[] = "Antelopes";
char *t = "Wombats";

printf("%d\n", my_strlen(s));  // Works!
printf("%d\n", my_strlen(t));  // Works, too!
```

:::

And it's also why these two function signatures are equivalent:

::: {#cb183 .sourceCode}

```c
int my_strlen(char *s)    // Works!
int my_strlen(char s[])   // Works, too!
```

:::

## [11.3] `void` Pointers {#void-pointers number="11.3"}

You've already seen the `void` keyword used with functions, but this is an entirely separate, unrelated animal.

> 你已经看到过 `void` 关键字与函数一起使用，但这是一种完全不同的动物。

Sometimes it's useful to have a pointer to a thing _that you don't know the type of_.

> 有时候指向一个你不知道类型的东西是有用的。

I know. Bear with me just a second.

There are basically two use cases for this.

1\. A function is going to operate on something byte-by-byte. For example, `memcpy()` copies bytes of memory from one pointer to another, but those pointers can point to any type. `memcpy()` takes advantage of the fact that if you iterate through `char*` s, you're iterating through the bytes of an object no matter what type the object is. More on this in the [Multibyte Values](#multibyte-values) subsection.

> 1. 一个函数将以字节为单位对某事进行操作。例如，`memcpy()` 从一个指针复制内存的字节到另一个指针，但这些指针可以指向任何类型。`memcpy()` 利用了这样一个事实：如果你遍历 `char*`，你就在遍历一个对象的字节，无论这个对象是什么类型。有关此内容的更多信息，请参阅[多字节值](#multibyte-values)子节。

2. Another function is calling a function you passed to it (a callback), and it's passing you data. You know the type of the data, but the function calling you doesn't. So it passes you `void*` s---'cause it doesn't know the type---and you convert those to the type you need. The built-in [`qsort()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-qsort)[^84^] and [`bsearch()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-bsearch)[^85^] use this technique.

> 另一个功能是调用传递给它的函数(回调函数)，并传递给你数据。你知道数据的类型，但调用你的函数不知道。因此，它传递给你 `void*`，因为它不知道类型，你将这些转换为你需要的类型。内置的[`qsort()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-qsort)[^84^]和[`bsearch()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-bsearch)[^85^]使用了这种技术。

Let's look at an example, the built-in `memcpy()` function:

::: {#cb184 .sourceCode}

```c
void *memcpy(void *s1, void *s2, size_t n);
```

:::

This function copies `n` bytes of memory starting from address `s1` into the memory starting at address `s2`.

> 这个函数从地址 s1 开始复制 n 个字节的内存到地址 s2 开始的内存中。

But look! `s1` and `s2` are `void*` s! Why? What does it mean? Let's run more examples to see.

> 哎呀！s1 和 s2 都是 void*s！这是怎么回事？为什么？让我们运行更多的例子来看看吧。

For instance, we could copy a string with `memcpy()` (though `strcpy()` is more appropriate for strings):

> 例如，我们可以使用 `memcpy()` 复制一个字符串(尽管 `strcpy()` 更适合字符串)：

::: {#cb185 .sourceCode}

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    char s[] = "Goats!";
    char t[100];

    memcpy(t, s, 7);  // Copy 7 bytes--including the NUL terminator!

    printf("%s\n", t);  // "Goats!"
}
```

:::

Or we can copy some `int` s:

::: {#cb186 .sourceCode}

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
    int a[] = {11, 22, 33};
    int b[3];

    memcpy(b, a, 3 * sizeof(int));  // Copy 3 ints of data

    printf("%d\n", b[1]);  // 22
}
```

:::

That one's a little wild---you see what we did there with `memcpy()`? We copied the data from `a` to `b`, but we had to specify how many _bytes_ to copy, and an `int` is more than one byte.

> 那个有点疯狂---你看到我们在 `memcpy()` 里做了什么吗？我们从 `a` 复制到 `b`，但是我们必须指定复制多少_字节_，而一个 `int` 可以是一个字节以上。

OK, then---how many bytes does an `int` take? Answer: depends on the system. But we can tell how many bytes any type takes with the `sizeof` operator.

> 好的，那么---`int` 需要多少字节？答案：取决于系统。但是我们可以使用 `sizeof` 运算符来确定任何类型需要多少字节。

So there's the answer: an `int` takes `sizeof(int)` bytes of memory to store.

> 答案是：一个 `int` 需要 `sizeof(int)` 个字节的内存来存储。

And if we have 3 of them in our array, like we did in that example, the entire space used for the 3 `int` s must be `3 * sizeof(int)`.

> 如果我们在数组中有 3 个，就像我们在那个例子中所做的那样，用于这 3 个 int 的整个空间必须是 3 乘以 int 的大小。

(In the string example, earlier, it would have been more technically accurate to copy `7 * sizeof(char)` bytes. But `char` s are always one byte large, by definition, so that just devolves into `7 * 1`.)

> 在之前的字符串示例中，复制 `7 * sizeof(char)` 字节更加技术上准确。但是按照定义，`char` 总是一个字节大小，因此这只会降低到 `7 * 1`。

We could even copy a `float` or a `struct` with `memcpy()`! (Though this is abusive---we should just use `=` for that):

> 我们甚至可以用 `memcpy()` 复制一个 `float` 或 `struct`！(虽然这是不当的---我们应该只使用 `=`)

::: {#cb187 .sourceCode}

```c
struct antelope my_antelope;
struct antelopy my_clone_antelope;

// ...

memcpy(&my_clone_antelope, &my_antelope, sizeof my_antelope);
```

:::

Look at how versatile `memcpy()` is! If you have a pointer to a source and a pointer to a destination, and you have the number of bytes you want to copy, you can copy _any type of data_.

> 看看 `memcpy()` 有多灵活！如果你有一个指向源的指针和一个指向目标的指针，并且你有要复制的字节数，你可以复制任何类型的数据。

Imagine if we didn't have `void*`. We'd have to write specialized `memcpy()` functions for each type:

> 如果我们没有 `void*`，我们就必须为每种类型编写专门的 `memcpy()` 函数。

::: {#cb188 .sourceCode}

```c
memcpy_int(int *a, int *b, int count);
memcpy_float(float *a, float *b, int count);
memcpy_double(double *a, double *b, int count);
memcpy_char(char *a, char *b, int count);
memcpy_unsigned_char(unsigned char *a, unsigned char *b, int count);

// etc... blech!
```

:::

Much better to just use `void*` and have one function that can do it all.

That's the power of `void*`. You can write functions that don't care about the type and is still able to do things with it.

> 那就是 `void*` 的力量。你可以编写不关心类型的函数，仍然可以用它做一些事情。

But with great power comes great responsibility. Maybe not _that_ great in this case, but there are some limits.

> 随着强大的力量，也有着巨大的责任。也许在这种情况下不是那么巨大，但仍然有一些限制。

1\. You cannot do pointer arithmetic on a `void*`. 2. You cannot dereference a `void*`. 3. You cannot use the arrow operator on a `void*`, since it's also a dereference. 4. You cannot use array notation on a `void*`, since it's also a dereference, as well[^86^].

> 1. 你不能在 `void*` 上进行指针算术。2. 你不能对 `void*` 进行解引用。3. 你不能在 `void*` 上使用箭头操作符，因为它也是一个解引用。4. 你不能在 `void*` 上使用数组符号，因为它也是一个解引用。

And if you think about it, these rules make sense. All those operations rely on knowing the `sizeof` the type of data pointed to, and with `void*`, we don't know the size of the data being pointed to---it could be anything!

> 如果你仔细想想，这些规则是有意义的。所有这些操作都依赖于知道指向的数据类型的 `sizeof`，而 `void*`，我们不知道指向的数据的大小——它可以是任何东西！

But wait---if you can't dereference a `void*` what good can it ever do you?

> 但是等等---如果你不能解除 `void*` 的引用，它对你有什么好处？

Like with `memcpy()`, it helps you write generic functions that can handle multiple types of data. But the secret is that, deep down, _you convert the `void_` to another type before you use it\*!

> 就像使用 `memcpy()` 一样，它可以帮助您编写可以处理多种类型数据的通用函数。但秘诀是，在使用之前，您要将 `void` 转换为另一种类型！

And conversion is easy: you can just assign into a variable of the desired type[^87^].

> 转换很容易：您只需将其分配到所需类型的变量中[^87^]。

::: {#cb189 .sourceCode}

```c
char a = 'X';  // A single char

void *p = &a;  // p points to the 'X'
char *q = p;   // q also points to the 'X'

printf("%c\n", *p);  // ERROR--cannot dereference void*!
printf("%c\n", *q);  // Prints "X"
```

:::

Let's write our own `memcpy()` to try this out. We can copy bytes (`char` s), and we know the number of bytes because it's passed in.

> 让我们编写自己的 `memcpy()` 来试试。我们可以复制字节(`char` s)，并且我们知道字节的数量，因为它是传入的。

::: {#cb190 .sourceCode}

```c
void *my_memcpy(void *dest, void *src, int byte_count)
{
    // Convert void*s to char*s
    char *s = src, *d = dest;

    // Now that we have char*s, we can dereference and copy them
    while (byte_count--) {
        *d++ = *s++;
    }

    // Most of these functions return the destination, just in case
    // that's useful to the caller.
    return dest;
}
```

:::

Right there at the beginning, we copy the `void*` s into `char*` s so that we can use them as `char*` s. It's as easy as that.

> 在一开始，我们就把 `void*` 复制到 `char*` 中，这样我们就可以把它们当作 `char*` 来使用。就是这么简单。

Then some fun in a while loop, where we decrement `byte_count` until it becomes false (`0`). Remember that with post-decrement, the value of the expression is computed (for `while` to use) and _then_ the variable is decremented.

> 然后在一个 while 循环中玩一些乐趣，我们会逐渐减少 byte_count 直到它变成假(0)。记住，使用后置减法，表达式的值会被计算(供 while 使用)，然后变量才会被减少。

And some fun in the copy, where we assign `*d = *s` to copy the byte, but we do it with post-increment so that both `d` and `s` move to the next byte after the assignment is made.

> 将*d = *s 用于复制字节时，我们在复制中加入一些乐趣，我们使用后置增量来完成，这样 d 和 s 在赋值后都会移动到下一个字节。

Lastly, most memory and string functions return a copy of a pointer to the destination string just in case the caller wants to use it.

> 最后，大多数内存和字符串函数会返回一个指向目标字符串的指针的副本，以防调用者需要使用它。

Now that we've done that, I just want to quickly point out that we can use this technique to iterate over the bytes of _any_ object in C, `float` s, `struct` s, or anything!

> 现在我们已经完成了这个，我只想快速指出，我们可以使用这种技术来遍历 C 中任何对象的字节，float，struct 或任何东西！

[Let's]{#qsort-example} run one more real-world example with the built-in `qsort()` routine that can sort _anything_ thanks to the magic of `void*` s.

> 让我们再运行一个使用内置的 `qsort()` 例程的实际例子，它可以由于 `void*` 的魔力而对任何东西进行排序。

(In the following example, you can ignore the word `const`, which we haven't covered yet.)

> 在下面的例子中，您可以忽略我们尚未涵盖的 `const` 这个词。

::: {#cb191 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

// The type of structure we're going to sort
struct animal {
    char *name;
    int leg_count;
};

// This is a comparison function called by qsort() to help it determine
// what exactly to sort by. We'll use it to sort an array of struct
// animals by leg_count.
int compar(const void *elem1, const void *elem2)
{
    // We know we're sorting struct animals, so let's make both
    // arguments pointers to struct animals
    const struct animal *animal1 = elem1;
    const struct animal *animal2 = elem2;

    // Return <0 =0 or >0 depending on whatever we want to sort by.

    // Let's sort ascending by leg_count, so we'll return the difference
    // in the leg_counts
    if (animal1->leg_count > animal2->leg_count)
        return 1;

    if (animal1->leg_count < animal2->leg_count)
        return -1;

    return 0;
}

int main(void)
{
    // Let's build an array of 4 struct animals with different
    // characteristics. This array is out of order by leg_count, but
    // we'll sort it in a second.
    struct animal a[4] = {
        {.name="Dog", .leg_count=4},
        {.name="Monkey", .leg_count=2},
        {.name="Antelope", .leg_count=4},
        {.name="Snake", .leg_count=0}
    };

    // Call qsort() to sort the array. qsort() needs to be told exactly
    // what to sort this data by, and we'll do that inside the compar()
    // function.
    //
    // This call is saying: qsort array a, which has 4 elements, and
    // each element is sizeof(struct animal) bytes big, and this is the
    // function that will compare any two elements.
    qsort(a, 4, sizeof(struct animal), compar);

    // Print them all out
    for (int i = 0; i < 4; i++) {
        printf("%d: %s\n", a[i].leg_count, a[i].name);
    }
}
```

:::

As long as you give `qsort()` a function that can compare two items that you have in your array to be sorted, it can sort anything. And it does this without needing to have the types of the items hardcoded in there anywhere. `qsort()` just rearranges blocks of bytes based on the results of the `compar()` function you passed in.

> 只要给 `qsort()` 函数提供一个可以比较要排序的数组中的两个项目的函数，它就可以排序任何东西。它不需要在任何地方将项目的类型硬编码。 `qsort()` 只是根据传入的 `compar()` 函数的结果重新排列字节块。

# [12] Manual Memory Allocation {#manual-memory-allocation number="12"}

This is one of the big areas where C likely diverges from languages you already know: _manual memory management_.

> 这是 C 与你已知的语言可能有差异的一个重要领域：手动内存管理。

Other languages uses reference counting, garbage collection, or other means to determine when to allocate new memory for some data---and when to deallocate it when no variables refer to it.

> 其他语言使用引用计数、垃圾回收或其他方式来确定何时为某些数据分配新的内存，以及当没有变量引用它时何时释放它。

And that's nice. It's nice to be able to not worry about it, to just drop all the references to an item and trust that at some point the memory associated with it will be freed.

> 那很好。能够不用担心它，只需要放弃所有对该项目的引用，相信某个时刻相关的内存会被释放，这很好。

But C's not like that, entirely.

Of course, in C, some variables are automatically allocated and deallocated when they come into scope and leave scope. We call these automatic variables. They're your average run-of-the-mill block scope "local" variables. No problem.

> 在 C 语言中，有些变量会在它们进入作用域和离开作用域时自动分配和释放。我们称这些变量为自动变量。它们是普通的块作用域“局部”变量，没有问题。

But what if you want something to persist longer than a particular block? This is where manual memory management comes into play.

> 但是如果你想让某些东西比特定的块持久性更长，怎么办？这就是手动内存管理发挥作用的地方。

You can tell C explicitly to allocate for you a certain number of bytes that you can use as you please. And these bytes will remain allocated until you explicitly free that memory[^88^].

> 你可以明确地告诉 C 为你分配一定数量的字节，你可以随意使用这些字节。这些字节将一直保持分配状态，直到你明确释放该内存。

It's important to free the memory you're done with! If you don't, we call that a _memory leak_ and your process will continue to reserve that memory until it exits.

> 释放你完成使用的内存很重要！如果不这样做，我们称之为内存泄漏，你的进程将一直保留这部分内存直到退出。

_If you manually allocated it, you have to manually free it when you're done with it._

> 如果你手动分配它，当你完成时，你必须手动释放它。

So how do we do this? We're going to learn a couple new functions, and make use of the `sizeof` operator to help us learn how many bytes to allocate.

> 那么我们怎么做呢？我们要学习一些新的函数，并利用 `sizeof` 操作符来帮助我们了解要分配多少字节。

In common C parlance, devs say that automatic local variables are allocated "on the stack", and manually-allocated memory is "on the heap". The spec doesn't talk about either of those things, but all C devs will know what you're talking about if you bring them up.

> 在通常的 C 语言中，开发人员会说自动本地变量分配在"堆栈"上，而手动分配的内存则是"堆"上的。规范没有提及这些事情，但如果你提起它们，所有的 C 开发人员都会知道你在说什么。

All functions we're going to learn in this chapter can be found in `<stdlib.h>`.

> 所有我们将在本章中学习的函数都可以在 <stdlib.h> 中找到。

## [12.1] Allocating and Deallocating, `malloc()` and `free()` {#allocating-and-deallocating-malloc-and-free number="12.1"}

The `malloc()` function accepts a number of bytes to allocate, and returns a void pointer to that block of newly-allocated memory.

> `malloc()` 函数接受要分配的字节数，并返回一个指向新分配的内存块的 void 指针。

Since it's a `void*`, you can assign it into whatever pointer type you want... normally this will correspond in some way to the number of bytes you're allocating.

> 由于它是一个 `void*`，你可以把它赋值给任何指针类型...通常这将与你分配的字节数有一定的关联。

So... how many bytes should I allocate? We can use `sizeof` to help with that. If we want to allocate enough room for a single `int`, we can use `sizeof(int)` and pass that to `malloc()`.

> 那么...我应该分配多少字节？我们可以使用 `sizeof` 来帮助。如果我们想为单个 `int` 分配足够的空间，我们可以使用 `sizeof(int)` 并将其传递给 `malloc()`。

After we're done with some allocated memory, we can call `free()` to indicate we're done with that memory and it can be used for something else. As an argument, you pass the same pointer you got from `malloc()` (or a copy of it). It's undefined behavior to use a memory region after you `free()` it.

> 当我们完成分配的内存后，我们可以调用 `free()` 来表明我们已经完成了该内存，它可以用于其他用途。作为参数，您传递与 `malloc()` 相同的指针(或其副本)。在 `free()` 之后使用内存区域是未定义的行为。

Let's try. We'll allocate enough memory for an `int`, and then store something there, and the print it.

> 让我们试试吧。我们将为一个 `int` 分配足够的内存，然后将其存储起来，然后打印出来。

::: {#cb192 .sourceCode}

```c
// Allocate space for a single int (sizeof(int) bytes-worth):

int *p = malloc(sizeof(int));

*p = 12;  // Store something there

printf("%d\n", *p);  // Print it: 12

free(p);  // All done with that memory

//*p = 3490;  // ERROR: undefined behavior! Use after free()!
```

:::

Now, in that contrived example, there's really no benefit to it. We could have just used an automatic `int` and it would have worked. But we'll see how the ability to allocate memory this way has its advantages, especially with more complex data structures.

> 现在，在这个编造的例子中，它真的没有任何好处。我们可以使用自动 `int`，它也可以工作。但是我们将看到这种分配内存的能力有其优势，特别是对于更复杂的数据结构。

One more thing you'll commonly see takes advantage of the fact that `sizeof` can give you the size of the result type of any constant expression. So you could put a variable name in there, too, and use that. Here's an example of that, just like the previous one:

> 你经常会看到的另一件事是利用 `sizeof` 可以给出任何常量表达式的结果类型的大小的事实。因此，您也可以在其中放置一个变量名，并使用它。这里有一个类似于前一个的示例：

::: {#cb193 .sourceCode}

```c
int *p = malloc(sizeof *p);  // *p is an int, so same as sizeof(int)
```

:::

## [12.2] Error Checking {#error-checking number="12.2"}

All the allocation functions return a pointer to the newly-allocated stretch of memory, or `NULL` if the memory cannot be allocated for some reason.

> 所有的分配函数都会返回一个指向新分配的内存块的指针，如果因为某种原因无法分配内存，则返回 `NULL`。

Some OSes like Linux can be configured in such a way that `malloc()` never returns `NULL`, even if you're out of memory. But despite this, you should always code it up with protections in mind.

> 一些操作系统，如 Linux，可以进行配置，使 `malloc()` 即使内存耗尽也不会返回 `NULL`。但是，尽管如此，你仍然应该考虑保护性编码。

::: {#cb194 .sourceCode}

```c
int *x;

x = malloc(sizeof(int) * 10);

if (x == NULL) {
    printf("Error allocating 10 ints\n");
    // do something here to handle it
}
```

:::

Here's a common pattern that you'll see, where we do the assignment and the condition on the same line:

> 这里有一个你经常会看到的模式，我们在同一行上进行赋值和条件：

::: {#cb195 .sourceCode}

```c
int *x;

if ((x = malloc(sizeof(int) * 10)) == NULL)
    printf("Error allocating 10 ints\n");
    // do something here to handle it
}
```

:::

## [12.3] Allocating Space for an Array {#allocating-space-for-an-array number="12.3"}

We've seen how to allocate space for a single thing; now what about for a bunch of them in an array?

> 我们已经看到如何为单个物体分配空间；现在在数组中分配一堆物体怎么办？

In C, an array is a bunch of the same thing back-to-back in a contiguous stretch of memory.

> 在 C 语言中，数组是连续存储在内存中的一组相同的东西。

We can allocate a contiguous stretch of memory---we've seen how to do that. If we wanted 3490 bytes of memory, we could just ask for it:

> 我们可以分配连续的内存段---我们已经看到了如何做到这一点。如果我们想要 3490 字节的内存，我们可以只是简单地要求它：

::: {#cb196 .sourceCode}

```c
char *p = malloc(3490);  // Voila
```

:::

And---indeed!---that's an array of 3490 `char` s (AKA a string!) since each `char` is 1 byte. In other words, `sizeof(char)` is `1`.

> 而且，没错！那是一个 3490 个字符(也就是字符串！)的数组，因为每个字符是 1 个字节。换句话说，sizeof(char)是 1。

Note: there's no initialization done on the newly-allocated memory---it's full of garbage. Clear it with `memset()` if you want to, or see `calloc()`, below.

> 注意：新分配的内存没有进行初始化---它充满了垃圾数据。如果想要清除它，可以使用 `memset()`，或者参考下面的 `calloc()`。

But we can just multiply the size of the thing we want by the number of elements we want, and then access them using either pointer or array notation. Example!

> 我们可以通过指针或数组符号来乘以我们想要的东西的大小，然后访问它们。例子！

::: {#cb197 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // Allocate space for 10 ints
    int *p = malloc(sizeof(int) * 10);

    // Assign them values 0-45:
    for (int i = 0; i < 10; i++)
        p[i] = i * 5;

    // Print all values 0, 5, 10, 15, ..., 40, 45
    for (int i = 0; i < 10; i++)
        printf("%d\n", p[i]);

    // Free the space
    free(p);
}
```

:::

The key's in that `malloc()` line. If we know each `int` takes `sizeof(int)` bytes to hold it, and we know we want 10 of them, we can just allocate exactly that many bytes with:

> 那行 `malloc()` 中就有关键。如果我们知道每个 `int` 需要 `sizeof(int)` 个位元组来储存，而我们知道我们想要 10 个，我们可以只分配正好那么多位元组：

::: {#cb198 .sourceCode}

```c
sizeof(int) * 10
```

:::

And this trick works for every type. Just pass it to `sizeof` and multiply by the size of the array.

> 只需把它传给 `sizeof`，再乘以数组的大小，这个技巧就适用于所有类型。

## [12.4] An Alternative: `calloc()` {#an-alternative-calloc number="12.4"}

This is another allocation function that works similarly to `malloc()`, with two key differences:

> 这是一个类似于'malloc()'的另一个分配函数，有两个关键的不同之处：

- Instead of a single argument, you pass the size of one element, and the number of elements you wish to allocate. It's like it's made for allocating arrays.

> 代替一个参数，你传入一个元素的大小和你想要分配的元素的数量。这就像是专门用来分配数组的一样。

- It clears the memory to zero.

You still use `free()` to deallocate memory obtained through `calloc()`.

Here's a comparison of `calloc()` and `malloc()`.

::: {#cb199 .sourceCode}

```c
// Allocate space for 10 ints with calloc(), initialized to 0:
int *p = calloc(10, sizeof(int));

// Allocate space for 10 ints with malloc(), initialized to 0:
int *q = malloc(10 * sizeof(int));
memset(q, 0, 10 * sizeof(int));   // set to 0
```

:::

Again, the result is the same for both except `malloc()` doesn't zero the memory by default.

> 结果两者都是一样的，除了 `malloc()` 默认不会把内存清零。

## [12.5] Changing Allocated Size with `realloc()` {#changing-allocated-size-with-realloc number="12.5"}

If you've already allocated 10 `int` s, but later you decide you need 20, what can you do?

> 如果你已经分配了 10 个 int，但后来你决定需要 20 个，你该怎么办？

One option is to allocate some new space, and then `memcpy()` the memory over... but it turns out that sometimes you don't need to move anything. And there's one function that's just smart enough to do the right thing in all the right circumstances: `realloc()`.

> 一个选择是分配一些新的空间，然后使用 `memcpy()` 把内存复制过去…但是有时候你根本不需要移动任何东西。有一个函数足够聪明，可以在所有正确的情况下做出正确的事情：`realloc()`。

It takes a pointer to some previously-allocted memory (by `malloc()` or `calloc()`) and a new size for the memory region to be.

> 它需要一个指向先前分配的内存(通过 `malloc()` 或 `calloc()`)的指针以及该内存区域的新大小。

It then grows or shrinks that memory, and returns a pointer to it. Sometimes it might return the same pointer (if the data didn't have to be copied elsewhere), or it might return a different one (if the data did have to be copied).

> 它然后会增加或缩小这块内存，并返回一个指向它的指针。有时它可能会返回相同的指针(如果数据不必被复制到其他地方)，或者它可能会返回一个不同的指针(如果数据确实需要被复制)。

Be sure when you call `realloc()`, you specify the number of _bytes_ to allocate, and not just the number of array elements! That is:

> 确保在调用 `realloc()` 时，您指定的是要分配的字节数，而不仅仅是数组元素的数量！也就是：

::: {#cb200 .sourceCode}

```c
num_floats *= 2;

np = realloc(p, num_floats);  // WRONG: need bytes, not number of elements!

np = realloc(p, num_floats * sizeof(float));  // Better!
```

:::

Let's allocate an array of 20 `float` s, and then change our mind and make it an array of 40.

> 让我们分配一个 20 个 `float` 的数组，然后改变主意，把它变成一个 40 个元素的数组。

We're going to assign the return value of `realloc()` into another pointer just to make sure it's not `NULL`. If it's not, then we can reassign it into our original pointer. (If we just assigned the return value directly into the original pointer, we'd lose that pointer if the function returned `NULL` and we'd have no way to get it back.)

> 我们将 `realloc()` 的返回值赋值给另一个指针，以确保它不是 `NULL`。如果不是，我们可以将其重新分配给我们的原始指针。(如果我们直接将返回值分配给原始指针，则如果函数返回 `NULL`，我们将失去该指针，而无法恢复。)

::: {#cb201 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // Allocate space for 20 floats
    float *p = malloc(sizeof *p * 20);  // sizeof *p same as sizeof(float)

    // Assign them fractional values 0.0-1.0:
    for (int i = 0; i < 20; i++)
        p[i] = i / 20.0;

    // But wait! Let's actually make this an array of 40 elements
    float *new_p = realloc(p, sizeof *p * 40);

    // Check to see if we successfully reallocated
    if (new_p == NULL) {
        printf("Error reallocing\n");
        return 1;
    }

    // If we did, we can just reassign p
    p = new_p;

    // And assign the new elements values in the range 1.0-2.0
    for (int i = 20; i < 40; i++)
        p[i] = 1.0 + (i - 20) / 20.0;

    // Print all values 0.0-2.0 in the 40 elements:
    for (int i = 0; i < 40; i++)
        printf("%f\n", p[i]);

    // Free the space
    free(p);
}
```

:::

Notice in there how we took the return value from `realloc()` and reassigned it into the same pointer variable `p` that we passed in. That's pretty common to do.

> 在这里，我们从 `realloc()` 中获取返回值，并将其重新分配给我们传入的相同指针变量 `p`。这是非常常见的做法。

Also if line 7 is looking weird, with that `sizeof *p` in there, remember that `sizeof` works on the size of the type of the expression. And the type of `*p` is `float`, so that line is equivalent to `sizeof(float)`.

> 此外，如果第 7 行看起来有点奇怪，有那个 `sizeof *p` 在里面，请记住 `sizeof` 是用来计算表达式类型的大小的。而 `*p` 的类型是 `float`，因此该行等价于 `sizeof(float)`。

### [12.5.1] Reading in Lines of Arbitrary Length {#reading-in-lines-of-arbitrary-length number="12.5.1"}

I want to demonstrate two things with this full-blown example.

1. Use of `realloc()` to grow a buffer as we read in more data.
2. Use of `realloc()` to shrink the buffer down to the perfect size after we've completed the read.

> 使用'realloc()'在读取完成后缩小缓冲区到完美的大小。

What we see here is a loop that calls `fgetc()` over and over to append to a buffer until we see that the last character is a newline.

> 这里我们看到的是一个循环，它一次又一次地调用 `fgetc()` 来将内容添加到缓冲区，直到看到最后一个字符是换行符为止。

Once it finds the newline, it shrinks the buffer to just the right size and returns it.

> 一旦它找到换行符，它就会将缓冲区缩小到合适的大小并返回它。

::: {#cb202 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

// Read a line of arbitrary size from a file
//
// Returns a pointer to the line.
// Returns NULL on EOF or error.
//
// It's up to the caller to free() this pointer when done with it.
//
// Note that this strips the newline from the result. If you need
// it in there, probably best to switch this to a do-while.

char *readline(FILE *fp)
{
    int offset = 0;   // Index next char goes in the buffer
    int bufsize = 4;  // Preferably power of 2 initial size
    char *buf;        // The buffer
    int c;            // The character we've read in

    buf = malloc(bufsize);  // Allocate initial buffer

    if (buf == NULL)   // Error check
        return NULL;

    // Main loop--read until newline or EOF
    while (c = fgetc(fp), c != '\n' && c != EOF) {

        // Check if we're out of room in the buffer accounting
        // for the extra byte for the NUL terminator
        if (offset == bufsize - 1) {  // -1 for the NUL terminator
            bufsize *= 2;  // 2x the space

            char *new_buf = realloc(buf, bufsize);

            if (new_buf == NULL) {
                free(buf);   // On error, free and bail
                return NULL;
            }

            buf = new_buf;  // Successful realloc
        }

        buf[offset++] = c;  // Add the byte onto the buffer
    }

    // We hit newline or EOF...

    // If at EOF and we read no bytes, free the buffer and
    // return NULL to indicate we're at EOF:
    if (c == EOF && offset == 0) {
        free(buf);
        return NULL;
    }

    // Shrink to fit
    if (offset < bufsize - 1) {  // If we're short of the end
        char *new_buf = realloc(buf, offset + 1); // +1 for NUL terminator

        // If successful, point buf to new_buf;
        // otherwise we'll just leave buf where it is
        if (new_buf != NULL)
            buf = new_buf;
    }

    // Add the NUL terminator
    buf[offset] = '\0';

    return buf;
}

int main(void)
{
    FILE *fp = fopen("foo.txt", "r");

    char *line;

    while ((line = readline(fp)) != NULL) {
        printf("%s\n", line);
        free(line);
    }

    fclose(fp);
}
```

:::

When growing memory like this, it's common (though hardly a law) to double the space needed each step just to minimize the number of `realloc()` s that occur.

> 当内存增长这样时，为了最小化 `realloc()` 次数，通常(虽然不是法律)会每次将所需空间加倍。

Finally you might note that `readline()` returns a pointer to a `malloc()` d buffer. As such, it's up to the caller to explicitly `free()` that memory when it's done with it.

> 最后，你可能注意到 `readline()` 返回一个指向 `malloc()` d 缓冲区的指针。因此，当完成时，调用者必须显式地 `free()` 该内存。

### [12.5.2] `realloc()` with `NULL` {#realloc-with-null number="12.5.2"}

Trivia time! These two lines are equivalent:

::: {#cb203 .sourceCode}

```c
char *p = malloc(3490);
char *p = realloc(NULL, 3490);
```

:::

That could be convenient if you have some kind of allocation loop and you don't want to special-case the first `malloc()`.

> 如果你有一些分配循环，而你不想特殊处理第一个 malloc()，那可能会很方便。

::: {#cb204 .sourceCode}

```c
int *p = NULL;
int length = 0;

while (!done) {
    // Allocate 10 more ints:
    length += 10;
    p = realloc(p, sizeof *p * length);

    // Do amazing things
    // ...
}
```

:::

In that example, we didn't need an initial `malloc()` since `p` was `NULL` to start.

> 在这个例子中，由于 p 一开始是空的，我们不需要使用 malloc()函数。

## [12.6] Aligned Allocations {#aligned-allocations number="12.6"}

You probably aren't going to need to use this.

And I don't want to get too far off in the weeds talking about it right now, but there's this thing called _memory alignment_, which has to do with the memory address (pointer value) being a multiple of a certain number.

> 我现在不想太深入讨论这个，但有一个叫做内存对齐的东西，它与内存地址(指针值)是某个特定数字的倍数有关。

For example, a system might require that 16-bit values begin on memory addresses that are multiples of 2. Or that 64-bit values begin on memory addresses that are multiples of 2, 4, or 8, for example. It depends on the CPU.

> 例如，系统可能要求 16 位值从 2 的倍数的内存地址开始。或者 64 位值从 2 的倍数、4 的倍数或 8 的倍数的内存地址开始，例如。这取决于 CPU。

Some systems require this kind of alignment for fast memory access, or some even for memory access at all.

> 一些系统需要这种对齐来获得快速的内存访问，或者有些甚至需要这种对齐才能访问内存。

Now, if you use `malloc()`, `calloc()`, or `realloc()`, C will give you a chunk of memory that's well-aligned for any value at all, even `struct` s. Works in all cases.

> 现在，如果你使用 `malloc()`、`calloc()` 或 `realloc()`，C 将为任何值提供一块完全对齐的内存，甚至是 `struct` s。所有情况都可以正常工作。

But there might be times that you know that some data can be aligned at a smaller boundary, or must be aligned at a larger one for some reason. I imagine this is more common with embedded systems programming.

> 但有时你可能知道某些数据可以按照较小的边界对齐，或者出于某种原因必须按照较大的边界对齐。我想这在嵌入式系统编程中更为常见。

In those cases, you can specify an alignment with `aligned_alloc()`.

The alignment is an integer power of two greater than zero, so `2`, `4`, `8`, `16`, etc. and you give that to `aligned_alloc()` before the number of bytes you're interested in.

> 对齐必须是大于 0 的 2 的整数次幂，比如 2、4、8、16 等，在指定字节数之前，你需要将这个数传递给 `aligned_alloc()` 函数。

The other restriction is that the number of bytes you allocate needs to be a multiple of the alignment. But this might be changing. See [C Defect Report 460](http://www.open-std.org/jtc1/sc22/wg14/www/docs/summary.htm#dr_460)[^89^]

> 另一个限制是您分配的字节数必须是对齐的倍数。但这可能会改变。请参阅 [C 缺陷报告 460](http://www.open-std.org/jtc1/sc22/wg14/www/docs/summary.htm#dr_460)[^89^]

Let's do an example, allocating on a 64-byte boundary:

::: {#cb205 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
    // Allocate 256 bytes aligned on a 64-byte boundary
    char *p = aligned_alloc(64, 256);  // 256 == 64 * 4

    // Copy a string in there and print it
    strcpy(p, "Hello, world!");
    printf("%s\n", p);

    // Free the space
    free(p);
}
```

:::

I want to throw a note here about `realloc()` and `aligned_alloc()`. `realloc()` doesn't have any alignment guarantees, so if you need to get some aligned reallocated space, you'll have to do it the hard way with `memcpy()`.

> 我想在这里抛出一个关于 realloc()和 aligned_alloc()的注意事项。realloc()没有任何对齐保证，所以如果你需要获得一些对齐的重新分配空间，你就必须用 memcpy()来做这件事情。

Here's a non-standard `aligned_realloc()` function, if you need it:

::: {#cb206 .sourceCode}

```c
void *aligned_realloc(void *ptr, size_t old_size, size_t alignment, size_t size)
{
    char *new_ptr = aligned_alloc(alignment, size);

    if (new_ptr == NULL)
        return NULL;

    size_t copy_size = old_size < size? old_size: size;  // get min

    if (ptr != NULL)
        memcpy(new_ptr, ptr, copy_size);

    free(ptr);

    return new_ptr;
}
```

:::

Note that it _always_ copies data, taking time, while real `realloc()` will avoid that if it can. So this is hardly efficient. Avoid needing to reallocate custom-aligned data.

> 注意，它总是复制数据，花费时间，而真正的 `realloc()` 如果可以的话会避免这种情况。因此这并不是很有效率。避免需要重新分配自定义对齐的数据。

# [13] Scope {#scope number="13"}

Scope is all about what variables are visible in what contexts.

## [13.1] Block Scope {#block-scope number="13.1"}

This is the scope of almost all the variables devs define. It includes what other languages might call "function scope", i.e. variables that are declared inside functions.

> 这几乎包含了开发人员定义的所有变量的范围。它包括其他语言可能称为“函数范围”的变量，即在函数内声明的变量。

The basic rule is that if you've declared a variable in a block delimited by squirrelly braces, the scope of that variable is that block.

> 基本规则是，如果您在由括号括起来的块中声明了一个变量，那么该变量的作用域就是该块。

If there's a block inside a block, then variables declared in the _inner_ block are local to that block, and cannot be seen in the outer scope.

> 如果一个块内部有另一个块，那么在内部块中声明的变量只在该块中有效，在外部作用域中不可见。

Once a variable's scope ends, that variable can no longer be referenced, and you can consider its value to be gone into the great [bit bucket](https://en.wikipedia.org/wiki/Bit_bucket)[^90^] in the sky.

> 一旦变量的作用域结束，该变量就不能再被引用，你可以认为它的值已经飞上了天空中的[位桶](https://en.wikipedia.org/wiki/Bit_bucket)[^90^]。

An example with nested scope:

::: {#cb207 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int a = 12;         // Local to outer block, but visible in inner block

    if  (a == 12) {
        int b = 99;     // Local to inner block, not visible in outer block

        printf("%d %d\n", a, b);  // OK: "12 99"
    }

    printf("%d\n", a);  // OK, we're still in a's scope

    printf("%d\n", b);  // ILLEGAL, out of b's scope
}
```

:::

### [13.1.1] Where To Define Variables {#where-to-define-variables number="13.1.1"}

Another fun fact is that you can define variables anywhere in the block, within reason---they have the scope of that block, but cannot be used before they are defined.

> 另一个有趣的事实是，您可以在块中的任何位置定义变量，在合理的范围内---它们具有该块的范围，但在定义之前不能使用它们。

::: {#cb208 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i = 0;

    printf("%d\n", i);     // OK: "0"

    //printf("%d\n", j);   // ILLEGAL--can't use j before it's defined

    int j = 5;

    printf("%d %d\n", i, j);   // OK: "0 5"
}
```

:::

Historically, C required all the variables be defined before any code in the block, but this is no longer the case in the C99 standard.

> 在 C99 标准中，历史上 C 要求在块中的任何代码之前必须定义所有变量，但现在不再是这种情况。

### [13.1.2] Variable Hiding {#variable-hiding number="13.1.2"}

If you have a variable named the same thing at an inner scope as one at an outer scope, the one at the inner scope takes precedence as long as you're running in the inner scope. That is, it _hides_ the one at outer scope for the duration of its lifetime.

> 如果在内部作用域中有一个与外部作用域中同名的变量，只要你在内部作用域中运行，内部作用域中的变量优先。也就是说，在其生命周期内，它会隐藏外部作用域中的变量。

::: {#cb209 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i = 10;

    {
        int i = 20;

        printf("%d\n", i);  // Inner scope i, 20 (outer i is hidden)
    }

    printf("%d\n", i);  // Outer scope i, 10
}
```

:::

You might have noticed in that example that I just threw a block in there at line 7, not so much as a `for` or `if` statement to kick it off! This is perfectly legal. Sometimes a dev will want to group a bunch of local variables together for a quick computation and will do this, but it's rare to see.

> 你可能已经注意到，在第 7 行，我抛出了一个块，而不是作为 `for` 或 `if` 语句来启动它！这是完全合法的。有时开发人员会想要将一组本地变量组合起来进行快速计算，并会这样做，但很少见到。

## [13.2] File Scope {#file-scope number="13.2"}

If you define a variable outside of a block, that variable has _file scope_. It's visible in all functions in the file that come after it, and shared between them. (An exception is if a block defines a variable of the same name, it would hide the one at file scope.)

> 如果你在一个块之外定义一个变量，那么该变量具有文件范围。 它在之后的所有文件函数中都可见，并在它们之间共享。 (例外是，如果一个块定义了同名变量，它将隐藏文件范围内的变量。)

This is closest to what you would consider to be "global" scope in another language.

> 这最接近于您在其他语言中所认为的“全局”范围。

For example:

::: {#cb210 .sourceCode}

```c
#include <stdio.h>

int shared = 10;    // File scope! Visible to the whole file after this!

void func1(void)
{
    shared += 100;  // Now shared holds 110
}

void func2(void)
{
    printf("%d\n", shared);  // Prints "110"
}

int main(void)
{
    func1();
    func2();
}
```

:::

Note that if `shared` were declared at the bottom of the file, it wouldn't compile. It has to be declared _before_ any functions use it.

> 如果 `shared` 声明在文件的末尾，它将无法编译。它必须在任何函数使用它之前声明。

There are ways to further modify items at file scope, namely with [static](#static) and [extern](#extern), but we'll talk more about those later.

> 有方法可以进一步修改文件作用域中的项目，即使用[静态](#static)和 [extern](#extern)，但我们稍后会讨论更多关于这些的内容。

## [13.3] `for`-loop Scope {#for-loop-scope number="13.3"}

I really don't know what to call this, as C11 §6.8.5.3¶1 doesn't give it a proper name. We've done it already a few times in this guide, as well. It's when you declare a variable inside the first clause of a `for`-loop:

> 我真的不知道把它叫什么，因为 C11 §6.8.5.3¶1 没有给它一个正确的名字。我们在本指南中已经做过几次了，也是这样。这是指在 for 循环的第一个子句中声明一个变量：

::: {#cb211 .sourceCode}

```c
for (int i = 0; i < 10; i++)
    printf("%d\n", i);

printf("%d\n", i);  // ILLEGAL--i is only in scope for the for-loop
```

:::

In that example, `i`'s lifetime begins the moment it is defined, and continues for the duration of the loop.

> 在那个例子中，`i` 的生命周期从定义开始，一直持续到循环结束。

If the loop body is enclosed in a block, the variables defined in the `for`-loop are visible from that inner scope.

> 如果循环体被封装在一个块中，那么在 `for` 循环中定义的变量可以从内部作用域访问。

Unless, of course, that inner scope hides them. This crazy example prints `999` five times:

> 除非内部作用域隐藏它们。这个疯狂的例子会打印出“999”五次：

::: {#cb212 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    for (int i = 0; i < 5; i++) {
        int i = 999;  // Hides the i in the for-loop scope
        printf("%d\n", i);
    }
}
```

:::

## [13.4] A Note on Function Scope {#a-note-on-function-scope number="13.4"}

The C spec does refer to _function scope_, but it's used exclusively with _labels_, something we haven't discussed yet. More on that another day.

> C 规范确实提到了函数范围，但它仅用于我们尚未讨论过的标签。关于这个，我们改天再讨论。

# [14] Types II: Way More Types! {#types-ii-way-more-types number="14"}

We're used to `char`, `int`, and `float` types, but it's now time to take that stuff to the next level and see what else we have out there in the types department!

> 我们习惯于 `char`、`int` 和 `float` 类型，但现在是时候把这些东西提升到下一个层次，看看我们在类型部门还有什么！

## [14.1] Signed and Unsigned Integers {#signed-and-unsigned-integers number="14.1"}

So far we've used `int` as a _signed_ type, that is, a value that can be either negative or positive. But C also has specific _unsigned_ integer types that can only hold positive numbers.

> 到目前为止，我们使用 `int` 作为一种_有符号_类型，也就是可以是负数或正数的值。但是 C 也有特定的_无符号_整数类型，只能存储正数。

These types are prefaced by the keyword `unsigned`.

::: {#cb213 .sourceCode}

```c
int a;           // signed
signed int a;    // signed
signed a;        // signed, "shorthand" for "int" or "signed int", rare
unsigned int b;  // unsigned
unsigned c;      // unsigned, shorthand for "unsigned int"
```

:::

Why? Why would you decide you only wanted to hold positive numbers?

Answer: you can get larger numbers in an unsigned variable than you can in a signed ones.

> 答案：无符号变量中可以获得比有符号变量中更大的数字。

But why is that?

You can think of integers being represented by a certain number of _bits_[^91^]. On my computer, an `int` is represented by 64 bits.

> 可以把整数想象成由特定数量的位(bits)表示[^91^](#fn91)。在我的电脑上，一个 `int` 由 64 位表示。

And each permutation of bits that are either `1` or `0` represents a number. We can decide how to divvy up these numbers.

> 每一种由 1 或 0 组成的排列组合都代表一个数字。我们可以决定如何分配这些数字。

With signed numbers, we use (roughly) half the permutations to represent negative numbers, and the other half to represent positive numbers.

> 使用有符号数，我们大致使用一半的排列来表示负数，另一半来表示正数。

With unsigned, we use _all_ the permutations to represent positive numbers.

> 我们使用所有排列来表示正数，而不需要签名。

On my computer with 64-bit `int` s using [two's complement](https://en.wikipedia.org/wiki/Two%27s_complement)[^92^] to represent unsigned numbers, I have the following limits on integer range:

> 在我的计算机上，使用[二进制补码](https://en.wikipedia.org/wiki/Two%27s_complement)[^92^]来表示无符号数，我的整数范围有以下限制：

Type Minimum Maximum

---

`int` `-9,223,372,036,854,775,808` `9,223,372,036,854,775,807`
`unsigned int` `0` `18,446,744,073,709,551,615`

Notice that the largest positive `unsigned int` is approximately twice as large as the largest positive `int`. So you can get some flexibility there.

> 注意，最大的正 `unsigned int` 大约是最大的正 `int` 的两倍。因此，您可以获得一些灵活性。

## [14.2] Character Types {#character-types number="14.2"}

Remember `char`? The type we can use to hold a single character?

::: {#cb214 .sourceCode}

```c
char c = 'B';

printf("%c\n", c);  // "B"
```

:::

I have a shocker for you: it's actually an integer.

::: {#cb215 .sourceCode}

```c
char c = 'B';

// Change this from %c to %d:
printf("%d\n", c);  // 66 (!!)
```

:::

Deep down, `char` is just a small `int`, namely an integer that uses just a single byte of space, limiting its range to...

> 深入看去，`char` 只是一个小的 `int`，也就是一个只使用一个字节空间的整数，将其范围限制为...

Here the C spec gets just a little funky. It assures us that a `char` is a single byte, i.e. `sizeof(char) == 1`. But then in C11 §3.6¶3 it goes out of its way to say:

> 在 C 语言规范中，有一点有点棘手。它向我们保证 `char` 是一个字节，即 `sizeof(char) == 1`。但是在 C11 §3.6¶3 中，它特意强调：

> A byte is composed of a contiguous sequence of bits, _the number of which is implementation-defined._

Wait---what? Some of you might be used to the notion that a byte is 8 bits, right? I mean, that's what it is, right? And the answer is, "Almost certainly."[^93^] But C is an old language, and machines back in the day had, shall we say, a more _relaxed_ opinion over how many bits were in a byte. And through the years, C has retained this flexibility.

> 等等---什么？你们中的一些人可能习惯于一个字节是 8 位的概念，对吗？我的意思是，这就是它的样子，对吗？答案是：“几乎肯定。”[^93^]但是 C 是一种古老的语言，当时的机器对一个字节有多少位有着比较放松的看法。多年来，C 保留了这种灵活性。

But assuming your bytes in C are 8 bits, like they are for virtually all machines in the world that you'll ever see, the range of a `char` is...

> 假设你的 C 语言中的字节是 8 位，就像几乎所有你将会看到的机器上一样，`char` 的范围是...

---So before I can tell you, it turns out that `char` s might be signed or unsigned depending on your compiler. Unless you explicitly specify.

In many cases, just having `char` is fine because you don't care about the sign of the data. But if you need signed or unsigned `char` s, you _must_ be specific:

> 在许多情况下，只有 `char` 就足够了，因为你不关心数据的符号。但是如果你需要有符号或无符号的 `char`，你必须明确指出。

::: {#cb216 .sourceCode}

```c
char a;           // Could be signed or unsigned
signed char b;    // Definitely signed
unsigned char c;  // Definitely unsigned
```

:::

OK, now, finally, we can figure out the range of numbers if we assume that a `char` is 8 bits and your system uses the virtually universal two's complement representation for signed and unsigned[^94^].

> 好的，现在，最后，如果我们假设一个“char”是 8 位，而您的系统使用普遍通用的二进制补码表示有符号和无符号，我们就可以确定数字范围了。

So, assuming those constraints, we can finally figure our ranges:

`char` type Minimum Maximum

---

`signed char` `-128` `127`
`unsigned char` `0` `255`

And the ranges for `char` are implementation-defined.

Let me get this straight. `char` is actually a number, so can we do math on it?

> 让我弄清楚这一点，`char` 实际上是一个数字，那么我们可以对它进行数学运算吗？

Yup! Just remember to keep things in the range of a `char`!

::: {#cb217 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    char a = 10, b = 20;

    printf("%d\n", a + b);  // 30!
}
```

:::

What about those constant characters in single quotes, like `'B'`? How does that have a numeric value?

> 关于那些用单引号括起来的常量字符，比如 `'B'`，它们有什么数值含义？

The spec is also hand-wavey here, since C isn't designed to run on a single type of underlying system.

> 这里的规范也是模糊的，因为 C 不是专门为某一种底层系统设计的。

But let's just assume for the moment that your character set is based on [ASCII](https://en.wikipedia.org/wiki/ASCII)[^95^] for at least the first 128 characters. In that case, the character constant will be converted to a `char` whose value is the same as the ASCII value of the character.

> 假设您的字符集基于 [ASCII](https://en.wikipedia.org/wiki/ASCII)[^95^]至少前 128 个字符，那么字符常量将被转换为 `char`，其值与 ASCII 字符的值相同。

That was a mouthful. Let's just have an example:

::: {#cb218 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    char a = 10;
    char b = 'B';  // ASCII value 66

    printf("%d\n", a + b);  // 76!
}
```

:::

This depends on your execution environment and the [character set used](https://en.wikipedia.org/wiki/List_of_information_system_character_sets)[^96^]. One of the most popular character sets today is [Unicode](https://en.wikipedia.org/wiki/Unicode)[^97^] (which is a superset of ASCII), so for your basic 0-9, A-Z, a-z and punctuation, you'll almost certainly get the ASCII values out of them.

> 这取决于您的执行环境和使用的[字符集](https://en.wikipedia.org/wiki/List_of_information_system_character_sets)[^96^]。今天最流行的字符集之一是 [Unicode](https://en.wikipedia.org/wiki/Unicode)[^97^](它是 ASCII 的超集)，因此对于您的基本 0-9，A-Z，a-z 和标点符号，您几乎可以从中获得 ASCII 值。

## [14.3] More Integer Types: `short`, `long`, `long long` {#more-integer-types-short-long-long-long number="14.3"}

So far we've just generally been using two integer types:

- `char`
- `int`

and we recently learned about the unsigned variants of the integer types. And we learned that `char` was secretly a small `int` in disguise. So we know the `int` s can come in multiple bit sizes.

> 最近，我们了解了整数类型的无符号变体。我们发现 `char` 其实是一个小的 `int` 伪装者。因此，我们知道 `int` 可以有多种位大小。

But there are a couple more integer types we should look at, and the _minimum_ minimum and maximum values they can hold.

> 但我们还应该看一下其他几种整数类型，以及它们能够容纳的最小最大值。

Yes, I said "minimum" twice. The spec says that these types will hold numbers of _at least_ these sizes, so your implementation might be different. The header file `<limits.h>` defines macros that hold the minimum and maximum integer values; rely on that to be sure, and _never hardcode or assume these values_.

> 是的，我说了两次“最小”。规格说明这些类型将至少保存这些大小的数字，因此您的实现可能有所不同。头文件“<limits.h>”定义宏，用于保存最小和最大整数值；依靠它以确保，永远不要硬编码或假定这些值。

These additional types are `short int`, `long int`, and `long long int`. Commonly, when using these types, C developers leave the `int` part off (e.g. `long long`), and the compiler is perfectly happy.

> 这些附加类型是 `short int`、`long int` 和 `long long int`。通常，使用这些类型时，C 开发人员会省略 `int` 部分(例如 `long long`)，编译器也完全满意。

::: {#cb219 .sourceCode}

```c
// These two lines are equivalent:
long long int x;
long long x;

// And so are these:
short int x;
short x;
```

:::

Let's take a look at the integer data types and sizes in ascending order, grouped by signedness.

> 让我们按照有符号和无符号的顺序，按升序查看整数数据类型和大小。

---

Type Minimum Bytes Minimum Value Maximum Value

---

`char` 1 -127 or 0 127 or 255[^98^]

`signed char` 1 -127 127

`short` 2 -32767 32767

`int` 2 -32767 32767

`long` 4 -2147483647 2147483647

`long long` 8 -9223372036854775807 9223372036854775807

`unsigned char` 1 0 255

`unsigned short` 2 0 65535

`unsigned int` 2 0 65535

`unsigned long` 4 0 4294967295

## `unsigned long long` 8 0 18446744073709551615

There is no `long long long` type. You can't just keep adding `long` s like that. Don't be silly.

> 没有 `长长长` 这种类型。你不能一直加 `长`。别傻了。

> Two's complement fans might have noticed something funny about those numbers. Why does, for example, the `signed char` stop at -127 instead of -128? Remember: these are only the minimums required by the spec. Some number representations (like [sign and magnitude](https://en.wikipedia.org/wiki/Signed_number_representations#Signed_magnitude_representation)[^99^]) top off at ±127.

Let's run the same table on my 64-bit, two's complement system and see what comes out:

> 让我们在我的 64 位二进制补码系统上运行同一个表，看看会得到什么结果？

Type My Bytes Minimum Value Maximum Value

---

`char` 1 -128 127[^100^]
`signed char` 1 -128 127
`short` 2 -32768 32767
`int` 4 -2147483648 2147483647
`long` 8 -9223372036854775808 9223372036854775807
`long long` 8 -9223372036854775808 9223372036854775807
`unsigned char` 1 0 255
`unsigned short` 2 0 65535
`unsigned int` 4 0 4294967295
`unsigned long` 8 0 18446744073709551615
`unsigned long long` 8 0 18446744073709551615

That's a little more sensible, but we can see how my system has larger limits than the minimums in the specification.

> 这更加明智了，但我们可以看到我的系统比规范中的最低要求更有限制。

[So what are the macros in `<limits.h>`?]{#limits-macros}

Type Min Macro Max Macro

---

`char` `CHAR_MIN` `CHAR_MAX`
`signed char` `SCHAR_MIN` `SCHAR_MAX`
`short` `SHRT_MIN` `SHRT_MAX`
`int` `INT_MIN` `INT_MAX`
`long` `LONG_MIN` `LONG_MAX`
`long long` `LLONG_MIN` `LLONG_MAX`
`unsigned char` `0` `UCHAR_MAX`
`unsigned short` `0` `USHRT_MAX`
`unsigned int` `0` `UINT_MAX`
`unsigned long` `0` `ULONG_MAX`
`unsigned long long` `0` `ULLONG_MAX`

Notice there's a way hidden in there to determine if a system uses signed or unsigned `char` s. If `CHAR_MAX == UCHAR_MAX`, it must be unsigned.

> 注意有一种方法可以隐藏在那里，以确定系统是否使用带符号或无符号的 `char`。如果 `CHAR_MAX == UCHAR_MAX`，则必须是无符号的。

Also notice there's no minimum macro for the `unsigned` variants---they're just `0`.

> 也注意，无符号变体没有最小宏---它们只是“0”。

## [14.4] More Float: `double` and `long double` {#more-float-double-and-long-double number="14.4"}

Let's see what the spec has to say about floating point numbers in §5.2.4.2.2¶1-2:

> 让我们看看规范在§5.2.4.2.2¶1-2 中关于浮点数有什么说法：

> The following parameters are used to define the model for each floating-point type:
>
> ---
>
> Parameter Definition
>
> ---
>
> [\\(s\\)]{.math .inline} sign ([\\(\\pm1\\)]{.math .inline})
>
> [\\(b\\)]{.math .inline} base or radix of exponent representation (an integer [\\(\> 1\\)]{.math .inline})
>
> [\\(e\\)]{.math .inline} exponent (an integer between a minimum [\\(e\_{min}\\)]{.math .inline} and a maximum [\\(e\_{max}\\)]{.math .inline})
>
> [\\(p\\)]{.math .inline} precision (the number of base-[\\(b\\)]{.math .inline} digits in the significand)
>
> [\\(f_k\\)]{.math .inline} nonnegative integers less than [\\(b\\)]{.math .inline} (the significand digits)
>
> ---
>
> A _floating-point number_ ([\\(x\\)]{.math .inline}) is defined by the following model:
>
>> [\\(x=sb\^e\\sum\\limits\_{k=1}\^p f_kb\^{-k},\\)]{.math .inline}    [\\(e\_{min}\\le e\\le e\_{max}\\)]{.math .inline}
>>

I hope that cleared it right up for you.

Okay, fine. Let's step back a bit and see what's practical.

Note: we refer to a bunch of macros in this section. They can be found in the header `<float.h>`.

> 注意：在本节中，我们引用了一组宏。它们可以在头文件“<float.h>”中找到。

Floating point number are encoded in a specific sequence of bits ([IEEE-754 format](https://en.wikipedia.org/wiki/IEEE_754)[^101^] is tremendously popular) in bytes.

> 浮点数以特定的位序列([IEEE-754 格式](https://en.wikipedia.org/wiki/IEEE_754)[^101^]非常流行)存储在字节中。

Diving in a bit more, the number is basically represented as the _significand_ (which is the number part---the significant digits themselves, also sometimes referred to as the _mantissa_) and the _exponent_, which is what power to raise the digits to. Recall that a negative exponent can make a number smaller.

> 深入一点，这个数基本上表示为_有效位_(也就是数字部分-有效数字本身，有时也称为_尾数_)和_指数_，这是将数字提升到的幂。记住，负指数可以使数字变小。

Imagine we're using [\\(10\\)]{.math .inline} as a number to raise by an exponent. We could represent the following numbers by using a significand of [\\(12345\\)]{.math .inline}, and exponents of [\\(-3\\)]{.math .inline}, [\\(4\\)]{.math .inline}, and [\\(0\\)]{.math .inline} to encode the following floating point values:

> 假设我们使用[\\(10\\)]{.math .inline}作为一个指数来提高。我们可以使用[\\(12345\\)]{.math .inline}的有效位数，以及[\\(-3\\)]{.math .inline}，[\\(4\\)]{.math .inline}和[\\(0\\)]{.math .inline}的指数来表示以下浮点值：

[\\(12345\\times10\^{-3}=12.345\\)]{.math .inline}

[\\(12345\\times10\^4=123450000\\)]{.math .inline}

[\\(12345\\times10\^0=12345\\)]{.math .inline}

For all those numbers, the significand stays the same. The only difference is the exponent.

> 对于所有这些数字，显数都是相同的。唯一的不同之处在于指数。

On your machine, the base for the exponent is probably [\\(2\\)]{.math .inline}, not [\\(10\\)]{.math .inline}, since computers like binary. You can check it by printing the `FLT_RADIX` macro.

> 在你的机器上，指数的基础可能是[\(2\)]{.math .inline}，而不是[\(10\)]{.math .inline}，因为计算机喜欢二进制。你可以通过打印 `FLT_RADIX` 宏来检查它。

So we have a number that's represented by a number of bytes, encoded in some way. Because there are a limited number of bit patterns, a limited number of floating point numbers can be represented.

> 所以我们有一个由几个字节表示的数字，以某种方式编码。由于位模式有限，可以表示的浮点数也是有限的。

But more particularly, only a certain number of significant decimal digits can be represented accurately.

> 但更特别的是，只有一定数量的有效小数位数才能准确表示。

How can you get more? You can use larger data types!

And we have a couple of them. We know about `float` already, but for more precision we have `double`. And for even more precision, we have `long double` (unrelated to `long int` except by name).

> 我们有几个。我们已经知道 `float`，但为了更精确，我们有 `double`。为了更精确，我们有 `long double`(与 `long int` 除名字外无关)。

The spec doesn't go into how many bytes of storage each type should take, but on my system, we can see the relative size increases:

> 这个规格没有详细说明每种类型应该占用多少字节的存储空间，但是在我的系统上，我们可以看到相对大小的增加：

Type `sizeof`

---

`float` 4
`double` 8
`long double` 16

So each of the types (on my system) uses those additional bits for more precision.

> 每种类型(在我的系统上)都使用这些额外的位来获得更高的精度。

But _how much_ precision are we talking, here? How many decimal numbers can be represented by these values?

> 但是我们谈论的精度有多精确？这些值能表示多少位小数？

Well, C provides us with a bunch of macros in `<float.h>` to help us figure that out.

> 嗯，C 在 <float.h> 中提供了一堆宏来帮助我们弄清楚这一点。

It gets a little wonky if you are using a base-2 (binary) system for storing the numbers (which is virtually everyone on the planet, probably including you), but bear with me while we figure it out.

> 如果你使用基于 2(二进制)的系统来存储数字(几乎全世界的人都在使用，可能包括你在内)，情况会有点混乱，但请跟着我们一起来弄清楚它。

### [14.4.1] How Many Decimal Digits? {#how-many-decimal-digits number="14.4.1"}

The million dollar question is, "How many significant decimal digits can I store in a given floating point type so that I get out the same decimal number when I print it?"

> 这个百万美元的问题是：在给定的浮点类型中，我能存储多少有效的小数位，以便在打印时得到相同的小数？

The number of decimal digits you can store in a floating point type and surely get the same number back out when you print it is given by these macros:

> 浮点类型中可以存储的十进制数字数量，并且在打印时可以确保获得相同数字，由这些宏定义：

Type Decimal Digits You Can Store Minimum

---

`float` `FLT_DIG` 6
`double` `DBL_DIG` 10
`long double` `LDBL_DIG` 10

On my system, `FLT_DIG` is 6, so I can be sure that if I print out a 6 digit `float`, I'll get the same thing back. (It could be more digits---some numbers will come back correctly with more digits. But 6 is definitely coming back.)

> 在我的系统上，`FLT_DIG` 是 6，因此我可以确定，如果我打印出 6 位浮点数，我会得到相同的结果。(可能会有更多位数——一些数字可以用更多位数正确返回。但是 6 一定会返回。)

For example, printing out `float` s following this pattern of increasing digits, we apparently make it to 8 digits before something goes wrong, but after that we're back to 7 correct digits.

> 例如，按照逐渐增加的数字模式打印出 `float`，我们似乎在 8 位之前就出现了错误，但之后又回到了 7 位正确的数字。

::: {#cb220 .sourceCode}

```{.sourceCode .default}
0.12345
0.123456
0.1234567
0.12345678
0.123456791  <-- Things start going wrong
0.1234567910
```

:::

Let's do another demo. In this code we'll have two `float` s that both hold numbers that have `FLT_DIG` significant decimal digits[^102^]. Then we add those together, for what should be 12 significant decimal digits. But that's more than we can store in a `float` and correctly recover as a string---so we see when we print it out, things start going wrong after the 7th significant digit.

> 让我们做另一个演示。在这段代码中，我们有两个 `float`，它们都存储了具有 `FLT_DIG` 有效小数位的数字[^102^]。然后我们将它们加在一起，应该有 12 个有效小数位。但是这超出了我们可以存储在 `float` 中并正确恢复为字符串的范围-因此，当我们打印出来时，第 7 个有效位之后的事情就开始出错了。

::: {#cb221 .sourceCode}

```c
#include <stdio.h>
#include <float.h>

int main(void)
{
    // Both these numbers have 6 significant digits, so they can be
    // stored accurately in a float:

    float f = 3.14159f;
    float g = 0.00000265358f;

    printf("%.5f\n", f);   // 3.14159       -- correct!
    printf("%.11f\n", g);  // 0.00000265358 -- correct!

    // Now add them up
    f += g;                // 3.14159265358 is what f _should_ be

    printf("%.11f\n", f);  // 3.14159274101 -- wrong!
}
```

:::

(The above code has an `f` after the numeric constants---this indicates that the constant is type `float`, as opposed to the default of `double`. More on this later.)

> 以上的代码在数字常量后面有一个 `f`---这表明常量的类型是 `float`，而不是默认的 `double`。稍后会有更多关于这一点的内容。

Remember that `FLT_DIG` is the safe number of digits you can store in a `float` and retrieve correctly.

> 记住，`FLT_DIG` 是可以安全地存储在 `float` 中并正确检索的数字位数。

Sometimes you might get one or two more out of it. But sometimes you'll only get `FLT_DIG` digits back. The sure thing: if you store any number of digits up to and including `FLT_DIG` in a `float`, you're sure to get them back correctly.

> 有时你可能会得到一两个多余的数字。但有时你只会得到 `FLT_DIG` 位数。可以肯定的是：如果你在 `float` 中存储不超过 `FLT_DIG` 位的任何数字，你都可以正确地获取它们。

So that's the story. `FLT_DIG`. The End.

...Or is it?

### [14.4.2] Converting to Decimal and Back {#converting-to-decimal-and-back number="14.4.2"}

But storing a base 10 number in a floating point number and getting it back out is only half the story.

> 但是将十进制数存储在浮点数中，并将其取出来只是故事的一半。

Turns out floating point numbers can encode numbers that require more decimal places to print out completely. It's just that your big decimal number might not map to one of those numbers.

> 原来浮点数可以编码需要更多小数位才能完整打印出来的数字。只是你的大小数可能不会映射到其中的某个数字。

That is, when you look at floating point numbers from one to the next, there's a gap. If you try to encode a decimal number in that gap, it'll use the closest floating point number. That's why you can only encode `FLT_DIG` for a `float`.

> 当你从一个浮点数到下一个浮点数看时，会有一个间隙。如果你试图在这个间隙中编码一个十进制数，它会使用最接近的浮点数。这就是为什么你只能编码 `float` 的 `FLT_DIG`。

But what about those floating point numbers that _aren't_ in the gap? How many places do you need to print those out accurately?

> 但是那些不在间隙中的浮点数呢？你需要准确打印出多少位？

Another way to phrase this question is for any given floating point number, how many decimal digits do I have to preserve if I want to convert the decimal number back into an identical floating point number? That is, how many digits do I have to print in base 10 to recover **all** the digits in base 2 in the original number?

> 另一种表达这个问题的方式是，对于任意一个浮点数，如果我想将十进制数转换回相同的浮点数，我需要保留多少位小数？也就是说，我需要在十进制中打印多少位，才能恢复原始数字中的**所有**二进制数字？

Sometimes it might only be a few. But to be sure, you'll want to convert to decimal with a certain safe number of decimal places. That number is encoded in the following macros:

> 有时可能只有几个。但为了确保，您需要使用某个安全的小数位数将其转换为十进制数。该数字编码在以下宏中：

---

Macro Description

---

`FLT_DECIMAL_DIG` Number of decimal digits encoded in a `float`.

`DBL_DECIMAL_DIG` Number of decimal digits encoded in a `double`.

`LDBL_DECIMAL_DIG` Number of decimal digits encoded in a `long double`.

## `DECIMAL_DIG` Same as the widest encoding, `LDBL_DECIMAL_DIG`.

Let's see an example where `DBL_DIG` is 15 (so that's all we can have in a constant), but `DBL_DECIMAL_DIG` is 17 (so we have to convert to 17 decimal numbers to preserve all the bits of the original `double`).

> 让我们看一个例子，其中 `DBL_DIG` 是 15(所以在常量中只能有 15 位)，但 `DBL_DECIMAL_DIG` 是 17(因此我们必须将其转换为 17 位十进制数以保留原始 `double` 的所有位)。

Let's assign the 15 significant digit number `0.123456789012345` to `x`, and let's assign the 1 significant digit number `0.0000000000000006` to `y`.

> 让我们把 15 位有效数字 `0.123456789012345` 分配给 `x`，让我们把 1 位有效数字 `0.0000000000000006` 分配给 `y`。

::: {#cb222 .sourceCode}

```{.sourceCode .default}
x is exact: 0.12345678901234500    Printed to 17 decimal places
y is exact: 0.00000000000000060
```

:::

But let's add them together. This should give `0.1234567890123456`, but that's more than `DBL_DIG`, so strange things might happen... let's look:

> 但让我们把它们加在一起。这应该会得到 `0.1234567890123456`，但这超过了 `DBL_DIG`，所以可能会发生奇怪的事情...让我们看看：

::: {#cb223 .sourceCode}

```{.sourceCode .default}
x + y not quite right: 0.12345678901234559    Should end in 4560!
```

:::

That's what we get for printing more than `DBL_DIG`, right? But check this out... that number, above, is exactly representable as it is!

> 这就是我们因为打印出超过 DBL_DIG 而得到的结果，对吗？但看看这个...上面的数字可以精确表示出来！

If we assign `0.12345678901234559` (17 digits) to `z` and print it, we get:

> 如果我们将 0.12345678901234559(17 位)分配给 z 并打印它，我们得到：

::: {#cb224 .sourceCode}

```{.sourceCode .default}
z is exact: 0.12345678901234559   17 digits correct! More than DBL_DIG!
```

:::

If we'd truncated `z` down to 15 digits, it wouldn't have been the same number. That's why to preserve all the bits of a `double`, we need `DBL_DECIMAL_DIG` and not just the lesser `DBL_DIG`.

> 如果我们将 `z` 截断到 15 位数，它就不再是同一个数字了。这就是为什么我们需要 `DBL_DECIMAL_DIG` 而不仅仅是较小的 `DBL_DIG` 来保留双精度的所有位。

All that being said, it's clear that when we're messing with decimal numbers in general, it's not safe to print more than `FLT_DIG`, `DBL_DIG`, or `LDBL_DIG` digits to be sensible in relation to the original base 10 numbers and any subsequent math.

> 所有这些都说明，当我们处理十进制数字时，为了与原始的十进制数字和任何后续的数学操作保持一致，最好不要打印超过 `FLT_DIG`、`DBL_DIG` 或 `LDBL_DIG` 位数的数字。

But when converting from `float` to a decimal representation and _back_ to `float`, definitely use `FLT_DECIMAL_DIG` to do that so that all the bits are preserved exactly.

> 但是，在从 `float` 转换为十进制表示法并且_回_转换为 `float` 时，一定要使用 `FLT_DECIMAL_DIG` 来完成，以便完全保留所有位。

## [14.5] Constant Numeric Types {#constant-numeric-types number="14.5"}

When you write down a constant number, like `1234`, it has a type. But what type is it? Let's look at how C decides what type the constant is, and how to force it to choose a specific type.

> 当你写下一个常数，比如 `1234`，它有一种类型。但是它是什么类型呢？让我们看看 C 是如何决定常数的类型的，以及如何强制它选择一个特定的类型。

### [14.5.1] Hexadecimal and Octal {#hexadecimal-and-octal number="14.5.1"}

In addition to good ol' decimal like Grandma used to bake, C also supports constants of different bases.

> 除了像奶奶以前烘焙的传统十进制之外，C 还支持不同基数的常量。

If you lead a number with `0x`, it is read as a hex number:

::: {#cb225 .sourceCode}

```c
int a = 0x1A2B;   // Hexadecimal
int b = 0x1a2b;   // Case doesn't matter for hex digits

printf("%x", a);  // Print a hex number, "1a2b"
```

:::

If you lead a number with a `0`, it is read as an octal number:

::: {#cb226 .sourceCode}

```c
int a = 012;

printf("%o\n", a);  // Print an octal number, "12"
```

:::

This is particularly problematic for beginner programmers who try to pad decimal numbers on the left with `0` to line things up nice and pretty, inadvertently changing the base of the number:

> 这对于初学者程序员来说尤其成问题，他们试图用'0'在左边补充小数，以使其排列整齐美观，无意中改变了数字的基数：

::: {#cb227 .sourceCode}

```c
int x = 11111;  // Decimal 11111
int y = 00111;  // Decimal 73 (Octal 111)
int z = 01111;  // Decimal 585 (Octal 1111)
```

:::

#### [14.5.1.1] A Note on Binary {#a-note-on-binary number="14.5.1.1"}

An unofficial extension[^103^] in many C compilers allows you to represent a binary number with a `0b` prefix:

> 许多 C 编译器中的一个非官方扩展允许您使用“0b”前缀表示二进制数：

::: {#cb228 .sourceCode}

```c
int x = 0b101010;    // Binary 101010

printf("%d\n", x);   // Prints 42 decimal
```

:::

There's no `printf()` format specifier for printing a binary number. You have to do it a character at a time with bitwise operators.

> 没有 `printf()` 格式说明符可以用来打印二进制数字。你必须通过位运算一次一个字符地来实现。

### [14.5.2] Integer Constants {#integer-constants number="14.5.2"}

You can force a constant integer to be a certain type by appending a suffix to it that indicates the type.

> 你可以通过在常量整数后面添加一个指示其类型的后缀来强制将其转换为某种类型。

We'll do some assignments to demo, but most often devs leave off the suffixes unless needed to be precise. The compiler is pretty good at making sure the types are compatible.

> 我们会做一些作业来演示，但通常开发人员除非需要精确，否则不会使用后缀。编译器很好地确保类型兼容。

::: {#cb229 .sourceCode}

```c
int           x = 1234;
long int      x = 1234L;
long long int x = 1234LL

unsigned int           x = 1234U;
unsigned long int      x = 1234UL;
unsigned long long int x = 1234ULL;
```

:::

The suffix can be uppercase or lowercase. And the `U` and `L` or `LL` can appear either one first.

> 后缀可以是大写或小写。U 和 L 或 LL 可以先出现其中一个。

Type Suffix

---

`int` None
`long int` `L`
`long long int` `LL`
`unsigned int` `U`
`unsigned long int` `UL`
`unsigned long long int` `ULL`

I mentioned in the table that "no suffix" means `int`... but it's actually more complex than that.

> 我在表中提到“无后缀”意味着 `int`...但实际上比这更复杂。

So what happens when you have an unsuffixed number like:

::: {#cb230 .sourceCode}

```c
int x = 1234;
```

:::

What type is it?

What C will generally do is choose the smallest type from `int` up that can hold the value.

> 一般来说，C 会选择从 `int` 开始能够容纳该值的最小类型。

But specifically, that depends on the number's base (decimal, hex, or octal), as well.

> 但具体来说，这取决于数字的基数(十进制、十六进制或八进制)。

The spec has a great table indicating which type gets used for what unsuffixed value. In fact, I'm just going to copy it wholesale right here.

> 这个规范有一个很棒的表格，指示哪种类型用于什么无后缀值。事实上，我只是要在这里完整地复制它。

C11 §6.4.4.1¶5 reads, "The type of an integer constant is the first of the first of the corresponding list in which its value can be represented."

> C11 §6.4.4.1¶5 读：“整数常量的类型是可以表示其值的相应列表中的第一个。”

And then goes on to show this table:

---

Suffix Decimal Constant Octal or Hexadecimal
Constant

---

none `int`\ `int`
`long int` `unsigned int`
`long int`
`unsigned long int`
`long long int`
`unsigned long long int`\

`u` or `U` `unsigned int`\ `unsigned int`
`unsigned long int`\ `unsigned long int`
`unsigned long long int` `unsigned long long int`\

`l` or `L` `long int`\ `long int`
`long long int` `unsigned long int`
`long long int`
`unsigned long long int`\

Both `u` or `U`\ `unsigned long int`\ `unsigned long int`
and `l` or `L` `unsigned long long int` `unsigned long long int`\

`ll` or `LL` `long long int` `long long int`
`unsigned long long int`\

Both `u` or `U`\ `unsigned long long int` `unsigned long long int`
and `ll` or `LL`

---

What that's saying is that, for example, if you specify a number like `123456789U`, first C will see if it can be `unsigned int`. If it doesn't fit there, it'll try `unsigned long int`. And then `unsigned long long int`. It'll use the smallest type that can hold the number.

> 所说的是，例如，如果您指定一个像 `123456789U` 的数字，首先 C 会查看它是否可以是 `unsigned int`。 如果它不适合，它将尝试 `unsigned long int`。 然后是 `unsigned long long int`。 它将使用能够容纳该数字的最小类型。

### [14.5.3] Floating Point Constants {#floating-point-constants number="14.5.3"}

You'd think that a floating point constant like `1.23` would have a default type of `float`, right?

> 你可能会认为像 `1.23` 这样的浮点常量的默认类型应该是 `float`，对吗？

Surprise! Turns out unsuffiexed floating point numbers are type `double`! Happy belated birthday!

> 惊喜！原来不带后缀的浮点数是双精度的！祝你生日快乐！

You can force it to be of type `float` by appending an `f` (or `F`---it's case-insensitive). You can force it to be of type `long double` by appending `l` (or `L`).

> 你可以通过在末尾添加 `f`(或 `F`---大小写不敏感)来强制将其转换为 `float` 类型。你可以通过在末尾添加 `l`(或 `L`)来强制将其转换为 `long double` 类型。

Type Suffix

---

`float` `F`
`double` None
`long double` `L`

For example:

::: {#cb231 .sourceCode}

```c
float x       = 3.14f;
double x      = 3.14;
long double x = 3.14L;
```

:::

This whole time, though, we've just been doing this, right?

::: {#cb232 .sourceCode}

```c
float x = 3.14;
```

:::

Isn't the left a `float` and the right a `double`? Yes! But C's pretty good with automatic numeric conversions, so it's more common to have an unsuffixed floating point constant than not. More on that later.

> 不是左边是 `float` 而右边是 `double` 吗？是的！但 C 在自动数字转换方面很棒，所以更常见的是没有后缀的浮点常量。关于这一点稍后再说。

#### [14.5.3.1] Scientific Notation {#scientific-notation number="14.5.3.1"}

Remember earlier when we talked about how a floating point number can be represented by a significand, base, and exponent?

> 记得刚才我们谈到浮点数可以用有效数字、基底和指数来表示吗？

Well, there's a common way of writing such a number, shown here followed by it's more recognizable equivalent which is what you get when you actually run the math:

> 嗯，这里有一种常见的写法，它的更容易识别的等价物就是你实际运算出来的结果：

[\\(1.2345\\times10\^3 = 1234.5\\)]{.math .inline}

Writing numbers in the form [\\(s\\times b\^e\\)]{.math .inline} is called [_scientific notation_](https://en.wikipedia.org/wiki/Scientific_notation)[^104^]. In C, these are written using "E notation", so these are equivalent:

> 写数字的形式[\(s\times b\^e\)]{.math .inline}被称为[_科学记数法_](https://en.wikipedia.org/wiki/Scientific_notation)[^104^]。在 C 语言中，这些数字使用“E 记数法”来表示，因此这些是等价的：

Scientific Notation E notation

---

[\\(1.2345\\times10\^{-3}=0.0012345\\)]{.math .inline} `1.2345e-3`
[\\(1.2345\\times10\^8=123450000\\)]{.math .inline} `1.2345e+8`

You can print a number in this notation with `%e`:

::: {#cb233 .sourceCode}

```c
printf("%e\n", 123456.0);  // Prints 1.234560e+05
```

:::

A couple little fun facts about scientific notation:

- You don't have to write them with a single leading digit before the decimal point. Any number of numbers can go in front.

> 你不必在小数点前加上单个首位数字。可以在前面加上任意数量的数字。

::: {#cb234 .sourceCode}

```c
double x = 123.456e+3;  // 123456
```

:::

However, when you print it, it will change the exponent so there is only one digit in front of the decimal point.

> 然而，当你打印它时，它会改变指数，因此小数点前只有一个数字。

- The plus can be left off the exponent, as it's default, but this is uncommon in practice from what I've seen.

> 可以省略指数中的加号，因为它是默认的，但我所见到的情况下，这在实践中并不常见。

::: {#cb235 .sourceCode}

```c
1.2345e10 == 1.2345e+10
```

:::

- You can apply the `F` or `L` suffixes to E-notation constants:

  ::: {#cb236 .sourceCode}

  ```c
  1.2345e10F
  1.2345e10L
  ```

  :::

#### [14.5.3.2] Hexadecimal Floating Point Constants {#hexadecimal-floating-point-constants number="14.5.3.2"}

But wait, there's more floating to be done!

Turns out there are hexadecimal floating point constants, as well!

These work similar to decimal floating point numbers, but they begin with a `0x` just like integer numbers.

> 这些工作类似于十进制浮点数，但它们像整数一样以“0x”开头。

The catch is that you _must_ specify an exponent, and this exponent produces a power of 2. That is: [\\(2\^x\\)]{.math .inline}.

> 抓住的是你必须指定一个指数，而这个指数产生 2 的幂。也就是：[\\(2\^x\\)]{.math .inline}。

And then you use a `p` instead of an `e` when writing the number:

So `0xa.1p3` is [\\(10.0625\\times2\^3 == 80.5\\)]{.math .inline}.

When using floating point hex constants, We can print hex scientific notation with `%a`:

> 使用浮点十六进制常量时，我们可以使用 `%a` 打印十六进制科学记数法。

::: {#cb237 .sourceCode}

```c
double x = 0xa.1p3;

printf("%a\n", x);  // 0x1.42p+6
printf("%f\n", x);  // 80.500000
```

:::

# [15] Types III: Conversions {#types-iii-conversions number="15"}

In this chapter, we want to talk all about converting from one type to another. C has a variety of ways of doing this, and some might be a little different that you're used to in other languages.

> 在本章中，我们想谈论从一种类型转换到另一种类型。C 有各种转换方式，有些可能与您在其他语言中使用的有所不同。

Before we talk about how to make conversions happen, let's talk about how they work when they _do_ happen.

> 在我们讨论如何实现转换之前，让我们先讨论它们在发生时是如何工作的。

## [15.1] String Conversions {#string-conversions number="15.1"}

Unlike many languages, C doesn't do string-to-number (and vice-versa) conversions in quite as streamlined a manner as it does numeric conversions.

> 与许多语言不同，C 在进行字符串到数字(反之亦然)转换时，不像数字转换那样流畅。

For these, we'll have to call functions to do the dirty work.

### [15.1.1] Numeric Value to String {#numeric-value-to-string number="15.1.1"}

When we want to convert a number to a string, we can use either `sprintf()` (pronounced _SPRINT-f_) or `snprintf()` (_s-n-print-f_)[^105^]

> 当我们想要将一个数字转换为字符串时，我们可以使用 `sprintf()`(发音为_SPRINT-f_)或 `snprintf()`(发音为_s-n-print-f_)[^105^]。

These basically work like `printf()`, except they output to a string instead, and you can print that string later, or whatever.

> 这些基本上像 `printf()` 一样工作，只是它们输出到一个字符串，你可以稍后打印该字符串，或者其他任何东西。

For example, turning part of the value π into a string:

::: {#cb238 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    char s[10];
    float f = 3.14159;

    // Convert "f" to string, storing in "s", writing at most 10 characters
    // including the NUL terminator

    snprintf(s, 10, "%f", f);

    printf("String value: %s\n", s);  // String value: 3.141590
}
```

:::

So you can use `%d` or `%u` like you're used to for integers.

### [15.1.2] String to Numeric Value {#string-to-numeric-value number="15.1.2"}

There are a couple families of functions to do this in C. We'll call these the `atoi` (pronounced _a-to-i_) family and the `strtol` (_stir-to-long_) family.

> 在 C 中有几个函数系列可以完成这项工作，我们称之为 `atoi`(发音为_a-to-i_)系列和 `strtol`(发音为_stir-to-long_)系列。

For basic conversion from a string to a number, try the `atoi` functions from `<stdlib.h>`. These have bad error-handling characteristics (including undefined behavior if you pass in a bad string), so use them carefully.

> 对于从字符串到数字的基本转换，请尝试从 <stdlib.h> 中使用 atoi 函数。这些函数具有较差的错误处理特性(如果传入错误字符串会导致未定义的行为)，因此请小心使用。

Function Description

---

`atoi` String to `int`
`atof` String to `float`
`atol` String to `long int`
`atoll` String to `long long int`

Though the spec doesn't cop to it, the `a` at the beginning of the function stands for [ASCII](https://en.wikipedia.org/wiki/ASCII)[^106^], so really `atoi()` is "ASCII-to-integer", but saying so today is a bit ASCII-centric.

> 尽管规范没有提到，函数开头的 `a` 代表 [ASCII](https://en.wikipedia.org/wiki/ASCII)，因此 `atoi()` 实际上是“ASCII 到整数”，但是今天说这样有点偏向 ASCII。

Here's an example converting a string to a `float`:

::: {#cb239 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *pi = "3.14159";
    float f;

    f = atof(pi);

    printf("%f\n", f);
}
```

:::

But, like I said, we get undefined behavior from weird things like this:

::: {#cb240 .sourceCode}

```c
int x = atoi("what");  // "What" ain't no number I ever heard of
```

:::

(When I run that, I get `0` back, but you really shouldn't count on that in any way. You could get something completely different.)

> 当我运行它时，我得到了 `0`，但你不应该指望它会有任何不同。你可能会得到完全不同的东西。

For better error handling characteristics, let's check out all those `strtol` functions, also in `<stdlib.h>`. Not only that, but they convert to more types and more bases, too!

> 为了更好的错误处理特性，让我们查看所有的 `strtol` 函数，也在 `<stdlib.h>` 中。不仅如此，它们还可以转换为更多的类型和更多的基数！

Function Description

---

`strtol` String to `long int`
`strtoll` String to `long long int`
`strtoul` String to `unsigned long int`
`strtoull` String to `unsigned long long int`
`strtof` String to `float`
`strtod` String to `double`
`strtold` String to `long double`

These functions all follow a similar pattern of use, and are a lot of people's first experience with pointers to pointers! But never fret---it's easier than it looks.

> 这些函数都遵循类似的使用模式，也是很多人第一次接触指向指针的经历！但不要担心---它比看起来容易。

Let's do an example where we convert a string to an `unsigned long`, discarding error information (i.e. information about bad characters in the input string):

> 让我们做一个例子，将字符串转换为无符号长整型，忽略错误信息(即输入字符串中的错误字符的信息)：

::: {#cb241 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *s = "3490";

    // Convert string s, a number in base 10, to an unsigned long int.
    // NULL means we don't care to learn about any error information.

    unsigned long int x = strtoul(s, NULL, 10);

    printf("%lu\n", x);  // 3490
}
```

:::

Notice a couple things there. Even though we didn't deign to capture any information about error characters in the string, `strtoul()` won't give us undefined behavior; it will just return `0`.

> 注意一些事情。即使我们没有设计捕获字符串中的任何错误字符，`strtoul()` 也不会给我们带来不确定的行为；它只会返回 `0`。

Also, we specified that this was a decimal (base 10) number.

Does this mean we can convert numbers of different bases? Sure! Let's do binary!

> 当我们可以把不同进制的数字转换吗？当然可以！让我们来做二进制的吧！

::: {#cb242 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *s = "101010";  // What's the meaning of this number?

    // Convert string s, a number in base 2, to an unsigned long int.

    unsigned long int x = strtoul(s, NULL, 2);

    printf("%lu\n", x);  // 42
}
```

:::

OK, that's all fun and games, but what's with that `NULL` in there? What's that for?

> 好吧，这都很有趣，但是那里的 `NULL` 是什么意思？它是干什么用的？

That helps us figure out if an error occurred in the processing of the string. It's a pointer to a pointer to a `char`, which sounds scary, but isn't once you wrap your head around it.

> 这有助于我们弄清楚字符串处理过程中是否发生了错误。它是一个指向指向 `char` 的指针，听起来很可怕，但是一旦你理解它就不那么可怕了。

Let's do an example where we feed in a deliberately bad number, and we'll see how `strtol()` lets us know where the first invalid digit is.

> 让我们做一个例子，我们输入一个故意错误的数字，看看 `strtol()` 如何让我们知道第一个无效数字在哪里。

::: {#cb243 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *s = "34x90";  // "x" is not a valid digit in base 10!
    char *badchar;

    // Convert string s, a number in base 10, to an unsigned long int.

    unsigned long int x = strtoul(s, &badchar, 10);

    // It tries to convert as much as possible, so gets this far:

    printf("%lu\n", x);  // 34

    // But we can see the offending bad character because badchar
    // points to it!

    printf("Invalid character: %c\n", *badchar);  // "x"
}
```

:::

So there we have `strtoul()` modifying what `badchar` points to in order to show us where things went wrong[^107^].

> 所以我们有 `strtoul()` 修改 `badchar` 指向的内容，以显示出哪里出了问题 [^107^]。

But what if nothing goes wrong? In that case, `badchar` will point to the `NUL` terminator at the end of the string. So we can test for it:

> 如果一切顺利，那么 `badchar` 将指向字符串末尾的 `NUL` 终止符。因此，我们可以进行测试：

::: {#cb244 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *s = "3490";  // "x" is not a valid digit in base 10!
    char *badchar;

    // Convert string s, a number in base 10, to an unsigned long int.

    unsigned long int x = strtoul(s, &badchar, 10);

    // Check if things went well

    if (*badchar == '\0') {
        printf("Success! %lu\n", x);
    } else  {
        printf("Partial conversion: %lu\n", x);
        printf("Invalid character: %c\n", *badchar);
    }
}
```

:::

So there you have it. The `atoi()`-style functions are good in a controlled pinch, but the `strtol()`-style functions give you far more control over error handling and the base of the input.

> 这就是它了。`atoi()` 风格的函数在受控的情况下很有用，但 `strtol()` 风格的函数可以更好地控制错误处理和输入的基础。

## [15.2] `char` Conversions {#char-conversions number="15.2"}

What if you have a single character with a digit in it, like `'5'`... Is that the same as the value `5`?

> 如果你有一个带有数字的单个字符，比如'5'，那么它和值 5 是一样的吗？

Let's try it and see.

::: {#cb245 .sourceCode}

```c
printf("%d %d\n", 5, '5');
```

:::

On my UTF-8 system, this prints:

::: {#cb246 .sourceCode}

```{.sourceCode .default}
5 53
```

:::

So... no. And 53? What is that? That's the UTF-8 (and ASCII) code point for the character symbol `'5'`[^108^]

> 不，53 是什么？那是 UTF-8(和 ASCII)编码中的字符符号“5”的编码点。

So how do we convert the character `'5'` (which apparently has value 53) into the value `5`?

> 那么我们如何将字符 `'5'`(其值为 53)转换为值 `5`？

With one clever trick, that's how!

The C Standard guarantees that these character will have code points that are in sequence and in this order:

> 标准 C 保证这些字符的码点按顺序排列：

::: {#cb247 .sourceCode}

```{.sourceCode .default}
0  1  2  3  4  5  6  7  8  9
```

:::

Ponder for a second--how can we use that? Spoilers ahead...

Let's take a look at the characters and their code points in UTF-8:

::: {#cb248 .sourceCode}

```{.sourceCode .default}
0  1  2  3  4  5  6  7  8  9
48 49 50 51 52 53 54 55 56 57
```

:::

You see there that `'5'` is `53`, just like we were getting. And `'0'` is `48`.

> 你看到那里'5'是 53，就像我们所得到的一样。而'0'是 48。

So we can subtract `'0'` from any digit character to get its numeric value:

> 我们可以从任何数字字符中减去'0'来获得它的数值。

::: {#cb249 .sourceCode}

```c
char c = '6';

int x = c;  // x has value 54, the code point for '6'

int y = c - '0'; // y has value 6, just like we want
```

:::

And we can convert the other way, too, just by adding the value on.

::: {#cb250 .sourceCode}

```c
int x = 6;

char c = x + '0';  // c has value 54

printf("%d\n", c);  // prints 54
printf("%c\n", c);  // prints 6 with %c
```

:::

You might think this is a weird way to do this conversion, and by today's standards, it certainly is. But back in the olden days when computers were made literally out of wood, this was the method for doing this conversion. And it wasn't broke, so C never fixed it.

> 你可能认为这是一种奇怪的转换方式，按照当今的标准来看，当然是这样。但是在古老的时代，计算机是用木头做的，这就是这种转换的方法。它没有坏，所以 C 也没有修复它。

## [15.3] Numeric Conversions {#numeric-conversions number="15.3"}

### [15.3.1] Boolean {#boolean number="15.3.1"}

If you convert a zero to `bool`, the result is `0`. Otherwise it's `1`.

### [15.3.2] Integer to Integer Conversions {#integer-to-integer-conversions number="15.3.2"}

If an integer type is converted to unsigned and doesn't fit in it, the unsigned result wraps around odometer-style until it fits in the unsigned[^109^].

> 如果一个整数类型被转换为无符号数，而且不能容纳它，那么无符号结果就会像里程表一样绕回，直到它适合无符号数。

If an integer type is converted to a signed number and doesn't fit, the result is implementation-defined! Something documented will happen, but you'll have to look it up[^110^]

> 如果一个整数类型转换为有符号数，而又不符合要求，那么结果是实现定义的！会发生一些已经文档化的事情，但你需要查阅 [^110^]。

### [15.3.3] Integer and Floating Point Conversions {#integer-and-floating-point-conversions number="15.3.3"}

If a floating point type is converted to an integer type, the fractional part is discarded with prejudice[^111^].

> 如果一个浮点类型被转换为整数类型，则小数部分会被毫不留情地丢弃。

But---and here's the catch---if the number is too large to fit in the integer, you get undefined behavior. So don't do that.

> 但是---这里是个问题---如果数字太大而无法放入整数，你会得到未定义的行为。所以不要这么做。

Going From integer or floating point to floating point, C makes a best effort to find the closest floating point number to the integer that it can.

> 从整数或浮点数到浮点数，C 尽最大努力找到与整数最接近的浮点数。

Again, though, if the original value can't be represented, it's undefined behavior.

> 如果原始值无法表示，那么这是未定义的行为。

## [15.4] Implicit Conversions {#implicit-conversions number="15.4"}

These are conversions the compiler does automatically for you when you mix and match types.

> 这些是编译器在您混合和匹配类型时自动为您执行的转换。

### [15.4.1] The Integer Promotions {#integer-promotions number="15.4.1"}

In a number of places, if an `int` can be used to represent a value from `char` or `short` (signed or unsigned), that value is _promoted_ up to `int`. If it doesn't fit in an `int`, it's promoted to `unsigned int`.

> 在许多地方，如果一个 `int` 可以用来表示来自 `char` 或 `short`(有符号或无符号)的值，那么该值将被提升到 `int`。如果它不适合 `int`，它将被提升到 `unsigned int`。

This is how we can do something like this:

::: {#cb251 .sourceCode}

```c
char x = 10, y = 20;
int i = x + y;
```

:::

In that case, `x` and `y` get promoted to `int` by C before the math takes place.

> 在这种情况下，C 在进行数学运算之前，会将 x 和 y 提升为 int 类型。

The integer promotions take place during The Usual Arithmetic Conversions, with variadic functions[^112^], unary `+` and `-` operators, or when passing values to functions without prototypes[^113^].

> 整数提升在通常的算术转换、变参函数、一元加号和减号运算符，或者在传递值给没有原型的函数时发生。

### [15.4.2] The Usual Arithmetic Conversions {#usual-arithmetic-conversions number="15.4.2"}

These are automatic conversions that C does around numeric operations that you ask for. (That's actually what they're called, by the way, by C11 §6.3.1.8.) Note that for this section, we're just talking about numeric types---strings will come later.

> 这些是 C 在您要求的数字操作周围自动执行的转换。(事实上，这就是 C11§6.3.1.8 称之为的。)请注意，在本节中，我们只讨论数字类型---字符串将在稍后讨论。

These conversions answer questions about what happens when you mix types, like this:

> 这些转换回答了关于混合类型时会发生什么的问题，比如：

::: {#cb252 .sourceCode}

```c
int x = 3 + 1.2;   // Mixing int and double
                   // 4.2 is converted to int
                   // 4 is stored in x

float y = 12 * 2;  // Mixing float and int
                   // 24 is converted to float
                   // 24.0 is stored in y
```

:::

Do they become `int` s? Do they become `float` s? How does it work?

Here are the steps, paraphrased for easy consumption.

1. If one thing in the expression is a floating type, convert the other things to that floating type.

> 如果表达式中的一个东西是浮点类型，将其他东西转换为该浮点类型。

2. Otherwise, if both types are integer types, perform the integer promotions on each, then make the operand types as big as they need to be hold the common largest value. Sometimes this involves changing signed to unsigned.

> 如果两种类型都是整数类型，则对每个操作数执行整数提升，然后使操作数类型尽可能大，以容纳公共最大值。有时这涉及将有符号的改为无符号的。

If you want to know the gritty details, check out C11 §6.3.1.8. But you probably don't.

> 如果你想知道细节，可以查看 C11 §6.3.1.8。但你可能不想看。

Just generally remember that int types become float types if there's a floating point type anywhere in there, and the compiler makes an effort to make sure mixed integer types don't overflow.

> 一般来说，如果有任何浮点类型，int 类型就会变成 float 类型，编译器会尽力确保混合整数类型不会溢出。

Finally, if you convert from one floating point type to another, the compiler will try to make an exact conversion. If it can't, it'll do the best approximation it can. If the number is too large to fit in the type you're converting into, _boom_: undefined behavior!

> 最后，如果你从一种浮点类型转换到另一种，编译器会尝试做出精确的转换。如果它做不到，它会尽力做出最接近的近似值。如果数字太大而无法适应你要转换的类型，_砰_：未定义的行为！

### [15.4.3] `void*` {#void number="15.4.3"}

The `void*` type is interesting because it can be converted from or to any pointer type.

> void* 类型很有趣，因为它可以转换成任何指针类型或从任何指针类型转换。

::: {#cb253 .sourceCode}

```c
int x = 10;

void *p = &x;  // &x is type int*, but we store it in a void*

int *q = p;    // p is void*, but we store it in an int*
```

:::

## [15.5] Explicit Conversions {#explicit-conversions number="15.5"}

These are conversions from type to type that you have to ask for; the compiler won't do it for you.

> 这些是你必须要求的类型转换；编译器不会为你做。

You can convert from one type to another by assigning one type to another with an `=`.

> 你可以通过使用 `=` 将一种类型赋值给另一种类型来进行转换。

You can also convert explicitly with a _cast_.

### [15.5.1] Casting {#casting number="15.5.1"}

You can explicitly change the type of an expression by putting a new type in parentheses in front of it. Some C devs frown on the practice unless absolutely necessary, but it's likely you'll come across some C code with these in it.

> 你可以通过在表达式前面放置一个新类型的括号来显式地改变表达式的类型。一些 C 开发人员不喜欢这种做法，除非绝对必要，但你可能会遇到一些带有这些内容的 C 代码。

Let's do an example where we want to convert an `int` into a `long` so that we can store it in a `long`.

> 让我们做一个例子，我们想把一个 `int` 转换成 `long`，这样我们就可以把它存储在 `long` 中。

Note: this example is contrived and the cast in this case is completely unnecessary because the `x + 12` expression would automatically be changed to `long int` to match the wider type of `y`.

> 注意：这个例子是故意的，因为 `x + 12` 表达式会自动转换为更宽的类型 `long int` 来匹配 `y`，所以这种强制转换是完全不必要的。

::: {#cb254 .sourceCode}

```c
int x = 10;
long int y = (long int)x + 12;
```

:::

In that example, even those `x` was type `int` before, the expression `(long int)x` has type `long int`. We say, "We cast `x` to `long int`."

> 在这个例子中，即使 `x` 之前是 `int` 类型，表达式 `(long int)x` 的类型也是 `long int`。我们说，“我们将 `x` 转换为 `long int`。”

More commonly, you might see a cast being used to convert a `void*` into a specific pointer type so it can be dereferenced.

> 通常，您可能会看到使用强制转换将 `void *` 转换为特定的指针类型，以便可以对其进行解引用。

A callback from the built-in `qsort()` function might display this behavior since it has `void*` s passed into it:

> 内置的 `qsort()` 函数的回调可能会显示这种行为，因为它传入了 `void*`：

::: {#cb255 .sourceCode}

```c
int compar(const void *elem1, const void *elem2)
{
    if (*((const int*)elem2) > *((const int*)elem1)) return 1;
    if (*((const int*)elem2) < *((const int*)elem1)) return -1;
    return 0;
}
```

:::

But you could also clearly write it with an assignment:

::: {#cb256 .sourceCode}

```c
int compar(const void *elem1, const void *elem2)
{
    const int *e1 = elem1;
    const int *e2 = elem2;

    return *e2 - *e1;
}
```

:::

One place you'll see casts more commonly is to avoid a warning when printing pointer values with the rarely-used `%p` which gets picky with anything other than a `void*`:

> 你最常见到的应用场景是使用很少见的 `%p` 打印指针值时，为了避免警告，它只能接受 `void*` 类型：

::: {#cb257 .sourceCode}

```c
int x = 3490;
int *p = &x;

printf("%p\n", p);
```

:::

generates this warning:

::: {#cb258 .sourceCode}

```{.sourceCode .default}
warning: format ‘%p’ expects argument of type ‘void *’, but argument
         2 has type ‘int *’
```

:::

You can fix it with a cast:

::: {#cb259 .sourceCode}

```c
printf("%p\n", (void *)p);
```

:::

Another place is with explicit pointer changes, if you don't want to use an intervening `void*`, but these are also pretty uncommon:

> 另一种方法是显式更改指针，如果你不想使用中间的 `void*`，但这种方法也很少见：

::: {#cb260 .sourceCode}

```c
long x = 3490;
long *p = &x;
unsigned char *c = (unsigned char *)p;
```

:::

A third place it's often required is with the character conversion functions in [`<ctype.h>`](https://beej.us/guide/bgclr/html/split/ctype.html)[^114^] where you should cast questionably-signed values to `unsigned char` to avoid undefined behavior.

> 需要第三个位置的是在[`<ctype.h>`](https://beej.us/guide/bgclr/html/split/ctype.html)[^114^]中的字符转换函数，在这里，您应该将可疑签名值转换为 `unsigned char` 以避免未定义的行为。

Again, casting is rarely _needed_ in practice. If you find yourself casting, there might be another way to do the same thing, or maybe you're casting unnecessarily.

> 再次，实践中很少需要投射。如果你发现自己在投射，可能有另一种方法来做同样的事情，或者也许你是不必要地投射。

Or maybe it is necessary. Personally, I try to avoid it, but am not afraid to use it if I have to.

> 或许有必要。我个人尽量避免，但如果必须的话，也不怕使用它。

# [16] Types IV: Qualifiers and Specifiers {#types-iv-qualifiers-and-specifiers number="16"}

Now that we have some more types under our belts, turns out we can give these types some additional attributes that control their behavior. These are the _type qualifiers_ and _storage-class specifiers_.

> 现在我们有了更多的类型，原来我们可以给这些类型一些额外的属性来控制它们的行为。这些是类型限定符和存储类说明符。

## [16.1] Type Qualifiers {#type-qualifiers number="16.1"}

These are going to allow you to declare constant values, and also to give the compiler optimization hints that it can use.

> 这些将允许您声明常量值，并且还可以给编译器提供优化提示，以便它可以使用。

### [16.1.1] `const` {#const number="16.1.1"}

This is the most common type qualifier you'll see. It means the variable is constant, and any attempt to modify it will result in a very angry compiler.

> 这是你最常见的类型限定符。它意味着变量是常量，任何尝试修改它都会导致编译器非常生气。

::: {#cb261 .sourceCode}

```c
const int x = 2;

x = 4;  // COMPILER PUKING SOUNDS, can't assign to a constant
```

:::

You can't change a `const` value.

Often you see `const` in parameter lists for functions:

::: {#cb262 .sourceCode}

```c
void foo(const int x)
{
    printf("%d\n", x + 30);  // OK, doesn't modify "x"
}
```

:::

#### [16.1.1.1] `const` and Pointers {#const-and-pointers number="16.1.1.1"}

This one gets a little funky, because there are two usages that have two meanings when it comes to pointers.

> 这有点棘手，因为指针有两种用法，有两种含义。

For one thing, we can make it so you can't change the thing the pointer points to. You do this by putting the `const` up front with the type name (before the asterisk) in the type declaration.

> 对于一件事，我们可以让指针指向的东西不能改变。你可以在类型声明中在星号之前放置 `const` 来实现这一点。

::: {#cb263 .sourceCode}

```c
int x[] = {10, 20};
const int *p = x;

p++;  // We can modify p, no problem

*p = 30; // Compiler error! Can't change what it points to
```

:::

Somewhat confusingly, these two things are equivalent:

::: {#cb264 .sourceCode}

```c
const int *p;  // Can't modify what p points to
int const *p;  // Can't modify what p points to, just like the previous line
```

:::

Great, so we can't change the thing the pointer points to, but we can change the pointer itself. What if we want the other way around? We want to be able to change what the pointer points to, but _not_ the pointer itself?

> 很好，所以我们不能改变指针指向的东西，但我们可以改变指针自身。如果我们想要另一种方式呢？我们希望能够改变指针指向的东西，但不改变指针自身呢？

Just move the `const` after the asterisk in the declaration:

::: {#cb265 .sourceCode}

```c
int *const p;   // We can't modify "p" with pointer arithmetic

p++;  // Compiler error!
```

:::

But we can modify what they point to:

::: {#cb266 .sourceCode}

```c
int x = 10;
int *const p = &x;

*p = 20;   // Set "x" to 20, no problem
```

:::

You can also do make both things `const`:

::: {#cb267 .sourceCode}

```c
const int *const p;  // Can't modify p or *p!
```

:::

Finally, if you have multiple levels of indirection, you should `const` the appropriate levels. Just because a pointer is `const`, doesn't mean the pointer it points to must also be. You can explicitly set them like in the following examples:

> 最后，如果您有多个间接级别，您应该 `const` 适当的级别。 只是因为指针是 `const`，并不意味着它指向的指针也必须是。 您可以像以下示例一样显式设置它们：

::: {#cb268 .sourceCode}

```c
char **p;
p++;     // OK!
(*p)++;  // OK!

char **const p;
p++;     // Error!
(*p)++;  // OK!

char *const *p;
p++;     // OK!
(*p)++;  // Error!

char *const *const p;
p++;     // Error!
(*p)++;  // Error!
```

:::

#### [16.1.1.2] `const` Correctness {#const-correctness number="16.1.1.2"}

One more thing I have to mention is that the compiler will warn on something like this:

> 我还要提一件事，就是编译器会对这样的情况发出警告：

::: {#cb269 .sourceCode}

```c
const int x = 20;
int *p = &x;
```

:::

saying something to the effect of:

::: {#cb270 .sourceCode}

```{.sourceCode .default}
initialization discards 'const' qualifier from pointer type target
```

:::

What's happening there?

Well, we need to look at the types on either side of the assignment:

::: {#cb271 .sourceCode}

```c
    const int x = 20;
    int *p = &x;
//    ^       ^
//    |       |
//  int*    const int*
```

:::

The compiler is warning us that the value on the right side of the assignment is `const`, but the one of the left is not. And the compiler is letting us know that it is discarding the "const-ness" of the expression on the right.

> 编译器警告我们，赋值右侧的值是 `const`，但左侧的不是。编译器正在提醒我们，它正在丢弃右侧表达式的“const-ness”。

That is, we _can_ still try to do the following, but it's just wrong. The compiler will warn, and it's undefined behavior:

> 那就是，我们仍然可以尝试做下面的事情，但这是错误的。编译器会发出警告，而且这是未定义的行为：

::: {#cb272 .sourceCode}

```c
const int x = 20;
int *p = &x;

*p = 40;  // Undefined behavior--maybe it modifies "x", maybe not!

printf("%d\n", x);  // 40, if you're lucky
```

:::

### [16.1.2] `restrict` {#restrict number="16.1.2"}

TLDR: you never have to use this and you can ignore it every time you see it. If you use it correctly, you will likely realize some performance gain. If you use it incorrectly, you will realize undefined behavior.

> TLDR：你永远不需要使用它，每次看到它时你都可以忽略它。如果你正确使用它，你可能会看到一些性能提升。如果你使用不当，你会看到未定义的行为。

`restrict` is a hint to the compiler that a particular piece of memory will only be accessed by one pointer and never another. (That is, there will be no aliasing of the particular object the `restrict` pointer points to.) If a developer declares a pointer to be `restrict` and then accesses the object it points to in another way (e.g. via another pointer), the behavior is undefined.

Basically you're telling C, "Hey---I guarantee that this one single pointer is the only way I access this memory, and if I'm lying, you can pull undefined behavior on me."

> 基本上你是在告诉 C 语言：「嘿，我保证这个单一的指标是我存取记忆体的唯一方式，如果我撒谎，你可以对我执行未定义的行为。」

And C uses that information to perform certain optimizations. For instance, if you're dereferencing the `restrict` pointer repeatedly in a loop, C might decide to cache the result in a register and only store the final result once the loop completes. If any other pointer referred to that same memory and accessed it in the loop, the results would not be accurate.

> C 会利用这些资讯来执行某些优化。例如，如果你在回圈中反覆取用 `restrict` 指标，C 可能会决定将结果缓存在注册表中，并且只在回圈完成时储存最终结果。如果有任何其他指标指向相同的记忆体并在回圈中存取它，结果就不会是正确的。

(Note that `restrict` has no effect if the object pointed to is never written to. It's all about optimizations surrounding writes to memory.)

> 注意，如果从不写入指向的对象，`restrict` 就没有效果。这都是关于写入内存的优化。

Let's write a function to swap two variables, and we'll use the `restrict` keyword to assure C that we'll never pass in pointers to the same thing. And then let's blow it and try passing in pointers to the same thing.

> 让我们编写一个函数来交换两个变量，我们将使用 `restrict` 关键字来确保 C 永远不会传递指向同一个东西的指针。然后让我们犯错误，尝试传递指向同一个东西的指针。

::: {#cb273 .sourceCode}

```c
void swap(int *restrict a, int *restrict b)
{
    int t;

    t = *a;
    *a = *b;
    *b = t;
}

int main(void)
{
    int x = 10, y = 20;

    swap(&x, &y);  // OK! "a" and "b", above, point to different things

    swap(&x, &x);  // Undefined behavior! "a" and "b" point to the same thing
}
```

:::

If we were to take out the `restrict` keywords, above, that would allow both calls to work safely. But then the compiler might not be able to optimize.

> 如果我们把 `restrict` 关键字去掉，上面的调用就可以安全地工作。但是编译器可能无法进行优化。

`restrict` has block scope, that is, the restriction only lasts for the scope it's used. If it's in a parameter list for a function, it's in the block scope of that function.

If the restricted pointer points to an array, it only applies to the individual objects in the array. Other pointers could read and write from the array as long as they didn't read or write any of the same elements as the restricted one.

> 如果受限指针指向一个数组，它只适用于数组中的各个对象。只要它们不读取或写入与受限指针相同的元素，其他指针可以读取和写入数组。

If it's outside any function in file scope, the restriction covers the entire program.

> 如果它在文件作用域之外的任何函数中，限制就会覆盖整个程序。

You're likely to see this in library functions like `printf()`:

::: {#cb274 .sourceCode}

```c
int printf(const char * restrict format, ...);
```

:::

Again, that's just telling the compiler that inside the `printf()` function, there will be only one pointer that refers to any part of that `format` string.

> 再次，这只是告诉编译器，在 `printf()` 函数中，只有一个指针指向该 `格式` 字符串的任何部分。

One last note: if you're using array notation in your function parameter for some reason instead of pointer notation, you can use `restrict` like so:

> 最后一点：如果您出于某种原因在函数参数中使用数组表示法而不是指针表示法，可以像这样使用 `restrict`：

::: {#cb275 .sourceCode}

```c
void foo(int p[restrict])     // With no size

void foo(int p[restrict 10])  // Or with a size
```

:::

But pointer notation would be more common.

### [16.1.3] `volatile` {#volatile number="16.1.3"}

You're unlikely to see or need this unless you're dealing with hardware directly.

> 你很不可能看到或需要这个，除非你直接处理硬件。

`volatile` tells the compiler that a value might change behind its back and should be looked up every time.

An example might be where the compiler is looking in memory at an address that continuously updates behind the scenes, e.g. some kind of hardware timer.

> 一个例子可能是编译器在内存中查看一个不断更新的地址，例如某种硬件计时器。

If the compiler decides to optimize that and store the value in a register for a protracted time, the value in memory will update and won't be reflected in the register.

> 如果编译器决定优化并将值长时间存储在寄存器中，内存中的值将更新，而不会反映在寄存器中。

By declaring something `volatile`, you're telling the compiler, "Hey, the thing this points at might change at any time for reasons outside this program code."

> 通过声明某物为 `volatile`，你告诉编译器：“嘿，这个指向的东西可能会因为程序代码之外的原因随时发生变化。”

::: {#cb276 .sourceCode}

```c
volatile int *p;
```

:::

### [16.1.4] `_Atomic` {#atomic number="16.1.4"}

This is an optional C feature that we'll talk about in [the Atomics chapter](#chapter-atomics).

> 这是一个可选的 C 特性，我们将在[原子章节](#chapter-atomics)中讨论。

## [16.2] Storage-Class Specifiers {#storage-class-specifiers number="16.2"}

Storage-class specifiers are similar to type quantifiers. They give the compiler more information about the type of a variable.

> 存储类说明符类似于类型量化符。它们为编译器提供有关变量类型的更多信息。

### [16.2.1] `auto` {#auto number="16.2.1"}

You barely ever see this keyword, since `auto` is the default for block scope variables. It's implied.

> 你几乎从不会看到这个关键字，因为 `auto` 是块作用域变量的默认值。这是隐含的。

These are the same:

::: {#cb277 .sourceCode}

```c
{
    int a;         // auto is the default...
    auto int a;    // So this is redundant
}
```

:::

The `auto` keyword indicates that this object has _automatic storage duration_. That is, it exists in the scope in which it is defined, and is automatically deallocated when the scope is exited.

> `auto` 关键字表明此对象具有自动存储持续时间。也就是说，它存在于定义它的作用域中，并且在退出作用域时自动释放。

One gotcha about automatic variables is that their value is indeterminate until you explicitly initialize them. We say they're full of "random" or "garbage" data, though neither of those really makes me happy. In any case, you won't know what's in it unless you initialize it.

> 自动变量的一个坑是，除非你明确初始化它们，它们的值是不确定的。我们说它们充满了“随机”或“垃圾”数据，但这两者都不让我感到高兴。无论如何，除非你初始化它，否则你不会知道它里面有什么。

Always initialize all automatic variables before use!

### [16.2.2] `static` {#static number="16.2.2"}

This keyword has two meanings, depending on if the variable is file scope or block scope.

> 这个关键字有两种含义，取决于变量是文件作用域还是块作用域。

Let's start with block scope.

#### [16.2.2.1] `static` in Block Scope {#static-in-block-scope number="16.2.2.1"}

In this case, we're basically saying, "I just want a single instance of this variable to exist, shared between calls."

> 在这种情况下，我们基本上是说，“我只想要一个这个变量的实例存在，在调用之间共享。”

That is, its value will persist between calls.

`static` in block scope with an initializer will only be initialized one time on program startup, not each time the function is called.

Let's do an example:

::: {#cb278 .sourceCode}

```c
#include <stdio.h>

void counter(void)
{
    static int count = 1;  // This is initialized one time

    printf("This has been called %d time(s)\n", count);

    count++;
}

int main(void)
{
    counter();  // "This has been called 1 time(s)"
    counter();  // "This has been called 2 time(s)"
    counter();  // "This has been called 3 time(s)"
    counter();  // "This has been called 4 time(s)"
}
```

:::

See how the value of `count` persists between calls?

One thing of note is that `static` block scope variables are initialized to `0` by default.

> 一个值得注意的事情是，`静态` 块作用域变量默认初始化为 `0`。

::: {#cb279 .sourceCode}

```c
static int foo;      // Default starting value is `0`...
static int foo = 0;  // So the `0` assignment is redundant
```

:::

Finally, be advised that if you're writing multithreaded programs, you have to be sure you don't let multiple threads trample the same variable.

> 最后，请注意，如果您正在编写多线程程序，您必须确保不让多个线程践踏同一个变量。

#### [16.2.2.2] `static` in File Scope {#static-in-file-scope number="16.2.2.2"}

When you get out to file scope, outside any blocks, the meaning rather changes.

> 当你走出文件范围，在任何块之外，意义就会发生变化。

Variables at file scope already persist between function calls, so that behavior is already there.

> 变量在文件作用域中已经在函数调用之间持续存在，因此该行为已经存在。

Instead what `static` means in this context is that this variable isn't visible outside of this particular source file. Kinda like "global", but only in this file.

> 在这种情况下，`static` 的意思是这个变量不可以在这个特定的源文件之外可见。有点像“全局”，但只限于这个文件。

More on that in the section about building with multiple source files.

### [16.2.3] `extern` {#extern number="16.2.3"}

The `extern` storage-class specifier gives us a way to refer to objects in other source files.

> `extern` 存储类说明符为我们提供了一种引用其他源文件中对象的方式。

Let's say, for example, the file `bar.c` had the following as its entirety:

> 咱们举个例子，文件 `bar.c` 的全部内容如下：

::: {#cb280 .sourceCode}

```c
// bar.c

int a = 37;
```

:::

Just that. Declaring a new `int a` in file scope.

But what if we had another source file, `foo.c`, and we wanted to refer to the `a` that's in `bar.c`?

> 如果我们有另一个源文件 `foo.c`，我们想引用 `bar.c` 中的 `a`，会怎么样？

It's easy with the `extern` keyword:

::: {#cb281 .sourceCode}

```c
// foo.c

extern int a;

int main(void)
{
    printf("%d\n", a);  // 37, from bar.c!

    a = 99;

    printf("%d\n", a);  // Same "a" from bar.c, but it's now 99
}
```

:::

We could have also made the `extern int a` in block scope, and it still would have referred to the `a` in `bar.c`:

> 我们也可以在块作用域中定义 extern int a，它仍然会引用 bar.c 中的 a。

::: {#cb282 .sourceCode}

```c
// foo.c

int main(void)
{
    extern int a;

    printf("%d\n", a);  // 37, from bar.c!

    a = 99;

    printf("%d\n", a);  // Same "a" from bar.c, but it's now 99
}
```

:::

Now, if `a` in `bar.c` had been marked `static`. this wouldn't have worked. `static` variables at file scope are not visible outside that file.

> 现在，如果在 bar.c 中的 a 被标记为 static，这就不会起作用了。文件作用域内的静态变量在该文件外是不可见的。

A final note about `extern` on functions. For functions, `extern` is the default, so it's redundant. You can declare a function `static` if you only want it visible in a single source file.

> 关于函数的 `extern` 的最后一点说明：对于函数来说，`extern` 是默认的，因此是多余的。如果只想让它在单个源文件中可见，可以将其声明为 `static`。

### [16.2.4] `register` {#register number="16.2.4"}

This is a keyword to hint to the compiler that this variable is frequently-used, and should be made as fast as possible to access. The compiler is under no obligation to agree to it.

> 这是一个关键字，提示编译器这个变量经常使用，应尽可能快速访问。编译器不一定同意这一点。

Now, modern C compiler optimizers are pretty effective at figuring this out themselves, so it's rare to see these days.

> 现在，现代 C 编译器优化器在自行弄清这一点方面非常有效，因此这种情况很少见。

But if you must:

::: {#cb283 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    register int a;   // Make "a" as fast to use as possible.

    for (a = 0; a < 10; a++)
        printf("%d\n", a);
}
```

:::

It does come at a price, however. You can't take the address of a register:

> 这是有代价的，但是你不能拿到寄存器的地址。

::: {#cb284 .sourceCode}

```c
register int a;
int *p = &a;    // COMPILER ERROR! Can't take address of a register
```

:::

The same applies to any part of an array:

::: {#cb285 .sourceCode}

```c
register int a[] = {11, 22, 33, 44, 55};
int *p = a;  // COMPILER ERROR! Can't take address of a[0]
```

:::

Or dereferencing part of an array:

::: {#cb286 .sourceCode}

```c
register int a[] = {11, 22, 33, 44, 55};

int a = *(a + 2);  // COMPILER ERROR! Address of a[0] taken
```

:::

Interestingly, for the equivalent with array notation, gcc only warns:

::: {#cb287 .sourceCode}

```c
register int a[] = {11, 22, 33, 44, 55};

int a = a[2];  // COMPILER WARNING!
```

:::

with:

::: {#cb288 .sourceCode}

```{.sourceCode .default}
warning: ISO C forbids subscripting ‘register’ array
```

:::

The fact that you can't take the address of a register variable frees the compiler up to make optimizations around that assumption if it hasn't figured them out already. Also adding `register` to a `const` variable prevents one from accidentally passing its pointer to another function that willfully ignore its constness[^115^].

> 事实上，你不能拿取一个寄存器变量的地址，这使得编译器可以围绕这一假设做出优化，如果它还没有弄清楚的话。此外，将 `register` 添加到 `const` 变量中可以防止将其指针意外传递给另一个故意忽略其 constness 的函数。

A bit of historic backstory, here: deep inside the CPU are little dedicated "variables" called [_registers_](https://en.wikipedia.org/wiki/Processor_register)[^116^]. They are super fast to access compared to RAM, so using them gets you a speed boost. But they're not in RAM, so they don't have an associated memory address (which is why you can't take the address-of or get a pointer to them).

> 在 CPU 内部有一点历史背景：深处有一些专用的“变量”，称为[寄存器](https://en.wikipedia.org/wiki/Processor_register)[^116^]。与 RAM 相比，它们访问起来非常快，因此使用它们可以提高速度。但是它们不在 RAM 中，因此它们没有相关的内存地址(这就是为什么你不能取得它们的地址或者得到一个指向它们的指针)。

But, like I said, modern compilers are really good at producing optimal code, using registers whenever possible regardless of whether or not you specified the `register` keyword. Not only that, but the spec allows them to just treat it as if you'd typed `auto`, if they want. So no guarantees.

> 但是，正如我所说，现代编译器在生成最优代码方面非常出色，无论您是否指定了 `register` 关键字，都可以尽可能使用寄存器。不仅如此，规范还允许它们就好像您输入了 `auto` 一样，如果他们愿意的话。所以没有保证。

### [16.2.5] `_Thread_local` {#thread_local number="16.2.5"}

When you're using multiple threads and you have some variables in either global or `static` block scope, this is a way to make sure that each thread gets its own copy of the variable. This'll help you avoid race conditions and threads stepping on each other's toes.

> 当你使用多个线程，并且有一些变量在全局或静态块作用域中时，这是一种确保每个线程都有自己的变量副本的方法。这将帮助你避免竞争条件和线程互相干扰。

If you're in block scope, you have to use this along with either `extern` or `static`.

> 如果你处于块作用域，你必须使用 `extern` 或 `static` 之一来使用它。

Also, if you include `<threads.h>`, you can use the rather more palatable `thread_local` as an alias for the uglier `_Thread_local`.

> 如果你包含 `<threads.h>`，你可以使用更易用的 `thread_local` 作为 `_Thread_local` 的别名。

More information can be found in the [Threads section](#thread-local).

# [17] Multifile Projects {#multifile-projects number="17"}

So far we've been looking at toy programs that for the most part fit in a single file. But complex C programs are made up of many files that are all compiled and linked together into a single executable.

> 到目前为止，我们一直在研究大多数可以放在一个文件中的玩具程序。但是复杂的 C 程序由许多文件组成，这些文件都被编译和链接在一起，形成一个可执行文件。

In this chapter we'll check out some of the common patterns and practices for putting together larger projects.

> 在本章中，我们将检查一些组建大型项目的常见模式和实践。

## [17.1] Includes and Function Prototypes {#includes-func-protos number="17.1"}

A really common situation is that some of your functions are defined in one file, and you want to call them from another.

> 一个非常常见的情况是，您的一些函数定义在一个文件中，您想从另一个文件中调用它们。

This actually works out of the box with a warning... let's first try it and then look at the right way to fix the warning.

> 这实际上可以直接使用，但会有警告... 我们先尝试一下，然后再看看如何正确修复警告。

For these examples, we'll put the filename as the first comment in the source.

> 对于这些例子，我们将文件名放在源代码的第一个注释中。

To compile them, you'll need to specify all the sources on the command line:

> 编译它们，你需要在命令行中指定所有的源：

::: {#cb289 .sourceCode}

```zsh
# output file   source files
#     v            v
#   |----| |---------|
gcc -o foo foo.c bar.c
```

:::

In that examples, `foo.c` and `bar.c` get built into the executable named `foo`.

> 在那个例子中，`foo.c` 和 `bar.c` 被编译成可执行文件 `foo`。

So let's take a look at the source file `bar.c`:

::: {#cb290 .sourceCode}

```c
// File bar.c

int add(int x, int y)
{
    return x + y;
}
```

:::

And the file `foo.c` with main in it:

::: {#cb291 .sourceCode}

```c
// File foo.c

#include <stdio.h>

int main(void)
{
    printf("%d\n", add(2, 3));  // 5!
}
```

:::

See how from `main()` we call `add()`---but `add()` is in a completely different source file! It's in `bar.c`, while the call to it is in `foo.c`!

> 看看我们如何从 `main()` 调用 `add()`---但是 `add()` 在一个完全不同的源文件中！它在 `bar.c` 中，而对它的调用在 `foo.c` 中！

If we build this with:

::: {#cb292 .sourceCode}

```zsh
gcc -o foo foo.c bar.c
```

:::

we get this error:

::: {#cb293 .sourceCode}

```{.sourceCode .default}
error: implicit declaration of function 'add' is invalid in C99
```

:::

(Or you might get a warning. Which you should not ignore. Never ignore warnings in C; address them all.)

> 你可能会得到一个警告，你不应该忽略它。在 C 语言中永远不要忽略警告，要处理好所有警告。

If you recall from the [section on prototypes](#prototypes), implicit declarations are banned in modern C and there's no legitimate reason to introduce them into new code. We should fix it.

> 如果您回想起[原型部分](#prototypes)，现代 C 中禁止隐式声明，没有合法的理由将它们引入新代码。我们应该修复它。

What `implicit declaration` means is that we're using a function, namely `add()` in this case, without letting C know anything about it ahead of time. C wants to know what it returns, what types it takes as arguments, and things such as that.

> 所谓的隐式声明，就是我们在没有提前告诉 C 语言的情况下，使用一个函数，比如这里的 add()函数。C 语言需要知道它的返回值、参数类型等等。

We saw how to fix that earlier with a _function prototype_. Indeed, if we add one of those to `foo.c` before we make the call, everything works well:

> 我们之前看到如何通过一个函数原型来修复它。的确，如果我们在调用之前在 foo.c 中添加一个，一切都会很好：

::: {#cb294 .sourceCode}

```c
// File foo.c

#include <stdio.h>

int add(int, int);  // Add the prototype

int main(void)
{
    printf("%d\n", add(2, 3));  // 5!
}
```

:::

No more error!

But that's a pain---needing to type in the prototype every time you want to use a function. I mean, we used `printf()` right there and didn't need to type in a prototype; what gives?

> 但是这太麻烦了---每次想要使用一个函数都需要输入原型。我的意思是，我们刚才使用了 `printf()` 而不需要输入原型；这是怎么回事？

If you remember from what back with `hello.c` at the beginning of the book, _we actually did include the prototype for `printf()`_! It's in the file `stdio.h`! And we included that with `#include`!

> 如果你还记得书开头的 `hello.c`，我们实际上已经包含了 `printf()` 的原型！它在 `stdio.h` 文件中！我们用 `#include` 包含了它！

Can we do the same with our `add()` function? Make a prototype for it and put it in a header file?

> 我们可以用我们的 `add()` 函数做同样的事情吗？为它创建一个原型，并把它放在头文件中吗？

Sure!

Header files in C have a `.h` extension by default. And they often, but not always, have the same name as their corresponding `.c` file. So let's make a `bar.h` file for our `bar.c` file, and we'll stick the prototype in it:

> C 语言的头文件默认使用 `.h` 扩展名。它们通常(但不一定)和它们对应的 `.c` 文件有相同的名字。因此，让我们为我们的 `bar.c` 文件创建一个 `bar.h` 文件，并将原型放在其中：

::: {#cb295 .sourceCode}

```c
// File bar.h

int add(int, int);
```

:::

And now let's modify `foo.c` to include that file. Assuming it's in the same directory, we include it inside double quotes (as opposed to angle brackets):

> 现在让我们修改 `foo.c` 来包含该文件。假设它在同一个目录中，我们用双引号(而不是尖括号)将其包含在内：

::: {#cb296 .sourceCode}

```c
// File foo.c

#include <stdio.h>

#include "bar.h"  // Include from current directory

int main(void)
{
    printf("%d\n", add(2, 3));  // 5!
}
```

:::

Notice how we don't have the prototype in `foo.c` anymore---we included it from `bar.h`. Now _any_ file that wants that `add()` functionality can just `#include "bar.h"` to get it, and you don't need to worry about typing in the function prototype.

> 注意我们不再在 `foo.c` 中有原型了---我们从 `bar.h` 中包含了它。现在，任何想要 `add()` 功能的文件都可以通过 `#include "bar.h"` 来获取它，你不需要担心输入函数原型。

As you might have guessed, `#include` literally includes the named file _right there_ in your source code, just as if you'd typed it in.

> 你可能已经猜到了，`#include` 字面上就是将指定的文件直接插入到源代码中，就像你键入它一样。

And building and running:

::: {#cb297 .sourceCode}

```zsh
./foo
5
```

:::

Indeed, we get the result of [\\(2+3\\)]{.math .inline}! Yay!

But don't crack open your drink of choice quite yet. We're almost there! There's just one more piece of boilerplate we have to add.

> 但是现在还不要打开你喜欢的饮料。我们快到了！只有一个模板要添加。

## [17.2] Dealing with Repeated Includes {#dealing-with-repeated-includes number="17.2"}

It's not uncommon that a header file will itself `#include` other headers needed for the functionality of its corresponding C files. I mean, why not?

> 不是不常见的，一个头文件会自身 `#include` 其他头文件以支持它对应的 C 文件的功能。我的意思是，为什么不呢？

And it could be that you have a header `#include` d multiple times from different places. Maybe that's no problem, but maybe it would cause compiler errors. And we can't control how many places `#include` it!

> 可能你从不同的地方多次包含了头文件 `#include`，也许没有问题，但也可能会导致编译器错误。而我们无法控制有多少地方会 `#include` 它！

Even, worse we might get into a crazy situation where header `a.h` includes header `b.h`, and `b.h` includes `a.h`! It's an `#include` infinite cycle!

> 即使更糟糕的是，我们可能会陷入一个疯狂的情况，其中头文件 a.h 包含头文件 b.h，而 b.h 又包含 a.h！这是一个无限循环的#include！

Trying to build such a thing gives an error:

::: {#cb298 .sourceCode}

```{.sourceCode .default}
error: #include nested depth 200 exceeds maximum of 200
```

:::

What we need to do is make it so that if a file gets included once, subsequent `#include` s for that file are ignored.

> 我们需要做的是，如果一个文件被包含一次，那么后续对该文件的 `#include` 就会被忽略。

**The stuff that we're about to do is so common that you should just automatically do it every time you make a header file!**

> 我们即将要做的事情是如此常见，以至于每次你创建一个头文件时你都应该自动去做！

And the common way to do this is with a preprocessor variable that we set the first time we `#include` the file. And then for subsequent `#include` s, we first check to make sure that the variable isn't defined.

> 常见的做法是使用一个预处理器变量，我们在第一次 `#include` 文件时设置它。然后，对于后续的 `#include`，我们首先确保该变量未定义。

For that variable name, it's super common to take the name of the header file, like `bar.h`, make it uppercase, and replace the period with an underscore: `BAR_H`.

> 对于这个变量名，最常见的做法是把头文件的名字，比如 `bar.h`，改为大写，并把句号替换为下划线：`BAR_H`。

So put a check at the very, very top of the file where you see if it's already been included, and effectively comment the whole thing out if it has.

> 在文件顶部检查一下是否已经包含，如果已经包含，就把整个东西注释掉。

(Don't put a leading underscore (because a leading underscore followed by a capital letter is reserved) or a double leading underscore (because that's also reserved.))

> 不要加入前导下划线(因为前导下划线后面跟着大写字母是保留的)或双前导下划线(因为那也是保留的)。

::: {#cb299 .sourceCode}

```c
#ifndef BAR_H   // If BAR_H isn't defined...
#define BAR_H   // Define it (with no particular value)

// File bar.h

int add(int, int);

#endif          // End of the #ifndef BAR_H
```

:::

This will effectively cause the header file to be included only a single time, no matter how many places try to `#include` it.

> 这有效地意味着，无论有多少地方尝试 `#include` 它，头文件只会被包含一次。

## [17.3] `static` and `extern` {#static-and-extern number="17.3"}

When it comes to multifile projects, you can make sure file-scope variables and functions are _not_ visible from other source files with the `static` keyword.

> 当涉及多文件项目时，可以使用 `static` 关键字确保文件范围变量和函数不能从其他源文件中可见。

And you can refer to objects in other files with `extern`.

For more info, check out the sections in the book on the [`static`](#static) and [`extern`](#extern) storage-class specifiers.

> 更多信息，请查看书中有关[“静态”](#static)和[“extern”](#extern)存储类说明符的部分。

## [17.4] Compiling with Object Files {#compiling-with-object-files number="17.4"}

This isn't part of the spec, but it's 99.999% common in the C world.

You can compile C files into an intermediate representation called _object files_. These are compiled machine code that hasn't been put into an executable yet.

> 你可以将 C 文件编译成一种叫做_对象文件_的中间表示。这些是编译好的机器代码，但尚未编译成可执行文件。

Object files in Windows have a `.OBJ` extension; in Unix-likes, they're `.o`.

> 在 Windows 中，对象文件的扩展名为 `.OBJ`；而在类 Unix 系统中，它们的扩展名为 `.o`。

In gcc, we can build some like this, with the `-c` (compile only!) flag:

::: {#cb300 .sourceCode}

```zsh
gcc -c foo.c     # produces foo.o
gcc -c bar.c     # produces bar.o
```

:::

And then we can _link_ those together into a single executable:

::: {#cb301 .sourceCode}

```zsh
gcc -o foo foo.o bar.o
```

:::

_Voila_, we've produced an executable `foo` from the two object files.

But you're thinking, why bother? Can't we just:

::: {#cb302 .sourceCode}

```zsh
gcc -o foo foo.c bar.c
```

:::

and kill two [boids](https://en.wikipedia.org/wiki/Boids)[^117^] with one stone?

> 用一块石头杀死两只鸟？

For little programs, that's fine. I do it all the time.

But for larger programs, we can take advantage of the fact that compiling from source to object files is relatively slow, and linking together a bunch of object files is relatively fast.

> 但是对于更大的程序，我们可以利用从源代码编译到对象文件相对较慢，而将一堆对象文件链接在一起相对较快的事实。

This really shows with the `make` utility that only rebuilds sources that are newer than their outputs.

> 这真的表明，只有 `make` 实用程序才能重新构建比其输出更新的源。

Let's say you had a thousand C files. You could compile them all to object files to start (slowly) and then combine all those object files into an executable (fast).

> 假设你有一千个 C 文件。你可以先把它们编译成对象文件(慢慢地)，然后把所有这些对象文件合并成一个可执行文件(快速)。

Now say you modified just one of those C source files---here's the magic: _you only have to rebuild that one object file for that source file_! And then you rebuild the executable (fast). All the other C files don't have to be touched.

> 现在说你只修改了其中一个 C 源文件---这就是魔法：_你只需要重新构建那个源文件的一个对象文件_！然后你重新构建可执行文件(快速)。其他所有的 C 文件都不需要触碰。

In other words, by only rebuilding the object files we need to, we cut down on compilation times radically. (Unless of course you're doing a "clean" build, in which case all the object files have to be created.)

> 另一种说法，只重新构建我们需要的对象文件，我们可以大大减少编译时间。(除非你在做一个“清理”构建，在这种情况下，所有的对象文件都必须被创建。)

# [18] The Outside Environment {#the-outside-environment number="18"}

When you run a program, it's actually you talking to the shell, saying, "Hey, please run this thing." And the shell says, "Sure," and then tells the operating system, "Hey, could you please make a new process and run this thing?" And if all goes well, the OS complies and your program runs.

> 当你运行一个程序时，实际上你是在和壳程序对话，说：“嘿，请运行这个东西。”然后壳程序说：“当然可以”，然后告诉操作系统：“嘿，你能不能创建一个新的进程并运行这个东西？”如果一切顺利，操作系统就会照做，你的程序就会运行起来。

But there's a whole world outside your program in the shell that can be interacted with from within C. We'll look at a few of those in this chapter.

> 但是，在 C 中可以从外部 shell 中与之交互的整个世界。我们将在本章中看到其中的一些。

## [18.1] Command Line Arguments {#command-line-arguments number="18.1"}

Many command line utilities accept _command line arguments_. For example, if we want to see all files that end in `.txt`, we can type something like this on a Unix-like system:

> 在类 Unix 系统上，许多命令行实用程序都接受命令行参数。例如，如果我们想查看所有以 `.txt` 结尾的文件，我们可以输入类似这样的内容：

::: {#cb303 .sourceCode}

```zsh
ls *.txt
```

:::

(or `dir` instead of `ls` on a Windows system).

In this case, the command is `ls`, but it arguments are all all files that end with `.txt`[^118^].

> 在这种情况下，命令是 `ls`，但它的参数都是以 `.txt` 结尾的所有文件[^118^] (#fn118) {#fnref118 .footnote-ref role="doc-noteref"}。

So how can we see what is passed into program from the command line?

Say we have a program called `add` that adds all numbers passed on the command line and prints the result:

> 我们有一个叫做“add”的程序，它可以把命令行传递的所有数字相加，并打印出结果：

::: {#cb304 .sourceCode}

```zsh
./add 10 30 5
45
```

:::

That's gonna pay the bills for sure!

But seriously, this is a great tool for seeing how to get those arguments from the command line and break them down.

> 但是说真的，这是一个很棒的工具，可以看到如何从命令行获取参数并将其分解。

First, let's see how to get them at all. For this, we're going to need a new `main()`!

> 首先，让我们看看如何获得它们。为此，我们需要一个新的 `main()`！

Here's a program that prints out all the command line arguments. For example, if we name the executable `foo`, we can run it like this:

> 这是一个程序，可以打印出所有命令行参数。例如，如果我们将可执行文件命名为 `foo`，我们可以像这样运行它：

::: {#cb305 .sourceCode}

```zsh
./foo i like turtles
```

:::

and we'll see this output:

::: {#cb306 .sourceCode}

```{.sourceCode .default}
arg 0: ./foo
arg 1: i
arg 2: like
arg 3: turtles
```

:::

It's a little weird, because the zeroth argument is the name of the executable, itself. But that's just something to get used to. The arguments themselves follow directly.

> 这有点奇怪，因为第零个参数是可执行文件本身的名称。但这只是一种习惯。参数本身直接接着。

Source:

::: {#cb307 .sourceCode}

```c
#include <stdio.h>

int main(int argc, char *argv[])
{
    for (int i = 0; i < argc; i++) {
        printf("arg %d: %s\n", i, argv[i]);
    }
}
```

:::

Whoa! What's going on with the `main()` function signature? What's `argc` and `argv`[^119^] (pronounced _arg-cee_ and _arg-vee_)?

> 哇！`main()` 函数签名怎么了？`argc` 和 `argv`[^119^](发音为_arg-cee_和_arg-vee_)是什么？

Let's start with the easy one first: `argc`. This is the _argument count_, including the program name, itself. If you think of all the arguments as an array of strings, which is exactly what they are, then you can think of `argc` as the length of that array, which is exactly what it is.

> 让我们先从简单的开始：`argc`。这是参数计数，包括程序本身的名称。如果把所有参数都看作一个字符串数组，这正是它们的样子，那么你可以把 `argc` 看作这个数组的长度，这正是它的意义。

And so what we're doing in that loop is going through all the `argv` s and printing them out one at a time, so for a given input:

> 我们在循环中所做的就是遍历所有的 argv，并逐个打印出来，因此对于给定的输入：

::: {#cb308 .sourceCode}

```zsh
./foo i like turtles
```

:::

we get a corresponding output:

::: {#cb309 .sourceCode}

```{.sourceCode .default}
arg 0: ./foo
arg 1: i
arg 2: like
arg 3: turtles
```

:::

With that in mind, we should be good to go with our adder program.

Our plan:

- Look at all the command line arguments (past `argv[0]`, the program name)
- Convert them to integers
- Add them to a running total
- Print the result

Let's get to it!

::: {#cb310 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
    int total = 0;

    for (int i = 1; i < argc; i++) {  // Start at 1, the first argument
        int value = atoi(argv[i]);    // Use strtol() for better error handling

        total += value;
    }

    printf("%d\n", total);
}
```

:::

Sample runs:

::: {#cb311 .sourceCode}

```zsh
$ ./add
0
$ ./add 1
1
$ ./add 1 2
3
$ ./add 1 2 3
6
$ ./add 1 2 3 4
10
```

:::

Of course, it might puke if you pass in a non-integer, but hardening against that is left as an exercise to the reader.

> 当然，如果你传入一个非整数，它可能会吐，但是防止这种情况的方法留给读者自行练习。

### [18.1.1] The Last `argv` is `NULL` {#the-last-argv-is-null number="18.1.1"}

One bit of fun trivia about `argv` is that after the last string is a pointer to `NULL`.

> 关于 `argv` 的一个有趣的趣闻是，在最后一个字符串之后是一个指向 `NULL` 的指针。

That is:

::: {#cb312 .sourceCode}

```c
argv[argc] == NULL
```

:::

is always true!

This might seem pointless, but it turns out to be useful in a couple places; we'll take a look at one of those right now.

> 这可能看起来毫无意义，但实际上在一些地方是有用的；我们现在就来看一个例子。

### [18.1.2] The Alternate: `char **argv` {#the-alternate-char-argv number="18.1.2"}

Remember that when you call a function, C doesn't differentiate between array notation and pointer notation in the function signature.

> 记住，当你调用一个函数时，C 在函数签名中不区分数组表示法和指针表示法。

That is, these are the same:

::: {#cb313 .sourceCode}

```c
void foo(char a[])
void foo(char *a)
```

:::

Now, it's been convenient to think of `argv` as an array of strings, i.e. an array of `char*` s, so this made sense:

> 现在，把 `argv` 想象成一个字符串数组，即 `char*` 数组，这样就有意义了：

::: {#cb314 .sourceCode}

```c
int main(int argc, char *argv[])
```

:::

but because of the equivalence, you could also write:

::: {#cb315 .sourceCode}

```c
int main(int argc, char **argv)
```

:::

Yeah, that's a pointer to a pointer, all right! If it makes it easier, think of it as a pointer to a string. But really, it's a pointer to a value that points to a `char`.

> 哦，没错，那是一个指针指向另一个指针！如果这样更容易理解，可以把它想象成一个指向字符串的指针。但实际上，它是一个指向指向字符的值的指针。

Also recall that these are equivalent:

::: {#cb316 .sourceCode}

```c
argv[i]
*(argv + i)
```

:::

which means you can do pointer arithmetic on `argv`.

So an alternate way to consume the command line arguments might be to just walk along the `argv` array by bumping up a pointer until we hit that `NULL` at the end.

> 另一种消费命令行参数的方法可能是通过提升指针来遍历 `argv` 数组，直到遇到末尾的 `NULL`。

Let's modify our adder to do that:

::: {#cb317 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
    int total = 0;

    // Cute trick to get the compiler to stop warning about the
    // unused variable argc:
    (void)argc;

    for (char **p = argv + 1; *p != NULL; p++) {
        int value = atoi(*p);  // Use strtol() for better error handling

        total += value;
    }

    printf("%d\n", total);
}
```

:::

Personally, I use array notation to access `argv`, but have seen this style floating around, as well.

> 我个人使用数组符号来访问 argv，但也看到这种风格的代码。

### [18.1.3] Fun Facts {#fun-facts number="18.1.3"}

Just a few more things about `argc` and `argv`.

- Some environments might not set `argv[0]` to the program name. If it's not available, `argv[0]` will be an empty string. I've never seen this happen.

> 有些环境可能不会将 `argv[0]` 设置为程序名称。如果不可用，`argv[0]` 将是一个空字符串。我从未见过这种情况。

- The spec is actually pretty liberal with what an implementation can do with `argv` and where those values come from. But every system I've been on works the same way, as we've discussed in this section.

> 实际上，规范对于实现中可以对 `argv` 做什么以及这些值来自何处比较宽松。但是每个系统我都使用过，都是我们在本节中讨论过的方式。

- You can modify `argc`, `argv`, or any of the strings that `argv` points to. (Just don't make those strings longer than they already are!)

> 你可以修改 argc、argv 或 argv 指向的任何字符串(只要不要让这些字符串比原来长！)

- On some Unix-like systems, modifying the string `argv[0]` results in the output of `ps` changing[^120^].

> 在某些类 Unix 系统上，修改字符串 `argv[0]` 会导致 `ps` 的输出发生变化[^120^]。

Normally, if you have a program called `foo` that you've run with `./foo`, you might see this in the output of `ps`:

> 通常，如果你有一个程序叫做“foo”，你可以通过“./foo”来运行它，那么在“ps”的输出中你可能会看到：

::: {#cb318 .sourceCode}

```{.sourceCode .default}
 4078 tty1     S      0:00 ./foo
```

:::

But if you modify `argv[0]` like so, being careful that the new string `"Hi!  "` is the same length as the old one `"./foo"`:

> 如果你像这样修改 `argv[0]`，要确保新的字符串 `"Hi！"` 和旧的字符串 `"./foo"` 长度一致：

::: {#cb319 .sourceCode}

```c
strcpy(argv[0], "Hi!  ");
```

:::

and then run `ps` while the program `./foo` is still executing, we'll see this instead:

> 然后当程序 `./foo` 正在执行时，运行 `ps`，我们会看到这样的结果：

::: {#cb320 .sourceCode}

```{.sourceCode .default}
 4079 tty1     S      0:00 Hi!
```

:::

This behavior is not in the spec and is highly system-dependent.

## [18.2] Exit Status {#exit-status number="18.2"}

Did you notice that the function signatures for `main()` have it returning type `int`? What's that all about? It has to do with a thing called the _exit status_, which is an integer that can be returned to the program that launched yours to let it know how things went.

> 你有注意到 `main()` 函数的签名有一个返回类型 `int` 吗？这是怎么回事？这与一个叫做_exit status_的东西有关，它是一个整数，可以返回给启动你的程序，让它知道事情如何进行。

Now, there are a number of ways a program can exit in C, including `return` ing from `main()`, or calling one of the `exit()` variants.

> 现在，C 语言中有多种程序退出的方式，包括从 main()中返回，或者调用其中一个 exit()变体。

All of these methods accept an `int` as an argument.

Side note: did you see that in basically all my examples, even though `main()` is supposed to return an `int`, I don't actually `return` anything? In any other function, this would be illegal, but there's a special case in C: if execution reaches the end of `main()` without finding a `return`, it automatically does a `return 0`.

> 边注：你有没有发现，在我的所有例子中，尽管 `main()` 应该返回一个 `int`，但我实际上没有 `return` 任何东西？在任何其他函数中，这将是非法的，但在 C 中有一个特殊情况：如果执行到 `main()` 的末尾而没有找到 `return`，它会自动执行 `return 0`。

But what does the `0` mean? What other numbers can we put there? And how are they used?

> 但是 0 代表什么意思？我们可以放入其他数字吗？它们又被用来做什么？

The spec is both clear and vague on the matter, as is common. Clear because it spells out what you can do, but vague in that it doesn't particularly limit it, either.

> 这件事情的规格既清晰又模糊，这是常见的情况。清晰的是它清楚地说明你可以做什么，但模糊的是它并没有特别限制它。

Nothing for it but to _forge ahead_ and figure it out!

Let's get [Inception](https://en.wikipedia.org/wiki/Inception)[^121^] for a second: turns out that when you run your program, _you're running it from another program_.

> 让我们来看看 [Inception](https://en.wikipedia.org/wiki/Inception)[^121^]一下：原来当你运行你的程序时，你是从另一个程序中运行它的。

Usually this other program is some kind of [shell](https://en.wikipedia.org/wiki/Shell_(computing))[^122^] that doesn't do much on its own except launch other programs.

> 通常，这个其他程序是一种 [shell](https://en.wikipedia.org/wiki/Shell_(computing))[^122^]，除了启动其他程序外，本身并不能做太多的事情。

But this is a multi-phase process, especially visible in command-line shells:

> 但这是一个多阶段的过程，尤其是在命令行 shell 中更加明显：

1. The shell launches your program
2. The shell typically goes to sleep (for command-line shells)
3. Your program runs
4. Your program terminates
5. The shell wakes up and waits for another command

Now, there's a little piece of communication that takes place between steps 4 and 5: the program can return a _status value_ that the shell can interrogate. Typically, this value is used to indicate the success or failure of your program, and, if a failure, what type of failure.

> 现在，在第 4 步和第 5 步之间会发生一点点的通信：程序可以返回一个_状态值_，shell 可以查询它。通常，这个值用来表示程序的成功或失败，如果失败，是什么类型的失败。

This value is what we've been `return` ing from `main()`. That's the status.

> 这个值就是我们从 main()函数中返回的。这就是状态。

Now, the C spec allows for two different status values, which have macro names defined in `<stdlib.h>`:

> 现在，C 规范允许两个不同的状态值，它们在 <stdlib.h> 中定义了宏名称：

Status Description

---

`EXIT_SUCCESS` or `0` Program terminated successfully.
`EXIT_FAILURE` Program terminated with an error.

Let's write a short program that multiplies two numbers from the command line. We'll require that you specify exactly two values. If you don't, we'll print an error message, and exit with an error status.

> 让我们编写一个简短的程序，从命令行中乘以两个数字。我们要求您指定两个值。如果没有，我们将打印一条错误消息，并以错误状态退出。

::: {#cb321 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
    if (argc != 3) {
        printf("usage: mult x y\n");
        return EXIT_FAILURE;   // Indicate to shell that it didn't work
    }

    printf("%d\n", atoi(argv[1]) * atoi(argv[2]));

    return 0;  // same as EXIT_SUCCESS, everything was good.
}
```

:::

Now if we try to run this, we get the expected effect until we specify exactly the right number of command-line arguments:

> 现在，如果我们尝试运行它，我们会得到预期的效果，直到我们指定正确数量的命令行参数：

::: {#cb322 .sourceCode}

```zsh
$ ./mult
usage: mult x y

$ ./mult 3 4 5
usage: mult x y

$ ./mult 3 4
12
```

:::

But that doesn't really show the exit status that we returned, does it? We can get the shell to print it out, though. Assuming you're running Bash or another POSIX shell, you can use `echo $?` to see it[^123^].

> 但这并不能真正显示我们返回的退出状态，是吗？不过，我们可以让 shell 打印出来。假设您正在运行 Bash 或其他 POSIX shell，您可以使用 `echo $?` 来查看它[^123^]。

Let's try:

::: {#cb323 .sourceCode}

```zsh
$ ./mult
usage: mult x y
$ echo $?
1

$ ./mult 3 4 5
usage: mult x y
$ echo $?
1

$ ./mult 3 4
12
$ echo $?
0
```

:::

Interesting! We see that on my system, `EXIT_FAILURE` is `1`. The spec doesn't spell this out, so it could be any number. But try it; it's probably `1` on your system, too.

> 有趣！我们可以看到在我的系统上，`EXIT_FAILURE` 是 `1`。规范没有明确说明，所以它可以是任何数字。但是试试看，在你的系统上它可能也是 `1`。

### [18.2.1] Other Exit Status Values {#other-exit-status-values number="18.2.1"}

The status `0` most definitely means success, but what about all the other integers, even negative ones?

> 状态 `0` 绝对意味着成功，但是其他整数，甚至是负数又会怎样呢？

Here we're going off the C spec and into Unix land. In general, while `0` means success, a positive non-zero number means failure. So you can only have one type of success, and multiple types of failure. Bash says the exit code should be between 0 and 255, though a number of codes are reserved.

> 我们现在离开 C 语言规范，进入 Unix 领域。一般来说，当 `0` 表示成功时，正数非零表示失败。因此，只能有一种成功，多种失败。Bash 说退出代码应该介于 0 到 255 之间，尽管有一些代码是保留的。

In short, if you want to indicate different error exit statuses in a Unix environment, you can start with `1` and work your way up.

> 简而言之，如果你想在 Unix 环境中指示不同的错误退出状态，你可以从 `1` 开始，一步一步地完成。

On Linux, if you try any code outside the range 0-255, it will bitwise AND the code with `0xff`, effectively clamping it to that range.

> 在 Linux 上，如果您尝试超出 0-255 范围的任何代码，它将使用“0xff”进行位运算，有效地将其钳制在该范围内。

You can script the shell to later use these status codes to make decisions about what to do next.

> 你可以编写脚本来控制 shell，以便以后使用这些状态码来做出关于下一步该做什么的决定。

## [18.3] Environment Variables {#env-var number="18.3"}

Before I get into this, I need to warn you that C doesn't specify what an environment variable is. So I'm going to describe the environment variable system that works on every major platform I'm aware of.

> 在我开始讨论之前，我需要警告你 C 不指定环境变量是什么。因此，我将描述我知道的每个主要平台上的环境变量系统。

Basically, the environment is the program that's going to run your program, e.g. the bash shell. And it might have some bash variables defined. In case you didn't know, the shell can make its own variables. Each shell is different, but in bash you can just type `set` and it'll show you all of them.

> 基本上，环境是运行你的程序的程序，例如 bash shell。它可能定义了一些 bash 变量。如果你不知道，shell 可以创建自己的变量。每个 shell 都不同，但是在 bash 中，你可以输入 `set`，它会显示所有变量。

Here's an excerpt from the 61 variables that are defined in my bash shell:

> 以下是我的 bash shell 中定义的 61 个变量的摘录：

::: {#cb324 .sourceCode}

```{.sourceCode .default}
HISTFILE=/home/beej/.bash_history
HISTFILESIZE=500
HISTSIZE=500
HOME=/home/beej
HOSTNAME=FBILAPTOP
HOSTTYPE=x86_64
IFS=$' \t\n'
```

:::

Notice they are in the form of key/value pairs. For example, one key is `HOSTTYPE` and its value is `x86_64`. From a C perspective, all values are strings, even if they're numbers[^124^].

> 注意它们是以键/值对的形式出现的。例如，一个键是 `HOSTTYPE`，它的值是 `x86_64`。从 C 的角度来看，所有的值都是字符串，即使它们是数字[^124^]。

So, _anyway_! Long story short, it's possible to get these values from inside your C program.

> 所以，无论如何！简而言之，可以从你的 C 程序内部获取这些值。

Let's write a program that uses the standard `getenv()` function to look up a value that you set in the shell.

> 让我们编写一个使用标准 `getenv()` 函数查找您在 shell 中设置的值的程序。

`getenv()` will return a pointer to the value string, or else `NULL` if the environment variable doesn't exist.

::: {#cb325 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    char *val = getenv("FROTZ");  // Try to get the value

    // Check to make sure it exists
    if (val == NULL) {
        printf("Cannot find the FROTZ environment variable\n");
        return EXIT_FAILURE;
    }

    printf("Value: %s\n", val);
}
```

:::

If I run this directly, I get this:

::: {#cb326 .sourceCode}

```zsh
$ ./foo
Cannot find the FROTZ environment variable
```

:::

which makes sense, since I haven't set it yet.

In bash, I can set it to something with[^125^]:

> 在 Bash 中，我可以用 [^125^]来设置它：

::: {#cb327 .sourceCode}

```zsh
$ export FROTZ="C is awesome!"
```

:::

Then if I run it, I get:

::: {#cb328 .sourceCode}

```zsh
$ ./foo
Value: C is awesome!
```

:::

In this way, you can set up data in environment variables, and you can get it in your C code and modify your behavior accordingly.

> 在这种方式中，您可以在环境变量中设置数据，并可以在 C 代码中获取它，从而更改您的行为。

### [18.3.1] Setting Environment Variables {#setting-environment-variables number="18.3.1"}

This isn't standard, but a lot of systems provide ways to set environment variables.

> 这不是标准的，但很多系统都提供设置环境变量的方法。

If on a Unix-like, look up the documentation for `putenv()`, `setenv()`, and `unsetenv()`. On Windows, see `_putenv()`.

> 如果是类 Unix 系统，查看 `putenv()`、`setenv()` 和 `unsetenv()` 的文档。在 Windows 上，参见 `_putenv()`。

### [18.3.2] Unix-like Alternative Environment Variables {#unix-like-alternative-environment-variables number="18.3.2"}

If you're on a Unix-like system, odds are you have another couple ways of getting access to environment variables. Note that although the spec points this out as a common extension, it's not truly part of the C standard. It is, however, part of the POSIX standard.

> 如果你使用类 Unix 系统，你可能有另外几种方式访问环境变量。请注意，尽管规范指出这是一个常见的扩展，它并不是 C 标准的一部分。但它是 POSIX 标准的一部分。

One of these is a variable called `environ` that must be declared like so:

> 一个变量叫做 `environ`，必须像这样声明：

::: {#cb329 .sourceCode}

```c
extern char **environ;
```

:::

It's an array of strings terminated with a `NULL` pointer.

You should declare it yourself before you use it, or you might find it in the non-standard `<unistd.h>` header file.

> 你使用它之前应该自己声明它，否则你可能会在非标准的 <unistd.h> 头文件中找到它。

Each string is in the form `"key=value"` so you'll have to split it and parse it yourself if you want to get the keys and values out.

> 每个字符串都是 `"key=value"` 的形式，所以如果你想获取键和值，你需要自己拆分和解析它们。

Here's an example of looping through and printing out the environment variables a couple different ways:

> 这里有几种不同的方式循环并打印出环境变量的例子：

::: {#cb330 .sourceCode}

```c
#include <stdio.h>

extern char **environ;  // MUST be extern AND named "environ"

int main(void)
{
    for (char **p = environ; *p != NULL; p++) {
        printf("%s\n", *p);
    }

    // Or you could do this:
    for (int i = 0; environ[i] != NULL; i++) {
        printf("%s\n", environ[i]);
    }
}
```

:::

For a bunch of output that looks like this:

::: {#cb331 .sourceCode}

```{.sourceCode .default}
SHELL=/bin/bash
COLORTERM=truecolor
TERM_PROGRAM_VERSION=1.53.2
LOGNAME=beej
HOME=/home/beej
... etc ...
```

:::

Use `getenv()` if at all possible because it's more portable. But if you have to iterate over environment variables, using `environ` might be the way to go.

> 尽量使用 `getenv()`，因为它更具可移植性。但如果你必须遍历环境变量，使用 `environ` 可能是最佳方式。

Another non-standard way to get the environment variables is as a parameter to `main()`. It works much the same way, but you avoid needing to add your `extern` `environ` variable. [Not even the POSIX spec supports this](https://pubs.opengroup.org/onlinepubs/9699919799/functions/exec.html)[^126^] as far as I can tell, but it's common in Unix land.

> 另一种非标准的方法来获取环境变量是作为 `main()` 的参数。它的工作原理大致相同，但是您可以避免添加 `extern` `environ` 变量。[据我所知，即使 POSIX 规范也不支持这一点](https://pubs.opengroup.org/onlinepubs/9699919799/functions/exec.html)[^126^]，但在 Unix 领域很常见。

::: {#cb332 .sourceCode}

```c
#include <stdio.h>

int main(int argc, char **argv, char **env)  // <-- env!
{
    (void)argc; (void)argv;  // Suppress unused warnings

    for (char **p = env; *p != NULL; p++) {
        printf("%s\n", *p);
    }

    // Or you could do this:
    for (int i = 0; env[i] != NULL; i++) {
        printf("%s\n", env[i]);
    }
}
```

:::

Just like using `environ` but _even less portable_. It's good to have goals.

> 就像使用 `environ` 一样，但更不可移植。有目标是好事。

# [19] The C Preprocessor {#the-c-preprocessor number="19"}

Before your program gets compiled, it actually runs through a phase called _preprocessing_. It's almost like there's a language _on top_ of the C language that runs first. And it outputs the C code, which then gets compiled.

> 在你的程序编译之前，它实际上会经历一个叫做预处理的阶段。就好像 C 语言之上有一种语言先运行一样。然后它会输出 C 代码，然后再进行编译。

We've already seen this to an extent with `#include`! That's the C Preprocessor! Where it sees that directive, it includes the named file right there, just as if you'd typed it in there. And _then_ the compiler builds the whole thing.

> 我们已经在 `#include` 中看到了这一点！那就是 C 预处理器！当它看到这个指令时，它就会把指定的文件包含进来，就好像你在那里输入了一样。然后编译器就会把整个东西构建起来。

But it turns out it's a lot more powerful than just being able to include things. You can define _macros_ that are substituted... and even macros that take arguments!

> 但事实证明，它比只能包括东西更强大。您可以定义_宏_，它们将被替换...甚至可以定义带参数的宏！

## [19.1] `#include` {#include number="19.1"}

Let's start with the one we've already seen a bunch. This is, of course, a way to include other sources in your source. Very commonly used with header files.

> 让我们从我们已经看到的一个开始。这当然是一种将其他来源包含在您的源中的方法。通常与头文件一起使用。

While the spec allows for all kinds of behavior with `#include`, we're going to take a more pragmatic approach and talk about the way it works on every system I've ever seen.

> 尽管规范允许使用 `#include` 实现各种行为，但我们将采取更加实用的方法，讨论我见过的每个系统上的工作方式。

We can split header files into two categories: system and local. Things that are built-in, like `stdio.h`, `stdlib.h`, `math.h`, and so on, you can include with angle brackets:

> 我们可以将头文件分为两类：系统和本地。像 `stdio.h`、`stdlib.h`、`math.h` 等内置的东西，可以用尖括号包含：

::: {#cb333 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
```

:::

The angle brackets tell C, "Hey, don't look in the current directory for this header file---look in the system-wide include directory instead."

> 括号告诉 C：“嘿，不要在当前目录中查找这个头文件---而是在系统范围内的 include 目录中查找。”

Which, of course, implies that there must be a way to include local files from the current directory. And there is: with double quotes:

> 当然，这意味着必须有一种方法可以从当前目录中包含本地文件。有的：用双引号：

::: {#cb334 .sourceCode}

```c
#include "myheader.h"
```

:::

Or you can very probably look in relative directories using forward slashes and dots, like this:

> 你也可以使用斜杠和点来查看相关目录，就像这样：

::: {#cb335 .sourceCode}

```c
#include "mydir/myheader.h"
#include "../someheader.py"
```

:::

Don't use a backslash (`\`) for your path separators in your `#include`! It's undefined behavior! Use forward slash (`/`) only, even on Windows.

> 不要在你的 `#include` 中使用反斜杠(`\`)作为路径分隔符！这是未定义的行为！无论是在 Windows 上，都只使用正斜杠(`/`)。

In summary, used angle brackets (`<` and `>`) for the system includes, and use double quotes (`"`) for your personal includes.

> 总之，使用尖括号(< 和 >)表示系统包含的内容，使用双引号(")表示你个人包含的内容。

## [19.2] Simple Macros {#simple-macros number="19.2"}

A _macro_ is an identifier that gets _expanded_ to another piece of code before the compiler even sees it. Think of it like a placeholder---when the preprocessor sees one of those identifiers, it replaces it with another value that you've defined.

> 一个宏是一个标识符，在编译器看到它之前，它会被展开成另一段代码。把它想象成一个占位符——当预处理器看到其中一个标识符时，它会用你定义的另一个值来替换它。

We do this with `#define` (often read "pound define"). Here's an example:

::: {#cb336 .sourceCode}

```c
#include <stdio.h>

#define HELLO "Hello, world"
#define PI 3.14159

int main(void)
{
    printf("%s, %f\n", HELLO, PI);
}
```

:::

On lines 3 and 4 we defined a couple macros. Wherever these appear elsewhere in the code (line 8), they'll be substituted with the defined values.

> 在第 3 行和第 4 行，我们定义了一对宏。无论这些在代码的其他地方(第 8 行)出现，它们都会被定义的值替换。

From the C compiler's perspective, it's exactly as if we'd written this, instead:

> 从 C 编译器的角度来看，这就好像我们写了这个一样：

::: {#cb337 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    printf("%s, %f\n", "Hello, world", 3.14159);
}
```

:::

See how `HELLO` was replaced with `"Hello, world"` and `PI` was replaced with `3.14159`? From the compiler's perspective, it's just like those values had appeared right there in the code.

> 看看"HELLO"被替换成了"Hello, world"，而"PI"被替换成了 3.14159？从编译器的角度来看，就好像这些值已经出现在代码中一样。

Note that the macros don't have a specific type, _per se_. Really all that happens is they get replaced wholesale with whatever they're `#define` d as. If the resulting C code is invalid, the compiler will puke.

> 注意宏本身并不具有特定的类型。只是它们会被完全替换成 `#define` 的内容。如果编译出的 C 代码是无效的，编译器就会报错。

You can also define a macro with no value:

::: {#cb338 .sourceCode}

```c
#define EXTRA_HAPPY
```

:::

in that case, the macro exists and is defined, but is defined to be nothing. So anyplace it occurs in the text will just be replaced with nothing. We'll see a use for this later.

> 在这种情况下，宏存在并且已经定义，但是定义为空。因此，文本中的任何位置都会被替换为空。稍后我们会看到它的用处。

It's conventional to write macro names in `ALL_CAPS` even though that's not technically required.

> 一般来说，尽管技术上不是必须的，但宏名称通常以 `全大写` 的形式书写。

Overall, this gives you a way to define constant values that are effectively global and can be used _any_ place. Even in those places where a `const` variable won't work, e.g. in `switch` `case` s and fixed array lengths.

> 总的来说，这给你提供了一种定义有效全局的常量值的方法，可以在_任何_地方使用。即使是在 `const` 变量无法工作的地方，例如 `switch` `case` 和固定数组长度。

That said, the debate rages online whether a typed `const` variable is better than `#define` macro in the general case.

> 提到这一点，争论仍在网上激烈，一般情况下，输入的 `const` 变量是否比 `#define` 宏更好。

It can also be used to replace or modify keywords, a concept completely foreign to `const`, though this practice should be used sparingly.

> 它也可以用来替换或修改关键字，这是一种对 `const` 完全陌生的概念，但应谨慎使用此种做法。

## [19.3] Conditional Compilation {#conditional-compilation number="19.3"}

It's possible to get the preprocessor to decide whether or not to present certain blocks of code to the compiler, or just remove them entirely before compilation.

> 可以让预处理器决定是否将某些代码块提交给编译器，或者在编译之前完全移除它们。

We do that by basically wrapping up the code in conditional blocks, similar to `if`-`else` statements.

> 我们通过将代码包裹在条件块中来实现，类似于 `if`-`else` 语句。

### [19.3.1] If Defined, `#ifdef` and `#endif` {#if-defined-ifdef-and-endif number="19.3.1"}

First of all, let's try to compile specific code depending on whether or not a macro is even defined.

> 首先，让我们根据宏是否定义，尝试编译特定的代码。

::: {#cb339 .sourceCode}

```c
#include <stdio.h>

#define EXTRA_HAPPY

int main(void)
{

#ifdef EXTRA_HAPPY
    printf("I'm extra happy!\n");
#endif

    printf("OK!\n");
}
```

:::

In that example, we define `EXTRA_HAPPY` (to be nothing, but it _is_ defined), then on line 8 we check to see if it is defined with an `#ifdef` directive. If it is defined, the subsequent code will be included up until the `#endif`.

> 在这个例子中，我们定义了 `EXTRA_HAPPY`(没有任何东西，但它_是_定义的)，然后在第 8 行我们使用 `#ifdef` 指令检查它是否定义。如果它被定义，随后的代码将被包括直到 `#endif`。

So because it is defined, the code will be included for compilation and the output will be:

> 因此，由于它已经定义，代码将被包含在编译中，输出将是：

::: {#cb340 .sourceCode}

```{.sourceCode .default}
I'm extra happy!
OK!
```

:::

If we were to comment out the `#define`, like so:

::: {#cb341 .sourceCode}

```c
//#define EXTRA_HAPPY
```

:::

then it wouldn't be defined, and the code wouldn't be included in compilation. And the output would just be:

> 如果没有定义，代码就不会被包含在编译中。输出就只有：

::: {#cb342 .sourceCode}

```{.sourceCode .default}
OK!
```

:::

It's important to remember that these decisions happen at compile time! The code actually gets compiled or removed depending on the condition. This is in contrast to a standard `if` statement that gets evaluated while the program is running.

> 重要的是要记住，这些决定是在编译时发生的！代码实际上会根据条件而编译或被删除。这与标准的 `if` 语句在程序运行时被评估形成了对比。

### [19.3.2] If Not Defined, `#ifndef` {#if-not-defined-ifndef number="19.3.2"}

There's also the negative sense of "if defined": "if not defined", or `#ifndef`. We could change the previous example to output different things based on whether or not something was defined:

> 也有“如果定义”的负面意义：“如果未定义”或“#ifndef”。我们可以根据是否定义某事物来更改先前的示例以输出不同的内容：

::: {#cb343 .sourceCode startfrom="8"}

```c
#ifdef EXTRA_HAPPY
    printf("I'm extra happy!\n");
#endif

#ifndef EXTRA_HAPPY
    printf("I'm just regular\n");
#endif
```

:::

We'll see a cleaner way to do that in the next section.

Tying it all back in to header files, we've seen how we can cause header files to only be included one time by wrapping them in preprocessor directives like this:

> 将它们都与头文件联系起来，我们已经看到我们如何通过用预处理器指令将它们包裹起来，以使头文件只包含一次：

::: {#cb344 .sourceCode}

```c
#ifndef MYHEADER_H  // First line of myheader.h
#define MYHEADER_H

int x = 12;

#endif  // Last line of myheader.h
```

:::

This demonstrates how a macro persists across files and multiple `#include` s. If it's not yet defined, let's define it and compile the whole header file.

> 这表明宏如何跨文件和多个 `#include` 持续存在。如果它还没有定义，让我们定义它并编译整个头文件。

But the next time it's included, we see that `MYHEADER_H` _is_ defined, so we don't send the header file to the compiler---it gets effectively removed.

> 下次包含时，我们发现 `MYHEADER_H` 已经定义了，所以我们不需要将头文件发送给编译器——它实际上被移除了。

### [19.3.3] `#else` {#else number="19.3.3"}

But that's not all we can do! There's also an `#else` that we can throw in the mix.

> 但这还不是我们能做的全部！我们还可以加入 `#else`。

Let's mod the previous example:

::: {#cb345 .sourceCode startfrom="8"}

```c
#ifdef EXTRA_HAPPY
    printf("I'm extra happy!\n");
#else
    printf("I'm just regular\n");
#endif
```

:::

Now if `EXTRA_HAPPY` is not defined, it'll hit the `#else` clause and print:

> 如果没有定义 `EXTRA_HAPPY`，它将会进入 `#else` 子句，并打印：

::: {#cb346 .sourceCode}

```{.sourceCode .default}
I'm just regular
```

:::

### [19.3.4] General Conditional: `#if`, `#elif` {#general-conditional-if-elif number="19.3.4"}

This works very much like the `#ifdef` and `#ifndef` directives in that you can also have an `#else` and the whole thing wraps up with `#endif`.

> 这与 `#ifdef` 和 `#ifndef` 指令非常相似，你也可以有一个 `#else`，整件事情最后用 `#endif` 来结束。

The only difference is that the constant expression after the `#if` must evaluate to true (non-zero) for the code in the `#if` to be compiled. So instead of whether or not something is defined, we want an expression that evaluates to true.

> `#if` 后面的常量表达式必须求值为真(非零)，才能编译 `#if` 中的代码。因此，我们需要一个求值为真的表达式，而不是某件东西是否被定义。

::: {#cb347 .sourceCode}

```c
#include <stdio.h>

#define HAPPY_FACTOR 1

int main(void)
{

#if HAPPY_FACTOR == 0
    printf("I'm not happy!\n");
#elif HAPPY_FACTOR == 1
    printf("I'm just regular\n");
#else
    printf("I'm extra happy!\n");
#endif

    printf("OK!\n");
}
```

:::

Again, for the unmatched `#if` clauses, the compiler won't even see those lines. For the above code, after the preprocessor gets finished with it, all the compiler sees is:

> 再次，对于不匹配的 `#if` 子句，编译器甚至不会看到这些行。对于上面的代码，在预处理器完成后，编译器看到的只有：

::: {#cb348 .sourceCode}

```c
#include <stdio.h>

int main(void)
{

    printf("I'm just regular\n");

    printf("OK!\n");
}
```

:::

One hackish thing this is used for is to comment out large numbers of lines quickly[^127^].

> 一种 hackish 的用法是快速注释掉大量的行[^127^]。

If you put an `#if 0` ("if false") at the front of the block to be commented out and an `#endif` at the end, you can get this effect:

> 如果在要被注释掉的块的前面放置一个 `#if 0`("如果为假")，并在末尾放置一个 `#endif`，您就可以获得这种效果：

::: {#cb349 .sourceCode}

```c
#if 0
    printf("All this code"); /* is effectively */
    printf("commented out"); // by the #if 0
#endif
```

:::

You might have noticed that there's no `#elifdef` or `#elifndef` directives. How can we get the same effect with `#if`? That is, what if I wanted this:

> 你可能已经注意到没有 `#elifdef` 或 `#elifndef` 指令。我们如何用 `#if` 达到同样的效果？也就是说，如果我想要这样：

::: {#cb350 .sourceCode}

```c
#ifdef FOO
    x = 2;
#elifdef BAR  // ERROR: Not supported by standard C
    x = 3;
#endif
```

:::

How could I do it?

Turns out there's a preprocessor operator called `defined` that we can use with an `#if` statement.

> 原来有一个叫做“defined”的预处理符号，我们可以用它来和一个“#if”语句一起使用。

These are equivalent:

::: {#cb351 .sourceCode}

```c
#ifdef FOO
#if defined FOO
#if defined(FOO)   // Parentheses optional
```

:::

As are these:

::: {#cb352 .sourceCode}

```c
#ifndef FOO
#if !defined FOO
#if !defined(FOO)   // Parentheses optional
```

:::

Notice how we can use the standard logical NOT operator (`!`) for "not defined".

> 注意我们可以使用标准的逻辑非运算符(`！`)来表示“未定义”。

So now we're back in `#if` land and we can use `#elif` with impunity!

This broken code:

::: {#cb353 .sourceCode}

```c
#ifdef FOO
    x = 2;
#elifdef BAR  // ERROR: Not supported by standard C
    x = 3;
#endif
```

:::

can be replaced with:

::: {#cb354 .sourceCode}

```c
#if defined FOO
    x = 2;
#elif defined BAR
    x = 3;
#endif
```

:::

### [19.3.5] Losing a Macro: `#undef` {#losing-a-macro-undef number="19.3.5"}

If you've defined something but you don't need it any longer, you can undefine it with `#undef`.

> 如果你定义了某些东西，但不再需要它，你可以使用 `#undef` 取消它的定义。

::: {#cb355 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
#define GOATS

#ifdef GOATS
    printf("Goats detected!\n");  // prints
#endif

#undef GOATS  // Make GOATS no longer defined

#ifdef GOATS
    printf("Goats detected, again!\n"); // doesn't print
#endif
}
```

:::

## [19.4] Built-in Macros {#built-in-macros number="19.4"}

The standard defines a lot of built-in macros that you can test and use for conditional compilation. Let's look at those here.

> 标准定义了许多内置宏，您可以对其进行测试并用于条件编译。让我们来看看这些。

### [19.4.1] Mandatory Macros {#mandatory-macros number="19.4.1"}

These are all defined:

---

Macro Description

---

`__DATE__` The date of compilation---like when you're compiling this file---in `Mmm dd yyyy` format

`__TIME__` The time of compilation in `hh:mm:ss` format

`__FILE__` A string containing this file's name

`__LINE__` The line number of the file this macro appears on

`__func__` The name of the function this appears in, as a string[^128^]

`__STDC__` Defined with `1` if this is a standard C compiler

`__STDC_HOSTED__` This will be `1` if the compiler is a _hosted implementation_[^129^], otherwise `0`

## `__STDC_VERSION__` This version of C, a constant `long int` in the form `yyyymmL`, e.g. `201710L`

Let's put these together.

::: {#cb356 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    printf("This function: %s\n", __func__);
    printf("This file: %s\n", __FILE__);
    printf("This line: %d\n", __LINE__);
    printf("Compiled on: %s %s\n", __DATE__, __TIME__);
    printf("C Version: %ld\n", __STDC_VERSION__);
}
```

:::

The output on my system is:

::: {#cb357 .sourceCode}

```{.sourceCode .default}
This function: main
This file: foo.c
This line: 7
Compiled on: Nov 23 2020 17:16:27
C Version: 201710
```

:::

`__FILE__`, `__func__` and `__LINE__` are particularly useful to report error conditions in messages to developers. The `assert()` macro in `<assert.h>` uses these to call out where in the code the assertion failed.

#### [19.4.1.1] `__STDC_VERSION__` s {#stdc_version\_\_s number="19.4.1.1"}

In case you're wondering, here are the version numbers for different major releases of the C Language Spec:

> 如果你想知道，以下是 C 语言规范的不同主要版本的版本号：

Release ISO/IEC version `__STDC_VERSION__`

---

C89 ISO/IEC 9899:1990 undefined
**C89** ISO/IEC 9899:1990/Amd.1:1995 `199409L`
**C99** ISO/IEC 9899:1999 `199901L`
**C11** ISO/IEC 9899:2011/Amd.1:2012 `201112L`

Note the macro did not exist originally in C89.

Also note that the plan is that the version numbers will strictly increase, so you could always check for, say, "at least C99" with:

> 此外，计划是版本号会严格增加，因此你可以总是检查，比如“至少 C99”：

::: {#cb358 .sourceCode}

```c
#if __STDC_VERSION__ >= 1999901L
```

:::

### [19.4.2] Optional Macros {#optional-macros number="19.4.2"}

Your implementation might define these, as well. Or it might not.

---

Macro Description

---

`__STDC_ISO_10646__` If defined, `wchar_t` holds Unicode values, otherwise something else

`__STDC_MB_MIGHT_NEQ_WC__` A `1` indicates that the values in multibyte characters might not map equally to values in wide characters

`__STDC_UTF_16__` A `1` indicates that the system uses UTF-16 encoding in type `char16_t`

`__STDC_UTF_32__` A `1` indicates that the system uses UTF-32 encoding in type `char32_t`

`__STDC_ANALYZABLE__` A `1` indicates the code is analyzable[^130^]

`__STDC_IEC_559__` `1` if IEEE-754 (aka IEC 60559) floating point is supported

`__STDC_IEC_559_COMPLEX__` `1` if IEC 60559 complex floating point is supported

`__STDC_LIB_EXT1__` `1` if this implementation supports a variety of "safe" alternate standard library functions (they have `_s` suffixes on the name)

`__STDC_NO_ATOMICS__` `1` if this implementation does **not** support `_Atomic` or `<stdatomic.h>`

`__STDC_NO_COMPLEX__` `1` if this implementation does **not** support complex types or `<complex.h>`

`__STDC_NO_THREADS__` `1` if this implementation does **not** support `<threads.h>`

## `__STDC_NO_VLA__` `1` if this implementation does **not** support variable-length arrays

## [19.5] Macros with Arguments {#macros-with-arguments number="19.5"}

Macros are more powerful than simple substitution, though. You can set them up to take arguments that are substituted in, as well.

> 宏比简单的替换更强大，而且还可以设置参数进行替换。

A question often arises for when to use parameterized macros versus functions. Short answer: use functions. But you'll see lots of macros in the wild and in the standard library. People tend to use them for short, mathy things, and also for features that might change from platform to platform. You can define different keywords for one platform or another.

> 经常会有一个问题，即何时使用参数化宏而不是函数。简短的答案是：使用函数。但是你会在野外和标准库中看到很多宏。人们倾向于用它们来处理简短的数学问题，以及那些可能因平台而异的特性。你可以为不同的平台定义不同的关键字。

### [19.5.1] Macros with One Argument {#macros-with-one-argument number="19.5.1"}

Let's start with a simple one that squares a number:

::: {#cb359 .sourceCode}

```c
#include <stdio.h>

#define SQR(x) x * x  // Not quite right, but bear with me

int main(void)
{
    printf("%d\n", SQR(12));  // 144
}
```

:::

What that's saying is "everywhere you see `SQR` with some value, replace it with that value times itself".

> 所说的是：每当你看到带有某个值的 `SQR`，就用该值乘以它自身来替换它。

So line 7 will be changed to:

::: {#cb360 .sourceCode startfrom="7"}

```c
    printf("%d\n", 12 * 12);  // 144
```

:::

which C comfortably converts to 144.

But we've made an elementary error in that macro, one that we need to avoid.

> 但是我们在那个宏中犯了一个基本错误，我们需要避免。

Let's check it out. What if we wanted to compute `SQR(3 + 4)`? Well, [\\(3+4=7\\)]{.math .inline}, so we must want to compute [\\(7\^2=49\\)]{.math .inline}. That's it; `49`---final answer.

> 咱们来检查一下，如果我们想计算 SQR(3 + 4)呢？嗯，[\(3+4=7\)]{.math .inline}，所以我们必须想计算[\(7\ ^ 2=49\)]{.math .inline}。就是这样；`49`---最终答案。

Let's drop it in our code and see that we get... 19?

::: {#cb361 .sourceCode startfrom="7"}

```c
    printf("%d\n", SQR(3 + 4));  // 19!!??
```

:::

What happened?

If we follow the macro expansion, we get

::: {#cb362 .sourceCode startfrom="7"}

```c
    printf("%d\n", 3 + 4 * 3 + 4);  // 19!
```

:::

Oops! Since multiplication takes precedence, we do the [\\(4\\times3=12\\)]{.math .inline} first, and get [\\(3+12+4=19\\)]{.math .inline}. Not what we were after.

> 哎呀！由于乘法优先，我们先做[\(4\times3=12\)]{.math .inline}，结果是[\(3+12+4=19\)]{.math .inline}，这不是我们想要的结果。

So we have to fix this to make it right.

**This is so common that you should automatically do it every time you make a parameterized math macro!**

> 这是如此常见，以至于每次你创建一个参数化的数学宏时都应该自动进行！

The fix is easy: just add some parentheses!

::: {#cb363 .sourceCode startfrom="3"}

```c
#define SQR(x) (x) * (x)   // Better... but still not quite good enough!
```

:::

And now our macro expands to:

::: {#cb364 .sourceCode startfrom="7"}

```c
    printf("%d\n", (3 + 4) * (3 + 4));  // 49! Woo hoo!
```

:::

But we actually still have the same problem which might manifest if we have a higher-precedence operator than multiply (`*`) nearby.

> 但是，如果我们附近有一个优先级比乘法(*)更高的运算符，我们实际上仍然存在相同的问题，可能会出现。

So the safe, proper way to put the macro together is to wrap the whole thing in additional parentheses, like so:

> 所以安全正确的方式来把宏组合在一起就是在整个东西外面包裹额外的括号，像这样：

::: {#cb365 .sourceCode startfrom="3"}

```c
#define SQR(x) ((x) * (x))   // Good!
```

:::

Just make it a habit to do that when you make a math macro and you can't go wrong.

> 就把它变成一个习惯，当你做数学宏的时候，你就不会出错了。

### [19.5.2] Macros with More than One Argument {#macros-with-more-than-one-argument number="19.5.2"}

You can stack these things up as much as you want:

::: {#cb366 .sourceCode}

```c
#define TRIANGLE_AREA(w, h) (0.5 * (w) * (h))
```

:::

Let's do some macros that solve for [\\(x\\)]{.math .inline} using the quadratic formula. Just in case you don't have it on the top of your head, it says for equations of the form:

> 让我们做一些宏，使用二次公式来求解[\\(x\\)]{.math .inline}。以防万一你没有记住，它适用于形式为：

[\\(ax\^2+bx+c=0\\)]{.math .inline}

you can solve for [\\(x\\)]{.math .inline} with the quadratic formula:

[\\(x=\\displaystyle\\frac{-b\\pm\\sqrt{b\^2-4ac}}{2a}\\)]{.math .inline}

Which is crazy. Also notice the plus-or-minus ([\\(\\pm\\)]{.math .inline}) in there, indicating that there are actually two solutions.

> 这太疯狂了。另外注意那里的正负号(±)，表明实际上有两个解决方案。

So let's make macros for both:

::: {#cb367 .sourceCode}

```c
#define QUADP(a, b, c) ((-(b) + sqrt((b) * (b) - 4 * (a) * (c))) / (2 * (a)))
#define QUADM(a, b, c) ((-(b) - sqrt((b) * (b) - 4 * (a) * (c))) / (2 * (a)))
```

:::

So that gets us some math. But let's define one more that we can use as arguments to `printf()` to print both answers.

> 那么我们就有了一些数学。但是让我们定义一个更多的，我们可以用它作为 `printf()` 的参数来打印两个答案。

::: {#cb368 .sourceCode}

```c
//          macro              replacement
//      |-----------| |----------------------------|
#define QUAD(a, b, c) QUADP(a, b, c), QUADM(a, b, c)
```

:::

That's just a couple values separated by a comma---and we can use that as a "combined" argument of sorts to `printf()` like this:

> 这只是一些用逗号分隔的值---我们可以把它们作为一个"组合"参数传递给 `printf()`，就像这样：

::: {#cb369 .sourceCode}

```c
printf("x = %f or x = %f\n", QUAD(2, 10, 5));
```

:::

Let's put it together into some code:

::: {#cb370 .sourceCode}

```c
#include <stdio.h>
#include <math.h>  // For sqrt()

#define QUADP(a, b, c) ((-(b) + sqrt((b) * (b) - 4 * (a) * (c))) / (2 * (a)))
#define QUADM(a, b, c) ((-(b) - sqrt((b) * (b) - 4 * (a) * (c))) / (2 * (a)))
#define QUAD(a, b, c) QUADP(a, b, c), QUADM(a, b, c)

int main(void)
{
    printf("2*x^2 + 10*x + 5 = 0\n");
    printf("x = %f or x = %f\n", QUAD(2, 10, 5));
}
```

:::

And this gives us the output:

::: {#cb371 .sourceCode}

```{.sourceCode .default}
2*x^2 + 10*x + 5 = 0
x = -0.563508 or x = -4.436492
```

:::

Plugging in either of those values gives us roughly zero (a bit off because the numbers aren't exact):

> 插入这两个值中的任何一个都会给我们大致得到零(因为数字不是精确的，所以略有偏差)：

[\\(2\\times-0.563508\^2+10\\times-0.563508+5\\approx0.000003\\)]{.math .inline}

> [\\(2 \times -0.563508^2 + 10 \times -0.563508 + 5 \approx 0.000003\\)]{.math .inline}

[\\(2 \times -0.563508^2 + 10 \times -0.563508 + 5 \approx 0.000003\\)]{.math .inline} 约等于 0.000003

### [19.5.3] Macros with Variable Arguments {#macros-with-variable-arguments number="19.5.3"}

There's also a way to have a variable number of arguments passed to a macro, using ellipses (`...`) after the known, named arguments. When the macro is expanded, all of the extra arguments will be in a comma-separated list in the `__VA_ARGS__` macro, and can be replaced from there:

> 也可以使用省略号(`...`)在已知的命名参数后传递可变数量的参数给宏。当宏展开时，所有额外的参数都会在 `__VA_ARGS__` 宏中以逗号分隔的列表形式出现，可以从那里替换：

::: {#cb372 .sourceCode}

```c
#include <stdio.h>

// Combine the first two arguments to a single number,
// then have a commalist of the rest of them:

#define X(a, b, ...) (10*(a) + 20*(b)), __VA_ARGS__

int main(void)
{
    printf("%d %f %s %d\n", X(5, 4, 3.14, "Hi!", 12));
}
```

:::

The substitution that takes place on line 10 would be:

::: {#cb373 .sourceCode startfrom="10"}

```c
    printf("%d %f %s %d\n", (10*(5) + 20*(4)), 3.14, "Hi!", 12);
```

:::

for output:

::: {#cb374 .sourceCode}

```{.sourceCode .default}
130 3.140000 Hi! 12
```

:::

You can also "stringify" `__VA_ARGS__` by putting a `#` in front of it:

::: {#cb375 .sourceCode}

```c
#define X(...) #__VA_ARGS__

printf("%s\n", X(1,2,3));  // Prints "1, 2, 3"
```

:::

### [19.5.4] Stringification {#stringification number="19.5.4"}

Already mentioned, just above, you can turn any argument into a string by preceding it with a `#` in the replacement text.

> 已经提到，在上面，你可以通过在替换文本中添加一个 `#` 来将任何参数转换为字符串。

For example, we could print anything as a string with this macro and `printf()`:

> 例如，我们可以使用这个宏和 `printf()` 将任何内容打印为字符串：

::: {#cb376 .sourceCode}

```c
#define STR(x) #x

printf("%s\n", STR(3.14159));
```

:::

In that case, the substitution leads to:

::: {#cb377 .sourceCode}

```c
printf("%s\n", "3.14159");
```

:::

Let's see if we can use this to greater effect so that we can pass any `int` variable name into a macro, and have it print out it's name and value.

> 让我们看看我们是否可以使用这个来取得更大的效果，以便我们可以将任何 `int` 变量名传递给宏，并打印出它的名称和值。

::: {#cb378 .sourceCode}

```c
#include <stdio.h>

#define PRINT_INT_VAL(x) printf("%s = %d\n", #x, x)

int main(void)
{
    int a = 5;

    PRINT_INT_VAL(a);  // prints "a = 5"
}
```

:::

On line 9, we get the following macro replacement:

::: {#cb379 .sourceCode startfrom="9"}

```c
    printf("%s = %d\n", "a", 5);
```

:::

### [19.5.5] Concatenation {#concatenation number="19.5.5"}

We can concatenate two arguments together with `##`, as well. Fun times!

::: {#cb380 .sourceCode}

```c
#define CAT(a, b) a ## b

printf("%f\n", CAT(3.14, 1592));   // 3.141592
```

:::

## [19.6] Multiline Macros {#multiline-macros number="19.6"}

It's possible to continue a macro to multiple lines if you escape the newline with a backslash (`\`).

> 可以通过使用反斜杠(\)转义换行符来将宏延续到多行。

Let's write a multiline macro that prints numbers from `0` to the product of the two arguments passed in.

> 让我们编写一个多行宏，从传入的两个参数的乘积开始打印数字。

::: {#cb381 .sourceCode}

```c
#include <stdio.h>

#define PRINT_NUMS_TO_PRODUCT(a, b) do { \
    int product = (a) * (b); \
    for (int i = 0; i < product; i++) { \
        printf("%d\n", i); \
    } \
} while(0)

int main(void)
{
    PRINT_NUMS_TO_PRODUCT(2, 4);  // Outputs numbers from 0 to 7
}
```

:::

A couple things to note there:

- Escapes at the end of every line except the last one to indicate that the macro continues.
- The whole thing is wrapped in a `do`-`while(0)` loop with squirrley braces.

The latter point might be a little weird, but it's all about absorbing the trailing `;` the coder drops after the macro.

> 这个后面的观点可能有点奇怪，但是它是关于吸收编码者在宏之后丢弃的分号 `;` 的。

At first I thought that just using squirrely braces would be enough, but there's a case where it fails if the coder puts a semicolon after the macro. Here's that case:

> 首先我以为只使用花括号就足够了，但是如果程序员在宏之后放置分号，就会出现失败的情况。这是那种情况：

::: {#cb382 .sourceCode}

```c
#include <stdio.h>

#define FOO(x) { (x)++; }

int main(void)
{
    int i = 0;

    if (i == 0)
        FOO(i);
    else
        printf(":-(\n");

    printf("%d\n", i);
}
```

:::

Looks simple enough, but it won't build without a syntax error:

::: {#cb383 .sourceCode}

```{.sourceCode .default}
foo.c:11:5: error: ‘else’ without a previous ‘if’
```

:::

Do you see it?

Let's look at the expansion:

::: {#cb384 .sourceCode}

```c
    if (i == 0) {
        (i)++;
    };             // <-- Trouble with a capital-T!

    else
        printf(":-(\n");
```

:::

The `;` puts an end to the `if` statement, so the `else` is just floating out there illegally[^131^].

> `分号` 结束了 `if` 语句，所以 `else` 就漂浮在那里，违法了 [^131^]。

So wrap that multiline macro with a `do`-`while(0)`.

## [19.7] Example: An Assert Macro {#my-assert number="19.7"}

Adding asserts to your code is a good way to catch conditions that you think shouldn't happen. C provides `assert()` functionality. It checks a condition, and if it's false, the program bombs out telling you the file and line number on which the assertion failed.

> 在你的代码中添加断言是捕获你认为不应该发生的情况的一个好方法。C 提供了 `assert()` 功能。它检查一个条件，如果它是错误的，程序会告诉你断言失败的文件和行号。

But this is wanting.

1. First of all, you can't specify an additional message with the assert.
2. Secondly, there's no easy on-off switch for all the asserts.

We can address the first with macros.

Basically, when I have this code:

::: {#cb385 .sourceCode}

```c
ASSERT(x < 20, "x must be under 20");
```

:::

I want something like this to happen (assuming the `ASSERT()` is on line 220 of `foo.c`):

> 我希望像这样的事情发生(假设 `ASSERT()` 在 `foo.c` 的第 220 行)：

::: {#cb386 .sourceCode}

```c
if (!(x < 20)) {
    fprintf(stderr, "foo.c:220: assertion x < 20 failed: ");
    fprintf(stderr, "x must be under 20\n");
    exit(1);
}
```

:::

We can get the filename out of the `__FILE__` macro, and the line number from `__LINE__`. The message is already a string, but `x < 20` is not, so we'll have to stringify it with `#`. We can make a multiline macro by using backslash escapes at the end of the line.

> 我们可以从 `__FILE__` 宏中获取文件名，从 `__LINE__` 中获取行号。消息已经是一个字符串，但 `x < 20` 不是，所以我们必须使用 `#` 将其字符串化。我们可以通过在行末使用反斜杠转义来创建多行宏。

::: {#cb387 .sourceCode}

```c
#define ASSERT(c, m) \
do { \
    if (!(c)) { \
        fprintf(stderr, __FILE__ ":%d: assertion %s failed: %s\n", \
                        __LINE__, #c, m); \
        exit(1); \
    } \
} while(0)
```

:::

(It looks a little weird with `__FILE__` out front like that, but remember it is a string literal, and string literals next to each other are automagically concatenated. `__LINE__` on the other hand, it's just an `int`.)

> 看起来有点奇怪，`__FILE__` 前面这样，但要记住它是一个字符串文字，而且相邻的字符串文字会自动连接在一起。另一方面，`__LINE__` 只是一个 `int`。

And that works! If I run this:

::: {#cb388 .sourceCode}

```c
int x = 30;

ASSERT(x < 20, "x must be under 20");
```

:::

I get this output:

```
foo.c:23: assertion x < 20 failed: x must be under 20
```

Very nice!

The only thing left is a way to turn it on and off, and we could do that with conditional compilation.

> 唯一剩下的事情就是找到一种开关的方式，我们可以通过条件编译来实现。

Here's the complete example:

::: {#cb390 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

#define ASSERT_ENABLED 1

#if ASSERT_ENABLED
#define ASSERT(c, m) \
do { \
    if (!(c)) { \
        fprintf(stderr, __FILE__ ":%d: assertion %s failed: %s\n", \
                        __LINE__, #c, m); \
        exit(1); \
    } \
} while(0)
#else
#define ASSERT(c, m)  // Empty macro if not enabled
#endif

int main(void)
{
    int x = 30;

    ASSERT(x < 20, "x must be under 20");
}
```

:::

This has the output:

::: {#cb391 .sourceCode}

```{.sourceCode .default}
foo.c:23: assertion x < 20 failed: x must be under 20
```

:::

## [19.8] The `#error` Directive {#the-error-directive number="19.8"}

This directive causes the compiler to error out as soon as it sees it.

Commonly, this is used inside a conditional to prevent compilation unless some prerequisites are met:

> 通常，这在条件中使用，以防止编译，除非满足一些先决条件：

::: {#cb392 .sourceCode}

```c
#ifndef __STDC_IEC_559__
    #error I really need IEEE-754 floating point to compile. Sorry!
#endif
```

:::

Some compilers have a non-standard complementary `#warning` directive that will output a warning but not stop compilation, but this is not in the C11 spec.

> 一些编译器有一个非标准的补充 `#warning` 指令，它可以输出警告，但不会停止编译，但这不在 C11 规范中。

## [19.9] The `#pragma` Directive {#pragma number="19.9"}

This is one funky directive, short for "pragmatic". You can use it to do... well, anything your compiler supports you doing with it.

> 这是一个有趣的指令，简称“实用主义”。你可以用它做任何你的编译器支持你做的事情。

Basically the only time you're going to add this to your code is if some documentation tells you to do so.

> 基本上，你只有在文档告诉你这么做的时候才会把它加入到你的代码中。

### [19.9.1] Non-Standard Pragmas {#non-standard-pragmas number="19.9.1"}

Here's one non-standard example of using `#pragma` to cause the compiler to execute a `for` loop in parallel with multiple threads (if the compiler supports the [OpenMP](https://www.openmp.org/)[^132^] extension):

> 这里有一个使用 `#pragma` 的非标准示例，可以使编译器使用多个线程并行执行 `for` 循环(如果编译器支持 [OpenMP](https://www.openmp.org/)[^132^]扩展)：

::: {#cb393 .sourceCode}

```c
#pragma omp parallel for
for (int i = 0; i < 10; i++) { ... }
```

:::

There are all kinds of `#pragma` directives documented across all four corners of the globe.

> 在全球四个角落都有文档记载的各种 `#pragma` 指令。

All unrecognized `#pragma` s are ignored by the compiler.

### [19.9.2] Standard Pragmas {#standard-pragmas number="19.9.2"}

There are also a few standard ones, and these start with `STDC`, and follow the same form:

> 也有一些标准的，以 `STDC` 开头，遵循相同的形式：

::: {#cb394 .sourceCode}

```c
#pragma STDC pragma_name on-off
```

:::

The `on-off` portion can be either `ON`, `OFF`, or `DEFAULT`.

And the `pragma_name` can be one of these:

---

Pragma Name Description

---

`FP_CONTRACT` Allow floating point expressions to be contracted into a single operation to avoid rounding errors that might occur from multiple operations.

`FENV_ACCESS` Set to `ON` if you plan to access the floating point status flags. If `OFF`, the compiler might perform optimizations that cause the values in the flags to be inconsistent or invalid.

## `CX_LIMITED_RANGE` Set to `ON` to allow the compiler to skip overflow checks when performing complex arithmetic. Defaults to `OFF`.

For example:

::: {#cb395 .sourceCode}

```c
#pragma STDC FP_CONTRACT OFF
#pragma STDC CX_LIMITED_RANGE ON
```

:::

As for `CX_LIMITED_RANGE`, the spec points out:

> The purpose of the pragma is to allow the implementation to use the formulas:
>
> [\\((x+iy)\\times(u+iv) = (xu-yv)+i(yu+xv)\\)]{.math .inline}
>
> [\\((x+iy)/(u+iv) = \[(xu+yv)+i(yu-xv)\]/(u\^2+v\^2)\\)]{.math .inline}
>
> [\\(\|x+iy\|=\\sqrt{x\^2+y\^2}\\)]{.math .inline}
>
> where the programmer can determine they are safe.

### [19.9.3] `_Pragma` Operator {#pragma-operator number="19.9.3"}

This is another way to declare a pragma that you could use in a macro.

These are equivalent:

::: {#cb396 .sourceCode}

```c
#pragma "Unnecessary" quotes
_Pragma("\"Unnecessary\" quotes")
```

:::

This can be used in a macro, if need be:

::: {#cb397 .sourceCode}

```c
#define PRAGMA(x) _Pragma(#x)
```

:::

## [19.10] The `#line` Directive {#the-line-directive number="19.10"}

This allows you to override the values for `__LINE__` and `__FILE__`. If you want.

> 这允许您覆盖 `__LINE__` 和 `__FILE__` 的值。如果你想的话。

I've never wanted to do this, but in K&R2, they write:

> For the benefit of other preprocessors that generate C programs \[...\]

So maybe there's that.

To override the line number to, say 300:

::: {#cb398 .sourceCode}

```c
#line 300
```

:::

and `__LINE__` will keep counting up from there.

To override the line number and the filename:

::: {#cb399 .sourceCode}

```c
#line 300 "newfilename"
```

:::

## [19.11] The Null Directive {#the-null-directive number="19.11"}

A `#` on a line by itself is ignored by the preprocessor. Now, to be entirely honest, I don't know what the use case is for this.

> 预处理器会忽略一行中的 `#`。说实话，我不知道这有什么用处。

I've seen examples like this:

::: {#cb400 .sourceCode}

```c
#ifdef FOO
    #
#else
    printf("Something");
#endif
```

:::

which is just cosmetic; the line with the solitary `#` can be deleted with no ill effect.

> 这只是外观上的；只有一个 `#` 的行可以被删除而不会造成任何不良影响。

Or maybe for cosmetic consistency, like this:

::: {#cb401 .sourceCode}

```c
#
#ifdef FOO
    x = 2;
#endif
#
#if BAR == 17
    x = 12;
#endif
#
```

:::

But, with respect to cosmetics, that's just ugly.

Another post mentions elimination of comments---that in GCC, a comment after a `#` will not be seen by the compiler. Which I don't doubt, but the specification doesn't seem to say this is standard behavior.

> 另一篇文章提到消除注释---在 GCC 中，`#` 后面的注释将不会被编译器看到。我不怀疑这一点，但规范似乎没有说这是标准行为。

My searches for rationale aren't bearing much fruit. So I'm going to just say this is some good ol' fashioned C esoterica.

> 我寻找理由的结果并没有太大的成果，所以我只能说这是一些古老的 C 语言奥秘。

# [20] `struct` s II: More Fun with `struct` s {#structs-ii-more-fun-with-structs number="20"}

Turns out there's a lot more you can do with `struct` s than we've talked about, but it's just a big pile of miscellaneous things. So we'll throw them in this chapter.

> 原来你可以用 `struct` 做的事情比我们讨论的要多得多，但它们只是一大堆杂项。所以我们将把它们放在这一章中。

If you're good with `struct` basics, you can round out your knowledge here.

> 如果你对 `struct` 基础有所了解，你可以在这里完善你的知识。

## [20.1] Initializers of Nested `struct` s and Arrays {#initializers-of-nested-structs-and-arrays number="20.1"}

Remember how you could [initialize structure members along these lines](#struct-initializers)?

> 记住你怎样可以这样[初始化结构成员](#struct-initializers)吗？

::: {#cb402 .sourceCode}

```c
struct foo x = {.a=12, .b=3.14};
```

:::

Turns out we have more power in these initializers than we'd originally shared. Exciting!

> 原来我们在这些初始化程序中拥有的力量比我们最初分享的要多。令人兴奋！

For one thing, if you have a nested substructure like the following, you can initialize members of that substructure by following the variable names down the line:

> 如果你有一个嵌套的子结构，你可以通过沿着变量名称来初始化该子结构的成员。

::: {#cb403 .sourceCode}

```c
struct foo x = {.a.b.c=12};
```

:::

Let's look at an example:

::: {#cb404 .sourceCode}

```c
#include <stdio.h>

struct cabin_information {
    int window_count;
    int o2level;
};

struct spaceship {
    char *manufacturer;
    struct cabin_information ci;
};

int main(void)
{
    struct spaceship s = {
        .manufacturer="General Products",
        .ci.window_count = 8,   // <-- NESTED INITIALIZER!
        .ci.o2level = 21
    };

    printf("%s: %d seats, %d%% oxygen\n",
        s.manufacturer, s.ci.window_count, s.ci.o2level);
}
```

:::

Check out lines 16-17! That's where we're initializing members of the `struct cabin_information` in the definition of `s`, our `struct spaceship`.

> 查看 16-17 行！这就是我们在定义's'(我们的'struct spaceship')时初始化'struct cabin_information'成员的地方。

And here is another option for that same initializer---this time we'll do something more standard-looking, but either approach works:

> 这里有另一个选项来初始化，这次我们会做一些看起来更标准的事情，但是任何一种方法都可以工作：

::: {#cb405 .sourceCode startfrom="15"}

```c
    struct spaceship s = {
        .manufacturer="General Products",
        .ci={
            .window_count = 8,
            .o2level = 21
        }
    };
```

:::

Now, as if the above information isn't spectacular enough, we can also mix in array initializers in there, too.

> 现在，就好像上面的信息还不够出色，我们还可以把数组初始化器混合进去。

Let's change this up to get an array of passenger information in there, and we can check out how the initializers work in there, too.

> 让我们改变一下，把乘客信息放进数组里，我们也可以看看初始化器是如何在里面工作的。

::: {#cb406 .sourceCode}

```c
#include <stdio.h>

struct passenger {
    char *name;
    int covid_vaccinated; // Boolean
};

#define MAX_PASSENGERS 8

struct spaceship {
    char *manufacturer;
    struct passenger passenger[MAX_PASSENGERS];
};

int main(void)
{
    struct spaceship s = {
        .manufacturer="General Products",
        .passenger = {
            // Initialize a field at a time
            [0].name = "Gridley, Lewis",
            [0].covid_vaccinated = 0,

            // Or all at once
            [7] = {.name="Brown, Teela", .covid_vaccinated=1},
        }
    };

    printf("Passengers for %s ship:\n", s.manufacturer);

    for (int i = 0; i < MAX_PASSENGERS; i++)
        if (s.passenger[i].name != NULL)
            printf("    %s (%svaccinated)\n",
                s.passenger[i].name,
                s.passenger[i].covid_vaccinated? "": "not ");
}
```

:::

## [20.2] Anonymous `struct` s {#anonymous-structs number="20.2"}

These are "the `struct` with no name". We also mention these in the [`typedef`](#typedef-struct) section, but we'll refresh here.

> 这些是没有名字的 `struct`。我们也在[`typedef`](#typedef-struct)部分提到了这些，但我们在这里重新回顾一下。

Here's a regular `struct`:

::: {#cb407 .sourceCode}

```c
struct animal {
    char *name;
    int leg_count, speed;
};
```

:::

And here's the anonymous equivalent:

::: {#cb408 .sourceCode}

```c
struct {              // <-- No name!
    char *name;
    int leg_count, speed;
};
```

:::

Okaaaaay. So we have a `struct`, but it has no name, so we have no way of using it later? Seems pretty pointless.

> 哦，好吧。所以我们有一个 `struct`，但它没有名字，所以我们没有办法以后使用它？看起来没什么意义。

Admittedly, in that example, it is. But we can still make use of it a couple ways.

> 承认，在那个例子里，是这样。但我们仍然可以利用它几种方式。

One is rare, but since the anonymous `struct` represents a type, we can just put some variable names after it and use them.

> 一个是罕见的，但由于匿名 `struct` 代表一种类型，我们可以在它后面放一些变量名，并使用它们。

::: {#cb409 .sourceCode}

```c
struct {                   // <-- No name!
    char *name;
    int leg_count, speed;
} a, b, c;                 // 3 variables of this struct type

a.name = "antelope";
c.leg_count = 4;           // for example
```

:::

But that's still not that useful.

Far more common is use of anonymous `struct` s with a `typedef` so that we can use it later (e.g. to pass variables to functions).

> 更常见的是使用匿名结构体和 `typedef`，以便我们稍后使用它(例如将变量传递给函数)。

::: {#cb410 .sourceCode}

```c
typedef struct {                   // <-- No name!
    char *name;
    int leg_count, speed;
} animal;                          // New type: animal

animal a, b, c;

a.name = "antelope";
c.leg_count = 4;           // for example
```

:::

Personally, I don't use many anonymous `struct` s. I think it's more pleasant to see the entire `struct animal` before the variable name in a declaration.

> 我个人不常使用匿名结构体。我认为在声明中在变量名称之前看到整个 `struct animal` 更加令人愉悦。

But that's just, like, my opinion, man.

## [20.3] Self-Referential `struct` s {#self-referential-structs number="20.3"}

For any graph-like data structure, it's useful to be able to have pointers to the connected nodes/vertices. But this means that in the definition of a node, you need to have a pointer to a node. It's chicken and eggy!

> 对于任何类似图形的数据结构，能够指向相连的节点/顶点是很有用的。但这意味着在节点的定义中，你需要有一个指向节点的指针。这就是先有鸡还是先有蛋的问题！

But it turns out you can do this in C with no problem whatsoever.

For example, here's a linked list node:

::: {#cb411 .sourceCode}

```c
struct node {
    int data;
    struct node *next;
};
```

:::

It's important to note that `next` is a pointer. This is what allows the whole thing to even build. Even though the compiler doesn't know what the entire `struct node` looks like yet, all pointers are the same size.

> 重要的是要注意 `next` 是一个指针。这就是使整个事情能够建立的原因。尽管编译器还不知道整个 `struct node` 的样子，但所有的指针都是相同大小的。

Here's a cheesy linked list program to test it out:

::: {#cb412 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *next;
};

int main(void)
{
    struct node *head;

    // Hackishly set up a linked list (11)->(22)->(33)
    head = malloc(sizeof(struct node));
    head->data = 11;
    head->next = malloc(sizeof(struct node));
    head->next->data = 22;
    head->next->next = malloc(sizeof(struct node));
    head->next->next->data = 33;
    head->next->next->next = NULL;

    // Traverse it
    for (struct node *cur = head; cur != NULL; cur = cur->next) {
        printf("%d\n", cur->data);
    }
}
```

:::

Running that prints:

::: {#cb413 .sourceCode}

```{.sourceCode .default}
11
22
33
```

:::

## [20.4] Flexible Array Members {#flexible-array-members number="20.4"}

Back in the good old days, when people carved C code out of wood, some folks thought would be neat if they could allocate `struct` s that had variable length arrays at the end of them.

> 回到那美好的日子，当人们用木头雕刻 C 代码时，有些人认为如果他们可以在结构体的末尾分配可变长度数组就很棒。

I want to be clear that the first part of the section is the old way of doing things, and we're going to do things the new way after that.

> 我想清楚地表明，这一部分的第一部分是旧的做法，在那之后我们将以新的方式来做事情。

For example, maybe you could define a `struct` for holding strings and the length of that string. It would have a length and an array to hold the data. Maybe something like this:

> 例如，也许你可以定义一个 `struct` 来保存字符串和字符串的长度。它将具有长度和一个数组来保存数据。也许像这样：

::: {#cb414 .sourceCode}

```c
struct len_string {
    int length;
    char data[8];
};
```

:::

But that has `8` hardcoded as the maximum length of a string, and that's not much. What if we did something _clever_ and just `malloc()` d some extra space at the end after the struct, and then let the data overflow into that space?

> 但是，它将 `8` 硬编码为字符串的最大长度，这不是很多。如果我们做一些聪明的事情，在结构之后 `malloc()` 一些额外的空间，然后让数据溢出到该空间呢？

Let's do that, and then allocate another 40 bytes on top of it:

::: {#cb415 .sourceCode}

```c
struct len_string *s = malloc(sizeof *s + 40);
```

:::

Because `data` is the last field of the `struct`, if we overflow that field, it runs out into space that we already allocated! For this reason, this trick only works if the short array is the _last_ field in the `struct`.

> 因为 `data` 是 `struct` 的最后一个字段，如果我们溢出了该字段，它就会进入我们已经分配的空间！因此，这个技巧只有在短数组是 `struct` 的最后一个字段时才有效。

::: {#cb416 .sourceCode}

```c
// Copy more than 8 bytes!

strcpy(s->data, "Hello, world!");  // Won't crash. Probably.
```

:::

In fact, there was a common compiler workaround for doing this, where you'd allocate a zero length array at the end:

> 事实上，有一种通用的编译器解决方案可以做到这一点，即在末尾分配一个零长度数组：

::: {#cb417 .sourceCode}

```c
struct len_string {
    int length;
    char data[0];
};
```

:::

And then every extra byte you allocated was ready for use in that string.

Because `data` is the last field of the `struct`, if we overflow that field, it runs out into space that we already allocated!

> 因为 `data` 是 `struct` 的最后一个字段，如果我们溢出了该字段，它就会进入我们已经分配的空间！

::: {#cb418 .sourceCode}

```c
// Copy more than 8 bytes!

strcpy(s->data, "Hello, world!");  // Won't crash. Probably.
```

:::

But, of course, actually accessing the data beyond the end of that array is undefined behavior! In these modern times, we no longer deign to resort to such savagery.

> 但是，当然，实际访问数组末尾之外的数据是没有定义的行为！在这个现代时代，我们不再屈尊于这种野蛮行为。

Luckily for us, we can still get the same effect with C99 and later, but now it's legal.

> 幸运的是，我们可以使用 C99 及更高版本来获得同样的效果，而且现在这是合法的。

Let's just change our above definition to have no size for the array[^133^]:

> 让我们把上面的定义改变一下，让数组没有大小(133 号脚注)：

::: {#cb419 .sourceCode}

```c
struct len_string {
    int length;
    char data[];
};
```

:::

Again, this only works if the flexible array member is the _last_ field in the `struct`.

> 再次，只有当灵活数组成员是 `struct` 中的最后一个字段时，此操作才有效。

And then we can allocate all the space we want for those strings by `malloc()` ing larger than the `struct len_string`, as we do in this example that makes a new `struct len_string` from a C string:

> 然后，我们可以为这些字符串分配我们想要的所有空间，就像我们在这个例子中一样，使用 `malloc()` 从 C 字符串创建新的 `struct len_string`：

::: {#cb420 .sourceCode}

```c
struct len_string *len_string_from_c_string(char *s)
{
    int len = strlen(s);

    // Allocate "len" more bytes than we'd normally need
    struct len_string *ls = malloc(sizeof *ls + len);

    ls->length = len;

    // Copy the string into those extra bytes
    memcpy(ls->data, s, len);

    return ls;
}
```

:::

## [20.5] Padding Bytes {#struct-padding-bytes number="20.5"}

Beware that C is allowed to add padding bytes within or after a `struct` as it sees fit. You can't trust that they will be directly adjacent in memory[^134^].

> 小心，C 可以根据自己的意愿在 `struct` 中或之后添加填充字节。你不能相信它们会直接排列在内存中[^134^]。

Let's take a look at this program. We output two numbers. One is the sum of the `sizeof` s the individual field types. The other is the `sizeof` the entire `struct`.

> 让我们看一下这个程序。我们输出两个数字。一个是各个字段类型的 `sizeof` 之和，另一个是整个 `struct` 的 `sizeof`。

One would expect them to be the same. The size of the total is the size of the sum of its parts, right?

> 一个人会期望它们是相同的。总体的大小就是它的部分之和的大小，对吗？

::: {#cb421 .sourceCode}

```c
#include <stdio.h>

struct foo {
    int a;
    char b;
    int c;
    char d;
};

int main(void)
{
    printf("%zu\n", sizeof(int) + sizeof(char) + sizeof(int) + sizeof(char));
    printf("%zu\n", sizeof(struct foo));
}
```

:::

But on my system, this outputs:

::: {#cb422 .sourceCode}

```{.sourceCode .default}
10
16
```

:::

They're not the same! The compiler has added 6 bytes of padding to help it be more performant. Maybe you got different output with your compiler, but unless you're forcing it, you can't be sure there's no padding.

> 他们不一样！编译器添加了 6 个字节的填充来帮助它更具性能。也许你用你的编译器得到了不同的输出，但除非你强制它，你不能确定没有填充。

## [20.6] `offsetof` {#offsetof number="20.6"}

In the previous section, we saw that the compiler could inject padding bytes at will inside a structure.

> 在上一节中，我们看到编译器可以随意在结构内部注入填充字节。

What if we needed to know where those were? We can measure it with `offsetof`, defined in `<stddef.h>`.

> 如果我们需要知道这些在哪里？我们可以使用 `offsetof`，它定义在 `<stddef.h>` 中来测量它。

Let's modify the code from above to print the offsets of the individual fields in the `struct`:

> 让我们修改上面的代码，打印 `struct` 中各个字段的偏移量：

::: {#cb423 .sourceCode}

```c
#include <stdio.h>
#include <stddef.h>

struct foo {
    int a;
    char b;
    int c;
    char d;
};

int main(void)
{
    printf("%zu\n", offsetof(struct foo, a));
    printf("%zu\n", offsetof(struct foo, b));
    printf("%zu\n", offsetof(struct foo, c));
    printf("%zu\n", offsetof(struct foo, d));
}
```

:::

For me, this outputs:

::: {#cb424 .sourceCode}

```{.sourceCode .default}
0
4
8
12
```

:::

indicating that we're using 4 bytes for each of the fields. It's a little weird, because `char` is only 1 byte, right? The compiler is putting 3 padding bytes after each `char` so that all the fields are 4 bytes long. Presumably this will run faster on my CPU.

> 指出我们为每个字段使用 4 个字节。这有点奇怪，因为 `char` 只有 1 个字节，对吗？编译器在每个 `char` 后面添加 3 个填充字节，以使所有字段长度为 4 个字节。据推测，这将在我的 CPU 上运行得更快。

## [20.7] Fake OOP {#fake-oop number="20.7"}

There's a slightly abusive thing that's sort of OOP-like that you can do with `struct` s.

> 你可以用 `struct` 做一些略带滥用性质的、类似面向对象编程的事情。

Since the pointer to the `struct` is the same as a pointer to the first element of the `struct`, you can freely cast a pointer to the `struct` to a pointer to the first element.

> 由于指向结构体的指针与指向结构体第一个元素的指针相同，因此可以自由地将指向结构体的指针转换为指向结构体第一个元素的指针。

What this means is that we can set up a situation like this:

::: {#cb425 .sourceCode}

```c
struct parent {
    int a, b;
};

struct child {
    struct parent super;  // MUST be first
    int c, d;
};
```

:::

Then we are able to pass a pointer to a `struct child` to a function that expects either that _or_ a pointer to a `struct parent`!

> 那么我们就可以将一个指向 `struct child` 的指针传递给一个期望接收一个指向 `struct parent` 的指针的函数！

Because `struct parent super` is the first item in the `struct child`, a pointer to any `struct child` is the same as a pointer to that `super` field[^135^].

> 因为 `struct parent super` 是 `struct child` 中的第一个项目，所以指向任何 `struct child` 的指针都与指向该 `super` 字段的指针相同。

Let's set up an example here. We'll make `struct` s as above, but then we'll pass a pointer to a `struct child` to a function that needs a pointer to a `struct parent`... and it'll still work.

> 让我们在这里设置一个例子。我们将创建上述的 `struct`，然后将一个 `struct child` 的指针传递给一个需要一个 `struct parent` 指针的函数...它仍然可以正常工作。

::: {#cb426 .sourceCode}

```c
#include <stdio.h>

struct parent {
    int a, b;
};

struct child {
    struct parent super;  // MUST be first
    int c, d;
};

// Making the argument `void*` so we can pass any type into it
// (namely a struct parent or struct child)
void print_parent(void *p)
{
    // Expects a struct parent--but a struct child will also work
    // because the pointer points to the struct parent in the first
    // field:
    struct parent *self = p;

    printf("Parent: %d, %d\n", self->a, self->b);
}

void print_child(struct child *self)
{
    printf("Child: %d, %d\n", self->c, self->d);
}

int main(void)
{
    struct child c = {.super.a=1, .super.b=2, .c=3, .d=4};

    print_child(&c);
    print_parent(&c);  // Also works even though it's a struct child!
}
```

:::

See what we did on the last line of `main()`? We called `print_parent()` but passed a `struct child*` as the argument! Even though `print_parent()` needs the argument to point to a `struct parent`, we're _getting away with it_ because the first field in the `struct child` is a `struct parent`.

> 看看我们在 `main()` 的最后一行做了什么？我们调用了 `print_parent()`，但是传入了一个 `struct child*` 作为参数！尽管 `print_parent()` 需要参数指向一个 `struct parent`，但是我们_逃脱了_，因为 `struct child` 的第一个字段是一个 `struct parent`。

Again, this works because a pointer to a `struct` has the same value as a pointer to the first field in that `struct`.

> 再次，这是因为指向 `struct` 的指针与指向该 `struct` 的第一个字段的指针的值相同。

This all hinges on this part of the spec:

> **§6.7.2.1¶15** \[...\] A pointer to a structure object, suitably converted, points to its initial member \[...\], and vice versa.

and

> **§6.5¶7** An object shall have its stored value accessed only by an lvalue expression that has one of the following types:
>
> - a type compatible with the effective type of the object
> - \[...\]

and my assumption that "suitably converted" means "cast to the effective type of the initial member".

> 我的假设是"适当转换"意味着"转换为初始成员的有效类型"。

## [20.8] Bit-Fields {#bit-fields number="20.8"}

In my experience, these are rarely used, but you might see them out there from time to time, especially in lower-level applications that pack bits together into larger spaces.

> 在我的经验中，这些很少被使用，但您可能会时不时地在较低级别的应用程序中看到它们，特别是将位打包到更大空间中的应用程序。

Let's take a look at some code to demonstrate a use case:

::: {#cb427 .sourceCode}

```c
#include <stdio.h>

struct foo {
    unsigned int a;
    unsigned int b;
    unsigned int c;
    unsigned int d;
};

int main(void)
{
    printf("%zu\n", sizeof(struct foo));
}
```

:::

For me, this prints `16`. Which makes sense, since `unsigned` s are 4 bytes on my system.

> 对我来说，这会打印出 `16`。这是有意义的，因为在我的系统上，`无符号` 的字节数是 4 个。

But what if we knew that all the values that were going to be stored in `a` and `b` could be stored in 5 bits, and the values in `c`, and `d` could be stored in 3 bits? That's only a total 16 bits. Why have 128 bits reserved for them if we're only going to use 16?

> 如果我们知道可以用 5 位来存储 a 和 b 中的所有值，而 c 和 d 中的值可以用 3 位来存储，那么只需要 16 位就可以了，为什么要预留 128 位呢？

Well, we can tell C to pretty-please try to pack these values in. We can specify the maximum number of bits that values can take (from 1 up the size of the containing type).

> 嗯，我们可以让 C 语言尽量把这些值打包起来。我们可以指定值所能占用的最大位数(从 1 开始到包含类型的大小)。

We do this by putting a colon after the field name, followed by the field width in bits.

> 我们通过在字段名称后面加上冒号，然后跟上字段宽度的位数来实现这一点。

::: {#cb428 .sourceCode startfrom="3"}

```c
struct foo {
    unsigned int a:5;
    unsigned int b:5;
    unsigned int c:3;
    unsigned int d:3;
};
```

:::

Now when I ask C how big my `struct foo` is, it tells me 4! It was 16 bytes, but now it's only 4. It has "packed" those 4 values down into 4 bytes, which is a four-fold memory savings.

> 现在当我问 C 有多大的 `struct foo` 时，它告诉我 4！它原来是 16 字节，现在只有 4 字节。它把这 4 个值压缩到 4 字节中，节省了 4 倍的内存。

The tradeoff is, of course, that the 5-bit fields can only hold values from 0-31 and the 3-bit fields can only hold values from 0-7. But life's all about compromise, after all.

> 交换的是，5 位字段只能保存 0-31 的值，而 3 位字段只能保存 0-7 的值。但毕竟，生活就是要做出妥协。

### [20.8.1] Non-Adjacent Bit-Fields {#non-adjacent-bit-fields number="20.8.1"}

A gotcha: C will only combine **adjacent** bit-fields. If they're interrupted by non-bit-fields, you get no savings:

> C 只会合并相邻的位域，如果它们被非位域打断，你就无法节省空间。

::: {#cb429 .sourceCode}

```c
struct foo {            // sizeof(struct foo) == 16 (for me)
    unsigned int a:1;   // since a is not adjacent to c.
    unsigned int b;
    unsigned int c:1;
    unsigned int d;
};
```

:::

In that example, since `a` is not adjacent to `c`, they are both "packed" in their own `int` s.

> 在这个例子中，由于 a 与 c 不相邻，它们都被“打包”在自己的 int 中。

So we have one `int` each for `a`, `b`, `c`, and `d`. Since my `int` s are 4 bytes, that's a grand total of 16 bytes.

> 所以我们每个 `a`、`b`、`c` 和 `d` 有一个 `int`。由于我的 `int` 是 4 个字节，总共是 16 个字节。

A quick rearrangement yields some space savings from 16 bytes down to 12 bytes (on my system):

> 快速重新排列可以将字节数从 16 字节减少到 12 字节(在我的系统上)。

::: {#cb430 .sourceCode}

```c
struct foo {            // sizeof(struct foo) == 12 (for me)
    unsigned int a:1;
    unsigned int c:1;
    unsigned int b;
    unsigned int d;
};
```

:::

And now, since `a` is next to `c`, the compiler puts them together into a single `int`.

> 现在，由于'a'紧挨着'c'，编译器将它们合并成一个整数。

So we have one `int` for a combined `a` and `c`, and one `int` each for `b` and `d`. For a grand total of 3 `int` s, or 12 bytes.

> 所以我们有一个 `int` 用于组合 `a` 和 `c`，还有一个 `int` 分别用于 `b` 和 `d`。总共 3 个 `int`，或者 12 个字节。

Put all your bitfields together to get the compiler to combine them.

### [20.8.2] Signed or Unsigned `int` s {#signed-or-unsigned-ints number="20.8.2"}

If you just declare a bit-field to be `int`, the different compilers will treat it as `signed` or `unsigned`. Just like the situation with `char`.

> 如果你只是声明一个位域是 `int`，不同的编译器会将其视为 `signed` 或 `unsigned`，就像 `char` 的情况一样。

Be specific about the signedness when using bit-fields.

### [20.8.3] Unnamed Bit-Fields {#unnamed-bit-fields number="20.8.3"}

In some specific circumstances, you might need to reserve some bits for hardware reasons, but not need to use them in code.

> 在某些特定情况下，您可能需要出于硬件原因保留一些位，但不需要在代码中使用它们。

For example, let's say you have a byte where the top 2 bits have a meaning, the bottom 1 bit has a meaning, but the middle 5 bits do not get used by you[^136^].

> 例如，假设你有一个字节，其中顶部 2 位有意义，底部 1 位有意义，但中间 5 位没有被你使用[^136^](＃fn136){＃fnref136 。脚注引用 role =“doc-noteref”}。

We _could_ do something like this:

::: {#cb431 .sourceCode}

```c
struct foo {
    unsigned char a:2;
    unsigned char dummy:5;
    unsigned char b:1;
};
```

:::

And that works---in our code we use `a` and `b`, but never `dummy`. It's just there to eat up 5 bits to make sure `a` and `b` are in the "required" (by this contrived example) positions within the byte.

> 我们的代码中使用了 `a` 和 `b`，但从不使用 `dummy`，它只是为了占据 5 位，以确保 `a` 和 `b` 在字节中处于所需(由这个约定的例子)的位置。

C allows us a way to clean this up: _unnamed bit-fields_. You can just leave the name (`dummy`) out in this case, and C is perfectly happy for the same effect:

> C 允许我们清理这个：_未命名的位域_。在这种情况下，可以省略名称(`dummy`)，C 也完全可以接受，以达到同样的效果：

::: {#cb432 .sourceCode}

```c
struct foo {
    unsigned char a:2;
    unsigned char :5;   // <-- unnamed bit-field!
    unsigned char b:1;
};
```

:::

### [20.8.4] Zero-Width Unnamed Bit-Fields {#zero-width-unnamed-bit-fields number="20.8.4"}

Some more esoterica out here... Let's say you were packing bits into an `unsigned int`, and you needed some adjacent bit-fields to pack into the _next_ `unsigned int`.

> 如果你需要把一些相邻的位字段打包到下一个无符号整数中，那么在这里有更多的深奥知识...

That is, if you do this:

::: {#cb433 .sourceCode}

```c
struct foo {
    unsigned int a:1;
    unsigned int b:2;
    unsigned int c:3;
    unsigned int d:4;
};
```

:::

the compiler packs all those into a single `unsigned int`. But what if you needed `a` and `b` in one `int`, and `c` and `d` in a different one?

> 编译器将所有这些打包到一个无符号整数中。但是如果你需要将 a 和 b 放在一个整数中，将 c 和 d 放在另一个整数中怎么办？

There's a solution for that: put an unnamed bit-field of width `0` where you want the compiler to start anew with packing bits in a different `int`:

> 这有一个解决方案：在你想要编译器从新开始在不同的 int 中打包位的地方放置一个未命名的宽度为 0 的位域。

::: {#cb434 .sourceCode}

```c
struct foo {
    unsigned int a:1;
    unsigned int b:2;
    unsigned int :0;   // <--Zero-width unnamed bit-field
    unsigned int c:3;
    unsigned int d:4;
};
```

:::

It's analogous to an explicit page break in a word processor. You're telling the compiler, "Stop packing bits in this `unsigned`, and start packing them in the next one."

> 这类似于文字处理软件中的显式分页符。你在告诉编译器：“停止在这个 `unsigned` 中填充位，开始在下一个中填充位。”

By adding the zero-width unnamed bit field in that spot, the compiler puts `a` and `b` in one `unsigned int`, and `c` and `d` in another `unsigned int`. Two total, for a size of 8 bytes on my system (`unsigned int` s are 4 bytes each).

> 通过在那个位置添加零宽度未命名位域，编译器将 `a` 和 `b` 放入一个 `unsigned int` 中，将 `c` 和 `d` 放入另一个 `unsigned int` 中。在我的系统上，总共有两个，大小为 8 字节(`unsigned int` 每个 4 字节)。

## [20.9] Unions {#unions number="20.9"}

These are basically just like `struct` s, except the fields overlap in memory. The `union` will be only large enough for the largest field, and you can only use one field at a time.

> 这些基本上就像 `struct` 一样，只是字段在内存中重迭。 `union` 只会足够大以容纳最大的字段，您一次只能使用一个字段。

It's a way to reuse the same memory space for different types of data.

You declare them just like `struct` s, except it's `union`. Take a look at this:

> 你像声明 `struct` 一样声明它们，只是它是 `union`。看看这个：

::: {#cb435 .sourceCode}

```c
union foo {
    int a, b, c, d, e, f;
    float g, h;
    char i, j, k, l;
};
```

:::

Now, that's a lot of fields. If this were a `struct`, my system would tell me it took 36 bytes to hold it all.

> 现在，这可是很多字段。如果这是一个'struct'，我的系统会告诉我需要 36 个字节来容纳它们。

But it's a `union`, so all those fields overlap in the same stretch of memory. The biggest one is `int` (or `float`), taking up 4 bytes on my system. And, indeed, if I ask for the `sizeof` the `union foo`, it tells me 4!

> 但它是一个联合，所以所有这些字段都在同一块内存中重迭。最大的是 int(或 float)，在我的系统上占用 4 个字节。而且，如果我询问 union foo 的 sizeof，它告诉我 4！

The tradeoff is that you can only portably use one of those fields at a time. However...

> 交换是你一次只能可移植地使用其中一个字段。但是...

### [20.9.1] Unions and Type Punning {#union-type-punning number="20.9.1"}

You can non-portably write to one `union` field and read from another!

Doing so is called [type punning](https://en.wikipedia.org/wiki/Type_punning)[^137^], and you'd use it if you really knew what you were doing, typically with some kind of low-level programming.

> 这样做被称为[类型双关](https://en.wikipedia.org/wiki/Type_punning)[^137^], 如果你真的知道自己在做什么，通常是在做一些低级编程时会用到它。

Since the members of a union share the same memory, writing to one member necessarily affects the others. And if you read from one what was written to another, you get some weird effects.

> 由于工会成员共享同一个内存，写入一个成员自然也会影响其他成员。如果你从一个成员那里读取写给另一个成员的内容，就会产生一些奇怪的效果。

::: {#cb436 .sourceCode}

```c
#include <stdio.h>

union foo {
    float b;
    short a;
};

int main(void)
{
    union foo x;

    x.b = 3.14159;

    printf("%f\n", x.b);  // 3.14159, fair enough

    printf("%d\n", x.a);  // But what about this?
}
```

:::

On my system, this prints out:

```
3.141590
4048
```

because under the hood, the object representation for the float `3.14159` was the same as the object representation for the short `4048`. On my system. Your results may vary.

> 因为在底层，浮点数 `3.14159` 的对象表示与短数 `4048` 的对象表示相同。在我的系统上，结果可能会有所不同。

### [20.9.2] Pointers to `union` s {#pointers-to-unions number="20.9.2"}

If you have a pointer to a `union`, you can cast that pointer to any of the types of the fields in that `union` and get the values out that way.

> 如果你有一个指向联合体的指针，你可以把这个指针转换成联合体中任何一种类型，然后从中取出值。

In this example, we see that the `union` has `int` s and `float` s in it. And we get pointers to the `union`, but we cast them to `int*` and `float*` types (the cast silences compiler warnings). And then if we dereference those, we see that they have the values we stored directly in the `union`.

> 在这个例子中，我们看到联合体中有整数和浮点数。我们得到指向联合体的指针，但我们将它们转换为 int *和 float *类型(转换可以消除编译器警告)。然后，如果我们解引用它们，我们会看到它们具有我们直接存储在联合体中的值。

::: {#cb438 .sourceCode}

```c
#include <stdio.h>

union foo {
    int a, b, c, d, e, f;
    float g, h;
    char i, j, k, l;
};

int main(void)
{
    union foo x;

    int *foo_int_p = (int *)&x;
    float *foo_float_p = (float *)&x;

    x.a = 12;
    printf("%d\n", x.a);           // 12
    printf("%d\n", *foo_int_p);    // 12, again

    x.g = 3.141592;
    printf("%f\n", x.g);           // 3.141592
    printf("%f\n", *foo_float_p);  // 3.141592, again
}
```

:::

The reverse is also true. If we have a pointer to a type inside the `union`, we can cast that to a pointer to the `union` and access its members.

> 反之亦然。如果我们在联合体内有一个指向类型的指针，我们可以将其转换为指向联合体的指针，并访问其成员。

::: {#cb439 .sourceCode}

```c
union foo x;
int *foo_int_p = (int *)&x;             // Pointer to int field
union foo *p = (union foo *)foo_int_p;  // Back to pointer to union

p->a = 12;  // This line the same as...
x.a = 12;   // this one.
```

:::

All this just lets you know that, under the hood, all these values in a `union` start at the same place in memory, and that's the same as where the entire `union` is.

> 所有这些只是让你知道，在底层，联合中的所有这些值都从内存中的同一个位置开始，这就是整个联合的位置。

### [20.9.3] Common Initial Sequences in Unions {#common-initial-sequences-in-unions number="20.9.3"}

If you have a `union` of `struct` s, and all those `struct` s begin with a _common initial sequence_, it's valid to access members of that sequence from any of the `union` members.

> 如果你有一个结构体的联合，并且所有这些结构体都以一个共同的初始序列开头，那么从联合的任何成员中访问该序列的成员是有效的。

What?

Here are two `struct` s with a common initial sequence:

::: {#cb440 .sourceCode}

```c
struct a {
    int x;     //
    float y;   // Common initial sequence

    char *p;
};

struct b {
    int x;     //
    float y;   // Common initial sequence

    double *p;
    short z;
};
```

:::

Do you see it? It's that they start with `int` followed by `float`---that's the common initial sequence. The members in the sequence of the `struct` s have to be compatible types. And we see that with `x` and `y`, which are `int` and `float` respectively.

> 你看到了吗？它们以 `int` 开头，然后是 `float`——这是常见的初始序列。结构体序列中的成员必须是兼容类型。我们可以看到 `x` 和 `y`，它们分别是 `int` 和 `float`。

Now let's build a union of these:

::: {#cb441 .sourceCode}

```c
union foo {
    struct a sa;
    struct b sb;
};
```

:::

What this rule tells us is that we're guaranteed that the members of the common initial sequences are interchangeable in code. That is:

> 这条规则告诉我们，我们可以保证代码中的公共初始序列成员是可互换的。也就是说：

- `f.sa.x` is the same as `f.sb.x`.

and

- `f.sa.y` is the same as `f.sb.y`.

Because fields `x` and `y` are both in the common initial sequence.

Also, the names of the members in the common initial sequence don't matter---all that matters is that the types are the same.

> 也就是说，共同初始序列中成员的名称并不重要---重要的是类型是相同的。

All together, this allows us a way to safely add some shared information between `struct` s in the `union`. The best example of this is probably using a field to determine the type of `struct` out of all the `struct` s in the `union` that is currently "in use".

> 所有这些加在一起，让我们有一种安全的方式来在 union 中添加一些共享信息。最好的例子可能是使用一个字段来确定当前“使用”的 union 中的 struct 类型。

That is, if we weren't allowed this and we passed the `union` to some function, how would that function know which member of the `union` was the one it should look at?

> 如果我们不允许这样做，并将这个联合传递给某个函数，那么这个函数如何知道应该查看哪个联合成员呢？

Take a look at these `struct` s. Note the common initial sequence:

::: {#cb442 .sourceCode}

```c
#include <stdio.h>

struct common {
    int type;   // common initial sequence
};

struct antelope {
    int type;   // common initial sequence

    int loudness;
};

struct octopus {
    int type;   // common initial sequence

    int sea_creature;
    float intelligence;
};
```

:::

Now let's throw them into a `union`:

::: {#cb443 .sourceCode startfrom="20"}

```c
union animal {
    struct common common;
    struct antelope antelope;
    struct octopus octopus;
};
```

:::

Also, please indulge me these two `#define` s for the demo:

::: {#cb444 .sourceCode startfrom="26"}

```c
#define ANTELOPE 1
#define OCTOPUS  2
```

:::

So far, nothing special has happened here. It seems like the `type` field is completely useless.

> 到目前为止，这里没有发生什么特别的事情。看起来 `type` 字段完全没有用处。

But now let's make a generic function that prints a `union animal`. It has to somehow be able to tell if it's looking at a `struct antelope` or a `struct octopus`.

> 现在让我们创建一个通用函数，打印一个“联合动物”。它必须以某种方式能够判断它是在看“羚羊结构”还是“章鱼结构”。

Because of the magic of common initial sequences, it can look up the animal type in any of these places for a particular `union animal x`:

> 由于常见初始序列的魔力，它可以在这些地方查找特定的“联合动物 x”的动物类型：

::: {#cb445 .sourceCode}

```c
int type = x.common.type;    \\ or...
int type = x.antelope.type;  \\ or...
int type = x.octopus.type;
```

:::

All those refer to the same value in memory.

And, as you might have guessed, the `struct common` is there so code can agnostically look at the type without mentioning a particular animal.

> 而且，正如你可能已经猜到的，`struct common` 存在是为了让代码可以不提及特定动物就可以不受限制地查看类型。

Let's look at the code to print a `union animal`:

::: {#cb446 .sourceCode startfrom="29"}

```c
void print_animal(union animal *x)
{
    switch (x->common.type) {
        case ANTELOPE:
            printf("Antelope: loudness=%d\n", x->antelope.loudness);
            break;

        case OCTOPUS:
            printf("Octopus : sea_creature=%d\n", x->octopus.sea_creature);
            printf("          intelligence=%f\n", x->octopus.intelligence);
            break;

        default:
            printf("Unknown animal type\n");
    }

}

int main(void)
{
    union animal a = {.antelope.type=ANTELOPE, .antelope.loudness=12};
    union animal b = {.octopus.type=OCTOPUS, .octopus.sea_creature=1,
                                       .octopus.intelligence=12.8};

    print_animal(&a);
    print_animal(&b);
}
```

:::

See how on line 29 we're just passing in the `union`---we have no idea what type of animal `struct` is in use within it.

> 看看我们在第 29 行只是传入 `union`---我们不知道在其中使用的 `struct` 是什么类型的动物。

But that's OK! Because on line 31 we check the type to see if it's an antelope or an octopus. And then we can look at the proper `struct` to get the members.

> 没关系！因为在第 31 行，我们检查类型，看它是羚羊还是章鱼。然后我们可以看看正确的 `struct` 来获取成员。

It's definitely possible to get this same effect using just `struct` s, but you can do it this way if you want the memory-saving effects of a `union`.

> 只使用 `struct` 也可以达到同样的效果，但如果你想要节省内存，可以使用 `union` 来实现。

## [20.10] Unions and Unnamed Structs {#unions-and-unnamed-structs number="20.10"}

You know how you can have an unnamed `struct`, like this:

::: {#cb447 .sourceCode}

```c
struct {
    int x, y;
} s;
```

:::

That defines a variable `s` that is of anonymous `struct` type (because the `struct` has no name tag), with members `x` and `y`.

> 这定义了一个变量 `s`，它是一个匿名 `struct` 类型(因为 `struct` 没有名称标签)，具有成员 `x` 和 `y`。

So things like this are valid:

::: {#cb448 .sourceCode}

```c
s.x = 34;
s.y = 90;

printf("%d %d\n", s.x, s.y);
```

:::

Turns out you can drop those unnamed `struct` s in `union` s just like you might expect:

> 结果你可以像你预期的那样，在联合中丢弃那些未命名的结构体：

::: {#cb449 .sourceCode}

```c
union foo {
    struct {       // unnamed!
        int x, y;
    } a;

    struct {       // unnamed!
        int z, w;
    } b;
};
```

:::

And then access them as per normal:

::: {#cb450 .sourceCode}

```c
union foo f;

f.a.x = 1;
f.a.y = 2;
f.b.z = 3;
f.b.w = 4;
```

:::

No problem!

## [20.11] Passing and Returning `struct` s and `union` s {#passing-and-returning-structs-and-unions number="20.11"}

You can pass a `struct` or `union` to a function by value (as opposed to a pointer to it)---a copy of that object to the parameter will be made as if by assignment as per usual.

> 你可以通过值(而不是指向它的指针)将 `struct` 或 `union` 传递给函数，就像通常一样，将该对象的副本分配给参数。

You can also return a `struct` or `union` from a function and it is also passed by value back.

> 你也可以从一个函数返回一个 `struct` 或 `union`，它也是以值的方式传回的。

::: {#cb451 .sourceCode}

```c
#include <stdio.h>

struct foo {
    int x, y;
};

struct foo f(void)
{
    return (struct foo){.x=34, .y=90};
}

int main(void)
{
    struct foo a = f();  // Copy is made

    printf("%d %d\n", a.x, a.y);
}
```

:::

Fun fact: if you do this, you can use the `.` operator right off the function call:

> 事实有趣：如果你这样做，你可以直接在函数调用中使用“.”操作符。

::: {#cb452 .sourceCode startfrom="16"}

```c
    printf("%d %d\n", f().x, f().y);
```

:::

(Of course that example calls the function twice, inefficiently.)

And the same holds true for returning pointers to `struct` s and `union` s---just be sure to use the `->` arrow operator in that case.

> 同样的情况也适用于返回指向 `struct` 和 `union` 的指针---只需确保在这种情况下使用 `->` 箭头操作符即可。

# [21] Characters and Strings II {#characters-and-strings-ii number="21"}

We've talked about how `char` types are actually just small integer types... but it's the same for a character in single quotes.

> 我们讨论过 `char` 类型实际上只是小整数类型...但对于单引号中的字符也是一样的。

But a string in double quotes is type `const char *`.

Turns out there are few more types of strings and characters, and it leads down one of the most infamous rabbit holes in the language: the whole multibyte/wide/Unicode/localization thingy.

> 原来还有更多类型的字符串和字符，这就引出了语言中最臭名昭着的兔子洞之一：多字节/宽/Unicode/本地化的东西。

We're going to peer into that rabbit hole, but not go in. ...Yet!

## [21.1] Escape Sequences {#escape-sequences number="21.1"}

We're used to strings and characters with regular letters, punctuation, and numbers:

> 我们习惯于使用带有常规字母、标点符号和数字的字符串和字符：

::: {#cb453 .sourceCode}

```c
char *s = "Hello!";
char t = 'c';
```

:::

But what if we want some special characters in there that we can't type on the keyboard because they don't exist (e.g. "€"), or even if we want a character that's a single quote? We clearly can't do this:

> 如果我们想在里面添加一些无法通过键盘输入的特殊字符(例如“€”)，或者甚至想要一个单引号，我们显然无法这样做：

::: {#cb454 .sourceCode}

```c
char t = ''';
```

:::

To do these things, we use something called _escape sequences_. These are the backslash character (`\`) followed by another character. The two (or more) characters together have special meaning.

> 我们使用一种叫做逃离序列的东西来做这些事情。这些是由反斜杠字符(\)后跟另一个字符组成的。这两个(或更多)字符在一起有特殊的意义。

For our single quote character example, we can put an escape (that is, `\`) in front of the central single quote to solve it:

> 对于我们的单引号字符示例，我们可以在中间单引号前面加上转义字符(即 `\`)来解决它：

::: {#cb455 .sourceCode}

```c
char t = '\'';
```

:::

Now C knows that `\'` means just a regular quote we want to print, not the end of the character sequence.

> 现在 C 知道'表示一个普通的引号，我们想要打印，而不是字符序列的结束。

You can say either "backslash" or "escape" in this context ("escape that quote") and C devs will know what you're talking about. Also, "escape" in this context is different than your `Esc` key or the ASCII `ESC` code.

> 在这种情况下(“转义引号”)，你可以说“反斜杠”或“转义”，C 开发人员都会明白你的意思。此外，在这种情况下的“转义”与你的 `Esc` 键或 ASCII `ESC` 代码不同。

### [21.1.1] Frequently-used Escapes {#frequently-used-escapes number="21.1.1"}

In my humble opinion, these escape characters make up 99.2%[^138^] of all escapes.

> 在我看来，这些转义字符占据了 99.2％[^138^](＃fn138){＃fnref138 .footnote-ref role =“doc-noteref”}的所有转义字符。

---

Code Description

---

`\n` Newline character---when printing, continue subsequent output on the next line

`\'` Single quote---used for a single quote character constant

`\"` Double quote---used for a double quote in a string literal

## `\\` Backslash---used for a literal `\` in a string or character

Here are some examples of the escapes and what they output when printed.

::: {#cb456 .sourceCode}

```c
printf("Use \\n for newline\n");  // Use \n for newline
printf("Say \"hello\"!\n");       // Say "hello"!
printf("%c\n", '\'');             // '
```

:::

### [21.1.2] Rarely-used Escapes {#rarely-used-escapes number="21.1.2"}

But there are more escapes! You just don't see these as often.

---

Code Description

---

`\a` Alert. This makes the terminal make a sound or flash, or both!

`\b` Backspace. Moves the cursor back a character. Doesn't delete the character.

`\f` Formfeed. This moves to the next "page", but that doesn't have much modern meaning. On my system, this behaves like `\v`.

`\r` Return. Move to the beginning of the same line.

`\t` Horizontal tab. Moves to the next horizontal tab stop. On my machine, this lines up on columns that are multiples of 8, but YMMV.

`\v` Vertical tab. Moves to the next vertical tab stop. On my machine, this moves to the same column on the next line.

## `\?` Literal question mark. Sometimes you need this to avoid trigraphs, as shown below.

#### [21.1.2.1] Single Line Status Updates {#single-line-status-updates number="21.1.2.1"}

A use case for `\b` or `\r` is to show status updates that appear on the same line on the screen and don't cause the display to scroll. Here's an example that does a countdown from 10. (Note this makes use of the non-standard POSIX function `sleep()` from `<unistd.h>`---if you're not on a Unix-like, search for your platform and `sleep` for the equivalent.)

> `\b` 或 `\r` 的一个用例是在屏幕上显示同一行的状态更新，而不会导致显示滚动。这里有一个从 10 开始倒计时的示例(注意，它使用了非标准的 POSIX 函数 `sleep()`，来自 `<unistd.h>`——如果你不是在类 Unix 系统上，搜索你的平台和 `sleep` 以获得等效的函数)。

::: {#cb457 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>

int main(void)
{
    for (int i = 10; i >= 0; i--) {
        printf("\rT minus %d second%s... \b", i, i != 1? "s": "");

        fflush(stdout);  // Force output to update

        // Sleep for 1 second
        thrd_sleep(&(struct timespec){.tv_sec=1}, NULL);
    }

    printf("\rLiftoff!             \n");
}
```

:::

Quite a few things are happening on line 7. First of all, we lead with a `\r` to get us to the beginning of the current line, then we overwrite whatever's there with the current countdown. (There's ternary operator out there to make sure we print `1 second` instead of `1 seconds`.)

> 在第 7 行发生了不少事情。首先，我们用 `\r` 开头，让我们回到当前行的开头，然后用当前倒计时覆盖原来的内容。(有一个三元运算符可以确保我们打印 `1秒` 而不是 `1秒钟`。)

Also, there's a space after the `...` That's so that we properly overwrite the last `.` when `i` drops from `10` to `9` and we get a column narrower. Try it without the space to see what I mean.

> 此外，在 `...` 后面有一个空格。这样，当 `i` 从 `10` 减少到 `9` 时，我们可以正确覆盖最后的 `.`。不加空格试试，你就会明白我的意思。

And we wrap it up with a `\b` to back up over that space so the cursor sits at the exact end of the line in an aesthetically-pleasing way.

> 最后，我们使用\b 来回退到空格，以便光标以美观的方式停留在行末。

Note that line 14 also has a lot of spaces at the end to overwrite the characters that were already there from the countdown.

> 注意第 14 行也有很多空格，用来覆盖倒计时中已经存在的字符。

Finally, we have a weird `fflush(stdout)` in there, whatever that means. Short answer is that most terminals are _line buffered_ by default, meaning they don't actually display anything until a newline character is encountered. Since we don't have a newline (we just have `\r`), without this line, the program would just sit there until `Liftoff!` and then print everything all in one instant. `fflush()` overrides this behavior and forces output to happen _right now_.

> 最后，我们在那里有一个奇怪的 `fflush(stdout)`，不管那是什么意思。简短的答案是，大多数终端默认情况下是行缓冲的，这意味着它们实际上不会显示任何东西，直到遇到换行符。由于我们没有换行符(我们只有 `\r`)，没有这一行，程序只会坐在那里，直到 `Liftoff！` 然后一次性打印所有内容。 `fflush()` 覆盖了这种行为，并强制立即发生输出。

#### [21.1.2.2] The Question Mark Escape {#the-question-mark-escape number="21.1.2.2"}

Why bother with this? After all, this works just fine:

::: {#cb458 .sourceCode}

```c
printf("Doesn't it?\n");
```

:::

And it works fine with the escape, too:

::: {#cb459 .sourceCode}

```c
printf("Doesn't it\?\n");   // Note \?
```

:::

So what's the point??!

Let's get more emphatic with another question mark and an exclamation point:

> 让我们用另一个问号和感叹号变得更有力量！

::: {#cb460 .sourceCode}

```c
printf("Doesn't it??!\n");
```

:::

When I compile this, I get this warning:

::: {#cb461 .sourceCode}

```zsh
foo.c: In function ‘main’:
foo.c:5:23: warning: trigraph ??! converted to | [-Wtrigraphs]
    5 |     printf("Doesn't it??!\n");
      |
```

:::

And running it gives this unlikely result:

::: {#cb462 .sourceCode}

```{.sourceCode .default}
Doesn't it|
```

:::

So _trigraphs_? What the heck is this??!

I'm sure we'll revisit this dusty corner of the language later, but the short of it is the compiler looks for certain triplets of characters starting with `??` and it substitutes other characters in their place. So if you're on some ancient terminal without a pipe symbol (`|`) on the keyboard, you can type `??!` instead.

> 我相信我们以后会再次探讨这个语言的这个掘角角落，但简单来说，编译器会查找以 `??` 开头的三个字符，并用其他字符替换它们。因此，如果您使用的是一些没有管道符号(`|`)的古老终端，您可以改为输入 `??！`。

You can fix this by escaping the second question mark, like so:

::: {#cb463 .sourceCode}

```c
printf("Doesn't it?\?!\n");
```

:::

And then it compiles and works as-expected.

These days, of course, no one ever uses trigraphs. But that whole `??!` does sometimes appear if you decide to use it in a string for emphasis.

> 这些日子，当然，没有人会使用三字符组。但是，如果你决定在一个字符串中使用它来强调，那么整个 `??!` 有时会出现。

### [21.1.3] Numeric Escapes {#numeric-escapes number="21.1.3"}

In addition, there are ways to specify numeric constants or other character values inside strings or character constants.

> 此外，还有方法可以在字符串或字符常量中指定数值常量或其他字符值。

If you know an octal or hexadecimal representation of a byte, you can include that in a string or character constant.

> 如果你知道一个字节的八进制或十六进制表示，你可以将它包含在字符串或字符常量中。

The following table has example numbers, but any hex or octal numbers may be used. Pad with leading zeros if necessary to read the proper digit count.

> 以下表格给出了示例数字，但可以使用任何十六进制或八进制数字。如有必要，请用前导零填充以获得正确的数字位数。

---

Code Description

---

`\123` Embed the byte with octal value `123`, 3 digits exactly.

`\x4D` Embed the byte with hex value `4D`, 2 digits.

`\u2620` Embed the Unicode character at code point with hex value `2620`, 4 digits.

## `\U0001243F` Embed the Unicode character at code point with hex value `1243F`, 8 digits.

Here's an example of the less-commonly used octal notation to represent the letter `B` in between `A` and `C`. Normally this would be used for some kind of special unprintable character, but we have other ways to do that, below, and this is just an octal demo:

> 这是一个不太常用的八进制符号，用来表示字母 A 和 C 之间的字母 B。通常这种符号用于表示一些不可打印的特殊字符，但我们有其他方法来实现，下面是八进制演示：

::: {#cb464 .sourceCode}

```c
printf("A\102C\n");  // 102 is `B` in ASCII/UTF-8
```

:::

Note there's no leading zero on the octal number when you include it this way. But it does need to be three characters, so pad with leading zeros if you need to.

> 提示：以这种方式包含八进制数时，前导零不存在。但它需要三个字符，因此如果需要，请用前导零进行填充。

But far more common is to use hex constants these days. Here's a demo that you shouldn't use, but it demos embedding the UTF-8 bytes 0xE2, 0x80, and 0xA2 in a string, which corresponds to the Unicode "bullet" character (•).

> 但是现在更常用的是使用十六进制常量。这里有一个演示，你不应该使用，但它演示了在字符串中嵌入 UTF-8 字节 0xE2、0x80 和 0xA2，这对应于 Unicode 的“子弹”字符(•)。

::: {#cb465 .sourceCode}

```c
printf("\xE2\x80\xA2 Bullet 1\n");
printf("\xE2\x80\xA2 Bullet 2\n");
printf("\xE2\x80\xA2 Bullet 3\n");
```

:::

Produces the following output if you're on a UTF-8 console (or probably garbage if you're not):

> 如果您使用 UTF-8 控制台，则会产生以下输出(如果您不是，可能会产生垃圾)：

::: {#cb466 .sourceCode}

```{.sourceCode .default}
• Bullet 1
• Bullet 2
• Bullet 3
```

:::

But that's a crummy way to do Unicode. You can use the escapes `\u` (16-bit) or `\U` (32-bit) to just refer to Unicode by code point number. The bullet is `2022` (hex) in Unicode, so you can do this and get more portable results:

> 但这是一种糟糕的 Unicode 方式。您可以使用转义符 `\u`(16 位)或 `\U`(32 位)来引用 Unicode 的代码点数。子弹是 Unicode 中的 `2022`(十六进制)，因此您可以这样做以获得更多可移植的结果：

::: {#cb467 .sourceCode}

```c
printf("\u2022 Bullet 1\n");
printf("\u2022 Bullet 2\n");
printf("\u2022 Bullet 3\n");
```

:::

Be sure to pad `\u` with enough leading zeros to get to four characters, and `\U` with enough to get to eight.

> 确保在 `\u` 前面补足足够的零使其达到 4 个字符，而在 `\U` 前面补足足够的零使其达到 8 个字符。

For example, that bullet could be done with `\U` and four leading zeros:

::: {#cb468 .sourceCode}

```c
printf("\U00002022 Bullet 1\n");
```

:::

But who has time to be that verbose?

# [22] Enumerated Types: `enum` {#enumerated-types-enum number="22"}

C offers us another way to have constant integer values by name: `enum`.

For example:

::: {#cb469 .sourceCode}

```c
enum {
  ONE=1,
  TWO=2
};

printf("%d %d", ONE, TWO);  // 1 2
```

:::

In some ways, it can be better---or different---than using a `#define`. Key differences:

> 在某些方面，它可以比使用 `#define` 更好或不同。主要区别是：

- `enum` s can only be integer types.
- `#define` can define anything at all.
- `enum` s are often shown by their symbolic identifier name in a debugger.
- `#define` d numbers just show as raw numbers which are harder to know the meaning of while debugging.

> `#define` 定义的数字只会显示为原始数字，在调试时更难理解其含义。

Since they're integer types, they can be used any place integers can be used, including in array dimensions and `case` statements.

> 由于它们是整数类型，它们可以用在任何整数可以使用的地方，包括数组维度和 `case` 语句中。

Let's tear into this more.

## [22.1] Behavior of `enum` {#behavior-of-enum number="22.1"}

### [22.1.1] Numbering {#numbering number="22.1.1"}

`enum` s are automatically numbered unless you override them.

They start at `0`, and autoincrement up from there, by default:

::: {#cb470 .sourceCode}

```c
enum {
    SHEEP,  // Value is 0
    WHEAT,  // Value is 1
    WOOD,   // Value is 2
    BRICK,  // Value is 3
    ORE     // Value is 4
};

printf("%d %d\n", SHEEP, BRICK);  // 0 3
```

:::

You can force particular integer values, as we saw earlier:

::: {#cb471 .sourceCode}

```c
enum {
  X=2,
  Y=18,
  Z=-2
};
```

:::

Duplicates are not a problem:

::: {#cb472 .sourceCode}

```c
enum {
  X=2,
  Y=2,
  Z=2
};
```

:::

if values are omitted, numbering continues counting in the positive direction from whichever value was last specified. For example:

> 如果值被省略，编号将从上一次指定的值继续以正向方向计数。例如：

::: {#cb473 .sourceCode}

```c
enum {
  A,    // 0, default starting value
  B,    // 1
  C=4,  // 4, manually set
  D,    // 5
  E,    // 6
  F=3   // 3, manually set
  G,    // 4
  H     // 5
}
```

:::

### [22.1.2] Trailing Commas {#trailing-commas number="22.1.2"}

This is perfectly fine, if that's your style:

::: {#cb474 .sourceCode}

```c
enum {
  X=2,
  Y=18,
  Z=-2,   // <-- Trailing comma
};
```

:::

It's gotten more popular in languages of the recent decades so you might be pleased to see it.

> 近几十年来，它变得越来越受欢迎，所以你可能会很高兴看到它。

### [22.1.3] Scope {#scope-1 number="22.1.3"}

`enum` s scope as you'd expect. If at file scope, the whole file can see it. If in a block, it's local to that block.

It's really common for `enum` s to be defined in header files so they can be `#include` d at file scope.

> 这种将枚举定义在头文件中以便能够在文件范围内#include 的做法非常常见。

### [22.1.4] Style {#style number="22.1.4"}

As you've noticed, it's common to declare the `enum` symbols in uppercase (with underscores).

> 你可能已经注意到，通常使用大写(带下划线)来声明枚举符号。

This isn't a requirement, but is a very, very common idiom.

## [22.2] Your `enum` is a Type {#your-enum-is-a-type number="22.2"}

This is an important thing to know about `enum`: they're a type, analogous to how a `struct` is a type.

> 这是关于枚举的一件重要的事情要知道：它们是一种类型，类似于结构体是一种类型。

You can give them a tag name so you can refer to the type later and declare variables of that type.

> 你可以给它们一个标签名，这样你以后就可以引用这种类型，并声明该类型的变量。

Now, since `enum` s are integer types, why not just use `int`?

In C, the best reason for this is code clarity--it's a nice, typed way to describe your thinking in code. C (unlike C++) doesn't actually enforce any values being in range for a particular `enum`.

> 在 C 中，最好的理由是代码清晰度-它是一种很好的、类型化的方式来用代码描述你的思考。C(不像 C++)实际上不强制任何特定的枚举值在范围内。

Let's do an example where we declare a variable `r` of type `enum resource` that can hold those values:

> 让我们做一个例子，声明一个类型为 `enum resource` 的变量 `r`，它可以存储这些值：

::: {#cb475 .sourceCode}

```c
// Named enum, type is "enum resource"

enum resource {
    SHEEP,
    WHEAT,
    WOOD,
    BRICK,
    ORE
};

// Declare a variable "r" of type "enum resource"

enum resource r = BRICK;

if (r == BRICK) {
    printf("I'll trade you a brick for two sheep.\n");
}
```

:::

You can also `typedef` these, of course, though I personally don't like to.

> 你也可以对它们进行 `typedef`，不过我个人不喜欢这样做。

::: {#cb476 .sourceCode}

```c
typedef enum {
    SHEEP,
    WHEAT,
    WOOD,
    BRICK,
    ORE
} RESOURCE;

RESOURCE r = BRICK;
```

:::

Another shortcut that's legal but rare is to declare variables when you declare the `enum`:

> 另一种合法但不多见的快捷方式是在声明枚举时声明变量：

::: {#cb477 .sourceCode}

```c
// Declare an enum and some initialized variables of that type:

enum {
    SHEEP,
    WHEAT,
    WOOD,
    BRICK,
    ORE
} r = BRICK, s = WOOD;
```

:::

You can also give the `enum` a name so you can use it later, which is probably what you want to do in most cases:

> 你也可以给枚举起一个名字，这样你以后就可以使用它，这可能是你在大多数情况下想要做的。

::: {#cb478 .sourceCode}

```c
// Declare an enum and some initialized variables of that type:

enum resource {   // <-- type is now "enum resource"
    SHEEP,
    WHEAT,
    WOOD,
    BRICK,
    ORE
} r = BRICK, s = WOOD;
```

:::

In short, `enum` s are a great way to write nice, scoped, typed, clean code.

> 简而言之，`enum` 是编写优雅、范围限定、类型安全、干净代码的一种很好的方式。

# [23] Pointers III: Pointers to Pointers and More {#pointers-iii-pointers-to-pointers-and-more number="23"}

Here's where we cover some intermediate and advanced pointer usage. If you don't have pointers down well, review the previous chapters on [pointers](#pointers) and [pointer arithmetic](#pointers2) before starting on this stuff.

> 在这里，我们将涵盖一些中级和高级指针使用方法。如果您对指针不太了解，请先回顾有关[指针](#pointers)和[指针算术](#pointers2)的前几章，然后再开始学习这些内容。

## [23.1] Pointers to Pointers {#pointers-to-pointers number="23.1"}

If you can have a pointer to a variable, and a variable can be a pointer, can you have a pointer to a variable that it itself a pointer?

> 如果你可以拥有一个指向变量的指针，而且变量可以是一个指针，那么你可以拥有一个指向它自身是指针的变量的指针吗？

Yes! This is a pointer to a pointer, and it's held in variable of type pointer-pointer.

> 是的！这是一个指向指针的指针，它存储在指针-指针类型的变量中。

Before we tear into that, I want to try for a _gut feel_ for how pointers to pointers work.

> 在我们深入研究之前，我想尝试一下指针指向指针的直觉感受。

Remember that a pointer is just a number. It's a number that represents an index in computer memory, typically one that holds a value we're interested in for some reason.

> 记住指针只是一个数字。它是一个表示计算机内存中的索引的数字，通常是一个我们由于某种原因而感兴趣的值。

That pointer, which is a number, has to be stored somewhere. And that place is memory, just like everything else[^139^].

> 那个指针，它是一个数字，必须存储在某个地方。就像其他所有东西一样，那个地方就是内存。

But because it's stored in memory, it must have an index it's stored at, right? The pointer must have an index in memory where it is stored. And that index is a number. It's the address of the pointer. It's a pointer to the pointer.

> 但是由于它存储在内存中，它必须有一个存储它的索引，对吗？指针必须在内存中有一个索引。那个索引是一个数字。它是指针的地址。它是一个指向指针的指针。

Let's start with a regular pointer to an `int`, back from the earlier chapters:

> 让我们从前几章节中的一个普通 `int` 指针开始：

::: {#cb479 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int x = 3490;  // Type: int
    int *p = &x;   // Type: pointer to an int

    printf("%d\n", *p);  // 3490
}
```

:::

Straightforward enough, right? We have two types represented: `int` and `int*`, and we set up `p` to point to `x`. Then we can dereference `p` on line 8 and print out the value `3490`.

> 很简单吧？我们有两种类型：`int` 和 `int*`，然后我们把 `p` 设置为指向 `x`。然后我们可以在第 8 行解引用 `p` 并打印出值 `3490`。

But, like we said, we can have a pointer to any variable... so does that mean we can have a pointer to `p`?

> 但是，正如我们所说，我们可以拥有一个指向任何变量的指针...那么这是否意味着我们可以拥有一个指向 `p` 的指针？

In other words, what type is this expression?

::: {#cb480 .sourceCode}

```c
int x = 3490;  // Type: int
int *p = &x;   // Type: pointer to an int

&p  // <-- What type is the address of p? AKA a pointer to p?
```

:::

If `x` is an `int`, then `&x` is a pointer to an `int` that we've stored in `p` which is type `int*`. Follow? (Repeat this paragraph until you do!)

> 如果 x 是一个 int，那么&x 就是一个指向 int 的指针，我们将它存储在 p 中，p 的类型是 int*。明白了吗？(重复这段话，直到你明白为止！)

And therefore `&p` is a pointer to an `int*`, AKA a "pointer to a pointer to an `int`". AKA "`int`-pointer-pointer".

> 因此，&p 是一个指向 int*的指针，也就是所谓的“指向指向 int 的指针”，也就是“int 指针指针”。

Got it? (Repeat the previous paragraph until you do!)

We write this type with two asterisks: `int **`. Let's see it in action.

::: {#cb481 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int x = 3490;  // Type: int
    int *p = &x;   // Type: pointer to an int
    int **q = &p;  // Type: pointer to pointer to int

    printf("%d %d\n", *p, **q);  // 3490 3490
}
```

:::

Let's make up some pretend addresses for the above values as examples and see what these three variables might look like in memory. The address values, below are just made up by me for example purposes:

> 让我们为上述值制作一些假地址作为示例，看看这三个变量在内存中可能是什么样子。 下面的地址值是我为示例目的而编造的：

Variable Stored at Address Value Stored There

---

`x` `28350` `3490`---the value from the code
`p` `29122` `28350`---the address of `x`!
`q` `30840` `29122`---the address of `p`!

Indeed, let's try it for real on my computer[^140^] and print out the pointer values with `%p` and I'll do the same table again with actual references (printed in hex).

> 的确，让我们在我的电脑上实际尝试一下，并用 `%p` 打印出指针值，我会用实际的引用(以十六进制打印)再做一张表格。

Variable Stored at Address Value Stored There

---

`x` `0x7ffd96a07b94` `3490`---the value from the code
`p` `0x7ffd96a07b98` `0x7ffd96a07b94`---the address of `x`!
`q` `0x7ffd96a07ba0` `0x7ffd96a07b98`---the address of `p`!

You can see those addresses are the same except the last byte, so just focus on those.

> 你可以看到这些地址除了最后一个字节以外都是相同的，所以只需要关注那些。

On my system, `int` s are 4 bytes, which is why we're seeing the address go up by 4 from `x` to `p`[^141^] and then goes up by 8 from `p` to `q`. On my system, all pointers are 8 bytes.

> 在我的系统中，`int` 大小为 4 个字节，这就是为什么从 `x` 到 `p` 的地址增加 4 个字节，然后从 `p` 到 `q` 增加 8 个字节。在我的系统中，所有指针都是 8 个字节。

Does it matter if it's an `int*` or an `int**`? Is one more bytes than the other? Nope! Remember that all pointers are addresses, that is indexes into memory. And on my machine you can represent an index with 8 bytes... doesn't matter what's stored at that index.

> 这是 `int*` 还是 `int**` 有关系吗？其中一个比另一个多几个字节吗？不！记住，所有指针都是地址，也就是内存中的索引。在我的机器上，你可以用 8 个字节来表示一个索引...不管那个索引上存储的是什么都没关系。

Now check out what we did there on line 9 of the previous example: we _double dereferenced_ `q` to get back to our `3490`.

> 现在看看我们在前面例子的第 9 行做了什么：我们_双重解引用_ `q` 以获取我们的 `3490`。

This is the important bit about pointers and pointers to pointers:

- You can get a pointer to anything with `&` (including to a pointer!)
- You can get the thing a pointer points to with `*` (including a pointer!)

So you can think of `&` as being used to make pointers, and `*` being the inverse---it goes the opposite direction of `&`---to get to the thing pointed to.

> 所以你可以把 `&` 想象成用来创建指针，而 `*` 则相反——它与 `&` 相反，可以访问指针所指向的东西。

In terms of type, each time you `&`, that adds another pointer level to the type.

> 每次你使用'&'，在类型上就会增加一个指针层级。

If you have Then you run The result type is

---

`int x` `&x` `int *`
`int *x` `&x` `int **`
`int **x` `&x` `int ***`
`int ***x` `&x` `int ****`

And each time you use dereference (`*`), it does the opposite:

If you have Then you run The result type is

---

`int ****x` `*x` `int ***`
`int ***x` `*x` `int **`
`int **x` `*x` `int *`
`int *x` `*x` `int`

Note that you can use multiple `*` s in a row to quickly dereference, just like we saw in the example code with `**q`, above. Each one strips away one level of indirection.

> 注意，您可以在一行中使用多个 `*` 来快速解引用，就像我们在上面的 `**q` 示例代码中看到的那样。每个都会消除一个间接层次。

If you have Then you run The result type is

---

`int ****x` `***x` `int *`
`int ***x` `**x` `int *`
`int **x` `**x` `int`

In general, `&*E == E`[^142^]. The dereference "undoes" the address-of.

> 一般来说，“&*E == E”[^142^]。取消引用操作取消了地址。

But `&` doesn't work the same way---you can only do those one at a time, and have to store the result in an intermediate variable:

> 但是 `&` 不能以同样的方式工作---你只能一次做一个，并且必须将结果存储在一个中间变量中：

::: {#cb482 .sourceCode}

```c
int x = 3490;     // Type: int
int *p = &x;      // Type: int *, pointer to an int
int **q = &p;     // Type: int **, pointer to pointer to int
int ***r = &q;    // Type: int ***, pointer to pointer to pointer to int
int ****s = &r;   // Type: int ****, you get the idea
int *****t = &s;  // Type: int *****
```

:::

### [23.1.1] Pointer Pointers and `const` {#pointer-pointers-and-const number="23.1.1"}

If you recall, declaring a pointer like this:

::: {#cb483 .sourceCode}

```c
int *const p;
```

:::

means that you can't modify `p`. Trying to `p++` would give you a compile-time error.

> 这意味着你不能修改 `p`。尝试 `p++` 会给你一个编译时错误。

But how does that work with `int **` or `int ***`? Where does the `const` go, and what does it mean?

> 但是，`int **` 或 `int ***` 怎么样？`const` 放在哪里，意思是什么？

Let's start with the simple bit. The `const` right next to the variable name refers to that variable. So if you want an `int***` that you can't change, you can do this:

> 让我们从简单的部分开始。变量名旁边的 `const` 指的是该变量。因此，如果您想要一个不能更改的 `int***`，您可以这样做：

::: {#cb484 .sourceCode}

```c
int ***const p;

p++;  // Not allowed
```

:::

But here's where things get a little weird.

What if we had this situation:

::: {#cb485 .sourceCode}

```c
int main(void)
{
    int x = 3490;
    int *const p = &x;
    int **q = &p;
}
```

:::

When I build that, I get a warning:

::: {#cb486 .sourceCode}

```{.sourceCode .default}
warning: initialization discards ‘const’ qualifier from pointer target type
    7 |     int **q = &p;
      |               ^
```

:::

What's going on? The compiler is telling us here that we had a variable that was `const`, and we're assigning its value into another variable that is not `const` in the same way. The "`const` ness" is discarded, which probably isn't what we wanted to do.

> 这里发生了什么？编译器告诉我们，我们有一个 `const` 变量，但我们以相同的方式将其值赋给另一个不是 `const` 的变量。“`const` ness”被丢弃了，这可能不是我们想要做的。

The type of `p` is `int *const p`, and so `&p` is type `int *const *`. And we try to assign that into `q`.

> `p` 的类型是 `int *const p`，因此 `&p` 的类型是 `int *const *`。我们试图将其赋值给 `q`。

But `q` is `int **`! A type with different `const` ness on the first `*`! So we get a warning that the `const` in `p`'s `int *const *` is being ignored and thrown away.

> 但是 `q` 是 `int **`！一种在第一个 `*` 上有不同 `const` ness 的类型！因此，我们得到一个警告，`p` 的 `int *const *` 中的 `const` 被忽略并丢弃了。

We can fix that by making sure `q`'s type is at least as `const` as `p`.

::: {#cb487 .sourceCode}

```c
int x = 3490;
int *const p = &x;
int *const *q = &p;
```

:::

And now we're happy.

We could make `q` even more `const`. As it is, above, we're saying, "`q` isn't itself `const`, but the thing it points to is `const`." But we could make them both `const`:

> 我们可以让 `q` 变得更加 `const`。 就像上面的情况一样，我们说“`q` 本身不是 `const`，但它指向的东西是 `const` 的。” 但是我们可以让它们都变成 `const`：

::: {#cb488 .sourceCode}

```c
int x = 3490;
int *const p = &x;
int *const *const q = &p;  // More const!
```

:::

And that works, too. Now we can't modify `q`, or the pointer `q` points to.

> 而这也行得通。现在我们不能修改 `q`，或者 `q` 指向的指针。

## [23.2] Multibyte Values {#multibyte-values number="23.2"}

We kinda hinted at this in a variety of places earlier, but clearly not every value can be stored in a single byte of memory. Things take up multiple bytes of memory (assuming they're not `char` s). You can tell how many bytes by using `sizeof`. And you can tell which address in memory is the _first_ byte of the object by using the standard `&` operator, which always returns the address of the first byte.

> 我们之前在各个地方都暗示过，但显然不是所有的值都可以存储在一个字节的内存中。一些东西需要多个字节的内存(假设它们不是 `char`)。您可以通过使用 `sizeof` 来告诉有多少字节。您可以通过使用标准的 `&` 运算符来告诉内存中的哪个地址是对象的第一个字节。

And here's another fun fact! If you iterate over the bytes of any object, you get its _object representation_. Two things with the same object representation in memory are equal.

> 在这里有另一个有趣的事实！如果你遍历任何对象的字节，你就可以得到它的_对象表示_。在内存中具有相同对象表示的两个东西是相等的。

If you want to iterate over the object representation, you should do it with pointers to `unsigned char`.

> 如果你想遍历对象表示，你应该使用指向 `unsigned char` 的指针来做。

Let's make our own version of [`memcpy()`](https://beej.us/guide/bgclr/html/split/stringref.html#man-memcpy)[^143^] that does exactly this:

> 让我们制作自己版本的 memcpy()，它可以完全做到这一点：

::: {#cb489 .sourceCode}

```c
void *my_memcpy(void *dest, const void *src, size_t n)
{
    // Make local variables for src and dest, but of type unsigned char

    const unsigned char *s = src;
    unsigned char *d = dest;

    while (n-- > 0)   // For the given number of bytes
        *d++ = *s++;  // Copy source byte to dest byte

    // Most copy functions return a pointer to the dest as a convenience
    // to the caller

    return dest;
}
```

:::

(There are some good examples of post-increment and post-decrement in there for you to study, as well.)

> 在那里有一些很好的后置增量和后置减量的例子供你学习。

It's important to note that the version, above, is probably less efficient than the one that comes with your system.

> 重要的是要注意，上面的版本可能比系统自带的版本效率低。

But you can pass pointers to anything into it, and it'll copy those objects. Could be `int*`, `struct animal*`, or anything.

> 但是你可以把指针传递给它，它会复制这些对象。可以是 `int*`，`struct animal*`，或者任何东西。

Let's do another example that prints out the object representation bytes of a `struct` so we can see if there's any padding in there and what values it has[^144^].

> 让我们做另一个例子，打印出 `struct` 的对象表示字节，以便我们可以查看其中是否有填充，以及它有什么值[^144^]。

::: {#cb490 .sourceCode}

```c
#include <stdio.h>

struct foo {
    char a;
    int b;
};

int main(void)
{
    struct foo x = {0x12, 0x12345678};
    unsigned char *p = (unsigned char *)&x;

    for (size_t i = 0; i < sizeof x; i++) {
        printf("%02X\n", p[i]);
    }
}
```

:::

What we have there is a `struct foo` that's built in such a way that should encourage a compiler to inject padding bytes (though it doesn't have to). And then we get an `unsigned char *` to the first byte of the `struct foo` variable `x`.

> 我们有一个 `struct foo`，它的构造方式应该鼓励编译器插入填充字节(尽管它不必这样做)。然后我们得到一个 `unsigned char *` 指向 `struct foo` 变量 `x` 的第一个字节。

From there, all we need to know is the `sizeof x` and we can loop through that many bytes, printing out the values (in hex for ease).

> 从那里，我们所需要知道的只是 `sizeof x`，我们可以通过循环遍历多少个字节，打印出这些值(以十六进制方便)。

Running this gives a bunch of numbers as output. I've annotated it below to identify where the values were stored:

> 运行此操作会产生一堆数字作为输出。我在下面标注了它们，以确定值存储的位置：

::: {#cb491 .sourceCode}

```{.sourceCode .default}
12  | x.a == 0x12

AB  |
BF  | padding bytes with "random" value
26  |

78  |
56  | x.b == 0x12345678
34  |
12  |
```

:::

On all systems, `sizeof(char)` is 1, and we see that first byte at the top of the output holding the value `0x12` that we stored there.

> 在所有系统中，`sizeof(char)` 都是 1，我们可以看到输出的第一个字节持有我们存储的值 `0x12`。

Then we have some padding bytes---for me, these varied from run to run.

Finally, on my system, `sizeof(int)` is 4, and we can see those 4 bytes at the end. Notice how they're the same bytes as are in the hex value `0x12345678`, but strangely in reverse order[^145^].

> 最后，在我的系统上，`sizeof(int)` 为 4，我们可以在末尾看到这 4 个字节。注意它们与十六进制值 `0x12345678` 中的字节相同，但奇怪的是顺序是相反的[^145^](＃fn145){＃fnref145 .footnote-ref role =“doc-noteref”}。

So that's a little peek under the hood at the bytes of a more complex entity in memory.

> 这是一个关于内存中更复杂实体的字节的小小洞察。

## [23.3] The `NULL` Pointer and Zero {#the-null-pointer-and-zero number="23.3"}

These things can be used interchangeably:

- `NULL`
- `0`
- `'\0'`
- `(void *)0`

Personally, I always use `NULL` when I mean `NULL`, but you might see some other variants from time to time. Though `'\0'` (a byte with all bits set to zero) will also compare equal, it's _weird_ to compare it to a pointer; you should compare `NULL` against the pointer. (Of course, lots of times in string processing, you're comparing _the thing the pointer points to_ to `'\0'`, and that's right.)

> 就我个人而言，我总是用 `NULL` 来表示 `NULL`，但有时你可能会看到其他的变体。虽然 `'\0'`(一个全部位设置为零的字节)也可以相等，但是将其与指针进行比较是很奇怪的；你应该将 `NULL` 与指针进行比较。(当然，在字符串处理中，你经常会比较指针指向的东西与 `'\0'`，这是正确的。)

`0` is called the _null pointer constant_, and, when compared to or assigned into another pointer, it is converted to a null pointer of the same type.

## [23.4] Pointers as Integers {#pointers-as-integers number="23.4"}

You can cast pointers to integers and vice-versa (since a pointer is just an index into memory), but you probably only ever need to do this if you're doing some low-level hardware stuff. The results of such machinations are implementation-defined, so they aren't portable. And _weird things_ could happen.

> 你可以把指针转换成整数，反之亦然(因为指针只是一个指向内存的索引)，但是你可能只在做一些底层硬件的事情时才需要这样做。这种操作的结果是实现定义的，因此它们是不可移植的。而且可能会发生奇怪的事情。

C does make one guarantee, though: you can convert a pointer to a `uintptr_t` type and you'll be able to convert it back to a pointer without losing any data.

> C 确实有一个保证：你可以将指针转换为 `uintptr_t` 类型，并且可以将其转换回指针而不会丢失任何数据。

`uintptr_t` is defined in `<stdint.h>`[^146^].

Additionally, if you feel like being signed, you can use `intptr_t` to the same effect.

> 如果您想要签署，您可以使用 `intptr_t` 来达到同样的效果。

## [23.5] Casting Pointers to other Pointers {#casting-pointers-to-other-pointers number="23.5"}

There's only one safe pointer conversion:

1. Converting to `intptr_t` or `uintptr_t`.
2. Converting to and from `void*`.

TWO! Two safe pointer conversions.

3. Converting to and from `char*`.

THREE! Three safe conversions!

4. Converting to and from a pointer to a `struct` and a pointer to its first member, and vice-versa.

> 4. 将指向结构体的指针和指向其第一个成员的指针之间相互转换。

FOUR! Four safe conversions!

If you cast to a pointer of another type and then access the object it points to, the behavior is undefined due to something called _strict aliasing_.

> 如果您将指针转换为另一种类型，然后访问它指向的对象，由于所谓的严格别名，行为是未定义的。

Plain old _aliasing_ refers to the ability to have more than one way to access the same object. The access points are aliases for each other.

> 普通的别名指的是能够有多种方式访问同一个对象的能力。访问点彼此是别名。

_Strict aliasing_ says you are only allowed to access an object via pointers to _compatible types_ to that object.

> 严格别名规则规定，只允许通过与该对象兼容类型的指针来访问该对象。

For example, this is definitely allowed:

::: {#cb492 .sourceCode}

```c
int a = 1;
int *p = &a;
```

:::

`p` is a pointer to an `int`, and it points to a compatible type---namely `int`---so we're golden.

But the following isn't good because `int` and `float` are not compatible types:

> 但是下面的不好，因为 `int` 和 `float` 不兼容：

::: {#cb493 .sourceCode}

```c
int a = 1;
float *p = (float *)&a;
```

:::

Here's a demo program that does some aliasing. It takes a variable `v` of type `int32_t` and aliases it to a pointer to a `struct words`. That `struct` has two `int16_t` s in it. These types are incompatible, so we're in violation of strict aliasing rules. The compiler will assume that these two pointers never point to the same object... but we're making it so they do. Which is naughty of us.

> 这里有一个演示程序，它执行一些别名。它接受类型为 `int32_t` 的变量 `v`，并将其别名为指向 `struct words` 的指针。该 `struct` 中有两个 `int16_t`。这些类型是不兼容的，因此我们违反了严格的别名规则。编译器将假定这两个指针永远不指向同一个对象...但我们却让它们指向同一个对象。这是我们的不良行为。

Let's see if we can break something.

::: {#cb494 .sourceCode}

```c
#include <stdio.h>
#include <stdint.h>

struct words {
    int16_t v[2];
};

void fun(int32_t *pv, struct words *pw)
{
    for (int i = 0; i < 5; i++) {
        (*pv)++;

        // Print the 32-bit value and the 16-bit values:

        printf("%x, %x-%x\n", *pv, pw->v[1], pw->v[0]);
    }
}

int main(void)
{
    int32_t v = 0x12345678;

    struct words *pw = (struct words *)&v;  // Violates strict aliasing

    fun(&v, pw);
}
```

:::

See how I pass in the two incompatible pointers to `fun()`? One of the types is `int32_t*` and the other is `struct words*`.

> 看看我如何传递两个不兼容的指针给 `fun()`？其中一种类型是 `int32_t*`，另一种是 `struct words*`。

But they both point to the same object: the 32-bit value initialized to `0x12345678`.

> 但它们都指向同一个对象：初始化为“0x12345678”的 32 位值。

So if we look at the fields in the `struct words`, we should see the two 16-bit halves of that number. Right?

> 如果我们看一下 `struct words` 中的字段，我们应该看到该数字的两个 16 位半部分。对吗？

And in the `fun()` loop, we increment the pointer to the `int32_t`. That's it. But since the `struct` points to that same memory, it, too, should be updated to the same value.

> 在 `fun()` 循环中，我们增加指向 `int32_t` 的指针。就是这样。但是由于 `struct` 指向相同的内存，它也应该更新到相同的值。

So let's run it and get this, with the 32-bit value on the left and the two 16-bit portions on the right. It should match[^147^]:

> 让我们运行它，得到这个，左边是 32 位值，右边是两个 16 位部分。它应该匹配[^147^]：

::: {#cb495 .sourceCode}

```{.sourceCode .default}
12345679, 1234-5679
1234567a, 1234-567a
1234567b, 1234-567b
1234567c, 1234-567c
1234567d, 1234-567d
```

:::

and it does... _UNTIL TOMORROW!_

Let's try it compiling GCC with `-O3` and `-fstrict-aliasing`:

::: {#cb496 .sourceCode}

```{.sourceCode .default}
12345679, 1234-5678
1234567a, 1234-5679
1234567b, 1234-567a
1234567c, 1234-567b
1234567d, 1234-567c
```

:::

They're off by one! But they point to the same memory! How could this be? Answer: it's undefined behavior to alias memory like that. _Anything is possible_, except not in a good way.

> 他们相差一个！但它们指向同一个内存！这怎么可能？答案：这种类似的内存别名是未定义的行为。_任何事情都有可能_，但不是以一种好的方式。

If your code violates strict aliasing rules, whether it works or not depends on how someone decides to compile it. And that's a bummer since that's beyond your control. Unless you're some kind of omnipotent deity.

> 如果你的代码违反了严格的别名规则，它是否能正常工作取决于某人如何编译它。这很糟糕，因为这超出了你的控制范围。除非你是某种全能的神。

Unlikely, sorry.

GCC can be forced to not use the strict aliasing rules with `-fno-strict-aliasing`. Compiling the demo program, above, with `-O3` and this flag causes the output to be as expected.

> GCC 可以通过 `-fno-strict-aliasing` 强制不使用严格的别名规则。使用 `-O3` 和此标志编译上述示例程序可以使输出结果如预期。

Lastly, _type punning_ is using pointers of different types to look at the same data. Before strict aliasing, this kind of things was fairly common:

> 最后，_类型双关_是使用不同类型的指针来查看相同的数据。在严格别名之前，这种事情是相当常见的：

::: {#cb497 .sourceCode}

```c
int a = 0x12345678;
short b = *((short *)&a);   // Violates strict aliasing
```

:::

If you want to do type punning (relatively) safely, see the section on [Unions and Type Punning](#union-type-punning).

> 如果你想要安全地进行类型捉弄(相对)，请参阅[联合和类型捉弄](#union-type-punning)一节。

## [23.6] Pointer Differences {#ptr_differences number="23.6"}

As you know from the section on pointer arithmetic, you can subtract one pointer from another[^148^] to get the difference between them in count of array elements.

> 根据指针算术部分的内容，你可以从一个指针减去另一个指针，以获得它们之间的元素数量差异。

Now the _type of that difference_ is something that's up to the implementation, so it could vary from system to system.

> 现在，这种差异的类型取决于实现，因此可能因系统而异。

To be more portable, you can store the result in a variable of type `ptrdiff_t` defined in `<stddef.h>`.

> 要更方便携带，您可以将结果存储在 `<stddef.h>` 中定义的 `ptrdiff_t` 类型的变量中。

::: {#cb498 .sourceCode}

```c
int cats[100];

int *f = cats + 20;
int *g = cats + 60;

ptrdiff_t d = g - f;  // difference is 40
```

:::

And you can print it by prefixing the integer format specifier with `t`:

::: {#cb499 .sourceCode}

```c
printf("%td\n", d);  // Print decimal: 40
printf("%tX\n", d);  // Print hex:     28
```

:::

## [23.7] Pointers to Functions {#pointers-to-functions number="23.7"}

Functions are just collections of machine instructions in memory, so there's no reason we can't get a pointer to the first instruction of the function.

> 函数只是存储在内存中的机器指令的集合，因此没有理由我们不能获得函数第一条指令的指针。

And then call it.

This can be useful for passing a pointer to a function into another function as an argument. Then the second one could call whatever was passed in.

> 这可以用来将指针传递给另一个函数作为参数。然后第二个函数可以调用传入的任何内容。

The tricky part with these, though, is that C needs to know the type of the variable that is the pointer to the function.

> 这里的棘手部分是 C 需要知道指向函数的变量的类型。

And it would really like to know all the details.

Like "this is a pointer to a function that takes two `int` arguments and returns `void`".

> 这是一个指向一个接受两个整数参数并返回无类型的函数的指针。

How do you write all that down so you can declare a variable?

Well, it turns out it looks very much like a function prototype, except with some extra parentheses:

> 嗯，结果看起来很像一个函数原型，只是多了一些括号：

::: {#cb500 .sourceCode}

```c
// Declare p to be a pointer to a function.
// This function returns a float, and takes two ints as arguments.

float (*p)(int, int);
```

:::

Also notice that you don't have to give the parameters names. But you can if you want; they're just ignored.

> 也注意到你不必给参数起名字，但如果你想，它们只是被忽略了。

::: {#cb501 .sourceCode}

```c
// Declare p to be a pointer to a function.
// This function returns a float, and takes two ints as arguments.

float (*p)(int a, int b);
```

:::

So now that we know how to declare a variable, how do we know what to assign into it? How do we get the address of a function?

> 现在我们知道如何声明一个变量，那么我们该如何给它赋值？我们如何获取一个函数的地址？

Turns out there's a shortcut just like with getting a pointer to an array: you can just refer to the bare function name without parens. (You can put an `&` in front of this if you like, but it's unnecessary and not idiomatic.)

> 原来也有一个快捷方式，就像获取指向数组的指针一样：只需引用纯函数名而不加括号。(如果你愿意，可以在前面加上一个'&'，但这是不必要的，也不是惯用的。)

Once you have a pointer to a function, you can call it just by adding parens and an argument list.

> 一旦您有一个指向函数的指针，您可以通过添加括号和参数列表来调用它。

Let's do a simple example where I effectively make an alias for a function by setting a pointer to it. Then we'll call it.

> 让我们做一个简单的例子，我可以通过设置指针来有效地为函数创建一个别名，然后我们就可以调用它了。

This code prints out `3490`:

::: {#cb502 .sourceCode}

```c
#include <stdio.h>

void print_int(int n)
{
    printf("%d\n", n);
}

int main(void)
{
    // Assign p to point to print_int:

    void (*p)(int) = print_int;

    p(3490);          // Call print_int via the pointer
}
```

:::

Notice how the type of `p` represents the return value and parameter types of `print_int`. It has to, or else C will complain about incompatible pointer types.

> 注意 `p` 的类型如何表示 `print_int` 的返回值和参数类型。它必须这样，否则 C 会抱怨指针类型不兼容。

One more example here shows how we might pass a pointer to a function as an argument to another function.

> 这里的另一个例子显示了我们如何将指针作为参数传递给另一个函数。

We'll write a function that takes a couple integer arguments, plus a pointer to a function that operates on those two arguments. Then it prints the result.

> 我们将编写一个函数，它接受一对整数参数，以及一个指向操作这两个参数的函数的指针。然后它打印出结果。

::: {#cb503 .sourceCode}

```c
#include <stdio.h>

int add(int a, int b)
{
    return a + b;
}

int mult(int a, int b)
{
    return a * b;
}

void print_math(int (*op)(int, int), int x, int y)
{
    int result = op(x, y);

    printf("%d\n", result);
}

int main(void)
{
    print_math(add, 5, 7);   // 12
    print_math(mult, 5, 7);  // 35
}
```

:::

Take a moment to digest that. The idea here is that we're going to pass a pointer to a function to `print_math()`, and it's going to call that function to do some math.

> 花一点时间理解这个。这里的想法是我们会把一个指针传递给 `print_math()`，它会调用这个函数来做一些数学运算。

This way we can change the behavior of `print_math()` by passing another function into it. You can see we do that on lines 22-23 when we pass in pointers to functions `add` and `mult`, respectively.

> 我们可以通过传入另一个函数来改变 `print_math()` 的行为。你可以在 22-23 行看到我们分别传入了 `add` 和 `mult` 函数的指针。

Now, on line 13, I think we can all agree the function signature of `print_math()` is a sight to behold. And, if you can believe it, this one is actually pretty straight-forward compared to some things you can construct[^149^].

> 现在，在第 13 行，我们可以一致认为 `print_math()` 的函数签名是一个可观的景象。而且，如果你能相信，这个比你可以构建的一些东西实际上相当直接[^149^](＃fn149){＃fnref149.footnote-ref role =“doc-noteref”}。

But let's digest it. Turns out there are only three parameters, but they're a little hard to see:

> 但让我们消化它。结果只有三个参数，但它们有点难以看到：

::: {#cb504 .sourceCode}

```c
//                      op             x      y
//              |-----------------|  |---|  |---|
void print_math(int (*op)(int, int), int x, int y)
```

:::

The first, `op`, is a pointer to a function that takes two `int` s as arguments and returns an `int`. This matches the signatures for both `add()` and `mult()`.

> 第一个 `op` 是一个指向一个接受两个 `int` 参数并返回一个 `int` 的函数的指针，这与 `add()` 和 `mult()` 的签名匹配。

The second and third, `x` and `y`, are just standard `int` parameters.

Slowly and deliberately let your eyes play over the signature while you identify the working parts. One thing that always stands out for me is the sequence `(*op)(`, the parens and the asterisk. That's the giveaway it's a pointer to a function.

> 慢慢而有条理地让你的眼睛在签名上移动，一边识别其中的工作部分。对我来说，总有一件事情会引起我的注意，那就是序列 `(*op)(`，括号和星号。这是一个指向函数的暗示。

Finally, jump back to the _Pointers II_ chapter for a pointer-to-function [example using the built-in `qsort()`](#qsort-example).

> 最后，跳回到_指针 II_章节，查看使用内置 `qsort()` 的指向函数的[示例](#qsort-example)。

# [24] Bitwise Operations {#bitwise-operations number="24"}

These numeric operations effectively allow you to manipulate individual bits in variables, fitting since C is such a low-level langauge[^150^].

> 这些数字操作有效地允许你操纵变量中的各个位，这很适合 C 这种低级语言。

If you're not familiar with bitwise operations, [Wikipedia has a good bitwise article](https://en.wikipedia.org/wiki/Bitwise_operation)[^151^].

> 如果你不熟悉位运算，[维基百科有一篇很好的位运算文章](https://en.wikipedia.org/wiki/Bitwise_operation)[^151^]。

## [24.1] Bitwise AND, OR, XOR, and NOT {#bitwise-and-or-xor-and-not number="24.1"}

For each of these, the [usual arithmetic conversions](#usual-arithmetic-conversions) take place on the operands (which in this case must be an integer type), and then the appropriate bitwise operation is performed.

> 对于每一个，[通常的算术转换](#usual-arithmetic-conversions)会在操作数上进行(在这种情况下必须是整数类型)，然后执行适当的位运算。

---

Operation Operator Example

---

AND `&` `a = b & c`

OR `|` `a = b | c`

XOR `^` `a = b ^ c`

## NOT `~` `a = ~c`

Note how they're similar to the Boolean operators `&&` and `||`.

These have assignment shorthand variants similar to `+=` and `-=`:

---

Operator Example Longhand equivalent

---

`&=` `a &= c` `a = a & c`

`|=` `a |= c` `a = a | c`

## `^=` `a ^= c` `a = a ^ c`

## [24.2] Bitwise Shift {#bitwise-shift number="24.2"}

For these, the [integer promotions](#integer-promotions) are performed on each operand (which must be an integer type) and then a bitwise shift is executed. The type of the result is the type of the promoted left operand.

> 对于这些，会对每个操作数(必须是整数类型)执行[整数提升](#integer-promotions)，然后执行位移运算。结果的类型是提升后的左操作数的类型。

New bits are filled with zeros, with a possible exception noted in the implementation-defined behavior, below.

> 新位元组填充为零，除了可能在实作定义行为中标记的例外情况。

---

Operation Operator Example

---

Shift left `<<` `a = b << c`

## Shift right `>>` `a = b >> c`

There's also the same similar shorthand for shifting:

---

Operator Example Longhand equivalent

---

`>>=` `a >>= c` `a = a >> c`

## `<<=` `a <<= c` `a = a << c`

Watch for undefined behavior: no negative shifts, and no shifts that are larger than the size of the promoted left operand.

> 注意未定义的行为：不允许负移位，也不允许移位数大于左操作数的大小。

Also watch for implementation-defined behavior: if you right-shift a negative number, the results are implementation-defined. (It's perfectly fine to right-shift a signed `int`, just make sure it's positive.)

> 也要注意实现定义的行为：如果你对一个负数进行右移，结果是实现定义的。(对有符号的 int 进行右移是完全可以的，只要确保它是正数)。

# [25] Variadic Functions {#variadic-functions number="25"}

_Variadic_ is a fancy word for functions that take arbitrary numbers of arguments.

> _可变参数_是指可以接受任意数量参数的函数的一个花哨的词。

A regular function takes a specific number of arguments, for example:

::: {#cb505 .sourceCode}

```c
int add(int x, int y)
{
    return x + y;
}
```

:::

You can only call that with exactly two arguments which correspond to parameters `x` and `y`.

> 你只能用两个与参数 `x` 和 `y` 对应的参数来调用它。

::: {#cb506 .sourceCode}

```c
add(2, 3);
add(5, 12);
```

:::

But if you try it with more, the compiler won't let you:

::: {#cb507 .sourceCode}

```c
add(2, 3, 4);  // ERROR
add(5);        // ERROR
```

:::

Variadic functions get around this limitation to a certain extent.

We've already seen a famous example in `printf()`! You can pass all kinds of things to it.

> 我们已经在 `printf()` 中看到了一个着名的例子！你可以把各种东西传递给它。

::: {#cb508 .sourceCode}

```c
printf("Hello, world!\n");
printf("The number is %d\n", 2);
printf("The number is %d and pi is %f\n", 2, 3.14159);
```

:::

It seems to not care how many arguments you give it!

Well, that's not entirely true. Zero arguments will give you an error:

::: {#cb509 .sourceCode}

```c
printf();  // ERROR
```

:::

This leads us to one of the limitations of variadic functions in C: they must have at least one argument.

> 这导致 C 中变参函数的一个限制：它们至少需要一个参数。

But aside from that, they're pretty flexible, even allows arguments to have different types just like `printf()` does.

> 除此之外，它们非常灵活，甚至允许参数具有不同类型，就像 `printf()` 一样。

Let's see how they work!

## [25.1] Ellipses in Function Signatures {#ellipses-in-function-signatures number="25.1"}

So how does it work, syntactically?

What you do is put all the arguments that _must_ be passed first (and remember there has to be at least one) and after that, you put `...`. Just like this:

> 你要做的是首先把所有必须传递的参数放在前面(记住至少有一个)，然后放置“...”。就像这样：

::: {#cb510 .sourceCode}

```c
void func(int a, ...)   // Literally 3 dots here
```

:::

Here's some code to demo that:

::: {#cb511 .sourceCode}

```c
#include <stdio.h>

void func(int a, ...)
{
    printf("a is %d\n", a);  // Prints "a is 2"
}

int main(void)
{
    func(2, 3, 4, 5, 6);
}
```

:::

So, great, we can get that first argument that's in variable `a`, but what about the rest of the arguments? How do you get to them?

> 好极了，我们可以得到存储在变量'a'中的第一个参数，但其余的参数呢？你怎么获得它们？

Here's where the fun begins!

## [25.2] Getting the Extra Arguments {#getting-the-extra-arguments number="25.2"}

You're going to want to include `<stdarg.h>` to make any of this work.

First things first, we're going to use a special variable of type `va_list` (variable argument list) to keep track of which variable we're accessing at a time.

> 首先，我们将使用一个特殊的类型 `va_list`(可变参数列表)的变量来跟踪我们每次访问的变量。

The idea is that we first start processing arguments with a call to `va_start()`, process each argument in turn with `va_arg()`, and then, when done, wrap it up with `va_end()`.

> 首先，我们使用 `va_start()` 函数开始处理参数，然后使用 `va_arg()` 函数一个一个处理每个参数，最后使用 `va_end()` 函数结束处理。

When you call `va_start()`, you need to pass in the _last named parameter_ (the one just before the `...`) so it knows where to start looking for the additional arguments.

> 当你调用 `va_start()` 时，你需要传入_最后一个命名参数_(就在 `...` 之前的那个)，这样它才知道从哪里开始寻找额外的参数。

And when you call `va_arg()` to get the next argument, you have to tell it the type of argument to get next.

> 当你调用 `va_arg()` 来获取下一个参数时，你必须告诉它下一个参数的类型。

Here's a demo that adds together an arbitrary number of integers. The first argument is the number of integers to add together. We'll make use of that to figure out how many times we have to call `va_arg()`.

> 这里有一个示例，它可以将任意数量的整数相加。第一个参数是要相加的整数的数量。我们将利用它来弄清楚我们要调用多少次 `va_arg()`。

::: {#cb512 .sourceCode}

```c
#include <stdio.h>
#include <stdarg.h>

int add(int count, ...)
{
    int total = 0;
    va_list va;

    va_start(va, count);   // Start with arguments after "count"

    for (int i = 0; i < count; i++) {
        int n = va_arg(va, int);   // Get the next int

        total += n;
    }

    va_end(va);  // All done

    return total;
}

int main(void)
{
    printf("%d\n", add(4, 6, 2, -4, 17));  // 6 + 2 - 4 + 17 = 21
    printf("%d\n", add(2, 22, 44));        // 22 + 44 = 66
}
```

:::

(Note that when `printf()` is called, it uses the number of `%d` s (or whatever) in the format string to know how many more arguments there are!)

> 注意，当调用 `printf()` 时，它会根据格式字符串中的 `%d` 数量(或其他)来确定还有多少个参数！

If the syntax of `va_arg()` is looking strange to you (because of that loose type name floating around in there), you're not alone. These are implemented with preprocessor macros in order to get all the proper magic in there.

> 如果 `va_arg()` 的语法对你来说看起来很奇怪(因为那里有一个松散的类型名称)，你并不是孤单一人。这些都是用预处理器宏实现的，以便获得所有正确的魔法。

## [25.3] `va_list` Functionality {#va_list-functionality number="25.3"}

What is that `va_list` variable we're using up there? It's an opaque variable[^152^] that holds information about which argument we're going to get next with `va_arg()`. You see how we just call `va_arg()` over and over? The `va_list` variable is a placeholder that's keeping track of progress so far.

> 那个 `va_list` 变量我们在上面使用的是什么？它是一个不透明的变量[^152^]，它保存有关我们下次使用 `va_arg()` 获取哪个参数的信息。你看到我们只是一次又一次地调用 `va_arg()` 吗？`va_list` 变量是一个占位符，它跟踪进度到目前为止。

But we have to initialize that variable to some sensible value. That's where `va_start()` comes into play.

> 但是我们必须将该变量初始化为一些合理的值。这就是 `va_start()` 发挥作用的地方。

When we called `va_start(va, count)`, above, we were saying, "Initialize the `va` variable to point to the variable argument _immediately after_ `count`."

> 当我们调用 `va_start(va, count)` 时，我们的意思是："将 `va` 变量初始化为指向 `count` 之后的可变参数。"

And that's _why_ we need to have at least one named variable in our argument list[^153^].

> 所以我们需要在参数列表中至少有一个命名变量 [^153^]。

Once you have that pointer to the initial parameter, you can easily get subsequent argument values by calling `va_arg()` repeatedly. When you do, you have to pass in your `va_list` variable (so it can keep on keeping track of where you are), as well as the type of argument you're about to copy off.

> 一旦你有了指向初始参数的指针，你可以通过多次调用 `va_arg()` 来轻松获取后续的参数值。当你这样做时，你必须传入你的 `va_list` 变量(以便它能够继续跟踪你的位置)以及你即将复制的参数的类型。

It's up to you as a programmer to figure out which type you're going to pass to `va_arg()`. In the above example, we just did `int` s. But in the case of `printf()`, it uses the format specifier to determine which type to pull off next.

> 作为程序员，你需要自己决定传递给 `va_arg()` 的类型。在上面的例子中，我们只传递了 `int`。但是在 `printf()` 中，它使用格式说明符来确定下一个要拉出的类型。

And when you're done, call `va_end()` to wrap it up. You **must** (the spec says) call this on a particular `va_list` variable before you decide to call either `va_start()` or `va_copy()` on it again. I know we haven't talked about `va_copy()` yet.

> 当你完成后，调用 `va_end()` 来结束它。根据规范，你**必须**在再次调用 `va_start()` 或 `va_copy()` 之前调用特定的 `va_list` 变量。我知道我们还没有讨论 `va_copy()`。

So the standard progression is:

- `va_start()` to initialize your `va_list` variable
- Repeatedly `va_arg()` to get the values
- `va_end()` to deinitialize your `va_list` variable

I also mentioned `va_copy()` up there; it makes a copy of your `va_list` variable in the exact same state. That is, if you haven't started with `va_arg()` with the source variable, the new one won't be started, either. If you've consumed 5 variables with `va_arg()` so far, the copy will also reflect that.

> 我在上面也提到了 `va_copy()`；它会把你的 `va_list` 变量复制成完全一样的状态。也就是说，如果你没有使用源变量开始 `va_arg()`，新变量也不会开始。如果你已经使用 `va_arg()` 消耗了 5 个变量，副本也会反映出来。

`va_copy()` can be useful if you need to scan ahead through the arguments but need to also remember your current place.

## [25.4] Library Functions That Use `va_list` s {#library-functions-that-use-va_lists number="25.4"}

One of the other uses for these is pretty cool: writing your own custom `printf()` variant. It would be a pain to have to handle all those format specifiers right? All zillion of them?

> 一个很酷的另一个用途是编写自己的自定义 `printf()` 变体。要处理所有这些格式说明符会很痛苦吧？所有的千千万万个？

Luckily, there are `printf()` variants that accept a working `va_list` as an argument. You can use these to wrap up and make your own custom `printf()` s!

> 幸运的是，有一些 `printf()` 变体接受一个有效的 `va_list` 作为参数。您可以使用这些来包装并制作自己的自定义 `printf()`！

These functions start with the letter `v`, such as `vprintf()`, `vfprintf()`, `vsprintf()`, and `vsnprintf()`. Basically all your `printf()` golden oldies except with a `v` in front.

> 这些函数以字母“v”开头，如 `vprintf()`、`vfprintf()`、`vsprintf()` 和 `vsnprintf()`。基本上，除了前面加上“v”之外，所有你的 `printf()` 老朋友都在这里。

Let's make a function `my_printf()` that works just like `printf()` except it takes an extra argument up front.

> 让我们创建一个名为 `my_printf()` 的函数，它的功能和 `printf()` 一样，只是它需要在前面多传入一个参数。

::: {#cb513 .sourceCode}

```c
#include <stdio.h>
#include <stdarg.h>

int my_printf(int serial, const char *format, ...)
{
    va_list va;

    // Do my custom work
    printf("The serial number is: %d\n", serial);

    // Then pass the rest off to vprintf()
    va_start(va, format);
    int rv = vprintf(format, va);
    va_end(va);

    return rv;
}

int main(void)
{
    int x = 10;
    float y = 3.2;

    my_printf(3490, "x is %d, y is %f\n", x, y);
}
```

:::

See what we did there? On lines 12-14 we started a new `va_list` variable, and then just passed it right into `vprintf()`. And it knows just want to do with it, because it has all the `printf()` smarts built-in.

> 看到我们刚才做了什么吗？在第 12-14 行，我们开始了一个新的 `va_list` 变量，然后直接传递给 `vprintf()`。它知道该怎么做，因为它内置了所有的 `printf()` 智能。

We still have to call `va_end()` when we're done, though, so don't forget that!

> 我们完成后还是要调用 `va_end()`，别忘了！

# [26] Locale and Internationalization {#locale-and-internationalization number="26"}

_Localization_ is the process of making your app ready to work well in different locales (or countries).

> 本地化是指使您的应用程序能够在不同的区域(或国家)中很好地运行的过程。

As you might know, not everyone uses the same character for decimal points or for thousands separators... or for currency.

> 你可能知道，不是每个人都使用相同的字符作为小数点或千位分隔符...或货币。

These locales have names, and you can select one to use. For example, a US locale might write a number like:

> 这些地区有名称，您可以选择一个来使用。例如，美国地区可能会写一个数字：

100,000.00

Whereas in Brazil, the same might be written with the commas and decimal points swapped:

> 在巴西，可以用逗号和小数点交换的方式来写：

100.000,00

Makes it easier to write your code so it ports to other nationalities with ease!

> 使编写代码更容易，以便轻松地将其移植到其他民族！

Well, sort of. Turns out C only has one built-in locale, and it's limited. The spec really leaves a lot of ambiguity here; it's hard to be completely portable.

> 嗯，有点儿。原来 C 只有一个内置的地区设置，而且有限。规范在这里留下了很多模糊不清的地方；要完全兼容很难。

But we'll do our best!

## [26.1] Setting the Localization, Quick and Dirty {#setting-the-localization-quick-and-dirty number="26.1"}

For these calls, include `<locale.h>`.

There is basically one thing you can portably do here in terms of declaring a specific locale. This is likely what you want to do if you're going to do locale anything:

> 基本上，您可以在这里以声明特定区域设置的方式执行一项可移植的操作。如果您要进行区域设置，这可能就是您想要做的：

::: {#cb514 .sourceCode}

```c
setlocale(LC_ALL, "");  // Use this environment's locale for everything
```

:::

You'll want to call that so that the program gets initialized with your current locale.

> 你需要调用它，以便使用你当前的语言环境来初始化程序。

Getting into more details, there is one more thing you can do and stay portable:

> 进一步详细说明，你还可以做一件事情，并保持便携：

::: {#cb515 .sourceCode}

```c
setlocale(LC_ALL, "C");  // Use the default C locale
```

:::

but that's called by default every time your program starts, so there's not much need to do it yourself.

> 但是每次程序启动时都会自动调用，所以没有必要自己去做。

In that second string, you can specify any locale supported by your system. This is completely system-dependent, so it will vary. On my system, I can specify this:

> 在第二个字符串中，您可以指定系统支持的任何区域设置。这完全取决于系统，因此会有所不同。在我的系统上，我可以指定：

::: {#cb516 .sourceCode}

```c
setlocale(LC_ALL, "en_US.UTF-8");  // Non-portable!
```

:::

And that'll work. But it's only portable to systems which have that exact same name for that exact same locale, and you can't guarantee it.

> 这样可以行，但只有那些拥有相同名称和相同语言环境的系统才能支持，而且你也无法保证。

By passing in an empty string (`""`) for the second argument, you're telling C, "Hey, figure out what the current locale on this system is so I don't have to tell you."

> 通过将一个空字符串("")作为第二个参数传入，您正在告诉 C：“嘿，找出这个系统上的当前区域设置，这样我就不必告诉您了。”

## [26.2] Getting the Monetary Locale Settings {#getting-the-monetary-locale-settings number="26.2"}

Because moving green pieces of paper around promises to be the key to happiness[^154^], let's talk about monetary locale. When you're writing portable code, you have to know what to type for cash, right? Whether that's "\$", "€", "¥", or "£".

> 因为移动绿色纸片承诺是幸福的关键 [^154^],让我们谈谈货币地区。当你写可移植代码时，你必须知道如何输入现金，对吗？无论是"\$"、"€"、"¥"还是"£"。

How can you write that code without going insane? Luckily, once you call `setlocale(LC_ALL, "")`, you can just look these up with a call to `localeconv()`:

> 你怎么能在不疯狂的情况下写出这段代码？幸运的是，一旦你调用 `setlocale(LC_ALL, "")`，你就可以通过调用 `localeconv()` 来查找这些信息：

::: {#cb517 .sourceCode}

```c
struct lconv *x = localeconv();
```

:::

This function returns a pointer to a statically-allocated `struct lconv` that has all that juicy information you're looking for.

> 这个函数返回一个指向静态分配的 `struct lconv` 的指针，它包含你正在寻找的所有有用信息。

Here are the fields of `struct lconv` and their meanings.

First, some conventions. An `_p_` means "positive", and `_n_` means "negative", and `int_` means "international". Though a lot of these are type `char` or `char*`, most (or the strings they point to) are actually treated as integers[^155^].

> 首先，一些约定。 `_p_` 意味着“正面”，`_n_` 意味着“负面”，`int_` 意味着“国际”。尽管大多数这些都是 `char` 或 `char*` 类型，但实际上大多数(或它们指向的字符串)都被视为整数[^155^] (#fn155){#fnref155 .footnote-ref role="doc-noteref"}。

Before we go further, know that `CHAR_MAX` (from `<limits.h>`) is the maximum value that can be held in a `char`. And that many of the following `char` values use that to indicate the value isn't available in the given locale.

> 在我们继续之前，请注意 `CHAR_MAX`(来自 `<limits.h>`)是可以存储在 `char` 中的最大值。许多以下的 `char` 值使用它来表示在给定的语言环境中不可用的值。

---

Field Description

---

`char *mon_decimal_point` Decimal pointer character for money, e.g. `"."`.

`char *mon_thousands_sep` Thousands separator character for money, e.g. `","`.

`char *mon_grouping` Grouping description for money (see below).

`char *positive_sign` Positive sign for money, e.g. `"+"` or `""`.

`char *negative_sign` Negative sign for money, e.g. `"-"`.

`char *currency_symbol` Currency symbol, e.g. `"$"`.

`char frac_digits` When printing monetary amounts, how many digits to print past the decimal point, e.g. `2`.

`char p_cs_precedes` `1` if the `currency_symbol` comes before the value for a non-negative monetary amount, `0` if after.

`char n_cs_precedes` `1` if the `currency_symbol` comes before the value for a negative monetary amount, `0` if after.

`char p_sep_by_space` Determines the separation of the `currency symbol` from the value for non-negative amounts (see below).

`char n_sep_by_space` Determines the separation of the `currency symbol` from the value for negative amounts (see below).

`char p_sign_posn` Determines the `positive_sign` position for non-negative values.

`char p_sign_posn` Determines the `positive_sign` position for negative values.

`char *int_curr_symbol` International currency symbol, e.g. `"USD "`.

`char int_frac_digits` International value for `frac_digits`.

`char int_p_cs_precedes` International value for `p_cs_precedes`.

`char int_n_cs_precedes` International value for `n_cs_precedes`.

`char int_p_sep_by_space` International value for `p_sep_by_space`.

`char int_n_sep_by_space` International value for `n_sep_by_space`.

`char int_p_sign_posn` International value for `p_sign_posn`.

## `char int_n_sign_posn` International value for `n_sign_posn`.

### [26.2.1] Monetary Digit Grouping {#monetary-digit-grouping number="26.2.1"}

OK, this is a trippy one. `mon_grouping` is a `char*`, so you might be thinking it's a string. But in this case, no, it's really an array of `char` s. It should always end either with a `0` or `CHAR_MAX`.

> 好的，这个有点奇怪。`mon_grouping` 是一个 `char*`，所以你可能会认为它是一个字符串。但在这种情况下，不，它实际上是一个 `char` 数组。它应该总是以 `0` 或 `CHAR_MAX` 结尾。

These values describe how to group sets of numbers in currency to the _left_ of the decimal (the whole number part).

> 这些值描述了如何将小数点左边(整数部分)的货币组合。

For example, we might have:

::: {#cb518 .sourceCode}

```{.sourceCode .default}
  2   1   0
 --- --- ---
$100,000,000.00
```

:::

These are groups of three. Group 0 (just left of the decimal) has 3 digits. Group 1 (next group to the left) has 3 digits, and the last one also has 3.

> 这些是三个组。组 0(小数点左边)有 3 位数字。组 1(左边的下一组)有 3 位数字，最后一组也有 3 位数字。

So we could describe these groups, from the right (the decimal) to the left with a bunch of integer values representing the group sizes:

> 我们可以从右(十进制)到左用一组整数值来描述这些组，这些整数值代表着组的大小。

::: {#cb519 .sourceCode}

```{.sourceCode .default}
3 3 3
```

:::

And that would work for values up to \$100,000,000.

But what if we had more? We could keep adding `3` s...

::: {#cb520 .sourceCode}

```{.sourceCode .default}
3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
```

:::

but that's crazy. Luckily, we can specify `0` to indicate that the previous group size repeats:

> 但那太疯狂了。幸运的是，我们可以指定 `0` 来表示前一组大小重复：

::: {#cb521 .sourceCode}

```{.sourceCode .default}
3 0
```

:::

Which means to repeat every 3. That would handle \$100, \$1,000, \$10,000, \$10,000,000, \$100,000,000,000, and so on.

> 这意味着每 3 次重复一次，可以处理\$100、\$1,000、\$10,000、\$10,000,000、\$100,000,000,000 等等。

You can go legitimately crazy with these to indicate some weird groupings.

> 你可以用这些来表示一些奇怪的分组，简直太疯狂了！

For example:

::: {#cb522 .sourceCode}

```{.sourceCode .default}
4 3 2 1 0
```

:::

would indicate:

::: {#cb523 .sourceCode}

```{.sourceCode .default}
$1,0,0,0,0,00,000,0000.00
```

:::

One more value that can occur is `CHAR_MAX`. This indicates that no more grouping should occur, and can appear anywhere in the array, including the first value.

> 有一个可能出现的另一个值是 `CHAR_MAX`。这表示不再进行分组，可以出现在数组的任何位置，包括第一个值。

::: {#cb524 .sourceCode}

```{.sourceCode .default}
3 2 CHAR_MAX
```

:::

would indicate:

::: {#cb525 .sourceCode}

```{.sourceCode .default}
100000000,00,000.00
```

:::

for example.

And simply having `CHAR_MAX` in the first array position would tell you there was to be no grouping at all.

> 简单地在第一个数组位置拥有 `CHAR_MAX` 就可以告诉你根本不会有任何分组。

### [26.2.2] Separators and Sign Position {#separators-and-sign-position number="26.2.2"}

All the `sep_by_space` variants deal with spacing around the currency sign. Valid values are:

> 所有的 sep_by_space 变体都处理货币符号周围的空格。有效值为：

---

```
    Value       Description
```

---

```
     `0`        No space between currency symbol and value.

     `1`        Separate the currency symbol (and sign, if any) from the value with a space.

     `2`        Separate the sign symbol from the currency symbol (if adjacent) with a space, otherwise separate the sign symbol from the value with a space.
```

---

The `sign_posn` variants are determined by the following values:

Value Description

---

```
`0`   Put parens around the value and the currency symbol.
`1`   Put the sign string in front of the currency symbol and value.
`2`   Put the sign string after the currency symbol and value.
`3`   Put the sign string directly in front of the currency symbol.
`4`   Put the sign string directly behind the currency symbol.
```

### [26.2.3] Example Values {#example-values number="26.2.3"}

When I get the values on my system, this is what I see (grouping string displayed as individual byte values):

> 当我在系统上获取值时，这就是我看到的(将字符串分组显示为单独的字节值)：

::: {#cb526 .sourceCode}

```c
mon_decimal_point  = "."
mon_thousands_sep  = ","
mon_grouping       = 3 3 0
positive_sign      = ""
negative_sign      = "-"
currency_symbol    = "$"
frac_digits        = 2
p_cs_precedes      = 1
n_cs_precedes      = 1
p_sep_by_space     = 0
n_sep_by_space     = 0
p_sign_posn        = 1
n_sign_posn        = 1
int_curr_symbol    = "USD "
int_frac_digits    = 2
int_p_cs_precedes  = 1
int_n_cs_precedes  = 1
int_p_sep_by_space = 1
int_n_sep_by_space = 1
int_p_sign_posn    = 1
int_n_sign_posn    = 1
```

:::

## [26.3] Localization Specifics {#localization-specifics number="26.3"}

Notice how we passed the macro `LC_ALL` to `setlocale()` earlier... this hints that there might be some variant that allows you to be more precise about which _parts_ of the locale you're setting.

> 注意我们之前如何将宏 `LC_ALL` 传递给 `setlocale()`...这暗示可能有一些变体可以让您更精确地设置_部分_区域设置。

Let's take a look at the values you can see for these:

---

Macro Description

---

`LC_ALL` Set all of the following to the given locale.

`LC_COLLATE` Controls the behavior of the `strcoll()` and `strxfrm()` functions.

`LC_CTYPE` Controls the behavior of the character-handling functions[^156^].

`LC_MONETARY` Controls the values returned by `localeconv()`.

`LC_NUMERIC` Controls the decimal point for the `printf()` family of functions.

## `LC_TIME` Controls time formatting of the `strftime()` and `wcsftime()` time and date printing functions.

It's pretty common to see `LC_ALL` being set, but, hey, at least you have options.

> 这种设置 `LC_ALL` 的情况很常见，但是，嘿，至少你有选择的余地。

Also I should point out that `LC_CTYPE` is one of the biggies because it ties into wide characters, a significant can of worms that we'll talk about later.

> 此外，我要指出 `LC_CTYPE` 是其中一个重要的因素，因为它与宽字符有关，这是一个重要的问题，我们稍后会讨论。

# [27] Unicode, Wide Characters, and All That {#unicode-wide-characters-and-all-that number="27"}

Before we begin, note that this is an active area of language development in C as it works to get past some, erm, _growing pains_. When C2x comes out, updates here are probable.

> 在开始之前，请注意，C 语言在努力克服一些痛点时，这是一个活跃的语言发展领域。当 C2x 发布时，这里的更新可能会发生变化。

Most people are basically interested in the deceptively simple question, "How do I use such-and-such character set in C?" We'll get to that. But as we'll see, it might already work on your system. Or you might have to punt to a third-party library.

> 大多数人都对这个看似简单的问题感兴趣：“我如何在 C 语言中使用这种字符集？”我们将会讨论这个问题。但是，我们会发现，它可能已经在你的系统上运行。或者你可能不得不使用第三方库。

We're going to talk about a lot of things this chapter---some are platform agnostic, and some are C-specific.

> 我们将在本章讨论很多事情---有些是跨平台的，有些是特定于 C 语言的。

Let's get an outline first of what we're going to look at:

- Unicode background
- Character encoding background
- Source and Execution character Sets
- Using Unicode and UTF-8
- Using other character types like `wchar_t`, `char16_t`, and `char32_t`

Let's dive in!

## [27.1] What is Unicode? {#what-is-unicode number="27.1"}

Back in the day, it was popular in the US and much of the world to use a 7-bit or 8-bit encoding for characters in memory. This meant we could have 128 or 256 characters (including non-printable characters) total. That was fine for a US-centric world, but it turns out there are actually other alphabets out there---who knew? Chinese has over 50,000 characters, and that's not fitting in a byte.

> 以前，在美国和世界大部分地区，使用 7 位或 8 位编码存储字符是很流行的。这意味着我们最多可以有 128 个或 256 个字符(包括不可打印字符)。这对于以美国为中心的世界来说已经够用了，但事实证明，其实还有其他的字母表——谁知道呢？中文有超过 50000 个字符，一个字节是装不下的。

So people came up with all kinds of alternate ways to represent their own custom character sets. And that was fine, but turned into a compatibility nightmare.

> 人们想出了各种不同的方式来表示他们自己的自定义字符集。这样做没什么问题，但却造成了兼容性的噩梦。

To escape it, Unicode was invented. One character set to rule them all. It extends off into infinity (effectively) so we'll never run out of space for new characters. It has Chinese, Latin, Greek, cuneiform, chess symbols, emojis... just about everything, really! And more is being added all the time!

> 为了逃脱这一点，Unicode 被发明出来。一套字符集可以规范它们。它可以无限地延伸，因此我们永远不会没有空间来添加新字符。它包括中文、拉丁文、希腊文、楔形文字、棋盘符号、表情符号……几乎所有的东西！而且还在不断添加！

## [27.2] Code Points {#code-points number="27.2"}

I want to talk about two concepts here. It's confusing because they're both numbers... different numbers for the same thing. But bear with me.

> 我想在这里谈论两个概念。它们之间有点混乱，因为它们都是数字... 同一件事的不同数字。但是请耐心等待。

Let's loosely define _code point_ to mean a numeric value representing a character. (Code points can also represent unprintable control characters, but just assume I mean something like the letter "B" or the character "π".)

> 让我们简单定义“码点”为表示字符的数字值。(码点也可以表示不可打印的控制字符，但只假设我指的是像字母“B”或字符“π”这样的东西。)

Each code point represents a unique character. And each character has a unique numeric code point associated with it.

> 每个码点代表一个唯一的字符。每个字符都有一个与之相关联的唯一数字码点。

For example, in Unicode, the numeric value 66 represents "B", and 960 represents "π". Other character mappings that aren't Unicode use different values, potentially, but let's forget them and concentrate on Unicode, the future!

> 例如，在 Unicode 中，数字值 66 表示“B”，而 960 表示“π”。其他不是 Unicode 的字符映射可能使用不同的值，但让我们忘记它们，专注于 Unicode，未来！

So that's one thing: there's a number that represents each character. In Unicode, these numbers run from 0 to over 1 million.

> 所以有一件事：每个字符都有一个代表它的数字。在 Unicode 中，这些数字从 0 到超过 100 万。

Got it?

Because we're about to flip the table a little.

## [27.3] Encoding {#encoding number="27.3"}

If you recall, an 8-bit byte can hold values from 0-255, inclusive. That's great for "B" which is 66---that fits in a byte. But "π" is 960, and that doesn't fit in a byte! We need another byte. How do we store all that in memory? Or what about bigger numbers, like 195,024? That's going to need a number of bytes to hold.

> 如果你还记得，一个 8 位字节可以容纳 0-255 之间的值(包括 255)。这对于“B”来说很棒，因为它的值是 66，可以放在一个字节里。但是“π”的值是 960，它不能放在一个字节里！我们需要另一个字节。我们如何把它存储在内存中？或者更大的数字，比如 195024？它需要一些字节来容纳。

The Big Question: how are these numbers represented in memory? This is what we call the _encoding_ of the characters.

> 这个大问题：这些数字是如何在内存中表示的？这就是我们所说的字符编码。

So we have two things: one is the code point which tells us effectively the serial number of a particular character. And we have the encoding which tells us how we're going to represent that number in memory.

> 所以我们有两件事：一个是代码点，它可以有效地告诉我们特定字符的序列号。我们还有编码，它告诉我们如何在内存中表示这个数字。

There are plenty of encodings. You can make up your own right now, if you want[^157^]. But we're going to look at some really common encodings that are in use with Unicode.

> 有很多编码。如果你想的话，你现在就可以自己创建一个。但是我们将要看一些非常常见的与 Unicode 一起使用的编码。

---

```
  Encoding     Description
```

---

```
   UTF-8       A byte-oriented encoding that uses a variable number of bytes per character. This is the one to use.

   UTF-16      A 16-bit per character[^158^] encoding.

   UTF-32      A 32-bit per character encoding.
```

---

With UTF-16 and UTF-32, the byte order matters, so you might see UTF-16BE for big-endian and UTF-16LE for little-endian. Same for UTF-32. Technically, if unspecified, you should assume big-endian. But since Windows uses UTF-16 extensively and is little-endian, sometimes that is assumed[^159^].

> 使用 UTF-16 和 UTF-32 时，字节顺序很重要，因此您可能会看到 UTF-16BE 用于大端，而 UTF-16LE 用于小端。 UTF-32 也是如此。 从技术上讲，如果未指定，您应该假定为大端。 但是由于 Windows 广泛使用 UTF-16 并且是小端，因此有时会假定[^159^](＃fn159){＃fnref159 。脚注引用 role =“doc-noteref”}。

简体中文：使用 UTF-16 和 UTF-32 时，字节顺序很重要，因此您可能会看到 UTF-16BE 用于大端，而 UTF-16LE 用于小端。 UTF-32 也是如此。 从技术上讲，如果未指定，应该假定为大端。 但是由于 Windows 广泛使用 UTF-16 并且是小端，因此有时会假定。

Let's look at some examples. I'm going to write the values in hex because that's exactly two digits per 8-bit byte, and it makes it easier to see how things are arranged in memory.

> 让我们来看一些例子。我会用十六进制来写这些值，因为每个 8 位字节只有两位，这样更容易看出内存中的布局。

Character Code Point UTF-16BE UTF-32BE UTF-16LE UTF-32LE UTF-8

---

```
  `A`          41         0041     00000041     4100     41000000     41
  `B`          42         0042     00000042     4200     42000000     42
  `~`          7E         007E     0000007E     7E00     7E000000     7E
  `π`         3C0         03C0     000003C0     C003     C0030000    CF80
  `€`         20AC        20AC     000020AC     AC20     AC200000   E282AC
```

Look in there for the patterns. Note that UTF-16BE and UTF-32BE are simply the code point represented directly as 16- and 32-bit values[^160^].

> 查看那里的模式。注意，UTF-16BE 和 UTF-32BE 只是将代码点直接表示为 16 位和 32 位值[^160^](＃fn160){＃fnref160 。脚注引用 role =“doc-noteref”}。

Little-endian is the same, except the bytes are in little-endian order.

Then we have UTF-8 at the end. First you might notice that the single-byte code points are represented as a single byte. That's nice. You might also notice that different code points take different number of bytes. This is a variable-width encoding.

> 最后我们使用 UTF-8。首先你可能会注意到单字节编码点被表示为单个字节。这很好。你也可能注意到不同的编码点需要不同数量的字节。这是一种可变宽度编码。

So as soon as we get above a certain value, UTF-8 starts using additional bytes to store the values. And they don't appear to correlate with the code point value, either.

> 当我们达到一定值时，UTF-8 就会开始使用额外的字节来存储值。而且它们似乎也与代码点值没有关联。

[The details of UTF-8 encoding](https://en.wikipedia.org/wiki/UTF-8)[^161^] are beyond the scope of this guide, but it's enough to know that it has a variable number of bytes per code point, and those byte values don't match up with the code point _except for the first 128 code points_. If you really want to learn more, [Computerphile has a great UTF-8 video with Tom Scott](https://www.youtube.com/watch?v=MijmeoH9LT4)[^162^].

> 细节的 UTF-8 编码([https://en.wikipedia.org/wiki/UTF-8](https://en.wikipedia.org/wiki/UTF-8))超出了本指南的范围，但是只需要知道它每个码点的字节数是可变的，而且这些字节值与码点(除了前 128 个码点)不匹配。如果您真的想了解更多信息，Computerphile 有一个由 Tom Scott 演示的关于 UTF-8 的很棒的视频([https://www.youtube.com/watch?v=MijmeoH9LT4](https://www.youtube.com/watch?v=MijmeoH9LT4))。

That last bit is a neat thing about Unicode and UTF-8 from a North American perspective: it's backward compatible with 7-bit ASCII encoding! So if you're used to ASCII, UTF-8 is the same! Every ASCII-encoded document is also UTF-8 encoded! (But not the other way around, obviously.)

> 最后一点对于北美人来说是关于 Unicode 和 UTF-8 的一个很棒的事情：它与 7 位 ASCII 编码兼容！所以如果你习惯于 ASCII，UTF-8 就是一样的！每个 ASCII 编码的文档也是 UTF-8 编码的！(但显然反过来不行。)

It's probably that last point more than any other that is driving UTF-8 to take over the world.

> 这可能是最后一点比其他任何东西更有助于 UTF-8 夺取世界统治地位。

## [27.4] Source and Execution Character Sets {#src-exec-charset number="27.4"}

When programming in C, there are (at least) three character sets that are in play:

> 当使用 C 语言编程时，至少有三种字符集可用：

- The one that your code exists on disk as.
- The one the compiler translates that into just as compilation begins (the _source character set_). This might be the same as the one on disk, or it might not.

> 编译器开始编译时将其转换为的(源字符集)。这可能与磁盘上的相同，也可能不同。

- The one the compiler translates the source character set into for execution (the _execution character set_). This might be the same as the source character set, or it might not.

> 编译器将源字符集转换为执行字符集(执行字符集)。这可能与源字符集相同，也可能不同。

Your compiler probably has options to select these character sets at build-time.

> 你的编译器可能有选项可以在构建时选择这些字符集。

The basic character set for both source and execution will contain the following characters:

> 基本字符集既用于源代码又用于执行程序将包含以下字符：

::: {#cb527 .sourceCode}

```{.sourceCode .default}
A B C D E F G H I J K L M
N O P Q R S T U V W X Y Z
a b c d e f g h i j k l m
n o p q r s t u v w x y z
0 1 2 3 4 5 6 7 8 9
! " # % & ' ( ) * + , - . / :
; < = > ? [ \ ] ^ _ { | } ~
space tab vertical-tab
form-feed end-of-line
```

:::

Those are the characters you can use in your source and remain 100% portable.

> 这些是您可以在源代码中使用并保持 100％可移植性的字符。

The execution character set will additionally have characters for alert (bell/flash), backspace, carriage return, and newline.

> 执行字符集还将具有用于警报(铃声/闪光)，退格，回车和换行的字符。

But most people don't go to that extreme and freely use their extended character sets in source and executable, especially now that Unicode and UTF-8 are getting more common. I mean, the basic character set doesn't even allow for `@`, `$`, or `` ` ``!

> 但大多数人不会走到极端，自由地在源代码和可执行文件中使用扩展字符集，尤其是现在 Unicode 和 UTF-8 变得越来越普遍。我的意思是，基本字符集甚至不允许使用 `@`，`$` 或 `` ` ``！

Notably, it's a pain (though possible with escape sequences) to enter Unicode characters using only the basic character set.

> 显而易见，只使用基本字符集输入 Unicode 字符是一件痛苦的事(尽管可以通过转义序列实现)。

## [27.5] Unicode in C {#unicode-in-c number="27.5"}

Before I get into encoding in C, let's talk about Unicode from a code point standpoint. There is a way in C to specify Unicode characters and these will get translated by the compiler into the execution character set[^163^].

> 在我们讨论 C 中的编码之前，让我们从代码点的角度来谈谈 Unicode。C 中有一种方法可以指定 Unicode 字符，这些字符将由编译器转换为执行字符集。

So how do we do it?

How about the euro symbol, code point 0x20AC. (I've written it in hex because both ways of representing it in C require hex.) How can we put that in our C code?

> 关于欧元符号，代码点 0x20AC(我以十六进制的方式表示，因为在 C 语言中表示它的两种方式都需要十六进制)。我们怎样在 C 代码中放置它？

Use the `\u` escape to put it in a string, e.g. `"\u20AC"` (case for the hex doesn't matter). You must put **exactly four** hex digits after the `\u`, padding with leading zeros if necessary.

> 使用 `\u` 转义符将其放入字符串中，例如 `"\u20AC"`(十六进制的大小写不重要)。你必须在 `\u` 后面**恰好**输入四个十六进制数字，如果需要，可以在前面补零。

Here's an example:

::: {#cb528 .sourceCode}

```c
char *s = "\u20AC1.23";

printf("%s\n", s);  // €1.23
```

:::

So `\u` works for 16-bit Unicode code points, but what about ones bigger than 16 bits? For that, we need capitals: `\U`.

> 所以\u 可以用于 16 位 Unicode 代码点，那么大于 16 位的呢？对于这个，我们需要大写字母：\U。

For example:

::: {#cb529 .sourceCode}

```c
char *s = "\U0001D4D1";

printf("%s\n", s);  // Prints a mathematical letter "B"
```

:::

It's the same as `\u`, just with 32 bits instead of 16. These are equivalent:

> 这和'\u'一样，只是用 32 位代替了 16 位。这些是等价的：

::: {#cb530 .sourceCode}

```c
\u03C0
\U000003C0
```

:::

Again, these are translated into the execution character set during compilation. They represent Unicode code points, not any specific encoding. Furthermore, if a Unicode code point is not representable in the execution character set, the compiler can do whatever it wants with it.

> 再次，这些在编译期间会被转换成执行字符集。它们代表的是 Unicode 代码点，而不是任何特定的编码。此外，如果 Unicode 代码点不能在执行字符集中表示，编译器可以对它做任何事情。

Now, you might wonder why you can't just do this:

::: {#cb531 .sourceCode}

```c
char *s = "€1.23";

printf("%s\n", s);  // €1.23
```

:::

And you probably can, given a modern compiler. The source character set will be translated for you into the execution character set by the compiler. But compilers are free to puke out if they find any characters that aren't included in their extended character set, and the € symbol certainly isn't in the basic character set.

> 给定一个现代编译器，你可能可以做到。源字符集将由编译器为您转换为执行字符集。但是，如果编译器发现不包含在其扩展字符集中的任何字符，它们可能会吐出，而 € 符号肯定不在基本字符集中。

Caveat from the spec: you can't use `\u` or `\U` to encode any code points below 0xA0 except for 0x24 (`$`), 0x40 (`@`), and 0x60 (`` ` ``)---yes, those are precisely the trio of common punctuation marks missing from the basic character set. Apparently this restriction is relaxed in the upcoming version of the spec.

> 规范中的警告：您不能使用\u 或\U 来编码基本字符集中缺少的常见标点符号 0x24($)、0x40(@)和 0x60(` `)以下的任何代码点，显然，这种限制在规范的新版本中已经放宽。

Finally, you can also use these in identifiers in your code, with some restrictions. But I don't want to get into that here. We're all about string handling in this chapter.

> 最后，您也可以在代码中的标识符中使用这些，但有一些限制。但我不想在这里讨论。我们本章节的主题是字符串处理。

And that's about it for Unicode in C (except encoding).

## [27.6] A Quick Note on UTF-8 Before We Swerve into the Weeds {#utf8-quick number="27.6"}

It could be that your source file on disk, the extended source characters, and the extended execution characters are all in UTF-8 format. And the libraries you use expect UTF-8. This is the glorious future of UTF-8 everywhere.

> 可能是您磁盘上的源文件、扩展源字符和扩展执行字符都是 UTF-8 格式的。而您使用的库期望 UTF-8。这就是 UTF-8 无处不在的美好未来。

If that's the case, and you don't mind being non-portable to systems that aren't like that, then just run with it. Stick Unicode characters in your source and data at will. Use regular C strings and be happy.

> 如果是这样的话，而且你不介意在那些不像这样的系统上不可移植，那就继续这样做吧。随意地在源代码和数据中放入 Unicode 字符。使用普通的 C 字符串，然后开心地享受它们吧。

A lot of things will just work (albeit non-portably) because UTF-8 strings can safely be NUL-terminated just like any other C string. But maybe losing portability in exchange for easier character handling is a tradeoff that's worth it to you.

> 很多事情会正常工作(尽管不能移植)，因为 UTF-8 字符串可以像其他 C 字符串一样安全地以 NUL 结尾。但也许为了更容易处理字符而牺牲移植性可能是值得的折衷。

There are some caveats, however:

- Things like `strlen()` report the number of bytes in a string, not the number of characters, necessarily. (The `mbstowcs()` returns the number of characters in a string when you convert it to wide characters. POSIX extends this so you can pass `NULL` for the first argument if you just want the character count.)

> 事情像 `strlen()` 报告字符串中的字节数，不一定是字符数。(`mbstowcs()` 在将字符串转换为宽字符时会返回字符数。POSIX 扩展了这一功能，因此如果只想获得字符数，可以将第一个参数传递为 `NULL`。)

- The following won't work properly with characters of more than one byte: `strtok()`, `strchr()` (use `strstr()` instead), `strspn()`-type functions, `toupper()`, `tolower()`, `isalpha()`-type functions, and probably more. Beware anything that operates on bytes.

> 以下函数不能正确处理多字节字符：strtok()、strchr()(改用 strstr())、strspn()类函数、toupper()、tolower()、isalpha()类函数等，可能还有更多。请注意任何操作字节的函数。

- `printf()` variants allow for a way to only print so many bytes of a string[^164^]. You want to make certain you print the correct number of bytes to end on a character boundary.

> `printf()` 的变体允许一种方式只打印字符串的一部分字节[^164^]。你想确保你打印正确数量的字节以结束在一个字符边界上。

- If you want to `malloc()` space for a string, or declare an array of `char` s for one, be aware that the maximum size could be more than you were expecting. Each character could take up to `MB_LEN_MAX` bytes (from `<limits.h>`)---except characters in the basic character set which are guaranteed to be one byte.

> 如果你想要为字符串 `malloc()` 空间，或者声明一个 `char` 数组，请注意最大尺寸可能比你预期的要大。每个字符可能占用多达 `MB_LEN_MAX` 字节(来自 `<limits.h>`)—— 除了基本字符集中被保证为一个字节的字符。

And probably others I haven't discovered. Let me know what pitfalls there are out there...

> 可能还有我没发现的其他问题。请告诉我外面还有哪些陷阱……

## [27.7] Different Character Types {#different-character-types number="27.7"}

I want to introduce more character types. We're used to `char`, right?

But that's too easy. Let's make things a lot more difficult! Yay!

### [27.7.1] Multibyte Characters {#multibyte-characters number="27.7.1"}

First of all, I want to potentially change your thinking about what a string (array of `char` s) is. These are _multibyte strings_ made up of _multibyte characters_.

> 首先，我想改变你对字符串(字符数组)的想法。这些是由多字节字符组成的多字节字符串。

That's right---your run-of-the-mill string of characters is multibyte. When someone says "C string", they mean "C multibyte string".

> 没错，一般的字符串是多字节的。当有人说“C 字符串”时，他们指的是“C 多字节字符串”。

Even if a particular character in the string is only a single byte, or if a string is made up of only single characters, it's known as a multibyte string.

> 即使字符串中的某个特定字符只有一个字节，或者字符串只由单个字符组成，它也被称为多字节字符串。

For example:

::: {#cb532 .sourceCode}

```c
char c[128] = "Hello, world!";  // Multibyte string
```

:::

What we're saying here is that a particular character that's not in the basic character set could be composed of multiple bytes. Up to `MB_LEN_MAX` of them (from `<limits.h>`). Sure, it only looks like one character on the screen, but it could be multiple bytes.

> 我们这里说的是，一个不在基本字符集中的特定字符可以由多个字节组成。最多可以有 `MB_LEN_MAX` 个字节(来自 `<limits.h>`)。当然，它只在屏幕上看起来像一个字符，但它可能是多个字节。

You can throw Unicode values in there, as well, as we saw earlier:

::: {#cb533 .sourceCode}

```c
char *s = "\u20AC1.23";

printf("%s\n", s);  // €1.23
```

:::

But here we're getting into some weirdness, because check this out:

::: {#cb534 .sourceCode}

```c
char *s = "\u20AC1.23";  // €1.23

printf("%zu\n", strlen(s));  // 7!
```

:::

The string length of `"€1.23"` is `7`?! Yes! Well, on my system, yes! Remember that `strlen()` returns the number of bytes in the string, not the number of characters. (When we get to "wide characters", coming up, we'll see a way to get the number of characters in the string.)

> "€1.23"的字符串长度是 7？！是的！好吧，在我的系统上是的！记住，`strlen()` 返回字符串中的字节数，而不是字符数。(当我们到达“宽字符”时，我们将看到一种获取字符串中字符数的方法。)

Note that while C allows individual multibyte `char` constants (as opposed to `char*`), the behavior of these varies by implementation and your compiler might warn on it.

> 注意，虽然 C 允许单独的多字节 `char` 常量(而不是 `char*`)，但这些变量的行为因实现而异，您的编译器可能会发出警告。

GCC, for example, warns of multi-character character constants for the following two lines (and, on my system, prints out the UTF-8 encoding):

> GCC，例如，会警告以下两行的多字符字符常量(并且，在我的系统上，会输出 UTF-8 编码)：

::: {#cb535 .sourceCode}

```c
printf("%x\n", '€');
printf("%x\n", '\u20ac');
```

:::

### [27.7.2] Wide Characters {#wide-characters number="27.7.2"}

If you're not a multibyte character, then you're a _wide character_.

A wide character is a single value that can uniquely represent any character in the current locale. It's analogous to Unicode code points. But it might not be. Or it might be.

> 一个宽字符是一个单一的值，可以唯一表示当前区域设置中的任何字符。它类似于 Unicode 代码点。但它可能不是。或者它可能是。

Basically, where multibyte character strings are arrays of bytes, wide character strings are arrays of _characters_. So you can start thinking on a character-by-character basis rather than a byte-by-byte basis (the latter of which gets all messy when characters start taking up variable numbers of bytes).

> 基本上，多字节字符串是字节数组，宽字符串是字符数组。因此，您可以以字符为基础而不是以字节为基础(当字符开始占用可变数量的字节时，后者变得非常混乱)开始思考。

Wide characters can be represented by a number of types, but the big standout one is `wchar_t`. It's the main one. It's like `char`, except wide.

> 宽字符可以由多种类型表示，但最引人注目的是 `wchar_t`。它是主要的一种。它就像 `char`，只是更宽。

You might be wondering if you can't tell if it's Unicode or not, how does that allow you much flexibility in terms of writing code? `wchar_t` opens some of those doors, as there are a rich set of functions you can use to deal with `wchar_t` strings (like getting the length, etc.) without caring about the encoding.

> 如果你不能判断它是不是 Unicode，那么这种情况又如何让你在编写代码时有更多的灵活性呢？`wchar_t` 可以为你打开一些大门，因为它提供了一系列丰富的函数，可以用来处理 `wchar_t` 字符串(例如获取长度等)，而无需关心编码。

## [27.8] Using Wide Characters and `wchar_t` {#using-wide-characters-and-wchar_t number="27.8"}

Time for a new type: `wchar_t`. This is the main wide character type. Remember how a `char` is only one byte? And a byte's not enough to represent all characters, potentially? Well, this one is enough.

> 是时候使用一种新类型了：`wchar_t`。这是主要的宽字符类型。还记得 `char` 只有一个字节吗？一个字节不足以表示所有字符，对吗？好吧，这个足够了。

To use `wchar_t`, include `<wchar.h>`.

How many bytes big is it? Well, it's not totally clear. Could be 16 bits. Could be 32 bits.

> 它有多大？嗯，这不太清楚。可能是 16 位。可能是 32 位。

But wait, you're saying---if it's only 16 bits, it's not big enough to hold all the Unicode code points, is it? You're right---it's not. The spec doesn't require it to be. It just has to be able to represent all the characters in the current locale.

> 但等等，你是说---如果只有 16 位，它不够大来容纳所有的 Unicode 代码点，是吗？你是对的---它不够。规范并不要求它必须是这样。它只需要能够表示当前区域的所有字符即可。

This can cause grief with Unicode on platforms with 16-bit `wchar_t` s (ahem---Windows). But that's out of scope for this guide.

> 这可能会在使用 16 位 `wchar_t` 的平台上(咳---Windows)导致 Unicode 出现问题。但这已经超出了本指南的范围。

You can declare a string or character of this type with the `L` prefix, and you can print them with the `%ls` ("ell ess") format specifier. Or print an individual `wchar_t` with `%lc`.

> 你可以使用 `L` 前缀声明这种类型的字符串或字符，并使用 `%ls`("ell ess")格式说明符来打印它们。或者使用 `%lc` 来打印单个 `wchar_t`。

::: {#cb536 .sourceCode}

```c
wchar_t *s = L"Hello, world!";
wchar_t c = L'B';

printf("%ls %lc\n", s, c);
```

:::

Now---are those characters stored as Unicode code points, or not? Depends on the implementation. But you can test if they are with the macro `__STDC_ISO_10646__`. If this is defined, the answer is, "It's Unicode!"

> 现在---这些字符是否以 Unicode 代码点存储？取决于实现。但是你可以使用宏 `__STDC_ISO_10646__` 来测试。如果定义了，答案就是："这是 Unicode！"

More detailedly, the value in that macro is an integer in the form `yyyymm` that lets you know what Unicode standard you can rely on---whatever was in effect on that date.

> 详细来说，该宏的值是一个以 `yyyymm` 形式的整数，它可以告诉您可以依赖哪个 Unicode 标准---无论是在那个日期生效的标准。

But how do you use them?

### [27.8.1] Multibyte to `wchar_t` Conversions {#multibyte-to-wchar_t-conversions number="27.8.1"}

So how do we get from the byte-oriented standard strings to the character-oriented wide strings and back?

> 那么，我们如何从基于字节的标准字符串转换到基于字符的宽字符串，又如何回来？

We can use a couple string conversion functions to make this happen.

First, some naming conventions you'll see in these functions:

- `mb`: multibyte
- `wc`: wide character
- `mbs`: multibyte string
- `wcs`: wide character string

So if we want to convert a multibyte string to a wide character string, we can call the `mbstowcs()`. And the other way around: `wcstombs()`.

> 如果我们想把多字节字符串转换成宽字符串，我们可以调用 `mbstowcs()` 函数。反之，可以调用 `wcstombs()` 函数。

---

Conversion Function Description

---

`mbtowc()` Convert a multibyte character to a wide character.

`wctomb()` Convert a wide character to a multibyte character.

`mbstowcs()` Convert a multibyte string to a wide string.

## `wcstombs()` Convert a wide string to a multibyte string.

Let's do a quick demo where we convert a multibyte string to a wide character string, and compare the string lengths of the two using their respective functions.

> 让我们做一个快速演示，将多字节字符串转换为宽字符串，并使用各自的函数比较两个字符串的长度。

::: {#cb537 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <wchar.h>
#include <string.h>
#include <locale.h>

int main(void)
{
    // Get out of the C locale to one that likely has the euro symbol
    setlocale(LC_ALL, "");

    // Original multibyte string with a euro symbol (Unicode point 20ac)
    char *mb_string = "The cost is \u20ac1.23";  // €1.23
    size_t mb_len = strlen(mb_string);

    // Wide character array that will hold the converted string
    wchar_t wc_string[128];  // Holds up to 128 wide characters

    // Convert the MB string to WC; this returns the number of wide chars
    size_t wc_len = mbstowcs(wc_string, mb_string, 128);

    // Print result--note the %ls for wide char strings
    printf("multibyte: \"%s\" (%zu bytes)\n", mb_string, mb_len);
    printf("wide char: \"%ls\" (%zu characters)\n", wc_string, wc_len);
}
```

:::

On my system, this outputs:

::: {#cb538 .sourceCode}

```{.sourceCode .default}
multibyte: "The cost is €1.23" (19 bytes)
wide char: "The cost is €1.23" (17 characters)
```

:::

(Your system might vary on the number of bytes depending on your locale.)

One interesting thing to note is that `mbstowcs()`, in addition to converting the multibyte string to wide, returns the length (in characters) of the wide character string. On POSIX-compliant systems, you can take advantage of a special mode where it _only_ returns the length-in-characters of a given multibyte string: you just pass `NULL` to the destination, and `0` to the maximum number of characters to convert (this value is ignored).

> 注意一件有趣的事情是，`mbstowcs()` 不仅可以将多字节字符串转换为宽字符，还可以返回字符串的长度(以字符为单位)。在符合 POSIX 标准的系统上，您可以利用一种特殊模式，只返回给定多字节字符串的字符长度：只需将 `NULL` 传递给目标，将 `0` 传递给要转换的最大字符数(此值将被忽略)。

(In the code below, I'm using my extended source character set---you might have to replace those with `\u` escapes.)

> 在下面的代码中，我正在使用我的扩展源字符集---您可能需要用 `\u` 转义替换它们。

::: {#cb539 .sourceCode}

```c
setlocale(LC_ALL, "");

// The following string has 7 characters
size_t len_in_chars = mbstowcs(NULL, "§¶°±π€•", 0);

printf("%zu", len_in_chars);  // 7
```

:::

Again, that's a non-portable POSIX extension.

And, of course, if you want to convert the other way, it's `wcstombs()`.

## [27.9] Wide Character Functionality {#wide-character-functionality number="27.9"}

Once we're in wide character land, we have all kinds of functionality at our disposal. I'm just going to summarize a bunch of the functions here, but basically what we have here are the wide character versions of the multibyte string functions that we're use to. (For example, we know `strlen()` for multibyte strings; there's a `wcslen()` for wide character strings.)

> 一旦我们进入宽字符领域，我们就有各种功能可供使用。我只是简要概括一些函数，但基本上我们这里有我们熟悉的多字节字符串函数的宽字符版本。(例如，我们知道多字节字符串的 `strlen()`; 宽字符串有 `wcslen()`。)

### [27.9.1] `wint_t` {#wint_t number="27.9.1"}

A lot of these functions use a `wint_t` to hold single characters, whether they are passed in or returned.

> 这些函数中有许多使用 `wint_t` 来存储单个字符，无论是传入的还是返回的。

It is related to `wchar_t` in nature. A `wint_t` is an integer that can represent all values in the extended character set, and also a special end-of-file character, `WEOF`.

> 它在本质上与 `wchar_t` 有关。`wint_t` 是一个整数，可以表示扩展字符集中的所有值，以及特殊的文件结束字符 `WEOF`。

This is used by a number of single-character-oriented wide character functions.

> 这被一些以单个字符为导向的宽字符函数所使用。

### [27.9.2] I/O Stream Orientation {#io-stream-orientation number="27.9.2"}

The tl;dr here is to not mix and match byte-oriented functions (like `fprintf()`) with wide-oriented functions (like `fwprintf()`). Decide if a stream will be byte-oriented or wide-oriented and stick with those types of I/O functions.

> 这里的简要说明是：不要混合使用字节导向函数(比如 `fprintf()`)和宽字节导向函数(比如 `fwprintf()`)。决定一个流是字节导向还是宽字节导向，并且只使用这种类型的 I/O 函数。

In more detail: streams can be either byte-oriented or wide-oriented. When a stream is first created, it has no orientation, but the first read or write will set the orientation.

> 流可以是字节导向的或宽导向的。当流首次创建时，它没有方向，但第一次读取或写入将设置方向。

If you first use a wide operation (like `fwprintf()`) it will orient the stream wide.

> 如果你首先使用一个宽操作(比如 `fwprintf()`)，它将会定向流宽。

If you first use a byte operation (like `fprintf()`) it will orient the stream by bytes.

> 如果你首先使用字节操作(如 `fprintf()`)，它将按字节定向流。

You can manually set an unoriented stream one way or the other with a call to `fwide()`. You can use that same function to get the orientation of a stream.

> 你可以通过调用 `fwide()` 来手动将一个未定向流设置为一个方向或另一个方向。你可以使用相同的函数来获取流的定向。

If you need to change the orientation mid-flight, you can do it with `freopen()`.

> 如果你需要在飞行中改变方向，你可以使用 `freopen()` 来实现。

### [27.9.3] I/O Functions {#io-functions number="27.9.3"}

Typically include `<stdio.h>` and `<wchar.h>` for these.

---

I/O Function Description

---

`wprintf()` Formatted console output.

`wscanf()` Formatted console input.

`getwchar()` Character-based console input.

`putwchar()` Character-based console output.

`fwprintf()` Formatted file output.

`fwscanf()` Formatted file input.

`fgetwc()` Character-based file input.

`fputwc()` Character-based file output.

`fgetws()` String-based file input.

`fputws()` String-based file output.

`swprintf()` Formatted string output.

`swscanf()` Formatted string input.

`vfwprintf()` Variadic formatted file output.

`vfwscanf()` Variadic formatted file input.

`vswprintf()` Variadic formatted string output.

`vswscanf()` Variadic formatted string input.

`vwprintf()` Variadic formatted console output.

`vwscanf()` Variadic formatted console input.

`ungetwc()` Push a wide character back on an output stream.

## `fwide()` Get or set stream multibyte/wide orientation.

### [27.9.4] Type Conversion Functions {#type-conversion-functions number="27.9.4"}

Typically include `<wchar.h>` for these.

---

Conversion Function Description

---

`wcstod()` Convert string to `double`.

`wcstof()` Convert string to `float`.

`wcstold()` Convert string to `long double`.

`wcstol()` Convert string to `long`.

`wcstoll()` Convert string to `long long`.

`wcstoul()` Convert string to `unsigned long`.

## `wcstoull()` Convert string to `unsigned long long`.

### [27.9.5] String and Memory Copying Functions {#string-and-memory-copying-functions number="27.9.5"}

Typically include `<wchar.h>` for these.

---

Copying Function Description

---

`wcscpy()` Copy string.

`wcsncpy()` Copy string, length-limited.

`wmemcpy()` Copy memory.

`wmemmove()` Copy potentially-overlapping memory.

`wcscat()` Concatenate strings.

## `wcsncat()` Concatenate strings, length-limited.

### [27.9.6] String and Memory Comparing Functions {#string-and-memory-comparing-functions number="27.9.6"}

Typically include `<wchar.h>` for these.

---

Comparing Function Description

---

`wcscmp()` Compare strings lexicographically.

`wcsncmp()` Compare strings lexicographically, length-limited.

`wcscoll()` Compare strings in dictionary order by locale.

`wmemcmp()` Compare memory lexicographically.

## `wcsxfrm()` Transform strings into versions such that `wcscmp()` behaves like `wcscoll()`[^165^].

### [27.9.7] String Searching Functions {#string-searching-functions number="27.9.7"}

Typically include `<wchar.h>` for these.

---

Searching Function Description

---

`wcschr()` Find a character in a string.

`wcsrchr()` Find a character in a string from the back.

`wmemchr()` Find a character in memory.

`wcsstr()` Find a substring in a string.

`wcspbrk()` Find any of a set of characters in a string.

`wcsspn()` Find length of substring including any of a set of characters.

`wcscspn()` Find length of substring before any of a set of characters.

## `wcstok()` Find tokens in a string.

### [27.9.8] Length/Miscellaneous Functions {#lengthmiscellaneous-functions number="27.9.8"}

Typically include `<wchar.h>` for these.

---

Length/Misc Function Description

---

`wcslen()` Return the length of the string.

`wmemset()` Set characters in memory.

## `wcsftime()` Formatted date and time output.

### [27.9.9] Character Classification Functions {#character-classification-functions number="27.9.9"}

Include `<wctype.h>` for these.

---

Length/Misc Function Description

---

`iswalnum()` True if the character is alphanumeric.

`iswalpha()` True if the character is alphabetic.

`iswblank()` True if the character is blank (space-ish, but not a newline).

`iswcntrl()` True if the character is a control character.

`iswdigit()` True if the character is a digit.

`iswgraph()` True if the character is printable (except space).

`iswlower()` True if the character is lowercase.

`iswprint()` True if the character is printable (including space).

`iswpunct()` True if the character is punctuation.

`iswspace()` True if the character is whitespace.

`iswupper()` True if the character is uppercase.

`iswxdigit()` True if the character is a hex digit.

`towlower()` Convert character to lowercase.

## `towupper()` Convert character to uppercase.

## [27.10] Parse State, Restartable Functions {#parse-state-restartable-functions number="27.10"}

We're going to get a little bit into the guts of multibyte conversion, but this is a good thing to understand, conceptually.

> 我们将深入了解多字节转换，但这是一个值得理解的概念。

Imagine how your program takes a sequence of multibyte characters and turns them into wide characters, or vice-versa. It might, at some point, be partway through parsing a character, or it might have to wait for more bytes before it makes the determination of the final value.

> 想象一下，你的程序如何将一系列多字节字符转换为宽字符，或者反之亦然。它可能会在某个时刻处于解析字符的过程中，或者可能需要等待更多字节才能确定最终值。

This parse state is stored in an opaque variable of type `mbstate_t` and is used every time conversion is performed. That's how the conversion functions keep track of where they are mid-work.

> 这个解析状态存储在一个不透明的变量中，类型为 `mbstate_t`，每次转换时都会使用它。这就是转换函数在工作过程中如何跟踪它们的位置的方式。

And if you change to a different character sequence mid-stream, or try to seek to a different place in your input sequence, it could get confused over that.

> 如果你在流中间改变不同的字符序列，或者试图寻找输入序列中的不同位置，它可能会感到困惑。

Now you might want to call me on this one: we just did some conversions, above, and I never mentioned any `mbstate_t` anywhere.

> 现在你可能想让我来解释一下：我们刚刚做了一些转换，但是我从没提到任何 `mbstate_t`。

That's because the conversion functions like `mbstowcs()`, `wctomb()`, etc. each have their own `mbstate_t` variable that they use. There's only one per function, though, so if you're writing multithreaded code, they're not safe to use.

> 因为像 `mbstowcs()`、`wctomb()` 等转换函数都有自己的 `mbstate_t` 变量，只有一个。所以，如果你写的是多线程代码，它们就不安全可用了。

Fortunately, C defines _restartable_ versions of these functions where you can pass in your own `mbstate_t` on per-thread basis if you need to. If you're doing multithreaded stuff, use these!

> 幸运的是，C 定义了这些函数的_可重启_版本，如果您需要，可以在每个线程上传递自己的 `mbstate_t`。如果您正在进行多线程操作，请使用这些！

Quick note on initializing an `mbstate_t` variable: just `memset()` it to zero. There is no built-in function to force it to be initialized.

> 快速记录初始化 `mbstate_t` 变量：只需使用 `memset()` 将其设置为零。没有内置函数来强制将其初始化。

::: {#cb540 .sourceCode}

```c
mbstate_t mbs;

// Set the state to the initial state
memset(&mbs, 0, sizeof mbs);
```

:::

Here is a list of the restartable conversion functions---note the naming convension of putting an "`r`" after the "from" type:

> 这里是可重启转换函数的列表---注意以"`r`"结尾的"from"类型的命名约定：

- `mbrtowc()`---multibyte to wide character
- `wcrtomb()`---wide character to multibyte
- `mbsrtowcs()`---multibyte string to wide character string
- `wcsrtombs()`---wide character string to multibyte string

These are really similar to their non-restartable counterparts, except they require you pass in a pointer to your own `mbstate_t` variable. And also they modify the source string pointer (to help you out if invalid bytes are found), so it might be useful to save a copy of the original.

> 这些与它们的非重启式对应物非常相似，只是它们需要您传入一个指向自己的 `mbstate_t` 变量的指针。此外，它们还会修改源字符串指针(如果发现无效字节，可以帮助您)，因此保存原始副本可能很有用。

Here's the example from earlier in the chapter reworked to pass in our own `mbstate_t`.

> 这里是第一章早先的例子，重新编写以传入我们自己的 mbstate_t。

::: {#cb541 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <stddef.h>
#include <wchar.h>
#include <string.h>
#include <locale.h>

int main(void)
{
    // Get out of the C locale to one that likely has the euro symbol
    setlocale(LC_ALL, "");

    // Original multibyte string with a euro symbol (Unicode point 20ac)
    char *mb_string = "The cost is \u20ac1.23";  // €1.23
    size_t mb_len = strlen(mb_string);

    // Wide character array that will hold the converted string
    wchar_t wc_string[128];  // Holds up to 128 wide characters

    // Set up the conversion state
    mbstate_t mbs;
    memset(&mbs, 0, sizeof mbs);  // Initial state

    // mbsrtowcs() modifies the input pointer to point at the first
    // invalid character, or NULL if successful. Let's make a copy of
    // the pointer for mbsrtowcs() to mess with so our original is
    // unchanged.
    //
    // This example will probably be successful, but we check farther
    // down to see.
    const char *invalid = mb_string;

    // Convert the MB string to WC; this returns the number of wide chars
    size_t wc_len = mbsrtowcs(wc_string, &invalid, 128, &mbs);

    if (invalid == NULL) {
        printf("No invalid characters found\n");

        // Print result--note the %ls for wide char strings
        printf("multibyte: \"%s\" (%zu bytes)\n", mb_string, mb_len);
        printf("wide char: \"%ls\" (%zu characters)\n", wc_string, wc_len);
    } else {
        ptrdiff_t offset = invalid - mb_string;
        printf("Invalid character at offset %td\n", offset);
    }
}
```

:::

For the conversion functions that manage their own state, you can reset their internal state to the initial one by passing in `NULL` for their `char*` arguments, for example:

> 对于管理自身状态的转换函数，您可以通过将 `NULL` 传递给它们的 `char*` 参数来将其内部状态重置为初始状态，例如：

::: {#cb542 .sourceCode}

```c
mbstowcs(NULL, NULL, 0);   // Reset the parse state for mbstowcs()
mbstowcs(dest, src, 100);  // Parse some stuff
```

:::

For I/O, each wide stream manages its own `mbstate_t` and uses that for input and output conversions as it goes.

> 对于 I/O，每个宽流都管理自己的 `mbstate_t`，并在输入和输出转换时使用它。

And some of the byte-oriented I/O functions like `printf()` and `scanf()` keep their own internal state while doing their work.

> 一些字节导向的 I/O 函数，如 `printf()` 和 `scanf()` 在工作的时候会保持它们自己的内部状态。

Finally, these restartable conversion functions do actually have their own internal state if you pass in `NULL` for the `mbstate_t` parameter. This makes them behave more like their non-restartable counterparts.

> 最后，如果您将 `NULL` 传递给 `mbstate_t` 参数，这些可重新启动的转换函数实际上具有自己的内部状态。这使它们更像它们的非重新启动对应物。

## [27.11] Unicode Encodings and C {#unicode-encodings-and-c number="27.11"}

In this section, we'll see what C can (and can't) do when it comes to three specific Unicode encodings: UTF-8, UTF-16, and UTF-32.

> 在这一节中，我们将看到 C 在三种特定的 Unicode 编码(UTF-8、UTF-16 和 UTF-32)方面能(和不能)做什么。

### [27.11.1] UTF-8 {#utf-8 number="27.11.1"}

To refresh before this section, read the [UTF-8 quick note, above](#utf8-quick).

> 在这一节之前，请阅读上面的 [UTF-8 快速笔记](#utf8-quick)以进行刷新。

Aside from that, what are C's UTF-8 capabilities?

Well, not much, unfortunately.

You can tell C that you specifically want a string literal to be UTF-8 encoded, and it'll do it for you. You can prefix a string with `u8`:

> 你可以告诉 C 你特别想要一个字符串文字以 UTF-8 编码，它会为你做到。你可以用 `u8` 前缀一个字符串：

::: {#cb543 .sourceCode}

```c
char *s = u8"Hello, world!";

printf("%s\n", s);   // Hello, world!--if you can output UTF-8
```

:::

Now, can you put Unicode characters in there?

::: {#cb544 .sourceCode}

```c
char *s = u8"€123";
```

:::

Sure! If the extended source character set supports it. (gcc does.)

What if it doesn't? You can specify a Unicode code point with your friendly neighborhood `\u` and `\U`, [as noted above](#unicode-in-c).

> 如果不行怎么办？你可以使用你友好的 `\u` 和 `\U` 指定一个 Unicode 代码点，如上文所述(#unicode-in-c)。

But that's about it. There's no portable way in the standard library to take arbirary input and turn it into UTF-8 unless your locale is UTF-8. Or to parse UTF-8 unless your locale is UTF-8.

> 但是就是这样了。标准库中没有可以将任意输入转换为 UTF-8 的便携式方法，除非你的语言环境是 UTF-8。或者解析 UTF-8，除非你的语言环境是 UTF-8。

So if you want to do it, either be in a UTF-8 locale and:

::: {#cb545 .sourceCode}

```c
setlocale(LC_ALL, "");
```

:::

or figure out a UTF-8 locale name on your local machine and set it explicitly like so:

::: {#cb546 .sourceCode}

```c
setlocale(LC_ALL, "en_US.UTF-8");  // Non-portable name
```

:::

Or use a [third-party library](#utf-3rd-party).

### [27.11.2] UTF-16, UTF-32, `char16_t`, and `char32_t` {#utf-16-utf-32-char16_t-and-char32_t number="27.11.2"}

`char16_t` and `char32_t` are a couple other potentially wide character types with sizes of 16 bits and 32 bits, respectively. Not necessarily wide, because if they can't represent every character in the current locale, they lose their wide character nature. But the spec refers them as "wide character" types all over the place, so there we are.

These are here to make things a little more Unicode-friendly, potentially.

> 这些是为了让事情变得更加 Unicode 友好，可能会有所帮助。

To use, include `<uchar.h>`. (That's "u", not "w".)

This header file doesn't exist on OS X---bummer. If you just want the types, you can:

> 这个头文件在 OS X 上不存在---太糟糕了。如果你只想要类型，你可以：

::: {#cb547 .sourceCode}

```c
#include <stdint.h>

typedef int_least16_t char16_t;
typedef int_least32_t char32_t;
```

:::

But if you also want the functions, that's all on you.

Assuming you're still good to go, you can declare a string or character of these types with the `u` and `U` prefixes:

> 假设你仍然可以继续，你可以使用 `u` 和 `U` 前缀声明这些类型的字符串或字符：

::: {#cb548 .sourceCode}

```c
char16_t *s = u"Hello, world!";
char16_t c = u'B';

char32_t *t = U"Hello, world!";
char32_t d = U'B';
```

:::

Now---are values in these stored in UTF-16 or UTF-32? Depends on the implementation.

> 现在这些值是存储在 UTF-16 还是 UTF-32 中？取决于实现方式。

But you can test to see if they are. If the macros `__STDC_UTF_16__` or `__STDC_UTF_32__` are defined (to `1`) it means the types hold UTF-16 or UTF-32, respectively.

> 但是你可以测试看看它们是否如此。如果宏 `__STDC_UTF_16__` 或 `__STDC_UTF_32__` 被定义(为 `1`)，这意味着这些类型分别持有 UTF-16 或 UTF-32。

If you're curious, and I know you are, the values, if UTF-16 or UTF-32, are stored in the native endianess. That is, you should be able to compare them straight up to Unicode code point values:

> 如果你很好奇，我知道你是这样的，如果是 UTF-16 或 UTF-32，它们就存储在本地的字节序中。也就是说，你应该能够直接将它们与 Unicode 代码点值进行比较：

::: {#cb549 .sourceCode}

```c
char16_t pi = u"\u03C0";  // pi symbol

#if __STDC_UTF_16__
pi == 0x3C0;  // Always true
#else
pi == 0x3C0;  // Probably not true
#endif
```

:::

### [27.11.3] Multibyte Conversions {#multibyte-conversions number="27.11.3"}

You can convert from your multibyte encoding to `char16_t` or `char32_t` with a number of helper functions.

> 你可以使用一些辅助函数将多字节编码转换为 `char16_t` 或 `char32_t`。

(Like I said, though, the result might not be UTF-16 or UTF-32 unless the corresponding macro is set to `1`.)

> (正如我所说，除非相应的宏被设置为“1”，否则结果可能不是 UTF-16 或 UTF-32。)

All of these functions are restartable (i.e. you pass in your own `mbstate_t`), and all of them operate character by character[^166^].

> 所有这些函数都可以重新启动(即您传入自己的 `mbstate_t`)，它们都是逐字符操作的。

---

Conversion Function Description

---

`mbrtoc16()` Convert a multibyte character to a `char16_t` character.

`mbrtoc32()` Convert a multibyte character to a `char32_t` character.

`c16rtomb()` Convert a `char16_t` character to a multibyte character.

## `c32rtomb()` Convert a `char32_t` character to a multibyte character.

### [27.11.4] Third-Party Libraries {#utf-3rd-party number="27.11.4"}

For heavy-duty conversion between different specific encodings, there are a couple mature libraries worth checking out. Note that I haven't used either of these.

> 对于不同特定编码之间的重型转换，有几个成熟的库值得查看。注意，我没有使用这些库中的任何一个。

- [iconv](https://en.wikipedia.org/wiki/Iconv)[^167^]---Internationalization Conversion, a common POSIX-standard API available on the major platforms.
- [ICU](http://site.icu-project.org/)[^168^]---International Components for Unicode. At least one blogger found this easy to use.

If you have more noteworthy libraries, let me know.

# [28] Exiting a Program {#exiting-a-program number="28"}

Turns out there are a lot of ways to do this, and even ways to set up "hooks" so that a function runs when a program exits.

> 结果发现有很多种方法可以做到这一点，甚至可以设置“钩子”，以便当程序退出时运行函数。

In this chapter we'll dive in and check them out.

We already covered the meaning of the exit status code in the [Exit Status](#exit-status) section, so jump back there and review if you have to.

> 我们已经在[退出状态](#exit-status)部分讨论了退出状态代码的含义，如果需要，可以回去复习一下。

All the functions in this section are in `<stdlib.h>`.

## [28.1] Normal Exits {#normal-exits number="28.1"}

We'll start with the regular ways to exit a program, and then jump to some of the rarer, more esoteric ones.

> 我们从常规的程序退出方式开始，然后跳转到一些更罕见、更深奥的方式。

When you exit a program normally, all open I/O streams are flushed and temporary files removed. Basically it's a nice exit where everything gets cleaned up and handled. It's what you want to do almost all the time unless you have reasons to do otherwise.

> 当您正常退出一个程序时，所有打开的 I / O 流都会被刷新，临时文件也会被删除。 基本上，这是一个很好的退出，一切都会被清理和处理。 除非有特殊原因，否则几乎所有时候都是这样做的。

### [28.1.1] Returning From `main()` {#returning-from-main number="28.1.1"}

If you've noticed, `main()` has a return type of `int`... and yet I've rarely, if ever, been `return` ing anything from `main()` at all.

> 如果你注意到了，`main()` 有一个 `int` 类型的返回值... 但是我几乎从来没有从 `main()` 中 `return` 过任何东西。

This is because for `main()` only (and I can't stress enough this special case _only_ applies to `main()` and no other functions anywhere) has an _implicit_ `return 0` if you fall off the end.

> 因为只有 `main()`(我强调这种特殊情况只适用于 `main()`，不适用于任何其他函数)会隐式地返回 0，如果你从末尾跳出。

You can explicitly `return` from `main()` any time you want, and some programmers feel it's more _Right_ to always have a `return` at the end of `main()`. But if you leave it off, C will put one there for you.

> 你可以随时从 main()中显式地返回，有些程序员认为在 main()的末尾总是有一个返回语句更加正确。但是如果你省略了它，C 语言会为你添加一个。

So... here are the `return` rules for `main()`:

- You can return an exit status from `main()` with a `return` statement. `main()` is the only function with this special behavior. Using `return` in any other function just returns from that function to the caller.

> 你可以通过 `return` 语句从 `main()` 返回一个退出状态。`main()` 是唯一具有这种特殊行为的函数。在任何其他函数中使用 `return` 只是从该函数返回给调用者。

- If you don't explicitly `return` and just fall off the end of `main()`, it's just as if you'd returned `0` or `EXIT_SUCCESS`.

> 如果您没有明确地 `返回`，而只是从 `main()` 跌落，那就好像您已经返回了 `0` 或 `EXIT_SUCCESS` 一样。

### [28.1.2] `exit()` {#exit number="28.1.2"}

This one has also made an appearance a few times. If you call `exit()` from anywhere in your program, it will exit at that point.

> 这个也出现过几次。如果你在程序的任何地方调用 `exit()`，它将在那一点退出。

The argument you pass to `exit()` is the exit status.

### [28.1.3] Setting Up Exit Handlers with `atexit()` {#setting-up-exit-handlers-with-atexit number="28.1.3"}

You can register functions to be called when a program exits whether by returning from `main()` or calling the `exit()` function.

> 你可以注册函数，以便在程序从 `main()` 返回或调用 `exit()` 函数时调用。

A call to `atexit()` with the handler function name will get it done. You can register multiple exit handlers, and they'll be called in the reverse order of registration.

> 调用 `atexit()` 函数并提供处理函数名称即可完成。您可以注册多个退出处理程序，它们将按照注册的相反顺序调用。

Here's an example:

::: {#cb550 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

void on_exit_1(void)
{
    printf("Exit handler 1 called!\n");
}

void on_exit_2(void)
{
    printf("Exit handler 2 called!\n");
}

int main(void)
{
    atexit(on_exit_1);
    atexit(on_exit_2);

    printf("About to exit...\n");
}
```

:::

And the output is:

::: {#cb551 .sourceCode}

```{.sourceCode .default}
About to exit...
Exit handler 2 called!
Exit handler 1 called!
```

:::

## [28.2] Quicker Exits with `quick_exit()` {#quicker-exits-with-quick_exit number="28.2"}

This is similar to a normal exit, except:

- Open files might not be flushed.
- Temporary files might not be removed.
- `atexit()` handlers won't be called.

But there is a way to register exit handlers: call `at_quick_exit()` analogously to how you'd call `atexit()`.

> 但是有一种方法可以注册退出处理程序：类似于调用 `atexit()` 一样调用 `at_quick_exit()`。

::: {#cb552 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>

void on_quick_exit_1(void)
{
    printf("Quick exit handler 1 called!\n");
}

void on_quick_exit_2(void)
{
    printf("Quick exit handler 2 called!\n");
}

void on_exit(void)
{
    printf("Normal exit--I won't be called!\n");
}

int main(void)
{
    at_quick_exit(on_quick_exit_1);
    at_quick_exit(on_quick_exit_2);

    atexit(on_exit);  // This won't be called

    printf("About to quick exit...\n");

    quick_exit(0);
}
```

:::

Which gives this output:

::: {#cb553 .sourceCode}

```{.sourceCode .default}
About to quick exit...
Quick exit handler 2 called!
Quick exit handler 1 called!
```

:::

It works just like `exit()`/`atexit()`, except for the fact that file flushing and cleanup might not be done.

> 它的工作方式和 `exit()`/`atexit()` 一样，只是文件刷新和清理可能不会完成。

## [28.3] Nuke it from Orbit: `_Exit()` {#nuke-it-from-orbit-\_exit number="28.3"}

Calling `_Exit()` exits immediately, period. No on-exit callback functions are executed. Files won't be flushed. Temp files won't be removed.

> 调用 `_Exit()` 会立即退出，不会执行任何退出回调函数。文件不会被刷新，临时文件也不会被删除。

Use this if you have to exit _right fargin' now_.

## [28.4] Exiting Sometimes: `assert()` {#exiting-sometimes-assert number="28.4"}

The `assert()` statement is used to insist that something be true, or else the program will exit.

> 断言(assert)语句用于坚持某事为真，否则程序将退出。

Devs often use an assert to catch Should-Never-Happen type errors.

::: {#cb554 .sourceCode}

```c
#define PI 3.14159

assert(PI > 3);   // Sure enough, it is, so carry on
```

:::

versus:

::: {#cb555 .sourceCode}

```c
goats -= 100;

assert(goats >= 0);  // Can't have negative goats
```

:::

In that case, if I try to run it and `goats` falls under `0`, this happens:

> 在这种情况下，如果我尝试运行它，而“山羊”落入“0”，这就会发生：

::: {#cb556 .sourceCode}

```{.sourceCode .default}
goat_counter: goat_counter.c:8: main: Assertion `goats >= 0' failed.
Aborted
```

:::

and I'm dropped back to the command line.

This isn't very user-friendly, so it's only used for things the user will never see. And often people [write their own assert macros that can more easily be turned off](#my-assert).

> 这不是很友好的用户界面，所以它只用于用户永远看不到的东西。而且经常有人[写自己的断言宏，可以更容易地关闭](#my-assert)。

## [28.5] Abnormal Exit: `abort()` {#abnormal-exit-abort number="28.5"}

You can use this if something has gone horribly wrong and you want to indicate as much to the outside environment. This also won't necessarily clean up any open files, etc.

> 你可以使用这个，如果某事出现了糟糕的错误，你想向外部环境表明这一点。这也不一定会清理任何打开的文件等。

I've rarely seen this used.

Some foreshadowing about _signals_: this actually works by raising a `SIGABRT` which will end the process.

> 一些关于信号的预示：它实际上是通过抛出 `SIGABRT` 来结束进程的。

What happens after that is up to the system, but on Unix-likes, it was common to [dump core](https://en.wikipedia.org/wiki/Core_dump)[^169^] as the program terminated.

> 接下来发生什么取决于系统，但在类 Unix 系统中，在程序终止时通常会[转储内核](https://en.wikipedia.org/wiki/Core_dump)[^169^]。

# [29] Signal Handling {#signal-handling number="29"}

Before we start, I'm just going to advise you to generally ignore this entire chapter and use your OS's (very likely) superior signal handling functions. Unix-likes have the `sigaction()` family of functions, and Windows has... whatever it does[^170^].

> 在我们开始之前，我只是想建议你忽略整个章节，并使用你的操作系统(很可能)更优秀的信号处理函数。类 Unix 系统有 `sigaction()` 系列函数，而 Windows 有...它所做的任何事情[^170^]。

With that out of the way, what are signals?

## [29.1] What Are Signals? {#what-are-signals number="29.1"}

A _signal_ is _raised_ on a variety of external events. Your program can be configured to be interrupted to _handle_ the signal, and, optionally, continue where it left off once the signal has been handled.

> 一种信号可以在各种外部事件上被触发。您的程序可以被配置来接收这种信号，并且可以选择在处理完信号后继续之前的操作。

Think of it like a function that's automatically called when one of these external events occurs.

> 想象它就像一个当外部事件发生时自动调用的函数。

What are these events? On your system, there are probably a lot of them, but in the C spec there are just a few:

> 这些事件是什么？在您的系统中可能有很多，但在 C 规范中只有几个：

---

Signal Description

---

`SIGABRT` Abnormal termination---what happens when `abort()` is called.

`SIGFPE` Floating point exception.

`SIGILL` Illegal instruction.

`SIGINT` Interrupt---usually the result of `CTRL-C` being hit.

`SIGSEGV` "Segmentation Violation": invalid memory access.

## `SIGTERM` Termination requested.

You can set up your program to ignore, handle, or allow the default action for each of these by using the `signal()` function.

> 你可以使用 `signal()` 函数来设置程序，以忽略、处理或允许这些默认操作。

## [29.2] Handling Signals with `signal()` {#handling-signals-with-signal number="29.2"}

The `signal()` call takes two parameters: the signal in question, and an action to take when that signal is raised.

> `signal()` 调用需要两个参数：所涉及的信号，以及当该信号被触发时采取的行动。

The action can be one of three things:

- A pointer to a handler function.
- `SIG_IGN` to ignore the signal.
- `SIG_DFL` to restore the default handler for the signal.

Let's write a program that you can't `CTRL-C` out of. (Don't fret---in the following program, you can also hit `RETURN` and it'll exit.)

> 让我们编写一个你无法用 `CTRL-C` 退出的程序(别担心，在下面的程序中，你也可以按 `RETURN` 键退出)。

::: {#cb557 .sourceCode}

```c
#include <stdio.h>
#include <signal.h>

int main(void)
{
    char s[1024];

    signal(SIGINT, SIG_IGN);    // Ignore SIGINT, caused by ^C

    printf("Try hitting ^C... (hit RETURN to exit)\n");

    // Wait for a line of input so the program doesn't just exit
    fgets(s, sizeof s, stdin);
}
```

:::

Check out line 8---we tell the program to ignore `SIGINT`, the interrupt signal that's raised when `CTRL-C` is hit. No matter how much you hit it, the signal remains ignored. If you comment out line 8, you'll see you can `CTRL-C` with impunity and quit the program on the spot.

> 检查第 8 行——我们告诉程序忽略 `SIGINT`，当按下 `CTRL-C` 时会触发的中断信号。无论你按多少次，该信号都会被忽略。如果你注释掉第 8 行，你会发现你可以毫无顾忌地按 `CTRL-C` 并立即退出程序。

## [29.3] Writing Signal Handlers {#writing-signal-handlers number="29.3"}

I mentioned you could also write a handler function that gets called when the signal is raised.

> 我提到你也可以编写一个处理函数，当信号被触发时会调用它。

These are pretty straightforward, are also very capability-limited when it comes to the spec.

> 这些都很简单，但在规格方面能力有限。

Before we start, let's look at the function prototype for the `signal()` call:

> 在我们开始之前，让我们看一下 `signal()` 调用的函数原型：

::: {#cb558 .sourceCode}

```c
void (*signal(int sig, void (*func)(int)))(int);
```

:::

Pretty easy to read, right?

_WRONG!_ `:)`

Let's take a moment to take it apart for practice.

`signal()` takes two arguments: an integer `sig` representing the signal, and a pointer `func` to the handler (the handler returns `void` and takes an `int` as an argument), highlighted below:

::: {#cb559 .sourceCode}

```c
                sig          func
              |-----|  |---------------|
void (*signal(int sig, void (*func)(int)))(int);
```

:::

Basically, we're going to pass in the signal number we're interested in catching, and we're going to pass a pointer to a function of the form:

> 基本上，我们将传入我们感兴趣捕获的信号编号，并传入一个指向以下形式的函数的指针：

::: {#cb560 .sourceCode}

```c
void f(int x);
```

:::

that will do the actual catching.

Now---what about the rest of that prototype? It's basically all the return type. See, `signal()` will return whatever you passed as `func` on success... so that means it's returning a pointer to a function that returns `void` and takes an `int` as an argument.

> 现在---关于原型的剩余部分呢？基本上就是所有的返回类型。看，`signal()` 在成功时将会返回你传入的 `func`，所以这意味着它返回一个指向一个接受 `int` 作为参数并返回 `void` 的函数的指针。

::: {#cb561 .sourceCode}

```c
returned
function    indicates we're              and
returns     returning a                  that function
void        pointer to function          takes an int
|--|        |                                   |---|
void       (*signal(int sig, void (*func)(int)))(int);
```

:::

Also, it can return `SIG_ERR` in case of an error.

Let's do an example where we make it so you have to hit `CTRL-C` twice to exit.

> 让我们做一个例子，让你必须按两次 `CTRL-C` 才能退出。

I want to be clear that this program engages in undefined behavior in a couple ways. But it'll probably work for you, and it's hard to come up with portable non-trivial demos.

> 我想清楚地表明，这个程序以几种方式涉及未定义的行为。但它可能对你有用，而且很难想出可移植的非平凡演示。

::: {#cb562 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>

int count = 0;

void sigint_handler(int signum)
{
    // The compiler is allowed to run:
    //
    //   signal(signum, SIG_DFL)
    //
    // when the handler is called. So we reset the handler here:
    signal(SIGINT, sigint_handler);

    (void)signum;   // Get rid of unused variable warning

    count++;                       // Undefined behavior
    printf("Count: %d\n", count);  // Undefined behavior

    if (count == 2) {
        printf("Exiting!\n");      // Undefined behavior
        exit(0);
    }
}

int main(void)
{
    signal(SIGINT, sigint_handler);

    printf("Try hitting ^C...\n");

    for(;;);  // Wait here forever
}
```

:::

One of the things you'll notice is that on line 14 we reset the signal handler. This is because C has the option of resetting the signal handler to its `SIG_DFL` behavior before running your custom handler. In other words, it could be a one-off. So we reset it first thing so that we handle it again for the next one.

> 在第 14 行，你会注意到我们重置了信号处理程序。这是因为 C 有重置信号处理程序为其 `SIG_DFL` 行为的选项，在运行自定义处理程序之前。换句话说，它可能是一次性的。因此，我们首先重置它，以便我们为下一个再次处理它。

We're ignoring the return value from `signal()` in this case. If we'd set it to a different handler earlier, it would return a pointer to that handler, which we could get like this:

> 在这种情况下，我们忽略了 `signal()` 的返回值。如果我们之前设置了一个不同的处理程序，它将返回一个指向该处理程序的指针，我们可以这样获取它：

::: {#cb563 .sourceCode}

```c
// old_handler is type "pointer to function that takes a single
// int parameter and returns void":

void (*old_handler)(int);

old_handler = signal(SIGINT, sigint_handler);
```

:::

That said, I'm not sure of a common use case for this. But if you need the old handler for some reason, you can get it that way.

> 话虽如此，我不确定这有什么常见的用例。但如果您出于某种原因需要旧的处理程序，您可以通过这种方式获得它。

Quick note on line 16---that's just to tell the compiler to not warn that we're not using this variable. It's like saying, "I know I'm not using it; you don't have to warn me."

> 行 16 上的快速注释---这只是告诉编译器不要警告我们没有使用这个变量。这就像是说：“我知道我没有使用它；你不必警告我。”

And lastly you'll see that I've marked undefined behavior in a couple places. More on that in the next section.

> 最后，您会发现我在几个地方标记了未定义的行为。更多内容请参阅下一节。

## [29.4] What Can We Actually Do? {#what-can-we-actually-do number="29.4"}

Turns out we're pretty limited in what we can and can't do in our signal handlers. This is one of the reasons why I say you shouldn't even bother with this and instead use your OS's signal handling instead (e.g. `sigaction()` for Unix-like systems).

> 结果我们在信号处理程序中能做什么和不能做什么受到很大的限制。这就是为什么我说你不应该费心去做这件事，而是应该使用操作系统的信号处理(例如 Unix 系统中的 `sigaction()`)。

Wikipedia goes so far as to say the only really portable thing you can do is call `signal()` with `SIG_IGN` or `SIG_DFL` and that's it.

> 维基百科甚至说，唯一真正可移植的事情就是调用 `signal()` 函数，传入 `SIG_IGN` 或 `SIG_DFL` 参数，仅此而已。

Here's what we **can't** portably do:

- Call any standard library function.
  - Like `printf()`, for example.
  - I think it's probably safe to call restartable/reentrant functions, but the spec doesn't allow that liberty.

> 我认为调用可重启/可重入函数可能是安全的，但规范不允许这种自由。

- Get or set values from a local `static`, file scope, or thread-local variable.
  - Unless it's a lock-free atomic object or...
  - You're assigning into a variable of type `volatile sig_atomic_t`.

That last bit--`sig_atomic_t`--is your ticket to getting data out of a signal handler. (Unless you want to use lock-free atomic objects, which is outside the scope of this section[^171^].) It's an integer type that might or might not be signed. And it's bounded by what you can put in there.

> 那最后一点——`sig_atomic_t`——是你从信号处理程序中获取数据的入口。(除非你想使用无锁原子对象，这超出了本节的范围[^171^]。)它是一种可能有符号也可能无符号的整数类型。它的范围取决于你可以放进去的东西。

You can look at the minimum and maximum allowable values in the macros `SIG_ATOMIC_MIN` and `SIG_ATOMIC_MAX`[^172^].

> 你可以查看宏 `SIG_ATOMIC_MIN` 和 `SIG_ATOMIC_MAX` 中允许的最小值和最大值。

Confusingly, the spec also says you can't refer "to any object with static or thread storage duration that is not a lock-free atomic object other than by assigning a value to an object declared as `volatile sig_atomic_t` \[...\]"

> 更令人困惑的是，规范还说你不能通过除赋值给声明为 `volatile sig_atomic_t` 的对象以外的方式引用任何具有静态或线程存储持续时间的非无锁原子对象[...]

My read on this is that you can't read or write anything that's not a lock-free atomic object. Also you can assign to an object that's `volatile sig_atomic_t`.

> 我的解读是，你不能读写任何非锁定原子对象。此外，你可以将对象赋值给 `volatile sig_atomic_t`。

But can you read from it? I honestly don't see why not, except that the spec is very pointed about mentioning assigning into. But if you have to read it and make any kind of decision based on it, you might be opening up room for some kind of race conditions.

> 但你能从中读取吗？老实说，我不明白为什么不行，除了规格中特别提到了赋值。但是如果你必须读取它并基于它做出任何决定，你可能会开辟出一些竞争条件的空间。

With that in mind, we can rewrite our "hit `CTRL-C` twice to exit" code to be a little more portable, albeit less verbose on the output.

> 考虑到这一点，我们可以重写我们的“按两次 CTRL-C 退出”代码，使其更具可移植性，尽管输出更少。

Let's change our `SIGINT` handler to do nothing except increment a value that's of type `volatile sig_atomic_t`. So it'll count the number of `CTRL-C` s that have been hit.

> 让我们把我们的 SIGINT 处理程序改为除了增加一个类型为 volatile sig_atomic_t 的值以外什么也不做。这样它就可以计算出被按下的 CTRL-C 的次数。

Then in our main loop, we'll check to see if that counter is over `2`, then bail out if it is.

> 然后在我们的主循环中，我们会检查计数器是否超过 2，如果是的话就退出。

::: {#cb564 .sourceCode}

```c
#include <stdio.h>
#include <signal.h>

volatile sig_atomic_t count = 0;

void sigint_handler(int signum)
{
    (void)signum;                    // Unused variable warning

    signal(SIGINT, sigint_handler);  // Reset signal handler

    count++;                         // Undefined behavior
}

int main(void)
{
    signal(SIGINT, sigint_handler);

    printf("Hit ^C twice to exit.\n");

    while(count < 2);
}
```

:::

Undefined behavior again? It's my read that this is, because we have to read the value in order to increment and store it.

> 未定义的行为又来了？我的理解是，因为我们必须读取值才能增加并存储它。

If we only want to postpone the exit by one hitting of `CTRL-C`, we can do that without too much trouble. But any more postponement would require some ridiculous function chaining.

> 如果我们只是想通过按一下 CTRL-C 来推迟退出，我们可以轻松地做到。但是要再推迟，就需要一些荒谬的函数链接了。

What we'll do is handle it once, and the handler will reset the signal to its default behavior (that is, to exit):

> 我们将只处理一次，处理程序将信号重置为默认行为(即退出)：

::: {#cb565 .sourceCode}

```c
#include <stdio.h>
#include <signal.h>

void sigint_handler(int signum)
{
    (void)signum;                      // Unused variable warning
    signal(SIGINT, SIG_DFL);           // Reset signal handler
}

int main(void)
{
    signal(SIGINT, sigint_handler);

    printf("Hit ^C twice to exit.\n");

    while(1);
}
```

:::

Later when we look at lock-free atomic variables, we'll see a way to fix the `count` version (assuming lock-free atomic variables are available on your particular system).

> 稍后当我们看到无锁原子变量时，我们将看到一种修复 `count` 版本的方法(假设无锁原子变量可在您的特定系统上使用)。

This is why at the beginning, I was suggesting checking out your OS's built-in signal system as a probably-superior alternative.

> 这就是为什么一开始，我建议检查你的操作系统内置的信号系统作为一个可能更优的选择。

## [29.5] Friends Don't Let Friends `signal()` {#friends-dont-let-friends-signal number="29.5"}

Again, use your OS's built-in signal handling or the equivalent. It's not in the spec, not as portable, but probably is far more capable. Plus your OS probably has a number of signals defined that aren't in the C spec. And it's difficult to write portable code using `signal()` anyway.

> 再次使用您的操作系统内置的信号处理或等效的处理。这不在规范中，不太便于移植，但可能功能更强大。此外，您的操作系统可能定义了许多不在 C 规范中的信号。而且使用 `signal()` 编写可移植代码也很困难。

# [30] Variable-Length Arrays (VLAs) {#variable-length-arrays-vlas number="30"}

C provides a way for you to declare an array whose size is determined at runtime. This gives you the benefits of dynamic runtime sizing like you get with `malloc()`, but without needing to worry about `free()` ing the memory after.

> C 提供了一种方法，可以声明一个在运行时确定大小的数组。这样，您就可以获得像使用 malloc()一样的动态运行时调整大小的好处，而无需担心 free()内存。

Now, a lot of people don't like VLAs. They've been banned from the Linux kernel, for example. We'll dig into more of that rationale [later](#vla-general-issues).

> 现在，很多人不喜欢 VLAs。比如，它们已经被 Linux 内核禁止了。我们将在稍后更深入地研究[原因](#vla-general-issues)。

This is an optional feature of the language. The macro `__STDC_NO_VLA__` is set to `1` if VLAs are _not_ present. (They were mandatory in C99, and then became optional in C11.)

> 这是语言的一个可选特性。如果不存在可变长数组(VLAs)，宏 `__STDC_NO_VLA__` 将被设置为 `1`。(它们在 C99 中是必需的，然后在 C11 中变成可选的。)

::: {#cb566 .sourceCode}

```c
#if __STDC_NO_VLA__ == 1
   #error Sorry, need VLAs for this program!
#endif
```

:::

But since neither GCC nor Clang bother to define this macro, you may get limited mileage from this.

> 但是由于 GCC 和 Clang 都不会定义这个宏，你可能会受到一定的限制。

Let's dive in first with an example, and then we'll look for the devil in the details.

> 让我们先从一个例子开始，然后我们会仔细查找细节中的漏洞。

## [30.1] The Basics {#the-basics number="30.1"}

A normal array is declared with a constant size, like this:

::: {#cb567 .sourceCode}

```c
int v[10];
```

:::

But with VLAs, we can use a size determined at runtime to set the array, like this:

> 但是使用 VLAs，我们可以使用在运行时确定的大小来设置数组，就像这样：

::: {#cb568 .sourceCode}

```c
int n = 10;
int v[n];
```

:::

Now, that looks like the same thing, and in many ways is, but this gives you the flexibility to compute the size you need, and then get an array of exactly that size.

> 现在，看起来和以前的一样，而且在很多方面也是如此，但是这给了你灵活的计算所需大小的能力，然后得到一个精确大小的数组。

Let's ask the user to input the size of the array, and then store the index-times-10 in each of those array elements:

> 让我们请用户输入数组的大小，然后将每个数组元素的索引乘以 10 存储起来：

::: {#cb569 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int n;

    printf("Enter a number: "); fflush(stdout);
    scanf(" %d", &n);

    int v[n];

    for (int i = 0; i < n; i++)
        v[i] = i * 10;

    for (int i = 0; i < n; i++)
        printf("v[%d] = %d\n", i, v[i]);
}
```

:::

(On line 7, I have an `fflush()` that should force the line to output even though I don't have a newline at the end.)

> 在第 7 行，我有一个 `fflush()`，它应该强制输出即使我没有在末尾添加换行符。

Line 10 is where we declare the VLA---once execution gets past that line, the size of the array is set to whatever `n` was at that moment. The array length can't be changed later.

> 第 10 行是我们声明 VLA 的地方---一旦执行超过该行，数组的大小就被设置为当时的 `n`。之后数组的长度不能再改变。

You can put an expression in the brackets, as well:

::: {#cb570 .sourceCode}

```c
int v[x * 100];
```

:::

Some restrictions:

- You can't declare a VLA at file scope, and you can't make a `static` one in block scope[^173^].

> 不能在文件作用域中声明 VLA，也不能在块作用域中声明静态的 VLA。

- You can't use an initializer list to initialize the array.

Also, entering a negative value for the size of the array invokes undefined behavior---in this universe, anyway.

> 也就是说，在这个宇宙中，输入数组大小的负值会触发未定义的行为。

## [30.2] `sizeof` and VLAs {#sizeof-and-vlas number="30.2"}

We're used to `sizeof` giving us the size in bytes of any particular object, including arrays. And VLAs are no exception.

> 我们习惯于 `sizeof` 给我们任何特定对象(包括数组)的字节大小。可变长数组也不例外。

The main difference is that `sizeof` on a VLA is executed at _runtime_, whereas on a non-variably-sized variable it is computed at _compile time_.

> 主要区别是在 VLA 上的 `sizeof` 是在运行时执行的，而在非可变大小变量上是在编译时计算的。

But the usage is the same.

You can even compute the number of elements in a VLA with the usual array trick:

> 你甚至可以用通常的数组技巧来计算 VLA 中的元素数量：

::: {#cb571 .sourceCode}

```c
size_t num_elems = sizeof v / sizeof v[0];
```

:::

There's a subtle and correct implication from the above line: pointer arithmetic works just like you'd expect for a regular array. So go ahead and use it to your heart's content:

> 从上面的句子可以暗示出：指针算术像你期望的普通数组一样工作。所以尽情地使用它吧！

::: {#cb572 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int n = 5;
    int v[n];

    int *p = v;

    *(p+2) = 12;
    printf("%d\n", v[2]);  // 12

    p[3] = 34;
    printf("%d\n", v[3]);  // 34
}
```

:::

Like with regular arrays, you can use parentheses with `sizeof()` to get the size of a would-be VLA without actually declaring one:

> 就像使用普通数组一样，您可以使用 `sizeof()` 的括号来获取将要声明的 VLA 的大小，而无需实际声明它。

::: {#cb573 .sourceCode}

```c
int x = 12;

printf("%zu\n", sizeof(int [x]));  // Prints 48 on my system
```

:::

## [30.3] Multidimensional VLAs {#multidimensional-vlas number="30.3"}

You can go ahead and make all kinds of VLAs with one or more dimensions set to a variable

> 你可以继续制作各种 VLAs，其中一个或多个维度设置为可变的。

::: {#cb574 .sourceCode}

```c
int w = 10;
int h = 20;

int x[h][w];
int y[5][w];
int z[10][w][20];
```

:::

Again, you can navigate these just like you would a regular array.

## [30.4] Passing One-Dimensional VLAs to Functions {#passing-one-dimensional-vlas-to-functions number="30.4"}

Passing single-dimensional VLAs into a function can be no different than passing a regular array in. You just go for it.

> 传递单维可变长数组到函数中与传递普通数组没有什么不同。只需要去做就行了。

::: {#cb575 .sourceCode}

```c
#include <stdio.h>

int sum(int count, int *v)
{
    int total = 0;

    for (int i = 0; i < count; i++)
        total += v[i];

    return total;
}

int main(void)
{
    int x[5];   // Standard array

    int a = 5;
    int y[a];   // VLA

    for (int i = 0; i < a; i++)
        x[i] = y[i] = i + 1;

    printf("%d\n", sum(5, x));
    printf("%d\n", sum(a, y));
}
```

:::

But there's a bit more to it than that. You can also let C know that the array is a specific VLA size by passing that in first and then giving that dimension in the parameter list:

> 但是这还不止于此。您还可以通过首先传递该尺寸并在参数列表中给出该尺寸，让 C 知道该数组是特定的 VLA 大小：

::: {#cb576 .sourceCode}

```c
int sum(int count, int v[count])
{
    // ...
}
```

:::

Incidentally, there are a couple ways of listing a prototype for the above function; one of them involves an `*` if you don't want to specifically name the value in the VLA. It just indicates that the type is a VLA as opposed to a regular pointer.

> 顺便说一下，有几种方法可以列出上述函数的原型；其中一种涉及使用'*'，如果你不想特别指定 VLA 中的值。它只表明该类型是 VLA 而不是普通指针。

VLA prototypes:

::: {#cb577 .sourceCode}

```c
void do_something(int count, int v[count]);  // With names
void do_something(int, int v[*]);            // Without names
```

:::

Again, that `*` thing only works with the prototype---in the function itself, you'll have to put the explicit size.

> 再次，那个 `*` 只能在原型中使用---在函数本身中，你必须明确指定大小。

Now---_let's get multidimensional_! This is where the fun begins.

## [30.5] Passing Multi-Dimensional VLAs to Functions {#passing-multi-dimensional-vlas-to-functions number="30.5"}

Same thing as we did with the second form of one-dimensional VLAs, above, but this time we're passing in two dimensions and using those.

> 我们和上面一维 VLAs 的第二种形式做的同样的事情，但这次我们传入两个维度并使用它们。

In the following example, we build a multiplication table matrix of a variable width and height, and then pass it to a function to print it out.

> 在下面的例子中，我们构建了一个可变宽度和高度的乘法表矩阵，然后将其传递给一个函数来打印出来。

::: {#cb578 .sourceCode}

```c
#include <stdio.h>

void print_matrix(int h, int w, int m[h][w])
{
    for (int row = 0; row < h; row++) {
        for (int col = 0; col < w; col++)
            printf("%2d ", m[row][col]);
        printf("\n");
    }
}

int main(void)
{
    int rows = 4;
    int cols = 7;

    int matrix[rows][cols];

    for (int row = 0; row < rows; row++)
        for (int col = 0; col < cols; col++)
            matrix[row][col] = row * col;

    print_matrix(rows, cols, matrix);
}
```

:::

### [30.5.1] Partial Multidimensional VLAs {#partial-multidimensional-vlas number="30.5.1"}

You can have some of the dimensions fixed and some variable. Let's say we have a record length fixed at 5 elements, but we don't know how many records there are.

> 你可以固定一些维度，而另一些可变。比如说，记录长度固定为 5 个元素，但我们不知道有多少记录。

::: {#cb579 .sourceCode}

```c
#include <stdio.h>

void print_records(int count, int record[count][5])
{
    for (int i = 0; i < count; i++) {
        for (int j = 0; j < 5; j++)
            printf("%2d ", record[i][j]);
        printf("\n");
    }
}

int main(void)
{
    int rec_count = 3;
    int records[rec_count][5];

    // Fill with some dummy data
    for (int i = 0; i < rec_count; i++)
        for (int j = 0; j < 5; j++)
            records[i][j] = (i+1)*(j+2);

    print_records(rec_count, records);
}
```

:::

## [30.6] Compatibility with Regular Arrays {#compatibility-with-regular-arrays number="30.6"}

Because VLAs are just like regular arrays in memory, it's perfectly permissible to pass them interchangeably... as long as the dimensions match.

> 因为 VLAs 在内存中就像普通数组一样，所以可以完全允许将它们互换传递...只要维度匹配就可以了。

For example, if we have a function that specifically wants a [\\(3\\times5\\)]{.math .inline} array, we can still pass a VLA into it.

> 例如，如果我们有一个特定要求[\\(3\\times5\\)]{.math .inline}数组的函数，我们仍然可以将 VLA 传递给它。

::: {#cb580 .sourceCode}

```c
int foo(int m[5][3]) {...}

\\ ...

int w = 3, h = 5;
int matrix[h][w];

foo(matrix);   // OK!
```

:::

Likewise, if you have a VLA function, you can pass a regular array into it:

> 同样，如果你有一个 VLA 函数，你可以将一个普通数组传入它：

::: {#cb581 .sourceCode}

```c
int foo(int h, int w, int m[h][w]) {...}

\\ ...

int matrix[3][5];

foo(3, 5, matrix);   // OK!
```

:::

Beware, though: if your dimensions mismatch, you're going to have some undefined behavior going on, likely.

> 小心：如果您的尺寸不匹配，您可能会遇到一些未定义的行为。

## [30.7] `typedef` and VLAs {#typedef-and-vlas number="30.7"}

You can `typedef` a VLA, but the behavior might not be as you expect.

Basically, `typedef` makes a new type with the values as they existed the moment the `typedef` was executed.

> 基本上，`typedef` 在执行时会创建一个新类型，其值与执行 `typedef` 时的值相同。

So it's not a `typedef` of a VLA so much as a new fixed size array type of the dimensions at the time.

> 所以它不是一个 VLA 的 `typedef`，而更像是一种新的固定大小数组类型，其大小由当时的维度决定。

::: {#cb582 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int w = 10;

    typedef int goat[w];

    // goat is an array of 10 ints
    goat x;

    // Init with squares of numbers
    for (int i = 0; i < w; i++)
        x[i] = i*i;

    // Print them
    for (int i = 0; i < w; i++)
        printf("%d\n", x[i]);

    // Now let's change w...

    w = 20;

    // But goat is STILL an array of 10 ints, because that was the
    // value of w when the typedef executed.
}
```

:::

So it acts like an array of fixed size.

But you still can't use an initializer list on it.

## [30.8] Jumping Pitfalls {#jumping-pitfalls number="30.8"}

You have to watch out when using `goto` near VLAs because a lot of things aren't legal.

> 你在使用 VLAs 附近的 `goto` 时要小心，因为很多事情都是不合法的。

And when you're using `longjmp()` there's a case where you could leak memory with VLAs.

> 当你使用 `longjmp()` 时，有一种情况可能会导致使用 VLAs 泄漏内存。

But both of these things we'll cover in their respective chapters.

## [30.9] General Issues {#vla-general-issues number="30.9"}

VLAs have been banned from the Linux kernel for a few reasons:

- Lots of places they were used should have just been fixed-size.
- The code behind VLAs is slower (to a degree that most people wouldn't notice, but makes a difference in an operating system).

> 代码背后的 VLAs 速度较慢(大多数人不会注意到，但在操作系统中有所不同)。

- VLAs are not supported to the same degree by all C compilers.
- Stack size is limited, and VLAs go on the stack. If some code accidentally (or maliciously) passes a large value into a kernel function that allocates a VLA, *Bad Things*™ could happen.

> 栈的大小是有限的，而可变长数组(VLAs)则存放在栈中。如果某些代码不小心(或恶意)将大量值传递给一个分配可变长数组的内核函数，就可能发生*坏事* ™。

Other folks online point out that there's no way to detect a VLA's failure to allocate, and programs that suffered such problems would likely just crash. While fixed-size arrays also have the same issue, it's far more likely that someone accidentally make a _VLA Of Unusual Size_ than somehow accidentally declare a fixed-size, say, 30 megabyte array.

> 其他在线的人指出没有办法检测 VLA 分配失败的情况，遇到这种问题的程序可能会崩溃。虽然固定大小的数组也有同样的问题，但更有可能是有人不小心声明了一个不寻常大小的 VLA，而不是不小心声明了一个 30 兆字节的固定大小数组。

# [31] `goto` {#goto number="31"}

The `goto` statement is universally revered and can be here presented without contest.

> 跳转语句普遍受到尊重，可以在这里毫无争议地提出。

Just kidding! Over the years, there has been a lot of back-and-forth over whether or not (often not) `goto` is [considered harmful](https://en.wikipedia.org/wiki/Goto#Criticism)[^174^].

> 只是开玩笑！多年来，关于是否(通常不是)“转到”被认为是有害的(参见 [Wikipedia 上的批评](https://en.wikipedia.org/wiki/Goto#Criticism))一直存在着许多争论。

In this programmer's opinion, you should use whichever constructs leads to the _best_ code, factoring in maintainability and speed. And sometimes this might be `goto`!

> 在这位程序员看来，你应该使用那些最能够达到最佳代码效果，考虑到可维护性和速度的构造。有时候，这可能是 `goto`！

In this chapter, we'll see how `goto` works in C, and then check out some of the common cases where it is used[^175^].

> 在本章中，我们将看到 `goto` 在 C 中的工作原理，然后检查一些常见的使用情况[^175^]。

## [31.1] A Simple Example {#a-simple-example number="31.1"}

In this example, we're going to use `goto` to skip a line of code and jump to a _label_. The label is the identifier that can be a `goto` target---it ends with a colon (`:`).

> 在这个例子中，我们将使用 `goto` 跳过一行代码并跳转到一个_标签_。标签是可以作为 `goto` 目标的标识符---它以冒号(`:`)结尾。

::: {#cb583 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    printf("One\n");
    printf("Two\n");

    goto skip_3;

    printf("Three\n");

skip_3:

    printf("Five!\n");
}
```

:::

The output is:

::: {#cb584 .sourceCode}

```{.sourceCode .default}
One
Two
Five!
```

:::

`goto` sends execution jumping to the specified label, skipping everything in between.

You can jump forward or backward with `goto`.

::: {#cb585 .sourceCode}

```c
infinite_loop:
    print("Hello, world!\n");
    goto infinite_loop;
```

:::

Labels are skipped over during execution. The following will print all three numbers in order just as if the labels weren't there:

> 标签在执行时被跳过。以下将按顺序打印所有三个数字，就像没有标签一样。

::: {#cb586 .sourceCode}

```c
    printf("Zero\n");
label_1:
label_2:
    printf("One\n");
label_3:
    printf("Two\n");
label_4:
    printf("Three\n");
```

:::

As you've noticed, it's common convention to justify the labels all the way on the left. This increases readability because a reader can quickly scan to find the destination.

> 你已经注意到了，把标签全部放在最左边是一种常见的约定。这样做可以提高可读性，因为读者可以快速浏览以找到目的地。

Labels have _function scope_. That is, no matter how many levels deep in blocks they appear, you can still `goto` them from anywhere in the function.

> 标签具有_函数范围_。也就是说，无论它们出现在块中的多少层深度，您仍然可以从函数中的任何位置 `goto` 它们。

It also means you can only `goto` labels that are in the same function as the `goto` itself. Labels in other functions are out of scope from `goto`'s perspective. And it means you can use the same label name in two functions---just not the same label name in the same function.

> 这也意味着，您只能跳转到与跳转本身位于同一函数中的标签。 其他函数中的标签对跳转来说是超出范围的。 这意味着您可以在两个函数中使用相同的标签名称 - 只是不能在同一函数中使用相同的标签名称。

## [31.2] Labeled `continue` {#labeled-continue number="31.2"}

In some languages, you can actually specify a label for a `continue` statement. C doesn't allow it, but you can easily use `goto` instead.

> 在某些语言中，你可以为 `continue` 语句指定一个标签。C 语言不允许这样做，但你可以轻松地使用 `goto` 来代替。

To show the issue, check out `continue` in this nested loop:

::: {#cb587 .sourceCode}

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d, %d\n", i, j);
        continue;   // Always goes to next j
    }
}
```

:::

As we see, that `continue`, like all `continues`, goes to the next iteration of the nearest enclosing loop. What if we want to `continue` in the next loop out, the loop with `i`?

> 正如我们所看到的，“继续”，像所有的“继续”一样，会进入最近的包围循环的下一次迭代。如果我们想要在下一个循环，也就是具有“i”的循环中继续，怎么办？

Well, we can `break` to get back to the outer loop, right?

::: {#cb588 .sourceCode}

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d, %d\n", i, j);
        break;     // Gets us to the next iteration of i
    }
}
```

:::

That gets us two levels of nested loop. But then if we nest another loop, we're out of options. What about this, where we don't have any statement that will get us out to the next iteration of `i`?

> 那就给我们带来了两层嵌套循环。但是如果我们再嵌套一个循环，我们就没有选择了。那么这个呢，我们没有任何语句可以让我们跳出到下一次 `i` 迭代？

::: {#cb589 .sourceCode}

```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        for (int k = 0; k < 3; k++) {
            printf("%d, %d, %d\n", i, j, k);

            continue;  // Gets us to the next iteration of k
            break;     // Gets us to the next iteration of j
            ????;      // Gets us to the next iteration of i???

        }
    }
}
```

:::

The `goto` statement offers us a way!

::: {#cb590 .sourceCode}

```c
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            for (int k = 0; k < 3; k++) {
                printf("%d, %d, %d\n", i, j, k);

                goto continue_i;   // Now continuing the i loop!!
            }
        }
continue_i: ;
    }
```

:::

We have a `;` at the end there---that's because you can't have a label pointing to the plain end of a compound statement (or before a variable declaration).

> 我们在最后面有一个 `;`，这是因为你不能把一个标签指向复合语句的结尾(或者变量声明之前)。

## [31.3] Bailing Out {#bailing-out number="31.3"}

When you're super nested in the middle of some code, you can use `goto` to get out of it in a manner that's often cleaner than nesting more `if` s and using flag variables.

> 当你被深嵌在代码中间时，你可以使用 `goto` 以比嵌入更多的 `if` 和使用标志变量更加干净的方式来脱离它。

::: {#cb591 .sourceCode}

```c
    // Pseudocode

    for(...) {
        for (...) {
            while (...) {
                do {
                    if (some_error_condition)
                        goto bail;

                } while(...);
            }
        }
    }

bail:
    // Cleanup here
```

:::

Without `goto`, you'd have to check an error condition flag in all of the loops to get all the way out.

> 没有 `goto`，你必须在所有循环中检查错误条件标志才能完全退出。

## [31.4] Labeled `break` {#labeled-break number="31.4"}

This is a very similar situation to how `continue` only continues the innermost loop. `break` also only breaks out of the innermost loop.

> 这种情况非常类似，只有 `continue` 只会继续内层循环，而 `break` 也只会中断内层循环。

::: {#cb592 .sourceCode}

```c
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d, %d\n", i, j);
            break;   // Only breaks out of the j loop
        }
    }

    printf("Done!\n");
```

:::

But we can use `goto` to break farther:

::: {#cb593 .sourceCode}

```c
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d, %d\n", i, j);
            goto break_i;   // Now breaking out of the i loop!
        }
    }

break_i:

    printf("Done!\n");
```

:::

## [31.5] Multi-level Cleanup {#multi-level-cleanup number="31.5"}

If you're calling multiple functions to initialize multiple systems and one of them fails, you should only de-initialize the ones that you've gotten to so far.

> 如果您调用多个函数来初始化多个系统，其中一个失败了，您应该只反初始化到目前为止的那些。

Let's do a fake example where we start initializing systems and checking to see if any returns an error (we'll use `-1` to indicate an error). If one of them does, we have to shutdown only the systems we've initialized so far.

> 让我们做一个假的例子，我们开始初始化系统并检查是否有任何返回错误(我们将使用 `-1` 来表示错误)。如果其中一个出错了，我们只能关闭我们到目前为止已经初始化的系统。

::: {#cb594 .sourceCode}

```c
    if (init_system_1() == -1)
        goto shutdown;

    if (init_system_2() == -1)
        goto shutdown_1;

    if (init_system_3() == -1)
        goto shutdown_2;

    if (init_system_4() == -1)
        goto shutdown_3;

    do_main_thing();   // Run our program

    shutdown_system4();

shutdown_3:
    shutdown_system3();

shutdown_2:
    shutdown_system2();

shutdown_1:
    shutdown_system1();

shutdown:
    print("All subsystems shut down.\n");
```

:::

Note that we're shutting down in the reverse order that we initialized the subsystems. So if subsystem 4 fails to start up, it will shut down 3, 2, then 1 in that order.

> 注意，我们正在按照我们初始化子系统的相反顺序关闭。因此，如果子系统 4 无法启动，它将按照 3、2、1 的顺序关闭。

## [31.6] Tail Call Optimization {#tail-call-optimization number="31.6"}

Kinda. For recursive functions only.

If you're unfamiliar, [Tail Call Optimization (TCO)](https://en.wikipedia.org/wiki/Tail_call)[^176^] is a way to not waste stack space when calling other functions under very specific circumstances. Unfortunately the details are beyond the scope of this guide.

> 如果你不熟悉，尾调用优化(TCO)是一种在特定情况下调用其他函数时不浪费堆栈空间的方法。不幸的是，细节超出了本指南的范围。

But if you have a recursive function you know can be optimized in this way, you can make use of this technique. (Note that you can't tail call other functions due to the function scope of labels.)

> 如果你有一个可以以这种方式优化的递归函数，你可以利用这种技术。(注意，由于标签的函数作用域，你不能尾调用其他函数。)

Let's do a straightforward example, factorial.

Here's a recursive version that's not TCO, but it can be!

::: {#cb595 .sourceCode}

```c
#include <stdio.h>
#include <complex.h>

int factorial(int n, int a)
{
    if (n == 0)
        return a;

    return factorial(n - 1, a * n);
}

int main(void)
{
    for (int i = 0; i < 8; i++)
        printf("%d! == %ld\n", i, factorial(i, 1));
}
```

:::

To make it happen, you can replace the call with two steps:

1. Set the values of the parameters to what they'd be on the next call.
2. `goto` a label on the first line of the function.

Let's try it:

::: {#cb596 .sourceCode}

```c
#include <stdio.h>

int factorial(int n, int a)
{
tco:  // add this

    if (n == 0)
        return a;

    // replace return by setting new parameter values and
    // goto-ing the beginning of the function

    //return factorial(n - 1, a * n);

    int next_n = n - 1;  // See how these match up with
    int next_a = a * n;  // the recursive arguments, above?

    n = next_n;   // Set the parameters to the new values
    a = next_a;

    goto tco;   // And repeat!
}

int main(void)
{
    for (int i = 0; i < 8; i++)
        printf("%d! == %d\n", i, factorial(i, 1));
}
```

:::

I used temporary variables up there to set the next values of the parameters before jumping to the start of the function. See how they correspond to the recursive arguments that were in the recursive call?

> 我在上面使用了临时变量来设置参数的下一个值，然后跳转到函数的开头。看看它们如何对应于递归调用中的递归参数？

Now, why use temp variables? I could have done this instead:

::: {#cb597 .sourceCode}

```c
    a *= n;
    n -= 1;

    goto tco;
```

:::

and that actually works just fine. But if I carelessly reverse those two lines of code:

> 这样做也很正常。但如果我粗心地反转了这两行代码：

::: {#cb598 .sourceCode}

```c
    n -= 1;  // BAD NEWS
    a *= n;
```

:::

---now we're in trouble. We modified `n` before using it to modify `a`. That's Bad because that's not how it works when you call recursively. Using the temporary variables avoids this problem even if you're not looking out for it. And the compiler likely optimizes them out, anyway.

## [31.7] Restarting Interrupted System Calls {#restarting-interrupted-system-calls number="31.7"}

This is outside the spec, but commonly seen in Unix-like systems.

Certain long-lived system calls might return an error if they're interrupted by a signal, and `errno` will be set to `EINTR` to indicate the syscall was doing fine; it was just interrupted.

> 某些长期存在的系统调用如果被信号中断，可能会返回一个错误，并且 `errno` 将被设置为 `EINTR` 以表明系统调用运行良好，只是被中断了。

In those cases, it's really common for the programmer to want to restart the call and try it again.

> 在这些情况下，程序员通常希望重新开始通话并再次尝试。

::: {#cb599 .sourceCode}

```c
retry:
    byte_count = read(0, buf, sizeof(buf) - 1);  // Unix read() syscall

    if (byte_count == -1) {            // An error occurred...
        if (errno == EINTR) {          // But it was just interrupted
            printf("Restarting...\n");
            goto retry;
        }
```

:::

Many Unix-likes have an `SA_RESTART` flag you can pass to `sigaction()` to request the OS automatically restart any slow syscalls instead of failing with `EINTR`.

> 许多类 Unix 操作系统都有一个 `SA_RESTART` 标志，可以传递给 `sigaction()`，以请求操作系统自动重新启动任何缓慢的系统调用，而不是以 `EINTR` 失败。

Again, this is Unix-specific and is outside the C standard.

That said, it's possible to use a similar technique any time any function should be restarted.

> 话虽如此，只要有需要重新启动任何函数的时候，就可以使用类似的技术。

## [31.8] `goto` and Thread Preemption {#goto-and-thread-preemption number="31.8"}

This example is ripped directly from [_Operating Systems: Three Easy Pieces_](http://www.ostep.org/), another excellent book from like-minded authors who also feel that quality books should be free to download. Not that I'm opinionated, or anything.

> 这个例子是直接从[_操作系统：三个简单的部分_](http://www.ostep.org/)抄袭的，这是另一本优秀的书，作者也认为优质的书应该免费下载。不是说我有什么意见，或者什么。

::: {#cb600 .sourceCode}

```c
retry:

    pthread_mutex_lock(L1);

    if (pthread_mutex_trylock(L2) != 0) {
        pthread_mutex_unlock(L1);
        goto retry;
    }

    save_the_day();

    pthread_mutex_unlock(L2);
    pthread_mutex_unlock(L1);
```

:::

There the thread happily acquires the mutex `L1`, but then potentially fails to get the second resource guarded by mutex `L2` (if some other uncooperative thread holds it, say). If our thread can't get the `L2` lock, it unlocks `L1` and then uses `goto` to cleanly retry.

> 在那里，线程开心地获得了互斥锁 `L1`，但是如果另一个不合作的线程持有它，则可能无法获得由互斥锁 `L2` 保护的第二个资源。如果我们的线程无法获得 `L2` 锁，它将解锁 `L1`，然后使用 `goto` 以干净的方式重试。

We hope our heroic thread eventually manages to acquire both mutexes and save the day, all while avoiding evil deadlock.

> 我们希望我们的英勇线程最终能够获得双重互斥锁，拯救这一天，同时避免邪恶的死锁。

## [31.9] `goto` and Variable Scope {#goto-and-variable-scope number="31.9"}

We've already seen that labels have function scope, but weird things can happen if we jump past some variable initialization.

> 我们已经看到标签具有函数范围，但是如果我们跳过一些变量初始化，可能会发生奇怪的事情。

Look at this example where we jump from a place where the variable `x` is out of scope into the middle of its scope (in the block).

> 看看这个例子，我们从变量 `x` 超出作用域的地方跳到它的作用域中间(在块中)。

::: {#cb601 .sourceCode}

```c
    goto label;

    {
        int x = 12345;

label:
        printf("%d\n", x);
    }
```

:::

This will compile and run, but gives me a warning:

::: {#cb602 .sourceCode}

```{.sourceCode .default}
warning: ‘x’ is used uninitialized in this function
```

:::

And then it prints out `0` when I run it (your mileage may vary).

Basically what has happened is that we jumped into `x`'s scope (so it was OK to reference it in the `printf()`) but we jumped over the line that actually initialized it to `12345`. So the value was indeterminate.

> 基本上发生的是我们跳入 `x` 的范围(因此在 `printf()` 中引用它是可以的)，但我们跳过了将其初始化为 `12345` 的行。因此，该值是不确定的。

The fix is, of course, to get the initialization _after_ the label one way or another.

> 解决方法当然是要以某种方式将初始化操作放在标签之后。

::: {#cb603 .sourceCode}

```c
    goto label;

    {
        int x;

label:
        x = 12345;
        printf("%d\n", x);
    }
```

:::

Let's look at one more example.

::: {#cb604 .sourceCode}

```c
    {
        int x = 10;

label:

        printf("%d\n", x);
    }

    goto label;
```

:::

What happens here?

The first time through the block, we're good. `x` is `10` and that's what prints.

> 第一次穿过块，我们很好。`x` 的值是 `10`，这就是打印出来的结果。

But after the `goto`, we're jumping into the scope of `x`, but past its initialization. Which means we can still print it, but the value is indeterminate (since it hasn't been reinitialized).

> 但是在跳转之后，我们进入了 `x` 的作用域，但是超出了它的初始化范围。这意味着我们仍然可以打印它，但是值是不确定的(因为它还没有被重新初始化)。

On my machine, it prints `10` again (to infinity), but that's just luck. It could print any value after the `goto` since `x` is uninitialized.

> 在我的机器上，它又会打印出“10”(无限次)，但这只是运气。自从“x”未初始化之后，它可能会打印出任何值。

## [31.10] `goto` and Variable-Length Arrays {#goto-and-variable-length-arrays number="31.10"}

When it comes to VLAs and `goto`, there's one rule: you can't jump from outside the scope of a VLA into the scope of that VLA.

> 当涉及 VLAs 和 `goto` 时，有一条规则：你不能从 VLAs 的外部范围跳转到 VLAs 的范围内。

If I try to do this:

::: {#cb605 .sourceCode}

```c
    int x = 10;

    goto label;

    {
        int v[x];

label:

        printf("Hi!\n");
    }
```

:::

I get an error:

::: {#cb606 .sourceCode}

```{.sourceCode .default}
error: jump into scope of identifier with variably modified type
```

:::

You can jump in ahead of the VLA declaration, like this:

::: {#cb607 .sourceCode}

```c
    int x = 10;

    goto label;

    {
label:  ;
        int v[x];

        printf("Hi!\n");
    }
```

:::

Because that way the VLA gets allocated properly before its inevitable deallocation once it falls out of scope.

> 因为那样，VLA 在它一旦超出作用域而被释放之前，可以得到正确的分配。

# [32] Types Part V: Compound Literals and Generic Selections {#types-part-v-compound-literals-and-generic-selections number="32"}

This is the final chapter for types! We're going to talk about two things:

> 这是有关类型的最后一章！我们将讨论两件事：

- How to have "anonymous" unnamed objects and how that's useful.
- How to generate type-dependent code.

They're not particularly related, but don't really each warrant their own chapters. So I crammed them in here like a rebel!

> 他们没有特别相关，但也不需要各自占据一章。所以我像个叛逆者一样把它们塞进了这里！

## [32.1] Compound Literals {#compound-literals number="32.1"}

This is a neat feature of the language that allows you to create an object of some type on the fly without ever assigning it to a variable. You can make simple types, arrays, `struct` s, you name it.

> 这是语言的一个酷炫特性，可以让你在不把它赋值给变量的情况下，动态地创建某种类型的对象。你可以创建简单类型、数组、`struct`，你说了算。

One of the main uses for this is passing complex arguments to functions when you don't want to make a temporary variable to hold the value.

> 这其中的一个主要用途是，当你不想创建一个临时变量来保存值时，可以用它来传递复杂的参数给函数。

The way you create a compound literal is to put the type name in parentheses, and then put an initializer list after. For example, an unnamed array of `int` s, might look like this:

> 你创建一个复合文字的方式是在括号中放入类型名称，然后在后面放入初始化列表。例如，一个未命名的 `int` 数组可能看起来像这样：

::: {#cb608 .sourceCode}

```c
(int []){1,2,3,4}
```

:::

Now, that line of code doesn't do anything on its own. It creates an unnamed array of 4 `int` s, and then throws them away without using them.

> 现在，这行代码本身没有任何作用。它创建了一个由 4 个 `int` 组成的未命名数组，然后把它们扔掉而不使用它们。

We could use a pointer to store a reference to the array...

::: {#cb609 .sourceCode}

```c
int *p = (int []){1 ,2 ,3 ,4};

printf("%d\n", p[1]);  // 2
```

:::

But that seems a little like a long-winded way to have an array. I mean, we could have just done this[^177^]:

> 但这似乎是一种繁琐的方式来拥有一个数组。我的意思是，我们本可以这样做 [^177^]：

::: {#cb610 .sourceCode}

```c
int p[] = {1, 2, 3, 4};

printf("%d\n", p[1]);  // 2
```

:::

So let's take a look at a more useful example.

### [32.1.1] Passing Unnamed Objects to Functions {#passing-unnamed-objects-to-functions number="32.1.1"}

Let's say we have a function to sum an array of `int` s:

::: {#cb611 .sourceCode}

```c
int sum(int p[], int count)
{
    int total = 0;

    for (int i = 0; i < count; i++)
        total += p[i];

    return total;
}
```

:::

If we wanted to call it, we'd normally have to do something like this, declaring an array and storing values in it to pass to the function:

> 如果我们想调用它，通常我们需要做类似这样的事情，声明一个数组并将值存储在其中以传递给函数：

::: {#cb612 .sourceCode}

```c
int a[] = {1, 2, 3, 4};

int s = sum(a, 4);
```

:::

But unnamed objects give us a way to skip the variable by passing it directly in (parameter names listed above). Check it out---we're going to replace the variable `a` with an unnamed array that we pass in as the first argument:

> 但是未命名的对象给我们一种方式来跳过变量，直接传入(上面列出的参数名称)。看一下---我们将用一个未命名的数组替换变量 `a`，作为第一个参数传入：

::: {#cb613 .sourceCode}

```c
//                   p[]         count
//           |-----------------|  |
int s = sum((int []){1, 2, 3, 4}, 4);
```

:::

Pretty slick!

### [32.1.2] Unnamed `struct` s {#unnamed-structs number="32.1.2"}

We can do something similar with `struct` s.

First, let's do things without unnamed objects. We'll define a `struct` to hold some `x`/`y` coordinates. Then we'll define one, passing in values into its initializer. Finally, we'll pass it to a function to print the values:

> 首先，让我们先不使用未命名的对象来做事情。我们将定义一个 `struct` 来保存一些 `x`/`y` 坐标。然后，我们将定义一个，将值传递给它的初始化程序。最后，我们将它传递给一个函数以打印这些值：

::: {#cb614 .sourceCode}

```c
#include <stdio.h>

struct coord {
    int x, y;
};

void print_coord(struct coord c)
{
    printf("%d, %d\n", c.x, c.y);
}

int main(void)
{
    struct coord t = {.x=10, .y=20};

    print_coord(t);   // prints "10, 20"
}
```

:::

Straightforward enough?

Let's modify it to use an unnamed object instead of the variable `t` we're passing to `print_coord()`.

> 让我们改用一个未命名的对象来取代我们传递给 `print_coord()` 的变量 `t`。

We'll just take `t` out of there and replace it with an unnamed `struct`:

::: {#cb615 .sourceCode startfrom="7"}

```c
    //struct coord t = {.x=10, .y=20};

    print_coord((struct coord){.x=10, .y=20});   // prints "10, 20"
```

:::

Still works!

### [32.1.3] Pointers to Unnamed Objects {#pointers-to-unnamed-objects number="32.1.3"}

You might have noticed in the last example that even through we were using a `struct`, we were passing a copy of the `struct` to `print_coord()` as opposed to passing a pointer to the `struct`.

> 在上一个例子中，你可能已经注意到，即使我们使用了 `struct`，我们也将 `struct` 的一个副本传递给 `print_coord()`，而不是传递一个指向 `struct` 的指针。

Turns out, we can just take the address of an unnamed object with `&` like always.

> 原来，我们可以像往常一样用'&'取得一个未命名对象的地址。

This is because, in general, if an operator would have worked on a variable of that type, you can use that operator on an unnamed object of that type.

> 因为一般来说，如果一个操作符可以用于某种类型的变量，你可以在该类型的未命名对象上使用该操作符。

Let's modify the above code so that we pass a pointer to an unnamed object

> 让我们修改上面的代码，以便我们传递一个指向未命名对象的指针。

::: {#cb616 .sourceCode}

```c
#include <stdio.h>

struct coord {
    int x, y;
};

void print_coord(struct coord *c)
{
    printf("%d, %d\n", c->x, c->y);
}

int main(void)
{
    //     Note the &
    //          |
    print_coord(&(struct coord){.x=10, .y=20});   // prints "10, 20"
}
```

:::

Additionally, this can be a nice way to pass even pointers to simple objects:

> 此外，这也可以是一种传递指针给简单对象的好方法：

::: {#cb617 .sourceCode}

```c
// Pass a pointer to an int with value 3490
foo(&(int){3490});
```

:::

Easy as that.

### [32.1.4] Unnamed Objects and Scope {#unnamed-objects-and-scope number="32.1.4"}

The lifetime of an unnamed object ends at the end of its scope. The biggest way this could bite you is if you make a new unnamed object, get a pointer to it, and then leave the object's scope. In that case, the pointer will refer to a dead object.

> 未命名对象的生命周期在其作用域结束时结束。这最可能会让你遭殃的是，如果你创建一个新的未命名对象，获得一个指向它的指针，然后离开对象的作用域。在这种情况下，指针将指向一个死对象。

So this is undefined behavior:

::: {#cb618 .sourceCode}

```c
int *p;

{
    p = &(int){10};
}

printf("%d\n", *p);  // INVALID: The (int){10} fell out of scope
```

:::

Likewise, you can't return a pointer to an unnamed object from a function. The object is deallocated when it falls out of scope:

> 同样，你不能从函数中返回一个指向未命名对象的指针。当对象超出作用域时，它将被释放。

::: {#cb619 .sourceCode}

```c
#include <stdio.h>

int *get3490(void)
{
    // Don't do this
    return &(int){3490};
}

int main(void)
{
    printf("%d\n", *get3490());  // INVALID: (int){3490} fell out of scope
}
```

:::

Just think of their scope like that of an ordinary local variable. You can't return a pointer to a local variable, either.

> 想象它们的范围就像普通的局部变量一样。你也不能返回一个指向局部变量的指针。

### [32.1.5] Silly Unnamed Object Example {#silly-unnamed-object-example number="32.1.5"}

You can put any type in there and make an unnamed object.

For example, these are effectively equivalent:

::: {#cb620 .sourceCode}

```c
int x = 3490;

printf("%d\n", x);               // 3490 (variable)
printf("%d\n", 3490);            // 3490 (constant)
printf("%d\n", (int){3490});     // 3490 (unnamed object)
```

:::

That last one is unnamed, but it's silly. Might as well do the simple one on the line before.

> 那最后一个没有名字，但是很傻。不如做前一行的简单的那个。

But hopefully that provides a little more clarity on the syntax.

## [32.2] Generic Selections {#type-generics number="32.2"}

This is an expression that allows you to select different pieces of code depending on the _type_ of the first argument to the expression.

> 这是一个表达式，它允许您根据表达式的第一个参数的_类型_来选择不同的代码片段。

We'll look at an example in just a second, but it's important to know this is processed at compile time, _not at runtime_. There's no runtime analysis going on here.

> 我们马上就会看一个例子，但重要的是要知道这是在编译时处理的，而不是在运行时。这里没有运行时分析。

The expression begins with `_Generic`, works kinda like a `switch`, and it takes at least two arguments.

> 表达式以 `_Generic` 开头，类似于 `switch`，至少需要两个参数。

The first argument is an expression (or variable[^178^]) that has a _type_. All expressions have a type. The remaining arguments to `_Generic` are the cases of what to substitute in for the result of the expression if the first argument is that type.

> 第一个参数是一个表达式(或变量)，它具有一个_类型_。所有表达式都有一个类型。`_Generic` 的其余参数是如果第一个参数是该类型，则用于替换表达式结果的情况。

Wat?

Let's try it out and see.

::: {#cb621 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int i;
    float f;
    char c;

    char *s = _Generic(i,
                    int: "that variable is an int",
                    float: "that variable is a float",
                    default: "that variable is some type"
                );

    printf("%s\n", s);
}
```

:::

Check out the `_Generic` expression starting on line 9.

When the compiler sees it, it looks at the type of the first argument. (In this example, the type of the variable `i`.) It then looks through the cases for something of that type. And then it substitutes the argument in place of the entire `_Generic` expression.

> 当编译器看到它时，它会查看第一个参数的类型(在本例中，变量 `i` 的类型)。然后，它会查找该类型的情况。然后，它会将参数替换为整个 `_Generic` 表达式。

In this case, `i` is an `int`, so it matches that case. Then the string is substituted in for the expression. So the line turns into this when the compiler sees it:

> 在这种情况下，“i”是一个“int”，因此它符合该情况。然后将字符串替换为表达式。因此，当编译器看到它时，该行变成了这样：

::: {#cb622 .sourceCode}

```c
    char *s = "that variable is an int";
```

:::

If the compiler can't find a type match in the `_Generic`, it looks for the optional `default` case and uses that.

> 如果编译器在 `_Generic` 中找不到类型匹配，它会查找可选的 `default` 情况并使用它。

If it can't find a type match and there's no `default`, you'll get a compile error. The first expression **must** match one of the types or `default`.

> 如果找不到类型匹配，而且没有 `default`，你会得到一个编译错误。第一个表达式**必须**与其中一种类型或 `default` 匹配。

Because it's inconvenient to write `_Generic` over and over, it's often used to make the body of a macro that can be easily repeatedly reused.

> 因为一遍又一遍地写 `_Generic` 不方便，所以它经常被用来创建一个宏，可以轻松重复使用。

Let's make a macro `TYPESTR(x)` that takes an argument and returns a string with the type of the argument.

> 让我们创建一个宏 `TYPESTR(x)`，它接受一个参数，并返回一个字符串，其中包含参数的类型。

So `TYPESTR(1)` will return the string `"int"`, for example.

Here we go:

::: {#cb623 .sourceCode}

```c
#include <stdio.h>

#define TYPESTR(x) _Generic((x), \
                        int: "int", \
                        long: "long", \
                        float: "float", \
                        double: "double", \
                        default: "something else")

int main(void)
{
    int i;
    long l;
    float f;
    double d;
    char c;

    printf("i is type %s\n", TYPESTR(i));
    printf("l is type %s\n", TYPESTR(l));
    printf("f is type %s\n", TYPESTR(f));
    printf("d is type %s\n", TYPESTR(d));
    printf("c is type %s\n", TYPESTR(c));
}
```

:::

This outputs:

::: {#cb624 .sourceCode}

```{.sourceCode .default}
i is type int
l is type long
f is type float
d is type double
c is type something else
```

:::

Which should be no surprise, because, like we said, that code in `main()` is replaced with the following when it is compiled:

> 这不足为奇，因为，正如我们所说，当编译时，`main()` 中的代码将被以下内容替换：

::: {#cb625 .sourceCode}

```c
    printf("i is type %s\n", "int");
    printf("l is type %s\n", "long");
    printf("f is type %s\n", "float");
    printf("d is type %s\n", "double");
    printf("c is type %s\n", "something else");
```

:::

And that's exactly the output we see.

Let's do one more. I've included some macros here so that when you run:

::: {#cb626 .sourceCode}

```c
int i = 10;
char *s = "Foo!";

PRINT_VAL(i);
PRINT_VAL(s);
```

:::

you get the output:

::: {#cb627 .sourceCode}

```{.sourceCode .default}
i = 10
s = Foo!
```

:::

We'll have to make use of some macro magic to do that.

::: {#cb628 .sourceCode}

```c
#include <stdio.h>
#include <string.h>

// Macro that gives back a format specifier for a type
#define FMTSPEC(x) _Generic((x), \
                        int: "%d", \
                        long: "%ld", \
                        float: "%f", \
                        double: "%f", \
                        char *: "%s")
                        // TODO: add more types

// Macro that prints a variable in the form "name = value"
#define PRINT_VAL(x) do { \
    char fmt[512]; \
    snprintf(fmt, sizeof fmt, #x " = %s\n", FMTSPEC(x)); \
    printf(fmt, (x)); \
} while(0)

int main(void)
{
    int i = 10;
    float f = 3.14159;
    char *s = "Hello, world!";

    PRINT_VAL(i);
    PRINT_VAL(f);
    PRINT_VAL(s);
}
```

:::

for the output:

::: {#cb629 .sourceCode}

```{.sourceCode .default}
i = 10
f = 3.141590
s = Hello, world!
```

:::

We could have crammed that all in one big macro, but I broke it into two to prevent eye bleeding.

> 我们本可以把所有这些都放在一个大宏里，但为了避免让人眼花缭乱，我把它分成了两个。

# [33] Arrays Part II {#arrays-part-ii number="33"}

We're going to go over a few extra misc things this chapter concerning arrays.

> 我们将在本章节中讨论一些关于数组的额外杂项。

- Type qualifiers with array parameters
- The `static` keyword with array parameters
- Partial multi-dimensional array initializers

They're not super-commonly seen, but we'll peek at them since they're part of the newer spec.

> 它们不是特别常见的，但既然它们是最新规范的一部分，我们会瞄一眼。

## [33.1] Type Qualifiers for Arrays in Parameter Lists {#type-qualifiers-for-arrays-in-parameter-lists number="33.1"}

If you recall from earlier, these two things are equivalent in function parameter lists:

> 如果你回想起之前，这两件事在功能参数列表中是等价的：

::: {#cb630 .sourceCode}

```c
int func(int *p) {...}
int func(int p[]) {...}
```

:::

And you might also recall that you can add type qualifiers to a pointer variable like so:

> 你也可以记得，你可以像这样给指针变量添加类型限定符：

::: {#cb631 .sourceCode}

```c
int *const p;
int *volatile p;
int *const volatile p;
// etc.
```

:::

But how can we do that when we're using array notation in your parameter list?

> 但是当我们在参数列表中使用数组符号时，我们该怎么做？

Turns out it goes in the brackets. And you can put the optional count after. The two following lines are equivalent:

> 结果它是放在括号里的。你可以在后面添加可选的计数。下面两行是等价的：

::: {#cb632 .sourceCode}

```c
int func(int *const volatile p) {...}
int func(int p[const volatile]) {...}
int func(int p[const volatile 10]) {...}
```

:::

If you have a multidimensional array, you need to put the type qualifiers in the first set of brackets.

> 如果你有一个多维数组，你需要在第一组括号中放置类型限定符。

## [33.2] `static` for Arrays in Parameter Lists {#static-for-arrays-in-parameter-lists number="33.2"}

Similarly, you can use the keyword static in the array in a parameter list.

> 你也可以在参数列表中使用关键字 static 来定义数组。

This is something I've never seen in the wild. It is **always** followed by a dimension:

> 这是我从未在野外见过的东西。它**总是**被一个尺寸所跟随。

::: {#cb633 .sourceCode}

```c
int func(int p[static 4]) {...}
```

:::

What this means, in the above example, is the compiler is going to assume that any array you pass to the function will be _at least_ 4 elements.

> 在上面的例子中，这意味着编译器将假设您传递给函数的任何数组都将至少有 4 个元素。

Anything else is undefined behavior.

::: {#cb634 .sourceCode}

```c
int func(int p[static 4]) {...}

int main(void)
{
    int a[] = {11, 22, 33, 44};
    int b[] = {11, 22, 33, 44, 55};
    int c[] = {11, 22};

    func(a);  // OK! a is 4 elements, the minimum
    func(b);  // OK! b is at least 4 elements
    func(c);  // Undefined behavior! c is under 4 elements!
}
```

:::

This basically sets the minimum size array you can have.

Important note: there is nothing in the compiler that prohibits you from passing in a smaller array. The compiler probably won't warn you, and it won't detect it at runtime.

> 重要提示：编译器中没有任何东西阻止你传入一个较小的数组。编译器可能不会警告你，也不会在运行时检测到它。

By putting `static` in there, you're saying, "I double secret PROMISE that I will never pass in a smaller array than this." And the compiler says, "Yeah, fine," and trusts you to not do it.

> 加入 `静态`，你是在说：“我双重秘密承诺，我不会传递比这更小的数组。”编译器会说：“好的，我相信你不会这么做。”

And then the compiler can make certain code optimizations, safe in the knowledge that you, the programmer, will always do the right thing.

> 然后编译器可以进行一些代码优化，放心地知道你作为程序员总是会做出正确的事情。

## [33.3] Equivalent Initializers {#equivalent-initializers number="33.3"}

C is a little bit, shall we say, _flexible_ when it comes to array initializers.

> C 在数组初始化方面有一点点，可以说是灵活的。

We've already seen some of this, where any missing values are replaced with zero.

> 我们已经看到了一些情况，其中任何缺失的值都被替换为零。

For example, we can initialize a 5 element array to `1,2,0,0,0` with this:

> 例如，我们可以用这个方法将一个 5 个元素的数组初始化为 `1,2,0,0,0`：

::: {#cb635 .sourceCode}

```c
int a[5] = {1, 2};
```

:::

Or set an array entirely to zero with:

::: {#cb636 .sourceCode}

```c
int a[5] = {0};
```

:::

But things get interesting when initializing multidimensional arrays.

Let's make an array of 3 rows and 2 columns:

::: {#cb637 .sourceCode}

```c
int a[3][2];
```

:::

Let's write some code to initialize it and print the result:

::: {#cb638 .sourceCode}

```c
#include <stdio.h>

int main(void)
{
    int a[3][2] = {
        {1, 2},
        {3, 4},
        {5, 6}
    };

    for (int row = 0; row < 3; row++) {
        for (int col = 0; col < 2; col++)
            printf("%d ", a[row][col]);
        printf("\n");
    }
}
```

:::

And when we run it, we get the expected:

::: {#cb639 .sourceCode}

```{.sourceCode .default}
1 2
3 4
5 6
```

:::

Let's leave off some of the initializer elements and see they get set to zero:

> 让我们省略一些初始化元素，看看它们是否被设置为零：

::: {#cb640 .sourceCode}

```c
    int a[3][2] = {
        {1, 2},
        {3},    // Left off the 4!
        {5, 6}
    };
```

:::

which produces:

::: {#cb641 .sourceCode}

```{.sourceCode .default}
1 2
3 0
5 6
```

:::

Now let's leave off the entire last middle element:

::: {#cb642 .sourceCode}

```c
    int a[3][2] = {
        {1, 2},
        // {3, 4},   // Just cut this whole thing out
        {5, 6}
    };
```

:::

And now we get this, which might not be what you expect:

::: {#cb643 .sourceCode}

```{.sourceCode .default}
1 2
5 6
0 0
```

:::

But if you stop to think about it, we only provided enough initializers for two rows, so they got used for the first two rows. And the remaining elements were initialized to zero.

> 但如果你停下来想一想，我们只提供了足够的初始值给两行，所以它们被用于前两行。剩下的元素被初始化为零。

So far so good. Generally, if we leave off parts of the initializer, the compiler sets the corresponding elements to `0`.

> 到目前为止还不错。一般来说，如果我们省略初始化程序的某些部分，编译器会将相应的元素设置为“0”。

But let's get _crazy_.

::: {#cb644 .sourceCode}

```c
    int a[3][2] = { 1, 2, 3, 4, 5, 6 };
```

:::

What---? That's a 2D array, but it only has a 1D initializer!

Turns out that's legal (though GCC will warn about it with the proper warnings turned on).

> 结果这是合法的(尽管如果打开适当的警告，GCC 会发出警告)。

Basically, what it does is starts filling in elements in row 0, then row 1, then row 2 from left to right.

> 基本上，它做的是从左到右依次填充第 0 行、第 1 行和第 2 行的元素。

So when we print, it prints in order:

::: {#cb645 .sourceCode}

```{.sourceCode .default}
1 2
3 4
5 6
```

:::

If we leave some off:

::: {#cb646 .sourceCode}

```c
    int a[3][2] = { 1, 2, 3 };
```

:::

they fill with `0`:

::: {#cb647 .sourceCode}

```{.sourceCode .default}
1 2
3 0
0 0
```

:::

So if you want to fill the whole array with `0`, then go ahead and:

::: {#cb648 .sourceCode}

```c
    int a[3][2] = {0};
```

:::

But my recommendation is if you have a 2D array, use a 2D initializer. It just makes the code more readable. (Except for initializing the whole array with `0`, in which case it's idiomatic to use `{0}` no matter the dimension of the array.)

> 但我的建议是，如果你有一个二维数组，请使用二维初始化程序。这只会使代码更具可读性。(除了使用 `{0}` 初始化整个数组，无论数组的维度如何，这都是惯例。)

# [34] Long Jumps with `setjmp`, `longjmp` {#setjmp-longjmp number="34"}

We've already seen `goto`, which jumps in function scope. But `longjmp()` allows you to jump back to an earlier point in execution, back to a function that called this one.

> 我们已经看到了 `goto`，它可以跳转到函数作用域中。但是 `longjmp()` 允许您跳回到执行的较早点，回到调用此函数的函数。

There are a lot of limitations and caveats, but this can be a useful function for bailing out from deep in the call stack back up to an earlier state.

> 有很多限制和注意事项，但这可以是一个有用的功能，可以从调用堆栈深处跳出，回到较早的状态。

In my experience, this is very rarely-used functionality.

## [34.1] Using `setjmp` and `longjmp` {#using-setjmp-and-longjmp number="34.1"}

The dance we're going to do here is to basically put a bookmark in execution with `setjmp()`. Later on, we'll call `longjmp()` and it'll jump back to the earlier point in execution where we set the bookmark with `setjmp()`.

> 我们要在这里做的舞蹈基本上是用 `setjmp()` 在执行中放置一个书签。稍后，我们将调用 `longjmp()`，它将跳回我们用 `setjmp()` 设置书签的较早点的执行。

And it can do this even if you've called subfunctions.

Here's a quick demo where we call into functions a couple levels deep and then bail out of it.

> 这里有一个快速演示，我们调用几个层次深的函数，然后从中退出。

We're going to use a file scope variable `env` to keep the _state_ of things when we call `setjmp()` so we can restore them when we call `longjmp()` later. This is the variable in which we remember our "place".

> 我们将使用一个文件范围变量 `env` 来保存当我们调用 `setjmp()` 时的状态，以便我们稍后调用 `longjmp()` 时可以恢复它们。这是我们记住“位置”的变量。

The variable `env` is of type `jmp_buf`, an opaque type declared in `<setjmp.h>`.

> 变量 `env` 的类型是 `jmp_buf`，这是一种在 `<setjmp.h>` 中声明的不透明类型。

::: {#cb649 .sourceCode}

```c
#include <stdio.h>
#include <setjmp.h>

jmp_buf env;

void depth2(void)
{
    printf("Entering depth 2\n");
    longjmp(env, 3490);           // Bail out
    printf("Leaving depth 2\n");  // This won't happen
}

void depth1(void)
{
    printf("Entering depth 1\n");
    depth2();
    printf("Leaving depth 1\n");  // This won't happen
}

int main(void)
{
    switch (setjmp(env)) {
      case 0:
          printf("Calling into functions, setjmp() returned 0\n");
          depth1();
          printf("Returned from functions\n");  // This won't happen
          break;

      case 3490:
          printf("Bailed back to main, setjmp() returned 3490\n");
          break;
    }
}
```

:::

When run, this outputs:

::: {#cb650 .sourceCode}

```{.sourceCode .default}
Calling into functions, setjmp() returned 0
Entering depth 1
Entering depth 2
Bailed back to main, setjmp() returned 3490
```

:::

If you try to take that output and match it up with the code, it's clear there's some really _funky_ stuff going on.

> 如果你试着把输出与代码匹配起来，很明显出现了一些非常奇怪的事情。

One of the most notable things is that `setjmp()` returns _twice_. What the actual frank? What is this sorcery?!

> 一个最值得注意的事情是 `setjmp()` 返回了两次。这到底是什么鬼？这是什么魔法？！

So here's the deal: if `setjmp()` returns `0`, it means that you've successfully set the "bookmark" at that point.

> 所以这是个交易：如果 `setjmp()` 返回 `0`，那意味着你已经成功地在那一点上设置了“书签”。

If it returns non-zero, it means you've just returned to the "bookmark" set earlier. (And the value returned is the one you pass to `longjmp()`.)

> 如果它返回非零值，意味着你刚刚返回到之前设置的“书签”。(返回的值就是你传递给 `longjmp()` 的值。)

This way you can tell the difference between setting the bookmark and returning to it later.

> 这样你就可以区分设置书签和稍后返回它们的区别了。

So when the code, above, calls `setjmp()` the first time, `setjmp()` _stores_ the state in the `env` variable and returns `0`. Later when we call `longjmp()` with that same `env`, it restores the state and `setjmp()` returns the value `longjmp()` was passed.

> 当上面的代码第一次调用 `setjmp()` 时，`setjmp()` 就会将状态存储在 `env` 变量中，并返回 `0`。稍后，当我们使用相同的 `env` 调用 `longjmp()` 时，它就会恢复状态，而 `setjmp()` 则会返回 `longjmp()` 接收的值。

## [34.2] Pitfalls {#pitfalls number="34.2"}

Under the hood, this is pretty straightforward. Typically the _stack pointer_ keeps track of the locations in memory that local variables are stored, and the _program counter_ keeps track of the address of the currently-executing instruction[^179^].

> 在底层，这很简单。通常，_堆栈指针_跟踪存储本地变量的内存位置，而_程序计数器_跟踪当前正在执行指令的地址。

So if we want to jump back to an earlier function, it's basically only a matter of restoring the stack pointer and program counter to the values kept in the `jmp_buf` variable, and making sure the return value is set correctly. And then execution will resume there.

> 如果我们想跳回到较早的函数，只需要将堆栈指针和程序计数器恢复到 `jmp_buf` 变量中保存的值，并确保返回值设置正确。然后执行将在那里恢复。

But a variety of factors confound this, making a significant number of undefined behavior traps.

> 但是许多因素使这种情况变得复杂，导致大量未定义行为陷阱。

### [34.2.1] The Values of Local Variables {#the-values-of-local-variables number="34.2.1"}

If you want the values of automatic (non-`static` and non-`extern`) local variables to persist in the function that called `setjmp()` after a `longjmp()` happens, you must declare those variables to be `volatile`.

> 如果你想让自动(非静态和非外部)局部变量在调用 setjmp()之后 longjmp()发生时在调用函数中持续存在，你必须将这些变量声明为 volatile。

Technically, they only have to be `volatile` if they change between the time `setjmp()` is called and `longjmp()` is called[^180^].

> 技术上，只有在调用 `setjmp()` 和 `longjmp()` 之间发生变化时，它们才必须是“易失性”的。

For example, if we run this code:

::: {#cb651 .sourceCode}

```c
int x = 20;

if (setjmp(env) == 0) {
    x = 30;
}
```

:::

and then later `longjmp()` back, the value of `x` will be indeterminate.

If we want to fix this, `x` must be `volatile`:

::: {#cb652 .sourceCode}

```c
volatile int x = 20;

if (setjmp(env) == 0) {
    x = 30;
}
```

:::

Now the value will be the correct `30` after a `longjmp()` returns us to this point.

> 现在，在 `longjmp()` 将我们带回这一点后，值将是正确的 `30`。

### [34.2.2] How Much State is Saved? {#how-much-state-is-saved number="34.2.2"}

When you `longjmp()`, execution resumes at the point of the corresponding `setjmp()`. And that's it.

> 当你使用 longjmp()时，执行将恢复到对应的 setjmp()的点。就是这样。

The spec points out that it's just as if you'd jumped back into the function at that point with local variables set to whatever values they had when the `longjmp()` call was made.

> 这个规格指出，就好像你在 `longjmp()` 调用时，以当时的局部变量值跳回函数的那个点一样。

Things that aren't restored include, paraphrasing the spec:

- Floating point status flags
- Open files
- Any other component of the abstract machine

### [34.2.3] You Can't Name Anything `setjmp` {#you-cant-name-anything-setjmp number="34.2.3"}

You can't have any `extern` identifiers with the name `setjmp`. Or, if `setjmp` is a macro, you can't undefine it.

> 你不能使用名为“setjmp”的任何“extern”标识符。或者，如果“setjmp”是一个宏，你不能取消它的定义。

Both are undefined behavior.

### [34.2.4] You Can't `setjmp()` in a Larger Expression {#you-cant-setjmp-in-a-larger-expression number="34.2.4"}

That is, you can't do something like this:

::: {#cb653 .sourceCode}

```c
if (x == 12 && setjmp(env) == 0) { ... }
```

:::

That's too complex to be allowed by the spec due to the machinations that must occur when unrolling the stack and all that. We can't `longjmp()` back into some complex expression that's only been partially executed.

> 这太复杂了，不符合规范，因为在展开堆栈和所有这些时必须进行的机械操作。我们不能 `longjmp()` 回到只执行了部分的复杂表达式中。

So there are limits on the complexity of that expression.

- It can be the entire controlling expression of the conditional.

  ::: {#cb654 .sourceCode}

  ```c
  if (setjmp(env)) {...}
  ```

  :::

  ::: {#cb655 .sourceCode}

  ```c
  switch (setjmp(env)) {...}
  ```

  :::
- It can be part of a relational or equality expression, as long as the other operand is an integer constant. And the whole thing is the controlling expression of the conditional.

> 它可以是关系或等式表达式的一部分，只要另一个操作数是整数常量。整个表达式是条件语句的控制表达式。

::: {#cb656 .sourceCode}

```c
if (setjmp(env) == 0) {...}
```

:::

- The operand to a logical NOT (`!`) operation, being the entire controlling expression.

  ::: {#cb657 .sourceCode}

  ```c
  if (!setjmp(env)) {...}
  ```

  :::
- A standalone expression, possibly cast to `void`.

  ::: {#cb658 .sourceCode}

  ```c
  setjmp(env);
  ```

  :::

  ::: {#cb659 .sourceCode}

  ```c
  (void)setjmp(env);
  ```

  :::

### [34.2.5] When Can't You `longjmp()`? {#when-cant-you-longjmp number="34.2.5"}

It's undefined behavior if:

- You didn't call `setjmp()` earlier
- You called `setjmp()` from another thread
- You called `setjmp()` in the scope of a variable length array (VLA), and execution left the scope of that VLA before `longjmp()` was called.

> 你在可变长数组(VLA)的范围内调用了 `setjmp()`，但在调用 `longjmp()` 之前，执行已经离开了该 VLA 的范围。

- The function containing the `setjmp()` exited before `longjmp()` was called.

On that last one, "exited" includes normal returns from the function, as well as the case if another `longjmp()` jumped back to "earlier" in the call stack than the function in question.

> 在最后一个，“退出”包括从函数的正常返回，以及另一个 `longjmp()` 跳回比该函数更早的调用栈的情况。

### [34.2.6] You Can't Pass `0` to `longjmp()` {#you-cant-pass-0-to-longjmp number="34.2.6"}

If you try to pass the value `0` to `longjmp()`, it will silently change that value to `1`.

> 如果你尝试把值 `0` 传递给 `longjmp()`，它会把这个值默默地改成 `1`。

Since `setjmp()` ultimately returns this value, and having `setjmp()` return `0` has special meaning, returning `0` is prohibited.

> 由于 `setjmp()` 最终会返回这个值，而且 `setjmp()` 返回 `0` 具有特殊含义，因此禁止返回 `0`。

### [34.2.7] `longjmp()` and Variable Length Arrays {#longjmp-and-variable-length-arrays number="34.2.7"}

If you are in scope of a VLA and `longjmp()` out there, the memory allocated to the VLA could leak[^181^].

> 如果你在 VLA 的范围内，并且使用 `longjmp()` 跳出，那么分配给 VLA 的内存可能会泄漏 [^181^]。

Same thing happens if you `longjmp()` back over any earlier functions that had VLAs still in scope.

> 如果你使用 `longjmp()` 回到任何以前的函数中，其中仍然有 VLAs，也会发生同样的情况。

This is one thing that really bugged me able VLAs---that you could write perfectly legitimate C code that squandered memory. But, hey---I'm not in charge of the spec.

> 这是一件真正让我烦恼的事情——VLAs，你可以编写完美合法的 C 代码，浪费内存。但是，嘿——我不负责规范。

# [35] Incomplete Types {#incomplete-types number="35"}

It might surprise you to learn that this builds without error:

::: {#cb660 .sourceCode}

```c
extern int a[];

int main(void)
{
    struct foo *x;
    union bar *y;
    enum baz *z;
}
```

:::

We never gave a size for `a`. And we have pointers to `struct` s `foo`, `bar`, and `baz` that never seem to be declared anywhere.

> 我们从未给出 `a` 的大小。我们有指向 `struct` s `foo`、`bar` 和 `baz` 的指针，但似乎从未声明过。

And the only warnings I get are that `x`, `y`, and `z` are unused.

These are examples of _incomplete types_.

An incomplete type is a type the size (i.e. the size you'd get back from `sizeof`) for which is not known. Another way to think of it is a type that you haven't finished declaring.

> 一个不完整的类型是大小(即从 `sizeof` 返回的大小)未知的类型。另一种理解它的方式是你还没有完成声明的类型。

You can have a pointer to an incomplete type, but you can't dereference it or use pointer arithmetic on it. And you can't `sizeof` it.

> 你可以拥有一个指向不完整类型的指针，但是你不能对其解引用或者使用指针运算。而且你也不能对它使用 `sizeof` 运算符。

So what can you do with it?

## [35.1] Use Case: Self-Referential Structures {#use-case-self-referential-structures number="35.1"}

I only know of one real use case: forward references to `struct` s or `union` s with self-referential or co-dependent structures. (I'm going to use `struct` for the rest of these examples, but they all apply equally to `union` s, as well.)

> 我只知道一个真实的用例：对具有自引用或相互依赖结构的 `struct` 或 `union` 进行前向引用。(我将在接下来的例子中使用 `struct`，但它们对 `union` 也同样适用。)

Let's do the classic example first.

But before I do, know this! As you declare a `struct`, the `struct` is incomplete until the closing brace is reached!

> 在我做之前，要知道！当你声明一个结构体时，结构体在直到闭括号被达到之前是不完整的！

::: {#cb661 .sourceCode}

```c
struct antelope {              // struct antelope is incomplete here
    int leg_count;             // Still incomplete
    float stomach_fullness;    // Still incomplete
    float top_speed;           // Still incomplete
    char *nickname;            // Still incomplete
};                             // NOW it's complete.
```

:::

So what? Seems sane enough.

But what if we're doing a linked list? Each linked list node needs to have a reference to another node. But how can we create a reference to another node if we haven't finished even declaring the node yet?

> 但是如果我们正在做链表呢？每个链表节点都需要有一个指向另一个节点的引用。但是如果我们甚至还没有完成声明节点，我们怎么能创建一个指向另一个节点的引用呢？

C's allowance for incomplete types makes it possible. We can't declare a node, but we _can_ declare a pointer to one, even if it's incomplete!

> C 允许不完整的类型，这使得可能。我们不能声明一个节点，但是我们可以声明一个指向它的指针，即使它是不完整的！

::: {#cb662 .sourceCode}

```c
struct node {
    int val;
    struct node *next;  // struct node is incomplete, but that's OK!
};
```

:::

Even though the `struct node` is incomplete on line 3, we can still declare a pointer to one[^182^].

> 即使第三行的 `struct node` 不完整，我们仍然可以声明一个指向它的指针 [^182^]。

We can do the same thing if we have two different `struct` s that refer to each other:

> 我们可以在有两个不同的 `struct` 相互引用的情况下做同样的事情：

::: {#cb663 .sourceCode}

```c
struct a {
    struct b *x;  // Refers to a `struct b`
};

struct b {
    struct a *x;  // Refers to a `struct a`
};
```

:::

We'd never be able to make that pair of structures without the relaxed rules for incomplete types.

> 我们没有不完整类型的宽松规则，就不可能制造出那对结构。

## [35.2] Incomplete Type Error Messages {#incomplete-type-error-messages number="35.2"}

Are you getting errors like these?

::: {#cb664 .sourceCode}

```{.sourceCode .default}
invalid application of ‘sizeof’ to incomplete type

invalid use of undefined type

dereferencing pointer to incomplete type
```

:::

Most likely culprit: you probably forgot to `#include` the header file that declares the type.

> 最有可能的罪魁祸首：您可能忘记了 `#include` 声明类型的头文件。

## [35.3] Other Incomplete Types {#other-incomplete-types number="35.3"}

Declaring a `struct` or `union` with no body makes an incomplete type, e.g. `struct foo;`.

> 声明一个没有体的结构体或联合体会产生一个不完整的类型，例如 `struct foo;`。

`enums` are incomplete until the closing brace.

`void` is an incomplete type.

Arrays declared `extern` with no size are incomplete, e.g.:

::: {#cb665 .sourceCode}

```c
extern int a[];
```

:::

If it's a non-`extern` array with no size followed by an initializer, it's incomplete until the closing brace of the initializer.

> 如果是一个没有大小的非 `extern` 数组，后面跟着一个初始化器，那么在初始化器的闭括号之前，它是不完整的。

## [35.4] Use Case: Arrays in Header Files {#use-case-arrays-in-header-files number="35.4"}

It can be useful to declare incomplete array types in header files. In those cases, the actual storage (where the complete array is declared) should be in a single `.c` file. If you put it in the `.h` file, it will be duplicated every time the header file is included.

> 在头文件中声明不完整的数组类型可能会有用。在这种情况下，实际存储(完整数组声明的位置)应该在单个 `.c` 文件中。如果把它放在 `.h` 文件中，每次包含头文件时都会重复。

So what you can do is make a header file with an incomplete type that refers to the array, like so:

> 那么你可以做的是创建一个头文件，其中包含一个指向数组的不完整类型，如下所示：

::: {#cb666 .sourceCode}

```c
// File: bar.h

#ifndef BAR_H
#define BAR_H

extern int my_array[];  // Incomplete type

#endif
```

:::

And the in the `.c` file, actually define the array:

::: {#cb667 .sourceCode}

```c
// File: bar.c

int my_array[1024];     // Complete type!
```

:::

Then you can include the header from as many places as you'd like, and every one of those places will refer to the same underlying `my_array`.

> 那么，您可以从任意多个位置包含头文件，每个位置都会引用相同的底层 `my_array`。

::: {#cb668 .sourceCode}

```c
// File: foo.c

#include <stdio.h>
#include "bar.h"    // includes the incomplete type for my_array

int main(void)
{
    my_array[0] = 10;

    printf("%d\n", my_array[0]);
}
```

:::

When compiling multiple files, remember to specify all the `.c` files to the compiler, but not the `.h` files, e.g.:

> 编译多个文件时，记得将所有 `.c` 文件指定给编译器，而不是 `.h` 文件，例如：

::: {#cb669 .sourceCode}

```zsh
gcc -o foo foo.c bar.c
```

:::

## [35.5] Completing Incomplete Types {#completing-incomplete-types number="35.5"}

If you have an incomplete type, you can complete it by defining the complete `struct`, `union`, `enum`, or array in the same scope.

> 如果你有一个不完整的类型，你可以通过在同一作用域内定义完整的 `struct`、`union`、`enum` 或数组来完成它。

::: {#cb670 .sourceCode}

```c
struct foo;        // incomplete type

struct foo *p;     // pointer, no problem

// struct foo f;   // Error: incomplete type!

struct foo {
    int x, y, z;
};                 // Now the struct foo is complete!

struct foo f;      // Success!
```

:::

Note that though `void` is an incomplete type, there's no way to complete it. Not that anyone ever thinks of doing that weird thing. But it does explain why you can do this:

> 注意，虽然 `void` 是一种不完整的类型，但没有办法完成它。不是每个人都会想做这种奇怪的事情。但这解释了为什么你可以这样做：

::: {#cb671 .sourceCode}

```c
void *p;             // OK: pointer to incomplete type
```

:::

and not either of these:

::: {#cb672 .sourceCode}

```c
void v;              // Error: declare variable of incomplete type

printf("%d\n", *p);  // Error: dereference incomplete type
```

:::

The more you know...

# [36] Complex Numbers {#complex-numbers number="36"}

A tiny primer on [Complex numbers](https://en.wikipedia.org/wiki/Complex_number)[^183^] stolen directly from Wikipedia:

> 一个关于复数([Complex numbers](https://en.wikipedia.org/wiki/Complex_number)[^183^] 的小简介，直接从维基百科抄录：

> A **complex number** is a number that can be expressed in the form [\\(a+bi\\)]{.math .inline}, where [\\(a\\)]{.math .inline} and [\\(b\\)]{.math .inline} are real numbers \[i.e. floating point types in C\], and [\\(i\\)]{.math .inline} represents the imaginary unit, satisfying the equation [\\(i\^2=−1\\)]{.math .inline}. Because no real number satisfies this equation, [\\(i\\)]{.math .inline} is called an imaginary number. For the complex number [\\(a+bi\\)]{.math .inline}, [\\(a\\)]{.math .inline} is called the **real part**, and [\\(b\\)]{.math .inline} is called the **imaginary part**.

But that's as far as I'm going to go. We'll assume that if you're reading this chapter, you know what a complex number is and what you want to do with them.

> 但是我就到此为止了。假设你在阅读本章，你知道什么是复数以及你想用它们做什么。

And all we need to cover is C's faculties for doing so.

Turns out, though, that complex number support in a compiler is an _optional_ feature. Not all compliant compilers can do it. And the ones that do, might do it to various degrees of completeness.

> 原来，编译器中的复数支持是一个可选的功能。并不是所有符合规范的编译器都能做到这一点。而且，那些能做到的，可能会以不同程度的完整性来实现。

You can test if your system supports complex numbers with:

::: {#cb673 .sourceCode}

```c
#ifdef __STDC_NO_COMPLEX__
#error Complex numbers not supported!
#endif
```

:::

Furthermore, there is a macro that indicates adherence to the ISO 60559 (IEEE 754) standard for floating point math with complex numbers, as well as the presence of the `_Imaginary` type.

> 此外，还有一个宏表示遵守 ISO 60559(IEEE 754)标准的复数浮点数学以及 `_Imaginary` 类型的存在。

::: {#cb674 .sourceCode}

```c
#if __STDC_IEC_559_COMPLEX__ != 1
#error Need IEC 60559 complex support!
#endif
```

:::

More details on that are spelled out in Annex G in the C11 spec.

## [36.1] Complex Types {#complex-types number="36.1"}

To use complex numbers, `#include <complex.h>`.

With that, you get at least two types:

::: {#cb675 .sourceCode}

```c
_Complex
complex
```

:::

Those both mean the same thing, so you might as well use the prettier `complex`.

> 这两个意思是一样的，所以你最好使用更漂亮的“复杂”。

You also get some types for imaginary numbers if you implementation is IEC 60559-compliant:

> 你也可以得到一些虚数的类型，如果你的实现符合 IEC 60559 标准：

::: {#cb676 .sourceCode}

```c
_Imaginary
imaginary
```

:::

These also both mean the same thing, so you might as well use the prettier `imaginary`.

> 这些也都意味着同一件事，所以你不妨使用更漂亮的 `虚拟`。

You also get values for the imaginary number [\\(i\\)]{.math .inline}, itself:

> 你也可以得到虚数[\\(i\\)]{.math .inline}本身的值：

::: {#cb677 .sourceCode}

```c
I
_Complex_I
_Imaginary_I
```

:::

The macro `I` is set to `_Imaginary_I` (if available), or `_Complex_I`. So just use `I` for the imaginary number.

> 宏 `I` 被设置为 `_Imaginary_I`(如果可用)或 `_Complex_I`。所以只需使用 `I` 表示虚数。

One aside: I've said that if a compiler has `__STDC_IEC_559_COMPLEX__` set to `1`, it must support `_Imaginary` types to be compliant. That's my read of the spec. However, I don't know of a single compiler that actually supports `_Imaginary` even though they have `__STDC_IEC_559_COMPLEX__` set. So I'm going to write some code with that type in here I have no way of testing. Sorry!

> 顺便提一句：如果编译器将 `__STDC_IEC_559_COMPLEX__` 设置为 `1`，它必须支持 `_Imaginary` 类型才能符合标准。这是我对规范的理解。但是，我不知道有哪个编译器实际上支持 `_Imaginary`，即使它们将 `__STDC_IEC_559_COMPLEX__` 设置了。所以我要在这里编写一些使用该类型的代码，但我没有办法测试它。抱歉！

OK, so now we know there's a `complex` type, how can we use it?

## [36.2] Assigning Complex Numbers {#assigning-complex-numbers number="36.2"}

Since the complex number has a real and imaginary part, but both of them rely on floating point numbers to store values, we need to also tell C what precision to use for those parts of the complex number.

> 由于复数有实部和虚部，但它们都依赖浮点数来存储值，我们还需要告诉 C 用于复数的各个部分的精度。

We do that by just pinning a `float`, `double`, or `long double` to the `complex`, either before or after it.

> 我们可以在复数之前或之后将 `float`、`double` 或 `long double` 固定到复数上来实现这一目的。

Let's define a complex number that uses `float` for its components:

::: {#cb678 .sourceCode}

```c
float complex c;   // Spec prefers this way
complex float c;   // Same thing--order doesn't matter
```

:::

So that's great for declarations, but how do we initialize them or assign to them?

> 那么，声明很棒，但我们如何初始化它们或者为它们赋值呢？

Turns out we get to use some pretty natural notation. Example!

::: {#cb679 .sourceCode}

```c
double complex x = 5 + 2*I;
double complex y = 10 + 3*I;
```

:::

For [\\(5+2i\\)]{.math .inline} and [\\(10+3i\\)]{.math .inline}, respectively.

> 对于(5+2i)和(10+3i)分别来说。

## [36.3] Constructing, Deconstructing, and Printing {#constructing-deconstructing-and-printing number="36.3"}

We're getting there...

We've already seen one way to write a complex number:

::: {#cb680 .sourceCode}

```c
double complex x = 5 + 2*I;
```

:::

There's also no problem using other floating point numbers to build it:

::: {#cb681 .sourceCode}

```c
double a = 5;
double b = 2;
double complex x = a + b*I;
```

:::

There is also a set of macros to help build these. The above code could be written using the `CMPLX()` macro, like so:

> 也有一套宏来帮助构建这些。上面的代码可以使用 `CMPLX()` 宏简写，如下所示：

::: {#cb682 .sourceCode}

```c
double complex x = CMPLX(5, 2);
```

:::

As far as I can tell in my research, these are _almost_ equivalent:

::: {#cb683 .sourceCode}

```c
double complex x = 5 + 2*I;
double complex x = CMPLX(5, 2);
```

:::

But the `CMPLX()` macro will handle negative zeros in the imaginary part correctly every time, whereas the other way might convert them to positive zeros. I _think_[^184^] This seems to imply that if there's a chance the imaginary part will be zero, you should use the macro... but someone should correct me on this if I'm mistaken!

> 但是 `CMPLX()` 宏每次都能正确处理虚数部分的负零，而其他方法可能会将它们转换为正零。我认为 [^184^]这似乎意味着，如果有可能虚数部分为零，你应该使用宏...但如果我错了，有人应该纠正我！

The `CMPLX()` macro works on `double` types. There are two other macros for `float` and `long double`: `CMPLXF()` and `CMPLXL()`. (These "f" and "l" suffixes appear in virtually all the complex-number-related functions.)

> CMPLX()宏在 double 类型上有效。另外还有两个宏分别用于 float 和 long double：CMPLXF()和 CMPLXL()(这些"f"和"l"后缀几乎出现在所有与复数相关的函数中)。

Now let's try the reverse: if we have a complex number, how do we break it apart into its real and imaginary parts?

> 现在让我们尝试反过来：如果我们有一个复数，我们如何将它分解成它的实部和虚部？

Here we have a couple functions that will extract the real and imaginary parts from the number: `creal()` and `cimag()`:

> 这里有一对函数可以从数字中提取实部和虚部：`creal()` 和 `cimag()`：

::: {#cb684 .sourceCode}

```c
double complex x = 5 + 2*I;
double complex y = 10 + 3*I;

printf("x = %f + %fi\n", creal(x), cimag(x));
printf("y = %f + %fi\n", creal(y), cimag(y));
```

:::

for the output:

::: {#cb685 .sourceCode}

```{.sourceCode .default}
x = 5.000000 + 2.000000i
y = 10.000000 + 3.000000i
```

:::

Note that the `i` I have in the `printf()` format string is a literal `i` that gets printed---it's not part of the format specifier. Both return values from `creal()` and `cimag()` are `double`.

> 注意，`printf()` 格式字符串中的 `i` 是一个文字 `i`，会被打印出来，它不是格式说明符的一部分。`creal()` 和 `cimag()` 的返回值都是 `double` 类型的。

And as usual, there are `float` and `long double` variants of these functions: `crealf()`, `cimagf()`, `creall()`, and `cimagl()`.

> 正如往常一样，这些函数有 `float` 和 `long double` 两种变体：`crealf()`、`cimagf()`、`creall()` 和 `cimagl()`。

## [36.4] Complex Arithmetic and Comparisons {#complex-arithmetic-and-comparisons number="36.4"}

Arithmetic can be performed on complex numbers, though how this works mathematically is beyond the scope of the guide.

> 复数可以进行算术运算，但是如何从数学上实现这一点超出了本指南的范围。

::: {#cb686 .sourceCode}

```c
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2*I;
    double complex y = 3 + 4*I;
    double complex z;

    z = x + y;
    printf("x + y = %f + %fi\n", creal(z), cimag(z));

    z = x - y;
    printf("x - y = %f + %fi\n", creal(z), cimag(z));

    z = x * y;
    printf("x * y = %f + %fi\n", creal(z), cimag(z));

    z = x / y;
    printf("x / y = %f + %fi\n", creal(z), cimag(z));
}
```

:::

for a result of:

::: {#cb687 .sourceCode}

```{.sourceCode .default}
x + y = 4.000000 + 6.000000i
x - y = -2.000000 + -2.000000i
x * y = -5.000000 + 10.000000i
x / y = 0.440000 + 0.080000i
```

:::

You can also compare two complex numbers for equality (or inequality):

::: {#cb688 .sourceCode}

```c
#include <stdio.h>
#include <complex.h>

int main(void)
{
    double complex x = 1 + 2*I;
    double complex y = 3 + 4*I;

    printf("x == y = %d\n", x == y);  // 0
    printf("x != y = %d\n", x != y);  // 1
}
```

:::

with the output:

::: {#cb689 .sourceCode}

```{.sourceCode .default}
x == y = 0
x != y = 1
```

:::

They are equal if both components test equal. Note that as with all floating point, they could be equal if they're close enough due to rounding error[^185^].

> 他们如果两个组件都测试相等，就相等。请注意，由于所有浮点数都可能由于舍入误差而足够接近，因此它们也可能相等。

## [36.5] Complex Math {#complex-math number="36.5"}

But wait! There's more than just simple complex arithmetic!

Here's a summary table of all the math functions available to you with complex numbers.

> 以下是您可以使用复数的所有数学函数的摘要表。

I'm only going to list the `double` version of each function, but for all of them there is a `float` version that you can get by appending `f` to the function name, and a `long double` version that you can get by appending `l`.

> 我只会列出每个函数的 `双精度` 版本，但所有函数都有 `单精度` 版本，可以在函数名后面加上 `f` 来获取，还有 `长双精度` 版本，可以在函数名后面加上 `l` 来获取。

For example, the `cabs()` function for computing the absolute value of a complex number also has `cabsf()` and `cabsl()` variants. I'm omitting them for brevity.

> 例如，用于计算复数绝对值的 `cabs()` 函数也有 `cabsf()` 和 `cabsl()` 变体。为了简洁起见，我将它们省略。

### [36.5.1] Trigonometry Functions {#trigonometry-functions number="36.5.1"}

---

Function Description

---

`ccos()` Cosine

`csin()` Sine

`ctan()` Tangent

`cacos()` Arc cosine

`casin()` Arc sine

`catan()` Play _Settlers of Catan_

`ccosh()` Hyperbolic cosine

`csinh()` Hyperbolic sine

`ctanh()` Hyperbolic tangent

`cacosh()` Arc hyperbolic cosine

`casinh()` Arc hyperbolic sine

## `catanh()` Arc hyperbolic tangent

### [36.5.2] Exponential and Logarithmic Functions {#exponential-and-logarithmic-functions number="36.5.2"}

---

Function Description

---

`cexp()` Base-[\\(e\\)]{.math .inline} exponential

## `clog()` Natural (base-[\\(e\\)] {.math .inline}) logarithm

### [36.5.3] Power and Absolute Value Functions {#power-and-absolute-value-functions number="36.5.3"}

---

Function Description

---

`cabs()` Absolute value

`cpow()` Power

## `csqrt()` Square root

### [36.5.4] Manipulation Functions {#manipulation-functions number="36.5.4"}

---

Function Description

---

`creal()` Return real part

`cimag()` Return imaginary part

`CMPLX()` Construct a complex number

`carg()` Argument/phase angle

`conj()` Conjugate[^186^]

## `cproj()` Projection on Riemann sphere

# [37] Fixed Width Integer Types {#fixed-width-integer-types number="37"}

C has all those small, bigger, and biggest integer types like `int` and `long` and all that. And you can look in [the section on limits](#limits-macros) to see what the largest int is with `INT_MAX` and so on.

> C 有所有这些小的、大的和最大的整数类型，比如 `int` 和 `long` 等等。你可以查看[限制宏定义部分](#limits-macros)来查看最大的 int 是多少，使用 `INT_MAX` 等等。

How big are those types? That is, how many bytes do they take up? We could use `sizeof` to get that answer.

> 这些类型有多大？也就是说，它们占用多少字节？我们可以使用 `sizeof` 来获得答案。

But what if I wanted to go the other way? What if I needed a type that was exactly 32 bits (4 bytes) or at least 16 bits or somesuch?

> 如果我想要走另一条路怎么办？如果我需要一种精确的 32 位(4 字节)或至少 16 位的类型怎么办？

How can we declare a type that's a certain size?

The header `<stdint.h>` gives us a way.

## [37.1] The Bit-Sized Types {#the-bit-sized-types number="37.1"}

For both signed and unsigned integers, we can specify a type that is a certain number of bits, with some caveats, of course.

> 对于有符号和无符号整数，我们可以指定一种特定位数的类型，当然也有一些限制。

And there are three main classes of these types (in these examples, the `N` would be replaced by a certain number of bits):

> 这些类型有三个主要类别(在这些示例中，`N` 将被某个位数替换)：

- Integers of exactly a certain size (`intN_t`)
- Integers that are at least a certain size (`int_leastN_t`)
- Integers that are at least a certain size and are as fast as possible (`int_fastN_t`)[^187^]

> 整数至少要达到一定大小，并且尽可能快(`int_fastN_t`)[^187^]

How much faster is `fast`? Definitely maybe some amount faster. Probably. The spec doesn't say how much faster, just that they'll be the fastest on this architecture. Most C compilers are pretty good, though, so you'll probably only see this used in places where the most possible speed needs to be guaranteed (rather than just hoping the compiler is producing pretty-dang-fast code, which it is).

> "快多少？可能会快一些。指定没有说明快多少，只是说它在这个架构上是最快的。不过大多数 C 编译器都很不错，所以你可能只会在需要保证最大可能速度的地方使用它(而不是只是希望编译器能够产生相当快的代码，它确实可以)。

Finally, these unsigned number types have a leading `u` to differentiate them.

> 最后，这些无符号数类型有一个前导的“u”来区分它们。

For example, these types have the corresponding listed meaning:

::: {#cb690 .sourceCode}

```c
int32_t w;        // x is exactly 32 bits, signed
uint16_t x;       // y is exactly 16 bits, unsigned

int_least8_t y;   // y is at least 8 bits, signed

uint_fast64_t z;  // z is the fastest representation at least 64 bits, unsigned
```

:::

The following types are guaranteed to be defined:

::: {#cb691 .sourceCode}

```c
int_least8_t      uint_least8_t
int_least16_t     uint_least16_t
int_least32_t     uint_least32_t
int_least64_t     uint_least64_t

int_fast8_t       uint_fast8_t
int_fast16_t      uint_fast16_t
int_fast32_t      uint_fast32_t
int_fast64_t      uint_fast64_t
```

:::

There might be others of different widths, as well, but those are optional.

> 可能还有其他不同宽度的，但那些是可选的。

Hey! Where are the fixed types like `int16_t`? Turns out those are entirely optional...unless certain conditions are met[^188^]. And if you have an average run-of-the-mill modern computer system, those conditions probably are met. And if they are, you'll have these types:

> 嘿！像 `int16_t` 这样的固定类型在哪里？原来这些都是可选的...除非满足某些条件[^188^](#fn188)。如果你有一台普通的现代计算机系统，这些条件可能已经满足了。如果是这样，你将拥有这些类型：

::: {#cb692 .sourceCode}

```c
int8_t      uint8_t
int16_t     uint16_t
int32_t     uint32_t
int64_t     uint64_t
```

:::

Other variants with different widths might be defined, but they're optional.

> 其他不同宽度的变体可以定义，但它们是可选的。

## [37.2] Maximum Integer Size Type {#maximum-integer-size-type number="37.2"}

There's a type you can use that holds the largest representable integers available on the system, both signed and unsigned:

> 在系统中可以使用一种类型来保存最大的可表示的整数，无论是有符号的还是无符号的：

::: {#cb693 .sourceCode}

```c
intmax_t
uintmax_t
```

:::

Use these types when you want to go as big as possible.

Obviously values from any other integer types of the same sign will fit in this type, necessarily.

> 显然，任何具有相同符号的其他整数类型的值都必定适合这种类型。

## [37.3] Using Fixed Size Constants {#using-fixed-size-constants number="37.3"}

If you have a constant that you want to have fit in a certain number of bits, you can use these macros to automatically append the proper suffix onto the number (e.g. `22L` or `3490ULL`).

> 如果你有一个常数，你想让它适合某些位数，你可以使用这些宏自动在数字后面添加适当的后缀(例如 `22L` 或 `3490ULL`)。

::: {#cb694 .sourceCode}

```c
INT8_C(x)     UINT8_C(x)
INT16_C(x)    UINT16_C(x)
INT32_C(x)    UINT32_C(x)
INT64_C(x)    UINT64_C(x)
INTMAX_C(x)   UINTMAX_C(x)
```

:::

Again, these work only with constant integer values.

For example, we can use one of these to assign constant values like so:

::: {#cb695 .sourceCode}

```c
uint16_t x = UINT16_C(12);
intmax_t y = INTMAX_C(3490);
```

:::

## [37.4] Limits of Fixed Size Integers {#limits-of-fixed-size-integers number="37.4"}

We also have some limits defined so you can get the maximum and minimum values for these types:

> 我们也定义了一些限制，因此您可以获得这些类型的最大值和最小值：

::: {#cb696 .sourceCode}

```c
INT8_MAX           INT8_MIN           UINT8_MAX
INT16_MAX          INT16_MIN          UINT16_MAX
INT32_MAX          INT32_MIN          UINT32_MAX
INT64_MAX          INT64_MIN          UINT64_MAX

INT_LEAST8_MAX     INT_LEAST8_MIN     UINT_LEAST8_MAX
INT_LEAST16_MAX    INT_LEAST16_MIN    UINT_LEAST16_MAX
INT_LEAST32_MAX    INT_LEAST32_MIN    UINT_LEAST32_MAX
INT_LEAST64_MAX    INT_LEAST64_MIN    UINT_LEAST64_MAX

INT_FAST8_MAX      INT_FAST8_MIN      UINT_FAST8_MAX
INT_FAST16_MAX     INT_FAST16_MIN     UINT_FAST16_MAX
INT_FAST32_MAX     INT_FAST32_MIN     UINT_FAST32_MAX
INT_FAST64_MAX     INT_FAST64_MIN     UINT_FAST64_MAX

INTMAX_MAX         INTMAX_MIN         UINTMAX_MAX
```

:::

Note the `MIN` for all the unsigned types is `0`, so, as such, there's no macro for it.

> 注意所有无符号类型的 `MIN` 值都是 `0`，因此没有宏定义。

## [37.5] Format Specifiers {#format-specifiers number="37.5"}

In order to print these types, you need to send the right format specifier to `printf()`. (And the same issue for getting input with `scanf()`.)

> 为了打印这些类型，你需要发送正确的格式说明符到 `printf()`。(对于使用 `scanf()` 获取输入也是同样的问题。)

But how are you going to know what size the types are under the hood? Luckily, once again, C provides some macros to help with this.

> 但你怎么知道底层的类型大小呢？幸运的是，C 再次提供了一些宏来帮助解决这个问题。

All this can be found in `<inttypes.h>`.

Now, we have a bunch of macros. Like a complexity explosion of macros. So I'm going to stop listing out every one and just put the lowercase letter `n` in the place where you should put `8`, `16`, `32`, or `64` depending on your needs.

> 现在，我们有一堆宏。就像复杂性爆炸的宏一样。所以我要停止列出每一个，只需在您需要放置 `8`、`16`、`32` 或 `64` 的地方放置小写字母 `n`。

Let's look at the macros for printing signed integers:

::: {#cb697 .sourceCode}

```c
PRIdn    PRIdLEASTn    PRIdFASTn    PRIdMAX
PRIin    PRIiLEASTn    PRIiFASTn    PRIiMAX
```

:::

Look for the patterns there. You can see there are variants for the fixed, least, fast, and max types.

> 寻找那里的模式。你可以看到有固定、最少、快速和最大类型的变体。

And you also have a lowercase `d` and a lowercase `i`. Those correspond to the `printf()` format specifiers `%d` and `%i`.

> 你也有一个小写的'd'和一个小写的'i'。这些对应于 `printf()` 格式说明符 `%d` 和 `%i`。

So if I have something of type:

::: {#cb698 .sourceCode}

```c
int_least16_t x = 3490;
```

:::

I can print that with the equivalent format specifier for `%d` by using `PRIdLEAST16`.

> 我可以使用 `PRIdLEAST16` 来用等效的格式说明符 `%d` 来打印。

But how? How do we use that macro?

First of all, that macro specifies a string containing the letter or letters `printf()` needs to use to print that type. Like, for example, it could be `"d"` or `"ld"`.

> 首先，该宏指定一个包含 `printf()` 需要使用的字母或字母的字符串。例如，它可以是 `"d"` 或 `"ld"`。

So all we need to do is embed that in our format string to the `printf()` call.

> 所以我们需要做的就是将它嵌入我们的格式字串到 `printf()` 呼叫中。

To do this, we can take advantage of a fact about C that you might have forgotten: adjacent string literals are automatically concatenated to a single string. E.g.:

> 要做到这一点，我们可以利用一个你可能已经忘记的有关 C 的事实：相邻的字符串文字会自动连接成一个字符串。例如：`转换为` 简体中文 `

::: {#cb699 .sourceCode}

```c
printf("Hello, " "world!\n");   // Prints "Hello, world!"
```

:::

And since these macros are string literals, we can use them like so:

::: {#cb700 .sourceCode}

```c
#include <stdio.h>
#include <stdint.h>
#include <inttypes.h>

int main(void)
{
    int_least16_t x = 3490;

    printf("The value is %" PRIdLEAST16 "!\n", x);
}
```

:::

We also have a pile of macros for printing unsigned types:

::: {#cb701 .sourceCode}

```c
PRIon    PRIoLEASTn    PRIoFASTn    PRIoMAX
PRIun    PRIuLEASTn    PRIuFASTn    PRIuMAX
PRIxn    PRIxLEASTn    PRIxFASTn    PRIxMAX
PRIXn    PRIXLEASTn    PRIXFASTn    PRIXMAX
```

:::

In this case, `o`, `u`, `x`, and `X` correspond to the documented format specifiers in `printf()`.

> 在这种情况下，`o`，`u`，`x` 和 `X` 对应于 `printf()` 中文档中的格式说明符。

And, as before, the lowercase `n` should be substituted with `8`, `16`, `32`, or `64`.

> 而且，像以前一样，小写的 `n` 应该用 `8`、`16`、`32` 或 `64` 来替换。

But just when you think you had enough of the macros, it turns out we have a complete complementary set of them for `scanf()`!

> 但是，当你认为你已经足够了解宏时，原来我们还有一整套完整的宏专门用于 `scanf()`！

::: {#cb702 .sourceCode}

```c
SCNdn    SCNdLEASTn    SCNdFASTn    SCNdMAX
SCNin    SCNiLEASTn    SCNiFASTn    SCNiMAX
SCNon    SCNoLEASTn    SCNoFASTn    SCNoMAX
SCNun    SCNuLEASTn    SCNuFASTn    SCNuMAX
SCNxn    SCNxLEASTn    SCNxFASTn    SCNxMAX
```

:::

Remember: when you want to print out a fixed size integer type with `printf()` or `scanf()`, grab the correct corresponding format specifer from `<inttypes.h>`.

> 记住：当你想使用 `printf()` 或 `scanf()` 打印出固定大小的整数类型时，从 `<inttypes.h>` 中获取正确的对应格式说明符。

# [38] Date and Time Functionality {#date-and-time-functionality number="38"}

> "Time is an illusion. Lunchtime doubly so."
> ---Ford Prefect, The Hitchhikers Guide to the Galaxy

This isn't too complex, but it can be a little intimidating at first, both with the different types available and the way we can convert between them.

> 这不是太复杂，但一开始可能有点吓人，因为有不同类型，以及我们如何在它们之间进行转换。

Mix in GMT (UTC) and local time and we have all the *Usual Fun*™ one gets with times and dates.

> 在 GMT(UTC)和本地时间混合在一起，我们就可以享受到与时间和日期有关的所有 *Usual Fun*™。

And of course never forget the golden rule of dates and times: _Never attempt to write your own date and time functionality. Only use what the library gives you._

> 当然，永远不要忘记日期和时间的黄金法则：永远不要尝试编写自己的日期和时间功能。只使用库提供的功能。

Time is too complex for mere mortal programmers to handle correctly. Seriously, we all owe a point to everyone who worked on any date and time library, so put that in your budget.

> 时间太复杂，凡人程序员无法正确处理。说真的，我们都应该感谢每一个参与日期和时间库开发的人，所以要把这个放进你的预算中。

## [38.1] Quick Terminology and Information {#quick-terminology-and-information number="38.1"}

Just a couple quick terms in case you don't have them down.

- **UTC**: Coordinated Universal Time is a universally[^189^] agreed upon, absolute time. Everyone on the planet thinks it's the same time right now in UTC... even though they have different local times.

> UTC(协调世界时)是一种全球公认的绝对时间。全球每个人都认为现在的时间是 UTC 时间，尽管他们有不同的当地时间。

- **GMT**: Greenwich Mean Time, effectively the same as UTC[^190^]. You probably want to say UTC, or "universal time". If you're talking specifically about the GMT time zone, say GMT. Confusingly, many of C's UTC functions predate UTC and still refer to Greenwich Mean Time. When you see that, know that C means UTC.

> 格林威治标准时间(GMT)，与 UTC[^190^]实质上相同。你可能想说 UTC，或者“世界时”。如果你特别指的是 GMT 时区，就说 GMT。令人困惑的是，C 语言中的许多 UTC 函数都比 UTC 更早，仍然指的是格林威治标准时间。当你看到这个时，要知道 C 语言指的是 UTC。

- **Local time**: what time it is where the computer running the program is located. This is described as an offset from UTC. Although there are many time zones in the world, most computers do work in either local time or UTC.

> 本地时间：运行程序的计算机所在地的时间。这是以 UTC 时间偏移量来描述的。尽管世界上有许多时区，但大多数计算机都是以本地时间或 UTC 时间工作的。

As a general rule, if you are describing an event that happens one time, like a log entry, or a rocket launch, or when pointers finally clicked for you, use UTC.

> 一般而言，如果您要描述一次性发生的事件，如日志条目，火箭发射或指针终于对您起作用，请使用 UTC。

On the other hand, if it's something that happens the same time _in every time zone_, like New Year's Eve or dinner time, use local time.

> 另一方面，如果某件事情在每个时区都是同时发生的，比如新年夜或者晚餐时间，就使用当地时间。

Since a lot of languages are only good at converting between UTC and local time, you can cause yourself a lot of pain by choosing to store your dates in the wrong form. (Ask me how I know.)

> 由于许多语言只擅长在 UTC 和本地时间之间转换，如果你选择以错误的形式存储日期，可能会给自己带来很多麻烦(问我是怎么知道的)。

## [38.2] Date Types {#date-types number="38.2"}

There are two[^191^] main types in C when it comes to dates: `time_t` and `struct tm`.

> 在 C 语言中，涉及到日期时，有两种主要类型：`time_t` 和 `struct tm`。

The spec doesn't actually say much about them:

- `time_t`: a real type capable of holding a time. So by the spec, this could be a floating type or integer type. In POSIX (Unix-likes), it's an integer. This holds _calendar time_. Which you can think of as UTC time.

> `time_t`：一种能够容纳时间的实际类型。根据规范，这可能是浮点类型或整数类型。在 POSIX(类 Unix)中，它是一个整数。它保存_日历时间_。你可以把它想象成 UTC 时间。

- `struct tm`: holds the components of a calendar time. This is a _broken-down time_, i.e. the components of the time, like hour, minute, second, day, month, year, etc.

> `struct tm`：保存日历时间的组成部分。这是一个_分解的时间_，即时间的组成部分，如小时，分钟，秒，天，月，年等。

On a lot of systems, `time_t` represents the number of seconds since [_Epoch_](https://en.wikipedia.org/wiki/Unix_time)[^192^]. Epoch is in some ways the start of time from the computer's perspective, which is commonly January 1, 1970 UTC. `time_t` can go negative to represent times before Epoch. Windows behaves the same way as Unix from what I can tell.

> 在许多系统中，`time_t` 表示自 [Epoch](https://en.wikipedia.org/wiki/Unix_time)[^192^]以来的秒数。从计算机的角度来看，Epoch 可以说是时间的起点，通常是 1970 年 1 月 1 日 UTC。 `time_t` 可以为负，以表示 Epoch 之前的时间。据我所知，Windows 的行为与 Unix 相同。

And what's in a `struct tm`? The following fields:

::: {#cb703 .sourceCode}

```c
struct tm {
    int tm_sec;    // seconds after the minute -- [0, 60]
    int tm_min;    // minutes after the hour -- [0, 59]
    int tm_hour;   // hours since midnight -- [0, 23]
    int tm_mday;   // day of the month -- [1, 31]
    int tm_mon;    // months since January -- [0, 11]
    int tm_year;   // years since 1900
    int tm_wday;   // days since Sunday -- [0, 6]
    int tm_yday;   // days since January 1 -- [0, 365]
    int tm_isdst;  // Daylight Saving Time flag
};
```

:::

Note that everything is zero-based except the day of the month.

It's important to know that you can put any values in these types you want. There are functions to help get the time _now_, but the types hold _a_ time, not _the_ time.

> 重要的是要知道你可以在这些类型中放入任何值。有一些函数可以帮助你获取当前时间，但是这些类型只保存一个时间，而不是当前时间。

So the question becomes: "How do you initialize data of these types, and how do you convert between them?"

> 那么问题就变成了：“你如何初始化这些类型的数据，以及如何在它们之间进行转换？”

## [38.3] Initialization and Conversion Between Types {#initialization-and-conversion-between-types number="38.3"}

First, you can get the current time and store it in a `time_t` with the `time()` function.

> 首先，你可以使用 `time()` 函数获取当前时间并将其存储在 `time_t` 中。

::: {#cb704 .sourceCode}

```c
time_t now;  // Variable to hold the time now

now = time(NULL);  // You can get it like this...

time(&now);        // ...or this. Same as the previous line.
```

:::

Great! You have a variable that gets you the time now.

Amusingly, there's only one portable way to print out what's in a `time_t`, and that's the rarely-used `ctime()` function that prints the value in local time:

> 有趣的是，只有一种可移植的方法可以打印出'time_t'中的内容，那就是很少使用的 `ctime()` 函数，它会以本地时间打印出该值：

::: {#cb705 .sourceCode}

```c
now = time(NULL);
printf("%s", ctime(&now));
```

:::

This returns a string with a very specific form that includes a newline at the end:

> 这会返回一个具有非常特定形式的字符串，其中包括一个换行符在末尾：

::: {#cb706 .sourceCode}

```{.sourceCode .default}
Sun Feb 28 18:47:25 2021
```

:::

So that's kind of inflexible. If you want more control, you should convert that `time_t` into a `struct tm`.

> 如此不太灵活。如果你想要更多的控制，你应该把 `time_t` 转换成 `struct tm`。

### [38.3.1] Converting `time_t` to `struct tm` {#converting-time_t-to-struct-tm number="38.3.1"}

There are two amazing ways to do this conversion:

- `localtime()`: this function converts a `time_t` to a `struct tm` in local time.

```{=html}
<!-- -->
```

- `gmtime()`: this function converts a `time_t` to a `struct tm` in UTC. (See ye olde GMT creeping into that function name?)

> `gmtime()`：此函数将 `time_t` 转换为 UTC 中的 `struct tm`(看到古老的 GMT 悄悄出现在函数名中吗？)

Let's see what time it is now by printing out a `struct tm` with the `asctime()` function:

> 让我们通过使用 `asctime()` 函数打印出一个 `struct tm` 来看看现在是几点了：

::: {#cb707 .sourceCode}

```c
printf("Local: %s", asctime(localtime(&now)));
printf("  UTC: %s", asctime(gmtime(&now)));
```

:::

Output (I'm in the Pacific Standard Time zone):

::: {#cb708 .sourceCode}

```{.sourceCode .default}
Local: Sun Feb 28 20:15:27 2021
  UTC: Mon Mar  1 04:15:27 2021
```

:::

Once you have your `time_t` in a `struct tm`, it opens all kinds of doors. You can print out the time in a variety of ways, figure out which day of the week a date is, and so on. Or convert it back into a `time_t`.

> 一旦你把 `time_t` 放入 `struct tm` 中，就可以做很多事情。你可以以多种方式打印出时间，找出某个日期是星期几，等等。或者把它转换回 `time_t`。

More on that soon!

### [38.3.2] Converting `struct tm` to `time_t` {#converting-struct-tm-to-time_t number="38.3.2"}

If you want to go the other way, you can use `mktime()` to get that information.

> 如果你想以另一种方式去做，你可以使用 `mktime()` 来获取这些信息。

`mktime()` sets the values of `tm_wday` and `tm_yday` for you, so don't bother filling them out because they'll just be overwritten.

Also, you can set `tm_isdst` to `-1` to have it make the determination for you. Or you can manually set it to true or false.

> 也可以将 `tm_isdst` 设置为 `-1`，让它为您做出决定。或者您可以手动将其设置为 true 或 false。

::: {#cb709 .sourceCode}

```c
// Don't be tempted to put leading zeros on these numbers (unless you
// mean for them to be in octal)!

struct tm some_time = {
    .tm_year=82,   // years since 1900
    .tm_mon=3,     // months since January -- [0, 11]
    .tm_mday=12,   // day of the month -- [1, 31]
    .tm_hour=12,   // hours since midnight -- [0, 23]
    .tm_min=0,     // minutes after the hour -- [0, 59]
    .tm_sec=4,     // seconds after the minute -- [0, 60]
    .tm_isdst=-1,  // Daylight Saving Time flag
};

time_t some_time_epoch;

some_time_epoch = mktime(&some_time);

printf("%s", ctime(&some_time_epoch));
printf("Is DST: %d\n", some_time.tm_isdst);
```

:::

Output:

::: {#cb710 .sourceCode}

```{.sourceCode .default}
Mon Apr 12 12:00:04 1982
Is DST: 0
```

:::

When you manually load a `struct tm` like that, it should be in local time. `mktime()` will convert that local time into a `time_t` calendar time.

> 当你手动加载一个 `struct tm`，它应该是本地时间。`mktime()` 将会把本地时间转换成 `time_t` 日历时间。

Weirdly, however, the standard doesn't give us a way to load up a `struct tm` with a UTC time and convert that to a `time_t`. If you want to do that with Unix-likes, try the non-standard `timegm()`. On Windows, `_mkgmtime()`.

> 然而奇怪的是，标准没有给我们一种方法来加载一个 `struct tm` 并将其转换为 `time_t`。如果你想在 Unix 类系统上这样做，请尝试非标准的 `timegm()`。在 Windows 上，`_mkgmtime()`。

## [38.4] Formatted Date Output {#formatted-date-output number="38.4"}

We've already seen a couple ways to print formatted date output to the screen. With `time_t` we can use `ctime()`, and with `struct tm` we can use `asctime()`.

> 我们已经看到了几种将格式化的日期输出到屏幕的方法。使用 `time_t`，我们可以使用 `ctime()`，使用 `struct tm` 我们可以使用 `asctime()`。

::: {#cb711 .sourceCode}

```c
time_t now = time(NULL);
struct tm *local = localtime(&now);
struct tm *utc = gmtime(&now);

printf("Local time: %s", ctime(&now));     // Local time with time_t
printf("Local time: %s", asctime(local));  // Local time with struct tm
printf("UTC       : %s", asctime(utc));    // UTC with a struct tm
```

:::

But what if I told you, dear reader, that there's a way to have much more control over how the date was printed?

> 但是如果我告诉你，亲爱的读者，有一种方法可以更好地控制日期的打印呢？

Sure, we could fish individual fields out of the `struct tm`, but there's a great function called `strftime()` that will do a lot of the hard work for you. It's like `printf()`, except for dates!

> 当然可以，我们可以从 `struct tm` 中提取单个字段，但是有一个很棒的函数叫做 `strftime()` 可以为你做很多辛苦的工作。它就像 `printf()`，只不过是针对日期！

Let's see some examples. In each of these, we pass in a destination buffer, a maximum number of characters to write, and then a format string (in the style of---but not the same as---`printf()`) which tells `strftime()` which components of a `struct tm` to print and how.

> 让我们看一些例子。在每个例子中，我们传入一个目标缓冲区，一个最大字符数，然后是一个格式字符串(以 printf()的风格，但不是相同的)，它告诉 strftime()要打印 struct tm 的哪些组件以及如何打印。

You can add other constant characters to include in the output in the format string, as well, just like with `printf()`.

> 你也可以在格式字符串中添加其他常量字符，就像使用 `printf()` 一样。

We get a `struct tm` in this case from `localtime()`, but any source works fine.

> 在这种情况下，我们从 `localtime()` 获得一个 `struct tm`，但任何来源都可以。

::: {#cb712 .sourceCode}

```c
#include <stdio.h>
#include <time.h>

int main(void)
{
    char s[128];
    time_t now = time(NULL);

    // %c: print date as per current locale
    strftime(s, sizeof s, "%c", localtime(&now));
    puts(s);   // Sun Feb 28 22:29:00 2021

    // %A: full weekday name
    // %B: full month name
    // %d: day of the month
    strftime(s, sizeof s, "%A, %B %d", localtime(&now));
    puts(s);   // Sunday, February 28

    // %I: hour (12 hour clock)
    // %M: minute
    // %S: second
    // %p: AM or PM
    strftime(s, sizeof s, "It's %I:%M:%S %p", localtime(&now));
    puts(s);   // It's 10:29:00 PM

    // %F: ISO 8601 yyyy-mm-dd
    // %T: ISO 8601 hh:mm:ss
    // %z: ISO 8601 time zone offset
    strftime(s, sizeof s, "ISO 8601: %FT%T%z", localtime(&now));
    puts(s);   // ISO 8601: 2021-02-28T22:29:00-0800
}
```

:::

There are a _ton_ of date printing format specifiers for `strftime()`, so be sure to check them out in the [`strftime()` reference page](https://beej.us/guide/bgclr/html/split/time.html#man-strftime)[^193^].

> 有很多日期打印格式规范可以用于 `strftime()`，所以一定要在[`strftime()` 参考页面](https://beej.us/guide/bgclr/html/split/time.html#man-strftime)[^193^]上查看它们。

## [38.5] More Resolution with `timespec_get()` {#more-resolution-with-timespec_get number="38.5"}

You can get the number of seconds and nanoseconds since Epoch with `timespec_get()`.

> 你可以使用 `timespec_get()` 获取自 Epoch 以来的秒数和纳秒数。

Maybe.

Implementations might not have nanosecond resolution (that's one billionth of a second) so who knows how many significant places you'll get, but give it a shot and see.

> 实现可能没有纳秒分辨率(那是一个十亿分之一秒)，所以谁知道你会得到多少有效位，但是试一试，看看吧。

`timespec_get()` takes two arguments. One is a pointer to a `struct timespec` to hold the time information. And the other is the `base`, which the spec lets you set to `TIME_UTC` indicating that you're interested in seconds since Epoch. (Other implementations might give you more options for the `base`.)

And the structure itself has two fields:

::: {#cb713 .sourceCode}

```c
struct timespec {
    time_t tv_sec;   // Seconds
    long   tv_nsec;  // Nanoseconds (billionths of a second)
};
```

:::

Here's an example where we get the time and print it out both as integer values and also a floating value:

> 这里有一个例子，我们可以获取时间，并以整数值和浮点值的形式打印出来：

::: {#cb714 .sourceCode}

```c
struct timespec ts;

timespec_get(&ts, TIME_UTC);

printf("%ld s, %ld ns\n", ts.tv_sec, ts.tv_nsec);

double float_time = ts.tv_sec + ts.tv_nsec/1000000000.0;
printf("%f seconds since epoch\n", float_time);
```

:::

Example output:

::: {#cb715 .sourceCode}

```{.sourceCode .default}
1614581530 s, 806325800 ns
1614581530.806326 seconds since epoch
```

:::

`struct timespec` also makes an appearance in a number of the threading functions that need to be able to specify time with that resolution.

## [38.6] Differences Between Times {#differences-between-times number="38.6"}

One quick note about getting the difference between two `time_t` s: since the spec doesn't dictate how that type represents a time, you might not be able to simply subtract two `time_t` s and get anything sensible[^194^].

> 一个关于获取两个 `time_t` 之间差异的快速提示：由于规范没有规定这种类型如何表示时间，您可能无法简单地减去两个 `time_t` 并获得任何有意义的结果。

Luckily you can use `difftime()` to compute the difference in seconds between two dates.

> 幸运的是，你可以使用 `difftime()` 来计算两个日期之间的秒数差异。

In the following example, we have two events that occur some time apart, and we use `difftime()` to compute the difference.

> 在下面的例子中，我们有两个发生在一段时间间隔的事件，我们使用 `difftime()` 来计算差异。

::: {#cb716 .sourceCode}

```c
#include <stdio.h>
#include <time.h>

int main(void)
{
    struct tm time_a = {
        .tm_year=82,   // years since 1900
        .tm_mon=3,     // months since January -- [0, 11]
        .tm_mday=12,   // day of the month -- [1, 31]
        .tm_hour=4,    // hours since midnight -- [0, 23]
        .tm_min=00,    // minutes after the hour -- [0, 59]
        .tm_sec=04,    // seconds after the minute -- [0, 60]
        .tm_isdst=-1,  // Daylight Saving Time flag
    };

    struct tm time_b = {
        .tm_year=120,  // years since 1900
        .tm_mon=10,    // months since January -- [0, 11]
        .tm_mday=15,   // day of the month -- [1, 31]
        .tm_hour=16,   // hours since midnight -- [0, 23]
        .tm_min=27,    // minutes after the hour -- [0, 59]
        .tm_sec=00,    // seconds after the minute -- [0, 60]
        .tm_isdst=-1,  // Daylight Saving Time flag
    };

    time_t cal_a = mktime(&time_a);
    time_t cal_b = mktime(&time_b);

    double diff = difftime(cal_b, cal_a);

    double years = diff / 60 / 60 / 24 / 365.2425;  // close enough

    printf("%f seconds (%f years) between events\n", diff, years);
}
```

:::

Output:

::: {#cb717 .sourceCode}

```{.sourceCode .default}
1217996816.000000 seconds (38.596783 years) between events
```

:::

And there you have it! Remember to use `difftime()` to take the time difference. Even though you can just subtract on a POSIX system, might as well stay portable.

> 现在你知道了！记得使用 `difftime()` 来计算时间差。尽管在 POSIX 系统上可以直接相减，但最好还是保持可移植性。

# [39] Multithreading {#multithreading number="39"}

C11 introduced, formally, multithreading to the C language. It's very eerily similar to [POSIX threads](https://en.wikipedia.org/wiki/POSIX_Threads)[^195^], if you've ever used those.

> C11 正式地将多线程引入 C 语言。如果你曾经使用过 [POSIX 线程](https://en.wikipedia.org/wiki/POSIX_Threads)[^195^]，它们非常相似。

And if you've not, no worries. We'll talk it through.

Do note, however, that I'm not intending this to be a full-blown classic multithreading how-to[^196^]; you'll have to pick up a different very thick book for that, specifically. Sorry!

> 不过，请注意，我不打算把这当作一本全面的经典多线程教程[^196^]; 您需要另外找一本很厚的书来学习，抱歉！

Threading is an optional feature. If a C11+ compiler defines `__STDC_NO_THREADS__`, threads will **not** be present in the library. Why they decided to go with a negative sense in that macro is beyond me, but there we are.

> 线程是一个可选功能。如果 C11+ 编译器定义了 `__STDC_NO_THREADS__`，线程将不会出现在库中。为什么他们决定在该宏中使用负面意义，我无法理解，但事实如此。

You can test for it like this:

::: {#cb718 .sourceCode}

```c
#ifdef __STDC_NO_THREADS__
#error I need threads to build this program!
#endif
```

:::

Also, you might need to specify certain linker options when building. In the case of Unix-likes, try appending a `-lpthreads` to the end of the command line to link the `pthreads` library[^197^]:

> 你可能需要在构建时指定某些链接器选项。在 Unix 类系统中，尝试在命令行末尾添加 `-lpthreads` 来链接 `pthreads` 库 [^197^]：

::: {#cb719 .sourceCode}

```zsh
gcc -std=c11 -o foo foo.c -lpthreads
```

:::

If you're getting linker errors on your system, it could be because the appropriate library wasn't included.

> 如果您的系统出现链接器错误，可能是因为没有包含适当的库。

## [39.1] Background {#background number="39.1"}

Threads are a way to have all those shiny CPU cores you paid for do work for you in the same program.

> 线程是一种让你花钱买的闪亮的 CPU 核心为你的程序服务的方式。

Normally, a C program just runs on a single CPU core. But if you know how to split up the work, you can give pieces of it to a number of threads and have them do the work simultaneously.

> 一般来说，C 程序只能在单个 CPU 核心上运行。但是，如果你知道如何分解工作，你可以把它的一部分分配给多个线程，让它们同时完成工作。

Though the spec doesn't say it, on your system it's very likely that C (or the OS at its behest) will attempt to balance the threads over all your CPU cores.

> 尽管规格没有说明，但在您的系统上，C(或操作系统)很可能会尝试在所有 CPU 内核上平衡线程。

And if you have more threads than cores, that's OK. You just won't realize all those gains if they're all trying to compete for CPU time.

> 如果线程比核心多，没关系。只是如果它们都在争夺 CPU 时间，你就不会实现所有的收益。

## [39.2] Things You Can Do {#things-you-can-do number="39.2"}

You can create a thread. It will begin running the function you specify. The parent thread that spawned it will also continue to run.

> 你可以创建一个线程。它将开始运行你指定的函数。产生它的父线程也将继续运行。

And you can wait for the thread to complete. This is called _joining_.

Or if you don't care when the thread completes and don't want to wait, you can _detach it_.

> 如果你不关心线程何时完成，也不想等待，你可以将它分离。

A thread can explicitly _exit_, or it can implicitly call it quits by returning from its main function.

> 一个线程可以显式地_退出_，或者它可以通过从其主函数返回来隐式地结束。

A thread can also _sleep_ for a period of time, doing nothing while other threads run.

> 一个线程也可以休眠一段时间，在其他线程运行的时候什么也不做。

The `main()` program is a thread, as well.

Additionally, we have thread local storage, mutexes, and conditional variables. But more on those later. Let's just look at the basics for now.

> 此外，我们还有线程本地存储、互斥量和条件变量。但这些我们稍后再讨论。现在先来看看基础知识吧。

## [39.3] Data Races and the Standard Library {#data-races-and-the-standard-library number="39.3"}

Some of the functions in the standard library (e.g. `asctime()` and `strtok()`) return or use `static` data elements that aren't threadsafe. But in general unless it's said otherwise, the standard library makes an effort to be so[^198^].

> 一些标准库中的函数(例如 `asctime()` 和 `strtok()`)返回或使用的静态数据元素不是线程安全的。但一般情况下，除非另有说明，标准库都会努力做到这一点。

But keep an eye out. If a standard library function is maintaining state between calls in a variable you don't own, or if a function is returning a pointer to a thing that you didn't pass in, it's not threadsafe.

> 但要留心。如果标准库函数在您不拥有的变量之间保持状态，或者如果函数返回指向您没有传入的东西的指针，那么它就不是线程安全的。

## [39.4] Creating and Waiting for Threads {#creating-and-waiting-for-threads number="39.4"}

Let's hack something up!

We'll make some threads (create) and wait for them to complete (join).

We have a tiny bit to understand first, though.

Every single thread is identified by an opaque variable of type `thrd_t`. It's a unique identifier per thread in your program. When you create a thread, it's given a new ID.

> 每个线程都由一个 `thrd_t` 类型的不透明变量标识。它是程序中每个线程的唯一标识符。当你创建一个线程时，它会被赋予一个新的 ID。

Also when you make the thread, you have to give it a pointer to a function to run, and a pointer to an argument to pass to it (or `NULL` if you don't have anything to pass).

> 当你创建线程时，你必须给它一个指向要运行的函数的指针，以及一个指向要传递给它的参数的指针(或者如果没有要传递的参数，则为 `NULL`)。

The thread will begin execution on the function you specify.

When you want to wait for a thread to complete, you have to specify its thread ID so C knows which one to wait for.

> 当你想等待一个线程完成时，你必须指定它的线程 ID，这样 C 才知道要等待哪一个。

So the basic idea is:

1. Write a function to act as the thread's "`main`". It's not `main()`-proper, but analogous to it. The thread will start running there.

> 写一个函数来作为线程的“主要”部分。这不是真正的 `main()`，但类似于它。线程将从这里开始运行。

2. From the main thread, launch a new thread with `thrd_create()`, and pass it a pointer to the function to run.

> 从主线程中，使用 `thrd_create()` 启动一个新线程，并将指向要运行的函数的指针传递给它。

3. In that function, have the thread do whatever it has to do.
4. Meantimes, the main thread can continue doing whatever _it_ has to do.
5. When the main thread decides to, it can wait for the child thread to complete by calling `thrd_join()`. Generally you **must** `thrd_join()` the thread to clean up after it or else you'll leak memory[^199^]

> 5. 主线程可以通过调用 `thrd_join()` 来等待子线程完成。一般来说，你**必须**调用 `thrd_join()` 来清理线程，否则会泄漏内存 [^199^]。

`thrd_create()` takes a pointer to the function to run, and it's of type `thrd_start_t`, which is `int (*)(void *)`. That's Greek for "a pointer to a function that takes an `void*` as an argument, and returns an `int`."

Let's make a thread! We'll launch it from the main thread with `thrd_create()` to run a function, do some other things, then wait for it to complete with `thrd_join()`. I've named the thread's main function `run()`, but you can name it anything as long as the types match `thrd_start_t`.

> 让我们创建一个线程！我们将使用 `thrd_create()` 从主线程启动它来运行一个函数，做一些其他的事情，然后使用 `thrd_join()` 等待它完成。我已经将线程的主函数命名为 `run()`，但只要类型与 `thrd_start_t` 匹配，您可以将其命名为任何内容。

::: {#cb720 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>

// This is the function the thread will run. It can be called anything.
//
// arg is the argument pointer passed to `thrd_create()`.
//
// The parent thread will get the return value back from `thrd_join()`'
// later.

int run(void *arg)
{
    int *a = arg;  // We'll pass in an int* from thrd_create()

    printf("THREAD: Running thread with arg %d\n", *a);

    return 12;  // Value to be picked up by thrd_join() (chose 12 at random)
}

int main(void)
{
    thrd_t t;  // t will hold the thread ID
    int arg = 3490;

    printf("Launching a thread\n");

    // Launch a thread to the run() function, passing a pointer to 3490
    // as an argument. Also stored the thread ID in t:

    thrd_create(&t, run, &arg);

    printf("Doing other things while the thread runs\n");

    printf("Waiting for thread to complete...\n");

    int res;  // Holds return value from the thread exit

    // Wait here for the thread to complete; store the return value
    // in res:

    thrd_join(t, &res);

    printf("Thread exited with return value %d\n", res);
}
```

:::

See how we did the `thrd_create()` there to call the `run()` function? Then we did other things in `main()` and then stopped and waited for the thread to complete with `thrd_join()`.

> 看看我们如何在那里调用 `thrd_create()` 来调用 `run()` 函数？然后我们在 `main()` 中做了其他事情，然后停止并等待线程完成 `thrd_join()`。

Sample output (yours might vary):

::: {#cb721 .sourceCode}

```{.sourceCode .default}
Launching a thread
Doing other things while the thread runs
Waiting for thread to complete...
THREAD: Running thread with arg 3490
Thread exited with return value 12
```

:::

The `arg` that you pass to the function has to have a lifetime long enough so that the thread can pick it up before it goes away. Also, it needs to not be overwritten by the main thread before the new thread can use it.

> 传递给函数的 `arg` 参数必须拥有足够长的生命周期，以便线程在它消失之前可以捕获它。此外，在新线程使用它之前，它也不能被主线程覆盖。

Let's look at an example that launches 5 threads. One thing to note here is how we use an array of `thrd_t` s to keep track of all the thread IDs.

> 让我们来看一个启动 5 个线程的例子。需要注意的是，我们使用一个 `thrd_t` 数组来跟踪所有线程 ID。

::: {#cb722 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>

int run(void *arg)
{
    int i = *(int*)arg;

    printf("THREAD %d: running!\n", i);

    return i;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    int i;

    printf("Launching threads...\n");
    for (i = 0; i < THREAD_COUNT; i++)

        // NOTE! In the following line, we pass a pointer to i,
        // but each thread sees the same pointer. So they'll
        // print out weird things as i changes value here in
        // the main thread! (More in the text, below.)

        thrd_create(t + i, run, &i);

    printf("Doing other things while the thread runs...\n");
    printf("Waiting for thread to complete...\n");

    for (int i = 0; i < THREAD_COUNT; i++) {
        int res;
        thrd_join(t[i], &res);

        printf("Thread %d complete!\n", res);
    }

    printf("All threads complete!\n");
}
```

:::

When I run the threads, I count `i` up from 0 to 4. And pass a pointer to it to `thrd_create()`. This pointer ends up in the `run()` routine where we make a copy of it.

> 当我运行线程时，我从 0 到 4 逐个计数 `i`。并将指针传递给 `thrd_create()`。这个指针最终会进入 `run()` 例程，我们在那里对它进行复制。

Simple enough? Here's the output:

::: {#cb723 .sourceCode}

```{.sourceCode .default}
Launching threads...
THREAD 2: running!
THREAD 3: running!
THREAD 4: running!
THREAD 2: running!
Doing other things while the thread runs...
Waiting for thread to complete...
Thread 2 complete!
Thread 2 complete!
THREAD 5: running!
Thread 3 complete!
Thread 4 complete!
Thread 5 complete!
All threads complete!
```

:::

Whaaa---? Where's `THREAD 0`? And why do we have a `THREAD 5` when clearly `i` is never more than `4` when we call `thrd_create()`? And two `THREAD 2` s? Madness!

> 啊？线程 0 在哪？为什么我们在调用 thrd_create()的时候 i 永远不会超过 4，却有线程 5？还有两个线程 2？疯了！

This is getting into the fun land of _race conditions_. The main thread is modifying `i` before the thread has a chance to copy it. Indeed, `i` makes it all the way to `5` and ends the loop before the last thread gets a chance to copy it.

> 这正进入竞争条件的有趣之地。主线程在线程有机会复制它之前修改了 `i`。的确，`i` 一直变成 `5`，在最后一个线程有机会复制它之前就结束了循环。

We've got to have a per-thread variable that we can refer to so we can pass it in as the `arg`.

> 我们必须有一个每个线程变量，我们可以引用它，这样我们就可以把它作为“arg”传递进去。

We could have a big array of them. Or we could `malloc()` space (and free it somewhere---maybe in the thread itself.)

> 我们可以拥有一个大型的数组。或者我们可以使用 `malloc()` 函数分配空间(并在线程本身中释放它)。

Let's give that a shot:

::: {#cb724 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

int run(void *arg)
{
    int i = *(int*)arg;  // Copy the arg

    free(arg);  // Done with this

    printf("THREAD %d: running!\n", i);

    return i;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    int i;

    printf("Launching threads...\n");
    for (i = 0; i < THREAD_COUNT; i++) {

        // Get some space for a per-thread argument:

        int *arg = malloc(sizeof *arg);
        *arg = i;

        thrd_create(t + i, run, arg);
    }

    // ...
```

:::

Notice on lines 27-30 we `malloc()` space for an `int` and copy the value of `i` into it. Each new thread gets its own freshly-`malloc()` d variable and we pass a pointer to that to the `run()` function.

> 在 27-30 行，我们为一个 int 变量分配 malloc()空间，并将 i 的值复制到其中。每个新线程都有自己新分配的 malloc()变量，我们将指向该变量的指针传递给 run()函数。

Once `run()` makes its own copy of the `arg` on line 7, it `free()` s the `malloc()` d `int`. And now that it has its own copy, it can do with it what it pleases.

> 一旦 `run()` 在第 7 行上制作了它自己的 `arg` 副本，它就会 `free()` `malloc()` 的 `int`。现在它有了自己的副本，它可以随意处理它。

And a run shows the result:

::: {#cb725 .sourceCode}

```{.sourceCode .default}
Launching threads...
THREAD 0: running!
THREAD 1: running!
THREAD 2: running!
THREAD 3: running!
Doing other things while the thread runs...
Waiting for thread to complete...
Thread 0 complete!
Thread 1 complete!
Thread 2 complete!
Thread 3 complete!
THREAD 4: running!
Thread 4 complete!
All threads complete!
```

:::

There we go! Threads 0-4 all in effect!

Your run might vary---how the threads get scheduled to run is beyond the C spec. We see in the above example that thread 4 didn't even begin until threads 0-1 had completed. Indeed, if I run this again, I likely get different output. We cannot guarantee a thread execution order.

> 你的运行可能会有所不同---线程被调度运行的方式超出了 C 规范。我们在上面的例子中看到，线程 4 甚至都没有开始，直到线程 0-1 完成了。事实上，如果我再次运行这个程序，可能会得到不同的输出。我们不能保证线程的执行顺序。

## [39.5] Detaching Threads {#detaching-threads number="39.5"}

If you want to fire-and-forget a thread (i.e. so you don't have to `thrd_join()` it later), you can do that with `thrd_detach()`.

> 如果你想要一个可以"fire-and-forget"的线程(即不需要稍后 `thrd_join()` 它)，你可以使用 `thrd_detach()` 来实现。

This removes the parent thread's ability to get the return value from the child thread, but if you don't care about that and just want threads to clean up nicely on their own, this is the way to go.

> 这会移除父线程从子线程获取返回值的能力，但如果你不关心这一点，只想让线程自己干净地清理，那么这是一条正确的路径。

Basically we're going to do this:

::: {#cb726 .sourceCode}

```c
thrd_create(&t, run, NULL);
thrd_detach(t);
```

:::

where the `thrd_detach()` call is the parent thread saying, "Hey, I'm not going to wait for this child thread to complete with `thrd_join()`. So go ahead and clean it up on your own when it completes."

> 在 `thrd_detach()` 调用处，父线程正在说：“嘿，我不会等待这个子线程完成 `thrd_join()`。所以，当它完成时，请自行清理它。”

::: {#cb727 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>

int run(void *arg)
{
    (void)arg;

    //printf("Thread running! %lu\n", thrd_current()); // non-portable!
    printf("Thread running!\n");

    return 0;
}

#define THREAD_COUNT 10

int main(void)
{
    thrd_t t;

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_create(&t, run, NULL);
        thrd_detach(t);               // <-- DETACH!
    }

    // Sleep for a second to let all the threads finish
    thrd_sleep(&(struct timespec){.tv_sec=1}, NULL);
}
```

:::

Note that in this code, we put the main thread to sleep for 1 second with `thrd_sleep()`---more on that later.

> 在这段代码中，我们使用 `thrd_sleep()` 让主线程睡眠 1 秒钟，稍后会有更多介绍。

Also in the `run()` function, I have a commented-out line in there that prints out the thread ID as an `unsigned long`. This is non-portable, because the spec doesn't say what type a `thrd_t` is under the hood---it could be a `struct` for all we know. But that line works on my system.

> 在 `run()` 函数中，我有一行被注释掉的代码，它将线程 ID 打印为 `unsigned long`。这是不可移植的，因为规范没有说明 `thrd_t` 背后是什么类型---它可能是一个 `struct`。但是这行代码在我的系统上可以正常工作。

Something interesting I saw when I ran the code, above, and printed out the thread IDs was that some threads had duplicate IDs! This seems like it should be impossible, but C is allowed to _reuse_ thread IDs after the corresponding thread has exited. So what I was seeing was that some threads completed their run before other threads were launched.

> 当我运行上面的代码并打印出线程 ID 时，我看到一些有趣的东西，有些线程有重复的 ID！这似乎不可能，但 C 允许在相应的线程退出后_重用_线程 ID。因此，我所看到的是，一些线程在其他线程启动之前完成了运行。

## [39.6] Thread Local Data {#thread-local-data number="39.6"}

Threads are interesting because they don't have their own memory beyond local variables. If you want a `static` variable or file scope variable, all threads will see that same variable.

> 线程很有趣，因为它们除了局部变量之外没有自己的内存。如果你想要一个 `静态` 变量或文件范围变量，所有线程都将看到相同的变量。

This can lead to race conditions, where you get *Weird Things*™ happening.

> 这可能会导致竞争条件，使你遇到奇怪的事情 ™。

Check out this example. We have a `static` variable `foo` in block scope in `run()`. This variable will be visible to all threads that pass through the `run()` function. And the various threads can effectively step on each others toes.

> 查看这个例子。我们在 `run()` 中有一个块作用域中的 `静态` 变量 `foo`。这个变量将对所有通过 `run()` 函数的线程可见。各种线程可以有效地互相干扰。

Each thread copies `foo` into a local variable `x` (which is not shared between threads---all the threads have their own call stacks). So they _should_ be the same, right?

> 每个线程都会将 `foo` 复制到本地变量 `x`(不会在线程之间共享---所有线程都有自己的调用堆栈)。所以它们应该是相同的，对吗？

And the first time we print them, they are[^200^]. But then right after that, we check to make sure they're still the same.

> 第一次打印它们时，它们是[^200^]。但是接着，我们检查一下确保它们仍然是一样的。

And they _usually_ are. But not always!

::: {#cb728 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

int run(void *arg)
{
    int n = *(int*)arg;  // Thread number for humans to differentiate

    free(arg);

    static int foo = 10;  // Static value shared between threads

    int x = foo;  // Automatic local variable--each thread has its own

    // We just assigned x from foo, so they'd better be equal here.
    // (In all my test runs, they were, but even this isn't guaranteed!)

    printf("Thread %d: x = %d, foo = %d\n", n, x, foo);

    // And they should be equal here, but they're not always!
    // (Sometimes they were, sometimes they weren't!)

    // What happens is another thread gets in and increments foo
    // right now, but this thread's x remains what it was before!

    if (x != foo) {
        printf("Thread %d: Craziness! x != foo! %d != %d\n", n, x, foo);
    }

    foo++;  // Increment shared value

    return 0;
}

#define THREAD_COUNT 5

int main(void)
{
    thrd_t t[THREAD_COUNT];

    for (int i = 0; i < THREAD_COUNT; i++) {
        int *n = malloc(sizeof *n);  // Holds a thread serial number
        *n = i;
        thrd_create(t + i, run, n);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }
}
```

:::

Here's an example output (though this varies from run to run):

::: {#cb729 .sourceCode}

```{.sourceCode .default}
Thread 0: x = 10, foo = 10
Thread 1: x = 10, foo = 10
Thread 1: Craziness! x != foo! 10 != 11
Thread 2: x = 12, foo = 12
Thread 4: x = 13, foo = 13
Thread 3: x = 14, foo = 14
```

:::

In thread 1, between the two `printf()` s, the value of `foo` somehow changed from `10` to `11`, even though clearly there's no increment between the `printf()` s!

> 在线程 1 中，在两个 printf()之间，foo 的值从 10 变成了 11，尽管明显没有在 printf()之间增加！

It was another thread that got in there (probably thread 0, from the look of it) and incremented the value of `foo` behind thread 1's back!

> 这是另一条线程进入那里(看起来可能是线程 0)，在线程 1 背后增加了 `foo` 的值！

Let's solve this problem two different ways. (If you want all the threads to share the variable _and_ not step on each other's toes, you'll have to read on to the [mutex](#mutex) section.)

> 让我们用两种不同的方式来解决这个问题。(如果你想让所有的线程共享变量，而又不会相互干扰，你就得继续阅读[互斥](#互斥)部分)

### [39.6.1] `_Thread_local` Storage-Class {#thread-local number="39.6.1"}

First things first, let's just look at the easy way around this: the `_Thread_local` storage-class.

> 首先，让我们看看这个简单的方式：`_Thread_local` 存储类。

Basically we're just going to slap this on the front of our block scope `static` variable and things will work! It tells C that every thread should have its own version of this variable, so none of them step on each other's toes.

> 基本上，我们只需要在我们的块作用域变量前面加上 `static`，就可以让它们正常工作！它告诉 C，每个线程都应该有自己的变量版本，这样就不会互相干扰了。

The `<threads.h>` header defines `thread_local` as an alias to `_Thread_local` so your code doesn't have to look so ugly.

> <threads.h> 头文件将 thread_local 定义为_Thread_local 的别名，因此您的代码看起来不那么难看。

Let's take the previous example and make `foo` into a `thread_local` variable so that we don't share that data.

> 让我们以前面的例子为例，将 `foo` 变成一个 `thread_local` 变量，这样我们就不会共享数据了。

::: {#cb730 .sourceCode startfrom="5"}

```c
int run(void *arg)
{
    int n = *(int*)arg;  // Thread number for humans to differentiate

    free(arg);

    thread_local static int foo = 10;  // <-- No longer shared!!
```

:::

And running we get:

::: {#cb731 .sourceCode}

```{.sourceCode .default}
Thread 0: x = 10, foo = 10
Thread 1: x = 10, foo = 10
Thread 2: x = 10, foo = 10
Thread 4: x = 10, foo = 10
Thread 3: x = 10, foo = 10
```

:::

No more weird problems!

One thing: if a `thread_local` variable is block scope, it **must** be `static`. Them's the rules. (But this is OK because non-`static` variables are per-thread already since each thread has it's own non-`static` variables.)

> 一件事：如果一个 `thread_local` 变量是块作用域，它**必须**是 `static` 的。这就是规则。(但这是可以的，因为非 `static` 变量已经是每个线程的了，因为每个线程都有自己的非 `static` 变量。)

A bit of a lie there: block scope `thread_local` variables can also be `extern`.

> 这里有点谎言：块作用域的 `thread_local` 变量也可以是 `extern` 的。

### [39.6.2] Another Option: Thread-Specific Storage {#another-option-thread-specific-storage number="39.6.2"}

Thread-specific storage (TSS) is another way of getting per-thread data.

One additional feature is that these functions allow you to specify a destructor that will be called on the data when the TSS variable is deleted. Commonly this destructor is `free()` to automatically clean up `malloc()` d per-thread data. Or `NULL` if you don't need to destroy anything.

> 除此之外，这些函数还允许您指定一个析构函数，当 TSS 变量被删除时，该析构函数将被调用。通常，这个析构函数是 `free()`，以自动清理 `malloc()` d 的每个线程数据。或者如果您不需要销毁任何东西，则为 `NULL`。

The destructor is type `tss_dtor_t` which is a pointer to a function that returns `void` and takes a `void*` as an argument (the `void*` points to the data stored in the variable). In other words, it's a `void (*)(void*)`, if that clears it up. Which I admit it probably doesn't. Check out the example, below.

> 析构函数的类型是 `tss_dtor_t`，它是一个指向返回 `void` 并带有 `void*` 作为参数的函数的指针(`void*` 指向变量中存储的数据)。换句话说，它是一个 `void (*)(void*)`，如果这让你弄清楚了就好了。我承认它可能不会。请查看下面的示例。

Generally, `thread_local` is probably your go-to, but if you like the destructor idea, then you can make use of that.

> 一般来说，`thread_local` 可能是你的首选，但如果你喜欢析构函数的想法，那么你可以利用它。

The usage is a bit weird in that we need a variable of type `tss_t` to be alive to represent the value on a per thread basis. Then we initialize it with `tss_create()`. Eventually we get rid of it with `tss_delete()`. Note that calling `tss_delete()` doesn't run all the destructors---it's `thrd_exit()` (or returning from the run function) that does that. `tss_delete()` just releases any memory allocated by `tss_create()`.

> 使用方法有点奇怪，我们需要一个类型为'tss_t'的变量来代表每个线程的值。然后我们用'tss_create()'来初始化它。最后，我们用'tss_delete()'来摆脱它。注意，调用'tss_delete()'不会运行所有析构函数---只有'thrd_exit()'(或从运行函数返回)才能做到这一点。 'tss_delete()'只是释放'tss_create()'分配的任何内存。

In the middle, threads can call `tss_set()` and `tss_get()` to set and get the value.

> 在中间，线程可以调用 `tss_set()` 和 `tss_get()` 来设置和获取值。

In the following code, we set up the TSS variable before creating the threads, then clean up after the threads.

> 在下面的代码中，我们在创建线程之前设置 TSS 变量，然后在线程结束后清理。

In the `run()` function, the threads `malloc()` some space for a string and store that pointer in the TSS variable.

> 在 `run()` 函数中，线程会为字符串分配一些空间，并将指针存储在 TSS 变量中。

When the thread exits, the destructor function (`free()` in this case) is called for _all_ the threads.

> 当线程退出时，析构函数(在这种情况下是 `free()`)将被所有线程调用。

::: {#cb732 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

tss_t str;

void some_function(void)
{
    // Retrieve the per-thread value of this string
    char *tss_string = tss_get(str);

    // And print it
    printf("TSS string: %s\n", tss_string);
}

int run(void *arg)
{
    int serial = *(int*)arg;  // Get this thread's serial number
    free(arg);

    // malloc() space to hold the data for this thread
    char *s = malloc(64);
    sprintf(s, "thread %d! :)", serial);  // Happy little string

    // Set this TSS variable to point at the string
    tss_set(str, s);

    // Call a function that will get the variable
    some_function();

    return 0;   // Equivalent to thrd_exit(0)
}

#define THREAD_COUNT 15

int main(void)
{
    thrd_t t[THREAD_COUNT];

    // Make a new TSS variable, the free() function is the destructor
    tss_create(&str, free);

    for (int i = 0; i < THREAD_COUNT; i++) {
        int *n = malloc(sizeof *n);  // Holds a thread serial number
        *n = i;
        thrd_create(t + i, run, n);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }

    // All threads are done, so we're done with this
    tss_delete(str);
}
```

:::

Again, this is kind of a painful way of doing things compared to `thread_local`, so unless you really need that destructor functionality, I'd use that instead.

> 再次，与 `thread_local` 相比，这是一种痛苦的方式，所以除非你真的需要析构函数功能，否则我会使用它。

## [39.7] Mutexes {#mutex number="39.7"}

If you want to only allow a single thread into a critical section of code at a time, you can protect that section with a mutex[^201^].

> 如果你只想让一个线程进入代码的关键部分，你可以用互斥量来保护这一部分 [^201^]。

For example, if we had a `static` variable and we wanted to be able to get and set it in two operations without another thread jumping in the middle and corrupting it, we could use a mutex for that.

> 例如，如果我们有一个 `静态` 变量，我们希望能够在两个操作中获取和设置它，而不让另一个线程插入并破坏它，我们可以使用互斥锁来实现。

You can acquire a mutex or release it. If you attempt to acquire the mutex and succeed, you may continue execution. If you attempt and fail (because someone else holds it), you will _block_[^202^] until the mutex is released.

> 你可以获取一个互斥锁或释放它。如果你尝试获取互斥锁并成功，你可以继续执行。如果你尝试失败(因为别人持有它)，你将_阻塞_[^202^] 直到互斥锁被释放。

If multiple threads are blocked waiting for a mutex to be released, one of them will be chosen to run (at random, from our perspective), and the others will continue to sleep.

> 如果多个线程被阻塞等待一个互斥量被释放，其中一个将被随机选择运行(从我们的角度来看)，其他线程将继续睡眠。

The gameplan is that first we'll initialize a mutex variable to make it ready to use with `mtx_init()`.

> 计划是首先我们将使用 `mtx_init()` 初始化一个互斥变量以准备使用。

Then subsequent threads can call `mtx_lock()` and `mtx_unlock()` to get and release the mutex.

> 随后的线程可以调用 `mtx_lock()` 和 `mtx_unlock()` 来获取和释放互斥量。

When we're completely done with the mutex, we can destroy it with `mtx_destroy()`, the logical opposite of `mtx_init()`.

> 当我们完全完成互斥量操作后，我们可以使用 `mtx_destroy()` 销毁它，这是 `mtx_init()` 的逻辑反操作。

First, let's look at some code that does _not_ use a mutex, and endeavors to print out a shared (`static`) serial number and then increment it. Because we're not using a mutex over the getting of the value (to print it) and the setting (to increment it), threads might get in each other's way in that critical section.

> 首先，让我们看看一些没有使用互斥量的代码，并努力打印出一个共享(`静态`)的序列号，然后将其递增。由于我们没有在获取值(打印它)和设置(递增它)时使用互斥量，线程可能会在关键部分彼此干扰。

::: {#cb733 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>

int run(void *arg)
{
    (void)arg;

    static int serial = 0;   // Shared static variable!

    printf("Thread running! %d\n", serial);

    serial++;

    return 0;
}

#define THREAD_COUNT 10

int main(void)
{
    thrd_t t[THREAD_COUNT];

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_create(t + i, run, NULL);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }
}
```

:::

When I run this, I get something that looks like this:

::: {#cb734 .sourceCode}

```{.sourceCode .default}
Thread running! 0
Thread running! 0
Thread running! 0
Thread running! 3
Thread running! 4
Thread running! 5
Thread running! 6
Thread running! 7
Thread running! 8
Thread running! 9
```

:::

Clearly multiple threads are getting in there and running the `printf()` before anyone gets a change to update the `serial` variable.

> 显然，多个线程正在进入并在任何人有机会更新 `serial` 变量之前运行 `printf()`。

What we want to do is wrap the getting of the variable and setting of it into a single mutex-protected stretch of code.

> 我们想要做的是将变量的获取和设置封装到一个使用互斥锁保护的代码段中。

We'll add a new variable to represent the mutex of type `mtx_t` in file scope, initialize it, and then the threads can lock and unlock it in the `run()` function.

> 我们将在文件作用域中添加一个新的变量来表示类型为 `mtx_t` 的互斥量，对它进行初始化，然后线程可以在 `run()` 函数中对它进行锁定和解锁。

::: {#cb735 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>

mtx_t serial_mtx;     // <-- MUTEX VARIABLE

int run(void *arg)
{
    (void)arg;

    static int serial = 0;   // Shared static variable!

    // Acquire the mutex--all threads will block on this call until
    // they get the lock:

    mtx_lock(&serial_mtx);           // <-- ACQUIRE MUTEX

    printf("Thread running! %d\n", serial);

    serial++;

    // Done getting and setting the data, so free the lock. This will
    // unblock threads on the mtx_lock() call:

    mtx_unlock(&serial_mtx);         // <-- RELEASE MUTEX

    return 0;
}

#define THREAD_COUNT 10

int main(void)
{
    thrd_t t[THREAD_COUNT];

    // Initialize the mutex variable, indicating this is a normal
    // no-frills, mutex:

    mtx_init(&serial_mtx, mtx_plain);        // <-- CREATE MUTEX

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_create(t + i, run, NULL);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }

    // Done with the mutex, destroy it:

    mtx_destroy(&serial_mtx);                // <-- DESTROY MUTEX
}
```

:::

See how on lines 38 and 50 of `main()` we initialize and destroy the mutex.

> 在 main()的第 38 行和第 50 行，我们可以看到如何初始化和销毁互斥量。

But each individual thread acquires the mutex on line 15 and releases it on line 24.

> 但是每个线程在第 15 行获取互斥锁，并在第 24 行释放它。

In between the `mtx_lock()` and `mtx_unlock()` is the _critical section_, the area of code where we don't want multiple threads mucking about at the same time.

> 在 `mtx_lock()` 和 `mtx_unlock()` 之间是_临界区_，这是我们不希望多个线程同时混乱的代码区域。

And now we get proper output!

::: {#cb736 .sourceCode}

```{.sourceCode .default}
Thread running! 0
Thread running! 1
Thread running! 2
Thread running! 3
Thread running! 4
Thread running! 5
Thread running! 6
Thread running! 7
Thread running! 8
Thread running! 9
```

:::

If you need multiple mutexes, no problem: just have multiple mutex variables.

> 如果你需要多个互斥量，没问题：只需要多个互斥变量即可。

And always remember the Number One Rule of Multiple Mutexes: _Unlock mutexes in the opposite order in which you lock them!_

> 记住多个互斥锁的第一条规则：按照你加锁的相反顺序解锁它们！

### [39.7.1] Different Mutex Types {#different-mutex-types number="39.7.1"}

As hinted earlier, we have a few mutex types that you can create with `mtx_init()`. (Some of these types are the result of a bitwise-OR operation, as noted in the table.)

> 正如之前暗示的，您可以使用 `mtx_init()` 创建几种互斥类型。 (其中一些类型是位或操作的结果，如表中所示。)

---

Type Description

---

`mtx_plain` Regular ol' mutex

`mtx_timed` Mutex that supports timeouts

`mtx_plain|mtx_recursive` Recursive mutex

## `mtx_timed|mtx_recursive` Recursive mutex that supports timeouts

"Recursive" means that the holder of a lock can call `mtx_lock()` multiple times on the same lock. (They have to unlock it an equal number of times before anyone else can take the mutex.) This might ease coding from time to time, especially if you call a function that needs to lock the mutex when you already hold the mutex.

> "递归"意味着持有锁的人可以在同一锁上多次调用 mtx_lock()。 (他们必须在其他人可以获得互斥体之前相等数量地解锁它。)这可能会不时地简化编码，特别是当您已经持有互斥体时调用需要锁定互斥体的函数。

And the timeout gives a thread a chance to _try_ to get the lock for a while, but then bail out if it can't get it in that timeframe.

> 等待时间给线程一个机会尝试获取锁，但如果在该时间段内无法获取，则退出。

For a timeout mutex, be sure to create it with `mtx_timed`:

::: {#cb737 .sourceCode}

```c
mtx_init(&serial_mtx, mtx_timed);
```

:::

And then when you wait for it, you have to specify a time in UTC when it will unlock[^203^].

> 然后当你等待它时，你必须指定一个 UTC 时间，它将解锁。

The function `timespec_get()` from `<time.h>` can be of assistance here. It'll get you the current time in UTC in a `struct timespec` which is just what we need. In fact, it seems to exist merely for this purpose.

> `<time.h>` 中的 `timespec_get()` 函数可以在这里提供帮助。它可以以 `struct timespec` 的形式获取当前的 UTC 时间，这正是我们所需要的。事实上，它似乎只是为了这个目的而存在的。

It has two fields: `tv_sec` has the current time in seconds since epoch, and `tv_nsec` has the nanoseconds (billionths of a second) as the "fractional" part.

> 它有两个字段：`tv_sec` 自 epoch 以来的当前时间以秒计，`tv_nsec` 有纳秒(十亿分之一秒)作为“分数”部分。

So you can load that up with the current time, and then add to it to get a specific timeout.

> 你可以用当前时间加载它，然后添加它以获得特定的超时。

Then call `mtx_timedlock()` instead of `mtx_lock()`. If it returns the value `thrd_timedout`, it timed out.

> 然后调用 `mtx_timedlock()` 而不是 `mtx_lock()`。如果它返回值 `thrd_timedout`，则超时了。

::: {#cb738 .sourceCode}

```c
struct timespec timeout;

timespec_get(&timeout, TIME_UTC);  // Get current time
timeout.tv_sec += 1;               // Timeout 1 second after now

int result = mtx_timedlock(&serial_mtx, &timeout));

if (result == thrd_timedout) {
    printf("Mutex lock timed out!\n");
}
```

:::

Other than that, timed locks are the same as regular locks.

## [39.8] Condition Variables {#condition-variables number="39.8"}

Condition Variables are the last piece of the puzzle we need to make performant multithreaded applications and to compose more complex multithreaded structures.

> 条件变量是我们需要制作高性能多线程应用程序和组合更复杂的多线程结构的最后一块拼图。

A condition variable provides a way for threads to go to sleep until some event on another thread occurs.

> 一个条件变量提供了一种方式，让线程睡眠直到另一个线程发生某些事件。

In other words, we might have a number of threads that are rearing to go, but they have to wait until some event is true before they continue. Basically they're being told "wait for it!" until they get notified.

> 换句话说，我们可能有许多线程准备就绪，但它们必须等到某些事件发生后才能继续。基本上它们被告知“等着吧！”直到它们得到通知。

And this works hand-in-hand with mutexes since what we're going to wait on generally depends on the value of some data, and that data generally needs to be protected by a mutex.

> 这与互斥量是密切相关的，因为我们通常要等待的依赖于某些数据的值，而这些数据通常需要由互斥量来保护。

It's important to note that the condition variable itself isn't the holder of any particular data from our perspective. It's merely the variable by which C keeps track of the waiting/not-waiting status of a particular thread or group of threads.

> 重要的是要注意，从我们的角度来看，条件变量本身并不是任何特定数据的持有者。它仅仅是 C 用来跟踪特定线程或线程组等待/不等待状态的变量。

Let's write a contrived program that reads in groups of 5 numbers from the main thread one at a time. Then, when 5 numbers have been entered, the child thread wakes up, sums up those 5 numbers, and prints the result.

> 让我们编写一个程序，从主线程一次读取 5 个数字的组。然后，当输入 5 个数字时，子线程唤醒，将这 5 个数字相加，并打印结果。

The numbers will be stored in a global, shared array, as will the index into the array of the about-to-be-entered number.

> 数字将存储在一个全局共享数组中，即将要输入的数字的数组索引也将如此。

Since these are shared values, we at least have to hide them behind a mutex for both the main and child threads. (The main will be writing data to them and the child will be reading data from them.)

> 由于这些是共享的值，我们至少必须为主线程和子线程之间放置一个互斥锁。(主线程将向其中写入数据，子线程将从其中读取数据。)

But that's not enough. The child thread needs to block ("sleep") until 5 numbers have been read into the array. And then the parent thread needs to wake up the child thread so it can do its work.

> 但这还不够。子线程需要阻塞(“睡眠”)，直到数组中读取了 5 个数字。然后，父线程需要唤醒子线程，让它可以完成工作。

And when it wakes up, it needs to be holding that mutex. And it will! When a thread waits on a condition variable, it also acquires a mutex when it wakes up.

> 当它醒来时，它需要持有互斥量。它会的！当一个线程等待一个条件变量时，它也会在醒来时获得一个互斥量。

All this takes place around an additional variable of type `cnd_t` that is the _condition variable_. We create this variable with the `cnd_init()` function and destroy it when we're done with it with the `cnd_destroy()` function.

> 所有这些都发生在一个额外的类型为 `cnd_t` 的变量周围，这是条件变量。我们使用 `cnd_init()` 函数创建这个变量，当我们完成时使用 `cnd_destroy()` 函数销毁它。

But how's this all work? Let's look at the outline of what the child thread will do:

> 但是这一切如何工作？让我们看一下子线程将要做什么的概要：

1. Lock the mutex with `mtx_lock()`
2. If we haven't entered all the numbers, wait on the condition variable with `cnd_wait()`

> 如果我们还没有输入所有的数字，用 `cnd_wait()` 函数等待条件变量。

3. Do the work that needs doing
4. Unlock the mutex with `mtx_unlock()`

Meanwhile the main thread will be doing this:

1. Lock the mutex with `mtx_lock()`
2. Store the recently-read number into the array
3. If the array is full, signal the child to wake up with `cnd_signal()`
4. Unlock the mutex with `mtx_unlock()`

If you didn't skim that too hard (it's OK---I'm not offended), you might notice something weird: how can the main thread hold the mutex lock and signal the child, if the child has to hold the mutex lock to wait for the signal? They can't both hold the lock!

> 如果你没有太过分地浏览(没关系---我没有受到冒犯)，你可能会注意到一些奇怪的事情：主线程如何能够持有互斥锁并向子线程发出信号，如果子线程必须持有互斥锁来等待信号呢？它们不可能同时持有锁！

And indeed they don't! There's some behind-the-scenes magic with condition variables: when you `cnd_wait()`, it releases the mutex that you specify and the thread goes to sleep. And when someone signals that thread to wake up, it reacquires the lock as if nothing had happened.

> 他们的确没有！有一些条件变量的幕后魔法：当你调用 `cnd_wait()` 时，它会释放你指定的互斥锁，线程就会睡眠。当有人发出信号让该线程唤醒时，它会重新获取锁，就好像什么都没发生过一样。

It's a little different on the `cnd_signal()` side of things. This doesn't do anything with the mutex. The signaling thread still must manually release the mutex before the waiting threads can wake up.

> 在 `cnd_signal()` 方面有些不同。它不会和互斥量做任何事情。发信号的线程仍然必须在等待线程唤醒之前手动释放互斥量。

One more thing on the `cnd_wait()`. You'll probably be calling `cnd_wait()` if some condition[^204^] is not yet met (e.g. in this case, if not all the numbers have yet been entered). Here's the deal: this condition should be in a `while` loop, not an `if` statement. Why?

> 再说一件关于 `cnd_wait()` 的事情。如果某些条件 [^204^]尚未满足(例如，在本例中，如果还没有输入所有数字)，您可能会调用 `cnd_wait()`。事情是这样的：此条件应放在 `while` 循环中，而不是 `if` 语句中。为什么？

It's because of a mysterious phenomenon called a _spurious wakeup_. Sometimes, in some implementations, a thread can be woken up out of a `cnd_wait()` sleep for seemingly _no reason_. _\[X-Files music\]_[^205^]. And so we have to check to see that the condition we need is still actually met when we wake up. And if it's not, back to sleep with us!

> 这是因为一种神秘的现象，称为虚假唤醒[^205^](#fn205)。有时，在某些实现中，线程可以从 `cnd_wait()` 睡眠中被唤醒，似乎没有原因。\[X-Files 音乐\]。因此，我们必须检查我们需要的条件在我们醒来时仍然有效。如果不是，我们就睡觉吧！

So let's do this thing! Starting with the main thread:

- The main thread will set up the mutex and condition variable, and will launch the child thread.
- Then it will, in an infinite loop, get numbers as input from the console.
- It will also acquire the mutex to store the inputted number into a global array.
- When the array has 5 numbers in it, the main thread will signal the child thread that it's time to wake up and do its work.

> 当数组中有 5 个数字时，主线程将向子线程发出信号，表示是时候唤醒它并开始工作了。

- Then the main thread will unlock the mutex and go back to reading the next number from the console.

> 然后主线程将解锁互斥量，然后回到从控制台读取下一个数字。

Meanwhile, the child thread has been up to its own shenanigans:

- The child thread grabs the mutex
- While the condition is not met (i.e. while the shared array doesn't yet have 5 numbers in it), the child thread sleeps by waiting on the condition variable. When it waits, it implicitly unlocks the mutex.

> 当条件未满足(即共享数组中的数字还不足 5 个)时，子线程通过等待条件变量来休眠。当它等待时，它会隐式地解锁互斥量。

- Once the main thread signals the child thread to wake up, it wakes up to do the work and gets the mutex lock back.

> 一旦主线程发出信号让子线程唤醒，它就会醒来完成工作并重新获得互斥锁。

- The child thread sums the numbers and resets the variable that is the index into the array.
- It then releases the mutex and runs again in an infinite loop.

And here's the code! Give it some study so you can see where all the above pieces are being handled:

> 这里是代码！仔细研究一下，你就能看到上面的所有部分都是如何处理的：

::: {#cb739 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>

#define VALUE_COUNT_MAX 5

int value[VALUE_COUNT_MAX];  // Shared global
int value_count = 0;   // Shared global, too

mtx_t value_mtx;   // Mutex around value
cnd_t value_cnd;   // Condition variable on value

int run(void *arg)
{
    (void)arg;

    for (;;) {
        mtx_lock(&value_mtx);      // <-- GRAB THE MUTEX

        while (value_count < VALUE_COUNT_MAX) {
            printf("Thread: is waiting\n");
            cnd_wait(&value_cnd, &value_mtx);  // <-- CONDITION WAIT
        }

        printf("Thread: is awake!\n");

        int t = 0;

        // Add everything up
        for (int i = 0; i < VALUE_COUNT_MAX; i++)
            t += value[i];

        printf("Thread: total is %d\n", t);

        // Reset input index for main thread
        value_count = 0;

        mtx_unlock(&value_mtx);   // <-- MUTEX UNLOCK
    }

    return 0;
}

int main(void)
{
    thrd_t t;

    // Spawn a new thread

    thrd_create(&t, run, NULL);
    thrd_detach(t);

    // Set up the mutex and condition variable

    mtx_init(&value_mtx, mtx_plain);
    cnd_init(&value_cnd);

    for (;;) {
        int n;

        scanf("%d", &n);

        mtx_lock(&value_mtx);    // <-- LOCK MUTEX

        value[value_count++] = n;

        if (value_count == VALUE_COUNT_MAX) {
            printf("Main: signaling thread\n");
            cnd_signal(&value_cnd);  // <-- SIGNAL CONDITION
        }

        mtx_unlock(&value_mtx);  // <-- UNLOCK MUTEX
    }

    // Clean up (I know that's an infinite loop above here, but I
    // want to at least pretend to be proper):

    mtx_destroy(&value_mtx);
    cnd_destroy(&value_cnd);
}
```

:::

And here's some sample output (individual numbers on lines are my input):

::: {#cb740 .sourceCode}

```{.sourceCode .default}
Thread: is waiting
1
1
1
1
1
Main: signaling thread
Thread: is awake!
Thread: total is 5
Thread: is waiting
2
8
5
9
0
Main: signaling thread
Thread: is awake!
Thread: total is 24
Thread: is waiting
```

:::

It's a common use of condition variables in producer-consumer situations like this. If we didn't have a way to put the child thread to sleep while it waited for some condition to be met, it would be force to poll which is a big waste of CPU.

> 这在生产者-消费者情况下是一种常见的使用条件变量的方式。如果我们没有办法让子线程在等待某些条件满足时休眠，它将被迫轮询，这是一种巨大的 CPU 浪费。

### [39.8.1] Timed Condition Wait {#timed-condition-wait number="39.8.1"}

There's a variant of `cnd_wait()` that allows you to specify a timeout so you can stop waiting.

> 有一种 `cnd_wait()` 的变体，可以让你指定一个超时时间，以便你停止等待。

Since the child thread must relock the mutex, this doesn't necessarily mean that you'll be popping back to life the instant the timeout occurs; you still must wait for any other threads to release the mutex.

> 由于子线程必须重新锁定互斥量，这并不一定意味着超时发生时你就会马上复活；你仍然必须等待其他线程释放互斥量。

But it does mean that you won't be waiting until the `cnd_signal()` happens.

> 但这并不意味着你不用等待直到 `cnd_signal()` 发生。

To make this work, call `cnd_timedwait()` instead of `cnd_wait()`. If it returns the value `thrd_timedout`, it timed out.

> 要让这个工作，请调用 `cnd_timedwait()` 而不是 `cnd_wait()`。如果它返回值 `thrd_timedout`，则超时了。

The timestamp is an absolute time in UTC, not a time-from-now. Thankfully the `timespec_get()` function in `<time.h>` seems custom-made for exactly this case.

> 时间戳是一个 UTC 的绝对时间，而不是从现在开始的时间。幸运的是，<time.h> 中的 timespec_get()函数似乎专门为这种情况而设计。

::: {#cb741 .sourceCode}

```c
struct timespec timeout;

timespec_get(&timeout, TIME_UTC);  // Get current time
timeout.tv_sec += 1;               // Timeout 1 second after now

int result = cnd_timedwait(&condition, &mutex, &timeout));

if (result == thrd_timedout) {
    printf("Condition variable timed out!\n");
}
```

:::

### [39.8.2] Broadcast: Wake Up All Waiting Threads {#broadcast-wake-up-all-waiting-threads number="39.8.2"}

`cnd_signal()` function\]\] `cnd_signal()` only wakes up one thread to continue working. Depending on how you have your logic done, it might make sense to wake up more than one thread to continue once the condition is met.

Of course only one of them can grab the mutex, but if you have a situation where:

> 当然只有一个人能抢到互斥锁，但如果你有这样的情况：

- The newly-awoken thread is responsible for waking up the next one, and---
- There's a chance the spurious-wakeup loop condition will prevent it from doing so, then---

you'll want to broadcast the wake up so that you're sure to get at least one of the threads out of that loop to launch the next one.

> 你需要广播唤醒，以确保至少有一个线程从循环中脱离出来，以启动下一个线程。

How, you ask?

Simply use `cnd_broadcast()` instead of `cnd_signal()`. Exact same usage, except `cnd_broadcast()` wakes up **all** the sleeping threads that were waiting on that condition variable.

> 使用 `cnd_broadcast()` 代替 `cnd_signal()`，使用方法完全相同，但 `cnd_broadcast()` 会唤醒所有等待该条件变量的睡眠线程。

## [39.9] Running a Function One Time {#running-a-function-one-time number="39.9"}

Let's say you have a function that _could_ be run by many threads, but you don't know when, and it's not work trying to write all that logic.

> 假设你有一个可以由多个线程运行的函数，但你不知道什么时候运行，也不值得去写所有的逻辑。

There's a way around it: use `call_once()`. Tons of threads could try to run the function, but only the first one counts[^206^]

> 有一种解决方法：使用 `call_once()`。许多线程可以尝试运行该函数，但只有第一个线程有效 [^206^]。

To work with this, you need a special flag variable you declare to keep track of whether or not the thing's been run. And you need a function to run, which takes no parameters and returns no value.

> 要使用这个，你需要一个特殊的标志变量来跟踪它是否已经运行。你需要一个不带参数也不返回值的函数来运行。

::: {#cb742 .sourceCode}

```c
once_flag of = ONCE_FLAG_INIT;  // Initialize it like this

void run_once_function(void)
{
    printf("I'll only run once!\n");
}

int run(void *arg)
{
    (void)arg;

    call_once(&of, run_once_function);

    // ...
```

:::

In this example, no matter how many threads get to the `run()` function, the `run_once_function()` will only be called a single time.

> 在这个例子中，不管有多少线程进入 `run()` 函数，`run_once_function()` 只会被调用一次。

# [40] Atomics {#chapter-atomics number="40"}

> _"They tried and failed, all of them?"_ > _"Oh, no." She shook her head. "They tried and died."_
>
> ---Paul Atreides and The Reverend Mother Gaius Helen Mohiam, _Dune_

This is one of the more challenging aspects of multithreading with C. But we'll try to take it easy.

> 这是 C 多线程的更具挑战性的方面之一。但我们会尽量轻松一点。

Basically, I'll talk about the more straightforward uses of atomic variables, what they are, and how they work, etc. And I'll mention some of the more insanely-complex paths that are available to you.

> 基本上，我将讨论原子变量的更直接的用法，它们是什么，以及它们是如何工作的等等。我还会提到一些更复杂的选择，可供您使用。

But I won't go down those paths. Not only am I barely qualified to even write about them, but I figure if you know you need them, you already know more than I do.

> 但我不会走这些路。不仅我几乎没有资格去写关于它们的东西，而且我认为如果你知道你需要它们，你就比我更懂。

But there are some weird things out here even in the basics. So buckle your seatbelts, everyone, 'cause Kansas is goin' bye-bye.

> 但是这里连基本的东西也有一些奇怪的东西。所以大家都系好安全带，因为堪萨斯州要消失了。

## [40.1] Testing for Atomic Support {#testing-for-atomic-support number="40.1"}

Atomics are an optional feature. There's a macro `__STDC_NO_ATOMICS__` that's `1` if you _don't_ have atomics.

> 原子操作是一个可选功能。如果没有原子操作，就有一个宏 `__STDC_NO_ATOMICS__`，它的值为 `1`。

That macro might not exist pre-C11, so we should test the language version with `__STDC_VERSION__`[^207^].

> 那个宏可能在 C11 之前不存在，因此我们应该使用 `__STDC_VERSION__` 来测试语言版本 [^207^]。

::: {#cb743 .sourceCode}

```c
#if __STDC_VERSION__ < 201112L || __STDC_NO_ATOMICS__ == 1
#define HAS_ATOMICS 0
#else
#define HAS_ATOMICS 1
#endif
```

:::

If those tests pass, then you can safely include `<stdatomic.h>`, the header on which the rest of this chapter is based. But if there is no atomic support, that header might not even exist.

> 如果测试通过，那么您可以安全地包含 `<stdatomic.h>`，这是本章的其余部分所基于的头文件。但是，如果没有原子支持，那么该头文件可能根本不存在。

On some systems, you might need to add `-latomic` to the end of your compilation command line to use any functions in the header file.

> 在某些系统中，您可能需要在编译命令行末尾添加 `-latomic` 才能使用头文件中的任何函数。

## [40.2] Atomic Variables {#atomic-variables number="40.2"}

Here's _part_ of how atomic variables work:

If you have a shared atomic variable and you write to it from one thread, that write will be _all-or-nothing_ in a different thread.

> 如果你有一个共享的原子变量，并从一个线程中写入它，那么在另一个线程中，这个写入将是全部或无。

That is, the other thread will see the entire write of, say, a 32-bit value. Not half of it. There's no way for one thread to interrupt another that is in the _middle_ of an atomic multi-byte write.

> 那就是，另一个线程将看到整个写入，比如一个 32 位值。而不是一半。没有办法让一个线程中断另一个线程，它正处于原子多字节写入的_中间_。

It's almost like there's a little lock around the getting and setting of that one variable. (And there _might_ be! See [Lock-Free Atomic Variables](#lock-free-atomic), below.)

> 这就好像有一个小锁环绕着那个变量的获取和设置(也许真的有！参见下面的“无锁原子变量”)。

And on that note, you can get away with never using atomics if you use mutexes to lock your critical sections. It's just that there are a class of _lock-free data structures_ that always allow other threads to make progress instead of being blocked by a mutex... but these are tough to create correctly from scratch, and are one of the things that are beyond the scope of the guide, sadly.

> 在这个基础上，如果你使用互斥量来锁定关键部分，你就可以不使用原子操作。只是有一类_无锁数据结构_总是允许其他线程取得进展，而不是被互斥量阻塞...但是这些结构很难从头开始正确创建，而且是本指南范围之外的东西，很可惜。

That's only part of the story. But it's the part we'll start with.

Before we go further, how do you declare a variable to be atomic?

First, include `<stdatomic.h>`.

This gives us types such as `atomic_int`.

And then we can simply declare variables to be of that type.

But let's do a demo where we have two threads. The first runs for a while and then sets a variable to a specific value, then exits. The other runs until it sees that value get set, and then it exits.

> 但让我们做一个演示，我们有两个线程。第一个运行一段时间，然后将变量设置为特定值，然后退出。另一个运行，直到它看到该值被设置，然后它退出。

::: {#cb744 .sourceCode}

```c
#include <stdio.h>
#include <threads.h>
#include <stdatomic.h>

atomic_int x;   // THE POWER OF ATOMICS! BWHAHAHA!

int thread1(void *arg)
{
    (void)arg;

    printf("Thread 1: Sleeping for 1.5 seconds\n");
    thrd_sleep(&(struct timespec){.tv_sec=1, .tv_nsec=500000000}, NULL);

    printf("Thread 1: Setting x to 3490\n");
    x = 3490;

    printf("Thread 1: Exiting\n");
    return 0;
}

int thread2(void *arg)
{
    (void)arg;

    printf("Thread 2: Waiting for 3490\n");
    while (x != 3490) {}  // spin here

    printf("Thread 2: Got 3490--exiting!\n");
    return 0;
}

int main(void)
{
    x = 0;

    thrd_t t1, t2;

    thrd_create(&t1, thread1, NULL);
    thrd_create(&t2, thread2, NULL);

    thrd_join(t1, NULL);
    thrd_join(t2, NULL);

    printf("Main    : Threads are done, so x better be 3490\n");
    printf("Main    : And indeed, x == %d\n", x);
}
```

:::

The second thread spins in place, looking at the flag and waiting for it to get set to the value `3490`. And the first one does that.

> 第二个线程原地旋转，看着旗帜，等待它被设置为“3490”的值。第一个也是这样。

And I get this output:

::: {#cb745 .sourceCode}

```{.sourceCode .default}
Thread 1: Sleeping for 1.5 seconds
Thread 2: Waiting for 3490
Thread 1: Setting x to 3490
Thread 1: Exiting
Thread 2: Got 3490--exiting!
Main    : Threads are done, so x better be 3490
Main    : And indeed, x == 3490
```

:::

Look, ma! We're accessing a variable from different threads and not using a mutex! And that'll work every time thanks to the atomic nature of atomic variables.

> 看，妈妈！我们正在从不同的线程访问一个变量，而不使用互斥量！而且由于原子变量的原子性，这每次都能正常工作。

You might be wondering what happens if that's a regular non-atomic `int`, instead. Well, on my system it still works... unless I do an optimized build in which case it hangs on thread 2 waiting to see the 3490 to get set[^208^].

> 你可能想知道如果这是一个普通的非原子 `int`，会发生什么？嗯，在我的系统上它仍然可以工作... 除非我做了一个优化构建，在这种情况下，它在线程 2 上挂起，等待 3490 被设置[^208^]。

But that's just the beginning of the story. The next part is going to require more brain power and has to do with something called _synchronization_.

> 但这仅仅是故事的开始。下一部分需要更多的脑力，与一种叫做同步的东西有关。

## [40.3] Synchronization {#synchronization number="40.3"}

The next part of our story is all about when certain memory writes in one thread become visible to those in another thread.

> 下一部分的故事是关于当某些内存写入一个线程时，它们对另一个线程是可见的。

You might think, it's right away, right? But it's not. A number of things can go wrong. Weirdly wrong.

> 你可能会认为，这是立刻就可以的，对吗？但事实并非如此。可能会出现很多不妙的问题。奇怪的问题。

The compiler might have rearranged memory accesses so that when you think you set a value relative to another might not be true. And even if the compiler didn't, your CPU might have done it on the fly. Or maybe there's something else about this architecture that causes writes on one CPU to be delayed before they're visible on another.

> 编译器可能会重新排列内存访问，因此当您认为设置一个值相对于另一个值可能不正确。即使编译器没有，您的 CPU 也可能会实时进行重新排列。或者也许这种架构的某些其他方面会导致一个 CPU 上的写入在另一个 CPU 上可见之前被延迟。

The good news is that we can condense all these potential troubles into one: unsynchronized memory accesses can appear out of order depending on which thread is doing the observing, as if the lines of code themselves had been rearranged.

> 好消息是，我们可以把所有这些潜在问题归结为一个：根据哪个线程进行观察，未同步的内存访问可能会出现乱序，就好像代码行本身被重新排列了一样。

By way of example, which happens first in the following code, the write to `x` or the write to `y`?

> 例如，以下代码中哪个先执行，写入 `x` 还是写入 `y`？

::: {#cb746 .sourceCode}

```c
int x, y;  // global

// ...

x = 2;
y = 3;

printf("%d %d\n", x, y);
```

:::

Answer: we don't know. The compiler or CPU could silently reverse lines 5 and 6 and we'd be none-the-wiser. The code would run single-threaded _as-if_ it were executed in code order.

> 答案：我们不知道。编译器或 CPU 可以静默地反转第 5 行和第 6 行，我们也不会知道。代码将以单线程的方式按照代码顺序执行。

In a multithreaded scenario, we might have something like this pseudocode:

> 在多线程场景中，我们可能会有类似这样的伪代码：

::: {#cb747 .sourceCode}

```c
int x = 0, y = 0;

thread1() {
    x = 2;
    y = 3;
}

thread2() {
    while (y != 3) {}  // spin
    printf("x is now %d\n", x);  // 2? ...or 0?
}
```

:::

What is the output from thread 2?

Well, if `x` gets assigned `2` _before_ `y` is assigned `3`, then I'd expect the output to be the very sensible:

> 如果 x 在 y 被赋予 3 之前被赋予 2，那么我期望的输出是非常明智的：

::: {#cb748 .sourceCode}

```{.sourceCode .default}
x is now 2
```

:::

But something sneaky could rearrange lines 4 and 5 causing us to see the value of `0` for `x` when we print it.

> 但有什么狡猾的东西可以重新排列第 4 行和第 5 行，使我们在打印时看到 `x` 的值为 `0`。

In other words, all bets are off unless we can somehow say, "As of this point, I expect all previous writes in another thread to be visible in this thread."

> 换句话说，除非我们能够说“从这一点开始，我期望另一个线程中的所有写入都可以在这个线程中可见”，否则一切都无效。

Two threads _synchronize_ when they agree on the state of shared memory. As we've seen, they're not always in agreement with the code. So how do they agree?

> 两个线程在就共享内存的状态达成一致时会进行同步。正如我们所看到的，它们并不总是与代码保持一致。那么它们是如何达成一致的呢？

Using atomic variables can force the agreement[^209^]. If a thread writes to an atomic variable, it's saying "anyone who reads this atomic variable in the future will also see all the changes I made to memory (atomic or not) up to and including the atomic variable".

> 使用原子变量可以强制执行协议[^209^] (#fn209) {#fnref209 .footnote-ref role="doc-noteref"}。如果一个线程写入原子变量，就是在说“任何将来读取这个原子变量的人也将看到我对内存(原子的或非原子的)所做的所有更改，包括原子变量”。

Or, in more human terms, let's sit around the conference table and make sure we're on the same page as to which pieces of shared memory hold what values. You agree that the memory changes that you'd made up-to-and-including the atomic store will be visible to me after I do a load of the same atomic variable.

> 让我们坐在会议桌旁，确保我们对共享内存中哪些值是什么有同样的理解。您同意，您在原子存储之前所做的内存更改，在我加载相同的原子变量后，我将可以看到。

So we can easily fix our example:

::: {#cb749 .sourceCode}

```c
int x = 0;
atomic int y = 0;  // Make y atomic

thread1() {
    x = 2;
    y = 3;             // Synchronize on write
}

thread2() {
    while (y != 3) {}  // Synchronize on read
    printf("x is now %d\n", x);  // 2, period.
}
```

:::

Because the threads synchronize across `y`, all writes in thread 1 that happened _before_ the write to `y` are visible in thread 2 _after_ the read from `y` (in the `while` loop).

> 因为线程在 `y` 上同步，所以线程 1 中发生在写入 `y` 之前的所有写操作，在线程 2 在 `while` 循环中读取 `y` 之后都是可见的。

It's important to note a couple things here:

1. Nothing sleeps. The synchronization is not a blocking operation. Both threads are running full bore until they exit. Even the one stuck in the spin loop isn't blocking anyone else from running.

> 没有什么休眠。同步不是阻塞操作。两个线程都在全速运行，直到它们退出。即使那个被卡在旋转循环中的也不会阻止其他线程的运行。

2. The synchronization happens when one thread reads an atomic variable another thread wrote. So when thread 2 reads `y`, all previous memory writes in thread 1 (namely setting `x`) will be visible in thread 2.

> 当一个线程读取另一个线程写入的原子变量时，同步就发生了。因此，当线程 2 读取'y'时，线程 1 中所有先前的内存写入(即设置'x')将在线程 2 中可见。

3. Notice that `x` isn't atomic. That's OK because we're not synchronizing over `x`, and the synchronization over `y` when we write it in thread 1 means that all previous writes---including `x`---in thread 1 will become visible to other threads... if those other threads read `y` to synchronize.

> 注意 `x` 不是原子的。这没关系，因为我们不是在 `x` 上进行同步，而是在线程 1 中写入 `y` 时进行同步，这意味着所有先前的写入(包括 `x`)在线程 1 中将对其他线程可见......如果其他线程读取 `y` 进行同步的话。

Forcing this synchronization is inefficient and can be a lot slower than just using a regular variable. This is why we don't use atomics unless we have to for a particular application.

> 强制同步效率低下，比使用普通变量慢得多。这就是为什么除非在特定应用中必须使用原子变量，否则我们不会使用它们。

So that's the basics. Let's look deeper.

## [40.4] Acquire and Release {#acquire-and-release number="40.4"}

More terminology! It'll pay off to learn this now.

When a thread reads an atomic variable, it is said to be an _acquire_ operation.

> 当一个线程读取一个原子变量时，称之为获取操作。

When a thread writes an atomic variable, it is said to be a _release_ operation.

> 当一个线程写入一个原子变量时，称之为发布操作。

What are these? Let's line them up with terms you already know when it comes to atomic variables:

> 这是什么？让我们把它们与您在原子变量方面已经知道的术语对齐：

**Read = Load = Acquire**. Like when you compare an atomic variable or read it to copy it to another value.

> 读取=加载=获取。就像当你比较原子变量或读取它以将其复制到另一个值时。

**Write = Store = Release**. Like when you assign a value into an atomic variable.

> 写入=存储=发布，就像当你将一个值赋给原子变量时一样。

When using atomic variables with these acquire/release semantics, C spells out what can happen when.

> 当使用具有这些获取/释放语义的原子变量时，C 指出可能发生什么。

Acquire/release form the basis for the synchronization we just talked about.

> 获取/释放是我们刚才讨论的同步的基础。

When a thread acquires an atomic variable, it can see values set in another thread that released that same variable.

> 当一个线程获取原子变量时，它可以看到另一个线程释放同一个变量时设置的值。

In other words:

When a thread reads an atomic variable, it can see values set in another thread that wrote to that same variable.

> 当一个线程读取一个原子变量时，它可以看到另一个线程写入该变量的值。

The synchronization happens across the acquire/release pair.

More details:

With read/load/acquire of a particular atomic variable:

- All writes (atomic or non-atomic) in another thread that happened before that other thread wrote/stored/released this atomic variable are now visible in this thread.

> 所有在另一个线程中发生的(原子的或非原子的)写入，在该线程写入/存储/释放这个原子变量之前，现在在这个线程中可见。

- The new value of the atomic variable set by the other thread is also visible in this thread.
- No reads or writes of any variables/memory in the current thread can be reordered to happen before this acquire.

> 在当前线程中，不允许对任何变量/内存的读写重新排序，以便在此获取之前发生。

- The acquire acts as a one-way barrier when it comes to code reordering; reads and writes in the current thread can be moved down from _before_ the acquire to _after_ it. But, more importantly for synchronization, nothing can move up from _after_ the acquire to _before_ it.

> 当涉及到代码重排序时，获取行为充当单向屏障；当前线程中的读取和写入可以从获取之前移动到获取之后。但更重要的是，用于同步的任何内容都不能从获取之后移动到获取之前。

With write/store/release of a particular atomic variable:

- All writes (atomic or non-atomic) in the current thread that happened before this release become visible to other threads that have read/loaded/acquired the same atomic variable.

> 所有在当前线程中发生的写操作(无论是原子操作还是非原子操作)，在发布之前，都将对其他线程读取/加载/获取同一原子变量的线程可见。

- The value written to this atomic variable by this thread is also visible to other threads.
- No reads or writes of any variables/memory in the current thread can be reordered to happen after this release.

> 在当前线程中，不允许对任何变量/内存的读写重新排序，以发生在此发布之后。

- The release acts as a one-way barrier when it comes to code reordering: reads and writes in the current thread can be moved up from _after_ the release to _before_ it. But, more importantly for synchronization, nothing can move down from _before_ the release to _after_ it.

> 发布时，代码重新排序是一个单向屏障：当前线程中的读取和写入可以从发布之后移动到发布之前。但更重要的是，同步时，什么也不能从发布之前移动到发布之后。

Again, the upshot is synchronization of memory from one thread to another. The second thread can be sure that variables and memory are written in the order the programmer intended.

> 再次，结果是从一个线程到另一个线程的内存同步。第二个线程可以确保变量和内存按程序员预期的顺序写入。

```
int x, y, z = 0;
atomic_int a = 0;

thread1() {
    x = 10;
    y = 20;
    a = 999;  // Release
    z = 30;
}

thread2()
{
    while (a != 999) { } // Acquire

    assert(x == 10);  // never asserts, x is always 10
    assert(y == 20);  // never asserts, y is always 20

    assert(z == 0);  // might assert!!
}
```

In the above example, `thread2` can be sure of the values in `x` and `y` after it acquires `a` because they were set before `thread1` released the atomic `a`.

> 在上面的例子中，在线程 2 获取原子 a 之后，它可以确定 x 和 y 的值，因为它们是在线程 1 释放原子 a 之前设置的。

But `thread2` can't be sure of `z`'s value because it happened after the release. Maybe the assignment to `z` got moved before the assignment to `a`.

> 但是 thread2 不能确定 z 的值，因为这发生在释放之后。也许将 z 分配给 a 之前已经移动了。

An important note: releasing one atomic variable has no effect on acquires of different atomic variables. Each variable is isolated from the others.

> 重要提示：释放一个原子变量不会对获取不同原子变量产生影响。每个变量都与其他变量隔离。

## [40.5] Sequential Consistency {#sequential-consistency number="40.5"}

You hanging in there? We're through the meat of the simpler usage of atomics. And since we're not even going to talk about the more complex uses here, you can relax a bit.

> 你还在坚持吗？我们已经讨论完原子的简单用法了。由于我们这里不会讨论更复杂的用法，你可以放松一下了。

_Sequential consistency_ is what's called a _memory ordering_. There are many memory orderings, but sequential consistency is the sanest[^210^] C has to offer. It is also the default. You have to go out of your way to use other memory orderings.

> _顺序一致性_被称为_内存排序_。有许多内存排序，但顺序一致性是 C 提供的最合理的[^210^]。这也是默认值。要使用其他内存排序，必须特地去做。

All the stuff we've been talking about so far has happened within the realm of sequential consistency.

> 所有我们到目前为止讨论的东西都发生在顺序一致性的范围内。

We've talked about how the compiler or CPU can rearrange memory reads and writes in a single thread as long as it follows the _as-if_ rule.

> 我们讨论了编译器或 CPU 如何在单个线程中重新排列内存读取和写入，只要它遵守_as-if_规则即可。

And we've seen how we can put the brakes on this behavior by synchronizing over atomic variables.

> 我们已经看到，我们可以通过使用原子变量来阻止这种行为。

Let's formalize just a little more.

If operations are _sequentially consistent_, it means at the end of the day, when all is said and done, all the threads can kick up their feet, open their beverage of choice, and all agree on the order in which memory changes occurred during the run. And that order is the one specified by the code.

> 如果操作是顺序一致的，这意味着到最后，当一切都说完了，所有的线程都可以休息，打开他们喜欢的饮料，并且都能同意在运行期间内存变化的顺序。而这个顺序就是由代码指定的。

One won't say, "But didn't _B_ happen before _A_?" if the rest of them say, "_A_ definitely happened before _B_". They're all friends, here.

> 他们都是朋友，如果其他人都说“A 肯定发生在 B 之前”，没有人会说“但 B 没有发生在 A 之前吗？”

In particular, within a thread, none of the acquires and releases can be reordered with respect to one another. This is in addition to the rules about what other memory accesses can be reordered around them.

> 特别是在一个线程中，没有一个获取和释放可以相互重新排序。这是除了关于其他内存访问可以在它们周围重新排序的规则之外的。

This rule gives an additional level of sanity to the progression of atomic loads/acquires and stores/releases.

> 这条规则为原子负载/获取和存储/释放的进程增加了一个额外的正常水平。

Every other memory order in C involves a relaxation of the reordering rules, either for acquires/releases or other memory accesses, atomic or otherwise. You'd do that if you _really_ knew what you were doing and needed the speed boost. _Here be armies of dragons..._

> 每个其他的 C 内存顺序都涉及到对重新排序规则的放松，无论是获取/释放或其他内存访问，原子或其他。如果你真的知道你在做什么并且需要提升速度，你就会这样做。这里有一大群龙...

More on that later, but for now, let's stick to the safe and practical.

## [40.6] Atomic Assignments and Operators {#atomic-assignments-and-operators number="40.6"}

Certain operators on atomic variables are atomic. And others aren't.

Let's start with a counter-example:

::: {#cb751 .sourceCode}

```c
atomic_int x = 0;

thread1() {
    x = x + 3;  // NOT atomic!
}
```

:::

Since there's a read of `x` on the right hand side of the assignment and a write effectively on the left, these are two operations. Another thread could sneak in the middle and make you unhappy.

> 由于赋值右边有一个读取 `x` 的操作，左边有一个写入操作，这是两个操作。另一个线程可能会插入中间，让你不开心。

But you _can_ use the shorthand `+=` to get an atomic operation:

::: {#cb752 .sourceCode}

```c
atomic_int x = 0;

thread1() {
    x += 3;   // ATOMIC!
}
```

:::

In that case, `x` will be atomically incremented by `3`---no other thread can jump in the middle.

> 在这种情况下，`x` 将被原子性地增加 `3`-没有其他线程可以插入中间。

In particular, the following operators are atomic read-modify-write operations with sequential consistency, so use them with gleeful abandon. (In the example, `a` is atomic.)

> 特别是，以下操作符是原子读取-修改-写入操作，具有顺序一致性，因此可以欢快地使用它们。(在示例中，`a` 是原子的。)

::: {#cb753 .sourceCode}

```c
a++       a--       --a       ++a
a += b    a -= b    a *= b    a /= b    a %= b
a &= b    a |= b    a ^= b    a >>= b   a <<= b
```

:::

## [40.7] Library Functions that Automatically Synchronize {#library-functions-that-automatically-synchronize number="40.7"}

So far we've talked about how you can synchronize with atomic variables, but it turns out there are a few library functions that do some limited behind-the-scenes synchronization, themselves.

> 到目前为止，我们讨论了如何使用原子变量进行同步，但事实证明，一些库函数本身也可以进行一些有限的后台同步。

::: {#cb754 .sourceCode}

```c
call_once()      thrd_create()       thrd_join()
mtx_lock()       mtx_timedlock()     mtx_trylock()
malloc()         calloc()            realloc()
aligned_alloc()
```

:::

**`call_once()`**---Synchronizes with all subsequent calls to `call_once()` for a particular flag. This way subsequent calls can rest assured that if another thread sets the flag, they will see it.

> `call_once()`---与特定标志的所有后续调用同步。这样，后续调用可以确保，如果另一个线程设置了标志，它们将会看到它。

**`thrd_create()`**---Synchronizes with the beginning of the new thread. The new thread can be sure it will see all shared memory writes from the parent thread from before the `thrd_create()` call.

> `thrd_create()`--同步新线程的开始。新线程可以确保它会看到从 `thrd_create()` 调用之前父线程写入的所有共享内存。

**`thrd_join()`**---When a thread dies, it synchronizes with this function. The thread that has called `thrd_join()` can be assured that it can see all the late thread's shared writes.

> 当一个线程死亡时，它会与 `thrd_join()` 函数同步。调用 `thrd_join()` 的线程可以确保它可以看到所有后续线程的共享写入。

**`mtx_lock()`**---Earlier calls to `mtx_unlock()` on the same mutex synchronize on this call. This is the case that most mirrors the acquire/release process we've already talked about. `mtx_unlock()` performs a release on the mutex variable, assuring any subsequent thread that makes an acquire with `mtx_lock()` can see all the shared memory changes in the critical section.

> `mtx_lock()`——之前对同一个互斥量的 `mtx_unlock()` 调用会在此调用上同步。这是我们已经讨论过的获取/释放过程的典型情况。`mtx_unlock()` 对互斥量变量执行释放，确保任何后续使用 `mtx_lock()` 进行获取的线程都可以看到临界区中的所有共享内存更改。

**`mtx_timedlock()`** and **`mtx_trylock()`**---Similar to the situation with `mtx_lock()`, if this call succeeds, earlier calls to `mtx_unlock()` synchronize with this one.

> **`mtx_timedlock()`** 和 **`mtx_trylock()`** 的情况类似，如果调用成功，之前的 `mtx_unlock()` 调用将与此次调用同步。

**Dynamic Memory Functions**: if you allocate memory, it synchronizes with the previous deallocation of that same memory. And allocations and deallocations of that particular memory region happen in a single total order that all threads can agree upon. I _think_ the idea here is that the deallocation can wipe the region if it chooses, and we want to be sure that a subsequent allocation doesn't see the non-wiped data. Someone let me know if there's more to it.

> **动态内存功能**：如果您分配内存，它将与先前的该内存释放同步。并且该特定内存区域的分配和释放以所有线程都可以同意的单一总顺序发生。我认为这里的想法是，释放可以选择擦除该区域，我们希望确保后续分配不会看到未擦除的数据。如果还有其他内容，请有人告诉我。

## [40.8] Atomic Type Specifier, Qualifier {#atomic-type-specifier-qualifier number="40.8"}

Let's take it down a notch and see what types we have available, and how we can even make new atomic types.

> 让我们放慢一点，看看我们有哪些类型可用，以及我们如何甚至可以创建新的原子类型。

First things first, let's look at the built-in atomic types and what they are `typedef`'d to. (Spoiler: `_Atomic` is a type qualifier!)

> 首先，让我们看看内置的原子类型以及它们被 `typedef` 到什么。(剧透：`_Atomic` 是一种类型限定符！)

---

Atomic type Longhand equivalent

---

`atomic_bool` `_Atomic _Bool`

`atomic_char` `_Atomic char`

`atomic_schar` `_Atomic signed char`

`atomic_uchar` `_Atomic unsigned char`

`atomic_short` `_Atomic short`

`atomic_ushort` `_Atomic unsigned short`

`atomic_int` `_Atomic int`

`atomic_uint` `_Atomic unsigned int`

`atomic_long` `_Atomic long`

`atomic_ulong` `_Atomic unsigned long`

`atomic_llong` `_Atomic long long`

`atomic_ullong` `_Atomic unsigned long long`

`atomic_char16_t` `_Atomic char16_t`

`atomic_char32_t` `_Atomic char32_t`

`atomic_wchar_t` `_Atomic wchar_t`

`atomic_int_least8_t` `_Atomic int_least8_t`

`atomic_uint_least8_t` `_Atomic uint_least8_t`

`atomic_int_least16_t` `_Atomic int_least16_t`

`atomic_uint_least16_t` `_Atomic uint_least16_t`

`atomic_int_least32_t` `_Atomic int_least32_t`

`atomic_uint_least32_t` `_Atomic uint_least32_t`

`atomic_int_least64_t` `_Atomic int_least64_t`

`atomic_uint_least64_t` `_Atomic uint_least64_t`

`atomic_int_fast8_t` `_Atomic int_fast8_t`

`atomic_uint_fast8_t` `_Atomic uint_fast8_t`

`atomic_int_fast16_t` `_Atomic int_fast16_t`

`atomic_uint_fast16_t` `_Atomic uint_fast16_t`

`atomic_int_fast32_t` `_Atomic int_fast32_t`

`atomic_uint_fast32_t` `_Atomic uint_fast32_t`

`atomic_int_fast64_t` `_Atomic int_fast64_t`

`atomic_uint_fast64_t` `_Atomic uint_fast64_t`

`atomic_intptr_t` `_Atomic intptr_t`

`atomic_uintptr_t` `_Atomic uintptr_t`

`atomic_size_t` `_Atomic size_t`

`atomic_ptrdiff_t` `_Atomic ptrdiff_t`

`atomic_intmax_t` `_Atomic intmax_t`

## `atomic_uintmax_t` `_Atomic uintmax_t`

Use those at will! They're consistent with the atomic aliases found in C++, if that helps.

> 随意使用它们！如果有帮助的话，它们与 C++ 中的原子别名一致。

But what if you want more?

You can do it either with a type qualifier or type specifier.

First, specifier! It's the keyword `_Atomic` with a type in parens after[^211^]---suitable for use with `typedef`:

> 首先，指定者！它是关键字 `_Atomic`，后面有一个括号中的类型[^211^]---适用于 `typedef`：

::: {#cb755 .sourceCode}

```c
typedef _Atomic(double) atomic_double;

atomic_double f;
```

:::

Restrictions on the specifier: the type you're making atomic can't be of type array or function, nor can it be atomic or otherwise qualified.

> 限制对规范者的限制：您正在制作的原子类型不能是数组或函数类型，也不能是原子类型或其他有资格的类型。

Next, qualifier! It's the keyword `_Atomic` _without_ a type in parens.

So these do similar things[^212^]:

> 这些做的事情很相似 [^212^]：

::: {#cb756 .sourceCode}

```c
_Atomic(int) i;   // type specifier
_Atomic int  j;   // type qualifier
```

:::

The thing is, you can include other type qualifiers with the latter:

::: {#cb757 .sourceCode}

```c
_Atomic volatile int k;   // qualified atomic variable
```

:::

Restrictions on the qualifier: the type you're making atomic can't be of type array or function.

> 限制条件：您正在创建的原子类型不能是数组或函数类型。

## [40.9] Lock-Free Atomic Variables {#lock-free-atomic number="40.9"}

Hardware architectures are limited in the amount of data they can atomically read and write. It depends on how it's wired together. And it varies.

> 硬件架构在原子读写的数据量上是有限的，这取决于它的接线方式，而且也会有所不同。

If you use an atomic type, you can be assured that accesses to that type will be atomic... but there's a catch: if the hardware can't do it, it's done with a lock, instead.

> 如果你使用原子类型，你可以确保对该类型的访问是原子的... 但是有一个问题：如果硬件不能做到，就需要使用锁来实现。

So the atomic access becomes lock-access-unlock, which is rather slower and has some implications for signal handlers.

> 所以原子访问变成了锁定-访问-解锁，这样比较慢，并且对信号处理程序有一些影响。

[Atomic flags](#atomic-flags), below, is the only atomic type that is guaranteed to be lock-free in all conforming implementations. In typical desktop/laptop computer world, other larger types are likely lock-free.

> 原子标志(#atomic-flags)是唯一一种在所有符合要求的实现中都保证是无锁的原子类型。在典型的台式/笔记本电脑世界中，其他较大的类型很可能是无锁的。

Luckily, we have a couple ways to determine if a particular type is a lock-free atomic or not.

> 幸运的是，我们有几种方法来确定特定类型是否是无锁原子的。

First of all, some macros---you can use these at compile time with `#if`. They apply to both signed and unsigned types.

> 首先，一些宏---您可以在编译时使用 `#if` 来使用它们。它们适用于有符号和无符号类型。

---

Atomic Type Lock Free Macro

---

`atomic_bool` `ATOMIC_BOOL_LOCK_FREE`

`atomic_char` `ATOMIC_CHAR_LOCK_FREE`

`atomic_char16_t` `ATOMIC_CHAR16_T_LOCK_FREE`

`atomic_char32_t` `ATOMIC_CHAR32_T_LOCK_FREE`

`atomic_wchar_t` `ATOMIC_WCHAR_T_LOCK_FREE`

`atomic_short` `ATOMIC_SHORT_LOCK_FREE`

`atomic_int` `ATOMIC_INT_LOCK_FREE`

`atomic_long` `ATOMIC_LONG_LOCK_FREE`

`atomic_llong` `ATOMIC_LLONG_LOCK_FREE`

## `atomic_intptr_t` `ATOMIC_POINTER_LOCK_FREE`

These macros can interestingly have _three_ different values:

Value Meaning

---

`0` Never lock-free.
`1` _Sometimes_ lock-free.
`2` Always lock-free.

Wait---how can something be _sometimes_ lock-free? This just means the answer isn't known at compile-time, but could later be known at runtime. Maybe the answer varies depending on whether or not you're running this code on Genuine Intel or AMD, or something like that[^213^].

> 等等---怎么有些时候可以是无锁的？这意味着答案在编译时不能确定，但可以在运行时确定。也许答案取决于你是在 Genuine Intel 还是 AMD 上运行这段代码，或者类似的情况。

But you can always test at runtime with the `atomic_is_lock_free()` function. This function returns true or false if the particular type is atomic right now.

> 但是您可以使用 `atomic_is_lock_free()` 函数在运行时测试。如果特定类型当前是原子的，此函数将返回 true 或 false。

So why do we care?

Lock-free is faster, so maybe there's a speed concern that you'd code around another way. Or maybe you need to use an atomic variable in a signal handler.

> 无锁更快，所以也许你可以用另一种方式编码来解决速度问题。或者也许你需要在信号处理程序中使用原子变量。

### [40.9.1] Signal Handlers and Lock-Free Atomics {#signal-handlers-and-lock-free-atomics number="40.9.1"}

If you read or write a shared variable (static storage duration or `_Thread_Local`) in a signal handler, it's undefined behavior \[gasp!\]... Unless you do one of the following:

> 如果在信号处理程序中读取或写入共享变量(静态存储持续时间或 `_Thread_Local`)，那么这是未定义的行为\[哇！\]... 除非你做以下之一：

1. Write to a variable of type `volatile sig_atomic_t`.
2. Read or write a lock-free atomic variable.

As far as I can tell, lock-free atomic variables are one of the few ways you get portably get information out of a signal handler.

> 据我所知，无锁原子变量是从信号处理程序中获取信息的少数可移植方式之一。

The spec is a bit vague, in my read, about the memory order when it comes to acquiring or releasing atomic variables in the signal handler. C++ says, and it makes sense, that such accesses are unsequenced with respect to the rest of the program[^214^]. The signal can be raised, after all, at any time. So I'm assuming C's behavior is similar.

> 这个规范在涉及信号处理程序中获取或释放原子变量的内存顺序方面有点模糊，据我所知，C++ 说，这是有道理的，这种访问与程序的其余部分是无序的[^214^]。毕竟，信号可以随时被触发。所以我假设 C 的行为是相似的。

## [40.10] Atomic Flags {#atomic-flags number="40.10"}

There's only one type the standard guarantees will be a lock-free atomic: `atomic_flag`. This is an opaque type for [test-and-set](https://en.wikipedia.org/wiki/Test-and-set)[^215^] operations.

> 只有一种类型可以保证是无锁原子操作：`atomic_flag`。这是一种用于[测试和设置](https://en.wikipedia.org/wiki/Test-and-set)[^215^]操作的不透明类型。

It can be either _set_ or _clear_. You can initialize it to clear with:

::: {#cb758 .sourceCode}

```c
atomic_flag f = ATOMIC_FLAG_INIT;
```

:::

You can set the flag atomically with `atomic_flag_test_and_set()`, which will set the flag and return its previous status as a `_Bool` (true for set).

> 你可以使用 `atomic_flag_test_and_set()` 原子性地设置标志，它会将标志设置为真，并返回其以前的状态作为 `_Bool`(真表示设置)。

You can clear the flag atomically with `atomic_flag_clear()`.

Here's an example where we init the flag to clear, set it twice, then clear it again.

> 这里有一个例子，我们将标志初始化为清除，设置两次，然后再次清除它。

::: {#cb759 .sourceCode}

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdatomic.h>

atomic_flag f = ATOMIC_FLAG_INIT;

int main(void)
{
    bool r = atomic_flag_test_and_set(&f);
    printf("Value was: %d\n", r);           // 0

    r = atomic_flag_test_and_set(&f);
    printf("Value was: %d\n", r);           // 1

    atomic_flag_clear(&f);
    r = atomic_flag_test_and_set(&f);
    printf("Value was: %d\n", r);           // 0
}
```

:::

## [40.11] Atomic `struct` s and `union` s {#atomic-structs-and-unions number="40.11"}

Using the `_Atomic` qualifier or specifier, you can make atomic `struct` s or `union` s! Pretty astounding.

> 使用 `_Atomic` 限定符，你可以使原子 `struct` 或 `union`！真是令人惊叹。

If there's not a lot of data in there (i.e. a handful of bytes), the resulting atomic type might be lock-free. Test it with `atomic_is_lock_free()`.

> 如果里面没有太多数据(即几个字节)，那么生成的原子类型可能是无锁的。使用 `atomic_is_lock_free()` 进行测试。

::: {#cb760 .sourceCode}

```c
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    struct point {
        float x, y;
    };

    _Atomic(struct point) p;

    printf("Is lock free: %d\n", atomic_is_lock_free(&p));
}
```

:::

Here's the catch: you can't access fields of an atomic `struct` or `union`... so what's the point? Well, you can atomically _copy_ the entire `struct` into a non-atomic variable and then use it. You can atomically copy the other way, too.

> 这里有个陷阱：你不能访问原子结构体或联合体的字段...那么有什么用呢？好吧，你可以原子地将整个结构体复制到一个非原子变量中，然后使用它。你也可以反向原子复制。

::: {#cb761 .sourceCode}

```c
#include <stdio.h>
#include <stdatomic.h>

int main(void)
{
    struct point {
        float x, y;
    };

    _Atomic(struct point) p;
    struct point t;

    p = (struct point){1, 2};  // Atomic copy

    //printf("%f\n", p.x);  // Error

    t = p;   // Atomic copy

    printf("%f\n", t.x);  // OK!
}
```

:::

You can also declare a `struct` where individual fields are atomic. It is implementation defined if atomic types are allowed on bitfields.

> 你也可以声明一个结构体，其中的各个字段是原子的。如果允许在位域上使用原子类型，则实现定义。

## [40.12] Atomic Pointers {#atomic-pointers number="40.12"}

Just a note here about placement of `_Atomic` when it comes to pointers.

First, pointers to atomics (i.e. the pointer value is not atomic, but the thing it points to is):

> 首先，指向原子的指针(即指针值不是原子的，但它指向的东西是原子的)：

::: {#cb762 .sourceCode}

```c
_Atomic int x;
_Atomic int *p;  // p is a pointer to an atomic int

p = &x;  // OK!
```

:::

Second, atomic pointers to non-atomic values (i.e. the pointer value itself is atomic, but the thing it points to is not):

> 第二，指向非原子值的原子指针(即指针值本身是原子的，但它指向的东西不是)：

::: {#cb763 .sourceCode}

```c
int x;
int * _Atomic p;  // p is an atomic pointer to an int

p = &x;  // OK!
```

:::

Lastly, atomic pointers to atomic values (i.e. the pointer and the thing it points to are both atomic):

> 最后，原子指针指向原子值(即指针和它指向的东西都是原子的)：

::: {#cb764 .sourceCode}

```c
_Atomic int x;
_Atomic int * _Atomic p;  // p is an atomic pointer to an atomic int

p = &x;  // OK!
```

:::

## [40.13] Memory Order {#memory-order number="40.13"}

We've already talked about sequential consistency, which is the sensible one of the bunch. But there are a number of other ones:

> 我们已经讨论过顺序一致性，这是其中最明智的一种。但是还有其他一些种类：

---

`memory_order` Description

---

`memory_order_seq_cst` Sequential Consistency

`memory_order_acq_rel` Acquire/Release

`memory_order_release` Release

`memory_order_acquire` Acquire

`memory_order_consume` Consume

## `memory_order_relaxed` Relaxed

You can specify other ones with certain library functions. For example, you can add a value to an atomic variable like this:

> 你可以使用某些库函数来指定其他的。例如，你可以像这样给原子变量添加一个值：

::: {#cb765 .sourceCode}

```c
atomic_int x = 0;

x += 5;  // Sequential consistency, the default
```

:::

Or you can do the same with this library function:

::: {#cb766 .sourceCode}

```c
atomic_int x = 0;

atomic_fetch_add(&x, 5);  // Sequential consistency, the default
```

:::

Or you can do the same thing with an explicit memory ordering:

::: {#cb767 .sourceCode}

```c
atomic_int x = 0;

atomic_fetch_add_explicit(&x, 5, memory_order_seq_cst);
```

:::

But what if we didn't want sequential consistency? And you wanted acquire/release instead for whatever reason? Just name it:

> 但是如果我们不想要顺序一致性呢？出于某种原因，你想要 acquire/release？只需要称之为：

::: {#cb768 .sourceCode}

```c
atomic_int x = 0;

atomic_fetch_add_explicit(&x, 5, memory_order_acq_rel);
```

:::

We'll do a breakdown of the different memory orders, below. Don't mess with anything other than sequential consistency unless you know what you're doing. It's really easy to make mistakes that will cause rare, hard-to-repro failures.

> 我们将在下面对不同的内存顺序进行分解。除了顺序一致性，不要操作其他任何内容，除非你知道自己在做什么。犯错很容易导致罕见的、难以重现的故障。

### [40.13.1] Sequential Consistency {#sequential-consistency-1 number="40.13.1"}

- Load operations acquire (see below).
- Store operations release (see below).
- Read-modify-write operations acquire then release.

Also, in order to maintain the total order of acquires and releases, no acquires or releases will be reordered with respect to each other. (The acquire/release rules do not forbid reordering a release followed by an acquire. But the sequentially consistent rules do.)

> 为了保持获取和释放的总顺序，不会对它们之间的获取或释放进行重新排序。(获取/释放规则不禁止释放后跟着获取进行重新排序，但顺序一致性规则禁止。)

### [40.13.2] Acquire {#acquire number="40.13.2"}

This is what happens on a load/read operation on an atomic variable.

- If another thread released this atomic variable, all the writes that thread did are now visible in this thread.

> 如果另一个线程释放了这个原子变量，那么该线程所做的所有写入现在在这个线程中可见。

- Memory accesses in this thread that happen after this load can't be reordered before it.

### [40.13.3] Release {#release number="40.13.3"}

This is what happens on a store/write of an atomic variable.

- If another thread later acquires this atomic variable, all memory writes in this thread before its atomic write become visible to that other thread.

> 如果另一个线程稍后获取此原子变量，则此线程在其原子写入之前的所有内存写入对该其他线程可见。

- Memory accesses in this thread that happen before the release can't be reordered after it.

### [40.13.4] Consume {#consume number="40.13.4"}

This is an odd one, similar to a less-strict version of acquire. It affects memory accesses that are _data dependent_ on the atomic variable.

> 这是一个奇怪的，类似于一个不那么严格的 acquire 版本。它会影响基于原子变量的数据依赖的内存访问。

Being "data dependent" vaguely means that the atomic variable is used in a calculation.

> 被称为“数据依赖”意味着原子变量被用于计算。

That is, if a thread consumes an atomic variable then all the operations in that thread that go on to use that atomic variable will be able to see the memory writes in the releasing thread.

> 如果一个线程消费原子变量，那么在该线程中使用该原子变量的所有操作都将能够看到释放线程中的内存写入。

Compare to acquire where memory writes in the releasing thread will be visible to _all_ operations in the current thread, not just the data-dependent ones.

> 比较获取，在释放线程中写入的内存将对当前线程中的所有操作可见，而不仅仅是数据相关的操作。

Also like acquire, there is a restriction on which operations can be reordered _before_ the consume. With acquire, you couldn't reorder anything before it. With consume, you can't reorder anything that depends on the loaded atomic value before it.

> 也像 acquire 一样，在消费之前对操作的重新排序有限制。使用 acquire，您无法在其之前重新排序任何内容。使用消费，您不能在其之前重新排序任何依赖于加载的原子值的操作。

### [40.13.5] Acquire/Release {#acquirerelease number="40.13.5"}

This only applies to read-modify-write operations. It's an acquire and release bundled into one.

> 这只适用于读-修改-写操作。它是一个获取和释放的组合。

- An acquire happens for the read.
- A release happens for the write.

### [40.13.6] Relaxed {#relaxed number="40.13.6"}

No rules; it's anarchy! Everyone can reorder everything everywhere! Dogs and cats living together---mass hysteria!

> 没有规则；这是无政府状态！每个人都可以随意重新排列一切！狗和猫一起生活--大混乱！

Actually, there is a rule. Atomic reads and writes are still all-or-nothing. But the operations can be reordered whimsically and there is zero synchronization between threads.

> 实际上，有一条规则。原子读写仍然是全部或全不。但是操作可以任意重新排序，而线程之间没有任何同步。

There are a few use cases for this memory order, which you can find with a tiny bit of searching, e.g. simple counters.

> 有几种使用情况可以使用这种内存顺序，只需要稍微搜索一下就可以找到，例如简单的计数器。

And you can use a fence to force synchronization after a bunch of relaxed writes.

> 你可以使用围栏来在一系列松散的写操作之后强制同步。

## [40.14] Fences {#fences number="40.14"}

You know how the releases and acquires of atomic variables occur as you read and write them?

> 你知道当你读写原子变量时，它们的发布和获取是如何发生的吗？

Well, it's possible to do a release or acquire _without_ an atomic variable, as well.

> 嗯，也可以在没有原子变量的情况下完成发布或获取。

This is called a _fence_. So if you want all the writes in a thread to be visible elsewhere, you can put up a release fence in one thread and an acquire fence in another, just like with how atomic variables work.

> 这叫做一个_围栏_。因此，如果你想要线程中的所有写入在其他地方可见，你可以在一个线程中设置一个发布围栏，在另一个线程中设置一个获取围栏，就像原子变量一样。

Since a consume operation doesn't really make sense on a fence[^216^], `memory_order_consume` is treated as an acquire.

> 由于对于栅栏 [^216^]来说，消费操作并不是很有意义，因此 `memory_order_consume` 被视为获取操作。

You can put up a fence with any specified order:

::: {#cb769 .sourceCode}

```c
atomic_thread_fence(memory_order_release);
```

:::

There's also a light version of a fence for use with signal handlers, called `atomic_signal_fence()`.

> 也有一个用于信号处理程序的轻量级围栏，称为 `atomic_signal_fence()`。

It works just the same way as `atomic_thread_fence()`, except:

- It only deals with visibility of values within the same thread; there is no synchronization with other threads.

> 它只处理同一个线程内的值的可见性；与其他线程没有同步。

- No hardware fence instructions are emitted.

If you want to be sure the side effects of non-atomic operations (and relaxed atomic operations) are visible in the signal handler, you can use this fence.

> 如果你想确保非原子操作(和松散原子操作)的副作用在信号处理程序中可见，你可以使用这个栅栏。

The idea is that the signal handler is executing in _this_ thread, not another, so this is a lighter-weight way of making sure changes outside the signal handler are visible within it (i.e. they haven't been reordered).

> 这个想法是信号处理程序在这个线程中执行，而不是另一个，因此这是一种更轻量级的方法，可以确保在信号处理程序之外的更改是可见的(即它们没有被重新排序)。

## [40.15] References {#references number="40.15"}

If you want to learn more about this stuff, here are some of the things that helped me plow through it:

> 如果你想学习更多关于这个东西，这里有一些帮助我渡过难关的东西：

- Herb Sutter's _`atomic<>` Weapons_ talk:

  - [Part 1](https://www.youtube.com/watch?v=A8eCGOqgvH4)[^217^]

> - [第一部分](https://www.youtube.com/watch?v=A8eCGOqgvH4)[^217^]

- [part 2](https://www.youtube.com/watch?v=KeLBd2EJLOU)[^218^]

> - [第二部分](https://www.youtube.com/watch?v=KeLBd2EJLOU)[^218^]

- [Jeff Preshing's materials](https://preshing.com/archives/)[^219^], in particular:

  - [An Introduction to Lock-Free Programming](https://preshing.com/20120612/an-introduction-to-lock-free-programming/)[^220^]

> [一个关于无锁编程的介绍](https://preshing.com/20120612/an-introduction-to-lock-free-programming/)[^220^]

- [Acquire and Release Semantics](https://preshing.com/20120913/acquire-and-release-semantics/)[^221^]

> [获取和释放语义](https://preshing.com/20120913/acquire-and-release-semantics/)[^221^]

- [The _Happens-Before_ Relation](https://preshing.com/20130702/the-happens-before-relation/)[^222^]

> [_发生前关系_](https://preshing.com/20130702/the-happens-before-relation/)[^222^]

- [The _Synchronizes-With_ Relation](https://preshing.com/20130823/the-synchronizes-with-relation/)[^223^]

> [同步关系](https://preshing.com/20130823/the-synchronizes-with-relation/)[^223^]

- [The Purpose of `memory_order_consume` in C++11](https://preshing.com/20140709/the-purpose-of-memory_order_consume-in-cpp11/)[^224^]

> [《C++11 中 `memory_order_consume` 的目的》](https://preshing.com/20140709/the-purpose-of-memory_order_consume-in-cpp11/)[^224^]

- [You Can Do Any Kind of Atomic Read-Modify-Write Operation](https://preshing.com/20150402/you-can-do-any-kind-of-atomic-read-modify-write-operation/)[^225^]

> 你可以进行任何类型的原子读-修改-写操作([https://preshing.com/20150402/you-can-do-any-kind-of-atomic-read-modify-write-operation/](https://preshing.com/20150402/you-can-do-any-kind-of-atomic-read-modify-write-operation/))[^225^]

- CPPReference:

  - [Memory Order](https://en.cppreference.com/w/c/atomic/memory_order)[^226^]

> [内存顺序](https://en.cppreference.com/w/c/atomic/memory_order)[^226^]

- [Atomic Types](https://en.cppreference.com/w/c/language/atomic)[^227^]

> - [原子类型](https://en.cppreference.com/w/c/language/atomic)[^227^]

- Bruce Dawson's [Lockless Programming Considerations](https://docs.microsoft.com/en-us/windows/win32/dxtecharts/lockless-programming)[^228^]

> 布鲁斯·道森的[无锁编程考虑](https://docs.microsoft.com/en-us/windows/win32/dxtecharts/lockless-programming)[^228^]

- The helpful and knowledgeable folks on [r/C_Programming](https://www.reddit.com/r/C_Programming/)[^229^]

> 在 [r/C_Programming](https://www.reddit.com/r/C_Programming/) 上有知识渊博且乐于助人的人们 [^229^]。

# [41] Function Specifiers, Alignment Specifiers/Operators {#function-specifiers-alignment-specifiersoperators number="41"}

These don't see a heck of a lot of use in my experience, but we'll cover them here for the sake of completeness.

> 在我的经验中，这些没有太多的用处，但为了完整性，我们还是会涵盖它们。

## [41.1] Function Specifiers {#function-specifiers number="41.1"}

When you declare a function, you can give the compiler a couple tips about how the functions could or will be used. This enables or encourages the compiler to make certain optimizations.

> 当你声明一个函数时，你可以向编译器提供关于函数如何使用的一些提示。这可以促使编译器进行某些优化。

### [41.1.1] `inline` for Speed---Maybe {#inline-for-speedmaybe number="41.1.1"}

You can declare a function to be inline like this:

::: {#cb770 .sourceCode}

```c
static inline int add(int x, int y) {
    return x + y;
}
```

:::

This is meant to encourage the compiler to make this function call as fast as possible. And, historically, one way to do this was _inlining_, which means that the body of the function would be embedded in its entirety where the call was made. This would avoid all the overhead of setting up the function call and tearing it down at the expense of larger code size as the function was copied all over the place instead of being reused.

> 这是为了鼓励编译器尽可能快地调用此函数。从历史上看，一种做法是_内联_，这意味着函数的主体将完整地嵌入调用处。这将避免设置函数调用和拆解它的开销，但代价是代码大小增加，因为函数被复制到各个地方，而不是被重复使用。

That would seem to be the end of the story, but it's not. `inline` comes with a whole pile of rules that make for _interesting times_. I'm not sure I even understand them all, and behavior seems to vary from compiler to compiler.

> 看起来这就是故事的结局，但事实并非如此。`inline` 带来了一大堆规则，让人们过上有趣的时光。我甚至不确定我是否完全理解它们，而且各种编译器的行为似乎也有所不同。

The short answer is define the `inline` function as `static` in the file that you need it. And then use it in that one file. And you never have to worry about the rest of it.

> 简短的答案是：在需要使用它的文件中将 `inline` 函数定义为 `static`。然后只在该文件中使用它，不用担心其他问题。

But if you're wondering, here are more fun times.

Let's try leaving the `static` off.

::: {#cb771 .sourceCode}

```c
#include <stdio.h>

inline int add(int x, int y)
{
    return x + y;
}

int main(void)
{
    printf("%d\n", add(1, 2));
}
```

:::

`gcc` gives a linker error on `add()`... unless you compile with optimizations on (probably)!

See, a compiler can choose to inline or not, but if it chooses not to, you're left with no function at all. `gcc` doesn't inline unless you're doing an optimized build.

> 看到，编译器可以选择内联或不内联，但如果它选择不内联，你就没有函数了。除非你做优化构建，否则 `gcc` 不会内联。

One way around this is to define a non-`inline` external linkage version of the function elsewhere, and that one will be used when the `inline` one isn't. But you as the programmer can't determine which, portably. If both are available, it's unspecified which one the compiler chooses. With `gcc` the inline function will be used if you're compiling with optimizations, and the non-inline one will be used otherwise. Even if the bodies of these functions are completely different. Zany!

> 一种解决方法是在其他地方定义一个非内联外部链接版本的函数，当内联函数不可用时，就会使用该函数。但是作为程序员，您无法确定哪一个是可移植的。如果两者都可用，则编译器选择哪一个是未指定的。使用 `gcc` 编译时，如果您使用优化，则会使用内联函数，否则会使用非内联函数。即使这些函数的函数体完全不同，也是如此！太疯狂了！

Another way is to declare the function as `extern inline`. This will attempt to inline in this file, but will also create a version with external linkage. And so `gcc` will use one or the other depending on optimizations, but at least they're the same function.

> 另一种方法是将函数声明为 `extern inline`。 这将尝试在此文件中内联，但也将创建具有外部链接的版本。 因此，根据优化，`gcc` 将使用其中一个或另一个，但至少它们是相同的函数。

Unless, of course, you have another source file with an `inline` function of the same name; it will use its `inline` function or the one with external linkage depending on optimizations.

> 除非你有另一个具有相同名称的内联函数的源文件；它将根据优化来使用内联函数或外部连接函数。

But let's say you're doing a build where the compiler _is_ inlining the function. In that case, you can just use a plain `inline` in the definition. However, there are now additional restrictions.

> 但是假设你正在进行编译，其中编译器正在内联函数。在这种情况下，你可以在定义中只使用一个普通的 `inline`。但是，现在有了额外的限制。

You can't refer to any `static` globals:

::: {#cb772 .sourceCode}

```c
static int b = 13;

inline int add(int x, int y)
{
    return x + y + b;  // BAD -- can't refer to b
}
```

:::

And you can't define any non-`const` `static` local variables:

::: {#cb773 .sourceCode}

```c
inline int add(int x, int y)
{
    static int b = 13;  // BAD -- can't define static

    return x + y + b;
}
```

:::

But making it `const` is OK:

::: {#cb774 .sourceCode}

```c
inline int add(int x, int y)
{
    static const int b = 13;  // OK -- static const

    return x + y + b;
}
```

:::

Now, you know the functions are `extern` by default, so we should be able to call `add()` from another file. You'd like to think that, wouldn't you!

> 现在，你知道函数默认是 `extern` 的，所以我们应该能够从另一个文件调用 `add()`。你想这样，不是吗！

But you can't! If it's just a plain `inline`, it's similar to `static`: it's only visible in that file.

> 但是你不能！如果它只是一个普通的“内联”，它类似于“静态”：它只能在该文件中可见。

Okay, so what if you throw an `extern` on there? Now we're coming full circle to when we discussed having `inline` mixed with functions with external linkage.

> 好吧，如果你在那里抛出一个 `extern`，怎么样？现在我们回到了我们讨论把 `inline` 与具有外部链接的函数混合在一起的时候。

If both are visible, the compiler can choose which to use.

Let's do a demo of this behavior. We'll have two files, `foo.c` and `bar.c`. They'll both call `func()` which is `inline` in `foo.c` and external linkage in `bar.c`.

> 让我们做一个这种行为的演示。我们将有两个文件，`foo.c` 和 `bar.c`。它们都会调用 `func()`，它在 `foo.c` 中是内联的，在 `bar.c` 中是外部链接的。

Here's `foo.c` with the `inline`.

::: {#cb775 .sourceCode}

```c
// foo.c

#include <stdio.h>

inline char *func(void)
{
    return "foo's function";
}

int main(void)
{
    printf("foo.c: %s\n", func());

    void bar(void);
    bar();
}
```

:::

Recall that unless we're doing an optimized build with `gcc`. `func()` will vanish and we'll get a linker error. Unless, or course, we have a version with external linkage defined elsewhere.

> 如果我们不使用 gcc 进行优化构建，请记住，`func()` 将消失，我们将得到一个链接器错误。除非，当然，我们有一个具有外部链接定义的版本。

And we do. In `bar.c`.

::: {#cb776 .sourceCode}

```c
// bar.c

#include <stdio.h>

char *func(void)
{
    return "bar's function";
}

void bar(void)
{
    printf("bar.c: %s\n", func());
}
```

:::

So the question is, what is the output?

Seems like when we call `func()` from `foo.c`, it should print "`foo's function`". And from `bar.c`, that `func()` should print "`bar's function`".

> 似乎当我们从 foo.c 调用 func()时，它应该打印“foo 的函数”。而从 bar.c，该 func()应该打印“bar 的函数”。

And if I compile with `gcc` with optimizations[^230^] it will use inline functions, and we'll get the expected:

> 如果我使用 `gcc` 进行优化编译[^230^]，它将使用内联函数，我们将得到预期的结果：

::: {#cb777 .sourceCode}

```{.sourceCode .default}
foo.c: foo's function
bar.c: bar's function
```

:::

Great!

But if we compile in `gcc` without optimizations, it ignores the inline function and uses the external linkage `func()` from `bar.c`! And we get this:

> 但是如果我们在 gcc 中不使用优化，它会忽略内联函数，并使用来自 bar.c 的外部链接 func！然后我们得到这个：

::: {#cb778 .sourceCode}

```{.sourceCode .default}
foo.c: bar's function
bar.c: bar's function
```

:::

In short, the rules are surprisingly complex. I give myself a good 30% chance of having described them correctly.

> 总之，规则非常复杂。我给自己一个很好的 30% 的机会来正确描述它们。

### [41.1.2] `noreturn` and `_Noreturn` {#noreturn number="41.1.2"}

This indicates to the compiler that a particular function will not ever return to its caller, i.e. the program will exit by some mechanism before the function returns.

> 这表明编译器，某个特定的函数永远不会返回其调用者，即在函数返回之前，程序将通过某种机制退出。

It allows the compiler to perhaps perform some optimizations around the function call.

> 它允许编译器可能在函数调用周围执行一些优化。

It also allows you to indicate to other devs that some program logic depends on a function _not_ returning.

> 它还允许您向其他开发人员指示某些程序逻辑取决于一个函数_不_返回。

You'll likely never need to use this, but you'll see it on some library calls like [`exit()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-exit)[^231^] and [`abort()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-abort)[^232^].

> 你很可能永远不需要使用这个，但你会在一些像[`exit()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-exit)[^231^]和[`abort()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-abort)[^232^]的库调用中看到它。

The built-in keyword is `_Noreturn`, but if it doesn't break your existing code, everyone would recommend including `<stdnoreturn.h>` and using the easier-to-read `noreturn` instead.

> 内置的关键字是 `_Noreturn`，但如果不破坏现有代码，大家都会建议包含 `<stdnoreturn.h>` 并使用更易读的 `noreturn`。

It's undefined behavior if a function specified as `noreturn` actually does return. It's computationally dishonest, see.

> 这是一种未定义的行为，如果一个被指定为“noreturn”的函数实际上却返回了，这是计算上不诚实的，你懂的。

Here's an example of using `noreturn` correctly:

::: {#cb779 .sourceCode}

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdnoreturn.h>

noreturn void foo(void) // This function should never return!
{
    printf("Happy days\n");

    exit(1);            // And it doesn't return--it exits here!
}

int main(void)
{
    foo();
}
```

:::

If the compiler detects that a `noreturn` function could return, it might warn you, helpfully.

> 如果编译器检测到一个 `noreturn` 函数可能会返回，它可能会给你友好地发出警告。

Replacing the `foo()` function with this:

::: {#cb780 .sourceCode}

```c
noreturn void foo(void)
{
    printf("Breakin' the law\n");
}
```

:::

gets me a warning:

::: {#cb781 .sourceCode}

```{.sourceCode .default}
foo.c:7:1: warning: function declared 'noreturn' should not return
```

:::

## [41.2] Alignment Specifiers and Operators {#alignment-specifiers-and-operators number="41.2"}

[_Alignment_](https://en.wikipedia.org/wiki/Data_structure_alignment)[^233^] is all about multiples of addresses on which objects can be stored. Can you store this at any address? Or must it be a starting address that's divisible by 2? Or 8? Or 16?

> [_对齐_](https://en.wikipedia.org/wiki/Data_structure_alignment)[^233^]是关于可以存储对象的多个地址的事情。你可以在任何地址存储它吗？还是必须是可以被 2 整除的起始地址？或者 8？或者 16？

If you're coding up something low-level like a memory allocator that interfaces with your OS, you might need to consider this. Most devs go their careers without using this functionality in C.

> 如果你正在编写一些低级别的东西，比如与操作系统接口的内存分配器，你可能需要考虑这一点。大多数开发人员在使用 C 语言时都不会使用这种功能。

### [41.2.1] `alignas` and `_Alignas` {#alignas-and-\_alignas number="41.2.1"}

This isn't a function. Rather, it's an _alignment specifier_ that you can use with a variable declaration.

> 这不是一个函数，而是一个可以用于变量声明的对齐指定符。

The built-in specifier is `_Alignas`, but the header `<stdalign.h>` defines it as `alignas` for something better looking.

> 内置的说明符是 `_Alignas`，但头文件 `<stdalign.h>` 将其定义为 `alignas`，以获得更好的外观。

If you need your `char` to be aligned like an `int`, you can force it like this when you declare it:

> 如果你需要将你的 `char` 类型像 `int` 一样对齐，你可以在声明时强制这样做：

::: {#cb782 .sourceCode}

```c
char alignas(int) c;
```

:::

You can also pass a constant value or expression in for the alignment. This has to be something supported by the system, but the spec stops short of dictating what values you can put in there. Small powers of 2 (1, 2, 4, 8, and 16) are generally safe bets.

> 你也可以传入一个常量值或表达式来进行对齐。这必须是系统支持的，但规范并不强制你使用什么值。2 的小次幂(1，2，4，8 和 16)通常是安全的选择。

::: {#cb783 .sourceCode}

```c
char alignas(8) c;   // align on 8-byte boundaries
```

:::

If you want to align at the maximum used alignment by your system, include `<stddef.h>` and use the type `max_align_t`, like so:

> 如果你想要对齐系统中使用的最大对齐，请包含 `<stddef.h>` 并使用类型 `max_align_t`，如下所示：

::: {#cb784 .sourceCode}

```c
char alignas(max_align_t) c;
```

:::

You could potentially _over-align_ by specifying an alignment more than that of `max_align_t`, but whether or not such things are allowed is system dependent.

> 你可能会通过指定比 `max_align_t` 更高的对齐来过度对齐，但是是否允许这样的事情取决于系统。

### [41.2.2] `alignof` and `_Alignof` {#alignof-and-\_alignof number="41.2.2"}

This operator will return the address multiple a particular type uses for alignment on this system. For example, maybe `char` s are aligned every 1 address, and `int` s are aligned every 4 addresses.

> 这个操作符将返回特定类型在此系统上用于对齐的地址。例如，也许 `char` 每 1 个地址对齐，而 `int` 每 4 个地址对齐。

The built-in operator is `_Alignof`, but the header `<stdalign.h>` defines it as `alignof` if you want to look cooler.

> 内置操作符是 `_Alignof`，但头文件 `<stdalign.h>` 将其定义为 `alignof`，如果你想看起来更酷一点。

Here's a program that will print out the alignments of a variety of different types. Again, these will vary from system to system. Note that the type `max_align_t` will give you the maximum alignment used by the system.

> 这里有一个程序，可以打印出各种不同类型的对齐方式。同样，这些将因系统而异。注意，类型 `max_align_t` 将给您系统使用的最大对齐方式。

::: {#cb785 .sourceCode}

```c
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

::: {#cb786 .sourceCode}

```{.sourceCode .default}
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

And there you have it. Alignment!

::: {#footnotes .section .footnotes .footnotes-end-of-document role="doc-endnotes"}

---

1. ::: {#fn1}

   [https://www.ioccc.org/](https://www.ioccc.org/)[↩︎](#fnref1){.footnote-back role="doc-backlink"}

> [https://www.ioccc.org/](https://www.ioccc.org/)[↩︎](#fnref1){.footnote-back role="doc-backlink"}

请访问 [https://www.ioccc.org/](https://www.ioccc.org/)[↩︎](#fnref1){.footnote-back role="doc-backlink"}
:::
2. ::: {#fn2}

[https://en.wikipedia.org/wiki/Python](https://en.wikipedia.org/wiki/Python)\_(programming_language)[↩︎](#fnref2){.footnote-back role="doc-backlink"}

> [Python(编程语言)](https://zh.wikipedia.org/wiki/Python)↩︎
> :::

3. ::: {#fn3}

   [https://en.wikipedia.org/wiki/JavaScript](https://en.wikipedia.org/wiki/JavaScript)[↩︎](#fnref3){.footnote-back role="doc-backlink"}

> [JavaScript(简体中文)](https://zh.wikipedia.org/wiki/JavaScript)↩︎
> :::

4. ::: {#fn4}

   [https://en.wikipedia.org/wiki/Java](https://en.wikipedia.org/wiki/Java)\_(programming_language)[↩︎](#fnref4){.footnote-back role="doc-backlink"}

> [维基百科：Java(编程语言)](https://zh.wikipedia.org/wiki/Java_(%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80))↩︎
> :::

5. ::: {#fn5}

   [https://en.wikipedia.org/wiki/Rust](https://en.wikipedia.org/wiki/Rust)\_(programming_language)[↩︎](#fnref5){.footnote-back role="doc-backlink"}

> [Rust(编程语言)](https://zh.wikipedia.org/wiki/Rust)↩︎
> :::

6. ::: {#fn6}

   [https://en.wikipedia.org/wiki/Go](https://en.wikipedia.org/wiki/Go)\_(programming_language)[↩︎](#fnref6){.footnote-back role="doc-backlink"}

> [Go(编程语言)](https://zh.wikipedia.org/wiki/Go_(%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80))↩︎{.footnote-back role="doc-backlink"}
> :::

7. ::: {#fn7}

   [https://en.wikipedia.org/wiki/Swift](https://en.wikipedia.org/wiki/Swift)\_(programming_language)[↩︎](#fnref7){.footnote-back role="doc-backlink"}

> [https://zh.wikipedia.org/wiki/Swift](https://zh.wikipedia.org/wiki/Swift)(编程语言)[↩︎](#fnref7){.footnote-back role="doc-backlink"}
> :::

8. ::: {#fn8}

   [https://en.wikipedia.org/wiki/Objective-C](https://en.wikipedia.org/wiki/Objective-C)[↩︎](#fnref8){.footnote-back role="doc-backlink"}

> [Objective-C(目标 C)](https://zh.wikipedia.org/wiki/Objective-C)
> :::

9. ::: {#fn9}

   https://beej.us/guide/bgclr/[↩︎](#fnref9){.footnote-back role="doc-backlink"}

> https://beej.us/guide/bgclr/[↩︎](#fnref9){.footnote-back role="doc-backlink"}
> :::

10. ::: {#fn10}
    [https://en.wikipedia.org/wiki/ANSI_C](https://en.wikipedia.org/wiki/ANSI_C)[↩︎](#fnref10){.footnote-back role="doc-backlink"}
    :::
11. ::: {#fn11}
    [https://en.wikipedia.org/wiki/POSIX](https://en.wikipedia.org/wiki/POSIX)[↩︎](#fnref11){.footnote-back role="doc-backlink"}
    :::
12. ::: {#fn12}
    [https://visualstudio.microsoft.com/vs/community/](https://visualstudio.microsoft.com/vs/community/)[↩︎](#fnref12){.footnote-back role="doc-backlink"}
    :::
13. ::: {#fn13}
    [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)[↩︎](#fnref13){.footnote-back role="doc-backlink"}
    :::
14. ::: {#fn14}
    [https://developer.apple.com/xcode/](https://developer.apple.com/xcode/)[↩︎](#fnref14){.footnote-back role="doc-backlink"}
    :::
15. ::: {#fn15}
    https://beej.us/guide/bgc/[↩︎](#fnref15){.footnote-back role="doc-backlink"}
    :::
16. ::: {#fn16}
    [https://en.cppreference.com/](https://en.cppreference.com/)[↩︎](#fnref16){.footnote-back role="doc-backlink"}
    :::
17. ::: {#fn17}
    [https://groups.google.com/g/comp.lang.c](https://groups.google.com/g/comp.lang.c)[↩︎](#fnref17){.footnote-back role="doc-backlink"}
    :::
18. ::: {#fn18}
    [https://www.reddit.com/r/C_Programming/](https://www.reddit.com/r/C_Programming/)[↩︎](#fnref18){.footnote-back role="doc-backlink"}
    :::
19. ::: {#fn19}
    [https://en.wikipedia.org/wiki/Assembly_language](https://en.wikipedia.org/wiki/Assembly_language)[↩︎](#fnref19){.footnote-back role="doc-backlink"}
    :::
20. ::: {#fn20}
    [https://en.wikipedia.org/wiki/Bare_machine](https://en.wikipedia.org/wiki/Bare_machine)[↩︎](#fnref20){.footnote-back role="doc-backlink"}
    :::
21. ::: {#fn21}
    [https://en.wikipedia.org/wiki/Operating_system](https://en.wikipedia.org/wiki/Operating_system)[↩︎](#fnref21){.footnote-back role="doc-backlink"}
    :::
22. ::: {#fn22}
    [https://en.wikipedia.org/wiki/Embedded_system](https://en.wikipedia.org/wiki/Embedded_system)[↩︎](#fnref22){.footnote-back role="doc-backlink"}
    :::
23. ::: {#fn23}
    [https://en.wikipedia.org/wiki/Rust](https://en.wikipedia.org/wiki/Rust)\_(programming_language)[↩︎](#fnref23){.footnote-back role="doc-backlink"}
    :::
24. ::: {#fn24}
    [https://en.wikipedia.org/wiki/Grok](https://en.wikipedia.org/wiki/Grok)[↩︎](#fnref24){.footnote-back role="doc-backlink"}
    :::
25. ::: {#fn25}
    I know someone will fight me on that, but it's gotta be at least in the top three, right?[↩︎](#fnref25){.footnote-back role="doc-backlink"}
    :::
26. ::: {#fn26}
    Well, technically there are more than two, but hey, let's pretend there are two---ignorance is bliss, right?[↩︎](#fnref26){.footnote-back role="doc-backlink"}
    :::
27. ::: {#fn27}
    [https://en.wikipedia.org/wiki/Assembly_language](https://en.wikipedia.org/wiki/Assembly_language)[↩︎](#fnref27){.footnote-back role="doc-backlink"}
    :::
28. ::: {#fn28}
    [https://en.wikipedia.org/wiki/Machine_code](https://en.wikipedia.org/wiki/Machine_code)[↩︎](#fnref28){.footnote-back role="doc-backlink"}
    :::
29. ::: {#fn29}
    Technically, it contains preprocessor directives and function prototypes (more on that later) for common input and output needs.[↩︎](#fnref29){.footnote-back role="doc-backlink"}
    :::
30. ::: {#fn30}
    [https://en.wikipedia.org/wiki/Unix](https://en.wikipedia.org/wiki/Unix)[↩︎](#fnref30){.footnote-back role="doc-backlink"}
    :::
31. ::: {#fn31}
    If you don't give it an output filename, it will export to a file called `a.out` by default---this filename has its roots deep in Unix history.[↩︎](#fnref31){.footnote-back role="doc-backlink"}
    :::
32. ::: {#fn32}
    https://formulae.brew.sh/formula/gcc[↩︎](#fnref32){.footnote-back role="doc-backlink"}
    :::
33. ::: {#fn33}
    A "byte" is typically an 8-bit binary number. Think of it as an integer that can only hold the values from 0 to 255, inclusive. Technically, C allows bytes to be any number of bits and if you want to unambiguously refer to an 8-bit number, you should use the term _octet_. But programmers are going assume you mean 8-bits when you say "byte" unless you specify otherwise.[↩︎](#fnref33){.footnote-back role="doc-backlink"}
    :::
34. ::: {#fn34}
    I'm seriously oversimplifying how modern memory works, here. But the mental model works, so please forgive me.[↩︎](#fnref34){.footnote-back role="doc-backlink"}
    :::
35. ::: {#fn35}
    I'm lying here a little. Technically `3.14159` is of type `double`, but we're not there yet and I want you to associate `float` with "Floating Point", and C will happily coerce that type into a `float`. In short, don't worry about it until later.[↩︎](#fnref35){.footnote-back role="doc-backlink"}
    :::
36. ::: {#fn36}
    Read this as "pointer to a char" or "char pointer". "Char" for character. Though I can't find a study, it seems anecdotally most people pronounce this as "char", a minority say "car", and a handful say "care". We'll talk more about pointers later.[↩︎](#fnref36){.footnote-back role="doc-backlink"}
    :::
37. ::: {#fn37}
    Colloquially, we say they have "random" values, but they aren't truly---or even pseudo-truly---random numbers.[↩︎](#fnref37){.footnote-back role="doc-backlink"}
    :::
38. ::: {#fn38}
    This isn't strictly 100% true. When we get to learning about static storage duration, you'll find the some variables are initialized to zero automatically. But the safe thing to do is always initialize them.[↩︎](#fnref38){.footnote-back role="doc-backlink"}
    :::
39. ::: {#fn39}
    The `_t` is short for `type`.[↩︎](#fnref39){.footnote-back role="doc-backlink"}
    :::
40. ::: {#fn40}
    Except for with variable length arrays---but that's a story for another time.[↩︎](#fnref40){.footnote-back role="doc-backlink"}
    :::
41. ::: {#fn41}
    https://beej.us/guide/bgclr/html/split/stdlib.html#man-srand[↩︎](#fnref41){.footnote-back role="doc-backlink"}
    :::
42. ::: {#fn42}
    This was considered such a hazard that the designers of the Go Programming Language made `break` the default; you have to explicitly use Go's `fallthrough` statement if you want to fall into the next case.[↩︎](#fnref42){.footnote-back role="doc-backlink"}
    :::
43. ::: {#fn43}
    Never say "never".[↩︎](#fnref43){.footnote-back role="doc-backlink"}
    :::
44. ::: {#fn44}
    Typically. I'm sure there are exceptions out there in the dark corridors of computing history.[↩︎](#fnref44){.footnote-back role="doc-backlink"}
    :::
45. ::: {#fn45}
    A byte is a number made up of no more than 8 binary digits, or _bits_ for short. This means in decimal digits just like grandma used to use, it can hold an unsigned number between 0 and 255, inclusive.[↩︎](#fnref45){.footnote-back role="doc-backlink"}
    :::
46. ::: {#fn46}
    The order that bytes come in is referred to as the _endianness_ of the number. The usual suspects are _big-endian_ (with the most significant byte first) and _little-endian_ (with the most-significant byte last), or, uncommonly now, _mixed-endian_ (with the most-significant bytes somewhere else).[↩︎](#fnref46){.footnote-back role="doc-backlink"}
    :::
47. ::: {#fn47}
    That is, base 16 with digits 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, and F.[↩︎](#fnref47){.footnote-back role="doc-backlink"}
    :::
48. ::: {#fn48}
    That's not all! It's used in `/*comments*/` and multiplication and in function prototypes with variable length arrays! It's all the same `*`, but the context gives it different meaning.[↩︎](#fnref48){.footnote-back role="doc-backlink"}
    :::
49. ::: {#fn49}
    [https://en.wikipedia.org/wiki/Null_pointer#History](https://en.wikipedia.org/wiki/Null_pointer#History)[↩︎](#fnref49){.footnote-back role="doc-backlink"}
    :::
50. ::: {#fn50}
    [https://en.wikipedia.org/wiki/Sentinel_value](https://en.wikipedia.org/wiki/Sentinel_value)[↩︎](#fnref50){.footnote-back role="doc-backlink"}
    :::
51. ::: {#fn51}
    The pointer type variables are `a`, `d`, `f`, and `i`, because those are the ones with `*` in front of them.[↩︎](#fnref51){.footnote-back role="doc-backlink"}
    :::
52. ::: {#fn52}
    These days, anyway.[↩︎](#fnref52){.footnote-back role="doc-backlink"}
    :::
53. ::: {#fn53}
    Again, not really, but variable-length arrays---of which I'm not really a fan---are a story for another time.[↩︎](#fnref53){.footnote-back role="doc-backlink"}
    :::
54. ::: {#fn54}
    Since arrays are just pointers to the first element of the array under the hood, there's no additional information recording the length.[↩︎](#fnref54){.footnote-back role="doc-backlink"}
    :::
55. ::: {#fn55}
    Because when you pass an array to a function, you're actually just passing a pointer to the first element of that array, not the "entire" array.[↩︎](#fnref55){.footnote-back role="doc-backlink"}
    :::
56. ::: {#fn56}
    In the good old MS-DOS days before memory protection was a thing, I was writing some particularly abusive C code that deliberately engaged in all kinds of undefined behavior. But I knew what I was doing, and things were working pretty well. Until I made a misstep that caused a lockup and, as I found upon reboot, nuked all my BIOS settings. That was fun. (Shout-out to [\@man]{.citation cites="man"} for those fun times.)[↩︎](#fnref56){.footnote-back role="doc-backlink"}
    :::
57. ::: {#fn57}
    There are a lot of things that cause undefined behavior, not just out-of-bounds array accesses. This is what makes the C language so _exciting_.[↩︎](#fnref57){.footnote-back role="doc-backlink"}
    :::
58. ::: {#fn58}
    [https://en.wikipedia.org/wiki/Row](https://en.wikipedia.org/wiki/Row)-\_and_column-major_order[↩︎](#fnref58){.footnote-back role="doc-backlink"}
    :::
59. ::: {#fn59}
    This is technically incorrect, as a pointer to an array and a pointer to the first element of an array have different types. But we can burn that bridge when we get to it.[↩︎](#fnref59){.footnote-back role="doc-backlink"}
    :::
60. ::: {#fn60}
    C11 §6.7.6.2¶1 requires it be greater than zero. But you might see code out there with arrays declared of zero length at the end of `struct` s and GCC is particularly lenient about it unless you compile with `-pedantic`. This zero-length array was a hackish mechanism for making variable-length structures. Unfortunately, it's technically undefined behavior to access such an array even though it basically worked everywhere. C99 codified a well-defined replacement for it called _flexible array members_, which we'll chat about later.[↩︎](#fnref60){.footnote-back role="doc-backlink"}
    :::
61. ::: {#fn61}
    This is also equivalent: `void print_2D_array(int (*a)[3])`, but that's more than I want to get into right now.[↩︎](#fnref61){.footnote-back role="doc-backlink"}
    :::
62. ::: {#fn62}
    Though it is true that C doesn't track the length of strings.[↩︎](#fnref62){.footnote-back role="doc-backlink"}
    :::
63. ::: {#fn63}
    If you're using the basic character set or an 8-bit character set, you're used to one character being one byte. This isn't true in all character encodings, though.[↩︎](#fnref63){.footnote-back role="doc-backlink"}
    :::
64. ::: {#fn64}
    This is different than the `NULL` pointer, and I'll abbreviate it `NUL` when talking about the character versus `NULL` for the pointer.[↩︎](#fnref64){.footnote-back role="doc-backlink"}
    :::
65. ::: {#fn65}
    Later we'll learn a neater way to do it with pointer arithmetic.[↩︎](#fnref65){.footnote-back role="doc-backlink"}
    :::
66. ::: {#fn66}
    There's a safer function called `strncpy()` that you should probably use instead, but we'll get to that later.[↩︎](#fnref66){.footnote-back role="doc-backlink"}
    :::
67. ::: {#fn67}
    Although in C individual items in memory like `int` s are referred to as "objects", they're not objects in an object-oriented programming sense.[↩︎](#fnref67){.footnote-back role="doc-backlink"}
    :::
68. ::: {#fn68}
    The Saturn was a popular brand of economy car in the United States until it was put out of business by the 2008 crash, sadly so to us fans.[↩︎](#fnref68){.footnote-back role="doc-backlink"}
    :::
69. ::: {#fn69}
    A pointer is likely 8 bytes on a 64-bit system.[↩︎](#fnref69){.footnote-back role="doc-backlink"}
    :::
70. ::: {#fn70}
    A _deep copy_ follows pointer in the `struct` and copies the data they point to, as well. A _shallow copy_ just copies the pointers, but not the things they point to. C doesn't come with any built-in deep copy functionality.[↩︎](#fnref70){.footnote-back role="doc-backlink"}
    :::
71. ::: {#fn71}
    https://beej.us/guide/bgclr/html/split/stringref.html#man-strcmp[↩︎](#fnref71){.footnote-back role="doc-backlink"}
    :::
72. ::: {#fn72}
    https://beej.us/guide/bgclr/html/split/stringref.html#man-memset[↩︎](#fnref72){.footnote-back role="doc-backlink"}
    :::
73. ::: {#fn73}
    [https://stackoverflow.com/questions/141720/how-do-you-compare-structs-for-equality-in-c](https://stackoverflow.com/questions/141720/how-do-you-compare-structs-for-equality-in-c)[↩︎](#fnref73){.footnote-back role="doc-backlink"}
    :::
74. ::: {#fn74}
    We used to have three different newlines in broad effect: Carriage Return (CR, used on old Macs), Linefeed (LF, used on Unix systems), and Carriage Return/Linefeed (CRLF, used on Windows systems). Thankfully the introduction of OS X, being Unix-based, reduced this number to two.[↩︎](#fnref74){.footnote-back role="doc-backlink"}
    :::
75. ::: {#fn75}
    If the buffer's not big enough to read in an entire line, it'll just stop reading mid-line, and the next call to `fgets()` will continue reading the rest of the line.[↩︎](#fnref75){.footnote-back role="doc-backlink"}
    :::
76. ::: {#fn76}
    Normally the second program would read all the bytes at once, and _then_ print them out in a loop. That would be more efficient. But we're going for demo value, here.[↩︎](#fnref76){.footnote-back role="doc-backlink"}
    :::
77. ::: {#fn77}
    [https://en.wikipedia.org/wiki/Hex_dump](https://en.wikipedia.org/wiki/Hex_dump)[↩︎](#fnref77){.footnote-back role="doc-backlink"}
    :::
78. ::: {#fn78}
    [https://en.wikipedia.org/wiki/Endianess](https://en.wikipedia.org/wiki/Endianess)[↩︎](#fnref78){.footnote-back role="doc-backlink"}
    :::
79. ::: {#fn79}
    And this is why I used individual bytes in my `fwrite()` and `fread()` examples, above, shrewdly.[↩︎](#fnref79){.footnote-back role="doc-backlink"}
    :::
80. ::: {#fn80}
    [https://en.wikipedia.org/wiki/Protocol_buffers](https://en.wikipedia.org/wiki/Protocol_buffers)[↩︎](#fnref80){.footnote-back role="doc-backlink"}
    :::
81. ::: {#fn81}
    We'll talk more about these later.[↩︎](#fnref81){.footnote-back role="doc-backlink"}
    :::
82. ::: {#fn82}
    Recall that the `sizeof` operator tells you the size in bytes of an object in memory.[↩︎](#fnref82){.footnote-back role="doc-backlink"}
    :::
83. ::: {#fn83}
    Or string, which is really an array of `char` s. Somewhat peculiarly, you can also have a pointer that references _one past_ the end of the array without a problem and still do math on it. You just can't dereference it when it's out there.[↩︎](#fnref83){.footnote-back role="doc-backlink"}
    :::
84. ::: {#fn84}
    https://beej.us/guide/bgclr/html/split/stdlib.html#man-qsort[↩︎](#fnref84){.footnote-back role="doc-backlink"}
    :::
85. ::: {#fn85}
    https://beej.us/guide/bgclr/html/split/stdlib.html#man-bsearch[↩︎](#fnref85){.footnote-back role="doc-backlink"}
    :::
86. ::: {#fn86}
    Because remember that array notation is just a dereference and some pointer math, and you can't dereference a `void*`![↩︎](#fnref86){.footnote-back role="doc-backlink"}
    :::
87. ::: {#fn87}
    You can also _cast_ the `void*` to another type, but we haven't gotten to casts yet.[↩︎](#fnref87){.footnote-back role="doc-backlink"}
    :::
88. ::: {#fn88}
    Or until the program exits, in which case all the memory allocated by it is freed. Asterisk: some systems allow you to allocate memory that persists after a program exits, but it's system dependent, out of scope for this guide, and you'll certainly never do it on accident.[↩︎](#fnref88){.footnote-back role="doc-backlink"}
    :::
89. ::: {#fn89}
    [http://www.open-std.org/jtc1/sc22/wg14/www/docs/summary.htm#dr_460](http://www.open-std.org/jtc1/sc22/wg14/www/docs/summary.htm#dr_460)[↩︎](#fnref89){.footnote-back role="doc-backlink"}
    :::
90. ::: {#fn90}
    [https://en.wikipedia.org/wiki/Bit_bucket](https://en.wikipedia.org/wiki/Bit_bucket)[↩︎](#fnref90){.footnote-back role="doc-backlink"}
    :::
91. ::: {#fn91}
    "Bit" is short for _binary digit_. Binary is just another way of representing numbers. Instead of digits 0-9 like we're used to, it's digits 0-1.[↩︎](#fnref91){.footnote-back role="doc-backlink"}
    :::
92. ::: {#fn92}
    [https://en.wikipedia.org/wiki/Two%27s_complement](https://en.wikipedia.org/wiki/Two%27s_complement)[↩︎](#fnref92){.footnote-back role="doc-backlink"}
    :::
93. ::: {#fn93}
    The industry term for a sequence of exactly, indisputably 8 bits is an _octet_.[↩︎](#fnref93){.footnote-back role="doc-backlink"}
    :::
94. ::: {#fn94}
    In general, f you have an [\\(n\\)]{.math .inline} bit two's complement number, the signed range is [\\(-2\^{n-1}\\)]{.math .inline} to [\\(2\^{n-1}-1\\)]{.math .inline}. And the unsigned range is [\\(0\\)]{.math .inline} to [\\(2\^n-1\\)]{.math .inline}.[↩︎](#fnref94){.footnote-back role="doc-backlink"}
    :::
95. ::: {#fn95}
    [https://en.wikipedia.org/wiki/ASCII](https://en.wikipedia.org/wiki/ASCII)[↩︎](#fnref95){.footnote-back role="doc-backlink"}
    :::
96. ::: {#fn96}
    [https://en.wikipedia.org/wiki/List_of_information_system_character_sets](https://en.wikipedia.org/wiki/List_of_information_system_character_sets)[↩︎](#fnref96){.footnote-back role="doc-backlink"}
    :::
97. ::: {#fn97}
    [https://en.wikipedia.org/wiki/Unicode](https://en.wikipedia.org/wiki/Unicode)[↩︎](#fnref97){.footnote-back role="doc-backlink"}
    :::
98. ::: {#fn98}
    Depends on if a `char` defaults to `signed char` or `unsigned char`[↩︎](#fnref98){.footnote-back role="doc-backlink"}
    :::
99. ::: {#fn99}
    [https://en.wikipedia.org/wiki/Signed_number_representations#Signed_magnitude_representation](https://en.wikipedia.org/wiki/Signed_number_representations#Signed_magnitude_representation)[↩︎](#fnref99){.footnote-back role="doc-backlink"}
    :::
100. ::: {#fn100}
     My `char` is signed.[↩︎](#fnref100){.footnote-back role="doc-backlink"}
     :::
101. ::: {#fn101}
     [https://en.wikipedia.org/wiki/IEEE_754](https://en.wikipedia.org/wiki/IEEE_754)[↩︎](#fnref101){.footnote-back role="doc-backlink"}
     :::
102. ::: {#fn102}
     This program runs as its comments indicate on a system with `FLT_DIG` of `6` that uses IEEE-754 base-2 floating point numbers. Otherwise, you might get different output.[↩︎](#fnref102){.footnote-back role="doc-backlink"}
     :::
103. ::: {#fn103}
     It's really surprising to me that C doesn't have this in the spec yet. In the C99 Rationale document, they write, "A proposal to add binary constants was rejected due to lack of precedent and insufficient utility." Which seems kind of silly in light of some of the other features they kitchen-sinked in there! I'll bet one of the next releases has it.[↩︎](#fnref103){.footnote-back role="doc-backlink"}
     :::
104. ::: {#fn104}
     [https://en.wikipedia.org/wiki/Scientific_notation](https://en.wikipedia.org/wiki/Scientific_notation)[↩︎](#fnref104){.footnote-back role="doc-backlink"}
     :::
105. ::: {#fn105}
     They're the same except `snprintf()` allows you to specify a maximum number of bytes to output, preventing the overrunning of the end of your string. So it's safer.[↩︎](#fnref105){.footnote-back role="doc-backlink"}
     :::
106. ::: {#fn106}
     [https://en.wikipedia.org/wiki/ASCII](https://en.wikipedia.org/wiki/ASCII)[↩︎](#fnref106){.footnote-back role="doc-backlink"}
     :::
107. ::: {#fn107}
     We have to pass a pointer to `badchar` to `strtoul()` or it won't be able to modify it in any way we can see, analogous to why you have to pass a pointer to an `int` to a function if you want that function to be able to change that value of that `int`.[↩︎](#fnref107){.footnote-back role="doc-backlink"}
     :::
108. ::: {#fn108}
     Each character has a value associated with it for any given character encoding scheme.[↩︎](#fnref108){.footnote-back role="doc-backlink"}
     :::
109. ::: {#fn109}
     In practice, what's probably happening on your implementation is that the high-order bits are just being dropped from the result, so a 16-bit number `0x1234` being converted to an 8-bit number ends up as `0x0034`, or just `0x34`.[↩︎](#fnref109){.footnote-back role="doc-backlink"}
     :::
110. ::: {#fn110}
     Again, in practice, what will likely happen on your system is that the bit pattern for the original will be truncated and then just used to represent the signed number, two's complement. For example, my system takes an `unsigned char` of `192` and converts it to `signed char` `-64`. In two's complement, the bit pattern for both these numbers is binary `11000000`.[↩︎](#fnref110){.footnote-back role="doc-backlink"}
     :::
111. ::: {#fn111}
     Not really---it's just discarded regularly.[↩︎](#fnref111){.footnote-back role="doc-backlink"}
     :::
112. ::: {#fn112}
     Functions with a variable number of arguments.[↩︎](#fnref112){.footnote-back role="doc-backlink"}
     :::
113. ::: {#fn113}
     This is rarely done because the compiler will complain and having a prototype is the _Right Thing_ to do. I think this still works for historic reasons, before prototypes were a thing.[↩︎](#fnref113){.footnote-back role="doc-backlink"}
     :::
114. ::: {#fn114}
     https://beej.us/guide/bgclr/html/split/ctype.html[↩︎](#fnref114){.footnote-back role="doc-backlink"}
     :::
115. ::: {#fn115}
     [https://gustedt.wordpress.com/2010/08/17/a-common-misconsception-the-register-keyword/](https://gustedt.wordpress.com/2010/08/17/a-common-misconsception-the-register-keyword/)[↩︎](#fnref115){.footnote-back role="doc-backlink"}
     :::
116. ::: {#fn116}
     [https://en.wikipedia.org/wiki/Processor_register](https://en.wikipedia.org/wiki/Processor_register)[↩︎](#fnref116){.footnote-back role="doc-backlink"}
     :::
117. ::: {#fn117}
     [https://en.wikipedia.org/wiki/Boids](https://en.wikipedia.org/wiki/Boids)[↩︎](#fnref117){.footnote-back role="doc-backlink"}
     :::
118. ::: {#fn118}
     Historially, MS-DOS and Windows programs would do this differently than Unix. In Unix, the shell would _expand_ the wildcard into all matching files before your program saw it, whereas the Microsoft variants would pass the wildcard expression into the program to deal with. In any case, there are arguments that get passed into the program.[↩︎](#fnref118){.footnote-back role="doc-backlink"}
     :::
119. ::: {#fn119}
     Since they're just regular parameter names, you don't actually have to call them `argc` and `argv`. But it's so very idiomatic to use those names, if you get creative, other C programmers will look at you with a suspicious eye, indeed![↩︎](#fnref119){.footnote-back role="doc-backlink"}
     :::
120. ::: {#fn120}
     `ps`, Process Status, is a Unix command to see what processes are running at the moment.[↩︎](#fnref120){.footnote-back role="doc-backlink"}
     :::
121. ::: {#fn121}
     [https://en.wikipedia.org/wiki/Inception](https://en.wikipedia.org/wiki/Inception)[↩︎](#fnref121){.footnote-back role="doc-backlink"}
     :::
122. ::: {#fn122}
     [https://en.wikipedia.org/wiki/Shell](https://en.wikipedia.org/wiki/Shell)\_(computing)[↩︎](#fnref122){.footnote-back role="doc-backlink"}
     :::
123. ::: {#fn123}
     In Windows `cmd.exe`, type `echo %errorlevel%`. In PowerShell, type `$LastExitCode`.[↩︎](#fnref123){.footnote-back role="doc-backlink"}
     :::
124. ::: {#fn124}
     If you need a numeric value, convert the string with something like `atoi()` or `strtol()`.[↩︎](#fnref124){.footnote-back role="doc-backlink"}
     :::
125. ::: {#fn125}
     In Windows CMD.EXE, use `set FROTZ=value`. In PowerShell, use `$Env:FROTZ=value`.[↩︎](#fnref125){.footnote-back role="doc-backlink"}
     :::
126. ::: {#fn126}
     [https://pubs.opengroup.org/onlinepubs/9699919799/functions/exec.html](https://pubs.opengroup.org/onlinepubs/9699919799/functions/exec.html)[↩︎](#fnref126){.footnote-back role="doc-backlink"}
     :::
127. ::: {#fn127}
     You can't always just wrap the code in `/*` `*/` comments because those won't nest.[↩︎](#fnref127){.footnote-back role="doc-backlink"}
     :::
128. ::: {#fn128}
     This isn't really a macro---it's technically an identifier. But it's the only predefined identifier and it feels very macro-like, so I'm including it here. Like a rebel.[↩︎](#fnref128){.footnote-back role="doc-backlink"}
     :::
129. ::: {#fn129}
     A hosted implementation basically means you're running the full C standard, probably on an operating system of some kind. Which you probably are. If you're running on bare metal in some kind of embedded system, you're probably on a _standalone implementation_.[↩︎](#fnref129){.footnote-back role="doc-backlink"}
     :::
130. ::: {#fn130}
     OK, I know that was a cop-out answer. Basically there's an optional extension compilers can implement wherein they agree to limit certain types of undefined behavior so that the C code is more amenable to static code analysis. It is unlikely you'll need to use this.[↩︎](#fnref130){.footnote-back role="doc-backlink"}
     :::
131. ::: {#fn131}
     _Breakin' the law... breakin' the law..._[↩︎](#fnref131){.footnote-back role="doc-backlink"}
     :::
132. ::: {#fn132}
     [https://www.openmp.org/](https://www.openmp.org/)[↩︎](#fnref132){.footnote-back role="doc-backlink"}
     :::
133. ::: {#fn133}
     Technically we say that it has an _incomplete type_.[↩︎](#fnref133){.footnote-back role="doc-backlink"}
     :::
134. ::: {#fn134}
     Though some compilers have options to force this to occur---search for `__attribute__((packed))` to see how to do this with GCC.[↩︎](#fnref134){.footnote-back role="doc-backlink"}
     :::
135. ::: {#fn135}
     `super` isn't a keyword, incidentally. I'm just stealing some OOP terminology.[↩︎](#fnref135){.footnote-back role="doc-backlink"}
     :::
136. ::: {#fn136}
     Assuming 8-bit `char` s, i.e. `CHAR_BIT == 8`.[↩︎](#fnref136){.footnote-back role="doc-backlink"}
     :::
137. ::: {#fn137}
     [https://en.wikipedia.org/wiki/Type_punning](https://en.wikipedia.org/wiki/Type_punning)[↩︎](#fnref137){.footnote-back role="doc-backlink"}
     :::
138. ::: {#fn138}
     I just made up that number, but it's probably not far off[↩︎](#fnref138){.footnote-back role="doc-backlink"}
     :::
139. ::: {#fn139}
     There's some devil in the details with values that are stored in registers only, but we can safely ignore that for our purposes here. Also the C spec makes no stance on these "register" things beyond the `register` keyword, the description for which doesn't mention registers.[↩︎](#fnref139){.footnote-back role="doc-backlink"}
     :::
140. ::: {#fn140}
     You're very likely to get different numbers on yours.[↩︎](#fnref140){.footnote-back role="doc-backlink"}
     :::
141. ::: {#fn141}
     There is absolutely nothing in the spec that says this will always work this way, but it happens to work this way on my system.[↩︎](#fnref141){.footnote-back role="doc-backlink"}
     :::
142. ::: {#fn142}
     Even if `E` is `NULL`, it turns out, weirdly.[↩︎](#fnref142){.footnote-back role="doc-backlink"}
     :::
143. ::: {#fn143}
     https://beej.us/guide/bgclr/html/split/stringref.html#man-memcpy[↩︎](#fnref143){.footnote-back role="doc-backlink"}
     :::
144. ::: {#fn144}
     Your C compiler is not required to add padding bytes, and the values of any padding bytes that are added are indeterminate.[↩︎](#fnref144){.footnote-back role="doc-backlink"}
     :::
145. ::: {#fn145}
     This will vary depending on the architecture, but my system is _little endian_, which means the least-significant byte of the number is stored first. _Big endian_ systems will have the `12` first and the `78` last. But the spec doesn't dictate anything about this representation.[↩︎](#fnref145){.footnote-back role="doc-backlink"}
     :::
146. ::: {#fn146}
     It's an optional feature, so it might not be there---but it probably is.[↩︎](#fnref146){.footnote-back role="doc-backlink"}
     :::
147. ::: {#fn147}
     I'm printing out the 16-bit values reversed since I'm on a little-endian machine and it makes it easier to read here.[↩︎](#fnref147){.footnote-back role="doc-backlink"}
     :::
148. ::: {#fn148}
     Assuming they point to the same array object.[↩︎](#fnref148){.footnote-back role="doc-backlink"}
     :::
149. ::: {#fn149}
     The Go Programming Language drew its type declaration syntax inspiration from the opposite of what C does.[↩︎](#fnref149){.footnote-back role="doc-backlink"}
     :::
150. ::: {#fn150}
     Not that other languages don't do this---they do. It is interesting how many modern languages use the same operators for bitwise that C does.[↩︎](#fnref150){.footnote-back role="doc-backlink"}
     :::
151. ::: {#fn151}
     [https://en.wikipedia.org/wiki/Bitwise_operation](https://en.wikipedia.org/wiki/Bitwise_operation)[↩︎](#fnref151){.footnote-back role="doc-backlink"}
     :::
152. ::: {#fn152}
     That is, us lowly developers aren't supposed to know what's in there or what it means. The spec doesn't dictate what it is in detail.[↩︎](#fnref152){.footnote-back role="doc-backlink"}
     :::
153. ::: {#fn153}
     Honestly, it would be possible to remove that limitation from the language, but the idea is that the macros `va_start()`, `va_arg()`, and `va_end()` should be able to be written in C. And to make that happen, we need some way to initialize a pointer to the location of the first parameter. And to do that, we need the _name_ of the first parameter. It would require a language extension to make this possible, and so far the committee hasn't found a rationale for doing so.[↩︎](#fnref153){.footnote-back role="doc-backlink"}
     :::
154. ::: {#fn154}
     "This planet has---or rather had---a problem, which was this: most of the people living on it were unhappy for pretty much of the time. Many solutions were suggested for this problem, but most of these were largely concerned with the movement of small green pieces of paper, which was odd because on the whole it wasn't the small green pieces of paper that were unhappy." ---The Hitchhiker's Guide to the Galaxy, Douglas Adams[↩︎](#fnref154){.footnote-back role="doc-backlink"}
     :::
155. ::: {#fn155}
     Remember that `char` is just a byte-sized integer.[↩︎](#fnref155){.footnote-back role="doc-backlink"}
     :::
156. ::: {#fn156}
     Except for `isdigit()` and `isxdigit()`.[↩︎](#fnref156){.footnote-back role="doc-backlink"}
     :::
157. ::: {#fn157}
     For example, we could store the code point in a big-endian 32-bit integer. Straightforward! We just invented an encoding! Actually not; that's what UTF-32BE encoding is. Oh well---back to the grind![↩︎](#fnref157){.footnote-back role="doc-backlink"}
     :::
158. ::: {#fn158}
     Ish. Technically, it's variable width---there's a way to represent code points higher than [\\(2\^{16}\\)]{.math .inline} by putting two UTF-16 characters together.[↩︎](#fnref158){.footnote-back role="doc-backlink"}
     :::
159. ::: {#fn159}
     There's a special character called the _Byte Order Mark_ (BOM), code point 0xFEFF, that can optionally precede the data stream and indicate the endianess. It is not required, however.[↩︎](#fnref159){.footnote-back role="doc-backlink"}
     :::
160. ::: {#fn160}
     Again, this is only true in UTF-16 for characters that fit in two bytes.[↩︎](#fnref160){.footnote-back role="doc-backlink"}
     :::
161. ::: {#fn161}
     [https://en.wikipedia.org/wiki/UTF-8](https://en.wikipedia.org/wiki/UTF-8)[↩︎](#fnref161){.footnote-back role="doc-backlink"}
     :::
162. ::: {#fn162}
     [https://www.youtube.com/watch?v=MijmeoH9LT4](https://www.youtube.com/watch?v=MijmeoH9LT4)[↩︎](#fnref162){.footnote-back role="doc-backlink"}
     :::
163. ::: {#fn163}
     Presumably the compiler makes the best effort to translate the code point to whatever the output encoding is, but I can't find any guarantees in the spec.[↩︎](#fnref163){.footnote-back role="doc-backlink"}
     :::
164. ::: {#fn164}
     With a format specifier like `"%.12s"`, for example.[↩︎](#fnref164){.footnote-back role="doc-backlink"}
     :::
165. ::: {#fn165}
     `wcscoll()` is the same as `wcsxfrm()` followed by `wcscmp()`.[↩︎](#fnref165){.footnote-back role="doc-backlink"}
     :::
166. ::: {#fn166}
     Ish---things get funky with multi-`char16_t` UTF-16 encodings.[↩︎](#fnref166){.footnote-back role="doc-backlink"}
     :::
167. ::: {#fn167}
     [https://en.wikipedia.org/wiki/Iconv](https://en.wikipedia.org/wiki/Iconv)[↩︎](#fnref167){.footnote-back role="doc-backlink"}
     :::
168. ::: {#fn168}
     [http://site.icu-project.org/](http://site.icu-project.org/)[↩︎](#fnref168){.footnote-back role="doc-backlink"}
     :::
169. ::: {#fn169}
     [https://en.wikipedia.org/wiki/Core_dump](https://en.wikipedia.org/wiki/Core_dump)[↩︎](#fnref169){.footnote-back role="doc-backlink"}
     :::
170. ::: {#fn170}
     Apparently it doesn't do Unix-style signals at all deep down, and they're simulated for console apps.[↩︎](#fnref170){.footnote-back role="doc-backlink"}
     :::
171. ::: {#fn171}
     Confusingly, `sig_atomic_t` predates the lock-free atomics and is not the same thing.[↩︎](#fnref171){.footnote-back role="doc-backlink"}
     :::
172. ::: {#fn172}
     If `sig_action_t` is signed, the range will be at least `-127` to `127`. If unsigned, at least `0` to `255`.[↩︎](#fnref172){.footnote-back role="doc-backlink"}
     :::
173. ::: {#fn173}
     This is due to how VLAs are typically allocated on the stack, whereas `static` variables are on the heap. And the whole idea with VLAs is they'll be automatically dellocated when the stack frame is popped at the end of the function.[↩︎](#fnref173){.footnote-back role="doc-backlink"}
     :::
174. ::: {#fn174}
     [https://en.wikipedia.org/wiki/Goto#Criticism](https://en.wikipedia.org/wiki/Goto#Criticism)[↩︎](#fnref174){.footnote-back role="doc-backlink"}
     :::
175. ::: {#fn175}
     I'd like to point out that using `goto` in all these cases is avoidable. You can use variables and loops instead. It's just that some people think `goto` produces the _best_ code in those circumstances.[↩︎](#fnref175){.footnote-back role="doc-backlink"}
     :::
176. ::: {#fn176}
     [https://en.wikipedia.org/wiki/Tail_call](https://en.wikipedia.org/wiki/Tail_call)[↩︎](#fnref176){.footnote-back role="doc-backlink"}
     :::
177. ::: {#fn177}
     Which isn't quite the same, since it's an array, not a pointer to an `int`.[↩︎](#fnref177){.footnote-back role="doc-backlink"}
     :::
178. ::: {#fn178}
     A variable used here _is_ an expression.[↩︎](#fnref178){.footnote-back role="doc-backlink"}
     :::
179. ::: {#fn179}
     Both "stack pointer" and "program counter" are related to the underlying architecture and C implementation, and are not part of the spec.[↩︎](#fnref179){.footnote-back role="doc-backlink"}
     :::
180. ::: {#fn180}
     The rationale here is that the program might store a value temporarily in a _CPU register_ while it's doing work on it. In that timeframe, the register holds the correct value, and the value on the stack might be out of date. Then later the register values would get overwritten and the changes to the variable lost.[↩︎](#fnref180){.footnote-back role="doc-backlink"}
     :::
181. ::: {#fn181}
     That is, remain allocated until the program ends with no way to free it.[↩︎](#fnref181){.footnote-back role="doc-backlink"}
     :::
182. ::: {#fn182}
     This works because in C, pointers are the same size regardless of the type of data they point to. So the compiler doesn't need to know the size of the `struct node` at this point; it just needs to know the size of a pointer.[↩︎](#fnref182){.footnote-back role="doc-backlink"}
     :::
183. ::: {#fn183}
     [https://en.wikipedia.org/wiki/Complex_number](https://en.wikipedia.org/wiki/Complex_number)[↩︎](#fnref183){.footnote-back role="doc-backlink"}
     :::
184. ::: {#fn184}
     This was a harder one to research, and I'll take any more information anyone can give me. `I` could be defined as `_Complex_I` or `_Imaginary_I`, if the latter exists. `_Imaginary_I` will handle signed zeros, but `_Complex_I` _might_ not. This has implications with branch cuts and other complex-numbery-mathy things. Maybe. Can you tell I'm really getting out of my element here? In any case, the `CMPLX()` macros behave as if `I` were defined as `_Imaginary_I`, with signed zeros, even if `_Imaginary_I` doesn't exist on the system.[↩︎](#fnref184){.footnote-back role="doc-backlink"}
     :::
185. ::: {#fn185}
     The simplicity of this statement doesn't do justice to the incredible amount of work that goes into simply understanding how floating point actually functions. [https://randomascii.wordpress.com/2012/02/25/comparing-floating-point-numbers-2012-edition/](https://randomascii.wordpress.com/2012/02/25/comparing-floating-point-numbers-2012-edition/)[↩︎](#fnref185){.footnote-back role="doc-backlink"}
     :::
186. ::: {#fn186}
     This is the only one that doesn't begin with an extra leading `c`, strangely.[↩︎](#fnref186){.footnote-back role="doc-backlink"}
     :::
187. ::: {#fn187}
     Some architectures have different sized data that the CPU and RAM can operate with at a faster rate than others. In those cases, if you need the fastest 8-bit number, it might give you have a 16- or 32-bit type instead because that's just faster. So with this, you won't know how big the type is, but it will be least as big as you say.[↩︎](#fnref187){.footnote-back role="doc-backlink"}
     :::
188. ::: {#fn188}
     Namely, the system has 8, 16, 32, or 64 bit integers with no padding that use two's complement representation, in which case the `intN_t` variant for that particular number of bits _must_ be defined.[↩︎](#fnref188){.footnote-back role="doc-backlink"}
     :::
189. ::: {#fn189}
     On Earth, anyway. Who know what crazy systems they use _out there_...[↩︎](#fnref189){.footnote-back role="doc-backlink"}
     :::
190. ::: {#fn190}
     OK, don't murder me! GMT is technically a time zone while UTC is a global time system. Also some countries might adjust GMT for daylight saving time, whereas UTC is never adjusted for daylight saving time.[↩︎](#fnref190){.footnote-back role="doc-backlink"}
     :::
191. ::: {#fn191}
     Admittedly, there are more than two.[↩︎](#fnref191){.footnote-back role="doc-backlink"}
     :::
192. ::: {#fn192}
     [https://en.wikipedia.org/wiki/Unix_time](https://en.wikipedia.org/wiki/Unix_time)[↩︎](#fnref192){.footnote-back role="doc-backlink"}
     :::
193. ::: {#fn193}
     https://beej.us/guide/bgclr/html/split/time.html#man-strftime[↩︎](#fnref193){.footnote-back role="doc-backlink"}
     :::
194. ::: {#fn194}
     You will on POSIX, where `time_t` is definitely an integer. Unfortunately the entire world isn't POSIX, so there we are.[↩︎](#fnref194){.footnote-back role="doc-backlink"}
     :::
195. ::: {#fn195}
     [https://en.wikipedia.org/wiki/POSIX_Threads](https://en.wikipedia.org/wiki/POSIX_Threads)[↩︎](#fnref195){.footnote-back role="doc-backlink"}
     :::
196. ::: {#fn196}
     I'm more a fan of shared-nothing, myself, and my skills with classic multithreading constructs are rusty, to say the least.[↩︎](#fnref196){.footnote-back role="doc-backlink"}
     :::
197. ::: {#fn197}
     Yes, `pthreads` with a "`p`". It's short for POSIX threads, a library that C11 borrowed liberally from for its threads implementation.[↩︎](#fnref197){.footnote-back role="doc-backlink"}
     :::
198. ::: {#fn198}
     Per §7.1.4¶5.[↩︎](#fnref198){.footnote-back role="doc-backlink"}
     :::
199. ::: {#fn199}
     Unless you `thrd_detach()`. More on this later.[↩︎](#fnref199){.footnote-back role="doc-backlink"}
     :::
200. ::: {#fn200}
     Though I don't think they have to be. It's just that the threads don't seem to get rescheduled until some system call like might happen with a `printf()`... which is why I have the `printf()` in there.[↩︎](#fnref200){.footnote-back role="doc-backlink"}
     :::
201. ::: {#fn201}
     Short for "mutual exclusion", AKA a "lock" on a section of code that only one thread is permitted to execute.[↩︎](#fnref201){.footnote-back role="doc-backlink"}
     :::
202. ::: {#fn202}
     That is, your process will go to sleep.[↩︎](#fnref202){.footnote-back role="doc-backlink"}
     :::
203. ::: {#fn203}
     You might have expected it to be "time from now", but you'd just like to think that, wouldn't you![↩︎](#fnref203){.footnote-back role="doc-backlink"}
     :::
204. ::: {#fn204}
     And that's why they're called _condition variables_![↩︎](#fnref204){.footnote-back role="doc-backlink"}
     :::
205. ::: {#fn205}
     I'm not saying it's aliens... but it's aliens. OK, really more likely another thread might have been woken up and gotten to the work first.[↩︎](#fnref205){.footnote-back role="doc-backlink"}
     :::
206. ::: {#fn206}
     Survival of the fittest! Right? I admit it's actually nothing like that.[↩︎](#fnref206){.footnote-back role="doc-backlink"}
     :::
207. ::: {#fn207}
     The `__STDC_VERSION__` macro didn't exist in early C89, so if you're worried about that, check it with `#ifdef`.[↩︎](#fnref207){.footnote-back role="doc-backlink"}
     :::
208. ::: {#fn208}
     The reason for this is when optimized, my compiler has put the value of `x` in a register to make the `while` loop fast. But the register has no way of knowing that the variable was updated in another thread, so it never sees the `3490`. This isn't really related to the _all-or-nothing_ part of atomicity, but is more related to the synchronization aspects in the next section.[↩︎](#fnref208){.footnote-back role="doc-backlink"}
     :::
209. ::: {#fn209}
     Until I say otherwise, I'm speaking generally about _sequentially consistent_ operations. More on what that means soon.[↩︎](#fnref209){.footnote-back role="doc-backlink"}
     :::
210. ::: {#fn210}
     Sanest from a programmer perspective.[↩︎](#fnref210){.footnote-back role="doc-backlink"}
     :::
211. ::: {#fn211}
     Apparently C++23 is adding this as a macro.[↩︎](#fnref211){.footnote-back role="doc-backlink"}
     :::
212. ::: {#fn212}
     The spec notes that they might differ in size, representation, and alignment.[↩︎](#fnref212){.footnote-back role="doc-backlink"}
     :::
213. ::: {#fn213}
     I just pulled that example out of nowhere. Maybe it doesn't matter on Intel/AMD, but it could matter somewhere, dangit![↩︎](#fnref213){.footnote-back role="doc-backlink"}
     :::
214. ::: {#fn214}
     C++ elaborates that if the signal is the result of a call to `raise()`, it is sequenced _after_ the `raise()`.[↩︎](#fnref214){.footnote-back role="doc-backlink"}
     :::
215. ::: {#fn215}
     [https://en.wikipedia.org/wiki/Test-and-set](https://en.wikipedia.org/wiki/Test-and-set)[↩︎](#fnref215){.footnote-back role="doc-backlink"}
     :::
216. ::: {#fn216}
     Because consume is all about the operations that are dependent on the value of the acquired atomic variable, and there is no atomic variable with a fence.[↩︎](#fnref216){.footnote-back role="doc-backlink"}
     :::
217. ::: {#fn217}
     [https://www.youtube.com/watch?v=A8eCGOqgvH4](https://www.youtube.com/watch?v=A8eCGOqgvH4)[↩︎](#fnref217){.footnote-back role="doc-backlink"}
     :::
218. ::: {#fn218}
     [https://www.youtube.com/watch?v=KeLBd2EJLOU](https://www.youtube.com/watch?v=KeLBd2EJLOU)[↩︎](#fnref218){.footnote-back role="doc-backlink"}
     :::
219. ::: {#fn219}
     [https://preshing.com/archives/](https://preshing.com/archives/)[↩︎](#fnref219){.footnote-back role="doc-backlink"}
     :::
220. ::: {#fn220}
     [https://preshing.com/20120612/an-introduction-to-lock-free-programming/](https://preshing.com/20120612/an-introduction-to-lock-free-programming/)[↩︎](#fnref220){.footnote-back role="doc-backlink"}
     :::
221. ::: {#fn221}
     [https://preshing.com/20120913/acquire-and-release-semantics/](https://preshing.com/20120913/acquire-and-release-semantics/)[↩︎](#fnref221){.footnote-back role="doc-backlink"}
     :::
222. ::: {#fn222}
     [https://preshing.com/20130702/the-happens-before-relation/](https://preshing.com/20130702/the-happens-before-relation/)[↩︎](#fnref222){.footnote-back role="doc-backlink"}
     :::
223. ::: {#fn223}
     [https://preshing.com/20130823/the-synchronizes-with-relation/](https://preshing.com/20130823/the-synchronizes-with-relation/)[↩︎](#fnref223){.footnote-back role="doc-backlink"}
     :::
224. ::: {#fn224}
     [https://preshing.com/20140709/the-purpose-of-memory_order_consume-in-cpp11/](https://preshing.com/20140709/the-purpose-of-memory_order_consume-in-cpp11/)[↩︎](#fnref224){.footnote-back role="doc-backlink"}
     :::
225. ::: {#fn225}
     [https://preshing.com/20150402/you-can-do-any-kind-of-atomic-read-modify-write-operation/](https://preshing.com/20150402/you-can-do-any-kind-of-atomic-read-modify-write-operation/)[↩︎](#fnref225){.footnote-back role="doc-backlink"}
     :::
226. ::: {#fn226}
     [https://en.cppreference.com/w/c/atomic/memory_order](https://en.cppreference.com/w/c/atomic/memory_order)[↩︎](#fnref226){.footnote-back role="doc-backlink"}
     :::
227. ::: {#fn227}
     [https://en.cppreference.com/w/c/language/atomic](https://en.cppreference.com/w/c/language/atomic)[↩︎](#fnref227){.footnote-back role="doc-backlink"}
     :::
228. ::: {#fn228}
     [https://docs.microsoft.com/en-us/windows/win32/dxtecharts/lockless-programming](https://docs.microsoft.com/en-us/windows/win32/dxtecharts/lockless-programming)[↩︎](#fnref228){.footnote-back role="doc-backlink"}
     :::
229. ::: {#fn229}
     [https://www.reddit.com/r/C_Programming/](https://www.reddit.com/r/C_Programming/)[↩︎](#fnref229){.footnote-back role="doc-backlink"}
     :::
230. ::: {#fn230}
     You can do this with `-O` on the command line.[↩︎](#fnref230){.footnote-back role="doc-backlink"}
     :::
231. ::: {#fn231}
     https://beej.us/guide/bgclr/html/split/stdlib.html#man-exit[↩︎](#fnref231){.footnote-back role="doc-backlink"}
     :::
232. ::: {#fn232}
     https://beej.us/guide/bgclr/html/split/stdlib.html#man-abort[↩︎](#fnref232){.footnote-back role="doc-backlink"}
     :::
233. ::: {#fn233}
     [https://en.wikipedia.org/wiki/Data_structure_alignment](https://en.wikipedia.org/wiki/Data_structure_alignment)[↩︎](#fnref233){.footnote-back role="doc-backlink"}
     :::
     :::
