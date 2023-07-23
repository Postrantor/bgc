# [20] `struct` s II: More Fun with `struct` s {#structs-ii-more-fun-with-structs number="20"}

Turns out there's a lot more you can do with `struct` s than we've talked about, but it's just a big pile of miscellaneous things. So we'll throw them in this chapter.

> 原来你可以用 `struct` 做的事情比我们讨论的要多得多，但它们只是一大堆杂项。所以我们将把它们放在这一章中。

If you're good with `struct` basics, you can round out your knowledge here.

> 如果你对 `struct` 基础有所了解，你可以在这里完善你的知识。

## [20.1] Initializers of Nested `struct` s and Arrays {#initializers-of-nested-structs-and-arrays number="20.1"}

Remember how you could [initialize structure members along these lines](#struct-initializers)?

> 记住你怎样可以这样[初始化结构成员](#struct-initializers)吗？

```c
struct foo x = {.a=12, .b=3.14};
```

Turns out we have more power in these initializers than we'd originally shared. Exciting!

> 原来我们在这些初始化程序中拥有的力量比我们最初分享的要多。令人兴奋！

For one thing, if you have a nested substructure like the following, you can initialize members of that substructure by following the variable names down the line:

> 如果你有一个嵌套的子结构，你可以通过沿着变量名称来初始化该子结构的成员。

```c
struct foo x = {.a.b.c=12};
```

Let's look at an example:

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
:17:        .ci.window_count = 8,   // <-- NESTED INITIALIZER!
        .ci.o2level = 21
    };

    printf("%s: %d seats, %d%% oxygen\n",
        s.manufacturer, s.ci.window_count, s.ci.o2level);
}
```

Check out lines 16-17! That's where we're initializing members of the `struct cabin_information` in the definition of `s`, our `struct spaceship`.

> 查看 16-17 行！这就是我们在定义`s`(我们的'struct spaceship')时初始化'struct cabin_information'成员的地方。

And here is another option for that same initializer---this time we'll do something more standard-looking, but either approach works:

> 这里有另一个选项来初始化，这次我们会做一些看起来更标准的事情，但是任何一种方法都可以工作：

```c
    struct spaceship s = {
        .manufacturer="General Products",
        .ci={
            .window_count = 8,
            .o2level = 21
        }
    };
```

Now, as if the above information isn't spectacular enough, we can also mix in array initializers in there, too.

> 现在，就好像上面的信息还不够出色，我们**还可以把数组初始化器混合进去**。

Let's change this up to get an array of passenger information in there, and we can check out how the initializers work in there, too.

> 让我们改变一下，把乘客信息放进数组里，我们也可以看看初始化器是如何在里面工作的。

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

int main(void) {
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

## [20.2] Anonymous `struct` s {#anonymous-structs number="20.2"}

These are "the `struct` with no name". We also mention these in the [`typedef`](#typedef-struct) section, but we'll refresh here.

> 这些是没有名字的 `struct`。我们也在[`typedef`](#typedef-struct)部分提到了这些，但我们在这里重新回顾一下。

Here's a regular `struct`:

```c
struct animal {
    char *name;
    int leg_count, speed;
};
```

And here's the anonymous equivalent:

```c
struct {              // <-- No name!
    char *name;
    int leg_count, speed;
};
```

Okaaaaay. So we have a `struct`, but it has no name, so we have no way of using it later? Seems pretty pointless.

> 哦，好吧。所以我们**有一个 `struct`，但它没有名字，所以我们没有办法以后使用它？看起来没什么意义**。

Admittedly, in that example, it is. But we can still make use of it a couple ways.

> 承认，在那个例子里，是这样。但我们仍然可以利用它几种方式。

One is rare, but since the anonymous `struct` represents a type, we can just put some variable names after it and use them.

> 一个是罕见的，但由于**匿名 `struct` 代表一种类型，我们可以在它后面放一些变量名，并使用它们**。

```c
struct {                   // <-- No name!
    char *name;
    int leg_count, speed;
} a, b, c;                 // 3 variables of this struct type

