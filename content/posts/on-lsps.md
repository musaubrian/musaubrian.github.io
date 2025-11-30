---
title: "On LSPs"
description: my thoughts on Language Servers"
date: 2025-03-02
tags: ["thoughts", "tooling", "rant"]
showTags: true
readTime: true
---

Language servers, whether you know about them or don't. You've almost likely used it.
It's the thing that allows your editor to autocomplete, go to definitions/type definitions.
Frankly they are pretty great.

But GingerBill had a kindof interesting take on LSPs where he said that he doesn't use them.
I thought, who the hell doesn't use an LSP completely, are they crazy or they those purists -same thing.
But a point he said supporting this, is that you get to understand the codebase slightly better.
I thought that can't possibly be true, so I decided to do an experiment -no I didn't ditch LSPs-
I disabled the autocomplete feature, and he may have been onto something.
I genuinely believe that I write code differently,
I think things through slightly better and better yet, I name things better.

In as much as I like the quickfix list subing out strings with
`:cdo <some_random_regex>`.

I could not get rid of `rename`. *Goto Definition* on the other hand I was kinda on-and-off about,
I sub it with `grep` or `live_grep` or `vimgrep`.

> Also from the linux kernel rust drama,
> I *understood the importance of a codebase being `greppable`

Was this experiment worth it. *Absolutely*.
Will I go back to using autocomplete, *No*. I never really truly disabled it it was just there,
but I had to intentionally trigger it if I wasn't really feeling like grepping for the thing I just forgot.

If you would like to try it out, you can add this to your *[blink \[dot\] lua](https://github.com/saghen/blink.cmp)*

```lua
-- blink.lua
opts = {
    -- rest of config

    completion = {
        menu = {
            auto_show = function()
                -- Dont show on command mode or insert
                if vim.fn.mode() == "c" or vim.fn.mode() == "i" then
                    return false
                end
                return true
            end,
            draw = {
                columns = {
                    { "label", "label_description", gap = 1 },
                    { "kind" }
                },
            },
        },
    }

    -- rest of config
}
```

Not really sure how to do it in nvim-cmp

