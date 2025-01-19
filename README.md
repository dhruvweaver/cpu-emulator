# Custom CPU Architecture Emulator

This is the codebase for the software-based emulator for my custom CPU architecture.

I intend on reproducing the hardware emulated here on an FPGA.
The related project for that will be linked here when I get there.

## Architectural Description
### Key features:
- 32-bit architecture
- Pipelined execution

### Registers:
-   R1, R2, R3, R4: General purpose registers
-   T1: Temporary register
-  MDR: Memory Data Register
-  MAR: Memory Address Register
-   AC: Accumulator
-    X: Index
-   SP: Stack pointer
-   PC: Program counter
- CVZN: Condition code bits (4-bits only)
     - C - Carry (add) / Borrow (subtract)
     - V - Overflow
     - Z - Zero
     - N - Negative

### Instructions:
#### ALU

| Instruction | Opcode |            Description             |
| ----------- | ------ | ---------------------------------- |
|         ADD | 000001 | Add (+), Register Addressing       |
|             | 000010 | Add (+), Immediate Addressing      |
|         SUB | 000011 | Sub (-), Register Addressing       |
|             | 000100 | Sub (-), Immediate Addressing      |
|         INC | 000101 | Inc (++), Register Addressing      |
|         AND | 000110 | AND (&), Register Addressing       |
|             | 000111 | AND (&), Immediate Addressing      |
|          OR | 001000 |  OR (&#124;), Register Addressing  |
|             | 001001 |  OR (&#124;), Immediate Addressing |
|         XOR | 001010 | XOR (^), Register Addressing       |
|             | 001011 | XOR (^), Immediate Addressing      |
|         SHL | 001100 | SHL (<<), Register Addressing      |
|             | 001101 | SHL (<<), Immediate Addressing     |
|         SHR | 001110 | SHR (>>), Register Addressing      |
|             | 001111 | SHR (>>), Immediate Addressing     |

#### Memory Access

| Instruction | Opcode |            Description             |
| ----------- | ------ | ---------------------------------- |
|        LOAD | 010000 | LOAD (>>), Register Addressing     |
|             | 010001 | LOAD (>>), Immediate Addressing    |
|       STORE | 010010 | STORE (>>), Register Addressing    |
|             | 010011 | STORE (>>), Immediate Addressing   |

#### Flow Control

| Instruction | Opcode |                 Description                 |
| ----------- | ------ | ------------------------------------------- |
|         BEQ | 010100 | Branch if equal, Register Addressing        |
|             | 010101 | Branch if equal, PC-Relative Addressing     |
|         BNE | 010110 | Branch if not equal, Register Addressing    |
|             | 010111 | Branch if not equal, PC-Relative Addressing |
|         BIZ | 011000 | Branch if zero, Register Addressing         |
|             | 011001 | Branch if zero, PC-Relative Addressing      |
|         NOP | 011010 | No operation                                |
|        HALT | 011011 | Halt                                        |
