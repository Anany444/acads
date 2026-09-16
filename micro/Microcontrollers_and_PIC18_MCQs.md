# Microcontrollers & PIC18 — 40 Practice MCQs

Based on the companion notes file (`Microcontrollers_and_PIC18_Notes.md`). Try to answer each question before checking the **Answer Key** at the end.

---

**Q1.** What does PIC stand for?
- A) Programmable Interface Controller
- B) Peripheral Interface Controller
- C) Personal Integrated Chip
- D) Processor Interconnect Controller

**Q2.** Which company developed the PIC microcontroller family, around 1989–1993?
- A) Intel
- B) Motorola
- C) Microchip Technology
- D) Texas Instruments

**Q3.** ARM stands for:
- A) Automated Reduced Machine
- B) Advanced RISC Machine
- C) Applied Register Module
- D) Advanced Register Microprocessor

**Q4.** The 8051 is best described as a:
- A) 16-bit microprocessor
- B) 32-bit microcontroller
- C) 8-bit microcontroller
- D) 4-bit microcontroller

**Q5.** How much on-chip program memory (ROM) does the classic 8051 have?
- A) 128 bytes
- B) 4 KB
- C) 8 KB
- D) 64 KB

**Q6.** How much on-chip data RAM does the classic 8051 have?
- A) 4 KB
- B) 32 bytes
- C) 128 bytes
- D) 256 bytes

**Q7.** How many 16-bit timers does the classic 8051 have on-chip?
- A) One
- B) Two
- C) Three
- D) Five

**Q8.** The memory organization of both the 8051 and PIC uses which architecture, where program memory and data memory are physically separate?
- A) Von Neumann architecture
- B) Harvard architecture
- C) Pipeline architecture
- D) RISC architecture

**Q9.** In a microcontroller instruction, "addressing mode" refers to:
- A) The physical pin layout of the chip
- B) The way an instruction specifies where its operand (data) comes from
- C) The IP address used for network communication
- D) The clock speed setting of the CPU

**Q10.** Which architecture design philosophy does PIC follow, using a small set of simple, fast instructions?
- A) CISC
- B) RISC
- C) VLIW
- D) SIMD

**Q11.** How many timers does the PIC18 family typically provide?
- A) 2
- B) 3
- C) 5
- D) 8

**Q12.** In the PIC18 timer set, which timers commonly operate in 16-bit mode?
- A) Timer0 and Timer1
- B) Timer1 and Timer3
- C) Timer2 and Timer4
- D) Timer0 and Timer4

**Q13.** MPLAB IDE bundles which of the following tools into one package?
- A) Only a text editor
- B) Text editor, assembler, linker, and simulator
- C) Only a debugger and emulator
- D) A web browser and compiler

**Q14.** Which registers are used to control the PIC's built-in Analog-to-Digital Converter?
- A) TRISA and TRISB
- B) ADCON0 and ADCON1
- C) T0CON and T1CON
- D) TXSTA and RCSTA

**Q15.** When selecting a microcontroller for a project, which of these is NOT typically listed as a selection criterion in the notes?
- A) Speed and power consumption
- B) Number of I/O pins and cost per unit
- C) Availability of compiler, debugger, and emulator
- D) The microcontroller manufacturer's stock price

**Q16.** MEMS stands for:
- A) Micro Electronic Memory System
- B) Micro Electrical Mechanical System
- C) Mechanical Embedded Microcontroller System
- D) Multi-Element Memory Storage

**Q17.** Which memory type can be programmed exactly ONE time and cannot be erased/reused?
- A) Flash
- B) Mask ROM
- C) OTP (One-Time Programmable)
- D) UV-EPROM

**Q18.** Which memory type is generally considered the CHEAPEST option, since the program is fixed into the chip during manufacturing?
- A) UV-EPROM
- B) Flash
- C) OTP
- D) Mask version ROM

**Q19.** In PIC memory organization, at which address does the CPU begin execution after a power-on reset?
- A) 0004H
- B) FFFFH
- C) 0000H
- D) 1000H

**Q20.** At which address does the CPU jump to service an interrupt?
- A) 0000H
- B) 0004H
- C) 0008H
- D) FFFFH

**Q21.** According to the notes, roughly how much better/faster is PIC18 compared to PIC16?
- A) About 1.5 times
- B) About 5 times
- C) About 10 times
- D) They perform identically

**Q22.** FPGA stands for:
- A) Fixed Program Gate Array
- B) Field Programmable Gate Array
- C) Fast Processing Gate Architecture
- D) Field Processing General Array

**Q23.** What does the instruction `MOVLW 25H` do?
- A) Moves the value in WREG to memory location 25H
- B) Moves the literal value 25H into the WREG register
- C) Adds 25H to the file register
- D) Compares WREG with 25H

