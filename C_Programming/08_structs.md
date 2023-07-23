# [8] Structs {#structs number="8"}

In C, we have something called a `struct`, which is a user-definable type that holds multiple pieces of data, potentially of different types.

> 在 C 语言中，我们有一种叫做 `struct` 的东西，它是一种用户可定义的类型，可以容纳多个不同类型的数据。

It's a convenient way to bundle multiple variables into a single one. This can be beneficial for passing variables to functions (so you just have to pass one instead of many), and useful for organizing data and making code more readable.

> 这是一种**将多个变量捆绑到一个变量的方便方法**。这对于**将变量传递给函数(只需要传递一个而不是多个)是有益的**，对于组织数据和使代码更具可读性也很有用。

If you've come from another language, you might be familiar with the idea of _classes_ and _objects_. These don't exist in C, natively[^67^]. You can think of a `struct` as a class with only data members, and no methods.

> 如果你来自另一种语言，你可能熟悉 _类_ 和 _对象_ 的概念。这些在 C 语言中本身不存在[^67^]。你**可以把 `struct` 看作是一个只有数据成员，没有方法的类**。

## [8.1] Declaring a Struct {#declaring-a-struct number="8.1"}

You can declare a `struct` in your code like so:

```c
struct car {
    char *name;
    float price;
    int speed;
};
```

This is often done at the global scope outside any functions so that the `struct` is globally available.

> 这通常在全局作用域之外的任何函数中完成，以便 `struct` 可以全局使用。

When you do this, you're making a new _type_. The full type name is `struct car`. (Not just `car`---that won't work.)

> 当你这样做时，你正在**创建一种新的类型。完整的类型名称是 `struct car`(不只是 `car`---这样不行)**。

There aren't any variables of that type yet, but we can declare some:

```c
struct car saturn;  // Variable "saturn" of type "struct car"
```

And now we have an uninitialized variable `saturn`[^68^] of type `struct car`.

> 现在我们有一个未初始化的变量 `saturn`(参见注释 68)，类型为 `struct car`。

We should initialize it! But how do we set the values of those individual fields?

> 我们应该初始化它！但是我们如何设置这些单独字段的值？

Like in many other languages that stole it from C, we're going to use the dot operator (`.`) to access the individual fields.

> 就像在许多从 C 偷来的其他语言中一样，我们将**使用点运算子(`.`)来访问个别字段**。

```c
saturn.name = "Saturn SL/2";
saturn.price = 15999.99;
saturn.speed = 175;

printf("Name:           %s\n", saturn.name);
printf("Price (USD):    %f\n", saturn.price);
printf("Top Speed (km): %d\n", saturn.speed);
```

There on the first lines, we set the values in the `struct car`, and then in the next bit, we print those values out.

> 在第一行，我们在 `struct car` 中设置了值，然后在下一段中，我们打印出这些值。

## [8.2] Struct Initializers {#struct-initializers number="8.2"}

That example in the previous section was a little unwieldy. There must be a better way to initialize that `struct` variable!

> 上一节中的那个例子有点繁琐。一定有更好的方法来初始化那个 `struct` 变量！

