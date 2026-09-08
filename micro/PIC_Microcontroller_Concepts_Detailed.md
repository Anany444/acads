# PIC Microcontrollers, PIC Assembly, Timers, I/O, and Serial Communication

> **Study guide based on the uploaded handwritten notes (38 pages).**
>
> The notes mainly cover PIC microcontrollers, especially
> PIC16/PIC18-family concepts, PIC assembly language, instruction
> formats, status flags, addressing modes, timers, I/O programming,
> serial communication, and basic C programming examples. Some
> handwritten values are difficult to read, so this guide explains the
> concepts without inventing uncertain device-specific details.

------------------------------------------------------------------------

## 1. Microcontrollers and Embedded Systems

### What is a microcontroller?

A **microcontroller (MCU)** is a small computer placed on a single
integrated circuit. It normally contains:

-   A CPU/core
-   Program memory
-   Data memory/RAM
-   Input/output (I/O) pins
-   Timers/counters
-   Communication peripherals
-   A clock/oscillator system

A microcontroller is designed to control a specific system rather than
run general-purpose desktop applications.

### Microcontroller vs microprocessor

A **microprocessor** mainly provides the CPU. Memory and peripherals are
commonly external.

A **microcontroller** integrates the CPU, memory, and peripherals on one
chip.

A simple mental model is:

``` text
Microprocessor:
CPU <----> External RAM
     <----> External ROM
     <----> External I/O

Microcontroller:
+--------------------------------+
| CPU | Program Memory | RAM     |
| Timers | I/O | Serial | Other |
+--------------------------------+
```

### Examples mentioned in the notes

The notes mention:

-   ARM --- Advanced RISC Machine
-   PIC --- Peripheral Interface Controller
-   8051 family
-   PIC16 and PIC18 families

The notes also mention that PIC devices are widely used because of their
integration, low cost, and suitability for embedded control.

------------------------------------------------------------------------

# 2. 8051 and PIC: Background

The notes briefly discuss the 8051 family and PIC architecture.

An 8051-type microcontroller is described in the notes as having an
8-bit CPU, program memory, RAM, timers, I/O ports, serial communication,
and an on-chip clock oscillator.

The notes then move primarily to PIC microcontrollers.

For exam preparation, the important transition is:

**8-bit MCU → CPU + memory + peripherals → instruction set → I/O
programming → timers → serial communication.**

------------------------------------------------------------------------

# 3. PIC Microcontroller Basics

## 3.1 What does PIC mean?

The notes use PIC as **Peripheral Interface Controller**.

PIC is a family of microcontrollers developed by Microchip Technology.

Different PIC families have different:

-   CPU architectures
-   Instruction sets
-   Memory sizes
-   Peripheral sets
-   Number of I/O pins
-   Timers
-   Communication modules

Therefore, always check the specific PIC datasheet when an exact
register address or bit definition is required.

------------------------------------------------------------------------

# 4. Harvard Architecture

One of the important concepts in the notes is **Harvard architecture**.

## 4.1 Basic idea

In a Harvard architecture, **program memory and data memory are
separate**.

``` text
             +--------+
             |  CPU   |
             +--------+
                |  |
       ----------  ----------
       |                    |
+--------------+      +-------------+
| Program      |      | Data Memory |
| Memory       |      | / RAM       |
+--------------+      +-------------+
```

This is different from a traditional von Neumann architecture, where
instructions and data share the same memory space/bus.

## 4.2 Why separate memories?

The CPU can access program instructions and data using separate paths.

This can improve:

-   Throughput
-   Instruction fetching
-   Parallelism
-   Overall execution efficiency

The notes explicitly connect PIC memory organization with Harvard
architecture.

------------------------------------------------------------------------

# 5. RISC Architecture

The notes describe PIC as using a **RISC** approach.

RISC means:

**Reduced Instruction Set Computer**

The basic idea is to use a relatively small set of simple instructions.

### Typical RISC characteristics

-   Simple instructions
-   Regular instruction formats
-   Efficient execution
-   Emphasis on fast instruction processing
-   Often supports pipelining

The notes contrast instruction-cycle behavior and mention that PIC18
uses more than one instruction cycle in some contexts, while PIC16 has a
simpler instruction-cycle relationship.

### RISC vs CISC --- beginner view

Imagine two approaches to giving instructions to a worker:

**RISC:** \> Do one simple operation quickly.

**CISC:** \> Give one complex instruction that performs several
operations.

Neither philosophy is universally "better"; they are different
architectural design approaches.

------------------------------------------------------------------------

# 6. PIC CPU Architecture

The notes contain a CPU architecture diagram showing the CPU connected
with:

-   Program memory
-   Data memory/RAM
-   EEPROM
-   Timers
-   I/O/peripheral devices

The central idea is that the CPU executes instructions while
communicating with memory and peripherals.

### Important CPU components

## ALU

The **Arithmetic Logic Unit (ALU)** performs operations such as:

-   Addition
-   Subtraction
-   AND
-   OR
-   XOR
-   Comparisons
-   Bit operations

## WREG

`WREG` is the **working register** in the PIC architecture discussed in
the notes.

It acts as a primary working register for many arithmetic, logical, and
data-transfer operations.

Example:

``` asm
MOVLW 0x25
```

Conceptually:

``` text
WREG ← 0x25
```

Then:

``` asm
MOVWF 0x20
```

means:

``` text
File register 0x20 ← WREG
```

------------------------------------------------------------------------

# 7. PIC Memory Organization

The notes distinguish:

-   Program memory
-   Data memory/RAM
-   EEPROM
-   Flash/program storage

## 7.1 Program memory

Program memory stores the instructions that the CPU executes.

The notes mention Flash memory and OTP/EPROM-type variants.

