---
title: Chip-8 Emulator
type: page
---

[GitHub Repository](https://github.com/evanacox/chip8)

This is a complete Chip-8 emulator written in a weekend.

### Technologies used:

- C++
- SFML (a graphics library in C++)
- CMake

### Important pieces of this project:

1. Designed a "virtual machine" emulating the hardware based on existing Chip-8 specifications
    - Chip-8 is an existing "architecture" specifically designed to be emulated, with an existing
      catalog of software written against that specification. This specification was followed and tested
      with that software catalog.

2. Applied SFML to display what was actually going on in that virtual machine
    - Chip-8 is a bit unique in that it actually includes the "display" as part of the specification,
      and has some instructions that directly manipulate the screen rather than manipulating specific
      parts of memory to communicate with devices like most real hardware does. This had to be integrated
      in a way that was both clean on the VM level and still provided some separation of concerns between
      the Chip-8 CPU emulator and the display driver.

### Things learned from this project:

#### How to use existing specifications

Chip-8 is not a 'formal' specification but informally it is very widely agreed-on with how it's supposed
to work, with many specifications being presented in a similar way to datasheets of real hardware. I had to 
learn how to properly make use of these specifications to make a working emulator.

I also used the existing software catalog to test my adherance to this specification rather than
make my own, as that catalog already exists and is what I was actually trying to emulate.