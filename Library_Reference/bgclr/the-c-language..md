---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}
[Prev](foreword.html) \| [Contents](index.html) \| [Next](assert.html)
:::

------------------------------------------------------------------------

# [2]{.header-section-number} The C Language {#the-c-language number="2"}

This is just a quick overview of the fashionable and fun highlights of the syntax, keywords, and other animals in the C menagerie.

## [2.1]{.header-section-number} Background {#background number="2.1"}

Some things you'll need to make sense of the examples, below.

### [2.1.1]{.header-section-number} Comments {#comments number="2.1.1"}

Comments in C start with `//` and go to the end of a line.

Multiline comments begin with `/*` and continue until a closing `*/`.

### [2.1.2]{.header-section-number} Separators {#separators number="2.1.2"}

Expressions in C are separated by semicolons (`;`). These tend to appear at the ends of lines.

### [2.1.3]{.header-section-number} Expressions {#expressions number="2.1.3"}

If it's not a keyword or other reserved punctuation, it tends to be an expression. Think "math including function calls".

### [2.1.4]{.header-section-number} Statements {#statements number="2.1.4"}

Think `if`, `while`, etc. Executable keywords.

### [2.1.5]{.header-section-number} Booleans {#booleans number="2.1.5"}

Ignoring the `bool` type, zero is false and non-zero is true.

### [2.1.6]{.header-section-number} Blocks {#blocks number="2.1.6"}

Multiple expressions and flow control keywords can be wrapped up in a block, made up of `{` followed by one or more expressions or statements, followed by `}`.

### [2.1.7]{.header-section-number} Code Examples {#code-examples number="2.1.7"}

They are meant to give an idea of how to use various statements, but not be comprehensive in terms of examples.

In the examples, below, if either an expression or statement can be used, the word `code` is inserted.

## [2.2]{.header-section-number} Operators {#operators number="2.2"}

### [2.2.1]{.header-section-number} Arithmetic Operators {#arithmetic-operators number="2.2.1"}

The arithmetic operators: `+`, `-`, `*`, `/`, `%` (remainder).

Division is integer if all arguments are integers. Otherwise it's a floating result.

