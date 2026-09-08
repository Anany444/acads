# PIC Microcontrollers, Assembly, Timers, I/O and Serial Communication --- 40 MCQs

> **Based on the uploaded handwritten notes.**
>
> Each question has four options. The answer and a short explanation are
> provided after the questions.

------------------------------------------------------------------------

# Questions

## 1. What is a microcontroller?

A. A CPU that must always use external memory\
B. A complete small computer system integrated on a chip\
C. A type of compiler\
D. A type of communication cable

**Answer: B**

**Explanation:** A microcontroller integrates a CPU/core with memory and
peripherals such as I/O, timers, and communication interfaces.

------------------------------------------------------------------------

## 2. What does RISC stand for?

A. Random Instruction System Controller\
B. Reduced Instruction Set Computer\
C. Register Integrated System Computer\
D. Reduced Internal Storage Controller

**Answer: B**

**Explanation:** RISC stands for Reduced Instruction Set Computer and
emphasizes a relatively small set of simple instructions.

------------------------------------------------------------------------

## 3. Which architecture separates program memory and data memory?

A. Harvard architecture\
B. Von Neumann architecture\
C. Ring architecture\
D. Pipeline architecture

**Answer: A**

**Explanation:** Harvard architecture uses separate program/instruction
and data-memory paths.

------------------------------------------------------------------------

## 4. What is the primary role of WREG in the PIC architecture discussed in the notes?

A. It is the program counter\
B. It is the working register used by many operations\
C. It is only a timer register\
D. It stores the oscillator frequency

**Answer: B**

**Explanation:** WREG is the working register and participates in many
data-transfer, arithmetic, and logical operations.

------------------------------------------------------------------------

## 5. What does `MOVLW 0x25` conceptually do?

A. Moves WREG into address 0x25\
B. Moves literal 0x25 into WREG\
C. Adds 0x25 to WREG\
D. Clears WREG

**Answer: B**

**Explanation:** `MOVLW` means move literal to WREG.

------------------------------------------------------------------------

## 6. What does `MOVWF PORTB` conceptually do?

A. Moves PORTB into WREG\
B. Moves WREG into PORTB\
C. Moves PORTB into the program counter\
D. Clears PORTB

**Answer: B**

**Explanation:** `MOVWF` transfers the contents of WREG to the specified
file register, such as PORTB.

------------------------------------------------------------------------

## 7. Which instruction is used to set an individual bit?

A. BCF\
B. BSF\
C. BTG\
D. DECF

**Answer: B**

**Explanation:** BSF means Bit Set File and sets the selected bit to 1.

------------------------------------------------------------------------

## 8. Which instruction clears an individual bit?

A. BSF\
B. BCF\
C. BTG\
D. INCF

**Answer: B**

**Explanation:** BCF means Bit Clear File and sets the selected bit to
0.

------------------------------------------------------------------------

## 9. What does `BTG` do?

A. Copies a byte\
B. Toggles a selected bit\
C. Decrements a register\
D. Branches if zero

**Answer: B**

**Explanation:** BTG changes a selected bit from 0 to 1 or from 1 to 0.

------------------------------------------------------------------------

## 10. What does `DECFSZ` do?

A. Decrements a file register and skips the next instruction if the
result is zero\
B. Increments WREG and branches if zero\
C. Clears a file register\
D. Adds two file registers

**Answer: A**

**Explanation:** DECFSZ is particularly useful for implementing counted
loops.

------------------------------------------------------------------------

## 11. Which instruction performs an unconditional branch?

A. BNZ\
B. GOTO\
C. RETURN\
D. MOVWF

**Answer: B**

**Explanation:** `GOTO label` transfers execution to the specified label
without checking a condition.

------------------------------------------------------------------------

## 12. What is the main purpose of `CALL`?

A. To configure a timer\
B. To call a subroutine\
C. To clear a bit\
D. To load a literal into WREG

**Answer: B**

**Explanation:** CALL transfers control to a subroutine while preserving
the return information needed by the return mechanism.

------------------------------------------------------------------------

## 13. Which instruction returns from a subroutine?

A. GOTO\
B. RETURN\
C. CALL\
D. BNZ

**Answer: B**

**Explanation:** `RETURN` transfers control back to the point after the
subroutine call.

------------------------------------------------------------------------

## 14. Which flag indicates an unsigned carry out of the most significant bit?

A. Z\
B. N\
C. C\
D. OV

**Answer: C**

**Explanation:** The Carry flag indicates a carry from the most
significant bit in an arithmetic operation.

------------------------------------------------------------------------

## 15. Which flag is associated with signed arithmetic overflow?

A. C\
B. OV\
C. DC\
D. Z

**Answer: B**

**Explanation:** OV indicates signed overflow. Carry and overflow should
not be confused.

------------------------------------------------------------------------

## 16. If an arithmetic result is zero, which flag is normally set?

A. C\
B. DC\
C. Z\
D. OV

**Answer: C**

**Explanation:** Z is the zero flag.

------------------------------------------------------------------------