**Q24.** In the STATUS register, which flag is set to 1 when the result of an ALU operation is exactly zero?
- A) Carry (C)
- B) Digital Carry (DC)
- C) Zero (Z)
- D) Overflow (OV)

**Q25.** The Digital Carry (DC) flag specifically tracks a carry generated between which two bits?
- A) Bit 6 to Bit 7
- B) Bit 3 to Bit 4
- C) Bit 0 to Bit 1
- D) Bit 7 out of the register entirely

**Q26.** In PIC18, the Program Counter (PC) is how many bits wide, enabling access to a larger program memory space than PIC16?
- A) 12 bits
- B) 16 bits
- C) 21 bits
- D) 32 bits

**Q27.** Pipelining improves CPU performance mainly by:
- A) Increasing the crystal oscillator frequency
- B) Overlapping the fetch, decode, and execute stages of multiple instructions
- C) Reducing the number of available instructions
- D) Removing the need for a stack

**Q28.** Which of the following is a PIC assembler DIRECTIVE (not an instruction executed by the CPU)?
- A) MOVLW
- B) ADDWF
- C) EQU
- D) GOTO

**Q29.** What is the key difference between the `EQU` and `SET` directives?
- A) EQU only works with hex numbers; SET only works with decimal
- B) A value defined with SET can be reassigned later; a value defined with EQU cannot
- C) SET is used only for I/O ports; EQU is used only for RAM addresses
- D) There is no difference; they are unrelated directives

**Q30.** Which directive marks the beginning of a specific address for code or data in a PIC assembly program?
- A) END
- B) LIST
- C) ORG
- D) EQU

**Q31.** What does the `DECFSZ` instruction do?
- A) Decrements WREG and always jumps to the next label
- B) Decrements a file register, and skips the next instruction if the result becomes zero
- C) Compares two file registers
- D) Divides a file register by 2

**Q32.** Which instruction always performs an unconditional jump and is 4 bytes in size?
- A) BNZ
- B) BNC
- C) GOTO
- D) RCALL

**Q33.** What is the primary purpose of the stack in subroutine calls (CALL/RETURN)?
- A) To hold the values of I/O ports temporarily
- B) To store the return address so execution can resume after the subroutine finishes
- C) To generate the system clock signal
- D) To store the checksum of the program

**Q34.** What is the key difference between `CALL` and `RCALL`?
- A) CALL is a "long call" (4 bytes) that can reach anywhere in memory; RCALL is a smaller, relative "short call" (2 bytes) with limited range
- B) RCALL can only be used inside interrupt service routines
- C) CALL only works with 8-bit data; RCALL only works with 16-bit data
- D) There is no functional difference between them

**Q35.** Setting a bit in the `TRISx` register to 1 configures the corresponding pin as:
- A) An output
- B) An input
- C) An analog reference pin
- D) A ground pin

**Q36.** In PIC18, one instruction cycle equals how many oscillator (crystal) clock periods?
- A) 1
- B) 2
- C) 4
- D) 8

**Q37.** If a PIC18 system uses a 16 MHz crystal, what is the resulting instruction cycle period (with no prescaler)?
- A) 1 µs
- B) 0.25 µs
- C) 0.5 µs
- D) 4 µs

**Q38.** What is the purpose of the `DAW` (Decimal Adjust WREG) instruction?
- A) It converts a byte into ASCII text
- B) It corrects the result of a BCD addition so it remains a valid decimal (BCD) value
- C) It rotates all bits in WREG to the left
- D) It divides WREG by 10

**Q39.** In the checksum method described in the notes, how is the checksum byte itself generated from a series of data bytes?
- A) Add all the bytes together (dropping the carry), then take the 2's complement of that sum
- B) Multiply all the bytes together
- C) Take the XOR of only the first and last byte
- D) Subtract the largest byte from the smallest byte

**Q40.** Which of the following is an advantage of using the C language (instead of assembly) for PIC programming, as listed in the notes?
- A) C code always runs faster than hand-written assembly
- B) C requires no compiler
- C) C code is portable to other microcontrollers without modification, and is easier/faster to write and maintain
- D) C eliminates the need for a stack

---

## Answer Key

| Q | Answer | Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|---|---|
| 1 | B | 11 | C | 21 | A | 31 | B |
| 2 | C | 12 | C | 22 | B | 32 | C |
| 3 | B | 13 | B | 23 | B | 33 | B |
| 4 | C | 14 | B | 24 | C | 34 | A |
| 5 | B | 15 | D | 25 | B | 35 | B |
| 6 | C | 16 | B | 26 | C | 36 | C |
| 7 | B | 17 | C | 27 | B | 37 | B |
| 8 | B | 18 | D | 28 | C | 38 | B |
| 9 | B | 19 | C | 29 | B | 39 | A |
| 10 | B | 20 | B | 30 | C | 40 | C |