### Flash

Flash is non-volatile memory.

That means its contents remain after power is removed.

It can be electrically reprogrammed.

### OTP

OTP means:

**One-Time Programmable**

It is programmed once and is not normally erased and reprogrammed like
Flash.

------------------------------------------------------------------------

# 8. Program Counter

The **Program Counter (PC)** stores the address of the instruction that
the processor will execute.

Conceptually:

``` text
PC → address of next instruction
```

After an ordinary instruction, the PC advances to the next instruction.

Branching, calling, returning, and jumping instructions modify the
normal sequence.

------------------------------------------------------------------------

# 9. Stack and Stack Pointer

The notes contain a section on the **stack** and **SP**.

A stack is a temporary storage structure following:

**LIFO --- Last In, First Out**

Think of a stack of plates:

``` text
Push → put something on top
Pop  → remove the top item
```

Stacks are particularly important for:

-   Subroutine calls
-   Return addresses
-   Nested calls
-   Temporary processor state in architectures that support it

The notes show the program counter/return address relationship with the
stack.

------------------------------------------------------------------------

# 10. PIC Instruction Format

The notes show instruction formats containing:

-   Opcode
-   Literal or operand
-   Address/file register information

A simplified view is:

``` text
+----------------------+------------------+
|       OPCODE         |    OPERAND       |
+----------------------+------------------+
```

The exact bit allocation depends on the PIC family and instruction.

## Common operand types

### Literal

A literal is a constant written directly in the instruction.

Example:

``` asm
MOVLW 0x25
```

Here `0x25` is a literal constant.

### File register

A file register refers to a memory/register location.

Example:

``` asm
MOVWF 0x20
```

The address `0x20` identifies a file-register location in the relevant
data-memory context.

------------------------------------------------------------------------

# 11. PIC Assembly Language

The notes describe three major concepts:

1.  Compiler
2.  Assembler
3.  Directives

## Compiler

A compiler translates a high-level language such as C into lower-level
machine-oriented code.

``` text
C source
   ↓
Compiler
   ↓
Assembly / object code
   ↓
Linking
   ↓
Machine code
```

## Assembler

An assembler converts assembly-language instructions into machine code.

For example:

``` asm
MOVLW 0x25
```

is translated into the corresponding machine representation for the
selected PIC.

## Linker

A linker combines program/object sections and resolves references to
produce the final program image.

------------------------------------------------------------------------

# 12. MPLAB

The notes mention **MPLAB** as an environment used for:

-   Assembly
-   Linking
-   Simulation
-   PIC development

For beginner understanding, think of MPLAB as the development
environment in which PIC firmware can be written, built,
simulated/debugged, and programmed using appropriate hardware/tools.

------------------------------------------------------------------------

# 13. Assembly Directives

Assembly directives are instructions to the assembler rather than
instructions executed by the microcontroller.

The notes mention directives such as:

-   `EQU`
-   `SET`
-   `ORG`
-   `END`
-   `LIST`
-   `CBLOCK`
-   `DEFSZ` in the instruction discussion

## 13.1 EQU

`EQU` defines a symbolic constant.

Example:

``` asm
COUNT EQU 0x25
```

Now `COUNT` represents the value/address assigned by the directive.

This improves readability.

Instead of:

``` asm
MOVLW 0x25
```

you can use a meaningful symbol where appropriate.

## 13.2 SET

`SET` can be used to assign/reassign a symbolic value in assembler
source, depending on assembler syntax.

## 13.3 ORG

`ORG` specifies an origin/address for subsequent assembled code or data.

Think:

> "Start placing the following code/data at this address."

## 13.4 END

Marks the end of the assembly source file.

## 13.5 LIST

Used for assembler/listing-related configuration.

------------------------------------------------------------------------

# 14. Labels

A **label** is a symbolic name attached to a location in the program.

Example:

``` asm
LOOP:
    DECFSZ COUNT,F
    GOTO LOOP
```

`LOOP` identifies the destination of the branch.

Labels are useful because you do not have to remember numeric
instruction addresses.

------------------------------------------------------------------------

# 15. Basic PIC Data-Movement Instructions

The notes repeatedly use:

-   `MOVLW`
-   `MOVWF`
-   `MOVF`
-   `MOVFF`
-   `LFSR`

## 15.1 MOVLW

Meaning:

**Move Literal to WREG**

Example:

``` asm
MOVLW 0x25
```

Conceptually:

``` text
WREG ← 0x25
```

## 15.2 MOVWF

Meaning:

**Move WREG to File register**

Example:

``` asm
MOVWF PORTB
```

Conceptually:

``` text
PORTB ← WREG
```

If WREG contains `0x55`, the instruction writes `0x55` to the
destination register.

## 15.3 MOVF

Moves a file-register value, with the exact destination/control
determined by the instruction's operands.

The important beginner idea is that the instruction operates on a **file
register** and can be used to move/test register data.

## 15.4 MOVFF

The notes associate `MOVFF` with moving a value directly from one file
register to another.

Conceptually:

``` text
destination ← source
```

This is useful when WREG does not need to be used as an intermediate
register.

------------------------------------------------------------------------

# 16. Arithmetic Instructions

The notes include:

-   `ADDWF`
-   `ADDWFC`
-   `SUBLW`
-   `SUBWF`
-   `DAW`
-   `INCF`
-   `DECF`

------------------------------------------------------------------------

## 16.1 ADDWF

Conceptually:

``` text
WREG + FileRegister → destination
```

The destination control determines whether the result goes to WREG or
the file register.

Example idea:

``` asm
MOVLW 0x05
ADDWF VALUE,W
```

The operation adds WREG and the file register and stores the result
according to the destination bit.