## 17. What does the DC flag represent?

A. Data counter\
B. Digit carry\
C. Direct control\
D. Decimal counter

**Answer: B**

**Explanation:** DC represents digit carry, especially relevant to the
lower-nibble carry used in BCD arithmetic.

------------------------------------------------------------------------

## 18. What is BCD?

A. Binary Control Data\
B. Binary-Coded Decimal\
C. Byte Carry Data\
D. Basic Counter Design

**Answer: B**

**Explanation:** BCD represents each decimal digit using four binary
bits.

------------------------------------------------------------------------

## 19. Why is decimal adjustment required after some BCD additions?

A. A binary addition can produce a nibble that is not a valid BCD digit\
B. WREG cannot store decimal values\
C. PORTB only accepts decimal values\
D. Timers require BCD values

**Answer: A**

**Explanation:** For example, a lower decimal digit can produce a
hexadecimal value such as A, which is invalid as a BCD digit.

------------------------------------------------------------------------

## 20. What is the purpose of `EQU`?

A. Execute a loop\
B. Define a symbolic constant/value\
C. Enable a timer\
D. End a program

**Answer: B**

**Explanation:** `EQU` allows a meaningful symbol to represent a
constant or assembler value.

------------------------------------------------------------------------

## 21. What does `ORG` generally specify?

A. The oscillator frequency\
B. The origin/address where subsequent assembly is placed\
C. The output direction of a port\
D. The UART baud rate

**Answer: B**

**Explanation:** ORG specifies an assembly origin for subsequent
code/data placement.

------------------------------------------------------------------------

## 22. What is the purpose of a label in assembly?

A. It stores electrical voltage\
B. It gives a symbolic name to a program location\
C. It changes the oscillator frequency\
D. It configures the UART

**Answer: B**

**Explanation:** Labels make branches and subroutine destinations
readable without requiring programmers to manually use instruction
addresses.

------------------------------------------------------------------------

## 23. Which addressing mode places the actual constant directly in the instruction?

A. Immediate\
B. Direct\
C. Register indirect\
D. Indexed

**Answer: A**

**Explanation:** In immediate addressing, the operand is the literal
value itself.

------------------------------------------------------------------------

## 24. In register-indirect addressing, what does a pointer register such as an FSR contain?

A. The actual instruction opcode\
B. The address of the data to access\
C. The oscillator frequency\
D. The status flags

**Answer: B**

**Explanation:** FSR acts as a pointer to a location in data memory.

------------------------------------------------------------------------

## 25. What does FSR stand for?

A. File Select Register\
B. Fast Storage Register\
C. Flag Status Register\
D. File System ROM

**Answer: A**

**Explanation:** FSR registers are used for indirect data-memory
addressing.

------------------------------------------------------------------------

## 26. Which concept is most useful for accessing successive elements of an array?

A. Register-indirect/indexed addressing\
B. Only immediate addressing\
C. Only the program counter\
D. The oscillator

**Answer: A**

**Explanation:** Pointer/index-based addressing is useful for arrays,
tables, and buffers.

------------------------------------------------------------------------

## 27. For the TRIS convention shown in the notes, what does a TRIS bit of 0 indicate?

A. Input\
B. Output\
C. High impedance timer mode only\
D. UART mode

**Answer: B**

**Explanation:** In the convention used in the notes, TRIS bit 0
configures the corresponding pin as an output; 1 configures it as an
input.

------------------------------------------------------------------------

## 28. For the same TRIS convention, what does a TRIS bit of 1 indicate?

A. Output\
B. Input\
C. Timer overflow\
D. Serial transmission

**Answer: B**

**Explanation:** TRIS bits control I/O direction in this convention: 1 =
input, 0 = output.

------------------------------------------------------------------------

## 29. What is the main purpose of a timer in a microcontroller?

A. Only to store program code\
B. To count clock events and support timing functions\
C. To replace RAM\
D. To compile assembly

**Answer: B**

**Explanation:** Timers can generate delays, measure intervals, generate
periodic events, and in some modes count external events.

------------------------------------------------------------------------

## 30. What is the main distinction between timer mode and counter mode?

A. Timer mode uses an internal time base, while counter mode counts
external events\
B. Timer mode uses RAM, while counter mode uses ROM\
C. Timer mode is software-only, while counter mode is compiler-only\
D. There is no distinction

**Answer: A**

**Explanation:** A timer normally counts an internal clock-derived
source; counter mode counts external events/pulses.

------------------------------------------------------------------------

## 31. What does a prescaler do?

A. Multiplies the clock frequency\
B. Divides the input clock before it reaches the timer/counter\
C. Stores program instructions\
D. Clears the status register

**Answer: B**

**Explanation:** A prescaler reduces the effective timer input
frequency, increasing the time represented by each timer count.

------------------------------------------------------------------------

## 32. If a timer input clock is 1 MHz and the prescaler divides by 4, what is the timer clock?

A. 4 MHz\
B. 2 MHz\
C. 500 kHz\
D. 250 kHz

