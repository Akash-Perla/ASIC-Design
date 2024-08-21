# ASIC-Design

## Contents

- [Task 1: A C program which calculates the sum of all numbers up to 'n'](#task-1-a-c-program-which-calculates-the-sum-of-all-numbers-up-to-n)
- [Task 2: Spike simulation](#task-2-spike-simulation)
- [Task 3: Functional simulation experiment](#task-3-functional-simulation-experiment)
- [Task 4: A C program which does a binary search on a sorted array and its Spike simulation](#task-4-a-c-program-which-does-a-binary-search-on-a-sorted-array-and-its-spike-simulation)
- [Task 5: A 5 stage RISCV processor](#task-5-a-5-stage-riscv-processor)


## Task-1: A C program which calculates the sum of all numbers upto 'n'

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

## Task-2: Spike simulation

- Run the `sum1ton.o` in the Spike simulator in order to debug the code.

![image](https://github.com/user-attachments/assets/377b644a-8fa3-47d7-860a-55999ba44559)

- This runs the `sum1ton.o` object file on the Spike RISC-V simulator with the Proxy Kernel and enables debugging mode.

![image](https://github.com/user-attachments/assets/04899006-ed76-4c1a-9ba4-bc28c07a7a25)

- We now bring the PC (program counter) to the start of the main function. We then check the contents of register `a2` before and after running the instructions. After executing the commands, we observe that the registers `a0` and `a2` are properly loaded with appropriate values.

![image](https://github.com/user-attachments/assets/8428f4bd-f3d0-41b5-b5c1-2af564ffa88f)

- We now bring the PC (program counter) to the location `100b8`. The addition of -16 (i.e., -10 in hexadecimal) has been executed properly.

![image](https://github.com/user-attachments/assets/8411cfe4-8c8a-4ebd-bb9c-3340856ab9c1)

The debugging process is successful.

## Task-3: Funtional simulation experiment

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

![image](https://github.com/user-attachments/assets/2becae8a-c60e-430b-aa3a-e003c1543cab)


- Hardcoded Instruction: `sub r7, r1, r2`

![image](https://github.com/user-attachments/assets/595f28d5-92a2-49b8-849c-a6887f60024b)

- Waveform for above command

 ![image](https://github.com/user-attachments/assets/26519470-874e-4716-9378-72ecdbeb3b7b)



- Hardcoded Instruction: `and r8, r1, r3`

![image](https://github.com/user-attachments/assets/fc1380a7-cd67-4506-83d4-23175cb2f07d)

- Waveform for above command

![image](https://github.com/user-attachments/assets/8ec67817-a5f2-4668-a448-2ecca2bd4d88)



- Hardcoded Instruction: `or r9, r2, r5`

![image](https://github.com/user-attachments/assets/36a6559d-adfd-468b-bbdc-2f7825278f78)

- Waveform for above command

![image](https://github.com/user-attachments/assets/45fe8941-ae28-45b6-a536-51065b7df66e)


- Hardcoded Instruction: `xor r10, r1, r4`

![image](https://github.com/user-attachments/assets/d8c5c654-4e4d-479a-bd38-e63c21264109)

- Waveform for above command

![image](https://github.com/user-attachments/assets/afbcd58a-848a-4115-b979-0bfa43a6f95b)


- Hardcoded Instruction: `slt r11, r2, r4`
![image](https://github.com/user-attachments/assets/27959424-668e-45aa-95cd-a156461826fa)

- Waveform for above command

 ![image](https://github.com/user-attachments/assets/43951a67-e816-437e-b32b-1fb46dd9bb27)

 
- Hardcoded Instruction: `addi r12, r4, 5`

![image](https://github.com/user-attachments/assets/6eac58ed-5781-4570-ba06-b57c895c56e6)
- Waveform for above command
![image](https://github.com/user-attachments/assets/9388869a-4130-4797-8290-c34921850294)



- Hardcoded Instruction: `sw r3, r1, 2`

![image](https://github.com/user-attachments/assets/5ba6e263-3e0c-41fa-b6e7-ba2b89844784)
- Waveform for above command

![image](https://github.com/user-attachments/assets/895f1cc6-9e0a-48f8-a685-9d58d7ccc377)


- Hardcoded Instruction: `lw r13, r1, 2`

![image](https://github.com/user-attachments/assets/7331b284-accf-451b-bf83-5e9d3d4a61e9)
- Waveform for above command
![image](https://github.com/user-attachments/assets/c11326ad-c03a-410c-8358-cfd49ee2d937)

 


- Hardcoded Instruction: `beq r0, r0, 15`
![image](https://github.com/user-attachments/assets/d3647f62-a32c-4d8a-bf55-c8df1d1a20bc)
- Waveform for above command
  ![image](https://github.com/user-attachments/assets/ac0e5326-903e-4787-9b83-6019cebc8fd5)



- Hardcoded Instruction: `add r14, r2, r2`

![image](https://github.com/user-attachments/assets/be01d386-8941-4749-8cfe-b3727b198029)
- Waveform for above command
  ![image](https://github.com/user-attachments/assets/a932a5ba-0add-4369-8194-f402da7c97b2)




- Hardcoded Instruction: `bne r0, r1, 20`

![image](https://github.com/user-attachments/assets/c79334e9-866c-433f-9a69-5182732a9c8b)
- Waveform for above command

 ![image](https://github.com/user-attachments/assets/09a44ba8-10d1-4ee4-8abb-9bea6a1a3444)



- Hardcoded Instruction: `sll r15, r1, r2(2)`

![image](https://github.com/user-attachments/assets/509433f0-a79a-433f-a0bf-65e85182ad16)
- Waveform for above command
![image](https://github.com/user-attachments/assets/2dcaa7b3-156a-4837-a37f-afbbacc2547e)



We can observe that there is a waveform difference

## Task-4: A C program which does a binary search on a sorted array and its Spike simulation

- We first create a new file named `binary_search.c` which does a binary search on a sorted array. The following is the code for the same:
![image](https://github.com/user-attachments/assets/18736546-3840-426f-bd2d-da6ef792c76c)

- The code is compiled using the command:
  ```
  gcc binary_search.c
  ./a.out
  ```

- The output is shown below:

![image](https://github.com/user-attachments/assets/c624c1f8-cf61-4e62-8270-0c6da4efd88f)

- Now, we compile the C program using the RISC-V compiler with O1 optimization


![image](https://github.com/user-attachments/assets/e3cbfa94-e2ee-4e10-83bb-5ef99359078e)


- Now, we create the object file `binary_search.o`


![image](https://github.com/user-attachments/assets/22b7038b-fd21-49ca-9570-d09b3eebe132)

- As soon as we press the Enter key, a huge list of opcodes is displayed on the terminal. But our focus is on the main section of the program. Type :/main to navigate to that portion.

![image](https://github.com/user-attachments/assets/1894f856-8169-4ed0-aa2c-10fc6530dfb1)

- The number of instructions are 1C(in hex) i.e 28(in decimal)
  
![image](https://github.com/user-attachments/assets/0fa0021c-e3b6-4b45-b14c-83281b4564ae)

- Next, we compile the C program using the RISC-V compiler with Ofast optimization.

![image](https://github.com/user-attachments/assets/55751db5-f47d-4918-b9df-e0cd00413101)


- Now, we create the object file `binary_search.o`

![image](https://github.com/user-attachments/assets/63042529-3e96-4360-b93d-84a6d1f970e3)

  
-  As soon as we press the Enter key, a huge list of opcodes is displayed on the terminal. But our focus is on the main section of the program. Type :/main to navigate to that portion.

![image](https://github.com/user-attachments/assets/cf6cd01c-088e-4051-8b77-055116979bd9)

- The number of instructions are 46

![image](https://github.com/user-attachments/assets/5d5b4e72-1696-49b6-9575-98127d83367a)

#### Spike simulation

- Run the `binary_search.o` in the Spike simulator in order to debug the code.

 ![image](https://github.com/user-attachments/assets/d5ff2224-3e15-4818-a71c-a62ef1cfd693)
  
- We now bring the PC (program counter) to the start of the main function using the command 'until pc 0 100b0'. We then check the contents of register 'a5' before and after running the instructions. After executing the commands, we observe that the registers 'a5' is properly loaded with appropriate values.

![image](https://github.com/user-attachments/assets/d3983438-9fa7-496d-94ed-9326a4784581)

- Debugging process is successful

## Task-5: A 5 stage RISCV processor

#### Day-3 Makerchip Tutorial (Lab: Combinational Logic)

- Inverter

  
Truth Table of an Inverter

![image](https://github.com/user-attachments/assets/d0e7ea18-a5e1-4cd1-aa9d-a64f437d1ad0)

Inverter design using Makerchip
 ![image](https://github.com/user-attachments/assets/e8f39f56-3636-4454-aefe-d0a296baad36)

- 2 AND(&&)
  
Truth Table of an AND
 
![image](https://github.com/user-attachments/assets/48b3dbc6-6adb-444b-8c66-271eefa0a30b)


AND design using Makerchip
![image](https://github.com/user-attachments/assets/8b636662-cbc7-4675-a14e-c6c55292783c)

 
  
- 2 OR(||)

Truth Table of an OR
 
![image](https://github.com/user-attachments/assets/2cf25436-c1b4-4ef7-89be-ede234c6852e)


OR design using Makerchip
![image](https://github.com/user-attachments/assets/d3c5635b-9eed-4ddf-a53a-974b69d517a3)

  
  
- 2 XOR(^)

Truth Table of an Xor

![image](https://github.com/user-attachments/assets/d0e7ea18-a5e1-4cd1-aa9d-a64f437d1ad0)

Xor design using Makerchip

![image](https://github.com/user-attachments/assets/bb02fff5-bf47-444b-85b5-91df695d0e5f)

- Vectors

![image](https://github.com/user-attachments/assets/1649f0b9-8859-419c-aa8a-43811053ddaf)

- 2:1 Mux

![image](https://github.com/user-attachments/assets/1f00099f-dd45-402f-8efc-b7886d2a5799)

- 2:1 Mux using vectors

![image](https://github.com/user-attachments/assets/3c97f795-b415-4c36-ab51-ec73aa95592b)


- Combinational Calculator

![image](https://github.com/user-attachments/assets/fb1dd3da-6776-47a1-9520-69d858eb8ff5)

#### Day-3 Makerchip Tutorial (Lab: Sequential Logic)

- Fibonacci

![image](https://github.com/user-attachments/assets/ebd8bbee-590f-43a0-9f62-aa8a7c07a900)

- Free running counter

![image](https://github.com/user-attachments/assets/badf4ccf-5d1c-4c5e-8993-3d1fefea488d)
  
- Sequential Calculator

![image](https://github.com/user-attachments/assets/5da9a4b7-ad89-47da-912d-0e399361134b)

  
#### Day-3 Makerchip Tutorial (Lab: Pipelined Logic)  

- Error Detection Demo

Diagram

![image](https://github.com/user-attachments/assets/4d13588f-afb4-4590-add5-ecac2d84fd24)

Using Makerchip

![image](https://github.com/user-attachments/assets/caebc3b9-8a7a-42f5-92ab-b76bdc969e8b)

- Counter and Calculator

Diagram

![image](https://github.com/user-attachments/assets/491e8f5a-17b8-49c2-969b-9f9dd90c6509)

Using Makerchip

![image](https://github.com/user-attachments/assets/bd8cd0dc-366a-44d7-b0a1-2c6a50f1ecab)


- 2 cycle calculator

Diagram

![image](https://github.com/user-attachments/assets/ac702c71-3abf-4c73-bdb4-a9dbe71b1b2d)

Using Makerchip

![image](https://github.com/user-attachments/assets/671f8a6b-4598-4c97-b64f-ce4767b77137)

#### Day-3 Makerchip Tutorial (Lab: Validity)

- Distance Calculator

Diagram

![image](https://github.com/user-attachments/assets/aa759b95-2fda-49ce-ace0-3ce3f66f36a7)


Using Makerchip

![image](https://github.com/user-attachments/assets/20a31855-c589-40cd-8c20-53ba9496c067)


- 2 Cycle Calculator
  
Diagram

![image](https://github.com/user-attachments/assets/32423d45-3d4a-40bb-8f69-f154854726e9)


Using Makerchip

![image](https://github.com/user-attachments/assets/3a88146d-c46f-4b42-8907-e5ac3ff8ce1d)

- Calculator with Single Value Memory

Diagram

![image](https://github.com/user-attachments/assets/ecfb657f-e228-44be-a9d1-c3c6d2c0c9fd)


Using Makerchip

![image](https://github.com/user-attachments/assets/7bf248bb-f7b9-4ac0-ae2e-10378a750baa)

#### Day-4 Basic RISC-V CPU core Micro-architecture

Diagram

![image](https://github.com/user-attachments/assets/cb869897-0f89-46db-9ba7-26680e40a8e5)

The basic components are:

1. **Program Counter (PC)**: A CPU register that tracks the memory address of the next instruction to fetch and execute.

2. **Instruction Decoder**: A circuit that interprets and decodes machine instructions, generating control signals for CPU operations.

3. **Instruction Memory**: A storage component holding the program's machine instructions, fetched using the program counter.

4. **Data Memory**: A storage component used to store and manipulate data during program execution; it supports both read and write operations.

5. **ALU (Arithmetic Logic Unit)**: A digital circuit that performs arithmetic and logical operations, such as addition, subtraction, and bitwise operations.

6. **Read Register File**: A set of registers used to store data during instruction execution, providing operands for ALU operations.

7. **Write Register File**: Stores the results of operations back into registers, ensuring updated data is available for subsequent instructions.

- Program Counter

![image](https://github.com/user-attachments/assets/ea1162a7-1424-4c93-808e-7c3c49f0627f)

- Instruction Fetch

![image](https://github.com/user-attachments/assets/790390c2-5c52-44aa-9573-5a68f1f1538a)


- Instruction Decode

![image](https://github.com/user-attachments/assets/19c080f3-6100-4125-8609-9f732ac509f2)

- Register File Read

![image](https://github.com/user-attachments/assets/92533982-4df7-4175-85f9-75a626b13bcf)


- ALU

![image](https://github.com/user-attachments/assets/b522b87e-1f62-4a88-b327-0dee59f51c23)

- Register File Write

![image](https://github.com/user-attachments/assets/84dc9eb0-214a-4061-ae1e-eac5bd74be5d)


- Branch Instructions

![image](https://github.com/user-attachments/assets/ae1dc245-0e37-4571-9ca9-f702b240bf4b)

To test the code using the testbech we include the line `*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9) ;` in @1 stage

![image](https://github.com/user-attachments/assets/e557fea9-c588-429f-b272-f2e5ea17e887)

#### Day-5 Complete Pipelined RISC-V CPU Micro-architecture


Pipelining can introduce hazards that disrupt instruction execution. A key hazard is the "branch instruction hazard" or "branch penalty."

###### Types of Hazards:

1. **Structural Hazard**: Occurs when multiple instructions compete for the same resource, causing pipeline stalls.

2. **Data Hazard**: Arises when an instruction depends on the result of a previous instruction that hasn't completed yet, potentially leading to incorrect results.

3. **Control Hazard (Branch Hazard)**: Happens due to uncertainty in whether a branch will be taken. If a branch prediction is wrong, the pipeline must be flushed, leading to a performance penalty.

- Final 4 stage Pipeline Logic


![image](https://github.com/user-attachments/assets/c1f534f7-ec55-48fd-9b64-60c1698d12c9)



 



















 