------------------------------------------------------------------------

# 17. Status Register and Flags

The notes give a status-register diagram containing flags including:

-   `N`
-   `OV`
-   `Z`
-   `DC`
-   `C`

The exact status register layout depends on the PIC family, but these
flags represent important arithmetic results.

## 17.1 Carry flag --- C

Carry indicates an unsigned carry out of the most significant bit during
an arithmetic operation.

For an 8-bit addition:

``` text
  11111111
+ 00000001
-----------
1 00000000
```

The result is `0x00` and a carry is produced.

Therefore, conceptually:

``` text
C = 1
```

## 17.2 Digit Carry --- DC

DC is the **digit carry** flag.

It is associated with carry from the lower nibble to the upper nibble.

For example, if the lower 4 bits overflow:

``` text
1111 + 0001
```

the lower nibble produces a carry.

This flag is important for BCD arithmetic.

## 17.3 Zero flag --- Z

The zero flag indicates whether an arithmetic/logical result is zero.

If:

``` text
result = 0x00
```

then:

``` text
Z = 1
```

If the result is nonzero, Z is cleared.

## 17.4 Overflow flag --- OV

Overflow is relevant to **signed arithmetic**.

It indicates that a signed result cannot be represented correctly in the
available bit width.

Do not confuse:

-   Carry → mainly associated with unsigned arithmetic
-   Overflow → signed arithmetic

## 17.5 Negative flag --- N

The N flag reflects the sign of the result in signed arithmetic,
typically based on the most significant bit.

------------------------------------------------------------------------

# 18. Example: Addition and Flags

Suppose:

``` asm
MOVLW 0xF5
ADDWF VALUE,W
```

If `VALUE = 0x2B`, then:

``` text
  F5
+ 2B
----
120
```

For an 8-bit result:

``` text
Result = 20H
Carry  = 1
```

Thus the carry flag is set.

When solving flag questions, always:

1.  Convert operands to binary if needed.
2.  Perform the operation.
3.  Keep the processor's result width.
4.  Identify carry.
5.  Check lower-nibble carry for DC.
6.  Check whether result is zero.
7.  For signed interpretation, check N and OV.

------------------------------------------------------------------------

# 19. Subtraction

The notes use instructions such as:

``` asm
SUBLW
SUBWF
```

The direction matters.

For example, the notes describe `SUBLW` in the form:

``` text
literal - WREG
```

and `SUBWF` as involving a file register and WREG.

### Why subtraction can be confusing

Microcontrollers commonly implement subtraction using two's-complement
arithmetic.

For an n-bit value:

``` text
-X = (~X) + 1
```

This allows subtraction to be implemented using addition hardware.

------------------------------------------------------------------------

# 20. Two's Complement

Two's complement is the standard representation used for signed integers
in most processors.

For an 8-bit number:

``` text
+5 = 0000 0101
```

To form `-5`:

1.  Invert bits:

``` text
1111 1010
```

2.  Add 1:

``` text
1111 1011
```

Therefore:

``` text
-5 = 1111 1011
```

The notes use two's-complement concepts while discussing subtraction.

------------------------------------------------------------------------

# 21. BCD and DAW

BCD means:

**Binary-Coded Decimal**

Each decimal digit is represented by four bits.

Examples:

``` text
Decimal 9 → 1001
Decimal 5 → 0101
Decimal 25 → 0010 0101
```

A 4-bit BCD digit is valid from:

``` text
0000 to 1001
```

Values `1010` through `1111` are not valid BCD digits.

## DAW

The notes describe `DAW` as **Decimal Adjust WREG**.

After BCD addition, the binary result may not be a valid BCD
representation.

`DAW` adjusts the result, using the relevant carry/digit-carry
conditions, so that it becomes valid packed BCD.

Example idea:

``` text
  29
+ 01
----
  2A
```

`2A` is not valid packed BCD because `A` is not a decimal digit.

A decimal adjustment converts the result into a valid BCD
representation.

------------------------------------------------------------------------

# 22. Bit Manipulation

The notes mention:

-   `BSF`
-   `BCF`
-   `BTG`

## BSF --- Bit Set File

Sets a specified bit to `1`.

Example:

``` asm
BSF PORTB,0
```

Conceptually:

``` text
PORTB bit 0 ← 1
```

## BCF --- Bit Clear File

Clears a specified bit to `0`.

``` asm
BCF PORTB,0
```

Conceptually:

``` text
PORTB bit 0 ← 0
```

## BTG --- Bit Toggle

Toggles a bit:

``` text
0 → 1
1 → 0
```

Example:

``` asm
BTG PORTB,0
```

This is useful for generating a square-wave-like output.

------------------------------------------------------------------------

# 23. Logical Instructions

The notes include:

-   `ANDWF`
-   `IORWF` / OR operation
-   `XORWF`
-   `COMF`

## AND

A bitwise AND keeps a bit as 1 only if both corresponding input bits are
1.

``` text
  1010
AND 1100
--------
  1000
```

## OR

A bitwise OR gives 1 if either corresponding bit is 1.

``` text
  1010
OR  1100
--------
  1110
```

## XOR

XOR gives 1 when the two corresponding bits are different.

``` text
  1010
XOR 1100
--------
  0110
```

## Complement

Complement flips every bit:

``` text
1010 → 0101
```

------------------------------------------------------------------------

# 24. Increment and Decrement

## INCF

Increment a file-register value by one.

``` text
x ← x + 1
```

## DECF

Decrement a file-register value by one.

``` text
x ← x - 1
```

These are especially useful for counters and loops.

------------------------------------------------------------------------

# 25. DECFSZ and Loop Programming

The notes emphasize `DECFSZ`.

Meaning:

**Decrement File, Skip if Zero**

Conceptually:

``` text
file ← file - 1

if file == 0:
    skip next instruction
else:
    execute next instruction
```

This makes it extremely useful for loops.

Example:

``` asm
COUNT EQU 0x25

MOVLW 0x0A
MOVWF COUNT

LOOP:
    ; body of loop
    DECFSZ COUNT,F
    GOTO LOOP
```

### What happens?

If COUNT starts at 10:

``` text
10 → 9 → 8 → ... → 2 → 1 → 0
```

When it becomes zero, `DECFSZ` skips the `GOTO LOOP`, so execution
continues after the loop.

------------------------------------------------------------------------

# 26. BNZ and Conditional Branching

The notes mention:

**BNZ --- Branch if Not Zero**

A conditional branch changes program flow depending on a condition.

Conceptually:

``` text
if result != 0:
    branch to target
```

The notes also mention conditional/unconditional control:

### Conditional

Examples include branches based on:

-   Zero
-   Carry
-   Other processor conditions

### Unconditional

`GOTO` transfers control to a specified label unconditionally.

------------------------------------------------------------------------

# 27. CALL and RETURN

A **subroutine** is a reusable block of code.

The notes describe `CALL` as a control-transfer instruction used to call
a subroutine.

Typical flow:

``` text
Main program
     |
     | CALL DELAY
     v
+-----------+
| DELAY     |
| ...       |
| RETURN    |
+-----------+
     |
     v
Continue main program
```

## CALL

Transfers execution to the subroutine and preserves the return address
using the processor's call/return mechanism.

## RETURN

Returns execution to the instruction after the call.

This is useful for:

-   Delay routines
-   Repeated calculations
-   Peripheral initialization
-   Communication routines

------------------------------------------------------------------------

# 28. Delay Subroutines

A delay routine intentionally consumes processor time.

A common method is a nested loop:

``` asm
OUTER:
    load inner counter

INNER:
    decrement inner counter
    branch until zero

    decrement outer counter
    branch until zero

    return
```

The notes repeatedly use delay subroutines for I/O examples.

### Important limitation

A software delay is not automatically an exact time delay.

The actual delay depends on:

-   Clock frequency
-   Instruction-cycle timing
-   Number of instructions
-   Branch/skip timing
-   Compiler/assembler behavior where relevant

For accurate timing, hardware timers are generally preferable.

------------------------------------------------------------------------

# 29. Pipelining

The notes compare pipelined and non-pipelined instruction processing.

A simplified pipeline can overlap stages such as:

``` text
Fetch → Decode → Execute
```

For multiple instructions:

``` text
Cycle 1: Fetch I1
Cycle 2: Decode I1 + Fetch I2
Cycle 3: Execute I1 + Decode I2 + Fetch I3
```

This improves throughput.

## Why branches affect pipelines

A branch changes the next instruction address.

Therefore, an instruction that was fetched speculatively/early may no
longer be the correct next instruction.

This can introduce a pipeline penalty.

------------------------------------------------------------------------

# 30. Instruction Cycle and Clock

A microcontroller executes instructions based on a clock generated from
the oscillator.

The notes discuss relationships between:

-   Crystal/oscillator frequency
-   Instruction cycle
-   Timer clock
-   Prescaler

For the PIC family discussed in the notes, instruction timing depends on
the architecture and selected oscillator configuration.

### Example concept

If an architecture uses an instruction cycle derived from the oscillator
by a fixed division, then:

``` text
Instruction-cycle frequency
= Oscillator frequency / division factor
```

and:

``` text
Instruction-cycle period
= 1 / instruction-cycle frequency
```

Always use the exact division specified by the particular PIC datasheet.

------------------------------------------------------------------------

# 31. I/O Ports

I/O ports allow the microcontroller to communicate with the external
world.

A port can be configured as:

-   Input
-   Output

Examples in the notes include:

-   PORTB
-   PORTC
-   Other port registers

## TRIS registers

The notes use TRIS registers for direction control.

The fundamental idea is:

``` text
TRIS bit → determines input/output direction
```

For the common PIC convention used in the notes:

``` text
TRIS bit = 1 → Input
TRIS bit = 0 → Output
```

Thus:

``` asm
TRISB = 0
```

configures PORTB as output in the C examples.

------------------------------------------------------------------------

# 32. PORT and Latch Concepts

The notes include a hardware diagram involving:

-   Data latch
-   TRIS latch
-   I/O pin
-   Read path
-   Output driver
-   Input path

This is important because an I/O port is not simply a wire connected to
a CPU register.

Conceptually:

``` text
CPU
 |
 | write
 v
Output Latch → Output Driver → Pin
                              |
                              v
                         External world
                              |
                              v
                         Input path
```

The direction-control circuitry determines whether the pin behaves as an
input or output.

------------------------------------------------------------------------

# 33. Port Multiplexing

The notes mention that PIC ports can be **multiplexed** with alternate
peripheral functions.

A physical pin may be capable of serving different functions, such as:

-   Digital I/O
-   Timer input/output
-   Serial communication
-   Other peripheral functions

Therefore, configuring a pin often requires more than simply setting its
direction.

You may also need to configure the peripheral or analog/digital function
associated with that pin.

------------------------------------------------------------------------

# 34. Port Bit Addressability

The notes mention bit-oriented instructions such as:

``` asm
BSF
BCF
BTG
```

These allow individual bits of registers to be controlled without
manually constructing a complete byte.

Example:

``` asm
BCF PORTB, 2
```

means:

``` text
PORTB bit 2 = 0
```

This is extremely useful for LEDs, control signals, enable lines, and
digital interfaces.

------------------------------------------------------------------------

# 35. Addressing Modes

