# [3] Variables and Statements {#variables-and-statements number="3"}

> _"It takes all kinds to make a world, does it not, Padre?"_ > _"So it does, my son, so it does."_
>
> ---Pirate Captain Thomas Bartholomew Red to the Padre, Pirates

There sure can be lotsa stuff in a C program.

Yup.

And for various reasons, it'll be easier for all of us if we classify some of the types of things you can find in a program, so we can be clear what we're talking about.

> 为了各种原因，如果我们对程序中可以找到的东西进行分类，这对我们所有人来说都会更容易，这样我们就能清楚地讨论这个问题。

## [3.1] Variables {#variables number="3.1"}

It's said that "**variables hold values**". But another way to think about it is that a variable is a human-readable name that refers to some data in memory.

> 据说“变量保存值”。但另一种思考方式是，**变量是一个人类可读的名称，指向内存中的某些数据**。

We're going to take a second here and take a peek down the rabbit hole that is pointers. Don't worry about it.

> 我们在这里停下来，看一看指针的兔子洞。别担心。

You can think of memory as a big array of bytes[^33^]. Data is stored in this "array"[^34^]. If a number is larger than a single byte, it is stored in multiple bytes. Because memory is like an array, each byte of memory can be referred to by its index. This index into memory is also called an _address_, or a _location_, or a _pointer_.

> 可以把内存想象成一个大的字节数组 [^33^]。数据存储在这个“数组”中 [^34^]。如果一个数字大于一个字节，它就会被存储在多个字节中。由于内存就像一个数组，每个内存字节都可以通过其索引来引用。这种内存索引也被称为地址、位置或指针。

When you have a variable in C, the value of that variable is in memory _somewhere_, at some address. Of course. After all, where else would it be? But it's a pain to refer to a value by its numeric address, so we make a name for it instead, and that's what the variable is.

> 当你在 C 语言中有一个变量时，该变量的值就存储在某个地址的内存中。当然，还有别的地方可以存储它吗？但是**用它的数字地址来引用它是很麻烦的，所以我们给它起了一个名字，这就是变量的用处**。

The reason I'm bringing all this up is twofold:

1. It's going to make it easier to understand pointer variables later---they're variables that hold the address of other variables!

> 它将使理解指针变量变得更容易---它们是**存储其他变量地址的变量**！

2. Also, it's going to make it easier to understand pointers later.

So a variable is a name for some data that's stored in memory at some address.

> 所以**变量是存储在某个地址的内存中的某些数据的名称**。

### [3.1.1] Variable Names {#variable-names number="3.1.1"}

You can use any characters in the range 0-9, A-Z, a-z, and underscore for variable names, with the following rules:

> 你可以在 0-9、A-Z、a-z 和下划线范围内使用任何字符作为变量名，并按照以下规则：

- You can't start a variable with a digit 0-9.
- You can't start a variable name with two underscores.
- You can't start a variable name with an underscore followed by a capital A-Z.

For Unicode, just try it. There are some rules in the spec in §D.2 that talk about which Unicode codepoint ranges are allowed in which parts of identifiers, but that's too much to write about here and is probably something you'll never have to think about anyway.

> 对于 Unicode，只需尝试一下。在§D.2 中有一些规则讨论了哪些 Unicode 代码点范围可以用于标识符的哪些部分，但这里不可能写太多，而且可能你永远也不需要去考虑它们。

### [3.1.2] Variable Types {#variable-types number="3.1.2"}

Depending on which languages you already have in your toolkit, you might or might not be familiar with the idea of types. But C's kinda picky about them, so we should do a refresher.

> 根据你已经拥有的语言，你可能对**类型的概念**已经很熟悉，也可能不太熟悉。但是 C 语言对它们非常挑剔，所以我们应该重新复习一下。

Some example types, some of the most basic:

```
---
Type Example C Type
---
Integer `3490` `int`
Floating point `3.14159` `float`[^35^]
Character (single) `'c'` `char`
```

## String `"Hello, world!"` `char *`[^36^]

C makes an effort to convert automatically between most numeric types when you ask it to. But other than that, all conversions are manual, notably between string and numeric.

> C 会尝试在你要求的时候**自动地在大多数数值类型之间进行转换**。但除此之外，所有的转换都是**手动的，特别是字符串和数值之间的转换**。

Almost all of the types in C are variants on these types.

Before you can use a variable, you have to _declare_ that variable and tell C what type the variable holds. Once declared, the type of variable cannot be changed later at runtime. What you set it to is what it is until it falls out of scope and is reabsorbed into the universe.

> **在使用变量之前，你必须声明该变量，并告诉 C 它所持有的类型**。一旦声明，变量的类型不能在运行时后期更改。你设置的就是它，**直到它超出作用域**并被重新吸收到宇宙中。

Let's take our previous "Hello, world" code and add a couple variables to it:

