---
title: "Building for you"
description: "Turns out, you can just build stuff"
date: 2024-09-24
tags: ["exploring"]
showTags: true
readTime: true
---

Recently, I've been getting back into python development.
I came upon the same issue: *virtual environment activation*.
Now this is an already solved problem; you can use an IDE or conda(I've heard it mentioned, but haven't really used it personally).


I didn't want to go setup an IDE, or conda. I just wanted the environment to be active when I open up neovim, and in neovim's terminal as well.

So I went on a tangent from doing the actual thing I wanted in python, to trying and figuring this already solved problem.

What I wanted was very simple:
- When I open a python project with a virtual env, activate it
- LSP should still work (documentation | go to definition...)

The first approach I took was just sourcing the virtual env as I'd normally do in the terminal.
This didn't work because of how neovim handles subprocesses.
Basically when a command like `source` is called, it doesn't persist in that sessions environment.

Took a different approach by just reading the virtual env activation script.
Found it that its just environment variables setting and unsetting, this fixed part of it.
This [reddit](https://www.reddit.com/r/neovim/comments/159z8lz/comment/jticsry/) post helped me solve the LSP issue.

This option was good but not good enough because when I open up the neovim terminal,
the interpreter still defaults to the global one. I didnt want that, because the packages won't be in the global environment.
I solved this by just appending the virtual envs interpreter to the `$PATH`

The cherry-on-top, this is completely within your neovim instance,
I was kinda skeptical because, messing with the `$PATH` can couse issues, but this was a nice finding.


Could I have solved this issue by just using an IDE or Conda, YES.
Could I have learnt about how virtual envirionment activation works, _absolutely NOT_.

Thats the beauty in building stuff for yourself, you get to understand a concept much better.

You can find it at [pye.nvim](https://github.com/musaubrian/pye.nvim)