a.name = "antelope";
c.leg_count = 4;           // for example
```

But that's still not that useful.

Far more common is use of anonymous `struct` s with a `typedef` so that we can use it later (e.g. to pass variables to functions).

> 更常见的是**使用匿名结构体和 `typedef`，以便我们稍后使用它(例如将变量传递给函数)**。

```c
typedef struct {                   // <-- No name!
    char *name;
    int leg_count, speed;
} animal;                          // New type: animal

animal a, b, c;

a.name = "antelope";
c.leg_count = 4;           // for example
```

Personally, I don't use many anonymous `struct` s. I think it's more pleasant to see the entire `struct animal` before the variable name in a declaration.

> 我个人不常使用匿名结构体。我认为在声明中在变量名称之前看到整个 `struct animal` 更加令人愉悦。

But that's just, like, my opinion, man.

## [20.3] Self-Referential `struct` s {#self-referential-structs number="20.3"}

For any graph-like data structure, it's useful to be able to have pointers to the connected nodes/vertices. But this means that in the definition of a node, you need to have a pointer to a node. It's chicken and eggy!

> 对于**任何类似图形的数据结构，能够指向相连的节点/顶点是很有用的**。但这意味着在节点的定义中，你**需要有一个指向节点的指针**。这就是先有鸡还是先有蛋的问题！

But it turns out you can do this in C with no problem whatsoever. For example, here's a linked list node:

```c
struct node {
    int data;
    struct node *next;
};
```

It's important to note that `next` is a pointer. This is what allows the whole thing to even build. Even though the compiler doesn't know what the entire `struct node` looks like yet, all pointers are the same size.

> 重要的是**要注意 `next` 是一个指针**。这就是使整个事情能够建立的原因。**尽管编译器还不知道整个 `struct node` 的样子，但所有的指针都是相同大小的**。

Here's a cheesy linked list program to test it out:

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

Running that prints:

```{.sourceCode .default}
11
22
33
```

## [20.4] Flexible Array Members {#flexible-array-members number="20.4"}

Back in the good old days, when people carved C code out of wood, some folks thought would be neat if they could allocate `struct` s that had variable length arrays at the end of them.

> 回到那美好的日子，当人们用木头雕刻 C 代码时，有些人认为如果他们**可以在结构体的末尾分配可变长度数组就很棒**。

I want to be clear that the first part of the section is the old way of doing things, and we're going to do things the new way after that.

> 我想清楚地表明，这一部分的第一部分是旧的做法，在那之后我们将以新的方式来做事情。

For example, maybe you could define a `struct` for holding strings and the length of that string. It would have a length and an array to hold the data. Maybe something like this:

> 例如，也许你可以定义一个 `struct` 来保存字符串和字符串的长度。它将具有长度和一个数组来保存数据。也许像这样：

```c
struct len_string {
    int length;
    char data[8];
};
```

But that has `8` hardcoded as the maximum length of a string, and that's not much. What if we did something _clever_ and just `malloc()` d some extra space at the end after the struct, and then let the data overflow into that space?

> 但是，它将 `8` 硬编码为字符串的最大长度，这不是很多。如果我们做一些聪明的事情，在结构之后 `malloc()` 一些额外的空间，然后让数据溢出到该空间呢？

Let's do that, and then allocate another 40 bytes on top of it:

```c
struct len_string *s = malloc(sizeof *s + 40);
```

Because `data` is the last field of the `struct`, if we overflow that field, it runs out into space that we already allocated! For this reason, this trick only works if the short array is the _last_ field in the `struct`.

> **因为 `data` 是 `struct` 的最后一个字段，如果我们溢出了该字段，它就会进入我们已经分配的空间！** 因此，这个技巧只有在短数组是 `struct` 的最后一个字段时才有效。

```c
// Copy more than 8 bytes!

