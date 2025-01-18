# Custom CPU Architecture Emulator

This is the codebase for the software-based emulator for my custom CPU architecture.

I intend on reproducing the hardware emulated here on an FPGA.
The related project for that will be linked here when I get there.

## Architectural Description
### Key features:
- 32-bit architecture
### Registers:
-   R1, R2, R3, R4: General purpose registers
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
- ADD: Add         (+)
- SUB: Subtract    (-)
- INC: Increment   (++)
- AND: Bitwise And (&)
-  OR: Bitwise Or  (|)
- XOR: Bitwise Xor (^)
- SHL: Left shift  (<<)
- SHR: Right shift (>>)
#### Memory Access
-  LOAD: Load from memory
- STORE: Store in memory
#### Flow Control
-  BEQ: Branch if equal
-  BNE: Branch if not equal
-  BIZ: Branch if zero
-  NOP: No operation
- HALT: Halt