> 让我们拿出我们之前的“你好，世界”代码，并加入几个变量：

```c
#include <stdio.h>

int main(void)
{
    int i;    // Holds signed integers, e.g. -3, -2, 0, 1, 10
    float f;  // Holds signed floating point numbers, e.g. -3.1416

    printf("Hello, World!\n");  // Ah, blessed familiarity
}
```

There! We've declared a couple of variables. We haven't used them yet, and they're both uninitialized. One holds an integer number, and the other holds a floating point number (a real number, basically, if you have a math background).

> 好了！我们宣布了几个变量。我们还没有使用它们，它们都是未初始化的。一个保存整数，另一个保存浮点数(基本上是实数，如果你有数学背景)。

Uninitialized variables have indeterminate value[^37^]. They have to be initialized or else you must assume they contain some nonsense number.

> **未初始化的变量具有不确定的值**[^37^]。它们必须被初始化，否则你必须假定它们包含一些无意义的数字。

> This is one of the places C can "get you". Much of the time, in my experience, the indeterminate value is zero... but it can vary from run to run! Never assume the value will be zero, even if you see it is. _Always_ explicitly initialize variables to some value before you use them[^38^].

> > 这是 C 可以“抓住您”的地方之一。在我的经验中，**大部分时间不确定的值为零...** 但是它的运行可能会有所不同！即使您看到的是值，也永远不要假设该值将为零。**_always_ 在使用[^38^]之前，将变量显着初始化为某些值。**

What's this? You want to store some numbers in those variables? Insanity!

Let's go ahead and do that:

```c
int main(void)
{
    int i;

    i = 2; // Assign the value 2 into the variable i

    printf("Hello, World!\n");
}
```

Killer. We've stored a value. Let's print it.

We're going to do that by passing _two_ amazing arguments to the `printf()` function. The first argument is a string that describes what to print and how to print it (called the _format string_), and the second is the value to print, namely whatever is in the variable `i`.

> 我们将通过向 `printf()` 函数传递 _两个_ 令人惊叹的参数来完成这一点。第一个参数是描述要打印什么以及如何打印的字符串(称为 _格式字符串_ )，第二个是要打印的值，即变量 `i` 中的值。

`printf()` hunts through the format string for a variety of special sequences which start with a percent sign (`%`) that tell it what to print. For example, if it finds a `%d`, it looks to the next parameter that was passed, and prints it out as an integer. If it finds a `%f`, it prints the value out as a float. If it finds a `%s`, it prints a string.

> `printf()` 通过格式字符串搜索各种特殊序列，这些序列以百分比（`%`）开头，该序列讲述了什么。例如，如果它找到了一个`%d`，它可以查看通过的下一个参数，并将其打印为整数。如果找到一个`%f`，它将值将其打印成浮子。如果找到一个`%s`，它将打印一个字符串。

As such, we can print out the value of various types like so:

```c
#include <stdio.h>

int main(void)
{
    int i = 2;
    float f = 3.14;
    char *s = "Hello, world!";  // char * ("char pointer") is the string type

    printf("%s  i = %d and f = %f!\n", s, i, f);
}
```

And the output will be:

```{.sourceCode .default}
Hello, world!  i = 2 and f = 3.14!
```

In this way, `printf()` might be similar to various types of format strings or parameterized strings in other languages you're familiar with.

> 在这种方式下，`printf()` 可能类似于您熟悉的其他语言中的各种格式字符串或参数化字符串。

### [3.1.3] Boolean Types {#boolean-types number="3.1.3"}

C has Boolean types, true or false?

`1`!

Historically, C didn't have a Boolean type, and some might argue it still doesn't. In C, `0` means "false", and non-zero means "true". So `1` is true. And `-37` is true. **And `0` is false.** You can just declare Boolean types as `int` s:

> **历史上，C 没有布尔类型**，有些人可能会认为它仍然没有。

```c
int x = 1;

if (x) {
    printf("x is true!\n");
}
```

If you `#include <stdbool.h>`, you also get access to some symbolic names that might make things look more familiar, namely a `bool` type and `true` and `false` values:

> 如果你 `#include <stdbool.h>`，你也可以访问一些符号名称，使事情看起来更加熟悉，即 bool 类型和 true 和 false 值：

```c
#include <stdio.h>
#include <stdbool.h>

int main(void) {
    bool x = true;

    if (x) {
        printf("x is true!\n");
    }
}
```

But these are identical to using integer values for true and false. They're just a facade to make things look nice.

> 但这些**与使用整数值来表示真和假是完全一样的**。它们只是一个外表，使事情看起来更好。

## [3.2] Operators and Expressions {#operators number="3.2"}

C operators should be familiar to you from other languages. Let's blast through some of them here.

> 你应该从其他语言中熟悉 C 运算符。让我们快速浏览一些运算符。