---

### Quick Explanations for Trickier Questions

- **Q17 vs Q18:** OTP = programmable once, no UV erase window (cheaper than UV-EPROM but not the cheapest overall). Mask ROM is baked in at the factory and is the cheapest *only* at very high production volumes.
- **Q21:** The notes state PIC18 is roughly **1.5×** better than PIC16 due to architectural improvements (pipelining, more buses, etc.).
- **Q25:** DC (Digital Carry / half-carry) specifically tracks the carry from bit 3 into bit 4 — essential for BCD correction with `DAW`.
- **Q34:** `CALL` = long call (4 bytes, unlimited range); `RCALL` = relative/short call (2 bytes, limited range but faster/smaller).
- **Q37:** 16 MHz ÷ 4 = 4 MHz instruction-cycle frequency → T = 1 / 4 MHz = **0.25 µs**.
- **Q39:** Checksum = (sum of all data bytes, carry dropped) → then take the **2's complement** of that result.


---

## Additional Practice MCQs (Q41–Q55) — LCD, Keyboard, Sensors & PIC18 Interrupts

**Q41.** A standard LCD module interfaced with a PIC microcontroller typically has how many pins?
- A) 8
- B) 14
- C) 16
- D) 20

**Q42.** Which LCD control pin determines whether the byte on the data bus is treated as a command or as displayable character data?
- A) EN
- B) RS
- C) R/W
- D) Vee

**Q43.** On an LCD, setting RS = 0 means:
- A) The data bus holds a character to display
- B) The instruction/command register is selected
- C) The LCD is currently busy
- D) The backlight is being powered

**Q44.** What is the specific function of the LCD's EN (Enable) pin?
- A) It sets the display contrast
- B) It selects between read and write direction
- C) It latches whatever data is currently on the data pins into the LCD
- D) It powers the LCD's backlight

**Q45.** When reading the LCD's busy flag (R/W = 1, RS = 0), what does D7 = 1 mean?
- A) The LCD is free and ready for the next instruction
- B) The LCD is busy and not yet ready for the next instruction
- C) A power failure has occurred
- D) A parity error has occurred

**Q46.** At the lowest hardware level, how are the keys of a keyboard typically organized?
- A) As a matrix of rows and columns
- B) As individually wired dedicated pins for every key
- C) As a single serial shift register
- D) As an analog voltage-divider ladder

**Q47.** Using two dedicated 8-bit I/O ports (one for rows, one for columns), how large a keypad matrix can a microcontroller scan?
- A) 2×2
- B) 4×4
- C) 8×8
- D) 16×16

**Q48.** In a sensor-based embedded system, what role does the ADC play between the sensor and the CPU?
- A) It amplifies the digital output signal
- B) It converts the sensor's analog voltage into a digital value the CPU can process
- C) It stores sensor readings permanently, like a hard disk
- D) It supplies power to the sensor

**Q49.** Which best describes an "actuator" in an embedded system?
- A) A device that converts a physical stimulus into an electrical signal
- B) A device that produces a physical action based on a command/input from the microcontroller
- C) A special type of ADC
- D) A type of interrupt flag

**Q50.** How many dedicated external hardware interrupt pins does PIC18 provide, and where are they located?
- A) 2 pins on PORTA
- B) 3 pins (INT0, INT1, INT2) on PORTB (RB0, RB1, RB2)
- C) 4 pins on PORTC
- D) 1 pin on PORTD

**Q51.** Immediately after any reset (power-on or otherwise), what is the default state of all interrupts on a PIC18?
- A) All interrupts are enabled automatically
- B) All interrupts are disabled by default and must be enabled by software
- C) Only the timer interrupts are enabled by default
- D) Interrupts cannot be configured at all after a reset

**Q52.** Which single bit acts as the master "global" switch that must be set before ANY interrupt can reach the CPU?
- A) INTEDG
- B) TMR0IE
- C) GIE (bit 7 of INTCON)
- D) RCIP

**Q53.** In the PIC18 interrupt vector table, which addresses are used for high-priority and low-priority interrupts respectively?
- A) 0x0008 (high), 0x0018 (low)
- B) 0x0000 (high), 0x0004 (low)
- C) 0x0018 (high), 0x0008 (low)
- D) Both priorities share the same address, 0x0008

**Q54.** What is the main advantage of an interrupt-driven approach over a polling approach?
- A) It requires writing less overall code
- B) The CPU can perform other useful work instead of continuously checking a status flag, and reacts immediately once notified
- C) It removes the need for a stack entirely
- D) It works without enabling any control bits

