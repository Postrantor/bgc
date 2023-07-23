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

> 事实就是你传递给函数的表达式会被*复制*到它们对应的参数上。参数是一个副本，而不是原件。

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

> 但是，没有花哨的名字能够让你忘记这样一个事实：_无一例外_，你传递给函数的*所有*内容都会被复制到相应的参数中，函数也会对这个本地副本进行操作，_无论如何_。即使我们在谈论所谓的引用传递，也要记住这一点。

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

> 但是在函数原型的情况下，使用 `void` 和不使用之间有*重大*的区别：

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
