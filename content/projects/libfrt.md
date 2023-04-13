---
title: Freestanding Runtime Library
type: page
---

[GitHub Repository](https://github.com/evanacox/freestanding-rt)

A C++ utility library made for use in bare-metal environments where there may not
actually be a standard library implementation. 

This was made specifically for use with some freestanding GCC cross-compilers where
a C library is not present and thus libstdc++ cannot be built. Some core language features
in C++ require a standard library (notably `operator<=>` in C++20), and other things from
the standard library would be useful in bare-metal (e.g. a `std::array`-like type, atomics,
iterator utilities, type traits). This library fills those needs.

### Technologies used:

- C++
- CMake

### Important pieces of this project:

1. Studied existing standard library implementations in order to implement efficient
   equivalents of some types provided in them
    - Things like `std::atomic` or `std::strong_ordering` require compiler support, I had
      to see how those were implemented to get equivalent facilities in libfrt.

2. Considered the design decisions in `std`, and adopted alternative designs where reasonable
    - Made `frt::atomic` memory orderings safe at compile time, the build will fail if an ordering incompatible
      with the operation being used is provided instead of it being undefined behavior.
    - Assertions have an optional message instead of needing to cram it into the condition
    - Algorithms are ranges-first rather than having both range versions and equivalent iterator versions
    - Iterators are concepts-first and have helper types for defining them that aren't insane
    - Provided `volatile_load` and `volatile_write` for explicit-ness reasons
    - Provided functions for unaligned accesses explicitly instead of relying on `memcpy`-ing everywhere

### Things learned from this project:

#### (Almost) every decision has a trade-off

Many "bad" design decision in `std` was made for a reason that seemed reasonable at
the time (at least to the people on the committee), and thus it wasn't as simple as just
changing something. Thought has to be put in before just changing things.

I will note that some bad decisions were really just bad decisions though (*cough* `std::vector<bool>` 
*cough*) or just can never be fixed due to backwards-compat.