**Q55.** What does the `RETFIE` instruction do at the end of an Interrupt Service Routine (ISR)?
- A) It permanently disables all future interrupts
- B) It pops the saved return address from the stack back into the Program Counter and re-enables the GIE bit, resuming the main program
- C) It clears the LCD display
- D) It performs a full microcontroller reset

---

## Answer Key (Q41–Q55)

| Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|
| 41 | B | 47 | C | 53 | A |
| 42 | B | 48 | B | 54 | B |
| 43 | B | 49 | B | 55 | B |
| 44 | C | 50 | B | | |
| 45 | B | 51 | B | | |
| 46 | A | 52 | C | | |

### Quick Explanations
- **Q41:** Standard interfacing LCDs used in this course have **14 pins** (16-pin versions add two backlight pins, but the core interface is 14).
- **Q50:** PIC18's three external interrupts map directly onto PORTB pins: **INT0→RB0, INT1→RB1, INT2→RB2**.
- **Q53:** Right after reset, every interrupt defaults to *high priority*, so it's worth remembering **0x0008 = high**, **0x0018 = low**.
- **Q55:** `RETFIE` is essentially "RETURN" plus "re-enable GIE" in one instruction — it's what lets the main program keep running normally after each interrupt is serviced.

---

## Additional Practice MCQs (Q56–Q65) — ADC in Detail

**Q56.** For a 10-bit ADC, how many distinct digital output values can it represent?
- A) 10
- B) 256
- C) 1024
- D) 2048

**Q57.** Using the formula Digital Output = (Vin / Vref) × (2ⁿ − 1), what is the approximate digital output of a 10-bit ADC with Vref = 5V and Vin = 2.5V?
- A) About 128
- B) About 255
- C) About 511
- D) About 1023

**Q58.** Why does a single PIC18 chip need a multiplexer for its ADC even though it can read several analog pins (AN0, AN1, AN2, …)?
- A) Because each analog pin has its own separate, independent ADC circuit
- B) Because there is only one physical ADC conversion circuit, time-shared across the analog input pins
- C) Because the multiplexer converts digital signals to analog
- D) Because the multiplexer stores the final result permanently

**Q59.** Which register is primarily responsible for selecting the ADC channel and starting a conversion?
- A) ADCON1
- B) TRISA
- C) ADCON0
- D) PORTA

**Q60.** Which register configures whether each AN pin behaves as an analog input or a plain digital I/O pin, and selects the voltage reference source?
- A) ADCON0
- B) ADCON1
- C) ADRESH
- D) INTCON

**Q61.** In ADCON0, what does setting the GO/DONE bit to 1 do?
- A) It immediately clears the ADC result registers
- B) It starts an ADC conversion
- C) It turns the entire ADC module off
- D) It selects channel AN0 specifically

**Q62.** How does the GO/DONE bit behave once an ADC conversion finishes?
- A) It stays at 1 until manually cleared by software
- B) It is automatically cleared to 0 by hardware, signaling the conversion is complete
- C) It toggles between 0 and 1 continuously
- D) It has no relationship to conversion completion

**Q63.** Why is a short "acquisition time" delay needed before starting an ADC conversion?
- A) To let the CPU clock stabilize
- B) To let the ADC's internal sample-and-hold capacitor fully charge to the input voltage, ensuring an accurate reading
- C) To reset the ADCON1 register
- D) To allow the LCD busy flag to clear

**Q64.** Since PIC18 registers are only 8 bits wide but the ADC produces a 10-bit result, where is that result stored?
- A) Entirely within ADCON0
- B) Split across the two registers ADRESH and ADRESL
- C) Directly inside WREG only
- D) In the STATUS register's unused bits

**Q65.** What is the smallest voltage difference (approximate resolution step) a 10-bit ADC with Vref = 5V can distinguish?
- A) About 4.89 mV
- B) About 48.9 mV
- C) About 489 mV
- D) About 5 mV

---

## Answer Key (Q56–Q65)

| Q | Answer | Q | Answer |
|---|---|---|---|
| 56 | C | 61 | B |
| 57 | C | 62 | B |
| 58 | B | 63 | B |
| 59 | C | 64 | B |
| 60 | B | 65 | A |

### Quick Explanations
- **Q57:** (2.5V / 5V) × 1023 ≈ **511–512**, i.e. exactly half of the full 10-bit range — makes sense since Vin is exactly half of Vref.
- **Q65:** Step size = Vref / (2ⁿ − 1) = 5V / 1023 ≈ **4.89 mV** — the same figure worked out in the notes.
