# Microcontrollers and Embedded Systems — Complete Study Notes
### (8051 Overview + Detailed PIC18 Microcontroller Guide)

> These notes are written to be readable by a complete beginner. Every technical term is explained the first time it's used, and worked examples are included wherever the original notes had one.

---

## Table of Contents

1. [What Is a Microcontroller?](#1-what-is-a-microcontroller)
2. [The 8051 Microcontroller](#2-the-8051-microcontroller)
3. [Introduction to PIC Microcontrollers](#3-introduction-to-pic-microcontrollers)
4. [Choosing a Microcontroller](#4-choosing-a-microcontroller)
5. [Memory Technologies: EPROM, OTP, Flash, Mask ROM](#5-memory-technologies-eprom-otp-flash-mask-rom)
6. [PIC Internal Architecture](#6-pic-internal-architecture)
7. [Registers: WREG, Status Register, Program Counter](#7-registers-wreg-status-register-program-counter)
8. [RISC Design and Pipelining](#8-risc-design-and-pipelining)
9. [PIC File Types and Popular Chips](#9-pic-file-types-and-popular-chips)
10. [Assembler Directives](#10-assembler-directives)
11. [Structure of a PIC Assembly Program (ALP)](#11-structure-of-a-pic-assembly-program-alp)
12. [The GPR / SFR File Register and Data Movement](#12-the-gpr--sfr-file-register-and-data-movement)
13. [Looping and Branching](#13-looping-and-branching)
14. [Subroutines: CALL, RCALL, and the Stack](#14-subroutines-call-rcall-and-the-stack)
15. [I/O Ports: TRIS, LAT, PORT](#15-io-ports-tris-lat-port)
16. [Instruction Cycle and Timing](#16-instruction-cycle-and-timing)
17. [Arithmetic Instructions and Flags](#17-arithmetic-instructions-and-flags)
18. [Decimal Adjust (DAW) for BCD Math](#18-decimal-adjust-daw-for-bcd-math)
19. [Subtraction Instructions](#19-subtraction-instructions)
20. [Compare and Rotate Instructions](#20-compare-and-rotate-instructions)
21. [Addressing Modes](#21-addressing-modes)
22. [Assembly vs. C: Why Use C?](#22-assembly-vs-c-why-use-c)
23. [Checksum Bytes](#23-checksum-bytes)
24. [Macros and Modules](#24-macros-and-modules)
25. [C Programming for PIC18 (C18 Compiler)](#25-c-programming-for-pic18-c18-compiler)
26. [Timers](#26-timers)
27. [Serial Communication Basics](#27-serial-communication-basics)
28. [Asynchronous Serial Communication and Framing](#28-asynchronous-serial-communication-and-framing)
29. [RS-232 and the MAX232 Chip](#29-rs-232-and-the-max232-chip)
30. [USART Registers and a Full Serial-Transmit Program](#30-usart-registers-and-a-full-serial-transmit-program)

---

## 1. What Is a Microcontroller?

A **microcontroller** is a small computer built onto a single chip. Unlike a general-purpose **microprocessor** (like the CPU in a laptop, which needs separate RAM, ROM, and I/O chips around it), a microcontroller already has a CPU, memory (RAM + ROM), and input/output circuitry all built in. This makes it cheap, compact, and ideal for dedicated jobs — running a washing machine, a microwave, a car's dashboard, a toy, etc.

An **embedded system** is any computer system that is built into (embedded in) a larger device to do one specific job, as opposed to a general-purpose computer that runs many different programs. Microcontrollers are the "brains" of most embedded systems.

**Addressing mode** — a term used constantly in this subject — simply means *the way an instruction specifies where its data (operand) comes from*. For example, "the number 5" is different from "the number stored at memory location 5" — these are two different addressing modes, explained fully in [Section 21](#21-addressing-modes).

---

## 2. The 8051 Microcontroller

The 8051 is the microcontroller that historically started this whole field and is still taught first in most courses because it's simple.

- **8051** = an **8-bit microcontroller**, meaning its CPU processes data 8 bits (1 byte) at a time.
- Originally made by **Intel**. Related chips in the same family: **8051, 8031, 8096**.
- Other companies made similar 8-bit microcontrollers too, e.g., **Motorola's 68HC11 family**.

### What's inside an 8051?
| Feature | Specification |
|---|---|
| CPU | 8-bit |
| On-chip program memory (ROM) | 4 KB |
| On-chip data RAM | 128 bytes |
| Timers | Two 16-bit timers |
| I/O Ports | Four 8-bit I/O ports |
| Serial Port | Full-duplex (can send and receive at the same time) |
| Clock | On-chip clock oscillator circuit |

### Memory Organization: Harvard Architecture
The 8051 (and PIC, as we'll see) uses **Harvard architecture**, which means the **program memory** (where instructions live) and the **data memory** (where variables live) are completely separate, with their own separate buses (wires) connecting them to the CPU. This is different from a **Von Neumann architecture**, where program and data share one memory and one bus.

*Why does this matter?* Because the CPU can fetch an instruction and read/write data **at the same time** in Harvard architecture, since they use different pathways — making it faster.

**Recommended textbooks (from the notes):**
- *"The 8051 Microcontroller and Embedded Systems"* — M. Mazidi
- D. Causey (co-author on related texts)
- SP Das lecture series — available on NPTEL

---

## 3. Introduction to PIC Microcontrollers

- **PIC** = **P**eripheral **I**nterface **C**ontroller.
- Introduced around **1989–1993** by **Microchip Technology**, initially as an 8-bit microcontroller family.
- PIC controllers are based on **RISC architecture** (explained in [Section 8](#8-risc-design-and-pipelining)).

### Quick specs (typical PIC family range)
| Feature | Typical range |
|---|---|
| ROM (program memory) | up to ~2 MB (varies hugely by chip) |
| RAM (data memory) | 256 bytes to 4096 bytes |
| Built-in peripherals | Data EEPROM, Timers, ADC (Analog-to-Digital Converter), USART, SPI (for PC/peripheral communication) |
| I/O pins | 16 to 72 pins depending on the chip |

### PIC18's Five Timers
PIC18 devices typically provide **5 timers**, labeled **Timer0, Timer1, Timer2, Timer3, Timer4**:
- Timers **0, 1, 3** → can operate in **8-bit** mode.
- Timers **2, 4** → **16-bit** timers.

*(Note: This is a general pattern seen across PIC18 parts; exact timer widths can differ slightly by specific chip model — the numbers above match what's commonly taught for this course.)*

### Development Tool: MPLAB IDE
**MPLAB IDE** is the free software from Microchip Technology (first released around 1993 alongside PIC) that bundles everything you need to write PIC programs in one package:
- A **text editor** (to type code)
- An **assembler** (converts assembly code to machine code)
- A **linker**
- A **simulator** (to test code without real hardware)

Some very old workflows used plain **Notepad** or **MS-DOS Edit** as the text editor before pasting code into the assembler separately — but MPLAB does it all in one place.

### A/D Converter Control
PIC's built-in Analog-to-Digital Converter is controlled through two special registers:
- **ADCON0**
- **ADCON1**

An on-chip **oscillator** generates the timing/clock pulses the whole chip runs on.

---

## 4. Choosing a Microcontroller

When an engineer picks a microcontroller for a project, they weigh several criteria:

1. **Can it handle the computational task effectively and efficiently?**
   - a) **Speed** — how fast can it execute instructions?
   - b) **Power consumption** — important for battery-powered devices.
   - c) **Amount of RAM/ROM** — enough memory for the program and variables?
   - d) **Number of I/O pins** — enough pins to connect all sensors/actuators?
   - e) **Cost per unit** — critical when making thousands/millions of units.

2. **How easy is it to develop a product around it?**
   - Availability of a good **compiler**, **debugger**, and **emulator** (tools that let you write, test, and troubleshoot code).

3. **Adaptability and compatibility** with other chips/peripherals in the design.

### PIC Part-Number Naming Convention
PIC part numbers often hint at the pin count, e.g., parts named like `10xxx`, `12xxx`, `14xxx`, `16xxx`, `17xxx`, `18xxx` roughly correspond to the PIC **family/generation** (PIC10, PIC12, PIC14, PIC16, PIC17, PIC18) — with PIC18 being a more powerful, later generation than PIC16.

### A related field: Mechatronics
**Mechatronics** combines mechanical engineering, electronics, and computer control. A related concept is **MEMS** (**M**icro **E**lectrical **M**echanical **S**ystems) — tiny mechanical devices (like accelerometer sensors) built using chip-fabrication techniques.

---

## 5. Memory Technologies: EPROM, OTP, Flash, Mask ROM

Microcontrollers store their program in non-volatile memory (memory that keeps its contents even when power is off). There are several kinds, differing in how they're written and how many times they can be rewritten:

| Type | Description |
|---|---|
| **UV-EPROM** | Erasable Programmable ROM — erased by exposing the chip (through a small quartz window) to ultraviolet light, then reprogrammed. Reusable, but slow/inconvenient to erase. |
| **OTP (One-Time Programmable)** | Can be programmed exactly once. Cheaper than UV-EPROM because it skips the erasing window. Example: **PIC16C74A** uses OTP EPROM. |
| **Flash** | Can be erased and reprogrammed electrically, many times, without UV light. Firmware is stored **permanently and effectively** until deliberately overwritten. Most modern PIC chips (e.g. **PIC16F877**, **PIC18F458**) use Flash. |
| **Mask ROM** | The program is "baked into" the chip permanently at the factory during manufacturing. This is the **cheapest** option, but only makes economic sense for extremely high production volumes (since a mistake means the whole batch has to be thrown away). |

### Example Chip Comparison (from the notes)

| Chip | Memory Type | Program Memory | Data Memory | I/O Ports | ADC |
|---|---|---|---|---|---|
| PIC16C74A | OTP EPROM | 4K EPROM | 32 bytes | 8 | 10-bit |
| PIC16F877 | Flash | 8K Flash | up to 4096 (varies by region) | 8 | 4 channels |

*(These figures are transcribed from classroom notes — always cross-check exact numbers against the official Microchip datasheet before using them in a real design.)*

### General PIC Clock/Package Facts
- Typical PIC controller clock speed: **20 MHz to 40 MHz**.
- Common package size: **40 pins**.
- Communication peripherals built in: **SPI** and **I²C** (both are protocols for chip-to-chip communication).

---

## 6. PIC Internal Architecture

### Block Diagram (conceptual)
A PIC microcontroller's internal blocks connect roughly like this:

```
 Program ROM ── Stack/PC ──┐
                            │
     Integrated  ── CPU ────┼── RAM
     Logic Control │        │
                   OSC     EEPROM
                    │        │
                 Timer     Ports ── Other peripheral devices
```

- **CPU** — the "brain" that fetches, decodes, and executes instructions.
- **OSC (Oscillator)** — generates the clock signal (like a metronome) that paces every operation.
- **Stack/PC (Program Counter)** — keeps track of which instruction runs next (see [Section 7](#7-registers-wreg-status-register-program-counter)).
- **Timer, Ports, EEPROM** — peripheral blocks the CPU can talk to.

### CPU-to-Memory Connections
```
Program Memory ⇄ (13-bit instruction bus) ⇄ CPU ⇄ (register address bus) ⇄ SFR / Data Memory (8-bit data bus)
```
This shows the Harvard architecture in action: a separate, wider bus carries **instructions** (13 bits wide in the baseline/mid-range PIC design shown in the notes) while a separate 8-bit bus carries **data**.

### Reset and Interrupt Vectors
When the chip powers on or resets, the CPU always jumps to a fixed, predefined address to start running code:
- **0000H (00H)** → **Reset vector** — execution starts here after power-on or reset.
- **0004H (04H)** → **Interrupt vector** — execution jumps here when an interrupt occurs (an interrupt is a signal that pauses normal program flow to handle something urgent, like a button press).

### PIC18 vs PIC16 Performance
The notes state that **PIC18 is roughly 1.5× better (faster/more capable) than PIC16** — a result of architectural improvements covered in [Section 8](#8-risc-design-and-pipelining).

### Related Chip Technologies (context)
- **FPGA (Field Programmable Gate Array)** — a chip whose internal digital logic can be reconfigured/rewired by the user, unlike a fixed microcontroller.
- **ASIC (Application Specific Integrated Circuit)** — a chip custom-designed and manufactured for one specific application; very efficient but expensive to design and impossible to change afterward.

---

## 7. Registers: WREG, Status Register, Program Counter

### The Working Register (WREG)
Think of **WREG** as the microcontroller's "scratchpad" or "calculator display." Almost every arithmetic/logic operation in PIC assembly involves WREG — data is loaded into WREG, operated on, and the result usually ends up back in WREG (or is sent to another location).

Basic instructions that use WREG:
```asm
MOVLW   K       ; Move Literal value K into WREG.  (WREG = K)
MOVLW   25H     ; WREG = 25H (a literal, i.e. a hard-coded constant)
ADDLW   28H     ; Add the literal 28H to WREG.  (WREG = WREG + 28H)
ADDLW   K       ; Add literal K to WREG. (WREG = WREG + K)
```

### The Status Register (Flags)
The **STATUS register** is an 8-bit register where individual bits ("flags") automatically record facts about the result of the last arithmetic/logic operation. The PIC18 STATUS register layout (from the detailed notes) is:

| Bit 7-5 | N | OV | Z | DC | C |
|---|---|---|---|---|---|
| unused | Negative | Overflow | Zero | Digital Carry | Carry |

Meaning of each flag:

- **C (Carry)** — Set to 1 when there is a carry **out of the most significant bit (bit 7)** during addition (or a borrow during subtraction).
- **DC (Digital Carry / half-carry)** — Set to 1 when there's a carry from bit 3 into bit 4 during addition/subtraction (i.e., a carry out of the lower nibble). This is essential for correcting BCD (Binary-Coded Decimal) math — see [Section 18](#18-decimal-adjust-daw-for-bcd-math).
- **Z (Zero)** — Set to 1 whenever the result of an ALU (Arithmetic Logic Unit) operation is exactly zero.
- **OV (Overflow)** — Set to 1 when the result of a **signed** arithmetic operation is too large to fit, causing the sign bit to be corrupted (e.g., adding two positive numbers and getting a result that looks negative).
- **N (Negative)** — Reflects the sign of the result: if bit 7 of the result is 0, the result is treated as positive (N = 0); if bit 7 is 1, the result is treated as negative (N = 1).

#### Worked Example
```asm
MOVLW   38H
ADDLW   2FH     ; Add 2FH to WREG
```
Doing the binary math:
```
  0011 1000   (38H)
+ 0010 1111   (2FH)
-----------
  0110 0111   (67H)
```
Result: **WREG = 67H**. Flags: **C = 0** (no carry out of bit 7), **DC = 1** (there was a carry from bit 3 into bit 4), **Z = 0** (result isn't zero).

#### Another Worked Example
```
  1001 1100   (9CH)
+ 0110 0100   (64H)
-----------
1 0000 0000   (100H → 8-bit result is 00H, with a carry out)
```
Flags here: **C = 1** (carry out of bit 7 — the result overflowed 8 bits), **DC = 1**, **Z = 1** (the 8-bit stored result is 00H, which is zero).

### The Program Counter (PC)
The **Program Counter** is a special register that always holds the address of the **next instruction to be executed**. After each instruction runs, the PC automatically increments to point to the following instruction (unless a jump/call instruction changes it directly).

- The **wider** the Program Counter (more bits), the **more memory locations** the CPU can address and therefore the larger a program it can run.
- **PIC16** family: **12-bit** Program Counter (or file registers sized around 4 KB in the mid-range family).
- **PIC18** family: **21-bit** Program Counter — able to address a much larger 2 MB program memory space (00000H – 1FFFFH shown in the notes for one specific example).

---

## 8. RISC Design and Pipelining

**RISC** stands for **R**educed **I**nstruction **S**et **C**omputer — a CPU design philosophy that uses a small set of simple instructions (each doing one simple thing), which lets the chip run each instruction very fast. This is the opposite of **CISC** (Complex Instruction Set Computer), which has many powerful but slower/more complex instructions.

PIC uses RISC-style architecture. According to the notes, three broad strategies improve microcontroller **speed**:

1. **Increase clock frequency** — but this also **increases power consumption**, so it's a trade-off.
2. **Use Harvard architecture with more system buses** — separate data and instruction pathways mean the CPU isn't waiting for one shared bus.
3. **Change the internal architecture** to use **pipelining / parallel processing** — this is how PIC18 grew its usable instruction set from roughly **21–35 instructions up to about 75 instructions** while staying fast.

### What Is Pipelining?
Normally (**non-pipelined**), the CPU does one full step at a time in sequence:
```
Fetch1 → Execute1 → Fetch2 → Execute2 → Fetch3 → Execute3
```
Each instruction has to completely finish before the next one even starts being fetched — wasteful, since the "fetch" circuitry sits idle during "execute" and vice versa.

With **pipelining**, the CPU overlaps these stages — while instruction 1 is executing, instruction 2 is already being fetched:
```
Fetch1 → Execute1
         Fetch2 → Execute2
                  Fetch3 → Execute3
                           Fetch4 → Execute4
```
This is like an assembly line: multiple instructions are "in flight" at different stages simultaneously, dramatically increasing throughput (instructions completed per second) without needing a faster clock.

A full instruction cycle in PIC is generally broken into three stages: **Fetch → Decode → Execute**.

---

## 9. PIC File Types and Popular Chips

### Data Formats
Data in PIC programming/documentation can be represented in several formats:
1. **HEX** (Hexadecimal, base 16) — most common in assembly code, e.g. `25H`.
2. **Binary** — base 2, e.g. `B'01011101'`.
3. **Decimal** — base 10, ordinary numbers, written like `D'10'` in PIC assembly.
4. **ASCII** — text characters represented as their standard numeric codes, e.g. `A'Y'` represents the letter Y.

### Compiler vs Assembler
- **Compiler** — translates a High-Level Language (HLL) like C directly into machine code (binary instructions the CPU understands).
- **Assembler** — translates **assembly language** (human-readable mnemonics like `MOVLW`) into machine code. Assembly is much closer to raw machine code than C is — each assembly instruction usually maps to exactly one machine instruction.

### Instructions vs. Directives (Pseudo-Instructions)
- **Instructions** are commands the CPU actually executes at run time (e.g. `MOVLW`, `ADDWF`).
- **Directives** (a.k.a. pseudo-instructions) are commands to the **assembler itself**, not the CPU — they don't produce executable code; they give the assembler instructions about how to build the program. Covered fully in [Section 10](#10-assembler-directives).

### PIC18F458 — Example Real Chip
A commonly studied chip in this course, the **PIC18F458**, has:
- **40 pins** total in DIP (Dual In-line Package) form.
- **33 I/O pins** usable (the remaining ~7 pins are dedicated to OSC1, OSC2 [clock crystal connections], Reset, VDD, Vss [power/ground] etc.).
- **5 I/O Ports**: PORTA, PORTB, PORTC, PORTD, PORTE
  - RA0–RA5/6 → PORTA (6 or 7 usable pins, chip-dependent)
  - RB0–RB7 → PORTB (8 pins)
  - RC0–RC7 → PORTC (8 pins)
  - RD0–RD7 → PORTD (8 pins)
  - RE0–RE2 → PORTE (3 pins)

Each port has **three** related Special Function Registers (SFRs):
- **PORTx** — reads/writes the actual pin logic level.
- **TRISx** — sets pin **direction** (input/output) — the "tristate" control register.
- **LATx** — the **output latch**, which holds the value being driven out (useful to avoid read-modify-write glitches).

---

## 10. Assembler Directives

Directives tell the **assembler** how to build the program; they are not executed by the CPU.

| Directive | Purpose |
|---|---|
| **EQU** | Defines a constant value or a fixed address, and gives it a name. Used, for instance, to name a counter constant, which is then loaded/stored via WREG. |
| **SET** | Functionally identical to EQU, **except** a value defined with SET can be reassigned later in the program, whereas an EQU-defined constant cannot. |
| **ORG** | Sets the **starting address** for the code/data that follows — used for both code sections and data sections. |
| **END** | Marks the end of the program's source file (`.asm` file) for the assembler. |
| **LIST** | A special directive that tells the assembler exactly **which PIC chip** the program should be assembled for (so the assembler knows the correct instruction set/memory map to use). |

### Example
```asm
COUNT   EQU     0x25        ; COUNT now means the address/value 25H
        MOVLW   COUNT       ; WREG = 25H
```

### Two more useful, related keywords (assembler output options)
- **LST** — tells the assembler to generate a listing file showing both the original source code and the generated binary machine codes side by side (handy for debugging).
- **MAP** — generates a memory map showing which memory locations are used and which are free, helping verify the overall system design is correct.

---

## 11. Structure of a PIC Assembly Program (ALP)

A PIC **Assembly Language Program (ALP)** is written using a fixed four-column layout:

| Label | Mnemonic | Operand(s) | Comment |
|---|---|---|---|
| (optional name for this line/address) | the instruction | the data it works on | explanation, starts with `;` |

**Workflow to write and run a PIC program:**
1. You type the program into a **text editor**, typically inside an all-in-one tool like **MPLAB IDE** (which bundles the editor, assembler, linker, and simulator). Older/simpler setups sometimes used plain Notepad on Windows.
2. The source code is saved as an **`.asm`** file.
3. The assembler translates the program (which may combine instructions written in different valid formats — hex, decimal, binary, ASCII) into machine code, which is further interpreted and stored at the correct memory locations in the chip.

---

## 12. The GPR / SFR File Register and Data Movement

PIC's data memory (RAM) is organized as a "file register" — essentially a big array of byte-sized storage locations. Some of these locations are **General Purpose Registers (GPR)** — free for the programmer to use as variables — and others are **Special Function Registers (SFR)** — pre-assigned to control specific hardware features (e.g., PORTB, PORTC, PORTD, PORTE, TRISx, timers, etc.).

### Moving Data with MOVWF and MOVLW
```asm
MOVLW   55H         ; Move the Literal value 55H into WREG.  WREG = 55H
MOVWF   PORTC       ; MOVe WREG to File register PORTC.      PORTC = 55H
MOVWF   PORTD
MOVWF   PORTE
```
- `MOVLW` moves a **literal (constant)** into WREG.
- `MOVWF` moves the **current value of WREG** into a file register (any RAM location, including an SFR like a PORT).

### ADDWF and the Destination Bit (d)
```asm
ADDWF   file_reg, d     ; Add the contents of WREG to the file register.
```
The letter **`d`** (the "destination bit") decides **where the result goes**:
- If **d = 0** → the result is stored back in **WREG**.
- If **d = 1** → the result is stored back in the **file register**.

#### Worked Example
Suppose the following values are already sitting in RAM:

| Address | Data |
|---|---|
| 005 | 22 |
| 006 | 22 |
| 007 | 00 |

```asm
MOVLW   22H          ; WREG = 22H
MOVWF   05H          ; move WREG into location 05H
MOVWF   06H
MOVWF   07H

ADDWF   05H, 0        ; Add WREG (22H) to loc 05H (22H) → total 44H, result stays in WREG
ADDWF   06H, 0        ; WREG = 66H now (44H + 22H from loc 06H)
ADDWF   07H, 1        ; WREG(66H) + loc 07H(22H) = 88H, this time result is stored IN the file register (loc 07H)
```
After this sequence: **WREG = 66H**, and **file register at 007 = 88H**. This illustrates exactly how the destination bit changes where a result lands.

### More Instructions Introduced in the Notes
| Instruction | Meaning (short) |
|---|---|
| `ADDWF` | Add WREG to File register |
| `ADDWFC` | Add WREG to File register, **with Carry** |
| `ANDWF` | Logical AND of WREG and File register |
| `MOVFF` | Move data directly File-to-File (does not go through WREG) |
| `ORWF` | Logical OR of WREG and File register |
| `SUBFW` (SUBWF) | Subtract WREG from File register |
| `SUBB` (SUBWFB) | Subtract WREG from File register, with Borrow |
| `COMF` | Complement (invert all bits of) a File register |
| `DECF` | Decrement (subtract 1 from) a File register |
| `XORWF` | Logical XOR of WREG and File register |
| `INCF` | Increment (add 1 to) a File register |
| `RLCF` | Rotate Left through Carry |

---

## 13. Looping and Branching

**Looping** means repeating a sequence of instructions or an operation a certain number of times — it is the most widely used programming technique for repetitive tasks (blinking an LED, scanning a keypad, generating a delay, etc.).

### DECFSZ — Decrement File, Skip if Zero
```asm
DECFSZ  file_reg, d
```
This instruction **decrements** (subtracts 1 from) the file register. Then:
- If the result becomes **zero**, the CPU **skips** the very next instruction (which is typically a jump back to the top of the loop, placed right after the `DECFSZ`).
- If the result is **not zero**, execution just continues to the next instruction normally (falling into the jump-back, and looping again).

This clever "decrement-and-conditionally-skip" behavior is exactly what's needed to build a "repeat N times" loop.

### BNZ — Branch if Not Zero
`BNZ` jumps to a target label **only if the Zero flag is 0** (i.e., the last result was not zero). It's commonly paired with `DECF` to build loops manually.

### Example: Add 3 to WREG, 10 Times
```asm
COUNT   EQU     0x25        ; use location 25H to hold the loop counter

        MOVLW   d'10'       ; WREG = 10 (decimal)
        MOVWF   COUNT       ; load the counter
        MOVLW   0           ; WREG = 0 (start the running total at zero)
Again:
        ADDLW   3           ; add 3 to WREG
        DECFSZ  COUNT, F    ; decrement counter; SKIP the next line if counter hits 0
        GOTO    Again       ; repeat until counter becomes 0
        MOVWF   PORTB       ; send the final sum to PORTB
```

**Simple flowchart for a two-number "add" program:**
```
Start → Send 1st number → Send 2nd number → Add the 2 numbers → Store the sum → Stop
```

### Nested Loops (a loop inside a loop)
Used when you need to repeat an *entire inner loop* multiple times — for example, "complement PORTB, and do that whole thing 100 times," where 100 = 10 (outer loop) × 10 (inner loop):

```asm
COUNT_1 EQU     d'10'       ; outer loop count
COUNT_2 EQU     d'10'       ; inner loop count

        MOVLW   0x55
        MOVWF   PORTB       ; PORTB = 55H
        MOVLW   COUNT_1
        MOVWF   R1          ; load 10 into outer-loop counter (R1)
        MOVLW   COUNT_2
        MOVWF   R2          ; load 10 into inner-loop counter (R2)

LOOP2:  COMF    PORTB, F    ; complement (invert) PORTB
        DECF    R2, F       ; decrement inner-loop counter
        BNZ     LOOP2       ; repeat inner loop until R2 = 0
        DECF    R1, F       ; decrement outer-loop counter
        BNZ     LOOP1       ; repeat the whole thing until R1 = 0
        END
```

### Conditional vs. Unconditional Branches
| Type | Instructions | Size |
|---|---|---|
| **Conditional** (short jump) | `BNZ` (branch if not zero), `BNC` (branch if no carry) | 2-byte instruction |
| **Unconditional** | `GOTO` | 4-byte instruction |

Conditional branches only jump if a specific flag condition is true; `GOTO` always jumps, no matter what.

---

## 14. Subroutines: CALL, RCALL, and the Stack

A **subroutine** (also called a function or procedure) is a reusable block of code you can jump to, run, and then return from — useful for tasks that need to be performed repeatedly (like a delay routine).

### CALL vs. RCALL
| Instruction | Description | Size |
|---|---|---|
| **CALL** | "Long call" — can jump to any subroutine anywhere in the full memory space. | 4 bytes |
| **RCALL** | "Relative call" (short call) — jumps to a subroutine near the current location. Smaller and faster, but limited range. | 2 bytes |

### How CALL/RETURN Works: The Stack
The **stack** is a special block of memory used to remember **where to come back to** after a subroutine finishes.

- When `CALL` runs, the current Program Counter value (the return address — the instruction right after the CALL) is **pushed** onto the stack, and the PC jumps to the subroutine.
- When the subroutine finishes with `RETURN`, that saved address is **popped** off the stack back into the PC, so execution resumes exactly where it left off.

The **Stack Pointer (SP)** is an 8-bit register that always points to the current top of the stack. It automatically **increments** as new return addresses are pushed, and decrements as they are popped.

In PIC18, each stack entry holds a full **21-bit** return address (matching the 21-bit Program Counter), split internally into three parts:
```
PCU (upper) | PCH (high) | PCL (low)
```

### Example Delay Subroutine Call
```asm
        MOVLW   0x55
        MOVWF   PORTB       ; put 55H on PORTB pins
        CALL    DELAY       ; call the delay subroutine
        MOVLW   0xAA
        MOVWF   PORTB       ; put AAH on PORTB
        CALL    DELAY
        GOTO    L1          ; loop forever, toggling PORTB with a delay in between
```

---

## 15. I/O Ports: TRIS, LAT, PORT

Every PIC18 I/O port has **bidirectional, digital I/O capability**, meaning each individual pin can independently be configured as an input or an output. These ports are also often **multiplexed** — shared — with special peripheral functions (like ADC input, serial TX/RX, etc.) so the chip can support many features without needing a separate pin for everything.

### TRISx Register — Direction Control
`TRISx` decides whether each pin of PORTx is an **Input** or **Output**:
- Bit = **1** → pin is an **Input**.
- Bit = **0** → pin is an **Output**.

```asm
MOVLW   0x0        ; WREG = 00
MOVWF   TRISB       ; make PORTB an OUTPUT port (all bits 0)
```

### LATx Register — Output Latch
`LATx` is used to reliably **store/hold** the output value being driven on the pins (helps avoid subtle glitches that can occur if you read-modify-write the PORTx register directly in rapid succession).

### Bit-Level Instructions (Bit Addressability)
Sometimes you want to control a single pin without disturbing the other 7 bits of the port. PIC18 provides bit-oriented instructions for exactly this:

| Instruction | Meaning |
|---|---|
| `BSF` | **B**it **S**et **F**ile register — sets one specific bit to 1 |
| `BCF` | **B**it **C**lear **F**ile register — clears one specific bit to 0 |
| `BTG` | **B**it **T**o**g**gle — flips one specific bit |

### Complete Example: Blink PORTB with a Delay Subroutine
```asm
        MOVLW   0x0
        MOVWF   TRISB       ; PORTB = output

L1:     MOVLW   0x55
        MOVWF   PORTB       ; PORTB = 55H
        CALL    DELAY
        MOVLW   0xAA
        MOVWF   PORTB       ; PORTB = AAH
        CALL    DELAY
        GOTO    L1
```

---

## 16. Instruction Cycle and Timing

The **instruction cycle** (also called the **machine cycle** or **T-cycle**) is the amount of time the CPU needs to fetch and execute one instruction.

- Since all PIC18 instructions are either **2 bytes** or **4 bytes** long, each instruction takes **no more than 1 or 2 instruction cycles** to execute.
- In PIC18, **1 instruction cycle = 4 oscillator (crystal) clock periods**, i.e.:

$$ \text{Instruction Cycle Frequency} = \frac{\text{Crystal Frequency}}{4} $$

- The **length** (duration) of one instruction cycle therefore directly depends on the crystal oscillator's frequency.

### Worked Examples
Given three different crystal frequencies, find the instruction-cycle period (T = 1 / frequency):

| Crystal Frequency | Instruction Cycle Frequency (÷4) | Instruction Cycle Period (T) |
|---|---|---|
| 4 MHz | 1 MHz | 1 µs |
| 16 MHz | 4 MHz | 0.25 µs |
| 20 MHz | 5 MHz | 0.2 µs |
| 10 MHz | 2.5 MHz | 0.4 µs |

*(These are basic "find T = 1/f" calculations, but applied after first dividing the crystal frequency by 4 to get the instruction-cycle frequency.)*

### Instruction Format
Each instruction word is split into an **opcode** (which operation to perform) and, for certain instructions, a **literal** (the constant data value):
```
[ 0000 0110 | -------- ]
   opcode      literal
```
Literals in PIC18 instructions (like `ADDLW`, `MOVLW`) can range from **00H to FFH** (0–255), since they fit in one 8-bit field.

Byte sizes of common instructions:
| Instruction | Size |
|---|---|
| `MOVLW`, `ADDLW`, `MOVWF` | 2 bytes |
| `MOVFF`, `GOTO` | 4 bytes |

---

## 17. Arithmetic Instructions and Flags

### ADDLW — Add Literal to WREG
```asm
ADDLW   K       ; WREG = WREG + K
```

#### Worked Example
```asm
MOVLW   0xF5    ; WREG = F5H
ADDLW   0xB     ; WREG = F5H + 0BH = 100H → stored 8-bit result = 00H
```
Resulting flags: **Z = 1** (result is 00H, zero), **C = 1** (carry out of bit 7), **DC = 1** (carry out of bit 3).

### Multi-Byte (Multi-Precision) Addition
Since a single PIC register only holds 8 bits (max value 255), adding numbers **larger than 255** requires adding them **byte by byte**, propagating any carry from one byte into the next — very similar to how you'd add large numbers by hand, column by column, carrying into the next column.

**Worked example:** Add four bytes stored at RAM locations 40H–43H (assume 7DH, EBH, C5H, 5BH) and store the 2-byte result at file locations 6 (low byte) and 7 (high byte):

```asm
L_byte  EQU     0x6         ; RAM location 6 will hold the LOW byte of the sum
H_byte  EQU     0x7         ; RAM location 7 will hold the HIGH byte of the sum

        MOVLW   0           ; clear WREG
        MOVWF   H_byte      ; H_byte = 0 (this will accumulate any carries)

        ADDWF   0x40, W     ; WREG = WREG + [40H]
        BNC     N_1         ; if no carry, skip ahead
        INCF    H_byte, F   ; carry occurred → increment H_byte

N_1:    ADDWF   0x41, W
        BNC     N_2
        INCF    H_byte, F

N_2:    ADDWF   0x42, W
        BNC     N_3
        INCF    H_byte, F

N_3:    ADDWF   0x43, W
        BNC     N_4
        INCF    H_byte, F

N_4:    MOVWF   L_byte       ; store the final low byte
        ; H_byte already holds the accumulated high byte
```
The core trick: after each `ADDWF`, check the Carry flag with `BNC` (**B**ranch if **N**o **C**arry). If a carry *did* occur, increment the high byte to account for it — exactly how you'd "carry the 1" doing addition by hand.

---

## 18. Decimal Adjust (DAW) for BCD Math

**BCD (Binary-Coded Decimal)** represents each decimal digit (0–9) using its own 4-bit binary code (a "nibble"), so a byte can hold two decimal digits (e.g., the number 29 is stored as `0010 1001`).

**Problem:** If you add two BCD numbers using ordinary binary addition, you can get an *invalid* result, because binary addition doesn't "know" it should wrap around at 9 (not 15) within each nibble.

**Example:** `29 + 01` in plain binary addition gives `2A` — but `2A` isn't a valid two-digit BCD number (the second digit "A" doesn't exist in decimal); the correct BCD answer should be `30`.

### DAW — Decimal Adjust WREG
`DAW` fixes this automatically. It inspects the value in WREG along with the **Carry** and **DC** flags, and corrects the byte back into valid BCD form:

1. If the **lower nibble** (bottom 4 bits) is greater than 9, **or** the DC flag is set → **add 0110 (6)** to the lower 4 bits.
2. If the **upper nibble** (top 4 bits) is greater than 9, **or** the Carry flag is set → **add 0110 (6)** to the upper 4 bits.

`DAW` should always be used **immediately after** a BCD addition instruction, to guarantee the result stays a valid two-digit BCD number.

---

## 19. Subtraction Instructions

### SUBLW — Subtract WREG from Literal
```asm
SUBLW   K       ; WREG = K - WREG   (note the order: literal MINUS WREG!)
```

#### Worked Example
```asm
MOVLW   0x23    ; WREG = 23H
SUBLW   0x3F    ; WREG = 3FH - 23H = 1CH
```

### Interpreting the Result's Sign
After a subtraction, check the **Carry (C)** and **Negative (N)** flags together:
- **C = 1, N = 0** → the result is **positive**.
- **C = 0, N = 1** → the result is **negative** (stored as a **2's complement** value).

### Subtracting Two 8-bit Values (with sign handling)
```asm
MYREG   EQU     0x20

        MOVLW   0x4C
        MOVWF   MYREG        ; MYREG = 4CH
        MOVLW   0x6E         ; WREG = 6EH
        SUBWF   MYREG, W     ; WREG = MYREG - WREG
        BNN     NEXT         ; if result is Not Negative (N=0), skip ahead
        NEGF    WREG         ; otherwise, take the 2's complement to get the magnitude
NEXT:   MOVWF   MYREG
```
`NEGF` computes the **negation (2's complement)** of a file register — used here to convert a negative result into its positive magnitude for display/further processing.

### Subtracting Two 16-bit Numbers
For numbers bigger than 8 bits, subtract byte-by-byte, propagating any **borrow** using `SUBWFB` (**Sub**tract **W**REG **F**rom file, with **B**orrow):

**Example:** Subtract `1296H` from `2762H`, storing the result's low byte at file location 6 and high byte at location 7:

```asm
        MOVLW   0x96
        SUBWF   0x6, F      ; F = F - W  →  62H - 96H = low byte with borrow generated
        MOVLW   0x12
        SUBWFB  0x7, F      ; F = F - W - borrow  →  27H - 12H - 1(borrow)
```
Result: **2762H − 1296H = 14CCH**, split as low byte = `CCH` at location 6 and high byte = `14H` at location 7.

### Other Arithmetic Instructions
- **MULLW K** — multiply WREG by literal K.
- **DIVLW K** — divide WREG by literal K.

---

## 20. Compare and Rotate Instructions

### Compare Instructions
PIC18 has three dedicated compare-and-skip instructions that compare a file register against WREG:

| Instruction | Skips next instruction if... |
|---|---|
| `CMPFSGT` | file register **>** WREG (Greater Than) |
| `CMPFSEQ` | file register **=** WREG (Equal) |
| `CMPFSLT` | file register **<** WREG (Less Than) |

#### Worked Example: Find the Smaller of Two Values (27 and 54)
```asm
VAL_1   EQU     D'27'
VAL_2   EQU     D'54'
LREG    EQU     0x20        ; location that will hold the smaller value

        MOVLW   VAL_1
        MOVWF   LREG        ; LREG = 27
        MOVLW   VAL_2       ; WREG = 54
        CPFSLT  LREG        ; skip next instruction if LREG < WREG
        MOVWF   LREG        ; (runs only if the skip did NOT happen) — place the smaller value
```

### Rotate Instructions
Rotate instructions shift all the bits in a register one position left or right, "wrapping around" the bit that falls off the end:

| Instruction | Meaning |
|---|---|
| `RRCF` | Rotate Right through Carry |
| `RRNCF` | Rotate Right, No Carry |
| `RLCF` | Rotate Left through Carry |
| `RLNCF` | Rotate Left, No Carry |

```
   ┌──────────────┐
   │  MSB ← → LSB │   (bits shift in a circle; "through Carry" versions route the
   └──────────────┘    bit that falls off through the Carry flag on its way around)
```

---

## 21. Addressing Modes

**Addressing mode** = the method an instruction uses to specify *where its operand (data) comes from*. PIC18 supports **four** addressing modes:

### 1. Immediate Addressing
The operand is a **literal constant** — it comes immediately after the opcode itself (baked directly into the instruction). In PIC18 documentation, immediate/literal data is simply called a **"literal."**

```asm
MOVLW   0x25            ; the constant 25H is the operand
SUBLW   D'62'
ANDLW   AND WREG
B'01011101'
```

### 2. Direct Addressing
The operand's data lives in a RAM location whose **address is directly and explicitly known/written** in the instruction.

```asm
MOVLW   0x56             ; WREG = 56H
MOVWF   0x40             ; copy WREG into RAM location 40H
MOVFF   0x40, 0x50       ; copy data directly from location 40H to location 50H
```

### 3. Register Indirect Addressing
Instead of naming an address directly, a special register is used as a **pointer** that *contains* the address of the actual data — similar to how a street address on an envelope points you to a house, rather than being the house itself.

PIC18 provides **three** such pointer registers: **FSR0, FSR1, FSR2** (**F**ile **S**elect **R**egister).
- Each FSR is a **12-bit register**, wide enough to point anywhere within the full 4096-byte (4 KB) data RAM space.
- The `LFSR` instruction is used to **load** an address into an FSR:

```asm
LFSR    0, 0x30      ; FSR0 now points to RAM address 30H
LFSR    1, 0x40      ; FSR1 → 40H
LFSR    2, 0x6F      ; FSR2 → 6FH
```

### 4. Indexed (ROM) Addressing
Data specifications are given in terms of **programmable and memory-access locations**, often used for accessing lookup tables stored in program memory (ROM), where an index/offset is combined with a base address to compute the final location.

---

## 22. Assembly vs. C: Why Use C?

Assembly language gives precise, low-level control but is tedious and error-prone. High-level languages like **C** (compiled with a tool such as the **C18 compiler** for PIC18) offer real advantages:

1. **Easier and less time-consuming** to write than assembly.
2. **Easier to modify and update** — changing logic doesn't require reworking raw registers by hand.
3. **Code is readily available in functional libraries** — you don't have to reinvent common routines.
4. **Portable to other microcontrollers** without modification (the same C logic can often be recompiled for a different chip, unlike assembly which is chip-specific).

---

## 23. Checksum Bytes

A **checksum** is an extra byte appended to the end of a series of data bytes, used to detect data corruption/errors — for example, when transmitting data or storing it, you can later verify nothing got flipped or corrupted along the way.

### The Two Rules
1. **To generate the checksum byte:** Add all the data bytes together and **drop any carry** (keep only the lowest 8 bits of the sum). Then take the **2's complement** of that sum — this is the checksum byte.
2. **To verify data integrity later:** Add all the data bytes **together with the checksum byte** included. If the data is intact, this total sum should come out to **00H** (with the carry dropped). If it's not zero, something in the data changed — an error is detected.

### Worked Example
Given four hex data bytes: `25H, 62H, 3FH, 52H`

**a) Find the checksum byte:**
```
  25
  62
  3F
+ 52
-----
 118H  → drop carry → 18H
2's complement of 18H = E8H
```
**Checksum byte = E8H**

**b) Verify integrity** (add all data bytes + the checksum byte, should total 00H after dropping carry):
```
  25
  62
  3F
  52
+ E8
-----
 200H → drop the carry (the leading "2") → 00H  ✓ (integrity confirmed)
```

**c) Detecting an error:** If the 2nd byte (62H) is accidentally changed to 22H, redo the same check:
```
  25
  22
  3F
  52
+ E8
-----
 1C0H → drop carry → C0H  ✗ (NOT zero → error detected!)
```
Since the result isn't zero, the checksum check correctly flags that the data has been corrupted.

---

## 24. Macros and Modules

### Macros
A **macro** is a feature in assembly language programming that lets you define a **group of instructions once**, then reuse it repeatedly by name — instead of retyping (or copy-pasting) the same block of code every time you need it. This saves time and reduces the chance of typos/errors.

**Syntax:**
```asm
name    MACRO   dummy1, dummy2, ...
        ; body of the macro (the instructions to repeat)
        ENDM
```

**Example:**
```asm
MOVLF   MACRO   K, MyReg
        MOVLW   K
        MOVWF   MyReg
        ENDM
```
Now anywhere in the program, writing `MOVLF 0x25, COUNTER` automatically expands into the two instructions above.

### Modules
Breaking a large program into separate, self-contained **modules** (often separately-assembled/compiled files or functions) has several advantages:
1. **Failure of one module doesn't necessarily stop the whole program** — problems can be isolated.
2. **Each module can be written, debugged, and tested individually**, before being combined with the rest.
3. **Easier and less time-consuming** to manage than one giant monolithic program.
4. **Can be linked together with code written in high-level languages like C**, mixing assembly and C where each is most useful.

---

## 25. C Programming for PIC18 (C18 Compiler)

### Basic C Data Types and Their Ranges
| Data Type | Size | Range |
|---|---|---|
| `unsigned char` | 8-bit | 0 to 255 |
| `char` | 8-bit | -128 to 127 (bit D7 is the sign bit) |
| `unsigned int` | 16-bit | 0 to 65,535 |
| `int` | 16-bit | -32,768 to 32,767 (bit D15 is the sign bit) |
| `short` | 24-bit | (used for medium-range values) |
| `long` | 32-bit | (used for large values, e.g. loop counters above 65,535) |

> **Tip:** if a loop needs to count higher than 65,535 (e.g. up to 100,000), use `long` instead of `int`, since `int` would overflow.

### Example 1: Send Values 00H–FFH to PORTB
```c
#include <P18F458.h>      // gives access to TRISB and PORTB definitions

void main(void)
{
    unsigned char z;
    TRISB = 0;                 // make PORTB an output
    for (z = 0; z <= 255; z++)
        PORTB = z;
    while(1);                  // infinite loop — needed so the program
                                // doesn't "fall off the end" on real hardware
}
```

### Example 2: Send ASCII Hex Codes for Characters to PORTB
```c
#include <P18F458.h>

void main(void)
{
    unsigned char my_num[] = "0123456ABCD";
    unsigned char z;
    TRISB = 0;
    for (z = 0; z < 10; z++)
        PORTB = my_num[z];
    while(1);
}
```

### Example 3: Toggle All Bits of PORTB Continuously
```c
#include <P18F458.h>

void main(void)
{
    TRISB = 0;
    for( ; ; )                 // infinite loop
    {
        PORTB = 0x55;           // 0101 0101
        PORTB = 0xAA;           // 1010 1010
    }
}
```

### Example 4: Toggle PORTB Bits 50,000 Times
```c
unsigned int z;
TRISB = 0;
for (z = 0; z <= 50000; z++)
{
    PORTB = 0x55;
    PORTB = 0xAA;
}
while(1);

// Note: for counts above 65,535 (e.g. 100,000 times), use `long` instead of `unsigned int`.
```

### Generating Time Delays in C — Two Methods
1. **Using a simple `for` loop** — the CPU just "wastes time" counting up (or down) an empty loop; simple but imprecise, and ties up the CPU entirely.
2. **Using a PIC18 hardware timer** — far more accurate and lets the CPU do other work while waiting (see [Section 26](#26-timers)).

---

## 26. Timers

Timers are hardware circuits inside the microcontroller that count clock pulses automatically, freeing the CPU from having to "waste time" in software loops. They serve **two main functions**:
1. **Create time delays.**
2. **Act as a counter** (e.g., counting external events like button presses).

### Timer Availability by Family
| Family | Number of Timers |
|---|---|
| PIC16 | 3 timers (Timer0, Timer1, Timer2) — 8-bit, 16-bit, 8-bit respectively |
| PIC18 | 5 timers (Timer0 – Timer4) |

### Clock Source: Internal or External
Every timer needs a **clock pulse** to "tick." This clock can come from:
- **Internal source:** Whenever the internal clock is used, **1/4th of the crystal oscillator frequency** is automatically fed to the timer (i.e., **Fosc/4**) — this is used for generating time delays.
- **External source:** Pulses are fed in through a dedicated PIC18 pin, letting the timer act as an **event counter** instead.

### Timer0 Registers
- **TMR0H** — holds the high byte of the timer's count (bits D8–D15, in 16-bit mode).
- **TMR0L** — holds the low byte of the timer's count (bits D0–D7).
- **T0CON** — the Timer0 **Control** register — configures how Timer0 behaves.
- **T0CS** — Timer0 **Clock Source select** bit — tells the timer whether to use the internal or external clock.

### T0CON Register Bits (8 bits total)
| Bit | Name | Function |
|---|---|---|
| D7 | **TMR0ON** | Timer ON/OFF control. 1 = ON (start), 0 = OFF (stop). |
| — | **T08BIT** | 1 = 8-bit timer mode, 0 = 16-bit timer mode. |
| — | **T0CS** | Timer Clock Source select. 1 = External clock (via the RA4 pin), 0 = Internal clock (Fosc/4). |
| — | **T0SE** | Timer Source Edge select. 1 = count on High-to-Low transitions, 0 = count on Low-to-High transitions. |
| — | **PSA** | Prescaler Assignment bit. 1 = timer clock bypasses the prescaler entirely, 0 = timer clock passes through (and is divided by) the prescaler. |

### What Is a Prescaler, and Why Use One?
A **prescaler** divides down the incoming clock frequency **before** it reaches the timer's counting circuit, in powers of 2: **÷2, ÷4, ÷8, ÷16, ÷32, ... up to ÷256**. It exists to help:
- Maintain the desired **resolution / accuracy**.
- Achieve longer **time delays** than the raw clock could produce directly.
- Control how often the timer **overflows** (wraps back to zero after reaching its maximum count).

*(Example: Fosc = 16 MHz → Fosc/4 = 4 MHz timer clock. If further divided by a prescaler of 8, the timer effectively ticks at 4 MHz ÷ 8 = 0.5 MHz... conceptually similar to how "16MHz/8 = 2MHz" appears as a scratch calculation in the notes.)*

### Example: Toggle PORTB with Timer0-Generated Delay (16-bit mode, no prescaler)
```c
#include <P18F458.h>
void T0Delay(void);

void main(void)
{
    TRISB = 0;
    while(1)
    {
        PORTB = 0x55;
        T0Delay();
        PORTB = 0xAA;
        T0Delay();
    }
}

void T0Delay()
{
    T0CON = 0x08;          // Timer0, 16-bit mode, no prescaler
    TMR0H = 0x35;           // load high byte
    TMR0L = 0x00;           // load low byte
    T0CONbits.TMR0ON = 1;   // turn Timer0 ON
    while (INTCONbits.TMR0IF == 0);  // wait here until Timer0 overflows (rolls over)
    T0CONbits.TMR0ON = 0;   // turn Timer0 OFF
    INTCONbits.TMR0IF = 0;  // clear the overflow flag, ready for next time
}
```
This works because you preload the timer with a starting count; it then counts up automatically until it overflows (wraps past its maximum), setting the **TMR0IF** flag — a simple, hardware-timed way to create an accurate delay.

A very similar version can use **Timer0 in 16-bit mode with a 1:4 prescaler** for a different (typically longer) delay duration, such as producing a ~50ms toggle interval.

---

## 27. Serial Communication Basics

Data can travel between devices in two fundamentally different ways:

| Type | Description | Typical Use |
|---|---|---|
| **Serial** | Data sent **one bit at a time**, over a single wire (or pair). | Chances of data loss are **lower** and it's **more cost-effective** (fewer wires needed) — this is why it's used for most modern long-distance/embedded communication. |
| **Parallel** | Multiple bits sent **simultaneously**, each on its own dedicated wire. | Historically used for devices like printers and hard disks — fast over short distances, but more wires = more cost and more chance of signal interference over long distances. |

### Communication Directions
- **Simplex** — data flows in **one direction only** (Transmitter → Receiver, never the reverse).
- **Half-duplex** — data can flow **both directions**, but **not at the same time** (devices take turns).
- **Full Duplex** — data can flow **both directions simultaneously** (separate Tx and Rx lines let both devices talk and listen at once).

---

## 28. Asynchronous Serial Communication and Framing

There are two broad styles of serial communication:
- **Asynchronous** — data is sent **character by character**, each wrapped in its own start/stop markers (no shared clock signal needed between sender and receiver).
- **Synchronous** — data is sent in larger **blocks**, using a shared clock signal to keep sender and receiver in sync; this style focuses on data integrity and compatibility, and needs a defined **framing** structure.

### Data Frame Structure (Asynchronous)
Each character sent asynchronously is wrapped in a "frame" like this:
```
[Start bit] [Data bits...] [Stop bit]
    0          (data first)    1 (Mark)
```
- The **Start bit** is always a logic **0** ("space") — it alerts the receiver that a new character is about to arrive.
- The actual **data bits go first**, right after the start bit.
- The **Stop bit** (logic **1**, called "Mark") comes **last**, signaling the end of that character's frame.

### Bits Per Second vs. Baud Rate
- **bps (bits per second)** — the actual number of data bits transmitted each second.
- **Baud rate** — the number of **signal changes (transitions)** per second on the communication line. (For simple encoding schemes, baud rate and bps are numerically the same, but they aren't always identical concepts in more complex modulation schemes.)

---

## 29. RS-232 and the MAX232 Chip

### RS-232 Standard
- **RS-232** = **R**ecommended **S**tandard 232, a serial I/O interfacing standard developed by the **EIA** (**E**lectronic **I**ndustries **A**lliance/Association) in the **1960s**, for connecting communication equipment.
- Variants exist: **RS-232A, RS-232B, RS-232C**.
- It's the serial standard used by essentially all PIC18-based systems that need to talk to a PC or similar equipment.

### DB-25 / DB-9 Connectors
- **DB-25** — a common connector type used with RS-232 (a smaller **DB-9** connector is also very common and shown in the PIC circuit examples).
- **P (Plug)** = the **male** connector.
- **S (Socket)** = the **female** connector.

### The Voltage Mismatch Problem — and MAX232
PIC18 pins operate at **TTL logic levels** (roughly 0V = logic 0, 5V = logic 1), but the RS-232 standard uses much larger voltage swings (traditionally around ±3V to ±15V) to improve noise immunity over longer cables. Connecting a PIC directly to an RS-232 port would damage it or fail to communicate.

The **MAX232** chip (made by **Maxim Corporation**) solves this — it's a **voltage converter / line driver** that translates between TTL levels (PIC side) and RS-232 voltage levels (PC/cable side).
- A related chip, **MAX233**, does the same job but needs **fewer external capacitors**, saving board space.
- On the PIC side, the Tx/Rx pins remain simple **TTL-compatible** signals.

### Typical Connection
```
PIC18 (PORTC: TXD, RXD) ── MAX232 ── DB-9 connector ── RS-232 cable ── PC
```

---

## 30. USART Registers and a Full Serial-Transmit Program

**USART** = **U**niversal **S**ynchronous/**A**synchronous **R**eceiver/**T**ransmitter — the PIC18's built-in hardware for serial communication.

- In **synchronous mode**, USART is typically used to transfer data between the PIC18 and external peripherals (like certain ADC or EEPROM chips) that need a shared clock.
- In **asynchronous mode**, USART connects the PIC18 to something like an IBM-PC-compatible serial port, enabling **full-duplex** serial data transfer (both sides can send and receive at once).

### The 6 Key USART Registers (all 8-bit)
| Register | Full Name | Purpose |
|---|---|---|
| **SPBRG** | Serial Port Baud Rate Generator | Sets the communication speed (baud rate) |
| **TXREG** | Transmit Register | Holds the byte about to be transmitted |
| **RCREG** | Receive Register | Holds the byte just received |
| **TXSTA** | Transmit Status & Control register | Configures/monitors transmission |
| **RCSTA** | Receive Status & Control register | Configures/monitors reception |
| **PIR** | Peripheral Interrupt Request register | Contains flags like TXIF (Transmit Interrupt Flag) that signal when the hardware is ready for more data |

### Full Example: Transmit the Message "YES" Serially
**Task:** Transmit "YES" at 9600 baud, 8-bit data, 1 stop bit, and repeat forever.

```asm
        MOVLW   B'00100000'
        MOVWF   TXSTA        ; configure transmit settings (enable transmitter, etc.)
        MOVLW   D'15'
        MOVWF   SPBRG        ; set baud rate generator value for 9600 baud (at the given crystal freq)
        BCF     TRISC, TX    ; make the TX pin an output
        BSF     RCSTA, SPEN  ; enable the serial port

OVER:   MOVLW   A'Y'
        CALL    TRANS
        MOVLW   A'E'
        CALL    TRANS
        MOVLW   A'S'
        CALL    TRANS
        BRA     OVER          ; repeat forever

TRANS:
S1:     BTFSS   PIR1, TXIF   ; check if the Transmit-Interrupt Flag is set (hardware ready for new byte)
        BRA     S1           ; if not ready yet, keep waiting (poll)
        MOVWF   TXREG        ; hardware is ready → send WREG's character out
        RETURN
```

**How it works, step by step:**
1. `TXSTA` and `SPBRG` are configured once at the start to set up the serial port's speed and mode.
2. The subroutine `TRANS` repeatedly checks the **TXIF** flag inside the `PIR1` register using `BTFSS` (**B**it **T**est **F**ile, **S**kip if **S**et) — this is a polling loop that waits until the transmit hardware is free.
3. Once free, the character currently in WREG is copied into `TXREG`, which triggers the hardware to actually shift it out, bit by bit, on the TX pin.
4. The main loop (`OVER`) sends 'Y', then 'E', then 'S', then loops back and does it again — forever.

*(A related practice exercise in the notes: write a similar program to continuously transmit the single letter 'G' at 9600 baud, using a 10 MHz crystal — the same TRANS subroutine pattern applies; only the baud-rate register value would need recalculating for the new crystal frequency.)*

---

## Quick-Reference Summary Table

| Concept | One-Line Summary |
|---|---|
| PIC | Peripheral Interface Controller, by Microchip, since ~1993 |
| RISC | Small, simple instruction set → faster execution |
| Harvard Architecture | Separate program & data memory/buses → simultaneous access |
| WREG | The "working register" — the accumulator for most operations |
| STATUS register | Holds flags: N, OV, Z, DC, C |
| Program Counter | Points to the next instruction to execute |
| TRISx | Sets pin direction (1 = input, 0 = output) |
| PORTx | The actual I/O pins |
| LATx | Output latch (safe way to drive output pins) |
| EQU / SET | Assembler directives defining named constants |
| ORG | Sets a starting address |
| DECFSZ | Decrement & skip if the result is zero — used to build loops |
| CALL / RCALL | Jump to a subroutine (long / short) |
| Stack | Remembers return addresses for CALL/RETURN |
| DAW | Fixes BCD math results after addition |
| Checksum | Extra byte used to detect data corruption |
| Macro | A reusable, named block of assembly instructions |
| Timer0-4 | Hardware counters for delays / event counting |
| USART | Hardware for serial (UART/RS-232-style) communication |
| MAX232 | Converts PIC's TTL signals to RS-232 voltage levels |

---

*Compiled and expanded from personal handwritten class notes (dated 18/7/26 – 3/9/26) on Microcontrollers and Embedded Systems, focused on the PIC18 family.*