The notes list four PIC18 addressing modes:

1.  Immediate
2.  Register indirect
3.  Indexed
4.  Direct

------------------------------------------------------------------------

## 35.1 Immediate addressing

The operand is a literal constant contained in the instruction.

Example:

``` asm
MOVLW 0x25
```

The CPU uses `0x25` directly.

Think:

> "Use this number itself."

------------------------------------------------------------------------

## 35.2 Direct addressing

The instruction directly specifies the address of the data/register
being accessed.

Example concept:

``` asm
MOVWF 0x20
```

Think:

> "Access location 0x20."

------------------------------------------------------------------------

## 35.3 Register indirect addressing

A register contains the address of the actual data.

Think of it as a pointer:

``` text
FSR → address
       ↓
     RAM data
```

The notes identify FSR registers as being used for this purpose.

This is useful when processing arrays, buffers, or sequences of memory
locations.

------------------------------------------------------------------------

# 36. FSR and INDF

The notes mention:

-   FSR0
-   FSR1
-   FSR2
-   INDF

### FSR

FSR means:

**File Select Register**

It is used as a pointer into data memory.

Conceptually:

``` text
FSR = 0x40

INDF → contents of RAM[0x40]
```

If FSR changes:

``` text
FSR = 0x41
```

then the indirect access refers to the new location.

This makes sequential memory operations easier.

------------------------------------------------------------------------

# 37. Indexed Addressing

Indexed addressing uses an index/offset mechanism to access data
relative to a base address.

It is useful for:

-   Arrays
-   Tables
-   Buffers
-   Lookup operations

Beginner analogy:

``` text
Base address + index = target element
```

For an array:

``` text
array[0]
array[1]
array[2]
array[3]
```

the index selects the desired element.

------------------------------------------------------------------------

# 38. Indirect ROM / Program-Memory Access

The notes describe indexed/indirect access to program-memory data.

This can be useful for lookup tables.

Example applications:

-   Seven-segment display codes
-   Character tables
-   Sine/cosine tables
-   Calibration constants

The general idea is:

``` text
Index → lookup table → required constant
```

------------------------------------------------------------------------

# 39. Checksum and Data Integrity

The notes include a checksum problem.

A **checksum** is a value calculated from a block of data and used to
detect corruption.

A simple checksum may be formed from the sum of bytes, sometimes with a
complement operation.

General process:

``` text
Data bytes
   ↓
Arithmetic operation
   ↓
Checksum
```

At the receiver:

``` text
Received data
   ↓
Recalculate checksum
   ↓
Compare
   ↓
Match → probably valid
Mismatch → error detected
```

### Important limitation

A simple checksum is an error-detection mechanism, not a guarantee of
correctness.

Some error patterns can cancel each other out.

------------------------------------------------------------------------

# 40. Macros

The notes devote a section to **macros and modules**.

A macro is a named block of assembly source that can be expanded
wherever the macro is invoked.

Example concept:

``` asm
MACRO_NAME MACRO
    instruction 1
    instruction 2
    instruction 3
ENDM
```

Then:

``` asm
MACRO_NAME
```

causes the assembler to insert the macro's body.

## Why use macros?

Macros can:

-   Reduce repetitive source code
-   Improve readability
-   Make repeated instruction sequences easier to maintain
-   Reduce typing
-   Standardize common operations

### Macro vs subroutine

This distinction is important.

**Macro:** - Expanded during assembly - Usually increases code size when
used repeatedly - No runtime CALL/RETURN required

**Subroutine:** - Stored once - Called at runtime - Saves code space
when the same routine is reused many times - Has CALL/RETURN overhead

------------------------------------------------------------------------

# 41. Modules

A module is a logically separated piece of a larger program.

The notes mention advantages such as:

-   A module can be developed/debugged/tested independently.
-   It can make program organization easier.
-   It can be linked with other modules.
-   It can support integration with higher-level languages such as C.

A modular design is especially useful for larger embedded projects.

------------------------------------------------------------------------

# 42. C Programming for PIC

The notes include C examples using:

``` c
#include <...>
void main(void)
```

and register operations such as:

``` c
TRISB = 0;
PORTB = 0x55;
```

The important idea is that C can provide a more readable way of
controlling microcontroller registers than raw assembly.

------------------------------------------------------------------------

# 43. C Data Types and Embedded Programming

The notes mention basic data types such as:

-   `char`
-   `int`
-   `long`

The exact size and range can depend on the compiler and target
architecture.

For embedded programming, always check the compiler's device-specific
documentation before assuming a type is a particular number of bits.

------------------------------------------------------------------------

# 44. Simple Port-Output Program

A typical conceptual C program is:

``` c
TRISB = 0;

while (1)
{
    PORTB = 0x55;
    delay();
    PORTB = 0xAA;
    delay();
}
```

What does this do?

1.  Configure PORTB as output.
2.  Put `0x55` on PORTB.
3.  Wait.
4.  Put `0xAA` on PORTB.
5.  Wait.
6.  Repeat forever.

Binary:

``` text
0x55 = 0101 0101
0xAA = 1010 1010
```

So the output pattern alternates.

------------------------------------------------------------------------

# 45. Toggle Programming

The notes contain a program that repeatedly changes PORTB between values
such as:

``` text
0x55
0xAA
```

This creates alternating bit patterns.

A toggle can also be achieved by toggling individual bits.

For a single output:

``` text
0 → 1 → 0 → 1 → ...
```

The output frequency depends on the total time taken by the program
loop.

------------------------------------------------------------------------

# 46. Timers

Timers are one of the most important peripheral concepts in the notes.

A timer is essentially a counter driven by a clock.

It can be used to:

-   Generate delays
-   Measure time
-   Count external events
-   Generate periodic events
-   Support waveform generation

The notes discuss multiple timers and timer registers.

------------------------------------------------------------------------

# 47. Timer Clock Source

A timer needs a clock/input event to count.

Possible sources include:

1.  Internal instruction-cycle clock
2.  External clock signal

The notes specifically discuss selecting an external clock so the timer
can act as a counter.

Conceptually:

``` text
Internal clock → Timer → count
External pin   → Timer → count
```

------------------------------------------------------------------------

# 48. Timer Control Register

The notes show a timer control register with fields including concepts
such as:

-   Timer enable
-   Timer/counter mode
-   Prescaler selection
-   Clock-source selection
-   Edge selection

The exact bit positions depend on the particular timer and PIC device.

------------------------------------------------------------------------

# 49. Timer ON/OFF

A timer control bit determines whether the timer is enabled.

Conceptually:

``` text
Timer ON  → counter operates
Timer OFF → counter stopped
```

------------------------------------------------------------------------

# 50. Timer Mode vs Counter Mode

This distinction is frequently tested.

## Timer mode

The timer counts internal clock events.

``` text
Internal clock
      ↓
    Timer
      ↓
   count/time
```

## Counter mode

The peripheral counts transitions/events arriving from an external
source.

``` text
External pulses
      ↓
    Timer
      ↓
 event count
```

So:

**Timer → measure elapsed time**

**Counter → count external events**

The same hardware may support both modes.

------------------------------------------------------------------------

# 51. Timer Prescaler

A prescaler divides the incoming timer clock before it reaches the timer
counter.

Example:

``` text
Input clock
    ↓
÷ 2
    ↓
Timer counter
```

If the incoming clock is 1 MHz and the prescaler is 2:

``` text
Timer clock = 1 MHz / 2
            = 500 kHz
```

The timer therefore increments more slowly.

The notes mention possible prescaler ratios such as:

``` text
1:1, 1:2, 1:4, 1:8, ...
```

The exact options depend on the timer.

------------------------------------------------------------------------

# 52. Timer Resolution

Timer resolution refers to the smallest time increment represented by
one timer count.

If:

``` text
timer clock = 1 MHz
```

then one count takes:

``` text
1 / 1 MHz = 1 µs
```

If a prescaler divides by 8:

``` text
timer clock = 125 kHz
```

and one count takes:

``` text
8 µs
```

Thus:

**Larger prescaler → slower counting → larger time step → longer maximum
interval for a fixed counter width.**

------------------------------------------------------------------------

# 53. Timer Overflow

Suppose a timer has an N-bit counter.

It can represent:

``` text
0 to 2^N - 1
```

After the maximum value, the next increment causes rollover/overflow.

For an 8-bit timer:

``` text
0 → 1 → ... → 254 → 255 → 0
```

Overflow can be used to generate periodic timing events.

------------------------------------------------------------------------

# 54. Timer Calculation

A generic timer calculation is:

``` text
Timer tick period
    = 1 / timer clock frequency

Required counts
    ≈ required delay / timer tick period
```

If a timer has a prescaler:

``` text
timer clock
    = source clock / prescaler
```

For an N-bit timer, the number of counts before overflow is related to:

``` text
2^N
```

For a preload value `P`, the number of increments to overflow is
approximately:

``` text
2^N - P
```

Use the exact timer architecture and overflow behavior from the target
PIC datasheet for precise calculations.

------------------------------------------------------------------------

# 55. Software Delay vs Hardware Timer

## Software delay

Uses CPU instructions:

``` text
loop
loop
loop
...
```

Advantages:

-   Simple
-   No timer configuration required

Disadvantages:

-   Consumes CPU time
-   Timing depends on instruction execution
-   Harder to make highly accurate
-   CPU cannot efficiently perform other work during the delay

## Hardware timer

Uses a peripheral:

``` text
Clock → Timer → overflow/event
```

Advantages:

-   More accurate and deterministic
-   CPU can perform other work
-   Useful for periodic interrupts/events

This distinction is important in embedded-system design.

------------------------------------------------------------------------

# 56. Serial Communication

The final portion of the notes covers **asynchronous serial
communication and data framing**.

The notes distinguish:

-   Asynchronous serial transmission
-   Synchronous serial transmission

------------------------------------------------------------------------

# 57. Asynchronous Serial Communication

In asynchronous serial communication, the sender and receiver do not
continuously share a separate clock line.

Instead, both sides agree on communication parameters such as:

-   Baud rate
-   Number of data bits
-   Parity configuration if used
-   Number of stop bits

A typical frame contains:

``` text
Idle | Start | Data bits | Optional parity | Stop
```

The notes illustrate a start bit and data bits in a serial waveform.

------------------------------------------------------------------------

# 58. Start and Stop Bits

For an asynchronous serial frame:

``` text
Idle → Start → Data → Stop → Idle
```

The **start bit** indicates the beginning of a character/frame.

The **stop bit** indicates the end.

This allows the receiver to synchronize to the incoming character even
without a continuously shared clock.

------------------------------------------------------------------------

# 59. Baud Rate

Baud rate describes the number of signaling symbols transmitted per
second.

For common simple serial links where one symbol represents one bit:

``` text
baud rate ≈ bits per second
```

The notes use **9600 baud** as an example.

At 9600 bits/s, ignoring framing overhead:

``` text
1 bit time = 1 / 9600 seconds
```

A complete character takes longer because it includes start/stop and
possibly parity bits.

------------------------------------------------------------------------

# 60. RS-232

The notes discuss **RS-232** and identify it as a serial communication
standard/interface.

Important beginner point:

**RS-232 is not the same thing as UART logic-level signaling.**