You can also negate an expression by putting `-` in front of it. (You can also put a `+` in front of it---this doesn't do anything mathematically, but it causes the Usual Arithmetic Conversions to be performed on the expression.)

### [2.2.2]{.header-section-number} Pre- and Post-Increment and -Decrement {#pre--and-post-increment-and--decrement number="2.2.2"}

The post-increment (`++`) and post-decrement (`--`) operators (after the variable) do their work *after* the rest of the expression has been evaluated.

::: {#cb1 .sourceCode}
``` {.sourceCode .c}
int x = 10;
int y = 20;
int z = 30;

int w = (x++) + (y--) + (z++);

print("%d %d %d %d\n", x, y, z, w);  // 11 19 31 60
```
:::

The pre-increment (`++`) and pre-decrement (`--`) operators (before the variable) do their work *before* the rest of the expression has been evaluated.

::: {#cb2 .sourceCode}
``` {.sourceCode .c}
int x = 10;
int y = 20;
int z = 30;

int w = (++x) + (--y) + (++z);

print("%d %d %d %d\n", x, y, z, w);  // 11 19 31 61
```
:::

### [2.2.3]{.header-section-number} Comparison Operators {#comparison-operators number="2.2.3"}

All of these return a Boolean true-y or false-y value.

Less than, greater than, and equal to are: `<`, `>`, `==`, respectively.

Less than or equal to and greater than or equal to are `<=` and `>=`.

Not equal to is `!=`.

### [2.2.4]{.header-section-number} Pointer Operators {#pointer-operators number="2.2.4"}

`*` in front of a pointer variable dereferences that variable.

`&` in front of a variable gives the address of that variable.

`+` and `-` arithmetic operators work on pointers for pointer arithmetic.

### [2.2.5]{.header-section-number} Structure and Union Operators {#structure-and-union-operators number="2.2.5"}

The dot operator (`.`) can get a field value out of a `struct` or `union`.

The arrow operator (`->`) can get a field value out of a pointer to a `struct` or `union`. These two are equivalent, assuming `p` is just such a pointer:

::: {#cb3 .sourceCode}
``` {.sourceCode .c}
(*p).bar;
p->bar;
```
:::

### [2.2.6]{.header-section-number} Array Operators {#array-operators number="2.2.6"}

The square bracket operators can reference a value in an array:

::: {#cb4 .sourceCode}
``` {.sourceCode .c}
a[10] = 99;
```
:::

This is syntactic sugar over pointer arithmetic and referencing. The above line is equivalent to:

::: {#cb5 .sourceCode}
``` {.sourceCode .c}
*(a + 10) = 99;
```
:::

### [2.2.7]{.header-section-number} Bitwise Operators {#bitwise-operators number="2.2.7"}

Bit shift right: `>>`, bit shift left: `<<`.

    int i = x << 3;  // left shift 3 bits

Whether or not a right shift on a signed value is sign-extended is implementation-defined.

Bitwise AND, OR, NOT, and XOR are `&`, `|`, `~`, and `^`, respectively.

### [2.2.8]{.header-section-number} Assignment Operators {#assignment-operators number="2.2.8"}

A standalone `=` is your basic assignment.

But there are also compound assignments that are like a shorthand version. For example, these two are basically equivalent:

::: {#cb7 .sourceCode}
``` {.sourceCode .c}
x = x + 1;
x += 1;
```
:::

There are compound assignment operators for many of the other operators.

Arithmetic: `+=`, `-=`, `*=`, `/=`, and `%=`.

Bitwise: `|=`, `&=`, `~=`, and `^=`.

### [2.2.9]{.header-section-number} The `sizeof` Operator {#the-sizeof-operator number="2.2.9"}

This is a compile-time operator that gives you the size in bytes of the type of the argument. The type of the expression is used; the expression is not evaluated. `sizeof` works with any type, even user-defined composite types.

The return type is the integer type `size_t`.

    float f;
    size_t x = sizeof f;

    printf("f is %zu bytes\n", x);

You can also specify a raw type name in there by wrapping it in parentheses:

::: {#cb9 .sourceCode}
``` {.sourceCode .c}
size_t x = sizeof(int);

printf("int is %zu bytes\n", x);
```
:::

### [2.2.10]{.header-section-number} Type Casts {#type-casts number="2.2.10"}

You can force an expression to be another type (within reason) by *casting* to that type.

You give the new type name in parentheses.

Here we are forcing the subexpression `x` to be type `float` just before the division[^11^](footnotes.html#fn11){#fnref11 .footnote-ref role="doc-noteref"}. This causes the division, which would otherwise be an integer division, to be a floating point division.

::: {#cb10 .sourceCode}
``` {.sourceCode .c}
int x = 17;
int y = 2;

float f = (float)x / y;
```
:::

### [2.2.11]{.header-section-number} `_Alignof` Operator {#alignof-operator number="2.2.11"}

You can get the byte alignment of any type with the `_Alignof` compile-time operator. If you include `<stdalign.h>`, you can use `alignof` instead.

Any type can be the argument to the operator, which must be in parenthesis. Unlike `sizeof`, the argument cannot be an expression.

::: {#cb11 .sourceCode}
``` {.sourceCode .c}
printf("Alignment of int is %zu\n", alignof(int));
```
:::

### [2.2.12]{.header-section-number} Comma Operator {#comma-operator number="2.2.12"}

You can separate subexpressions with commas, and each will be evaluated from left to right, and the value of the entire expression will be the value of the subexpression after the last comma.

::: {#cb12 .sourceCode}
``` {.sourceCode .c}
int x = (1, 2, 3);  // Silly way to assign `x = 3`
```
:::

Usually this is used in the various clauses in loops. For example, we can do multiple assignments in a `for` loop, and have multiple post expressions like this:

::: {#cb13 .sourceCode}
``` {.sourceCode .c}
for (i = 2, j = 10; i < 100; i++, j += 4) { ... }
```
:::

## [2.3]{.header-section-number} Type Specifiers {#type-specifiers number="2.3"}

Integer types from smallest to largest capacity: `char`, `short`, `int`, `long`, `long long`.

Any integer type may be prefaced with `signed` (the default except for `char`) or `unsigned`.

Whether or not `char` is signed is implementation defined.

Floating types from least accuracy to most: `float`, `double`, `long double`.

`void` is a type representing lack of type.

`_Bool` is a Boolean type. This becomes `bool` in C23. Earlier versions of C must include `<stdbool.h>` to get `bool`.

`_Complex` indicates a complex floating type type, when paired with such a type. Include `<complex.h>` to use `complex` instead.

::: {#cb14 .sourceCode}
``` {.sourceCode .c}
complex float x = 1.2 + 2.3*I;
complex double y = 1.2 + 2.3*I;
```
:::

`_Imaginary` is an optional keyword used to specify an imaginary type (the imaginary part of a complex number) when paired with a floating type. Include `<complex.h>` to use `imaginary` instead. Neither GCC nor clang support this.

::: {#cb15 .sourceCode}
``` {.sourceCode .c}
imaginary float f = 2.3*I;
```
:::

`_Generic` is a type "switcher" that allows you to emit different code at compile time depending on the type of the data.

## [2.4]{.header-section-number} Constant Types {#constant-types number="2.4"}

You can declare constants to be of specific types (though it might be a larger type). In the following example unqualified types, case doesn't matter, and the `U` can come before or after the `L` or `LL`.

::: {#cb16 .sourceCode}
``` {.sourceCode .c}
123              int or larger
123L             long int or larger
123LL            long long int

123U             unsigned int or larger
123UL            unsigned long int or larger
123ULL           unsigned long long int

123.4F           float
123.4            double
123.4L           long double

'a'              char
"hello, world"   char* (string)
```
:::

You can specify the constant in other bases as well:

::: {#cb17 .sourceCode}
``` {.sourceCode .c}
123              decimal
0x123            hexadecimal
0123             octal
```
:::

You can also specify floating constants in base-10 exponential notation:

::: {#cb18 .sourceCode}
``` {.sourceCode .c}
1.2e3            1.2 x 10^3
```
:::

And you can specify floats in hex! Except in this case the exponent is still in decimal, and the base is 2 instead of 10:

::: {#cb19 .sourceCode}
``` {.sourceCode .c}
0x1.2p3          0x1.2 x 2^3
```
:::

## [2.5]{.header-section-number} Composite Types {#composite-types number="2.5"}

### [2.5.1]{.header-section-number} `struct` Types {#struct-types number="2.5.1"}

You can build a composite type made out of other types with `struct` and then declare variables to be of that type.

::: {#cb20 .sourceCode}
``` {.sourceCode .c}
struct animal {
    char *name;
    int leg_count;
};

struct animal a;
struct animal b = {"goat", 4};
struct animal c = {.name="goat", .leg_count=4};
```
:::

Accessing is done with the dot operator (`.`) or, if the variable is a pointer to a `struct`, the arrow operator (`->`).

::: {#cb21 .sourceCode}
``` {.sourceCode .c}
struct animal *p = b;

printf("%d\n", b.leg_count);
printf("%d\n", p->leg_count);
```
:::

### [2.5.2]{.header-section-number} `union` Types {#union-types number="2.5.2"}

These are like `struct` types in usage, except that you can only use one field at a time. (The fields all use the same region of memory.)

::: {#cb22 .sourceCode}
``` {.sourceCode .c}
union dt {
    float distance;
    int time;
};

union dt a;
union dt b = {6};            // Initializes "distance", the first field
union dt c = {.distance=6};  // Initializes "distance"
union dt d = {.time=6};      // Initializes "time"
```
:::

Accessing is done with the dot operator (`.`) or, if the variable is a pointer to a `union`, the arrow operator (`->`).

::: {#cb23 .sourceCode}
``` {.sourceCode .c}
union dt *p = b;

printf("%d\n", b.time);
printf("%d\n", p->time);
```
:::

### [2.5.3]{.header-section-number} `enum` Types {#enum-types number="2.5.3"}

Gives you a typed way to have named constant integer values. These can be used with `switch()`, or as an array size, or any other place constant values are needed.

Names are conventionally capitalized.

::: {#cb24 .sourceCode}
``` {.sourceCode .c}
enum animal {
    ANTELOPE,
    BADGER,
    CAT,
    DOG,
    ELEPHANT,
    FISH
};

enum animal a = CAT;

if (a == CAT)
    printf("The animal is a cat.\n");
```
:::

The names have numeric values starting with zero and counting up. (In the example above, `DOG` would be `3`.)

The numeric value can be overridden by specifying an integer exactly. Subsequent values increment from the specified one.

::: {#cb25 .sourceCode}
``` {.sourceCode .c}
enum animal {
    ANTELOPE = 4,
    BADGER,         // Will be 5
    CAT,            // Will be 6
    DOG = 3,
    ELEPHANT,       // Will be 4
    FISH            // Will be 5
};
```
:::

As above, duplicate values are not illegal, but might be of marginal usefulness.

## [2.6]{.header-section-number} Initializers {#initializers number="2.6"}

You can do this when the variable is defined, but not elsewhere.

Initializing basic types:

::: {#cb26 .sourceCode}
``` {.sourceCode .c}
int x = 12;
float y = 1.2;
char c = 'a';
char *s = "Hello, world!";
```
:::

Initializing array types:

::: {#cb27 .sourceCode}
``` {.sourceCode .c}
int a[3] = {1,2,3};
int a[] = {1,2,3};   // Same as a[3]

int a[3] = {1, 2};   // Same as {1, 2, 0}
int a[3] = {1};      // Same as {1, 0, 0}
int a[3] = {0};      // Same as {0, 0, 0}
```
:::

Initializing pointer types:

::: {#cb28 .sourceCode}
``` {.sourceCode .c}
int q;
int *p = &q;
```
:::

Initializing `struct`s:

::: {#cb29 .sourceCode}
``` {.sourceCode .c}
struct s {
    int a;
    float b;
};

struct s x0 = {1, 2.2}; // Initialize fields in order

struct s x0 = {.a=1, .b=2.2}; // Initialize fields by name
struct s x0 = {.b=2.2, .a=1}; // Same thing

struct s x0 = {.b=2.2}; // All other fields initialized to 0
struct s x0 = {.b=2.2, .a-=0};  // Same thing
```
:::

Initializing `union`s:

::: {#cb30 .sourceCode}
``` {.sourceCode .c}
union u {
    int a;
    float b;
};

union u x0 = {1};  // Initialize the first field (a)

union u x0 = {.a=1};  // Initialize fields by name
union u x0 = {.b=2.2};

//union u x0 = {1, 2};       // ILLEGAL
//union u x0 = {.a1, ,b=2};  // ILLEGAL
```
:::

## [2.7]{.header-section-number} Compound Literals {#compound-literals number="2.7"}

You can declare "unnamed" objects in C. This is often useful for passing a `struct` to a function that otherwise doesn't need a name.

You use the type name in parens followed by an initializer to make the object.

Here's an example of passing a compound literal to a function. Note that there's no `struct s` variable in `main()`:

::: {#cb31 .sourceCode}
``` {.sourceCode .numberSource .c .numberLines}
#include <stdio.h>

struct s {
    int a, b;
};

int add(struct s x)
{
    return x.a + x.b;
}

int main(void)
{
    int t = add((struct s){.a=2, .b=4});  // <-- Here

    printf("%d\n", t);
}
```
:::

Compound literals have the lifetime of their scope.

You can also pass a pointer to a compound literal by taking its address:

::: {#cb32 .sourceCode}
``` {.sourceCode .c}
foo(&(struct s){1, 2});
```
:::

## [2.8]{.header-section-number} Type Aliases {#type-aliases number="2.8"}

You can set up a type alias for convenience or abstraction.

Here we'll make a new type called `time_counter` that is just an `int`. It can only be used exactly like an `int`. It's just an alias for an `int`.

::: {#cb33 .sourceCode}
``` {.sourceCode .c}
typedef int time_counter;

time_counter t = 3490;
```
:::

Also works with `struct`s or `union`s:

::: {#cb34 .sourceCode}
``` {.sourceCode .c}
struct foo {
    int bar;
    float baz;
};

typedef struct foo funtype;

funtype f = {1, 2}; // "funtype" is an alias for "struct foo";
```
:::

It also works inline, and with named or unnamed `struct`s or `union`s:

::: {#cb35 .sourceCode}
``` {.sourceCode .c}
typedef struct {
    int bar;
    float baz;
} funtype;

funtype f = {1, 2}; // "funtype" is an alias for the unnamed struct
```
:::

## [2.9]{.header-section-number} Additional Type-Related Specifiers {#additional-type-related-specifiers number="2.9"}

You can give the compiler more hints about what qualities a type should have using these specifiers and qualifiers.

### [2.9.1]{.header-section-number} Storage Class Specifiers {#storage-class-specifiers number="2.9.1"}

These can be placed before a type to provide more guidance about how the type is used.

::: {#cb36 .sourceCode}
``` {.sourceCode .c}
auto int a
register int a
static int a
extern int a
thread_local int a
```
:::

`auto` is the default, so it's basically never used. Indicates automatic storage duration (things like local variables get freed automatically when they fall out of scope). In C23 this keyword changes to indicate type inference like C++.

`register` indicates that accessing this variable should be as quick as possible. Restricts some usage of the variable giving the compiler a chance to optimize. Rare in daily use.

`static` at function scope indicates that this variable's value should persist from call to call. At file scope indicates that this variable should not be visible outside of this source file.

`extern` indicates that this variable refers to one declared in another source file.

`_Thread_local` means that every thread gets its own copy of this variable. You can use `thread_local` if you include `<threads.h>`.

### [2.9.2]{.header-section-number} Type Qualifiers {#type-qualifiers number="2.9.2"}

These can be placed before a type to provide more guidance about how the type is used.

::: {#cb37 .sourceCode}
``` {.sourceCode .c}
const int a
const int *p
int * const p
const int * const p
int * restrict p
volatile int a
atomic int a
```
:::

`const` means the value can't be modified. You can use it with pointers, as well:

::: {#cb38 .sourceCode}
``` {.sourceCode .c}
const int a = 10;        // Can't modify "a"

const int *p = &b        // Can't modify the thing "p" points to ("b")
int *const p = &b        // Can't modify "p"
const int *const p = &b  // Can't modify "p" or the thing it points to
```
:::

`restrict` on a pointer means that there will only be one pointer to the item in question, freeing the compiler to make some optimizations.

`volatile` indicates that the value in a variable might change at any time and should be loaded from memory instead of being kept in a register. Usually used with memory-mapped hardware.

`_Atomic` (or `atomic` if you include `<stdatomic.h>`) tells the compiler that reads or writes to this type should happen atomically. (This might be accomplished with a lock depending on the platform and type.)

### [2.9.3]{.header-section-number} Function Specifiers {#function-specifiers number="2.9.3"}

These are used on functions to provide additional guidance for the compiler.

`_Noreturn` indicates that a function will never return. It can only run forever or exit the program entirely. If you include `<stdnoreturn.h>`, you can use `noreturn` instead.

`inline` indicates that calls to this function should be as fast as possible. The intention here is that the code of the function be moved *inline* to remove the overhead of the call and return. The compiler regards `inline` as a suggestion, not a requirement.

### [2.9.4]{.header-section-number} Alignment Specifier {#alignment-specifier number="2.9.4"}

You can force the alignment of a variable with memory with `_Alignas`. If you include `<stdalign.h>` you can use `alignas` instead.

`alignas(0)` has no effect.

::: {#cb39 .sourceCode}
``` {.sourceCode .c}
alignas(16) int a = 12;    // 16-byte alignment
alignas(long) int b = 34;  // Same alignment as "long"
```
:::

## [2.10]{.header-section-number} `if` Statement {#if-statement number="2.10"}

::: {#cb40 .sourceCode}
``` {.sourceCode .c}
if (boolean_expression) code;

if (boolean_expression) {
    code;
    code;
    code;
}

if (boolean_expression) {
    code;
    code;
} else
    code;

if (boolean_expression) {
    code;
    code;
} else if {
    code;
    code;
    code;
} else {
    code;
}
```
:::

## [2.11]{.header-section-number} `for` Statement {#for-statement number="2.11"}

Classic `for`-loop.

The bit in parens comes in three parts separated by semicolons:

-   Initialization, executed once.
-   Block entry condition, evaluated every time before entering the loop body.
-   Post expression, evaluated every time after the loop body.

For example, initialize `i` to `0`, enter the loop body while `i < 10`, and then increment `i` after each loop iteration:

::: {#cb41 .sourceCode}
``` {.sourceCode .c}
for (i = 0; i < 10; i++) {
    code;
    code;
    code;
}
```
:::

You can declare loop-local variables by specifying their type:

::: {#cb42 .sourceCode}
``` {.sourceCode .c}
for (int i = 0; i < 10; i++) {
    code;
    code;
}
```
:::

You can separate parts of the expressions with the comma operator:

::: {#cb43 .sourceCode}
``` {.sourceCode .c}
for (i = 0, j = 5; i < 10; i++, j *= 3) {
    code;
    code;
}
```
:::

## [2.12]{.header-section-number} `while` Statement {#while-statement number="2.12"}

This loop won't enter if the Boolean expression is false. The continuation test happens before the loop.

::: {#cb44 .sourceCode}
``` {.sourceCode .c}
while (boolean_expression) code;

while (boolean_expression) {
    code;
    code;
}
```
:::

## [2.13]{.header-section-number} `do`-`while` Statement {#do-while-statement number="2.13"}

This loop will run at least once even if the Boolean expression is false. The continuation test doesn't happen until after the loop.

::: {#cb45 .sourceCode}
``` {.sourceCode .c}
do code while (boolean_expression);

do {
    code;
    code;
} while (boolean_expression);
```
:::

## [2.14]{.header-section-number} `switch` Statement {#switch-statement number="2.14"}

Performs actions based on the value of an expression. The cases that it is compared against must be constant values.

If the optional `default` is present, that code is executed if none of the cases match. Braces are not required around the cases.

::: {#cb46 .sourceCode}
``` {.sourceCode .c}
switch (expression) {
    case constant:
        code;
        code;
        break;

    case constant:
        code;
        code;
        break;

    default:
        code;
        break;
}
```
:::

The final `break` in the `switch` is unnecessary if there are no cases after it.

If the `break` isn't present, the `case` falls through to the next one. It's nice to put a comment to that effect so other devs don't hate you.

::: {#cb47 .sourceCode}
``` {.sourceCode .c}
switch (expression) {
    case constant:
        code;
        code;
        // fall through!

    case constant:
        code;
        break;
}
```
:::

## [2.15]{.header-section-number} `break` Statement {#break-statement number="2.15"}

This breaks out of a `switch` case, but it also can break out of any loop.

::: {#cb48 .sourceCode}
``` {.sourceCode .c}
while (boolean_expression) {
    code;

    if (boolean_expression)
        break;

    code;
}
```
:::

## [2.16]{.header-section-number} `continue` Statement {#continue-statement number="2.16"}

This can be used to short-circuit a loop and go to the next continuation condition test without completing the body of the loop.

::: {#cb49 .sourceCode}
``` {.sourceCode .c}
while (boolean_expression) {
    code;
    code;

    if (boolean_expression_2)
        continue;

    // If boolean_expression_2, code down here will be skipped:

    code;
    code;
}
```
:::

## [2.17]{.header-section-number} `goto` Statement {#goto-statement number="2.17"}

You can just jump anywhere within a function with `goto`. (You can't `goto` between functions, only within the same function as the `goto`.)

The destination of the `goto` is a *label*, which is an identifier followed by a colon (`:`). Labels are typically left-justified all the way to the margin to make them visually stand out.

::: {#cb50 .sourceCode}
``` {.sourceCode .c}
{
    // Abusive demo code that should be a while loop

    int i = 0;

loop:

    printf("%d\n", i++);

    if (i < 10)
        goto loop;
}
```
:::

## [2.18]{.header-section-number} `return` Statement {#return-statement number="2.18"}

This is how you get back from a function. You can `return` multiple times or just once.

If a function with `void` return type falls off the end, the `return` is implicit.

If the return type is not `void`, the `return` statement must specify a return value of the same type.

Parentheses around the return value are not necessary (as it's a statement, not a function).

::: {#cb51 .sourceCode}
``` {.sourceCode .c}
int increment(int a)
{
    return a + 1;
}
```
:::

## [2.19]{.header-section-number} `_Static_assert` Statement {#static_assert-statement number="2.19"}

This is a way to prevent *compilation* of a program if a certain constant condition is not met.

::: {#cb52 .sourceCode}
``` {.sourceCode .c}
_Static_assert(__STDC_VERSION__ >= 201112L, "You need at least C11!")
```
:::

## [2.20]{.header-section-number} Functions {#functions number="2.20"}

You need to specify the return type and parameter types for the function, and the body goes in a block afterward.

Variables in the function are local to that function.

::: {#cb53 .sourceCode}
``` {.sourceCode .c}
// Function that adds two numbers

int add(int x, int y)
{
    int sum = x + y;

    return sum;
}
```
:::

Functions that return nothing should be return type `void`. Functions that accept no parameters should have `void` as the parameter list.

::: {#cb54 .sourceCode}
``` {.sourceCode .c}
// All side effects, all the time!

void foo(void)
{
    some_global = 12;
    printf("Here we go!\n");
}
```
:::

### [2.20.1]{.header-section-number} `main()` Function {#main-function number="2.20.1"}

This is the function that runs when you first start the program. It will be one of these forms:

::: {#cb55 .sourceCode}
``` {.sourceCode .c}
int main(void)
int main(int argc, char *argv[])
```
:::

The first form ignores all command line parameters.

The second form stores the count of the command line parameters in `argc`, and stores the parameters themselves as an array of strings in `argv`. The first of these, `argv[0]`, is typically the name of the executable. The last `argv` pointer has the value `NULL`.

The return values usually show up as exit status codes in the OS. If there is no `return`, falling off the end of `main()` is an implied `return 0`[^12^](footnotes.html#fn12){#fnref12 .footnote-ref role="doc-noteref"}.

### [2.20.2]{.header-section-number} Variadic Functions {#variadic-functions number="2.20.2"}

Some functions can take a variable number of arguments. Every function must have at least one argument. The remaining arguments are specified by `...` and can be read with the `va_start()`, `va_arg()`, and `va_end()` macros.

Here's an example that adds up a variable number of integer values.

::: {#cb56 .sourceCode}
``` {.sourceCode .c}
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
```
:::

------------------------------------------------------------------------

::: {style="text-align:center"}
[Prev](foreword.html) \| [Contents](index.html) \| [Next](assert.html)
:::