strcpy(s->data, "Hello, world!");  // Won't crash. Probably.
```

In fact, there was a common compiler workaround for doing this, where you'd allocate a zero length array at the end:

> 事实上，有一种通用的编译器解决方案可以做到这一点，即**在末尾分配一个零长度数组**：

```c
struct len_string {
    int length;
    char data[0];
};
```

And then every extra byte you allocated was ready for use in that string.

Because `data` is the last field of the `struct`, if we overflow that field, it runs out into space that we already allocated!

> 因为 `data` 是 `struct` 的最后一个字段，如果我们溢出了该字段，它就会进入我们已经分配的空间！

```c
// Copy more than 8 bytes!

strcpy(s->data, "Hello, world!");  // Won't crash. Probably.
```

But, of course, actually accessing the data beyond the end of that array is undefined behavior! In these modern times, we no longer deign to resort to such savagery.

> 但是，当然，实际访问数组末尾之外的数据是没有定义的行为！在这个现代时代，我们不再屈尊于这种野蛮行为。

Luckily for us, we can still get the same effect with C99 and later, but now it's legal.

> 幸运的是，我们可以使用 C99 及更高版本来获得同样的效果，而且现在这是合法的。

Let's just change our above definition to have no size for the array[^133^]:

> 让我们把上面的定义改变一下，让数组没有大小(133 号脚注)：

```c
struct len_string {
    int length;
    char data[];
};
```

Again, this only works if the flexible array member is the _last_ field in the `struct`.

> 再次，只有当灵活数组成员是 `struct` 中的最后一个字段时，此操作才有效。

And then we can allocate all the space we want for those strings by `malloc()` ing larger than the `struct len_string`, as we do in this example that makes a new `struct len_string` from a C string:

> 然后，我们可以为这些字符串分配我们想要的所有空间，就像我们在这个例子中一样，使用 `malloc()` 从 C 字符串创建新的 `struct len_string`：

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

## [20.5] Padding Bytes {#struct-padding-bytes number="20.5"}

Beware that C is allowed to add padding bytes within or after a `struct` as it sees fit. You can't trust that they will be directly adjacent in memory[^134^].

> 小心，C 可以根据自己的意愿在 `struct` 中或之后添加填充字节。你不能相信它们会直接排列在内存中[^134^]。

Let's take a look at this program. We output two numbers. One is the sum of the `sizeof` s the individual field types. The other is the `sizeof` the entire `struct`.

> 让我们看一下这个程序。我们输出两个数字。一个是各个字段类型的 `sizeof` 之和，另一个是整个 `struct` 的 `sizeof`。

One would expect them to be the same. The size of the total is the size of the sum of its parts, right?

> 一个人会期望它们是相同的。总体的大小就是它的部分之和的大小，对吗？

```c
#include <stdio.h>

struct foo {
    int a;
    char b;
    int c;
    char d;
};

int main(void) {
    printf("%zu\n", sizeof(int) + sizeof(char) + sizeof(int) + sizeof(char));
    printf("%zu\n", sizeof(struct foo));
}
```

But on my system, this outputs:

```{.sourceCode .default}
10
16
```

:::

They're not the same! The compiler has added 6 bytes of padding to help it be more performant. Maybe you got different output with your compiler, but unless you're forcing it, you can't be sure there's no padding.

> 他们不一样！**编译器添加了 6 个字节的填充来帮助它更具性能**。也许你用你的编译器得到了不同的输出，但除非你强制它，**你不能确定没有填充**。

## [20.6] `offsetof` {#offsetof number="20.6"}

In the previous section, we saw that the compiler could inject padding bytes at will inside a structure.

> 在上一节中，我们看到编译器可以随意在结构内部注入填充字节。

What if we needed to know where those were? We can measure it with `offsetof`, defined in `<stddef.h>`.

> 如果我们需要知道这些在哪里？我们可以使用 `offsetof`，它定义在 `<stddef.h>` 中来测量它。

Let's modify the code from above to print the offsets of the individual fields in the `struct`:

> 让我们修改上面的代码，打印 `struct` 中各个字段的偏移量：

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

For me, this outputs:

```{.sourceCode .default}
0
4
8
12
```

indicating that we're using 4 bytes for each of the fields. It's a little weird, because `char` is only 1 byte, right? The compiler is putting 3 padding bytes after each `char` so that all the fields are 4 bytes long. Presumably this will run faster on my CPU.

> 指出我们**为每个字段使用 4 个字节。这有点奇怪，因为 `char` 只有 1 个字节**，对吗？编译器在每个 `char` 后面添加 3 个填充字节，以使所有字段长度为 4 个字节。据推测，**这将在我的 CPU 上运行得更快**。

## [20.7] Fake OOP {#fake-oop number="20.7"}

There's a slightly abusive thing that's sort of OOP-like that you can do with `struct` s.

> 你可以用 `struct` 做一些略带滥用性质的、类似面向对象编程的事情。

Since the pointer to the `struct` is the same as a pointer to the first element of the `struct`, you can freely cast a pointer to the `struct` to a pointer to the first element.

> **由于指向结构体的指针与指向结构体第一个元素的指针相同**，因此可以自由地将指向结构体的指针转换为指向结构体第一个元素的指针。

What this means is that we can set up a situation like this:

```c
struct parent {
    int a, b;
};