(There are a bunch more details than this, but we're going to do enough in this section to get started.)

### [3.2.1] Arithmetic {#arithmetic number="3.2.1"}

Hopefully these are familiar:

```c
i = i + 3;  // Addition (+) and assignment (=) operators, add 3 to i
i = i - 8;  // Subtraction, subtract 8 from i
i = i * 9;  // Multiplication
i = i / 2;  // Division
i = i % 5;  // Modulo (division remainder)
```

There are shorthand variants for all of the above. Each of those lines could more tersely be written as:

> 所有上述都有简写变体。每一行可以更简洁地写作：

```c
i += 3;  // Same as "i = i + 3", add 3 to i
i -= 8;  // Same as "i = i - 8"
i *= 9;  // Same as "i = i * 9"
i /= 2;  // Same as "i = i / 2"
i %= 5;  // Same as "i = i % 5"
```

There is no exponentiation. You'll have to use one of the `pow()` function variants from `math.h`.

> 没有指数运算。您必须使用 math.h 中的 `pow()`函数变体之一。

Let's get into some of the weirder stuff you might not have in your other languages!

> 让我们来看看一些你在其他语言中可能没有的更奇怪的东西！

### [3.2.2] Ternary Operator {#ternary-operator number="3.2.2"}

C also includes the _ternary operator_. This is an expression whose value depends on the result of a conditional embedded in it.

> C 也包括三元运算符。这是一个值取决于其中嵌入的条件结果的表达式。

::: {#cb18 .sourceCode}

```c
// If x > 10, add 17 to y. Otherwise add 37 to y.

y += x > 10? 17: 37;
```

:::

What a mess! You'll get used to it the more you read it. To help out a bit, I'll rewrite the above expression using `if` statements:

> 哎呀！你会随着阅读越多而习惯它的。为了帮助一点，我会用 if 语句重写上面的表达式：

```c
// This expression:

y += x > 10? 17: 37;

// is equivalent to this non-expression:

if (x > 10)
    y += 17;
else
    y += 37;
```

:::

Compare those two until you see each of the components of the ternary operator.

> 比较两者，直到你看到三元运算子的每个组件为止。

Or, another example that prints if a number stored in `x` is odd or even:

```c
printf("The number %d is %s.\n", x, x % 2 == 0? "even": "odd")
```

The `%s` format specifier in `printf()` means print a string. If the expression `x % 2` evaluates to `0`, the value of the entire ternary expression evaluates to the string `"even"`. Otherwise it evaluates to the string `"odd"`. Pretty cool!

> `printf()` 中的 `%s` 格式说明符意味着打印一个字符串。如果表达式 `x % 2` 的评估值为 `0`，那么三元表达式的整体值就会评估为字符串 `"even"`。否则就会评估为字符串 `"odd"`。太酷了！

It's important to note that the ternary operator isn't flow control like the `if` statement is. It's just an expression that evaluates to a value.

> 重要的是要注意，三元运算符不像 `if` 语句那样是流程控制。它只是一个表达式，它的值可以被评估。

### [3.2.3] Pre-and-Post Increment-and-Decrement {#pre-and-post-increment-and-decrement number="3.2.3"}

Now, let's mess with another thing that you might not have seen. These are the legendary post-increment and post-decrement operators:

```c
i++;        // Add one to i (post-increment)
i--;        // Subtract one from i (post-decrement)
```

Very commonly, these are just used as shorter versions of:

```c
i += 1;        // Add one to i
i -= 1;        // Subtract one from i
```

but they're more subtly different than that, the clever scoundrels.

Let's take a look at this variant, pre-increment and pre-decrement:

```c
++i;        // Add one to i (pre-increment)
--i;        // Subtract one from i (pre-decrement)
```

With pre-increment and pre-decrement, the value of the variable is incremented or decremented _before_ the expression is evaluated. Then the expression is evaluated with the new value.

> 使用前置增量和前置减量，变量的值会**在表达式被求值之前先增加或减少**。然后，用新值求值表达式。

With post-increment and post-decrement, the value of the expression is first computed with the value as-is, and _then_ the value is incremented or decremented after the value of the expression has been determined.

> 使用后置增量和后置减量，先使用原始值计算表达式的值，然后在确定表达式的值之后再增加或减少值。

You can actually embed them in expressions, like this:

```c
i = 10;
j = 5 + i++;  // Compute 5 + i, _then_ increment i

printf("%d, %d\n", i, j);  // Prints 11, 15
```

Let's compare this to the pre-increment operator:

```c
i = 10;
j = 5 + ++i;  // Increment i, _then_ compute 5 + i

printf("%d, %d\n", i, j);  // Prints 11, 16
```

This technique is used frequently with array and pointer access and manipulation. It gives you a way to use the value in a variable, and also increment or decrement that value before or after it is used.

> 这种技术经常用于数组和指针访问和操作。它为您提供了一种使用变量中的值的方法，并且在使用前或使用后可以对该值进行递增或递减。

But by far the most common place you'll see this is in a `for` loop:

```c
for (i = 0; i < 10; i++)
    printf("i is %d\n", i);
```

But more on that later.

### [3.2.4] The Comma Operator {#the-comma-operator number="3.2.4"}

This is an uncommonly-used way to separate expressions that will run left to right:

> 这是一种不寻常使用的方式，用来从左到右分离表达式：

```c
x = 10, y = 20;  // First assign 10 to x, then 20 to y
```

Seems a bit silly, since you could just replace the comma with a semicolon, right?

> 看起来有点傻，因为你可以用分号替换逗号，对吗？

```c
x = 10; y = 20;  // First assign 10 to x, then 20 to y
```

But that's a little different. The latter is two separate expressions, while the former is a single expression!

> 但是这有点不同。后者是两个独立的表达，而**前者是一个单一的表达**！

With the comma operator, the value of the comma expression is the value of the rightmost expression:

> 使用逗号运算子，**逗号表达式的值是最右边表达式的值**。

```c
x = (1, 2, 3);

printf("x is %d\n", x);  // Prints 3, because 3 is rightmost in the comma list
```

But even that's pretty contrived. One common place the comma operator is used is in `for` loops to do multiple things in each section of the statement:

> 但即使如此，也有些牵强。**逗号操作符常见的用法是在 `for` 循环中**，用来在每个语句部分做多件事：

```c
for (i = 0, j = 10; i < 100; i++, j++)
    printf("%d, %d\n", i, j);
```

We'll revisit that later.

### [3.2.5] Conditional Operators {#conditional-operators number="3.2.5"}

For Boolean values, we have a raft of standard operators:

```c
a == b;  // True if a is equivalent to b
a != b;  // True if a is not equivalent to b
a < b;   // True if a is less than b
a > b;   // True if a is greater than b
a <= b;  // True if a is less than or equal to b
a >= b;  // True if a is greater than or equal to b
```

Don't mix up assignment `=` with comparison `==`! Use two equals to compare, one to assign.

> 不要把赋值 `=` 和比较 `==` 混淆！用两个等号来比较，一个来赋值。

We can use the comparison expressions with `if` statements:

```c
if (a <= 10)
    printf("Success!\n");
```

### [3.2.6] Boolean Operators {#boolean-operators number="3.2.6"}

We can chain together or alter conditional expressions with Boolean operators for _and_, _or_, and _not_.

> 我们可以用**布尔运算符(and、or 和 not)来连接或改变条件表达式**。

Operator Boolean meaning

---

```
 `&&`           and
 `||`           or
 `!`            not
```

An example of Boolean "and":

```c
// Do something if x less than 10 and y greater than 20:
if (x < 10 && y > 20)
    printf("Doing something!\n");
```

An example of Boolean "not":

```c
if (!(x < 12))
    printf("x is not less than 12\n");
```

`!` has higher precedence than the other Boolean operators, so we have to use parentheses in that case.

> `!`比其他布尔操作员具有更高的优先级，因此我们必须在这种情况下使用括号。

Of course, that's just the same as:

```c
if (x >= 12)
    printf("x is not less than 12\n");
```

but I needed the example!

### [3.2.7] The `sizeof` Operator {#sizeof-operator number="3.2.7"}

This operator tells you the size (in bytes) that a particular variable or data type uses in memory.

> 这个操作符告诉你**特定变量或数据类型在内存中使用的大小(以字节为单位)**。

More particularly, it tells you the size (**in bytes**) that the _type of a particular expression_ (which might be just a single variable) uses in memory.

> 更具体地说，它告诉你**特定表达式(可能只是一个变量)的类型在内存中所占用的大小(以字节为单位)**。

This can be different on different systems, except for `char` and its variants (which are always 1 byte).

> 在不同的系统上，这可能会有所不同，除了 `char` 及其变体(总是 1 个字节)。

And this might not seem very useful now, but we'll be making references to it here and there, so it's worth covering.

> 这可能现在看起来不是很有用，但是我们会在这里和那里做出参考，所以值得覆盖。

Since this computes the number of bytes needed to store a type, you might think it would return an `int`. Or... since the size can't be negative, maybe an `unsigned`?

> 由于这个计算需要存储类型所需的字节数，你可能会认为它会返回一个 `int`。或者...由于大小不能为负，也许是一个 `unsigned`？

But it turns out C has a special type to represent the return value from `sizeof`. It's `size_t`, pronounced "_size tee_"[^39^]. All we know is that it's an unsigned integer type that can hold the size in bytes of anything you can give to `sizeof`.

> 但事实证明，**C 有一种特殊类型来表示 `sizeof` 的返回值。它叫做 `size_t`**，发音为“_size tee_”。我们只知道它是一种**无符号整数类型**，可以容纳你给 `sizeof` 的任何东西的字节数。

`size_t` shows up a lot of different places where counts of things are passed or returned. Think of it as a value that represents a count.

> `size_t`显示了许多不同的地方，其中事物的数量被传递或返回。将其视为代表计数的值。

You can take the `sizeof` a variable or expression:

```c
int a = 999;

// %zu is the format specifier for type size_t

printf("%zu\n", sizeof a);      // Prints 4 on my system
printf("%zu\n", sizeof(2 + 7)); // Prints 4 on my system
printf("%zu\n", sizeof 3.14);   // Prints 8 on my system

// If you need to print out negative size_t values, use %zd
```

Remember: it's the size in bytes of the _type_ of the expression, not the size of the expression itself. That's why the size of `2+7` is the same as the size of `a`---they're both type `int`. We'll revisit this number `4` in the very next block of code...

> 记住：**这是表达式的 _类型_ 的字节大小，而不是表达式本身的大小**。这就是为什么 `2+7` 的大小与 `a` 的大小相同---它们都是 `int` 类型。我们将在下一个代码块中重新讨论这个数字 `4`...

...Where we'll see you can take the `sizeof` a type (note the parentheses are required around a type name, unlike an expression):

> 在哪里，我们可以看到你可以**获取一个类型的大小(注意类型名称周围需要括号，不像表达式)**：

```c
printf("%zu\n", sizeof(int));   // Prints 4 on my system
printf("%zu\n", sizeof(char));  // Prints 1 on all systems
```

It's important to note that `sizeof` is a _compile-time_ operation[^40^]. The result of the expression is determined entirely at compile-time, not at runtime.

> 重要指出的是，**`sizeof` 是一个编译时操作[^40^]**。表达式的结果完全是在编译时确定的，而不是在运行时。

We'll make use of this later on.

## [3.3] Flow Control {#flow-control number="3.3"}

Booleans are all good, but of course we're nowhere if we can't control program flow. Let's take a look at a number of constructs: `if`, `for`, `while`, and `do-while`.

> 布尔值都很好，但是如果我们不能控制程序流程的话，我们就无处可去。让我们看看一些构造：`if`，`for`，`while` 和 `do-while`。

First, a general forward-looking note about statements and blocks of statements brought to you by your local friendly C developer:

> 首先，来自您本地友好的 C 开发人员的一些关于语句和语句块的前瞻性说明：

After something like an `if` or `while` statement, you can either put a single statement to be executed, or a block of statements to all be executed in sequence.

> 在 `if` 或 `while` 语句之后，你可以放置一个要执行的单独语句，或者一组要按顺序执行的语句块。

Let's start with a single statement:

```c
if (x == 10) printf("x is 10\n");
```

This is also sometimes written on a separate line. (Whitespace is largely irrelevant in C---it's not like Python.)

> 这有时也会写在单独的一行上。(**在 C 中空格基本上没有意义**——它不像 Python 那样。)

```c
if (x == 10)
    printf("x is 10\n");
```

But what if you want multiple things to happen due to the conditional? You can use squirrelly braces to mark a _block_ or _compound statement_.

> 如果你想要多件事由条件而发生，你可以使用大括号来标记一个块或复合语句。

```c
if (x == 10) {
    printf("x is 10\n");
    printf("And also this happens when x is 10\n");
}
```

It's a really common style to _always_ use squirrelly braces even if they aren't necessary:

> 这种总是使用大括号即使它们不是必需的风格真的很常见：

```c
if (x == 10) {
    printf("x is 10\n");
}
```

Some devs feel the code is easier to read and avoids errors like this where things visually look like they're in the `if` block, but actually they aren't.

> 一些开发人员认为代码更容易阅读，并避免了这种错误，即事物看起来像在 `if` 块中，但实际上它们并不在其中。

```c
// BAD ERROR EXAMPLE

if (x == 10)
    printf("This happens if x is 10\n");
    printf("This happens ALWAYS\n");  // Surprise!! Unconditional!
```

`while` and `for` and the other looping constructs work the same way as the examples above. If you want to do multiple things in a loop or after an `if`, wrap them up in squirrelly braces.

> `while` and `for` 其他循环构造的工作方式与上面的示例相同。如果您想在循环中或在“ if”之后做多件事，请将它们包裹在松鼠牙套中。

In other words, the `if` is going to run the one thing after the `if`. And that one thing can be a single statement or a block of statements.

> 如果条件成立，**`if` 将会运行之后的一件事情**。这一件事情可以是一个单独的语句，也可以是一组语句。

### [3.3.1] The `if`-`else` statement {#ifstat number="3.3.1"}

We've already been using `if` for multiple examples, since it's likely you've seen it in a language before, but here's another:

> 我们已经使用了 `if` 来做多个示例，因为你可能在其他语言中见过它，但这里还有另一个例子：

```c
int i = 10;

if (i > 10) {
    printf("Yes, i is greater than 10.\n");
    printf("And this will also print if i is greater than 10.\n");
}

if (i <= 10) printf("i is less than or equal to 10.\n");
```

In the example code, the message will print if `i` is greater than 10, otherwise execution continues to the next line. Notice the squirrley braces after the `if` statement; if the condition is true, either the first statement or expression right after the if will be executed, or else the collection of code in the squirlley braces after the `if` will be executed. This sort of _code block_ behavior is common to all statements.

> 在示例代码中，如果 `i` 大于 10，则会打印消息，否则执行会继续到下一行。注意 if 语句后面的大括号；如果条件为真，则会执行 if 后面的第一个语句或表达式，否则会执行 if 后面大括号中的代码块。所有语句都具有这种 _代码块_ 行为。

Of course, because C is fun this way, you can also do something if the condition is false with an `else` clause on your `if`:

> 当然，因为 C 有趣，所以如果条件为假，你也可以在 `if` 语句上使用 `else` 子句来做点什么：

```c
int i = 99;

if (i == 10)
    printf("i is 10!\n");
else {
    printf("i is decidedly not 10.\n");
    printf("Which irritates me a little, frankly.\n");
}
```

And you can even cascade these to test a variety of conditions, like this:

> 你甚至可以级联这些来测试各种条件，就像这样：

```c
int i = 99;

if (i == 10)
    printf("i is 10!\n");

else if (i == 20)
    printf("i is 20!\n");

else if (i == 99) {
    printf("i is 99! My favorite\n");
    printf("I can't tell you how happy I am.\n");
    printf("Really.\n");
}

else
    printf("i is some crazy number I've never heard of.\n");
```

:::

Though if you're going that route, be sure to check out the [`switch`](#switch-statement) statement for a potentially better solution. The catch is `switch` only works with equality comparisons with constant numbers. The above `if`-`else` cascade could check inequality, ranges, variables, or anything else you can craft in a conditional expression.

> 如果你要走这条路，一定要查看[`switch`](#switch-statement)语句以获得更好的解决方案。不过，**`switch` 只能用于恒定数字的等式比较。上述的 `if`-`else` 级联可以检查不等式、范围、变量或任何你可以在条件表达式中制作的内容**。

### [3.3.2] The `while` statement {#whilestat number="3.3.2"}

`while` is your average run-of-the-mill looping construct. Do a thing while a condition expression is true.

Let's do one!

```c
// Print the following output:
//
//   i is now 0!
//   i is now 1!
//   [ more of the same between 2 and 7 ]
//   i is now 8!
//   i is now 9!

i = 0;

while (i < 10) {
    printf("i is now %d!\n", i);
    i++;
}

printf("All done!\n");
```

That gets you a basic loop. C also has a `for` loop which would have been cleaner for that example.

> 这让你得到一个基本的循环。C 语言也有一个 `for` 循环，对于那个例子来说更加干净。

A not-uncommon use of `while` is for infinite loops where you repeat while true:

> 使用 `while` 的一种常见用法是用于无限循环，即重复执行，直到条件为真：

```c
while (1) {
    printf("1 is always true, so this repeats forever.\n");
}
```

### [3.3.3] The `do-while` statement {#dowhilestat number="3.3.3"}

So now that we've gotten the `while` statement under control, let's take a look at its closely related cousin, `do-while`.

> 现在我们已经掌握了 `while` 语句，让我们来看看它的近亲 `do-while`。

They are basically the same, except if the loop condition is false on the first pass, `do-while` will execute once, but `while` won't execute at all. In other words, the test to see whether or not to execute the block happens at the _end_ of the block with `do-while`. It happens at the _beginning_ of the block with `while`.

> 他们基本上是一样的，除非在第一次循环条件为假时，`do-while` 会执行一次，而 `while` 根本不会执行。换句话说，检查是否执行块的测试在 `do-while` 的块结尾处发生。在 `while` 的块开头发生。

Let's see by example:

```c
// Using a while statement:

i = 10;

// this is not executed because i is not less than 10:
while(i < 10) {
    printf("while: i is %d\n", i);
    i++;
}

// Using a do-while statement:

i = 10;

// this is executed once, because the loop condition is not checked until
// after the body of the loop runs:

do {
    printf("do-while: i is %d\n", i);
    i++;
} while (i < 10);

printf("All done!\n");
```

Notice that in both cases, the loop condition is false right away. So in the `while`, the loop fails, and the following block of code is never executed. With the `do-while`, however, the condition is checked _after_ the block of code executes, so it always executes at least once. In this case, it prints the message, increments `i`, then fails the condition, and continues to the "All done!" output.

> 在这两种情况下，循环条件都立即变为假。因此，在 `while` 中，循环失败，以下代码块不会被执行。但是，在 `do-while` 中，在代码块执行后才检查条件，因此它总是至少执行一次。在这种情况下，它会打印消息，增加 `i`，然后使条件失败，并继续输出“全部完成！”

The moral of the story is this: if you want the loop to execute at least once, no matter what the loop condition, use `do-while`.

> 故事的寓意是：如果你想让循环至少执行一次，无论循环条件如何，请使用“do-while”。

All these examples might have been better done with a `for` loop. Let's do something less deterministic---repeat until a certain random number comes up!

> 所有这些例子可能用 `for` 循环做得更好。让我们做点不那么确定性的——直到出现某个随机数为止！

```c
#include <stdio.h>   // For printf
#include <stdlib.h>  // For rand

int main(void)
{
    int r;

    do {
        r = rand() % 100; // Get a random number between 0 and 99
        printf("%d\n", r);
    } while (r != 37);    // Repeat until 37 comes up
}
```

Side note: did you run that more than once? If you did, did you notice the same sequence of numbers came up again. And again. And again? This is because `rand()` is a pseudorandom number generator that must be _seeded_ with a different number in order to generate a different sequence. Look up the [`srand()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-srand)[^41^] function for more details.

> 边注：你运行了多次吗？如果你运行了，你有没有注意到相同的数字序列出现了又一次？这是因为 `rand()` 是一种伪随机数生成器，必须使用不同的数字进行种子化才能生成不同的序列。查看[`srand()`](https://beej.us/guide/bgclr/html/split/stdlib.html#man-srand)函数了解更多详情。

### [3.3.4] The `for` statement {#forstat number="3.3.4"}

Welcome to one of the most popular loops in the world! The `for` loop!

This is a great loop if you know the number of times you want to loop in advance.

> 这是一个很棒的循环，**如果你事先知道要循环的次数**。

You could do the same thing using just a `while` loop, but the `for` loop can help keep the code cleaner.

> 你可以只使用一个 `while` 循环来做同样的事情，但是 **`for` 循环可以帮助保持代码更加整洁**。

Here are two pieces of equivalent code---note how the `for` loop is just a more compact representation:

> 这里有两段等价的代码---注意 **`for` 循环只是一种更紧凑的表示方式**：

```c
// Print numbers between 0 and 9, inclusive...

// Using a while statement:

i = 0;
while (i < 10) {
    printf("i is %d\n", i);
    i++;
}

// Do the exact same thing with a for-loop:

for (i = 0; i < 10; i++) {
    printf("i is %d\n", i);
}
```

That's right, folks---they do exactly the same thing. But you can see how the `for` statement is a little more compact and easy on the eyes. (JavaScript users will fully appreciate its C origins at this point.)

> 没错，伙计们——它们做的事情完全一样。但你可以看到 `for` 语句更紧凑，更容易看懂。(JavaScript 用户在这一点上会充分体会它的 C 语言来源。)

It's split into three parts, separated by semicolons. The first is the initialization, the second is the loop condition, and the third is what should happen at the end of the block if the loop condition is true. All three of these parts are optional.

> 它分为三部分，用分号分隔。第一部分是初始化，第二部分是循环条件，第三部分是如果循环条件为真时，块结束时应该发生的事情。这三个部分都是可选的。

```c
for (initialize things; loop if this is true; do this after each loop)
```

Note that the loop will not execute even a single time if the loop condition starts off false.

> 注意，如果循环条件一开始就是假的，循环将不会执行任何一次。

> **`for`-loop fun fact!**
>
> You can use the comma operator to do multiple things in each clause of the `for` loop!
>
> ::: {#cb52 .sourceCode}
>
> ```c
> for (i = 0, j = 999; i < 10; i++, j--) {
>     printf("%d, %d\n", i, j);
> }
> ```
>
> :::

An empty `for` will run forever:

```c
for(;;) {  // "forever"
    printf("I will print this again and again and again\n" );
    printf("for all eternity until the heat-death of the universe.\n");

    printf("Or until you hit CTRL-C.\n");
}
```

### [3.3.5] The `switch` Statement {#switch-statement number="3.3.5"}

Depending on what languages you're coming from, you might or might not be familiar with `switch`, or C's version might even be more restrictive than you're used to. This is a statement that allows you to take a variety of actions depending on the value of an integer expression.

> 根据您来自的语言，您可能对“switch”熟悉或不熟悉，甚至 C 的版本可能比您习惯的更加严格。这是一个语句，可以根据整数表达式的值采取各种行动。

Basically, it evaluates an expression to an integer value, jumps to the `case` that corresponds to that value. Execution resumes from that point. If a `break` statement is encountered, then execution jumps out of the `switch`.

> 基本上，它将表达式评估为整数值，跳转到与该值对应的 `case`。执行从那一点开始继续。如果遇到 `break` 语句，则执行跳出 `switch`。

Let's do an example where the user enters a number of goats and we print out a gut-feel of how many goats that is.

> 让我们做一个例子，用户输入一个数字的山羊，我们打印出这个数量的山羊的直觉感受。

```c
#include <stdio.h>

int main(void)
{
    int goat_count;

    printf("Enter a goat count: ");
    scanf("%d", &goat_count);       // Read an integer from the keyboard

    switch (goat_count) {
        case 0:
            printf("You have no goats.\n");
            break;

        case 1:
            printf("You have a singular goat.\n");
            break;

        case 2:
            printf("You have a brace of goats.\n");
            break;

        default:
            printf("You have a bona fide plethora of goats!\n");
            break;
    }
}
```

In that example, if the user enters, say, `2`, the `switch` will jump to the `case 2` and execute from there. When (if) it hits a `break`, it jumps out of the `switch`.

> 在这个例子中，如果用户输入 2，`switch` 就会跳到 `case 2` 并从那里开始执行。**当(如果)遇到 `break` 时，它就会跳出 `switch`**。

Also, you might see that `default` label there at the bottom. This is what happens when no cases match.

> 也可以看到底部有一个 `默认` 标签。当没有匹配的情况时就会出现这种情况。

Every `case`, including `default`, is optional. And they can occur in any order, but it's really typical for `default`, if any, to be listed last.

> 每个情况(包括默认情况)都是可选的，它们可以以任何顺序出现，但如果有默认情况，通常会放在最后。

So the whole thing acts like an `if`-`else` cascade:

```c
if (goat_count == 0)
    printf("You have no goats.\n");
else if (goat_count == 1)
    printf("You have a singular goat.\n");
else if (goat_count == 2)
    printf("You have a brace of goats.\n");
else
    printf("You have a bona fide plethora of goats!\n");
```

With some key differences:

- `switch` is often faster to jump to the correct code (though the spec makes no such guarantee).
- `if`-`else` can do things like relational conditionals like `<` and `>=` and floating point and other types, while `switch` cannot.

> 如果-else 可以像 < 和 >=这样的关系条件和浮点数以及其他类型，而 switch 则不能。

There's one more neat thing about switch that you sometimes see that is quite interesting: _fall through_.

> 有一件很有趣的事情可以在开关上看到，那就是“贯穿”：

Remember how `break` causes us to jump out of the switch? Well, what happens if we _don't_ `break`? Turns out we just keep on going into the next `case`! Demo!

> 还记得“断裂”是如何使我们跳出开关的吗？好吧，如果我们不休息会发生什么？原来我们只是继续进入下一个``case''！演示！

```c
switch (x) {
    case 1:
        printf("1\n");
        // Fall through!
    case 2:
        printf("2\n");
        break;
    case 3:
        printf("3\n");
        break;
}
```

If `x == 1`, this `switch` will first hit `case 1`, it'll print the `1`, but then it just continues on to the next line of code... which prints `2`!

> 如果 x 等于 1，这个 switch 将会首先执行 case 1，它会打印 1，但是接着它会继续执行下一行代码...它会打印 2！

And then, at last, we hit a `break` so we jump out of the `switch`.

if `x == 2`, then we just hit the `case 2`, print `2`, and `break` as normal.

> 如果 x 等于 2，那么我们就到达情况 2，打印 2，然后正常地 break。

Not having a `break` is called _fall through_.

ProTip: _ALWAYS_ put a comment in the code where you intend to fall through, like I did above. It will save other programmers from wondering if you meant to do that.

> ProTip：*总是*在您打算跳转的代码中添加注释，就像我上面做的那样。这将使其他程序员不必怀疑您是否有此意图。

In fact, this is one of the common places to introduce bugs in C programs: forgetting to put a `break` in your `case`. You gotta do it if you don't want to just roll into the next case[^42^].

> 事实上，这是 C 程序中常见的错误引入地方之一：忘记在 `case` 中添加 `break`。如果你不想让它跳到下一个 `case`，你就得这么做 [^42^]。

Earlier I said that `switch` works with integer types---keep it that way. Don't use floating point or string types in there. One loophole-ish thing here is that you can use character types because those are secretly integers themselves. So this is perfectly acceptable:

> 以前我说 `switch` 只能用整数类型，这样保持下去吧。**不要在里面使用浮点数或字符串类型。这里有一个漏洞，你可以使用字符类型，因为它们其实也是整数**。所以这样是完全可以接受的：

```c
char c = 'b';

switch (c) {
    case 'a':
        printf("It's 'a'!\n");
        break;

    case 'b':
        printf("It's 'b'!\n");
        break;

    case 'c':
        printf("It's 'c'!\n");
        break;
}
```

Finally, you can use `enum` s in `switch` since they are also integer types. But more on that in the `enum` chapter.

> 最后，您**可以在 `switch` 中使用 `enum`，因为它们也是整数类型**。但更多的内容在 `enum` 章节中。
