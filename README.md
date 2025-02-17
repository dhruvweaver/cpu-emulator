# Custom CPU Architecture Emulator
This is the codebase for the software-based emulator for my custom CPU architecture.

Further documentation for technology like the pipeline implementation will be linked when written

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

|    Category   | Instruction |  Opcode  |                 Description                  |
| ------------- | ----------- | -------- | -------------------------------------------- |
|           ALU |         ADD | `0001 0` | Add (+), Register Addressing                 |
|               |             | `0001 1` | Add (+), Immediate Addressing                |
|               |         SUB | `0010 0` | Sub (-), Register Addressing                 |
|               |             | `0010 1` | Sub (-), Immediate Addressing                |
|               |         INC | `0011 0` | Inc (++), Register Addressing                |
|               |         AND | `0100 0` | AND (&), Register Addressing                 |
|               |             | `0100 1` | AND (&), Immediate Addressing                |
|               |          OR | `0101 0` |  OR (&#124;), Register Addressing            |
|               |             | `0101 1` |  OR (&#124;), Immediate Addressing           |
|               |         XOR | `0110 0` | XOR (^), Register Addressing                 |
|               |             | `0110 1` | XOR (^), Immediate Addressing                |
|               |         SHL | `0111 0` | SHL (<<), Register Addressing                |
|               |             | `0111 1` | SHL (<<), Immediate Addressing               |
|               |         SHR | `1000 0` | SHR (>>), Register Addressing                |
|               |             | `1000 1` | SHR (>>), Immediate Addressing               |
| Memory Access |        LOAD | `1001 0` | LOAD, Register Addressing                    |
|               |             | `1001 1` | LOAD, Base + Addressing                      |
|               |       STORE | `1010 0` | STORE, Register Addressing                   |
|               |             | `1010 1` | STORE, Base + Addressing                     |
|  Flow Control |         BEQ | `1011 0` | Branch if equal, Register Addressing         |
|               |             | `1011 1` | Branch if equal, PC-Relative Addressing      |
|               |         BNE | `1100 0` | Branch if not equal, Register Addressing     |
|               |             | `1100 1` | Branch if not equal, PC-Relative Addressing  |
|               |         BIZ | `1101 0` | Branch if zero, Register Addressing          |
|               |             | `1101 1` | Branch if zero, PC-Relative Addressing       |
|               |         NOP | `1110 0` | No operation                                 |
|               |        HALT | `1111 0` | Halt                                         |
|    Aliased    |         MOV |    NA    | Moves data, Register or Immediate Addressing |

#### Syntax:
**ALU Register addressing**

`ADD DEST, SRC1, SRC2`: DEST = SRC1 + SRC2

**ALU Immediate addressing**

`ADD DEST, SRC1, #VAL`: DEST = SRC1 + VAL

**Memory Register addressing**

`LOAD DEST, [SRC]` : DEST <- Memory[SRC]

`STORE SRC, [DEST]` : Memory[DEST] <- SRC

**Memory Immediate addressing**

`LOAD DEST, [SRC + #VAL]` : DEST <- Memory[SRC + VAL]

`STORE SRC, [DEST + #VAL]` : Memory[DEST + VAL] <- SRC

### Pipeline:
This architecture supports pipelining. [Pipelining allows for more efficient instruction
execution, as it fully utilizes the execution hardware, and is critical to performance
in a RISC architecture.](https://en.wikipedia.org/wiki/Instruction_pipelining)

Instruction stages: **Fetch, Decode, Compute, Memory Access, Write**