You can do it with an initializer by putting values in for the fields _in the order they appear in the `struct`_ when you define the variable. (This won't work after the variable has been defined---it has to happen in the definition).

> 你可以通过在定义变量时为字段提供值(按照它们在结构中出现的顺序)来使用初始化程序(这在变量定义后不起作用---必须在定义时发生)。

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

The fact that the fields in the initializer need to be in the same order is a little freaky. If someone changes the order in `struct car`, it could break all the other code!

> 事实上，初始化程序中的字段**需要按相同的顺序排列有点可怕**。如果有人改变 `struct car` 中的顺序，可能会破坏所有其他代码！

We can be more specific with our initializers:

```c
struct car saturn = {.speed=175, .name="Saturn SL/2"};
```

Now it's independent of the order in the `struct` declaration. Which is safer code, for sure.

> 现在它**独立于结构声明中的顺序**，这是更安全的代码。

Similar to array initializers, any missing field designators are initialized to zero (in this case, that would be `.price`, which I've omitted).

> **类似于数组初始化，任何缺失的字段指示符都会被初始化为零**(在这种情况下，就是我省略的 `.price`)。

## [8.3] Passing Structs to Functions {#passing-structs-to-functions number="8.3"}

You can do a couple things to pass a `struct` to a function.

1. Pass the `struct`.
2. Pass a pointer to the `struct`.

Recall that when you pass something to a function, a _copy_ of that thing gets made for the function to operate on, whether it's a copy of a pointer, an `int`, a `struct`, or anything.

> 当你把某件事传递给一个函数时，会为该函数创建一个 _副本_，无论它是指针的副本、`int` 的副本、`struct` 的副本还是其他任何东西的副本。

There are basically two cases when you'd want to pass a pointer to the `struct`:

> 基本上有两种情况你会想要**传递一个指向结构体的指针**：

1. You need the function to be able to make changes to the `struct` that was passed in, and have those changes show in the caller.

> 你需要这个函数能够对传入的 `struct` 进行修改，并且在调用者中看到这些修改。

2. The `struct` is somewhat large and it's more expensive to copy that onto the stack than it is to just copy a pointer[^69^].

> 结构体有点大，把它复制到堆栈比只复制一个指针要贵得多。

For those two reasons, it's far more common to pass a pointer to a `struct` to a function, though its by no means illegal to pass the `struct` itself.

> 由于这两个原因，**传递指向结构体的指针到函数更为常见**，尽管传递结构体本身并不违法。

Let's try passing in a pointer, making a function that will allow you to set the `.price` field of the `struct car`:

> 让我们尝试传入一个指针，创建一个函数，让你可以设置 `struct car` 的 `price` 字段：

```c
#include <stdio.h>

struct car {
    char *name;
    float price;
    int speed;
};

int main(void) {
    struct car saturn = {.speed=175, .name="Saturn SL/2"};

    // Pass a pointer to this struct car, along with a new,
    // more realistic, price:
    set_price(&saturn, 799.99);
    printf("Price: %f\n", saturn.price);
}
```

You should be able to come up with the function signature for `set_price()` just by looking at the types of the arguments we have there.

> 你应该能够仅仅通过查看参数的类型就能想出 `set_price()` 的函数签名。

`saturn` is a `struct car`, so `&saturn` must be the address of the `struct car`, AKA a pointer to a `struct car`, namely a `struct car*`. And `799.99` is a `float`. So the function declaration must look like this:

```c
void set_price(struct car *c, float new_price)
```

We just need to write the body. One attempt might be:

```c
void set_price(struct car *c, float new_price) {
    c.price = new_price;  // ERROR!!
}
```

That won't work because the dot operator only works on `struct` s... it doesn't work on _pointers_ to `struct` s.

> 那不行，因为**点运算符只适用于 `struct`，不适用于 `struct` 的指针**。

Ok, so we can dereference the `struct` to de-pointer it to get to the `struct` itself. Dereferencing a `struct car*` results in the `struct car` that the pointer points to, which we should be able to use the dot operator on:

> 好的，所以我们可以取消引用结构体以取消指针，以获得结构体本身。 取消引用 `struct car *` 结果为指针指向的 `struct car`，我们应该能够使用点运算符：

```c
void set_price(struct car *c, float new_price) {
    (*c).price = new_price;  // Works, but is ugly and non-idiomatic :(
}
```

And that works! But it's a little clunky to type all those parens and the asterisk. C has some syntactic sugar called the _arrow operator_ that helps with that.

> 而且这可以工作！**但是要输入所有的括号和星号有点繁琐。C 有一些叫做箭头操作符的语法糖**，可以帮助解决这个问题。

## [8.4] The Arrow Operator {#the-arrow-operator number="8.4"}

The arrow operator helps refer to fields in pointers to `struct` s.

```c
void set_price(struct car *c, float new_price) {
    // (*c).price = new_price;  // Works, but non-idiomatic :(
    //
    // The line above is 100% equivalent to the one below:

    c->price = new_price;  // That's the one!
}
```

So when accessing fields, when do we use dot and when do we use arrow?

- If you have a `struct`, use dot (`.`).
- If you have a pointer to a `struct`, use arrow (`->`).

## [8.5] Copying and Returning `struct` s {#copying-and-returning-structs number="8.5"}

Here's an easy one for you! Just assign from one to the other!

```c
struct car a, b;

b = a;  // Copy the struct
```

And returning a `struct` (as opposed to a pointer to one) from a function also makes a similar copy to the receiving variable.

> 返回一个 `struct`(而不是指向它的指针)从一个函数也会给接收变量做一个类似的复制。

This is not a "deep copy"[^70^]. All fields are copied as-is, including pointers to things.

> 这不是一个“深拷贝”[^70^]。**所有字段都是原样复制，包括指向物体的指针**。

## [8.6] Comparing `struct` s {#comparing-structs number="8.6"}

There's only one safe way to do it: compare each field one at a time.

You might think you could use [`memcmp()`](https://beej.us/guide/bgclr/html/split/stringref.html#man-strcmp)[^71^], but that doesn't handle the case of the possible [padding bytes](#struct-padding-bytes) that might be in there.

> 你可能会认为可以使用 `memcmp()`，但这不能处理可能存在的填充字节的情况。

If you clear the `struct` to zero first with [`memset()`](https://beej.us/guide/bgclr/html/split/stringref.html#man-memset)[^72^], then it _might_ work, though there could be weird elements that [might not compare as you expect](https://stackoverflow.com/questions/141720/how-do-you-compare-structs-for-equality-in-c)[^73^].

> 如果你先用[`memset()`][^72^]把 `struct` 清零，那么它 _可能_ 会起作用，但也可能会有一些奇怪的元素[不能按你期望的方式比较][^73^]。
