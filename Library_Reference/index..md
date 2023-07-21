---
tip: translate by openai@2023-07-20 18:26:03
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}

[[Prev]() \| ]{style="visibility: hidden"}[Contents](index.html) \| [Next](foreword.html)

> [[上一页]() | ]{style="visibility: hidden"}[目录](index.html) | [下一页](foreword.html)
:::

------------------------------------------------------------------------

::: {#title-block-header}
# Beej\'s Guide to C Programming {#beejs-guide-to-c-programming .title}

Library Reference

Brian "Beej Jorgensen" Hall

v0.9.9, Copyright © December 30, 2022
:::

-   [[1]{.toc-section-number} Foreword](foreword.html#foreword){#toc-foreword}
    -   [[1.1]{.toc-section-number} Audience](foreword.html#audience){#toc-audience}
    -   [[1.2]{.toc-section-number} How to Read This Book](foreword.html#how-to-read-this-book){#toc-how-to-read-this-book}
    -   [[1.3]{.toc-section-number} Platform and Compiler](foreword.html#platform-and-compiler){#toc-platform-and-compiler}
    -   [[1.4]{.toc-section-number} Official Homepage](foreword.html#official-homepage){#toc-official-homepage}
    -   [[1.5]{.toc-section-number} Email Policy](foreword.html#email-policy){#toc-email-policy}
    -   [[1.6]{.toc-section-number} Mirroring](foreword.html#mirroring){#toc-mirroring}
    -   [[1.7]{.toc-section-number} Note for Translators](foreword.html#note-for-translators){#toc-note-for-translators}
    -   [[1.8]{.toc-section-number} Copyright and Distribution](foreword.html#copyright-and-distribution){#toc-copyright-and-distribution}
    -   [[1.9]{.toc-section-number} Dedication](foreword.html#dedication){#toc-dedication}

-   [[2]{.toc-section-number} The C Language](the-c-language.html#the-c-language){#toc-the-c-language}

> [[2]{.toc-section-number} C 语言](the-c-language.html#the-c-language){#toc-the-c-language}
    -   [[2.1]{.toc-section-number} Background](the-c-language.html#background){#toc-background}
        -   [[2.1.1]{.toc-section-number} Comments](the-c-language.html#comments){#toc-comments}
        -   [[2.1.2]{.toc-section-number} Separators](the-c-language.html#separators){#toc-separators}
        -   [[2.1.3]{.toc-section-number} Expressions](the-c-language.html#expressions){#toc-expressions}
        -   [[2.1.4]{.toc-section-number} Statements](the-c-language.html#statements){#toc-statements}
        -   [[2.1.5]{.toc-section-number} Booleans](the-c-language.html#booleans){#toc-booleans}
        -   [[2.1.6]{.toc-section-number} Blocks](the-c-language.html#blocks){#toc-blocks}
        -   [[2.1.7]{.toc-section-number} Code Examples](the-c-language.html#code-examples){#toc-code-examples}
    -   [[2.2]{.toc-section-number} Operators](the-c-language.html#operators){#toc-operators}
        -   [[2.2.1]{.toc-section-number} Arithmetic Operators](the-c-language.html#arithmetic-operators){#toc-arithmetic-operators}
        -   [[2.2.2]{.toc-section-number} Pre- and Post-Increment and -Decrement](the-c-language.html#pre--and-post-increment-and--decrement){#toc-pre--and-post-increment-and--decrement}
        -   [[2.2.3]{.toc-section-number} Comparison Operators](the-c-language.html#comparison-operators){#toc-comparison-operators}
        -   [[2.2.4]{.toc-section-number} Pointer Operators](the-c-language.html#pointer-operators){#toc-pointer-operators}
        -   [[2.2.5]{.toc-section-number} Structure and Union Operators](the-c-language.html#structure-and-union-operators){#toc-structure-and-union-operators}
        -   [[2.2.6]{.toc-section-number} Array Operators](the-c-language.html#array-operators){#toc-array-operators}
        -   [[2.2.7]{.toc-section-number} Bitwise Operators](the-c-language.html#bitwise-operators){#toc-bitwise-operators}
        -   [[2.2.8]{.toc-section-number} Assignment Operators](the-c-language.html#assignment-operators){#toc-assignment-operators}
        -   [[2.2.9]{.toc-section-number} The `sizeof` Operator](the-c-language.html#the-sizeof-operator){#toc-the-sizeof-operator}
        -   [[2.2.10]{.toc-section-number} Type Casts](the-c-language.html#type-casts){#toc-type-casts}
        -   [[2.2.11]{.toc-section-number} `_Alignof` Operator](the-c-language.html#alignof-operator){#toc-alignof-operator}
        -   [[2.2.12]{.toc-section-number} Comma Operator](the-c-language.html#comma-operator){#toc-comma-operator}
    -   [[2.3]{.toc-section-number} Type Specifiers](the-c-language.html#type-specifiers){#toc-type-specifiers}
    -   [[2.4]{.toc-section-number} Constant Types](the-c-language.html#constant-types){#toc-constant-types}
    -   [[2.5]{.toc-section-number} Composite Types](the-c-language.html#composite-types){#toc-composite-types}
        -   [[2.5.1]{.toc-section-number} `struct` Types](the-c-language.html#struct-types){#toc-struct-types}
        -   [[2.5.2]{.toc-section-number} `union` Types](the-c-language.html#union-types){#toc-union-types}
        -   [[2.5.3]{.toc-section-number} `enum` Types](the-c-language.html#enum-types){#toc-enum-types}
    -   [[2.6]{.toc-section-number} Initializers](the-c-language.html#initializers){#toc-initializers}
    -   [[2.7]{.toc-section-number} Compound Literals](the-c-language.html#compound-literals){#toc-compound-literals}
    -   [[2.8]{.toc-section-number} Type Aliases](the-c-language.html#type-aliases){#toc-type-aliases}
    -   [[2.9]{.toc-section-number} Additional Type-Related Specifiers](the-c-language.html#additional-type-related-specifiers){#toc-additional-type-related-specifiers}
        -   [[2.9.1]{.toc-section-number} Storage Class Specifiers](the-c-language.html#storage-class-specifiers){#toc-storage-class-specifiers}
        -   [[2.9.2]{.toc-section-number} Type Qualifiers](the-c-language.html#type-qualifiers){#toc-type-qualifiers}
        -   [[2.9.3]{.toc-section-number} Function Specifiers](the-c-language.html#function-specifiers){#toc-function-specifiers}
        -   [[2.9.4]{.toc-section-number} Alignment Specifier](the-c-language.html#alignment-specifier){#toc-alignment-specifier}
    -   [[2.10]{.toc-section-number} `if` Statement](the-c-language.html#if-statement){#toc-if-statement}
    -   [[2.11]{.toc-section-number} `for` Statement](the-c-language.html#for-statement){#toc-for-statement}
    -   [[2.12]{.toc-section-number} `while` Statement](the-c-language.html#while-statement){#toc-while-statement}
    -   [[2.13]{.toc-section-number} `do`-`while` Statement](the-c-language.html#do-while-statement){#toc-do-while-statement}
    -   [[2.14]{.toc-section-number} `switch` Statement](the-c-language.html#switch-statement){#toc-switch-statement}
    -   [[2.15]{.toc-section-number} `break` Statement](the-c-language.html#break-statement){#toc-break-statement}
    -   [[2.16]{.toc-section-number} `continue` Statement](the-c-language.html#continue-statement){#toc-continue-statement}
    -   [[2.17]{.toc-section-number} `goto` Statement](the-c-language.html#goto-statement){#toc-goto-statement}
    -   [[2.18]{.toc-section-number} `return` Statement](the-c-language.html#return-statement){#toc-return-statement}
    -   [[2.19]{.toc-section-number} `_Static_assert` Statement](the-c-language.html#static_assert-statement){#toc-static_assert-statement}
    -   [[2.20]{.toc-section-number} Functions](the-c-language.html#functions){#toc-functions}
        -   [[2.20.1]{.toc-section-number} `main()` Function](the-c-language.html#main-function){#toc-main-function}
        -   [[2.20.2]{.toc-section-number} Variadic Functions](the-c-language.html#variadic-functions){#toc-variadic-functions}

-   [[3]{.toc-section-number} `<assert.h>` Runtime and Compile-time Diagnostics](assert.html#assert){#toc-assert}

> - [[3]{.toc-section-number} <assert.h> 运行时和编译时诊断](assert.html#assert){#toc-assert}
    -   [[3.1]{.toc-section-number} Macros](assert.html#macros){#toc-macros}
    -   [[3.2]{.toc-section-number} `assert()`](assert.html#man-assert){#toc-man-assert}
    -   [[3.3]{.toc-section-number} `static_assert()`](assert.html#man-static_assert){#toc-man-static_assert}

-   [[4]{.toc-section-number} `<complex.h>` Complex Number Functionality](complex.html#complex){#toc-complex}

> [[4]{.toc-section-number} `<complex.h>` 复数功能](complex.html#complex){#toc-complex}
    -   [[4.1]{.toc-section-number} `cacos()`, `cacosf()`, `cacosl()`](complex.html#man-cacos){#toc-man-cacos}
    -   [[4.2]{.toc-section-number} `casin()`, `casinf()`, `casinl()`](complex.html#man-casin){#toc-man-casin}
    -   [[4.3]{.toc-section-number} `catan()`, `catanf()`, `catanl()`](complex.html#man-catan){#toc-man-catan}
    -   [[4.4]{.toc-section-number} `ccos()`, `ccosf()`, `ccosl()`](complex.html#man-ccos){#toc-man-ccos}
    -   [[4.5]{.toc-section-number} `csin()`, `csinf()`, `csinl()`](complex.html#man-csin){#toc-man-csin}
    -   [[4.6]{.toc-section-number} `ctan()`, `ctanf()`, `ctanl()`](complex.html#man-ctan){#toc-man-ctan}
    -   [[4.7]{.toc-section-number} `cacosh()`, `cacoshf()`, `cacoshl()`](complex.html#man-cacosh){#toc-man-cacosh}
    -   [[4.8]{.toc-section-number} `casinh()`, `casinhf()`, `casinhl()`](complex.html#man-casinh){#toc-man-casinh}
    -   [[4.9]{.toc-section-number} `catanh()`, `catanhf()`, `catanhl()`](complex.html#man-catanh){#toc-man-catanh}
    -   [[4.10]{.toc-section-number} `ccosh()`, `ccoshf()`, `ccoshl()`](complex.html#man-ccosh){#toc-man-ccosh}
    -   [[4.11]{.toc-section-number} `csinh()`, `csinhf()`, `csinhl()`](complex.html#man-csinh){#toc-man-csinh}
    -   [[4.12]{.toc-section-number} `ctanh()`, `ctanhf()`, `ctanhl()`](complex.html#man-ctanh){#toc-man-ctanh}
    -   [[4.13]{.toc-section-number} `cexp()`, `cexpf()`, `cexpl()`](complex.html#man-cexp){#toc-man-cexp}
    -   [[4.14]{.toc-section-number} `clog()`, `clogf()`, `clogl()`](complex.html#man-clog){#toc-man-clog}
    -   [[4.15]{.toc-section-number} `cabs()`, `cabsf()`, `cabsl()`](complex.html#man-cabs){#toc-man-cabs}
    -   [[4.16]{.toc-section-number} `cpow()`, `cpowf()`, `cpowl()`](complex.html#man-cpow){#toc-man-cpow}
    -   [[4.17]{.toc-section-number} `csqrt()`, `csqrtf()`, `csqrtl()`](complex.html#man-csqrt){#toc-man-csqrt}
    -   [[4.18]{.toc-section-number} `carg()`, `cargf()`, `cargl()`](complex.html#man-carg){#toc-man-carg}
    -   [[4.19]{.toc-section-number} `cimag()`, `cimagf()`, `cimagl()`](complex.html#man-cimag){#toc-man-cimag}
    -   [[4.20]{.toc-section-number} `CMPLX()`, `CMPLXF()`, `CMPLXL()`](complex.html#man-CMPLX){#toc-man-CMPLX}
    -   [[4.21]{.toc-section-number} `conj()`, `conjf()`, `conjl()`](complex.html#man-conj){#toc-man-conj}
    -   [[4.22]{.toc-section-number} `cproj()`, `cproj()`, `cproj()`](complex.html#man-cproj){#toc-man-cproj}
    -   [[4.23]{.toc-section-number} `creal()`, `crealf()`, `creall()`](complex.html#man-creal){#toc-man-creal}

-   [[5]{.toc-section-number} `<ctype.h>` Character Classification and Conversion](ctype.html#ctype){#toc-ctype}

> [[5]{.toc-section-number} <ctype.h> 字符分类和转换](ctype.html#ctype){#toc-ctype}
    -   [[5.1]{.toc-section-number} `isalnum()`](ctype.html#man-isalnum){#toc-man-isalnum}
    -   [[5.2]{.toc-section-number} `isalpha()`](ctype.html#man-isalpha){#toc-man-isalpha}
    -   [[5.3]{.toc-section-number} `isblank()`](ctype.html#man-isblank){#toc-man-isblank}
    -   [[5.4]{.toc-section-number} `iscntrl()`](ctype.html#man-iscntrl){#toc-man-iscntrl}
    -   [[5.5]{.toc-section-number} `isdigit()`](ctype.html#man-isdigit){#toc-man-isdigit}
    -   [[5.6]{.toc-section-number} `isgraph()`](ctype.html#man-isgraph){#toc-man-isgraph}
    -   [[5.7]{.toc-section-number} `islower()`](ctype.html#man-islower){#toc-man-islower}
    -   [[5.8]{.toc-section-number} `isprint()`](ctype.html#man-isprint){#toc-man-isprint}
    -   [[5.9]{.toc-section-number} `ispunct()`](ctype.html#man-ispunct){#toc-man-ispunct}
    -   [[5.10]{.toc-section-number} `isspace()`](ctype.html#man-isspace){#toc-man-isspace}
    -   [[5.11]{.toc-section-number} `isupper()`](ctype.html#man-isupper){#toc-man-isupper}
    -   [[5.12]{.toc-section-number} `isxdigit()`](ctype.html#man-isxdigit){#toc-man-isxdigit}
    -   [[5.13]{.toc-section-number} `tolower()`](ctype.html#man-tolower){#toc-man-tolower}
    -   [[5.14]{.toc-section-number} `toupper()`](ctype.html#man-toupper){#toc-man-toupper}
-   [[6]{.toc-section-number} `<errno.h>` Error Information](errno.html#errno){#toc-errno}
    -   [[6.1]{.toc-section-number} `errno`](errno.html#man-errno){#toc-man-errno}

-   [[7]{.toc-section-number} `<fenv.h>` Floating Point Exceptions and Environment](fenv.html#fenv){#toc-fenv}

> [[7]{.toc-section-number} <fenv.h> 浮点异常和环境](fenv.html#fenv){#toc-fenv}
    -   [[7.1]{.toc-section-number} Types and Macros](fenv.html#types-and-macros){#toc-types-and-macros}
    -   [[7.2]{.toc-section-number} Pragmas](fenv.html#pragmas){#toc-pragmas}
    -   [[7.3]{.toc-section-number} `feclearexcept()`](fenv.html#man-feclearexcept){#toc-man-feclearexcept}
    -   [[7.4]{.toc-section-number} `fegetexceptflag()` `fesetexceptflag()`](fenv.html#man-fegetexceptflag){#toc-man-fegetexceptflag}
    -   [[7.5]{.toc-section-number} `feraiseexcept()`](fenv.html#man-feraiseexcept){#toc-man-feraiseexcept}
    -   [[7.6]{.toc-section-number} `fetestexcept()`](fenv.html#man-fetestexcept){#toc-man-fetestexcept}
    -   [[7.7]{.toc-section-number} `fegetround()` `fesetround()`](fenv.html#man-fegetround){#toc-man-fegetround}
    -   [[7.8]{.toc-section-number} `fegetenv()` `fesetenv()`](fenv.html#man-fegetenv){#toc-man-fegetenv}
    -   [[7.9]{.toc-section-number} `feholdexcept()`](fenv.html#man-feholdexcept){#toc-man-feholdexcept}
    -   [[7.10]{.toc-section-number} `feupdateenv()`](fenv.html#man-feupdateenv){#toc-man-feupdateenv}
-   [[8]{.toc-section-number} `<float.h>` Floating Point Limits](float.html#float){#toc-float}
    -   [[8.1]{.toc-section-number} Background](float.html#background-1){#toc-background-1}
    -   [[8.2]{.toc-section-number} `FLT_ROUNDS` Details](float.html#flt_rounds-details){#toc-flt_rounds-details}
    -   [[8.3]{.toc-section-number} `FLT_EVAL_METHOD` Details](float.html#flt_eval_method-details){#toc-flt_eval_method-details}
    -   [[8.4]{.toc-section-number} Subnormal Numbers](float.html#subnormal-numbers){#toc-subnormal-numbers}
    -   [[8.5]{.toc-section-number} How Many Decimal Places Can I Use?](float.html#how-many-decimal-places-can-i-use){#toc-how-many-decimal-places-can-i-use}
    -   [[8.6]{.toc-section-number} Comprehensive Example](float.html#comprehensive-example){#toc-comprehensive-example}

-   [[9]{.toc-section-number} `<inttypes.h>` More Integer Conversions](inttypes.html#inttypes){#toc-inttypes}

> [[9]{.toc-section-number} <inttypes.h> 更多整数转换](inttypes.html#inttypes){#toc-inttypes}
    -   [[9.1]{.toc-section-number} Macros](inttypes.html#macros-1){#toc-macros-1}
    -   [[9.2]{.toc-section-number} `imaxabs()`](inttypes.html#man-imaxabs){#toc-man-imaxabs}
    -   [[9.3]{.toc-section-number} `imaxdiv()`](inttypes.html#man-imaxdiv){#toc-man-imaxdiv}
    -   [[9.4]{.toc-section-number} `strtoimax()` `strtoumax()`](inttypes.html#man-strtoimax){#toc-man-strtoimax}
    -   [[9.5]{.toc-section-number} `wcstoimax()` `wcstoumax()`](inttypes.html#man-wcstoimax){#toc-man-wcstoimax}

-   [[10]{.toc-section-number} `<iso646.h>` Alternative Operator Spellings](iso646.html#iso646){#toc-iso646}

> - [[10]{.toc-section-number} <iso646.h> 替代运算符拼写](iso646.html#iso646){#toc-iso646}
-   [[11]{.toc-section-number} `<limits.h>` Numeric Limits](limits.html#limits){#toc-limits}
    -   [[11.1]{.toc-section-number} `CHAR_MIN` and `CHAR_MAX`](limits.html#char_min-and-char_max){#toc-char_min-and-char_max}
    -   [[11.2]{.toc-section-number} Choosing the Correct Type](limits.html#choosing-the-correct-type){#toc-choosing-the-correct-type}
    -   [[11.3]{.toc-section-number} Whither Two's Complement?](limits.html#whither-twos-complement){#toc-whither-twos-complement}
    -   [[11.4]{.toc-section-number} Demo Program](limits.html#demo-program){#toc-demo-program}
-   [[12]{.toc-section-number} `<locale.h>` locale handling](locale.html#locale){#toc-locale}
    -   [[12.1]{.toc-section-number} `setlocale()`](locale.html#man-setlocale){#toc-man-setlocale}
    -   [[12.2]{.toc-section-number} `localeconv()`](locale.html#man-localeconv){#toc-man-localeconv}
-   [[13]{.toc-section-number} `<math.h>` Mathematics](math.html#math){#toc-math}
    -   [[13.1]{.toc-section-number} Math Function Idioms](math.html#func-idioms){#toc-func-idioms}
    -   [[13.2]{.toc-section-number} Math Types](math.html#math-types){#toc-math-types}
    -   [[13.3]{.toc-section-number} Math Macros](math.html#math-macros){#toc-math-macros}
    -   [[13.4]{.toc-section-number} Math Errors](math.html#math-errors){#toc-math-errors}
    -   [[13.5]{.toc-section-number} Math Pragmas](math.html#math-pragmas){#toc-math-pragmas}
    -   [[13.6]{.toc-section-number} `fpclassify()`](math.html#man-fpclassify){#toc-man-fpclassify}
    -   [[13.7]{.toc-section-number} `isfinite()`, `isinf()`, `isnan()`, `isnormal()`](math.html#man-isnan){#toc-man-isnan}
    -   [[13.8]{.toc-section-number} `signbit()`](math.html#man-signbit){#toc-man-signbit}
    -   [[13.9]{.toc-section-number} `acos()`, `acosf()`, `acosl()`](math.html#man-acos){#toc-man-acos}
    -   [[13.10]{.toc-section-number} `asin()`, `asinf()`, `asinl()`](math.html#man-asin){#toc-man-asin}
    -   [[13.11]{.toc-section-number} `atan()`, `atanf()`, `atanl()`, `atan2()`, `atan2f()`, `atan2l()`](math.html#man-atan){#toc-man-atan}
    -   [[13.12]{.toc-section-number} `cos()`, `cosf()`, `cosl()`](math.html#man-cos){#toc-man-cos}
    -   [[13.13]{.toc-section-number} `sin()`, `sinf()`, `sinl()`](math.html#man-sin){#toc-man-sin}
    -   [[13.14]{.toc-section-number} `tan()`, `tanf()`, `tanl()`](math.html#man-tan){#toc-man-tan}
    -   [[13.15]{.toc-section-number} `acosh()`, `acoshf()`, `acoshl()`](math.html#man-acosh){#toc-man-acosh}
    -   [[13.16]{.toc-section-number} `asinh()`, `asinhf()`, `asinhl()`](math.html#man-asinh){#toc-man-asinh}
    -   [[13.17]{.toc-section-number} `atanh()`, `atanhf()`, `atanhl()`](math.html#man-atanh){#toc-man-atanh}
    -   [[13.18]{.toc-section-number} `cosh()`, `coshf()`, `coshl()`](math.html#man-cosh){#toc-man-cosh}
    -   [[13.19]{.toc-section-number} `sinh()`, `sinhf()`, `sinhl()`](math.html#man-sinh){#toc-man-sinh}
    -   [[13.20]{.toc-section-number} `tanh()`, `tanhf()`, `tanhl()`](math.html#man-tanh){#toc-man-tanh}
    -   [[13.21]{.toc-section-number} `exp()`, `expf()`, `expl()`](math.html#man-exp){#toc-man-exp}
    -   [[13.22]{.toc-section-number} `exp2()`, `exp2f()`, `exp2l()`](math.html#man-exp2){#toc-man-exp2}
    -   [[13.23]{.toc-section-number} `expm1()`, `expm1f()`, `expm1l()`](math.html#man-expm1){#toc-man-expm1}
    -   [[13.24]{.toc-section-number} `frexp()`, `frexpf()`, `frexpl()`](math.html#man-frexp){#toc-man-frexp}
    -   [[13.25]{.toc-section-number} `ilogb()`, `ilogbf()`, `ilogbl()`](math.html#man-ilogb){#toc-man-ilogb}
    -   [[13.26]{.toc-section-number} `ldexp()`, `ldexpf()`, `ldexpl()`](math.html#man-ldexp){#toc-man-ldexp}
    -   [[13.27]{.toc-section-number} `log()`, `logf()`, `logl()`](math.html#man-log){#toc-man-log}
    -   [[13.28]{.toc-section-number} `log10()`, `log10f()`, `log10l()`](math.html#man-log10){#toc-man-log10}
    -   [[13.29]{.toc-section-number} `log1p()`, `log1pf()`, `log1pl()`](math.html#man-log1p){#toc-man-log1p}
    -   [[13.30]{.toc-section-number} `log2()`, `log2f()`, `log2l()`](math.html#man-log2){#toc-man-log2}
    -   [[13.31]{.toc-section-number} `logb()`, `logbf()`, `logbl()`](math.html#man-logb){#toc-man-logb}
    -   [[13.32]{.toc-section-number} `modf()`, `modff()`, `modfl()`](math.html#man-modf){#toc-man-modf}
    -   [[13.33]{.toc-section-number} `scalbn()`, `scalbnf()`, `scalbnl()` `scalbln()`, `scalblnf()`, `scalblnl()`](math.html#man-scalb){#toc-man-scalb}
    -   [[13.34]{.toc-section-number} `cbrt()`, `cbrtf()`, `cbrtl()`](math.html#man-cbrt){#toc-man-cbrt}
    -   [[13.35]{.toc-section-number} `fabs()`, `fabsf()`, `fabsl()`](math.html#man-fabs){#toc-man-fabs}
    -   [[13.36]{.toc-section-number} `hypot()`, `hypotf()`, `hypotl()`](math.html#man-hypot){#toc-man-hypot}
    -   [[13.37]{.toc-section-number} `pow()`, `powf()`, `powl()`](math.html#man-pow){#toc-man-pow}
    -   [[13.38]{.toc-section-number} `sqrt()`](math.html#man-sqrt){#toc-man-sqrt}
    -   [[13.39]{.toc-section-number} `erf()`, `erff()`, `erfl()`](math.html#man-erf){#toc-man-erf}
    -   [[13.40]{.toc-section-number} `erfc()`, `erfcf()`, `erfcl()`](math.html#man-erfc){#toc-man-erfc}
    -   [[13.41]{.toc-section-number} `lgamma()`, `lgammaf()`, `lgammal()`](math.html#man-lgamma){#toc-man-lgamma}
    -   [[13.42]{.toc-section-number} `tgamma()`, `tgammaf()`, `tgammal()`](math.html#man-tgamma){#toc-man-tgamma}
    -   [[13.43]{.toc-section-number} `ceil()`, `ceilf()`, `ceill()`](math.html#man-ceil){#toc-man-ceil}
    -   [[13.44]{.toc-section-number} `floor()`, `floorf()`, `floorl()`](math.html#man-floor){#toc-man-floor}
    -   [[13.45]{.toc-section-number} `nearbyint()`, `nearbyintf()`, `nearbyintl()`](math.html#man-nearbyint){#toc-man-nearbyint}
    -   [[13.46]{.toc-section-number} `rint()`, `rintf()`, `rintl()`](math.html#man-rint){#toc-man-rint}
    -   [[13.47]{.toc-section-number} `lrint()`, `lrintf()`, `lrintl()`, `llrint()`, `llrintf()`, `llrintl()`](math.html#man-lrint){#toc-man-lrint}
    -   [[13.48]{.toc-section-number} `round()`, `roundf()`, `roundl()`](math.html#man-round){#toc-man-round}
    -   [[13.49]{.toc-section-number} `lround()`, `lroundf()`, `lroundl()` `llround()`, `llroundf()`, `llroundl()`](math.html#man-lround){#toc-man-lround}
    -   [[13.50]{.toc-section-number} `trunc()`, `truncf()`, `truncl()`](math.html#man-trunc){#toc-man-trunc}
    -   [[13.51]{.toc-section-number} `fmod()`, `fmodf()`, `fmodl()`](math.html#man-fmod){#toc-man-fmod}
    -   [[13.52]{.toc-section-number} `remainder()`, `remainderf()`, `remainderl()`](math.html#man-remainder){#toc-man-remainder}
    -   [[13.53]{.toc-section-number} `remquo()`, `remquof()`, `remquol()`](math.html#man-remquo){#toc-man-remquo}
    -   [[13.54]{.toc-section-number} `copysign()`, `copysignf()`, `copysignl()`](math.html#man-copysign){#toc-man-copysign}
    -   [[13.55]{.toc-section-number} `nan()`, `nanf()`, `nanl()`](math.html#man-nan){#toc-man-nan}
    -   [[13.56]{.toc-section-number} `nextafter()`, `nextafterf()`, `nextafterl()`](math.html#man-nextafter){#toc-man-nextafter}
    -   [[13.57]{.toc-section-number} `nexttoward()`, `nexttowardf()`, `nexttowardl()`](math.html#man-nexttoward){#toc-man-nexttoward}
    -   [[13.58]{.toc-section-number} `fdim()`, `fdimf()`, `fdiml()`](math.html#man-fdim){#toc-man-fdim}
    -   [[13.59]{.toc-section-number} `fmax()`, `fmaxf()`, `fmaxl()`, `fmin()`, `fminf()`, `fminl()`](math.html#man-fmax){#toc-man-fmax}
    -   [[13.60]{.toc-section-number} `fma()`, `fmaf()`, `fmal()`](math.html#man-fma){#toc-man-fma}
    -   [[13.61]{.toc-section-number} `isgreater()`, `isgreaterequal()`, `isless()`, `islessequal()`](math.html#man-isgreater){#toc-man-isgreater}
    -   [[13.62]{.toc-section-number} `islessgreater()`](math.html#man-islessgreater){#toc-man-islessgreater}
    -   [[13.63]{.toc-section-number} `isunordered()`](math.html#man-isunordered){#toc-man-isunordered}
-   [[14]{.toc-section-number} `<setjmp.h>` Non-local Goto](setjmp.html#setjmp){#toc-setjmp}
    -   [[14.1]{.toc-section-number} `setjmp()`](setjmp.html#man-setjmp){#toc-man-setjmp}
    -   [[14.2]{.toc-section-number} `longjmp()`](setjmp.html#man-longjmp){#toc-man-longjmp}
-   [[15]{.toc-section-number} `<signal.h>` signal handling](signal.html#signal){#toc-signal}
    -   [[15.1]{.toc-section-number} `signal()`](signal.html#man-signal){#toc-man-signal}
    -   [[15.2]{.toc-section-number} `raise()`](signal.html#man-raise){#toc-man-raise}

-   [[16]{.toc-section-number} `<stdalign.h>` Macros for Alignment](stdalign.html#stdalign){#toc-stdalign}

> [[16]{.toc-section-number} `<stdalign.h>` 宏用于对齐](stdalign.html#stdalign){#toc-stdalign}
    -   [[16.1]{.toc-section-number} `alignas()` `_Alignas()`](stdalign.html#man-alignas){#toc-man-alignas}
    -   [[16.2]{.toc-section-number} `alignof()` `_Alignof()`](stdalign.html#man-alignof){#toc-man-alignof}
-   [[17]{.toc-section-number} `<stdarg.h>` Variable Arguments](stdarg.html#stdarg){#toc-stdarg}
    -   [[17.1]{.toc-section-number} `va_arg()`](stdarg.html#man-va_arg){#toc-man-va_arg}
    -   [[17.2]{.toc-section-number} `va_copy()`](stdarg.html#man-va_copy){#toc-man-va_copy}
    -   [[17.3]{.toc-section-number} `va_end()`](stdarg.html#man-va_end){#toc-man-va_end}
    -   [[17.4]{.toc-section-number} `va_start()`](stdarg.html#man-va_start){#toc-man-va_start}

-   [[18]{.toc-section-number} `<stdatomic.h>` Atomic-Related Functions](stdatomic.html#stdatomic){#toc-stdatomic}

> [[18]{.toc-section-number} `<stdatomic.h>` 原子相关函数](stdatomic.html#stdatomic){#toc-stdatomic}
    -   [[18.1]{.toc-section-number} Atomic Types](stdatomic.html#atomic-types){#toc-atomic-types}
    -   [[18.2]{.toc-section-number} Lock-free Macros](stdatomic.html#lock-free-macros){#toc-lock-free-macros}
    -   [[18.3]{.toc-section-number} Atomic Flag](stdatomic.html#atomic-flag){#toc-atomic-flag}
    -   [[18.4]{.toc-section-number} Memory Order](stdatomic.html#memory-order){#toc-memory-order}
    -   [[18.5]{.toc-section-number} `ATOMIC_VAR_INIT()`](stdatomic.html#man-ATOMIC_VAR_INIT){#toc-man-ATOMIC_VAR_INIT}
    -   [[18.6]{.toc-section-number} `atomic_init()`](stdatomic.html#man-atomic_init){#toc-man-atomic_init}
    -   [[18.7]{.toc-section-number} `kill_dependency()`](stdatomic.html#man-kill_dependency){#toc-man-kill_dependency}
    -   [[18.8]{.toc-section-number} `atomic_thread_fence()`](stdatomic.html#man-atomic_thread_fence){#toc-man-atomic_thread_fence}
    -   [[18.9]{.toc-section-number} `atomic_signal_fence()`](stdatomic.html#man-atomic_signal_fence){#toc-man-atomic_signal_fence}
    -   [[18.10]{.toc-section-number} `atomic_is_lock_free()`](stdatomic.html#man-atomic_is_lock_free){#toc-man-atomic_is_lock_free}
    -   [[18.11]{.toc-section-number} `atomic_store()`](stdatomic.html#man-atomic_store){#toc-man-atomic_store}
    -   [[18.12]{.toc-section-number} `atomic_load()`](stdatomic.html#man-atomic_load){#toc-man-atomic_load}
    -   [[18.13]{.toc-section-number} `atomic_exchange()`](stdatomic.html#man-atomic_exchange){#toc-man-atomic_exchange}
    -   [[18.14]{.toc-section-number} `atomic_compare_exchange_*()`](stdatomic.html#man-atomic_compare_exchange){#toc-man-atomic_compare_exchange}
    -   [[18.15]{.toc-section-number} `atomic_fetch_*()`](stdatomic.html#man-atomic_fetch){#toc-man-atomic_fetch}
    -   [[18.16]{.toc-section-number} `atomic_flag_test_and_set()`](stdatomic.html#man-atomic_flag_test_and_set){#toc-man-atomic_flag_test_and_set}
    -   [[18.17]{.toc-section-number} `atomic_flag_clear()`](stdatomic.html#man-atomic_flag_clear){#toc-man-atomic_flag_clear}
-   [[19]{.toc-section-number} `<stdbool.h>` Boolean Types](stdbool.html#stdbool){#toc-stdbool}
    -   [[19.1]{.toc-section-number} Example](stdbool.html#example-135){#toc-example-135}
    -   [[19.2]{.toc-section-number} `_Bool`?](stdbool.html#bool){#toc-bool}

-   [[20]{.toc-section-number} `<stddef.h>` A Few Standard Definitions](stddef.html#stddef){#toc-stddef}

> [[20]{.toc-section-number} <stddef.h> 一些标准定义](stddef.html#stddef){#toc-stddef}
    -   [[20.1]{.toc-section-number} `ptrdiff_t`](stddef.html#man-ptrdiff_t){#toc-man-ptrdiff_t}
    -   [[20.2]{.toc-section-number} `size_t`](stddef.html#man-size_t){#toc-man-size_t}
    -   [[20.3]{.toc-section-number} `max_align_t`](stddef.html#man-max_align_t){#toc-man-max_align_t}
    -   [[20.4]{.toc-section-number} `wchar_t`](stddef.html#man-wchar_t){#toc-man-wchar_t}
    -   [[20.5]{.toc-section-number} `offsetof`](stddef.html#man-offsetof){#toc-man-offsetof}
-   [[21]{.toc-section-number} `<stdint.h>` More Integer Types](stdint.html#stdint){#toc-stdint}
    -   [[21.1]{.toc-section-number} Specific-Width Integers](stdint.html#specific-width-integers){#toc-specific-width-integers}
    -   [[21.2]{.toc-section-number} Other Integer Types](stdint.html#other-integer-types){#toc-other-integer-types}
    -   [[21.3]{.toc-section-number} Macros](stdint.html#macros-2){#toc-macros-2}
    -   [[21.4]{.toc-section-number} Other Limits](stdint.html#other-limits){#toc-other-limits}
    -   [[21.5]{.toc-section-number} Macros for Declaring Constants](stdint.html#macros-for-declaring-constants){#toc-macros-for-declaring-constants}
-   [[22]{.toc-section-number} `<stdio.h>` Standard I/O Library](stdio.html#stdio){#toc-stdio}
    -   [[22.1]{.toc-section-number} `remove()`](stdio.html#man-remove){#toc-man-remove}
    -   [[22.2]{.toc-section-number} `rename()`](stdio.html#man-rename){#toc-man-rename}
    -   [[22.3]{.toc-section-number} `tmpfile()`](stdio.html#man-tmpfile){#toc-man-tmpfile}
    -   [[22.4]{.toc-section-number} `tmpnam()`](stdio.html#man-tmpnam){#toc-man-tmpnam}
    -   [[22.5]{.toc-section-number} `fclose()`](stdio.html#man-fclose){#toc-man-fclose}
    -   [[22.6]{.toc-section-number} `fflush()`](stdio.html#man-fflush){#toc-man-fflush}
    -   [[22.7]{.toc-section-number} `fopen()`](stdio.html#man-fopen){#toc-man-fopen}
    -   [[22.8]{.toc-section-number} `freopen()`](stdio.html#man-freopen){#toc-man-freopen}
    -   [[22.9]{.toc-section-number} `setbuf()`, `setvbuf()`](stdio.html#man-setbuf){#toc-man-setbuf}
    -   [[22.10]{.toc-section-number} `printf()`, `fprintf()`, `sprintf()`, `snprintf()`](stdio.html#man-printf){#toc-man-printf}
    -   [[22.11]{.toc-section-number} `scanf()`, `fscanf()`, `sscanf()`](stdio.html#man-scanf){#toc-man-scanf}
    -   [[22.12]{.toc-section-number} `vprintf()`, `vfprintf()`, `vsprintf()`, `vsnprintf()`](stdio.html#man-vprintf){#toc-man-vprintf}
    -   [[22.13]{.toc-section-number} `vscanf()`, `vfscanf()`, `vsscanf()`](stdio.html#man-vscanf){#toc-man-vscanf}
    -   [[22.14]{.toc-section-number} `getc()`, `fgetc()`, `getchar()`](stdio.html#man-getc){#toc-man-getc}
    -   [[22.15]{.toc-section-number} `gets()`, `fgets()`](stdio.html#man-gets){#toc-man-gets}
    -   [[22.16]{.toc-section-number} `putc()`, `fputc()`, `putchar()`](stdio.html#man-putc){#toc-man-putc}
    -   [[22.17]{.toc-section-number} `puts()`, `fputs()`](stdio.html#man-puts){#toc-man-puts}
    -   [[22.18]{.toc-section-number} `ungetc()`](stdio.html#man-ungetc){#toc-man-ungetc}
    -   [[22.19]{.toc-section-number} `fread()`](stdio.html#man-fread){#toc-man-fread}
    -   [[22.20]{.toc-section-number} `fwrite()`](stdio.html#man-fwrite){#toc-man-fwrite}
    -   [[22.21]{.toc-section-number} `fgetpos()`, `fsetpos()`](stdio.html#man-fgetpos){#toc-man-fgetpos}
    -   [[22.22]{.toc-section-number} `fseek()`, `rewind()`](stdio.html#man-fseek){#toc-man-fseek}
    -   [[22.23]{.toc-section-number} `ftell()`](stdio.html#man-ftell){#toc-man-ftell}
    -   [[22.24]{.toc-section-number} `feof()`, `ferror()`, `clearerr()`](stdio.html#man-feof){#toc-man-feof}
    -   [[22.25]{.toc-section-number} `perror()`](stdio.html#man-perror){#toc-man-perror}

-   [[23]{.toc-section-number} `<stdlib.h>` Standard Library Functions](stdlib.html#stdlib){#toc-stdlib}

> - [[23]{.toc-section-number} <stdlib.h> 标准库函数](stdlib.html#stdlib){#toc-stdlib}
    -   [[23.1]{.toc-section-number} `<stdlib.h>` Types and Macros](stdlib.html#stdlib.h-types-and-macros){#toc-stdlib.h-types-and-macros}
    -   [[23.2]{.toc-section-number} `atof()`](stdlib.html#man-atof){#toc-man-atof}
    -   [[23.3]{.toc-section-number} `atoi()`, `atol()`, `atoll()`](stdlib.html#man-atoi){#toc-man-atoi}
    -   [[23.4]{.toc-section-number} `strtod()`, `strtof()`, `strtold()`](stdlib.html#man-strtod){#toc-man-strtod}
    -   [[23.5]{.toc-section-number} `strtol()`, `strtoll()`, `strtoul()`, `strtoull()`](stdlib.html#man-strtol){#toc-man-strtol}
    -   [[23.6]{.toc-section-number} `rand()`](stdlib.html#man-rand){#toc-man-rand}
    -   [[23.7]{.toc-section-number} `srand()`](stdlib.html#man-srand){#toc-man-srand}
    -   [[23.8]{.toc-section-number} `aligned_alloc()`](stdlib.html#man-aligned_alloc){#toc-man-aligned_alloc}
    -   [[23.9]{.toc-section-number} `calloc()`, `malloc()`](stdlib.html#man-malloc){#toc-man-malloc}
    -   [[23.10]{.toc-section-number} `free()`](stdlib.html#man-free){#toc-man-free}
    -   [[23.11]{.toc-section-number} `realloc()`](stdlib.html#man-realloc){#toc-man-realloc}
    -   [[23.12]{.toc-section-number} `abort()`](stdlib.html#man-abort){#toc-man-abort}
    -   [[23.13]{.toc-section-number} `atexit()`, `at_quick_exit()`](stdlib.html#man-atexit){#toc-man-atexit}
    -   [[23.14]{.toc-section-number} `exit()`, `quick_exit()`, `_Exit()`](stdlib.html#man-exit){#toc-man-exit}
    -   [[23.15]{.toc-section-number} `getenv()`](stdlib.html#man-getenv){#toc-man-getenv}
    -   [[23.16]{.toc-section-number} `system()`](stdlib.html#man-system){#toc-man-system}
    -   [[23.17]{.toc-section-number} `bsearch()`](stdlib.html#man-bsearch){#toc-man-bsearch}
    -   [[23.18]{.toc-section-number} `qsort()`](stdlib.html#man-qsort){#toc-man-qsort}
    -   [[23.19]{.toc-section-number} `abs()`, `labs()`, `llabs()`](stdlib.html#man-abs){#toc-man-abs}
    -   [[23.20]{.toc-section-number} `div()`, `ldiv()`, `lldiv()`](stdlib.html#man-div){#toc-man-div}
    -   [[23.21]{.toc-section-number} `mblen()`](stdlib.html#man-mblen){#toc-man-mblen}
    -   [[23.22]{.toc-section-number} `mbtowc()`](stdlib.html#man-mbtowc){#toc-man-mbtowc}
    -   [[23.23]{.toc-section-number} `wctomb()`](stdlib.html#man-wctomb){#toc-man-wctomb}
    -   [[23.24]{.toc-section-number} `mbstowcs()`](stdlib.html#man-mbstowcs){#toc-man-mbstowcs}
    -   [[23.25]{.toc-section-number} `wcstombs()`](stdlib.html#man-wcstombs){#toc-man-wcstombs}

-   [[24]{.toc-section-number} `<stdnoreturn.h>` Macros for Non-Returning Functions](stdnoreturn.html#stdnoreturn){#toc-stdnoreturn}

> [[24]{.toc-section-number}  <stdnoreturn.h> 宏：非返回函数](stdnoreturn.html#stdnoreturn){#toc-stdnoreturn}

-   [[25]{.toc-section-number} `<string.h>` String Manipulation](stringref.html#stringref){#toc-stringref}

> [[25]{.toc-section-number} <string.h> 字符串操作](stringref.html#stringref){#toc-stringref}
    -   [[25.1]{.toc-section-number} `memcpy()`, `memmove()`](stringref.html#man-memcpy){#toc-man-memcpy}
    -   [[25.2]{.toc-section-number} `strcpy()`, `strncpy()`](stringref.html#man-strcpy){#toc-man-strcpy}
    -   [[25.3]{.toc-section-number} `strcat()`, `strncat()`](stringref.html#man-strcat){#toc-man-strcat}
    -   [[25.4]{.toc-section-number} `strcmp()`, `strncmp()`, `memcmp()`](stringref.html#man-strcmp){#toc-man-strcmp}
    -   [[25.5]{.toc-section-number} `strcoll()`](stringref.html#man-strcoll){#toc-man-strcoll}
    -   [[25.6]{.toc-section-number} `strxfrm()`](stringref.html#man-strxfrm){#toc-man-strxfrm}
    -   [[25.7]{.toc-section-number} `strchr()`, `strrchr()`, `memchr()`](stringref.html#man-strchr){#toc-man-strchr}
    -   [[25.8]{.toc-section-number} `strspn()`, `strcspn()`](stringref.html#man-strspn){#toc-man-strspn}
    -   [[25.9]{.toc-section-number} `strpbrk()`](stringref.html#man-strpbrk){#toc-man-strpbrk}
    -   [[25.10]{.toc-section-number} `strstr()`](stringref.html#man-strstr){#toc-man-strstr}
    -   [[25.11]{.toc-section-number} `strtok()`](stringref.html#man-strtok){#toc-man-strtok}
    -   [[25.12]{.toc-section-number} `memset()`](stringref.html#man-memset){#toc-man-memset}
    -   [[25.13]{.toc-section-number} `strerror()`](stringref.html#man-strerror){#toc-man-strerror}
    -   [[25.14]{.toc-section-number} `strlen()`](stringref.html#man-strlen){#toc-man-strlen}

-   [[26]{.toc-section-number} `<tgmath.h>` Type-Generic Math Functions](tgmath.html#tgmath){#toc-tgmath}

> [[26]{.toc-section-number} <tgmath.h> 类型通用数学函数（tgmath.html#tgmath）{#toc-tgmath}
    -   [[26.1]{.toc-section-number} Example](tgmath.html#example-199){#toc-example-199}

-   [[27]{.toc-section-number} `<threads.h>` Multithreading Functions](threads.html#threads){#toc-threads}

> [[27]{.toc-section-number} <threads.h> 多线程函数](threads.html#threads){#toc-threads}
    -   [[27.1]{.toc-section-number} `call_once()`](threads.html#man-call_once){#toc-man-call_once}
    -   [[27.2]{.toc-section-number} `cnd_broadcast()`](threads.html#man-cnd_broadcast){#toc-man-cnd_broadcast}
    -   [[27.3]{.toc-section-number} `cnd_destroy()`](threads.html#man-cnd_destroy){#toc-man-cnd_destroy}
    -   [[27.4]{.toc-section-number} `cnd_init()`](threads.html#man-cnd_init){#toc-man-cnd_init}
    -   [[27.5]{.toc-section-number} `cnd_signal()`](threads.html#man-cnd_signal){#toc-man-cnd_signal}
    -   [[27.6]{.toc-section-number} `cnd_timedwait()`](threads.html#man-cnd_timedwait){#toc-man-cnd_timedwait}
    -   [[27.7]{.toc-section-number} `cnd_wait()`](threads.html#man-cnd_wait){#toc-man-cnd_wait}
    -   [[27.8]{.toc-section-number} `mtx_destroy()`](threads.html#man-mtx_destroy){#toc-man-mtx_destroy}
    -   [[27.9]{.toc-section-number} `mtx_init()`](threads.html#man-mtx_init){#toc-man-mtx_init}
    -   [[27.10]{.toc-section-number} `mtx_lock()`](threads.html#man-mtx_lock){#toc-man-mtx_lock}
    -   [[27.11]{.toc-section-number} `mtx_timedlock()`](threads.html#man-mtx_timedlock){#toc-man-mtx_timedlock}
    -   [[27.12]{.toc-section-number} `mtx_trylock()`](threads.html#man-mtx_trylock){#toc-man-mtx_trylock}
    -   [[27.13]{.toc-section-number} `mtx_unlock()`](threads.html#man-mtx_unlock){#toc-man-mtx_unlock}
    -   [[27.14]{.toc-section-number} `thrd_create()`](threads.html#man-thrd_create){#toc-man-thrd_create}
    -   [[27.15]{.toc-section-number} `thrd_current()`](threads.html#man-thrd_current){#toc-man-thrd_current}
    -   [[27.16]{.toc-section-number} `thrd_detach()`](threads.html#man-thrd_detach){#toc-man-thrd_detach}
    -   [[27.17]{.toc-section-number} `thrd_equal()`](threads.html#man-thrd_equal){#toc-man-thrd_equal}
    -   [[27.18]{.toc-section-number} `thrd_exit()`](threads.html#man-thrd_exit){#toc-man-thrd_exit}
    -   [[27.19]{.toc-section-number} `thrd_join()`](threads.html#man-thrd_join){#toc-man-thrd_join}
    -   [[27.20]{.toc-section-number} `thrd_sleep()`](threads.html#man-thrd_sleep){#toc-man-thrd_sleep}
    -   [[27.21]{.toc-section-number} `thrd_yield()`](threads.html#man-thrd_yield){#toc-man-thrd_yield}
    -   [[27.22]{.toc-section-number} `tss_create()`](threads.html#man-tss_create){#toc-man-tss_create}
    -   [[27.23]{.toc-section-number} `tss_delete()`](threads.html#man-tss_delete){#toc-man-tss_delete}
    -   [[27.24]{.toc-section-number} `tss_get()`](threads.html#man-tss_get){#toc-man-tss_get}
    -   [[27.25]{.toc-section-number} `tss_set()`](threads.html#man-tss_set){#toc-man-tss_set}
-   [[28]{.toc-section-number} `<time.h>` Date and Time Functions](time.html#time){#toc-time}
    -   [[28.1]{.toc-section-number} Thread Safety Warning](time.html#thread-safety-warning){#toc-thread-safety-warning}
    -   [[28.2]{.toc-section-number} `clock()`](time.html#man-clock){#toc-man-clock}
    -   [[28.3]{.toc-section-number} `difftime()`](time.html#man-difftime){#toc-man-difftime}
    -   [[28.4]{.toc-section-number} `mktime()`](time.html#man-mktime){#toc-man-mktime}
    -   [[28.5]{.toc-section-number} `time()`](time.html#man-time){#toc-man-time}
    -   [[28.6]{.toc-section-number} `timespec_get()`](time.html#man-timespec_get){#toc-man-timespec_get}
    -   [[28.7]{.toc-section-number} `asctime()`](time.html#man-asctime){#toc-man-asctime}
    -   [[28.8]{.toc-section-number} `ctime()`](time.html#man-ctime){#toc-man-ctime}
    -   [[28.9]{.toc-section-number} `gmtime()`](time.html#man-gmtime){#toc-man-gmtime}
    -   [[28.10]{.toc-section-number} `localtime()`](time.html#man-localtime){#toc-man-localtime}
    -   [[28.11]{.toc-section-number} `strftime()`](time.html#man-strftime){#toc-man-strftime}

-   [[29]{.toc-section-number} `<uchar.h>` Unicode utility functions](uchar.html#uchar){#toc-uchar}

> [[29]{.toc-section-number} <uchar.h> Unicode 实用函数](uchar.html#uchar){#toc-uchar}
    -   [[29.1]{.toc-section-number} Types](uchar.html#types){#toc-types}
    -   [[29.2]{.toc-section-number} OS X issue](uchar.html#os-x-issue){#toc-os-x-issue}
    -   [[29.3]{.toc-section-number} `mbrtoc16()` `mbrtoc32()`](uchar.html#man-mbrtoc16){#toc-man-mbrtoc16}
    -   [[29.4]{.toc-section-number} `c16rtomb()` `c32rtomb()`](uchar.html#man-c16rtomb){#toc-man-c16rtomb}
-   [[30]{.toc-section-number} `<wchar.h>` Wide Character Handling](wchar.html#wchar){#toc-wchar}
    -   [[30.1]{.toc-section-number} Restartable Functions](wchar.html#restartable-functions){#toc-restartable-functions}
    -   [[30.2]{.toc-section-number} `wprintf()`, `fwprintf()`, `swprintf()`](wchar.html#man-wprintf){#toc-man-wprintf}
    -   [[30.3]{.toc-section-number} `wscanf()` `fwscanf()` `swscanf()`](wchar.html#man-wscanf){#toc-man-wscanf}
    -   [[30.4]{.toc-section-number} `vwprintf()` `vfwprintf()` `vswprintf()`](wchar.html#man-vwprintf){#toc-man-vwprintf}
    -   [[30.5]{.toc-section-number} `vwscanf()`, `vfwscanf()`, `vswscanf()`](wchar.html#man-vwscanf){#toc-man-vwscanf}
    -   [[30.6]{.toc-section-number} `getwc()` `fgetwc()` `getwchar()`](wchar.html#man-getwc){#toc-man-getwc}
    -   [[30.7]{.toc-section-number} `fgetws()`](wchar.html#man-fgetws){#toc-man-fgetws}
    -   [[30.8]{.toc-section-number} `putwchar()` `putwc()` `fputwc()`](wchar.html#man-putwc){#toc-man-putwc}
    -   [[30.9]{.toc-section-number} `fputws()`](wchar.html#man-fputws){#toc-man-fputws}
    -   [[30.10]{.toc-section-number} `fwide()`](wchar.html#man-fwide){#toc-man-fwide}
    -   [[30.11]{.toc-section-number} `ungetwc()`](wchar.html#man-ungetwc){#toc-man-ungetwc}
    -   [[30.12]{.toc-section-number} `wcstod()` `wcstof()` `wcstold()`](wchar.html#man-wcstod){#toc-man-wcstod}
    -   [[30.13]{.toc-section-number} `wcstol()` `wcstoll()` `wcstoul()` `wcstoull()`](wchar.html#man-wcstol){#toc-man-wcstol}
    -   [[30.14]{.toc-section-number} `wcscpy()` `wcsncpy()`](wchar.html#man-wcscpy){#toc-man-wcscpy}
    -   [[30.15]{.toc-section-number} `wmemcpy()` `wmemmove()`](wchar.html#man-wmemcpy){#toc-man-wmemcpy}
    -   [[30.16]{.toc-section-number} `wcscat()` `wcsncat()`](wchar.html#man-wcscat){#toc-man-wcscat}
    -   [[30.17]{.toc-section-number} `wcscmp()`, `wcsncmp()`, `wmemcmp()`](wchar.html#man-wcscmp){#toc-man-wcscmp}
    -   [[30.18]{.toc-section-number} `wcscoll()`](wchar.html#man-wcscoll){#toc-man-wcscoll}
    -   [[30.19]{.toc-section-number} `wcsxfrm()`](wchar.html#man-wcsxfrm){#toc-man-wcsxfrm}
    -   [[30.20]{.toc-section-number} `wcschr()` `wcsrchr()`](wchar.html#man-wcschr){#toc-man-wcschr}
    -   [[30.21]{.toc-section-number} `wcsspn()` `wcscspn()`](wchar.html#man-wcsspn){#toc-man-wcsspn}
    -   [[30.22]{.toc-section-number} `wcspbrk()`](wchar.html#man-wcspbrk){#toc-man-wcspbrk}
    -   [[30.23]{.toc-section-number} `wcsstr()`](wchar.html#man-wcsstr){#toc-man-wcsstr}
    -   [[30.24]{.toc-section-number} `wcstok()`](wchar.html#man-wcstok){#toc-man-wcstok}
    -   [[30.25]{.toc-section-number} `wcslen()`](wchar.html#man-wcslen){#toc-man-wcslen}
    -   [[30.26]{.toc-section-number} `wcsftime()`](wchar.html#man-wcsftime){#toc-man-wcsftime}
    -   [[30.27]{.toc-section-number} `btowc()` `wctob()`](wchar.html#man-btowc){#toc-man-btowc}
    -   [[30.28]{.toc-section-number} `mbsinit()`](wchar.html#man-mbsinit){#toc-man-mbsinit}
    -   [[30.29]{.toc-section-number} `mbrlen()`](wchar.html#man-mbrlen){#toc-man-mbrlen}
    -   [[30.30]{.toc-section-number} `mbrtowc()`](wchar.html#man-mbrtowc){#toc-man-mbrtowc}
    -   [[30.31]{.toc-section-number} `wcrtomb()`](wchar.html#man-wcrtomb){#toc-man-wcrtomb}
    -   [[30.32]{.toc-section-number} `mbsrtowcs()`](wchar.html#man-mbsrtowcs){#toc-man-mbsrtowcs}
    -   [[30.33]{.toc-section-number} `wcsrtombs()`](wchar.html#man-wcsrtombs){#toc-man-wcsrtombs}

-   [[31]{.toc-section-number} `<wctype.h>` Wide Character Classification and Transformation](wctype.html#wctype){#toc-wctype}

> [[31]{.toc-section-number} <wctype.h> 宽字符分类和转换](wctype.html#wctype){#toc-wctype}
    -   [[31.1]{.toc-section-number} `iswalnum()`](wctype.html#man-iswalnum){#toc-man-iswalnum}
    -   [[31.2]{.toc-section-number} `iswalpha()`](wctype.html#man-iswalpha){#toc-man-iswalpha}
    -   [[31.3]{.toc-section-number} `iswblank()`](wctype.html#man-iswblank){#toc-man-iswblank}
    -   [[31.4]{.toc-section-number} `iswcntrl()`](wctype.html#man-iswcntrl){#toc-man-iswcntrl}
    -   [[31.5]{.toc-section-number} `iswdigit()`](wctype.html#man-iswdigit){#toc-man-iswdigit}
    -   [[31.6]{.toc-section-number} `iswgraph()`](wctype.html#man-iswgraph){#toc-man-iswgraph}
    -   [[31.7]{.toc-section-number} `iswlower()`](wctype.html#man-iswlower){#toc-man-iswlower}
    -   [[31.8]{.toc-section-number} `iswprint()`](wctype.html#man-iswprint){#toc-man-iswprint}
    -   [[31.9]{.toc-section-number} `iswpunct()`](wctype.html#man-iswpunct){#toc-man-iswpunct}
    -   [[31.10]{.toc-section-number} `iswspace()`](wctype.html#man-iswspace){#toc-man-iswspace}
    -   [[31.11]{.toc-section-number} `iswupper()`](wctype.html#man-iswupper){#toc-man-iswupper}
    -   [[31.12]{.toc-section-number} `iswxdigit()`](wctype.html#man-iswxdigit){#toc-man-iswxdigit}
    -   [[31.13]{.toc-section-number} `iswctype()`](wctype.html#man-iswctype){#toc-man-iswctype}
    -   [[31.14]{.toc-section-number} `wctype()`](wctype.html#man-wctype){#toc-man-wctype}
    -   [[31.15]{.toc-section-number} `towlower()`](wctype.html#man-towlower){#toc-man-towlower}
    -   [[31.16]{.toc-section-number} `towupper()`](wctype.html#man-towupper){#toc-man-towupper}
    -   [[31.17]{.toc-section-number} `towctrans()`](wctype.html#man-towctrans){#toc-man-towctrans}
    -   [[31.18]{.toc-section-number} `wctrans()`](wctype.html#man-wctrans){#toc-man-wctrans}

------------------------------------------------------------------------

::: {style="text-align:center"}

[[Prev]() \| ]{style="visibility: hidden"}[Contents](index.html) \| [Next](foreword.html)

> [[上一页]() \| ]{style="visibility: hidden"}[目录](index.html) \| [下一页](foreword.html)
:::
