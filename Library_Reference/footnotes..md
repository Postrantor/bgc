---
tip: translate by openai@2023-07-20 18:22:08
...
---
generator: pandoc
title: Beej\'s Guide to C Programming
viewport: width=device-width, initial-scale=1.0, user-scalable=yes
---

::: {style="text-align:center"}

[Prev](wctype.html) \| [Contents](index.html)[ \| [Next]()]{style="visibility: hidden"}

> [上一页](wctype.html) \| [目录](index.html) \| [下一页](){style="visibility: hidden"}
:::

------------------------------------------------------------------------

::: {#footnotes .section .footnotes .footnotes-end-of-document role="doc-endnotes"}
1.  ::: {#fn1}
    https://beej.us/guide/bgc/[↩︎](foreword.html#fnref1){.footnote-back role="doc-backlink"}
    :::

2.  ::: {#fn2}
    https://en.wikipedia.org/wiki/ANSI_C[↩︎](foreword.html#fnref2){.footnote-back role="doc-backlink"}
    :::

3.  ::: {#fn3}
    https://en.wikipedia.org/wiki/POSIX[↩︎](foreword.html#fnref3){.footnote-back role="doc-backlink"}
    :::

4.  ::: {#fn4}
    https://visualstudio.microsoft.com/vs/community/[↩︎](foreword.html#fnref4){.footnote-back role="doc-backlink"}
    :::

5.  ::: {#fn5}
    https://docs.microsoft.com/en-us/windows/wsl/install-win10[↩︎](foreword.html#fnref5){.footnote-back role="doc-backlink"}
    :::

6.  ::: {#fn6}
    https://developer.apple.com/xcode/[↩︎](foreword.html#fnref6){.footnote-back role="doc-backlink"}
    :::

7.  ::: {#fn7}
    https://beej.us/guide/bgclr/[↩︎](foreword.html#fnref7){.footnote-back role="doc-backlink"}
    :::

8.  ::: {#fn8}
    https://en.cppreference.com/[↩︎](foreword.html#fnref8){.footnote-back role="doc-backlink"}
    :::

9.  ::: {#fn9}
    https://groups.google.com/g/comp.lang.c[↩︎](foreword.html#fnref9){.footnote-back role="doc-backlink"}
    :::

10. ::: {#fn10}
    https://www.reddit.com/r/C_Programming/[↩︎](foreword.html#fnref10){.footnote-back role="doc-backlink"}
    :::

11. ::: {#fn11}
    This doesn't change the type of `x` in other contexts---it's just in this one usage in this expression.[↩︎](the-c-language.html#fnref11){.footnote-back role="doc-backlink"}
    :::

12. ::: {#fn12}
    Note that this implication only for `main()`, and not for any other functions.[↩︎](the-c-language.html#fnref12){.footnote-back role="doc-backlink"}
    :::

13. ::: {#fn13}
    https://en.wikipedia.org/wiki/Complex_conjugate[↩︎](complex.html#fnref13){.footnote-back role="doc-backlink"}
    :::

14. ::: {#fn14}
    https://en.wikipedia.org/wiki/Riemann_sphere[↩︎](complex.html#fnref14){.footnote-back role="doc-backlink"}
    :::

15. ::: {#fn15}
    Really it's just required to be a modifiable lvalue, so not necessarily a variable. But you can treat it as such.[↩︎](errno.html#fnref15){.footnote-back role="doc-backlink"}
    :::

16. ::: {#fn16}
    https://man.archlinux.org/man/errno.3.en[↩︎](errno.html#fnref16){.footnote-back role="doc-backlink"}
    :::

17. ::: {#fn17}
    https://docs.microsoft.com/en-us/cpp/c-runtime-library/errno-constants?view=msvc-160[↩︎](errno.html#fnref17){.footnote-back role="doc-backlink"}
    :::

18. ::: {#fn18}
    https://en.wikipedia.org/wiki/Subnormal_number[↩︎](float.html#fnref18){.footnote-back role="doc-backlink"}
    :::

19. ::: {#fn19}
    The minimum value of an `unsigned char` is `0`. Same fo an `unsigned short` and `unsigned long`. Or any unsigned type, for that matter.[↩︎](limits.html#fnref19){.footnote-back role="doc-backlink"}
    :::

20. ::: {#fn20}
    https://en.wikipedia.org/wiki/Two%27s_complement[↩︎](limits.html#fnref20){.footnote-back role="doc-backlink"}
    :::

21. ::: {#fn21}
    Remember that `char` is just a byte-sized integer.[↩︎](locale.html#fnref21){.footnote-back role="doc-backlink"}
    :::

22. ::: {#fn22}
    Though the system defines `MATH_ERRNO` as `1` and `MATH_ERREXCEPT` as `2`, it's best to always use their symbolic names. Just in case.[↩︎](math.html#fnref22){.footnote-back role="doc-backlink"}
    :::

23. ::: {#fn23}
    https://en.wikipedia.org/wiki/Denormal_number[↩︎](math.html#fnref23){.footnote-back role="doc-backlink"}
    :::

24. ::: {#fn24}
    This is on my system. Some systems will have different points at which numbers become subnormal, or they might not support subnormal values at all.[↩︎](math.html#fnref24){.footnote-back role="doc-backlink"}
    :::

25. ::: {#fn25}
    https://en.wikipedia.org/wiki/E\_(mathematical_constant)[↩︎](math.html#fnref25){.footnote-back role="doc-backlink"}
    :::

26. ::: {#fn26}
    https://en.wikipedia.org/wiki/Denormal_number[↩︎](math.html#fnref26){.footnote-back role="doc-backlink"}
    :::

27. ::: {#fn27}
    https://en.wikipedia.org/wiki/Pythagorean_theorem[↩︎](math.html#fnref27){.footnote-back role="doc-backlink"}
    :::

28. ::: {#fn28}
    https://en.wikipedia.org/wiki/Error_function[↩︎](math.html#fnref28){.footnote-back role="doc-backlink"}
    :::

29. ::: {#fn29}
    https://en.wikipedia.org/wiki/Error_function[↩︎](math.html#fnref29){.footnote-back role="doc-backlink"}
    :::

30. ::: {#fn30}
    https://en.wikipedia.org/wiki/Gamma_function[↩︎](math.html#fnref30){.footnote-back role="doc-backlink"}
    :::

31. ::: {#fn31}
    https://en.wikipedia.org/wiki/Gamma_function[↩︎](math.html#fnref31){.footnote-back role="doc-backlink"}
    :::

32. ::: {#fn32}
    https://en.cppreference.com/w/c/numeric/math/remquo[↩︎](math.html#fnref32){.footnote-back role="doc-backlink"}
    :::

33. ::: {#fn33}
    https://en.cppreference.com/w/c/numeric/math/remquo[↩︎](math.html#fnref33){.footnote-back role="doc-backlink"}
    :::

34. ::: {#fn34}
    A *quiet NaN* is one that doesn't raise any exceptions.[↩︎](math.html#fnref34){.footnote-back role="doc-backlink"}
    :::

35. ::: {#fn35}
    https://man.archlinux.org/man/sigaction.2.en[↩︎](signal.html#fnref35){.footnote-back role="doc-backlink"}
    :::

36. ::: {#fn36}
    As if might be sent from Unix's `kill` command.\][↩︎](signal.html#fnref36){.footnote-back role="doc-backlink"}
    :::

37. ::: {#fn37}
    https://en.wikipedia.org/wiki/Data_structure_alignment[↩︎](stdalign.html#fnref37){.footnote-back role="doc-backlink"}
    :::

38. ::: {#fn38}
    Maybe it depends on the run-time environment and can't be known at compile-time.[↩︎](stdatomic.html#fnref38){.footnote-back role="doc-backlink"}
    :::

39. ::: {#fn39}
    https://en.cppreference.com/w/cpp/atomic/ATOMIC_VAR_INIT[↩︎](stdatomic.html#fnref39){.footnote-back role="doc-backlink"}
    :::

40. ::: {#fn40}
    http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1138r0.pdf[↩︎](stdatomic.html#fnref40){.footnote-back role="doc-backlink"}
    :::

41. ::: {#fn41}
    This effectively does the same thing, but it's clearly not atomic.[↩︎](stdatomic.html#fnref41){.footnote-back role="doc-backlink"}
    :::

42. ::: {#fn42}
    The spec says, "This spurious failure enables implementation of compare-and-exchange on a broader class of machines, e.g. load-locked store-conditional machines." And adds, "When a compare-and-exchange is in a loop, the weak version will yield better performance on some platforms. When a weak compare-and-exchange would require a loop and a strong one would not, the strong one is preferable."[↩︎](stdatomic.html#fnref42){.footnote-back role="doc-backlink"}
    :::

43. ::: {#fn43}
    Don't use this unless you know what you're doing---use the thread mutex functionality instead. It'll let your blocked thread sleep and stop chewing up CPU.[↩︎](stdatomic.html#fnref43){.footnote-back role="doc-backlink"}
    :::

44. ::: {#fn44}
    Don't use this unless you know what you're doing---use the thread mutex functionality instead. It'll let your blocked thread sleep and stop chewing up CPU.[↩︎](stdatomic.html#fnref44){.footnote-back role="doc-backlink"}
    :::

45. ::: {#fn45}
    https://en.wikipedia.org/wiki/Data_structure_alignment[↩︎](stddef.html#fnref45){.footnote-back role="doc-backlink"}
    :::

46. ::: {#fn46}
    https://man.archlinux.org/man/unlinkat.2.en#DESCRIPTION[↩︎](stdio.html#fnref46){.footnote-back role="doc-backlink"}
    :::

47. ::: {#fn47}
    https://man.archlinux.org/man/mkstemp.3.en[↩︎](stdio.html#fnref47){.footnote-back role="doc-backlink"}
    :::

48. ::: {#fn48}
    https://nee.lv/2021/02/28/How-I-cut-GTA-Online-loading-times-by-70/[↩︎](stdio.html#fnref48){.footnote-back role="doc-backlink"}
    :::

49. ::: {#fn49}
    https://stackoverflow.com/questions/17017331/c99-vscanf-for-dummies/17018046#17018046[↩︎](stdio.html#fnref49){.footnote-back role="doc-backlink"}
    :::

50. ::: {#fn50}
    http://man.cat-v.org/unix-1st/3/atof[↩︎](stdlib.html#fnref50){.footnote-back role="doc-backlink"}
    :::

51. ::: {#fn51}
    http://man.cat-v.org/unix-1st/3/atoi[↩︎](stdlib.html#fnref51){.footnote-back role="doc-backlink"}
    :::

52. ::: {#fn52}
    https://en.wikipedia.org/wiki/Radix[↩︎](stdlib.html#fnref52){.footnote-back role="doc-backlink"}
    :::

53. ::: {#fn53}
    https://stackoverflow.com/questions/10984974/why-do-people-say-there-is-modulo-bias-when-using-a-random-number-generator[↩︎](stdlib.html#fnref53){.footnote-back role="doc-backlink"}
    :::

54. ::: {#fn54}
    https://mumble.net/\~campbell/2014/04/28/uniform-random-float[↩︎](stdlib.html#fnref54){.footnote-back role="doc-backlink"}
    :::

55. ::: {#fn55}
    https://www.gnu.org/software/gsl/doc/html/rng.html[↩︎](stdlib.html#fnref55){.footnote-back role="doc-backlink"}
    :::

56. ::: {#fn56}
    Minecraft enthusiasts might recall that when generating a new world, they were given the option to enter a random number seed. That single value is used to generate that entire random world. And if your friend starts a world with the same seed you did, they'll get the same world you did.[↩︎](stdlib.html#fnref56){.footnote-back role="doc-backlink"}
    :::

57. ::: {#fn57}
    https://en.wikipedia.org/wiki/Unix_time[↩︎](stdlib.html#fnref57){.footnote-back role="doc-backlink"}
    :::

58. ::: {#fn58}
    The C spec doesn't say exactly what `time(NULL)` will return, but the POSIX spec does! And virtually everyone returns exactly that: the number of seconds since epoch.[↩︎](stdlib.html#fnref58){.footnote-back role="doc-backlink"}
    :::

59. ::: {#fn59}
    https://en.wikipedia.org/wiki/Data_structure_alignment[↩︎](stdlib.html#fnref59){.footnote-back role="doc-backlink"}
    :::

60. ::: {#fn60}
    "Try to imagine all life as you know it stopping instantaneously and every molecule in your body exploding at the speed of light." ---Egon Spengler[↩︎](stdlib.html#fnref60){.footnote-back role="doc-backlink"}
    :::

61. ::: {#fn61}
    https://en.wikipedia.org/wiki/Core_dump[↩︎](stdlib.html#fnref61){.footnote-back role="doc-backlink"}
    :::

62. ::: {#fn62}
    `quick_exit()` differs from `exit()` in that open files might not be flushed and temporary files might not be removed.[↩︎](stdlib.html#fnref62){.footnote-back role="doc-backlink"}
    :::

63. ::: {#fn63}
    "In-place" meaning that the original array will hold the results; no new array is allocated.[↩︎](stdlib.html#fnref63){.footnote-back role="doc-backlink"}
    :::

64. ::: {#fn64}
    It always returns the number of bytes the transformed string took, but in this case because `s1` was `NULL`, it doesn't actually write a transformed string.[↩︎](stringref.html#fnref64){.footnote-back role="doc-backlink"}
    :::

65. ::: {#fn65}
    Which you should because of spurious wakeups.[↩︎](threads.html#fnref65){.footnote-back role="doc-backlink"}
    :::

66. ::: {#fn66}
    Well, as at least as many things as you have free cores. Your OS will schedule them as it can.[↩︎](threads.html#fnref66){.footnote-back role="doc-backlink"}
    :::

67. ::: {#fn67}
    For example, if a destructor caused more variables to be set.[↩︎](threads.html#fnref67){.footnote-back role="doc-backlink"}
    :::

68. ::: {#fn68}
    Unix-like systems have a `sleep()` syscall that sleeps for an integer number of seconds. But `thrd_sleep()` is likely more portable and gives subsecond resolution, besides![↩︎](threads.html#fnref68){.footnote-back role="doc-backlink"}
    :::

69. ::: {#fn69}
    When you say GMT, unless you're talking specifically about the time zone and not the time, you probably mean "UTC".[↩︎](time.html#fnref69){.footnote-back role="doc-backlink"}
    :::

70. ::: {#fn70}
    The spec doesn't actually say "clock ticks", but I... am.[↩︎](time.html#fnref70){.footnote-back role="doc-backlink"}
    :::

71. ::: {#fn71}
    Unless you're on a POSIX system where `time_t` is definitely an integer, in which case you can subtract. But you should still use `difftime()` for maximum portability.[↩︎](time.html#fnref71){.footnote-back role="doc-backlink"}
    :::

72. ::: {#fn72}
    https://man.archlinux.org/man/timegm.3.en[↩︎](time.html#fnref72){.footnote-back role="doc-backlink"}
    :::

73. ::: {#fn73}
    https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/mkgmtime-mkgmtime32-mkgmtime64?view=msvc-160[↩︎](time.html#fnref73){.footnote-back role="doc-backlink"}
    :::

74. ::: {#fn74}
    https://en.wikipedia.org/wiki/Unix_time[↩︎](time.html#fnref74){.footnote-back role="doc-backlink"}
    :::

75. ::: {#fn75}
    https://en.wikipedia.org/wiki/ISO_week_date[↩︎](time.html#fnref75){.footnote-back role="doc-backlink"}
    :::

76. ::: {#fn76}
    https://en.wikipedia.org/wiki/Symbols_for_Legacy_Computing[↩︎](uchar.html#fnref76){.footnote-back role="doc-backlink"}
    :::

77. ::: {#fn77}
    https://stackoverflow.com/questions/17017331/c99-vscanf-for-dummies/17018046#17018046[↩︎](wchar.html#fnref77){.footnote-back role="doc-backlink"}
    :::

78. ::: {#fn78}
    This is a variable, not a macro, so if you use it to define an array, it'll be a variable-length array.[↩︎](wchar.html#fnref78){.footnote-back role="doc-backlink"}
    :::
:::

------------------------------------------------------------------------

::: {style="text-align:center"}

[Prev](wctype.html) \| [Contents](index.html)[ \| [Next]()]{style="visibility: hidden"}

> [上一页](wctype.html) \| [目录](index.html) \| [下一页](){style="visibility: hidden"}
:::