struct child {
    struct parent super;  // MUST be first
    int c, d;
};
```

Then we are able to pass a pointer to a `struct child` to a function that expects either that _or_ a pointer to a `struct parent`!

> 那么我们就可以将一个指向 `struct child` 的指针传递给一个期望接收一个指向 `struct parent` 的指针的函数！

Because `struct parent super` is the first item in the `struct child`, a pointer to any `struct child` is the same as a pointer to that `super` field[^135^].

> 因为 `struct parent super` 是 `struct child` 中的第一个项目，**所以指向任何 `struct child` 的指针都与指向该 `super` 字段的指针相同**。

Let's set up an example here. We'll make `struct` s as above, but then we'll pass a pointer to a `struct child` to a function that needs a pointer to a `struct parent`... and it'll still work.

> 让我们在这里设置一个例子。我们将创建上述的 `struct`，然后将一个 `struct child` 的指针传递给一个需要一个 `struct parent` 指针的函数...它仍然可以正常工作。

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

See what we did on the last line of `main()`? We called `print_parent()` but passed a `struct child*` as the argument! Even though `print_parent()` needs the argument to point to a `struct parent`, we're _getting away with it_ because the first field in the `struct child` is a `struct parent`.

> 看看我们在 `main()` 的最后一行做了什么？我们调用了 `print_parent()`，但是传入了一个 `struct child*` 作为参数！尽管 `print_parent()` 需要参数指向一个 `struct parent`，但是我们*逃脱了*，因为 `struct child` 的第一个字段是一个 `struct parent`。

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

```c
#include <stdio.h>

struct foo {
    unsigned int a;
    unsigned int b;
    unsigned int c;
    unsigned int d;
};