**Answer: D**

**Explanation:**

``` text
1 MHz / 4 = 250 kHz
```

------------------------------------------------------------------------

## 33. If a timer clock is 1 MHz, how long does one timer count take?

A. 1 second\
B. 1 ms\
C. 1 µs\
D. 1 ns

**Answer: C**

**Explanation:**

``` text
T = 1 / 1 MHz = 1 µs
```

------------------------------------------------------------------------

## 34. What happens when an N-bit timer increments beyond its maximum value?

A. It necessarily stops permanently\
B. It overflows/rolls over according to the timer architecture\
C. It becomes a UART\
D. It clears program memory

**Answer: B**

**Explanation:** An N-bit counter has a finite range and wraps/overflows
after reaching its maximum count.

------------------------------------------------------------------------

## 35. Which is generally better for accurate periodic timing?

A. A long busy-wait loop\
B. A hardware timer\
C. Random instruction execution\
D. A compiler directive

**Answer: B**

**Explanation:** Hardware timers provide a dedicated and more
deterministic time base while allowing the CPU to perform other work.

------------------------------------------------------------------------

## 36. What is the purpose of a start bit in asynchronous serial communication?

A. It indicates the beginning of a serial frame/character\
B. It indicates the end of program memory\
C. It selects the timer prescaler\
D. It resets the CPU

**Answer: A**

**Explanation:** The start bit allows the receiver to detect the
beginning of the incoming character and establish its sampling timing.

------------------------------------------------------------------------

## 37. Which sequence best represents a typical asynchronous serial frame?

A. Stop → data → start\
B. Start → data → stop\
C. Data → timer → stop\
D. Start → RAM → ROM

**Answer: B**

**Explanation:** A typical frame is idle, start bit, data bits, optional
parity, and stop bit(s).

------------------------------------------------------------------------

## 38. What does SPBRG generally relate to in a PIC USART/UART?

A. Stack pointer\
B. Baud-rate generation\
C. Port direction\
D. Program memory

**Answer: B**

**Explanation:** SPBRG is commonly associated with configuring the
serial baud-rate generator.

------------------------------------------------------------------------

## 39. Which register is commonly associated with transmitting data in the PIC USART concepts from the notes?

A. TXREG\
B. RCREG\
C. TRISB\
D. PORTB

**Answer: A**

**Explanation:** TXREG is the transmit register; RCREG is associated
with received data.

------------------------------------------------------------------------

## 40. Which statement correctly distinguishes a macro from a subroutine?

A. A macro is expanded by the assembler, while a subroutine is called at
runtime\
B. A macro always requires CALL and RETURN\
C. A subroutine is always expanded into every call site\
D. Macros can only be used for timers

**Answer: A**

**Explanation:** A macro is expanded during assembly. A subroutine is
stored as executable code and entered using a call mechanism, normally
returning afterward.

------------------------------------------------------------------------

# Answer Key

     Q  Answer  Core concept
  ---- -------- -----------------------
     1    B     Microcontroller
     2    B     RISC
     3    A     Harvard architecture
     4    B     WREG
     5    B     MOVLW
     6    B     MOVWF
     7    B     BSF
     8    B     BCF
     9    B     BTG
    10    A     DECFSZ
    11    B     GOTO
    12    B     CALL
    13    B     RETURN
    14    C     Carry flag
    15    B     Overflow flag
    16    C     Zero flag
    17    B     Digit carry
    18    B     BCD
    19    A     Decimal adjustment
    20    B     EQU
    21    B     ORG
    22    B     Labels
    23    A     Immediate addressing
    24    B     Register indirect
    25    A     FSR
    26    A     Array/pointer access
    27    B     TRIS = output
    28    B     TRIS = input
    29    B     Timers
    30    A     Timer vs counter
    31    B     Prescaler
    32    D     Prescaler calculation
    33    C     Timer period
    34    B     Timer overflow
    35    B     Hardware timer
    36    A     Start bit
    37    B     Serial frame
    38    B     Baud-rate generator
    39    A     TXREG
    40    A     Macro vs subroutine

------------------------------------------------------------------------

# Mini Practice: Score Yourself

-   **36--40:** Excellent --- exam-ready on the core concepts.
-   **31--35:** Very good --- revise weaker areas.
-   **25--30:** Good foundation --- revisit flags, addressing, timers,
    and serial communication.
-   **20--24:** Needs another revision pass.
-   **Below 20:** Start with the concept guide, then retry these
    questions without looking at the answers.

## High-priority topics to revise

1.  Harvard vs RISC
2.  WREG and file registers
3.  `MOVLW`, `MOVWF`, `MOVFF`
4.  Status flags: C, DC, Z, OV, N
5.  `DECFSZ` and loops
6.  CALL/RETURN and stack
7.  Addressing modes
8.  TRIS and PORT registers
9.  Timer vs counter
10. Prescaler and timer calculations
11. UART/USART registers
12. Asynchronous serial framing
13. RS-232 vs UART
14. Macros vs subroutines
