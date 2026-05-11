---
title:  '#assert, assert and ensure in Odin'
description: 'Quick difference between #assert, assert and ensure in odin'
date: 2026-05-11
tags: ['odin']
showTags: true
readTime: true
---

Simply put:

- [**`#assert`**](https://odin-lang.org/docs/overview/#assertboolean) is a [builtin compile time directive](https://odin-lang.org/docs/overview/#built-in-directives)
meaning it gets evaluated as your program is compiling, similar to zig's comptime feature.

- **`assert`** is a runtime assertion that can be disabled.

- **`ensure`** is also a runtime assertion cannot be disabled at all, the invariant it checks must always hold

---


```odin
// assertions_ensure.odin
package main

import "core:fmt"
import "core:os"

EXPECTED :: 99
SHOW_COMPTIME_ASSERT :: #config(BREAK_ASSERT, "")

main :: proc() {
    program := os.args[0]

    if len(os.args) != 2 {
        fmt.eprintfln("usage: %s [ensure|assert]", program)
        os.exit(1)
    }


    #assert(SHOW_COMPTIME_ASSERT != "YES", "Assert caught at compile time")

    x := 45
    arg := os.args[1]

    switch arg {
    case "ensure":
        ensure(x == EXPECTED, fmt.tprintf("Expected x to be %d; Got: %d", EXPECTED, x))
    case "assert":
        assert(x == EXPECTED, fmt.tprintf("Expected x to be %d; Got: %d", EXPECTED, x))
        fmt.println("x:", x)
    case:
        fmt.eprintfln("Unexpected arg '%s'", arg)
    }
}
```
```sh
# Runtime Assertion + Ensure
$ odin build assertions_ensure.odin -out:assert_enabled -file

$ ./assert_enabled assert
/path/to/assertions_ensure.odin(27:9) runtime assertion: Expected x to be 99; Got: 45
fish: Job 1, './assert_enabled assert' terminated by signal SIGILL (Illegal instruction)


$ ./assert_enabled ensure
/path/to/assertions_ensure.odin(25:9) unsatisfied ensure: Expected x to be 99; Got: 45
fish: Job 1, './assert_enabled ensure' terminated by signal SIGILL (Illegal instruction)

# Asserts disabled
$ odin build assertions_ensure.odin -out:assert_disabled -disable-assert -file
$ ./assert_disabled assert
x: 45

$ ./assert_disabled ensure
unsatisfied ensure: Expected x to be 99; Got: 45
fish: Job 1, './assert_disabled ensure' terminated by signal SIGILL (Illegal instruction)


# Compile Time Assertion
$ odin build assertions_ensure.odin -out:break_assert -disable-assert -define:BREAK_ASSERT=YES -file
/path/to/assertions_ensure.odin(18:5) Error: Compile time assertion: SHOW_COMPTIME_ASSERT != "YES" ("Assert caught at compile time")
        #assert(SHOW_COMPTIME_ASSERT != "YES", "Assert caught a ...
        ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ ...
        Called within 'main' :: proc()


$ odin build assertions_ensure.odin -out:break_assert -define:BREAK_ASSERT=YES -file
/path/to/assertions_ensure.odin(18:5) Error: Compile time assertion: SHOW_COMPTIME_ASSERT != "YES" ("Assert caught at compile time")
        #assert(SHOW_COMPTIME_ASSERT != "YES", "Assert caught a ...
        ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ ...
        Called within 'main' :: proc()
```