int main(void) {
    printf("%zu\n", sizeof(struct foo));
}
```

For me, this prints `16`. Which makes sense, since `unsigned` s are 4 bytes on my system.

> 对我来说，这会打印出 `16`。这是有意义的，因为在我的系统上，`无符号` 的字节数是 4 个。

But what if we knew that all the values that were going to be stored in `a` and `b` could be stored in 5 bits, and the values in `c`, and `d` could be stored in 3 bits? That's only a total 16 bits. Why have 128 bits reserved for them if we're only going to use 16?

> 如果我们知道可以用 5 位来存储 a 和 b 中的所有值，而 c 和 d 中的值可以用 3 位来存储，那么只需要 16 位就可以了，为什么要预留 128 位呢？

Well, we can tell C to pretty-please try to pack these values in. We can specify the maximum number of bits that values can take (from 1 up the size of the containing type).

> 嗯，我们可以让 C 语言尽量把这些值打包起来。我们可以指定值所能占用的最大位数(从 1 开始到包含类型的大小)。

We do this by putting a colon after the field name, followed by the field width in bits.

> 我们通过**在字段名称后面加上冒号，然后跟上字段宽度的位数来实现这一点**。

```c
struct foo {
    unsigned int a:5;
    unsigned int b:5;
    unsigned int c:3;
    unsigned int d:3;
};
```

Now when I ask C how big my `struct foo` is, it tells me 4! It was 16 bytes, but now it's only 4. It has "packed" those 4 values down into 4 bytes, which is a four-fold memory savings.

> 现在当我问 C 有多大的 `struct foo` 时，它告诉我 4！它原来是 16 字节，现在只有 4 字节。它把这 4 个值压缩到 4 字节中，节省了 4 倍的内存。

The tradeoff is, of course, that the 5-bit fields can only hold values from 0-31 and the 3-bit fields can only hold values from 0-7. But life's all about compromise, after all.

> 交换的是，5 位字段只能保存 0-31 的值，而 3 位字段只能保存 0-7 的值。但毕竟，生活就是要做出妥协。

### [20.8.1] Non-Adjacent Bit-Fields {#non-adjacent-bit-fields number="20.8.1"}

A gotcha: C will only combine **adjacent** bit-fields. If they're interrupted by non-bit-fields, you get no savings:

> C 只会合并相邻的位域，如果它们被非位域打断，你就无法节省空间。

```c
struct foo {            // sizeof(struct foo) == 16 (for me)
    unsigned int a:1;   // since a is not adjacent to c.
    unsigned int b;
    unsigned int c:1;
    unsigned int d;
};
```

In that example, since `a` is not adjacent to `c`, they are both "packed" in their own `int` s.

> 在这个例子中，由于 a 与 c 不相邻，它们都被“打包”在自己的 int 中。

So we have one `int` each for `a`, `b`, `c`, and `d`. Since my `int` s are 4 bytes, that's a grand total of 16 bytes.

> 所以我们每个 `a`、`b`、`c` 和 `d` 有一个 `int`。由于我的 `int` 是 4 个字节，总共是 16 个字节。

A quick rearrangement yields some space savings from 16 bytes down to 12 bytes (on my system):

> 快速重新排列可以将字节数从 16 字节减少到 12 字节(在我的系统上)。

```c
struct foo {            // sizeof(struct foo) == 12 (for me)
    unsigned int a:1;
    unsigned int c:1;
    unsigned int b;
    unsigned int d;
};
```

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

> 例如，假设你有一个字节，其中顶部 2 位有意义，底部 1 位有意义，但中间 5 位没有被你使用[^136^]。

We _could_ do something like this:

```c
struct foo {
    unsigned char a:2;
    unsigned char dummy:5;
    unsigned char b:1;
};
```

And that works---in our code we use `a` and `b`, but never `dummy`. It's just there to eat up 5 bits to make sure `a` and `b` are in the "required" (by this contrived example) positions within the byte.

> 我们的代码中使用了 `a` 和 `b`，但从不使用 `dummy`，它只是为了占据 5 位，以确保 `a` 和 `b` 在字节中处于所需(由这个约定的例子)的位置。

C allows us a way to clean this up: _unnamed bit-fields_. You can just leave the name (`dummy`) out in this case, and C is perfectly happy for the same effect:

> C 允许我们清理这个：_未命名的位域_。在这种情况下，可以省略名称(`dummy`)，C 也完全可以接受，以达到同样的效果：

```c
struct foo {
    unsigned char a:2;
    unsigned char :5;   // <-- unnamed bit-field!
    unsigned char b:1;
};
```

### [20.8.4] Zero-Width Unnamed Bit-Fields {#zero-width-unnamed-bit-fields number="20.8.4"}

Some more esoterica out here... Let's say you were packing bits into an `unsigned int`, and you needed some adjacent bit-fields to pack into the _next_ `unsigned int`.

> 如果你需要把一些相邻的位字段打包到下一个无符号整数中，那么在这里有更多的深奥知识...

That is, if you do this:

```c
struct foo {
    unsigned int a:1;
    unsigned int b:2;
    unsigned int c:3;
    unsigned int d:4;
};
```

the compiler packs all those into a single `unsigned int`. But what if you needed `a` and `b` in one `int`, and `c` and `d` in a different one?

> 编译器将所有这些打包到一个无符号整数中。但是如果你需要将 a 和 b 放在一个整数中，将 c 和 d 放在另一个整数中怎么办？

There's a solution for that: put an unnamed bit-field of width `0` where you want the compiler to start anew with packing bits in a different `int`:

> 这有一个解决方案：在你想要编译器从新开始在不同的 int 中打包位的地方放置一个未命名的宽度为 0 的位域。

```c
struct foo {
    unsigned int a:1;
    unsigned int b:2;
    unsigned int :0;   // <--Zero-width unnamed bit-field
    unsigned int c:3;
    unsigned int d:4;
};
```

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

```c
union foo {
    int a, b, c, d, e, f;
    float g, h;
    char i, j, k, l;
};
```

Now, that's a lot of fields. If this were a `struct`, my system would tell me it took 36 bytes to hold it all.

> 现在，这可是很多字段。如果这是一个'struct'，我的系统会告诉我需要 36 个字节来容纳它们。

But it's a `union`, so all those fields overlap in the same stretch of memory. The biggest one is `int` (or `float`), taking up 4 bytes on my system. And, indeed, if I ask for the `sizeof` the `union foo`, it tells me 4!

> 但它是一个联合，所以所有这些字段都在同一块内存中重迭。最大的是 int(或 float)，在我的系统上占用 4 个字节。而且，如果我询问 union foo 的 sizeof，它告诉我 4！

The tradeoff is that you can only portably use one of those fields at a time. However...

> 交换是你一次只能可移植地使用其中一个字段。但是...

### [20.9.1] Unions and Type Punning {#union-type-punning number="20.9.1"}

You can non-portably write to one `union` field and read from another!

Doing so is called [type punning](https://en.wikipedia.org/wiki/Type_punning)[^137^], and you'd use it if you really knew what you were doing, typically with some kind of low-level programming.

> 这样做被称为[类型双关][^137^], 如果你真的知道自己在做什么，通常是在做一些低级编程时会用到它。

Since the members of a union share the same memory, writing to one member necessarily affects the others. And if you read from one what was written to another, you get some weird effects.

> 由于工会成员共享同一个内存，写入一个成员自然也会影响其他成员。如果你从一个成员那里读取写给另一个成员的内容，就会产生一些奇怪的效果。

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

On my system, this prints out:

```
3.141590
4048
```

because under the hood, the object representation for the float `3.14159` was the same as the object representation for the short `4048`. On my system. Your results may vary.

> 因为**在底层，浮点数 `3.14159` 的对象表示与短数 `4048` 的对象表示相同**。在我的系统上，结果可能会有所不同。

### [20.9.2] Pointers to `union` s {#pointers-to-unions number="20.9.2"}

If you have a pointer to a `union`, you can cast that pointer to any of the types of the fields in that `union` and get the values out that way.

> 如果你有**一个指向联合体的指针，你可以把这个指针转换成联合体中任何一种类型**，然后从中取出值。

In this example, we see that the `union` has `int` s and `float` s in it. And we get pointers to the `union`, but we cast them to `int*` and `float*` types (the cast silences compiler warnings). And then if we dereference those, we see that they have the values we stored directly in the `union`.

> 在这个例子中，我们看到联合体中有整数和浮点数。我们得到指向联合体的指针，但我们将它们转换为 int *和 float *类型(转换可以消除编译器警告)。然后，如果我们解引用它们，我们会看到它们具有我们直接存储在联合体中的值。

```c
#include <stdio.h>

union foo {
    int a, b, c, d, e, f;
    float g, h;
    char i, j, k, l;
};

int main(void) {
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

The reverse is also true. If we have a pointer to a type inside the `union`, we can cast that to a pointer to the `union` and access its members.

> 反之亦然。如果我们在联合体内有一个指向类型的指针，我们可以将其转换为指向联合体的指针，并访问其成员。

```c
union foo x;
int *foo_int_p = (int *)&x;             // Pointer to int field
union foo *p = (union foo *)foo_int_p;  // Back to pointer to union

p->a = 12;  // This line the same as...
x.a = 12;   // this one.
```

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
