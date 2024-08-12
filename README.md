# ASIC-Design

## Contents

- [Task 1](#task-1)
- [Task 2](#task-2)
- [Task 3](#task-3)

## Task-1

- We first create a new file named `sum1ton.c` which prints the sum of all numbers up to 'n'.

![image](https://github.com/user-attachments/assets/c27a1b39-7817-43a6-9f4b-570350ef50e6)

- The following is the C code for the same:

![image](https://github.com/user-attachments/assets/96ceaa26-146c-41e3-867d-60923823f02b)

- The code is compiled using the GCC compiler, producing an output file named `a.out`. Below is the output of the program.

![image](https://github.com/user-attachments/assets/15a83abf-13fb-4822-ac38-754fba4dff68)

- Now, the parameter 'n' in `sum1ton.c` is changed from 5 to 100.

![image](https://github.com/user-attachments/assets/cf321036-15cc-422c-84a3-c039fbb1798a)

- Now, we compile the C program using the RISC-V compiler with O1 optimization.

![image](https://github.com/user-attachments/assets/fa20235e-a636-4ae1-9e7e-03d58c1f8d85)

- Now, we create the object file `sum1ton.o`.

![image](https://github.com/user-attachments/assets/08c9d699-5237-4020-808b-5d19ccd24250)

- As soon as we press the Enter key, a huge list of opcodes is displayed on the terminal. But our focus is on the main section of the program. Type `:/main` to navigate to that portion.

![image](https://github.com/user-attachments/assets/e72e313c-bb12-4928-b743-0de1567e74ad)

- For the "main" section, we can determine the number of instructions by subtracting the address of the first instruction in the next section from the address of the first instruction in the main section, then dividing the difference by 4 (since each instruction is 4 bytes).

![image](https://github.com/user-attachments/assets/1913fb35-806c-475e-9737-1d890058ada2)
![image](https://github.com/user-attachments/assets/74d36fdc-4051-462c-bb76-830c059ed420)
The total number of instructions is 15.

-Next, we compile the C program using the RISC-V compiler with Ofast optimization.

![image](https://github.com/user-attachments/assets/3de390ef-3f7d-4a14-99ad-56ce6a19216d)

- Now, we create the object file `sum1ton.o`.

![image](https://github.com/user-attachments/assets/08c9d699-5237-4020-808b-5d19ccd24250)

- As soon as we press the Enter key, a huge list of opcodes is displayed on the terminal. But our focus is on the main section of the program. Type `:/main` to navigate to that portion.

![image](https://github.com/user-attachments/assets/95410174-0e12-47f4-a6bd-a3060ada6416)

- For the "main" section, we can determine the number of instructions by subtracting the address of the first instruction in the next section from the address of the first instruction in the main section, then dividing the difference by 4 (since each instruction is 4 bytes).

![image](https://github.com/user-attachments/assets/55fb8f17-1e71-4a37-a86f-c1b83a14d082)
![image](https://github.com/user-attachments/assets/74a22175-e3fc-4897-93d2-0374163e75ee)

The total number of instructions is 12.

- There are a total of 15 instructions using O1 and a total of 12 instructions using Ofast. O1 provides a balanced optimization, resulting in more instructions, whereas Ofast prioritizes faster compilation time, leading to fewer instructions.

## Task-2

- Run the `sum1ton.o` in the Spike simulator in order to debug the code.

![image](https://github.com/user-attachments/assets/377b644a-8fa3-47d7-860a-55999ba44559)

- This runs the `sum1ton.o` object file on the Spike RISC-V simulator with the Proxy Kernel and enables debugging mode.

![image](https://github.com/user-attachments/assets/04899006-ed76-4c1a-9ba4-bc28c07a7a25)

- We now bring the PC (program counter) to the start of the main function. We then check the contents of register `a2` before and after running the instructions. After executing the commands, we observe that the registers `a0` and `a2` are properly loaded with appropriate values.

![image](https://github.com/user-attachments/assets/8428f4bd-f3d0-41b5-b5c1-2af564ffa88f)

- We now bring the PC (program counter) to the location `100b8`. The addition of -16 (i.e., -10 in hexadecimal) has been executed properly.

![image](https://github.com/user-attachments/assets/8411cfe4-8c8a-4ebd-bb9c-3340856ab9c1)

The debugging process is successful.

## Task-3

#### Given Instructions

```
ADD r9, r10, r11
SUB r11, r9, r10
AND r10, r9, r11
OR r8, r10, r5
XOR r8, r9, r4
SLT r00, r1, r4
ADDI r02, r2, 5
SW r2, r0, 4
SRL r06, r01, r1
BNE r0, r0, 20
BEQ r0, r0, 15
LW r03, r01, 2
SLL r05, r01, r1
```


#### Instruction Types

The RISC-V instructions are classified into different types:

- **R-Type:** Performs operations between two registers.
- **I-Type:** Operates on a register and an immediate value
- **S-Type:** Stores data from a register to memory
- **B-Type:** Performs conditional branching based on register values.
- **U-Type:** Loads a 20-bit immediate into the upper 20 bits of a register.
- **J-Type:** Performs an unconditional jump to an address calculated from an immediate.

#### Instruction Format

Each instruction in RISC-V is represented by a 32-bit binary pattern, divided into several fields:

- **Opcode (7 bits):** Specifies the operation type.
- **Funct3 (3 bits):** Combined with the opcode to define the exact operation.
- **Funct7 (7 bits):** Used in some instructions to further specify the operation.
- **rs1, rs2 (5 bits each):** Source registers.
- **rd (5 bits):** Destination register.
- **Immediate/Offset:** The immediate value or memory offset, depending on the instruction type.

![image](https://github.com/user-attachments/assets/36f74bcb-c0f8-43f5-b3e1-9f7a854e7fba)

| **Instruction**       | **Type** | **Opcode** | **Funct3** | **Funct7** | **rs1** | **rs2** | **rd** | **Immediate/Offset** | **32-bit Binary Pattern**               |
|-----------------------|----------|------------|------------|------------|---------|---------|--------|-----------------------|------------------------------------------|
| `ADD r9, r10, r11`    | R-Type   | 0110011    | 000        | 0000000    | r10     | r11     | r9     | N/A                   | `0000000 01011 01010 000 01001 0110011` |
| `SUB r11, r9, r10`    | R-Type   | 0110011    | 000        | 0100000    | r9      | r10     | r11    | N/A                   | `0100000 01010 01001 000 01011 0110011` |
| `AND r10, r9, r11`    | R-Type   | 0110011    | 111        | 0000000    | r9      | r11     | r10    | N/A                   | `0000000 01011 01001 111 01010 0110011` |
| `OR r8, r10, r5`      | R-Type   | 0110011    | 110        | 0000000    | r10     | r5      | r8     | N/A                   | `0000000 00101 01010 110 01000 0110011` |
| `XOR r8, r9, r4`      | R-Type   | 0110011    | 100        | 0000000    | r9      | r4      | r8     | N/A                   | `0000000 00100 01001 100 01000 0110011` |
| `SLT r00, r1, r4`     | R-Type   | 0110011    | 010        | 0000000    | r1      | r4      | r00    | N/A                   | `0000000 00100 00001 010 00000 0110011` |
| `ADDI r02, r2, 5`     | I-Type   | 0010011    | 000        | N/A        | r2      | N/A     | r02    | 0000000000000101      | `000000000101 00010 000 00010 0010011` |
| `SW r2, r0, 4`        | S-Type   | 0100011    | 010        | N/A        | r0      | r2      | N/A    | 0000000000000100      | `0000000 00010 00000 010 00010 0100011` |
| `SRL r06, r01, r1`    | R-Type   | 0110011    | 101        | 0000000    | r01     | r1      | r06    | N/A                   | `0000000 00001 00001 101 00110 0110011` |
| `BNE r0, r0, 20`      | B-Type   | 1100011    | 001        | N/A        | r0      | r0      | N/A    | 0000000000010100      | `0000000 00000 00000 001 00001 1100011` |
| `BEQ r0, r0, 15`      | B-Type   | 1100011    | 000        | N/A        | r0      | r0      | N/A    | 0000000000001111      | `0000000 00000 00000 000 00000 1100011` |
| `LW r03, r01, 2`      | I-Type   | 0000011    | 010        | N/A        | r01     | N/A     | r03    | 0000000000000010      | `000000000010 00001 010 00011 0000011` |
| `SLL r05, r01, r1`    | R-Type   | 0110011    | 001        | 0000000    | r01     | r1      | r05    | N/A                   | `0000000 00001 00001 001 00101 0110011` |


| **Instruction**       | **32-bit Binary Pattern**          | **Hex Pattern**  |
|-----------------------|------------------------------------|------------------|
| `ADD r9, r10, r11`    | `0000000 01011 01010 000 01001 0110011` | `0x00B50433` |
| `SUB r11, r9, r10`    | `0100000 01010 01001 000 01011 0110011` | `0x40A4A433` |
| `AND r10, r9, r11`    | `0000000 01011 01001 111 01010 0110011` | `0x00B51733` |
| `OR r8, r10, r5`      | `0000000 00101 01010 110 01000 0110011` | `0x00552633` |
| `XOR r8, r9, r4`      | `0000000 00100 01001 100 01000 0110011` | `0x00451433` |
| `SLT r00, r1, r4`     | `0000000 00100 00001 010 00000 0110011` | `0x00402233` |
| `ADDI r02, r2, 5`     | `000000000101 00010 000 00010 0010011`  | `0x00510113` |
| `SW r2, r0, 4`        | `0000000 00010 00000 010 00010 0100011` | `0x00202023` |
| `SRL r06, r01, r1`    | `0000000 00001 00001 101 00110 0110011` | `0x00105233` |
| `BNE r0, r0, 20`      | `0000000 00000 00000 001 00001 1100011` | `0x0140A063` |
| `BEQ r0, r0, 15`      | `0000000 00000 00000 000 00000 1100011` | `0x00F0A063` |
| `LW r03, r01, 2`      | `000000000010 00001 010 00011 0000011`  | `0x00210283` |
| `SLL r05, r01, r1`    | `0000000 00001 00001 001 00101 0110011` | `0x00105033` |



#### Functional Simulation Experiment

|  **Operation**  |  **Standard RISCV ISA**  |  **Hardcoded ISA**  |  
|  :----:  |  :----:  |  :----:  |  
|  ADD R6, R2, R1  |  32'h00110333  |  32'h02208300  |  
|  SUB R7, R1, R2  |  32'h402083b3  |  32'h02209380  |  
|  AND R8, R1, R3  |  32'h0030f433  |  32'h0230a400  |  
|  OR R9, R2, R5  |  32'h005164b3  |  32'h02513480  |  
|  XOR R10, R1, R4  |  32'h0040c533  |  32'h0240c500  |  
|  SLT R1, R2, R4  |  32'h0045a0b3  |  32'h02415580  |  
|  ADDI R12, R4, 5  |  32'h004120b3  |  32'h00520600  |  
|  BEQ R0, R0, 15  |  32'h00000f63  |  32'h00f00002  |  
|  SW R3, R1, 2  |  32'h0030a123  |  32'h00209181  |  
|  LW R13, R1, 2  |  32'h0020a683  |  32'h00208681  |  
|  SRL R16, R14, R2  |  32'h0030a123  |  32'h00271803  |
|  SLL R15, R1, R2  |  32'h002097b3  |  32'h00208783  |   

Install iverilog and gtkwave using the following commands:

```
sudo apt get update
sudo apt get install iverilog gtkwave
```

Clone the following repository and download the netlist files for simulation 

```
git clone https://github.com/vinayrayapati/iiitb_rv32i
cd iiitb_rv32i
```

![image](https://github.com/user-attachments/assets/779e05a1-1361-47e0-b7fe-5247c6c22481)

Simulate and run the verilog code

```
iverilog -o iiitb_rv32i iiitb_rv32i.v iiitb_rv32i_tb.v
./iiitb_rv32i
```

```
gtkwave iiitb_rv32i.vcd
```

![image](https://github.com/user-attachments/assets/67a6ca8b-1e1d-4773-86be-54d22f4819d7)


#### Output Waveforms for the Hardcoded Code

Hardcoded instructions
![image](https://github.com/user-attachments/assets/6cac004f-5aa7-46e3-82a3-a88d2dce3059)

Output waveform for Hardcoded Instructions
![image](https://github.com/user-attachments/assets/bf582bb0-d860-4ddd-bc88-aa3b49faf6f3)

- Waveform for Hardcoded Instruction: `add r6, r1, r2`

![image](https://github.com/user-attachments/assets/c02e2869-7cec-4d93-be52-9e174af1998c)

- Waveform for above command

![image](https://github.com/user-attachments/assets/6357d0d6-de43-4452-8875-974f0d7e0b67)

- Hardcoded Instruction: `sub r7, r1, r2`

![image](https://github.com/user-attachments/assets/595f28d5-92a2-49b8-849c-a6887f60024b)

- Waveform for above command

  ![image](https://github.com/user-attachments/assets/89408c83-3a7d-40b5-a7ba-17c4c2c0097c)


- Hardcoded Instruction: `and r8, r1, r3`

![image](https://github.com/user-attachments/assets/fc1380a7-cd67-4506-83d4-23175cb2f07d)

- Waveform for above command

  ![image](https://github.com/user-attachments/assets/d8d85c62-6c45-47c7-9016-be259b31b464)


- Hardcoded Instruction: `or r9, r2, r5`

![image](https://github.com/user-attachments/assets/36a6559d-adfd-468b-bbdc-2f7825278f78)

- Waveform for above command

- ![image](https://github.com/user-attachments/assets/eba53fe1-d3a3-4ca3-8cba-2354ed103ef3)


- Hardcoded Instruction: `xor r10, r1, r4`

![image](https://github.com/user-attachments/assets/d8c5c654-4e4d-479a-bd38-e63c21264109)

- Waveform for above command
![image](https://github.com/user-attachments/assets/a1b659d2-530f-46f7-9ce5-2bbb8933e310)


- Hardcoded Instruction: `slt r11, r2, r4`
![image](https://github.com/user-attachments/assets/27959424-668e-45aa-95cd-a156461826fa)

- Waveform for above command

  ![image](https://github.com/user-attachments/assets/512a465e-f6c8-4c53-ac93-eddc0e579761)

  
- Hardcoded Instruction: `addi r12, r4, 5`

![image](https://github.com/user-attachments/assets/6eac58ed-5781-4570-ba06-b57c895c56e6)
- Waveform for above command
  ![image](https://github.com/user-attachments/assets/86ad1d71-59f3-41ec-bcb4-21bf9cb7bd13)


- Hardcoded Instruction: `sw r3, r1, 2`

![image](https://github.com/user-attachments/assets/5ba6e263-3e0c-41fa-b6e7-ba2b89844784)
- Waveform for above command

![image](https://github.com/user-attachments/assets/0305c1fe-37a9-46f8-9408-de4177816616)


- Hardcoded Instruction: `lw r13, r1, 2`

![image](https://github.com/user-attachments/assets/7331b284-accf-451b-bf83-5e9d3d4a61e9)
- Waveform for above command

  ![image](https://github.com/user-attachments/assets/14b155af-7dba-4e48-94be-7d6234d55b7d)


- Hardcoded Instruction: `beq r0, r0, 15`
![image](https://github.com/user-attachments/assets/d3647f62-a32c-4d8a-bf55-c8df1d1a20bc)
- Waveform for above command
![image](https://github.com/user-attachments/assets/e0268400-84cc-4f95-a78b-392a028288df)


- Hardcoded Instruction: `add r14, r2, r2`

![image](https://github.com/user-attachments/assets/be01d386-8941-4749-8cfe-b3727b198029)
- Waveform for above command
  ![image](https://github.com/user-attachments/assets/97662cd6-2dc8-41b0-b12f-f6380e862869)


- Hardcoded Instruction: `bne r0, r1, 20`

![image](https://github.com/user-attachments/assets/c79334e9-866c-433f-9a69-5182732a9c8b)
- Waveform for above command

  ![image](https://github.com/user-attachments/assets/a3932106-b0d2-4c04-b319-085b97ea8205)


- Hardcoded Instruction: `sll r15, r1, r2(2)`

![image](https://github.com/user-attachments/assets/509433f0-a79a-433f-a0bf-65e85182ad16)
- Waveform for above command

  ![image](https://github.com/user-attachments/assets/a29f1a1f-12a6-4dea-8dbe-9b73cdf1d97b)

We can observe that there is a waveform difference













 