A UART peripheral may generate serial data at logic levels, while RS-232
defines electrical signaling that normally requires appropriate level
conversion.

The notes show a PIC connected through an RS-232 interface toward a
PC/terminal.

------------------------------------------------------------------------

# 61. DB-9 Connector

The notes mention a **DB-9** connector.

A DB-9 connector is a common physical connector used with RS-232
interfaces.

The connector's physical pins and signal assignments are distinct from
the logical UART concepts.

------------------------------------------------------------------------

# 62. DTE and DCE

RS-232 commonly uses the concepts:

-   **DTE --- Data Terminal Equipment**
-   **DCE --- Data Communications Equipment**

The notes show DTE/DCE relationships and signals such as:

-   TXD
-   RXD
-   RTS
-   CTS

A key idea is that transmit and receive signals must be connected
according to the roles of the devices.

------------------------------------------------------------------------

# 63. UART-Related PIC Registers

The notes list UART-related registers including concepts such as:

-   `SPBRG` --- baud-rate generation
-   `RCREG` --- receive register
-   `TXREG` --- transmit register
-   `TXSTA` --- transmit status/control
-   `RCSTA` --- receive status/control

Exact names and features vary by PIC family, but these are common
concepts in PIC USART/UART peripherals.

------------------------------------------------------------------------

# 64. Transmitting Serial Data

The notes give an assembly-style transmission sequence.

The general process is:

1.  Configure the serial port.
2.  Configure the baud-rate generator.
3.  Configure transmitter settings.
4.  Put data in the transmit register.
5.  Wait until transmission is ready/complete as required.
6.  Send the next character.

Conceptually:

``` text
CPU
 ↓
TXREG
 ↓
UART transmitter
 ↓
TX pin
 ↓
RS-232/level converter
 ↓
PC
```

------------------------------------------------------------------------

# 65. Receiving Serial Data

For reception:

``` text
PC / external device
        ↓
      RX pin
        ↓
UART receiver
        ↓
Receive register
        ↓
CPU
```

The receiver detects the serial frame and reconstructs the received
byte.

The program can then read the receive register.

------------------------------------------------------------------------

# 66. USART

USART means:

**Universal Synchronous/Asynchronous Receiver/Transmitter**

It can support serial communication in appropriate synchronous or
asynchronous modes depending on the device.

The notes emphasize asynchronous operation for PIC serial communication.

------------------------------------------------------------------------

# 67. Data Framing Example

A common asynchronous frame may conceptually look like:

``` text
Idle  Start  D0 D1 D2 D3 D4 D5 D6 D7  Stop
 1      0     data bits                 1
```

The exact convention depends on the serial configuration.

A receiver uses the start transition to determine when to sample the
incoming data bits.

------------------------------------------------------------------------

# 68. Common PIC Programming Pattern

A large fraction of beginner PIC programs can be understood as:

``` text
1. Configure hardware
2. Configure I/O direction
3. Initialize peripheral
4. Load data
5. Perform operation
6. Check condition/status
7. Repeat or branch
```

For example:

``` asm
        ; initialization

        MOVLW ...
        MOVWF ...

LOOP:
        ; operation
        ...
        DECFSZ COUNT,F
        GOTO LOOP

        ; continue
```

Once you understand the flow, individual instructions become much easier
to learn.

------------------------------------------------------------------------

# 69. How to Read PIC Assembly

When you see an assembly program, read it in this order:

### Step 1 --- Find labels

Labels define important destinations.

### Step 2 --- Find initialization

Look for:

-   TRIS configuration
-   Timer configuration
-   UART configuration
-   Counter initialization

### Step 3 --- Track WREG

Whenever you see:

``` asm
MOVLW
MOVWF
ADDWF
SUBWF
```

ask:

> What is currently inside WREG?

### Step 4 --- Track file registers

Make a small table:

  Register     Current value
  ---------- ---------------
  COUNT                   10
  TEMP                  0x55
  WREG                  0x25

### Step 5 --- Follow branches

For:

``` asm
GOTO LOOP
```

jump to `LOOP`.

For:

``` asm
DECFSZ COUNT,F
GOTO LOOP
```

remember the skip behavior.

------------------------------------------------------------------------

# 70. Beginner Worked Example: Add a Constant Repeatedly

Suppose the task is:

> Add value 3 to WREG repeatedly until a counter reaches zero.

A conceptual structure is:

``` asm
COUNT EQU 0x25

MOVLW 0
MOVWF COUNT

LOOP:
    MOVLW 3
    ; perform addition
    ; update counter
    DECFSZ COUNT,F
    GOTO LOOP
```

The important concepts are:

-   Symbolic constants
-   WREG
-   File registers
-   Arithmetic
-   Loop control
-   `DECFSZ`

------------------------------------------------------------------------

# 71. Beginner Worked Example: Send Alternating Patterns

Suppose PORTB is connected to LEDs.

``` c
TRISB = 0;

while (1)
{
    PORTB = 0x55;
    delay();
    PORTB = 0xAA;
    delay();
}
```

Binary patterns:

``` text
0x55 = 01010101
0xAA = 10101010
```

The LEDs therefore alternate between two complementary patterns.

This combines:

-   I/O direction
-   Output registers
-   Binary/hexadecimal conversion
-   Delay
-   Infinite loops

------------------------------------------------------------------------

# 72. Beginner Worked Example: Toggle One Bit

Suppose bit 0 controls an LED.

Conceptually:

``` asm
LOOP:
    BTG PORTB,0
    CALL DELAY
    GOTO LOOP
```

The output becomes:

``` text
0 → 1 → 0 → 1 → ...
```

The resulting frequency is determined by the execution time of the loop
and delay routine.

------------------------------------------------------------------------

