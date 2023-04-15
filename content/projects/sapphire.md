---
title: Sapphire
type: page
---

[GitHub Repository](https://github.com/evanacox/sapphire)

This is an compiler middle and back-end that has an optimization framework.

In normal terms, this is the part of a compiler that does optimizations (middle-end) 
and generates instructions for a target (back-end).

### Technologies used:

- Rust
- Generated Parsers (pest.rs in this case)

### Important pieces of this project:

1. Designed and specified a custom intermediary representation
    - This is effectively designing a mini programming language that is designed to be
      easy to analyze and easy to "rewrite" inside of optimizations

2. Created a framework for building modular analyses and optimization passes, and combining them
    - Adapted common patterns and built abstractions allowing passes to be written easily without having
      to know about all the logic needed to orchestrate these passes (e.g. for handling analysis invalidation
      between passes while still allowing caching to avoid recomputing expensive analyses constantly)

3. Implemented a modular, easily re-targetable code generator
    - Designed another intermediary representation that models CPU-specific assembly, but also was generic
      enough to allow things like target-independent register allocation and instruction scheduling to be created

### Things learned from this project:

#### The value of studying existing solutions to similar problems

Many of the high-level design problems I had to solve here were similar to problems solved in projects like
LLVM and Cranelift, exploring how they solved those problems and the pros/cons of those solutions
meant I could make informed decisions and design a solution to avoid those problems where possible.

None of the designs were perfect, and they had to make trade-offs. I learned about those trade-offs and made
decisions that were the most reasonable for this project's unique situation.

#### How to properly apply and adapt 'textbook' approaches to an existing codebase

Compilers specifically are very well-studied in academia, but choosing the approach and
adapting can be difficult when instead of having a "best option" you have 15 different
options that all have pros and cons in different situations. Some of these approaches
are also based on different models of how the compiler and its intermediary representation
work, so they have to be adapted.