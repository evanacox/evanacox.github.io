---
title: Gallium
type: page
---

[GitHub Repository](https://github.com/evanacox/honors-forum-project)

This is a C-like programming language that compiles to native code via LLVM.

The language itself was designed and documented, and then a compiler for that
language was produced (along with a fairly sizable test suite to ensure that
the compiler kept working through refactors). 

### Technologies used:

- C++
- Generated Parsers (ANTLR in this case)
- Python

### Important pieces of this project:

1. Created a specification for a new C-like language
    - Considered the common issues experienced with C and its derivatives, designed the language to
      avoid these pitfalls.

2. Created a compiler for the language in that specification
    - Designed necessary abstractions and architected the front-end of a compiler from the ground up

### Things learned from this project:

#### The value of isolated, well-planned and well-documented modules

Some parts of this project are a bit gnarly just because I didn't plan out
how they would interact with other pieces, and they end up having many implicit
assumptions about how the other pieces work and what they do/don't do. While
this can work, it's not ideal for maintainability. This taught me a valuable
lesson about putting in the effort to plan beforehand and whenever things change
during the project.

#### When to not reinvent the wheel (and when it may be worth it)

Some problems are solved for the most part, in this case parsing. When there isn't a good
reason to reinvent the wheel, it's usually a good call to just use the existing tools. In
this case, I had no good reason to hand-write a fast parser with decent error messages,
so I just used an existing tool that generated high-quality ones automatically (ANTLR). Doing
so saved a significant amount of time, even if it didn't provide anything particularly amazing.
It was good enough for the job. 

However, sometimes those tools don't quite fill the need, I hit this when trying to write
integration tests against my compiler. No existing testing tools quite filled the need, so
I created a custom tool in Python for the project that did the necessary test parallelization
and nice pass/fail reporting while being configurable for exactly what the project needed.