# 73. Binary and Hexadecimal Skills

PIC programming frequently uses hexadecimal.

Important conversions:

``` text
0x00 = 0000 0000
0x55 = 0101 0101
0xAA = 1010 1010
0xFF = 1111 1111
```

Each hexadecimal digit represents exactly four binary bits.

For example:

``` text
0x3F
```

becomes:

``` text
3 = 0011
F = 1111

0x3F = 0011 1111
```

Being comfortable with hex/binary conversion is essential for
understanding register values.

------------------------------------------------------------------------

# 74. Common Exam Traps

## Trap 1: Carry vs overflow

**Carry** is associated primarily with unsigned arithmetic.

**Overflow** is associated with signed arithmetic.

## Trap 2: Timer vs counter

Timer → internal clock/time base.

Counter → external events.

## Trap 3: Macro vs subroutine

Macro → assembly-time expansion.

Subroutine → runtime CALL/RETURN.

## Trap 4: Immediate vs direct addressing

Immediate:

``` text
value itself
```

Direct:

``` text
address of value
```

## Trap 5: BSF vs BCF

BSF → set bit to 1.

BCF → clear bit to 0.

## Trap 6: DECFSZ

It decrements first, then skips the next instruction if the result is
zero.

## Trap 7: TRIS

For the convention shown in the notes:

``` text
1 → input
0 → output
```

------------------------------------------------------------------------

# 75. High-Yield Revision Sheet

## Architecture

-   PIC is a microcontroller family.
-   RISC = Reduced Instruction Set Computer.
-   Harvard architecture separates program and data memory.
-   CPU contains/works with ALU, WREG, PC, stack mechanism, etc.
-   Program memory stores instructions.
-   RAM/data memory stores working data.
-   Flash is non-volatile and reprogrammable.
-   OTP means one-time programmable.

## Assembly

-   `MOVLW` → literal to WREG.
-   `MOVWF` → WREG to file register.
-   `MOVFF` → file register to file register.
-   `ADDWF` → addition involving WREG and file register.
-   `SUBLW` → literal minus WREG.
-   `BSF` → set bit.
-   `BCF` → clear bit.
-   `BTG` → toggle bit.
-   `INCF` → increment.
-   `DECF` → decrement.
-   `DECFSZ` → decrement and skip if zero.
-   `GOTO` → unconditional branch.
-   `CALL` → call subroutine.
-   `RETURN` → return from subroutine.

## Flags

-   `C` → carry.
-   `DC` → digit carry.
-   `Z` → zero.
-   `OV` → signed overflow.
-   `N` → negative/sign indication.

## Directives

-   `EQU` → define symbolic constant.
-   `SET` → assign/reassign assembler symbol.
-   `ORG` → set assembly origin.
-   `END` → end source.
-   `LIST` → listing/assembler configuration.

## Addressing

-   Immediate
-   Direct
-   Register indirect
-   Indexed

## I/O

-   TRIS controls direction.
-   `TRIS bit = 1` → input in the convention used by the notes.
-   `TRIS bit = 0` → output.
-   Ports may have alternate peripheral functions.

## Timers

-   Internal clock → timer/time base.
-   External events → counter mode.
-   Prescaler divides input frequency.
-   Overflow occurs after the counter rolls over.
-   Hardware timers are preferable to busy-wait delays for accurate
    periodic timing.

## Serial

-   Asynchronous communication uses framing.
-   Start and stop bits help identify a character.
-   Baud rate defines signaling speed.
-   RS-232 is an electrical/interface standard, not merely the UART data
    format.
-   UART/USART peripherals provide serial transmit/receive
    functionality.
-   Common registers include baud-rate, transmit, receive, and
    status/control registers.

------------------------------------------------------------------------

# 76. Final Mental Model

If you are completely new to PIC programming, build your understanding
in this order:

``` text
Microcontroller
      ↓
CPU + Memory + Peripherals
      ↓
Harvard + RISC architecture
      ↓
WREG + File Registers
      ↓
Assembly instructions
      ↓
Status flags
      ↓
Branches + Loops + Subroutines
      ↓
I/O ports + TRIS
      ↓
Timers + Prescalers
      ↓
Serial communication
      ↓
Complete embedded application
```

Do not try to memorize every instruction first.

Instead, understand the **data flow**:

``` text
Literal / Input
      ↓
    WREG
      ↓
File register / ALU
      ↓
Status flags
      ↓
Branch decision
      ↓
I/O / Timer / UART
```

That mental model makes most of the handwritten examples much easier to
decode.

------------------------------------------------------------------------

## Source mapping to the uploaded notes

The uploaded pages cover these themes progressively:

-   **Pages 1--4:** microcontrollers, 8051/PIC background, PIC
    architecture, memory organization, RISC and instruction-cycle
    concepts.
-   **Pages 5--7:** PIC registers, status flags, arithmetic/logic
    operations, instruction examples.
-   **Pages 8--13:** PIC instruction format, assembler/compiler/MPLAB
    concepts, loops, branches, calls, stack.
-   **Pages 14--17:** instruction cycles, pipelining, I/O ports, port
    latches, bit-addressable operations.
-   **Pages 18--20:** arithmetic, BCD adjustment, subtraction,
    comparison, rotate operations.
-   **Pages 21--24:** addressing modes, FSR/indirect addressing,
    program-memory access, checksum, macros/modules.
-   **Pages 25--32:** PIC C programming, I/O examples, software delays,
    hardware timers, timer control.
-   **Pages 33--37:** serial communication, asynchronous framing,
    RS-232, UART/USART registers, transmission examples.
-   **Page 38:** repeated PIC assembly examples involving counters,
    PORTB, `DECFSZ`, and `BNZ`.
