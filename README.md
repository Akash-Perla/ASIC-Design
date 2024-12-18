
## Contents

- [Task 1: A C program which calculates the sum of all numbers up to 'n'](#task-1-a-c-program-which-calculates-the-sum-of-all-numbers-up-to-n)
- [Task 2: Spike simulation](#task-2-spike-simulation)
- [Task 3: Functional simulation experiment](#task-3-functional-simulation-experiment)
- [Task 4: A C program which does a binary search on a sorted array and its Spike simulation](#task-4-a-c-program-which-does-a-binary-search-on-a-sorted-array-and-its-spike-simulation)
- [Task 5: A 5 stage RISCV processor](#task-5-a-5-stage-riscv-processor)
- [Task 6: TLV to Verilog](#task-6-tlv-to-verilog)
- [Task 7: Generate PLL and DAC output waveforms](#task-7-Generate-PLL-and-dac-output-waveforms)
- [Task 8: RTL Design using Verilog with Sky130 Technology](#task-8-RTL-Design-using-Verilog-with-Sky130-Technology)
- [Task 9: Synthesize RISC-V and compare output with functional simulations](#task-9-Synthesize-RISC-V-and-compare-output-with-functional-simulations)
- [Task 10: Post Synthesis Static Timing Analysis using OpenSTA](#task-10-Post-Synthesis-Static-Timing-Analysis-using-OpenSTA)
- [Task 11: Post Synthesis Static Timing Analysis using OpenSTA for all the sky130 lib files](#task-11-Post-Synthesis-Static-Timing-Analysis-using-OpenSTA-for-all-the-sky130-lib-files)
- [Task 12: Advanced Physical Design using OpenLane using Sky130 ](#task-12-Advanced-Physical-Design-using-OpenLane-using-Sky130)
- [Task 13: OpenRoad Physical Design ](#task-13-OpenRoad-Physical-Design)
  
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

Final Code

```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1011)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_aka = *clk;
         //$pc[31:0] = >>1$reset ? 0 : ( >>1$pc + 31'h4 );
         
         $pc[31:0] = (>>1$reset) ? '0 :
                     (>>1$taken_br) ? >>1$br_tgt_pc : >>1$pc + 32'd4;

         
         $imem_rd_en = >>1$reset ? 0 : 1;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
      @1
         $instr[31:0] = $imem_rd_data[31:0];
         
         //decode
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b10100;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         //imm decode
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                      32'b0;
         
         //decode logic for other fields
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
            
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
            
         $funct7_valid = $is_r_instr ;
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
            
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         
         //RF read and enable
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         
         // ALU
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value : 32'bx ;
                         
         //RF write and enable
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         
         //branch
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
         
         $br_tgt_pc[31:0] = $pc + $imm;
         

         
      

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = |cpu/xreg[14]>>5$value == (1+2+3+4+5+6+7+8+9) ;
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)

   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule

```

To test the code using the testbech we include the line `*passed = |cpu/xreg[14]>>5$value == (1+2+3+4+5+6+7+8+9) ;` in @1 stage

![image](https://github.com/user-attachments/assets/21caf487-7a62-4a03-b0b8-12189532e527)

![image](https://github.com/user-attachments/assets/e641b1bc-e2f4-4669-a54d-d70469a84860)

![image](https://github.com/user-attachments/assets/c76f9237-ff2e-4f4e-8265-eae0bff09918)

![image](https://github.com/user-attachments/assets/6d54738d-1e10-4f4d-9e72-bb38f028b51a)


The sum of numbers from 1 to 9 is 45(i.e 2D in hex) which is verified in the waveform for `|cpu/xreg[14]` in the above figure



#### Day-5 Complete Pipelined RISC-V CPU Micro-architecture


Pipelining can introduce hazards that disrupt instruction execution. A key hazard is the "branch instruction hazard" or "branch penalty."

###### Types of Hazards:

1. **Structural Hazard**: Occurs when multiple instructions compete for the same resource, causing pipeline stalls.

2. **Data Hazard**: Arises when an instruction depends on the result of a previous instruction that hasn't completed yet, potentially leading to incorrect results.

3. **Control Hazard (Branch Hazard)**: Happens due to uncertainty in whether a branch will be taken. If a branch prediction is wrong, the pipeline must be flushed, leading to a performance penalty.

- Final 4 stage Pipeline Logic

Code:

```

\m4_TLV_version 1d: tl-x.org
\SV
   // Template code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 0 to 9 Program |
   // \====================/
   //
   // Add 0,1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store r10 result in dmem
   m4_asm(LW, r17, r0, 10000)           // Load contents of dmem to r17
   m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_aka = *clk;
         
         //PC fetch - branch, jumps and loads introduce 2 cycle bubbles in this pipeline
         $pc[31:0] = >>1$reset ? '0 : (>>3$valid_taken_br ? >>3$br_tgt_pc :
                                       >>3$valid_load     ? >>3$inc_pc[31:0] :
                                       >>3$jal_valid      ? >>3$br_tgt_pc :
                                       >>3$jalr_valid     ? >>3$jalr_tgt_pc :
                                                     (>>1$inc_pc[31:0]));
         // Access instruction memory using PC
         $imem_rd_en = ~ $reset;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
         
      @1
         //Getting instruction from IMem
         $instr[31:0] = $imem_rd_data[31:0];
         
         //Increment PC
         $inc_pc[31:0] = $pc[31:0] + 32'h4;
         
         //Decoding I,R,S,U,B,J type of instructions based on opcode [6:0]
         //Only [6:2] is used here because this implementation is for RV64I which does not use [1:0]
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         
         $is_r_instr = $instr[6:2] == 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] == 5'b10100;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_b_instr = $instr[6:2] == 5'b11000;
         
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         //Immediate value decode
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20]} :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7]} :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31] , $instr[30:12] , { 12{1'b0}} } :
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} :
                      >>1$imm[31:0];
         
         //Generate valid signals for each instruction fields
         $rs1_or_funct3_valid    = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid              = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid               = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct7_valid           = $is_r_instr;
         
         //Decode other fields of instruction - source and destination registers, funct, opcode
         ?$rs1_or_funct3_valid
            $rs1[4:0]    = $instr[19:15];
            $funct3[2:0] = $instr[14:12];
         
         ?$rs2_valid
            $rs2[4:0]    = $instr[24:20];
         
         ?$rd_valid
            $rd[4:0]     = $instr[11:7];
         
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         
         $opcode[6:0] = $instr[6:0];
         
         //Decode instruction in subset of base instruction set based on RISC-V 32I
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         //Branch instructions
         $is_beq   = $dec_bits ==? 11'bx_000_1100011;
         $is_bne   = $dec_bits ==? 11'bx_001_1100011;
         $is_blt   = $dec_bits ==? 11'bx_100_1100011;
         $is_bge   = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu  = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu  = $dec_bits ==? 11'bx_111_1100011;
         
         //Jump instructions
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal   = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr  = $dec_bits ==? 11'bx_000_1100111;
         
         //Arithmetic instructions
         $is_addi  = $dec_bits ==? 11'bx_000_0010011;
         $is_add   = $dec_bits ==  11'b0_000_0110011;
         $is_lui   = $dec_bits ==? 11'bx_xxx_0110111;
         $is_slti  = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_xori  = $dec_bits ==? 11'bx_100_0010011;
         $is_ori   = $dec_bits ==? 11'bx_110_0010011;
         $is_andi  = $dec_bits ==? 11'bx_111_0010011;
         $is_slli  = $dec_bits ==? 11'b0_001_0010011;
         $is_srli  = $dec_bits ==? 11'b0_101_0010011;
         $is_srai  = $dec_bits ==? 11'b1_101_0010011;
         $is_sub   = $dec_bits ==? 11'b1_000_0110011;
         $is_sll   = $dec_bits ==? 11'b0_001_0110011;
         $is_slt   = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu  = $dec_bits ==? 11'b0_011_0110011;
         $is_xor   = $dec_bits ==? 11'b0_100_0110011;
         $is_srl   = $dec_bits ==? 11'b0_101_0110011;
         $is_sra   = $dec_bits ==? 11'b1_101_0110011;
         $is_or    = $dec_bits ==? 11'b0_110_0110011;
         $is_and   = $dec_bits ==? 11'b0_111_0110011;
         
         //Store instructions
         $is_sb    = $dec_bits ==? 11'bx_000_0100011;
         $is_sh    = $dec_bits ==? 11'bx_001_0100011;
         $is_sw    = $dec_bits ==? 11'bx_010_0100011;
         
         //Load instructions - support only 4 byte load
         $is_load  = $dec_bits ==? 11'bx_xxx_0000011;
         
         $is_jump = $is_jal || $is_jalr;
         
      @2
         //Get Source register values from reg file
         $rf_rd_en1 = $rs1_or_funct3_valid;
         $rf_rd_en2 = $rs2_valid;
         
         $rf_rd_index1[4:0] = $rs1[4:0];
         $rf_rd_index2[4:0] = $rs2[4:0];
         
         //Register file bypass logic - data forwarding from ALU to resolve RAW dependence
         $src1_value[31:0] = $rs1_bypass ? >>1$result[31:0] : $rf_rd_data1[31:0];
         $src2_value[31:0] = $rs2_bypass ? >>1$result[31:0] : $rf_rd_data2[31:0];
         
         //Branch target PC computation for branches and JAL
         $br_tgt_pc[31:0] = $imm[31:0] + $pc[31:0];
         
         //RAW dependence check for ALU data forwarding
         //If previous instruction was writing to reg file, and current instruction is reading from same register
         $rs1_bypass = >>1$rf_wr_en && (>>1$rd == $rs1);
         $rs2_bypass = >>1$rf_wr_en && (>>1$rd == $rs2);
         
      @3
         //ALU
         $result[31:0] = $is_addi  ? $src1_value +  $imm :
                         $is_add   ? $src1_value +  $src2_value :
                         $is_andi  ? $src1_value &  $imm :
                         $is_ori   ? $src1_value |  $imm :
                         $is_xori  ? $src1_value ^  $imm :
                         $is_slli  ? $src1_value << $imm[5:0]:
                         $is_srli  ? $src1_value >> $imm[5:0]:
                         $is_and   ? $src1_value &  $src2_value:
                         $is_or    ? $src1_value |  $src2_value:
                         $is_xor   ? $src1_value ^  $src2_value:
                         $is_sub   ? $src1_value -  $src2_value:
                         $is_sll   ? $src1_value << $src2_value:
                         $is_srl   ? $src1_value >> $src2_value:
                         $is_sltu  ? $sltu_rslt[31:0]:
                         $is_sltiu ? $sltiu_rslt[31:0]:
                         $is_lui   ? {$imm[31:12], 12'b0}:
                         $is_auipc ? $pc + $imm:
                         $is_jal   ? $pc + 4:
                         $is_jalr  ? $pc + 4:
                         $is_srai  ? ({ {32{$src1_value[31]}} , $src1_value} >> $imm[4:0]) :
                         $is_slt   ? (($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]}):
                         $is_slti  ? (($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]}) :
                         $is_sra   ? ({ {32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $is_load  ? $src1_value +  $imm :
                         $is_s_instr ? $src1_value + $imm :
                                    32'bx;
         
         $sltu_rslt[31:0]  = $src1_value <  $src2_value;
         $sltiu_rslt[31:0] = $src1_value <  $imm;
         
         //Jump instruction target PC computation
         $jalr_tgt_pc[31:0] = $imm[31:0] + $src1_value[31:0]; 
         
         //Branch resolution
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) :
                     1'b0;
         
         //Current instruction is valid if one of the previous 2 instructions were not (taken_branch or load or jump)
         $valid = ~(>>1$valid_taken_br || >>2$valid_taken_br || >>1$is_load || >>2$is_load || >>2$jump_valid || >>1$jump_valid);
         
         //Current instruction is valid & is a taken branch
         $valid_taken_br = $valid && $taken_br;
         
         //Current instruction is valid & is a load
         $valid_load = $valid && $is_load;
         
         //Current instruction is valid & is jump
         $jump_valid = $valid && $is_jump;
         $jal_valid  = $valid && $is_jal;
         $jalr_valid = $valid && $is_jalr;
         
         //Destination register update - ALU result or load result depending on instruction
         $rf_wr_en = (($rd != '0) && $rd_valid && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = $valid ? $rd[4:0] : >>2$rd[4:0];
         $rf_wr_data[31:0] = $valid ? $result[31:0] : >>2$ld_data[31:0];
         
      @4
         //Data memory access for load, store
         $dmem_addr[3:0]     =  $result[5:2];
         $dmem_wr_en         =  $valid && $is_s_instr;
         $dmem_wr_data[31:0] =  $src2_value[31:0];
         $dmem_rd_en         =  $valid_load;
         
      
         //Write back data read from load instruction to register
         $ld_data[31:0]      =  $dmem_rd_data[31:0];
         
      
      

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   //Checks if sum of numbers from 1 to 9 is obtained in reg[17] and runs 10 cycles extra after this is met
   *passed = |cpu/xreg[14]>>10$value == (1+2+3+4+5+6+7+8+9);
   //Run for 200 cycles without any checks
   //*passed = *cyc_cnt > 200;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule

```

![image](https://github.com/user-attachments/assets/2c611a07-d54e-4c84-8b3b-35a5e582960d)

![image](https://github.com/user-attachments/assets/dfff4909-118b-4057-800a-3604f950c106)

![image](https://github.com/user-attachments/assets/ac25da23-5fe2-4a27-afd2-65f50a3bd634)

![image](https://github.com/user-attachments/assets/e97d390e-c275-440a-800e-b9a5602b0bf9)

![image](https://github.com/user-attachments/assets/42700a78-af27-4392-8ed9-dce199cc43bc)

The sum of numbers from 1 to 9 is 45(i.e 2D in hex) which is verified in the waveform for `|cpu/xreg[14]` in the above figure

## Task-6: TLV to Verilog

We will first set-up a development environment for working with simulation and synthesis tools using the below commands:

```
sudo apt install make python python3 python3-pip git iverilog gtkwave
cd ~
sudo apt-get install python3-venv
python3 -m venv .venv
source ~/.venv/bin/activate
pip3 install pyyaml click sandpiper-saas
```

![image](https://github.com/user-attachments/assets/46cf40a8-1a09-4ab9-9e0c-2fcfd04ba9c4)

```
sudo apt install make python python3 python3-pip git iverilog gtkwave docker.io
sudo chmod 666 /var/run/docker.sock
cd ~
pip3 install pyyaml click sandpiper-saas
```

![image](https://github.com/user-attachments/assets/7e1a581a-22f6-42f2-9619-29b0930e7d0f)

```
cd ~
git clone https://github.com/manili/VSDBabySoC.git
cd /home/vsduser/VSDBabySoC
make pre_synth_sim
```

![image](https://github.com/user-attachments/assets/7100db7f-502b-4130-88d4-39fad175fa0a)

Now, we replace the rvmyth.tlv file in the VSDBabySoC/src/module folder with our RISC-V design from makerchip .tlv file which is to be converted into verilog and also we change the testbench according to our makerchip code.

Inorder to get verilog code of our TLV code ie, to translate .tlv definition of RISC-V into .v definition use the following code.

```
sandpiper-saas -i ./src/module/rvmyth.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```

![image](https://github.com/user-attachments/assets/2c2dd542-3723-46d2-b9da-172d0663c892)

Now we compile and simulate RISC-V design

```
iverilog -o output/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module
```

Result of the simulation (i.e. pre_synth_sim.vcd) is stored in the output/pre_synth_sim directory

```
cd output
./pre_synth_sim.out
```
![image](https://github.com/user-attachments/assets/fb83007f-21be-46b4-8131-2234b0d9eead)

Now,

```
gtkwave pre_synth_sim.vcd
```

#### Pre-synthesis Simulation results: Signals to plot are the following:

- clk_aka: Clock input to the RISC-V core.
- reset: Reset signal to the RISC-V core.
- OUT[9:0]: 10-bit output [9:0] OUT port of the RISC-V core. This port comes from the RISC-V register #14, originally.

GTKWave Waveforms:

![image](https://github.com/user-attachments/assets/3dfdaea2-f3c3-4694-95aa-e1a910ac3dfb)

![image](https://github.com/user-attachments/assets/80a2e77f-c24c-426d-9419-5d5af8bdd2cb)

![image](https://github.com/user-attachments/assets/cc1b2800-e5f9-4ef1-a733-b8aa96e23268)

Makerchip Waveforms:

![image](https://github.com/user-attachments/assets/c08ea09c-bec9-4627-83b4-9cea716ddcb8)

![image](https://github.com/user-attachments/assets/c69b0bdf-313c-4ab0-b1e4-74e52c333941)

![image](https://github.com/user-attachments/assets/6644ae4f-0905-4570-96fa-66f3a80066c4)

We can observe the gradual increment in sum from 0 to 9 and at the end the sum of numbers from 0 to 9 is 45 which is Ox2D in hexadecimal which is observed in the waveform.

## Task-7: Generate PLL and DAC output waveforms

Verilog and GTKWave Installation:

![image](https://github.com/user-attachments/assets/a9d04d02-7714-4faf-bf0d-58c9a04da345)

Yosys Installation:

![image](https://github.com/user-attachments/assets/a2f39896-07ac-469a-903f-95c8706b9fb2)

We first clone the BabySoC_Simulation repository:

```
git clone https://github.com/Subhasis-Sahu/BabySoC_Simulation.git
```

Then edit the top level code:

![image](https://github.com/user-attachments/assets/efe5a061-799f-42f7-86cb-d11936fbc965)

Then run the following commands:

```
cd BabySoC_Simulation
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```

Output Waveforms:

![image](https://github.com/user-attachments/assets/b9ae62f9-6664-49a4-9f4d-3fa3629fc04a)

![image](https://github.com/user-attachments/assets/81df3f22-c148-4c14-a82d-ecd128f87aba)

## Task-8: RTL Design using Verilog with Sky130 Technology

### Day 1: Introduction to Verilog RTL Design and Synthesis

Simulator is a tool used to check if it adheres to the designed specifications by simualating the code. Simulator looks for the changes on the input signals and upon change to the input the output is evaluated. RTL design is the Verilog code that implements a circuit. To verify it, a testbench is written and simulated using Icarus Verilog. The VCD(Value Change Dump) file generated is viewed using GTKWave to debug and verify the design's functionality. GTKWave allows users to load and inspect waveforms generated during the simulation, helping them understand signal interactions, timing relationships, and overall circuit behavior.

The below is the Iverilog based Simulation Flow

![image](https://github.com/user-attachments/assets/7da43121-8525-4e69-9543-694f9b843260)

Set up the tool flow using the below commands:

```
mkdir ASIC
cd ASIC
git clone https://github.com/kunalg123/vsdflow.git
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```

![image](https://github.com/user-attachments/assets/42113764-02f5-4872-bc1e-2ece969ef0d8)


Command to view the folder structure of the lab, and list the contents of the directory:

```
cd sky130RTLDesignAndSynthesisWorkshop
ls -R
```

![image](https://github.com/user-attachments/assets/736aa42f-afa3-4a9b-9575-d33f07d6dead)

The below consists of the verilog files used in this lab:

![image](https://github.com/user-attachments/assets/75b475ae-e94f-4b61-a6d6-fed3c0496054)

There are a number of verilog designs and testbench files for simulation. Run the following commands to simulate the verilog code 'good_mux.v'.
The first line will compile and check for syntax errors in both the design and testbench. An executable file 'a.out' is generated on successful compilation. On executing a.out, a vcd file is generated that captures changes in the input and output values. GTKWave is used to view the waveforms

```
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```

![image](https://github.com/user-attachments/assets/05acc3e9-249e-46af-bd2f-afdc0c6ffef2)

![image](https://github.com/user-attachments/assets/a3210335-6fef-4b0e-b305-76382009e1bc)

**Code for good_mux.v :**

```
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule

```

**Code for tb_good_mux.v :**

```
`timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule

```

Synthesizer is the tool used for converting the RTL to netlist. Yosys is one such open source synthesizer. Yosys optimizes the design, mapping it to specific target technology libraries or FPGA architectures, and generates an optimized netlist that can be further analyzed and prepared for physical layout and fabrication.

**Yosys Flow**

![image](https://github.com/user-attachments/assets/b70ab253-cba9-41eb-9d5b-ad23971384cd)

**Verify the Synthesis**

The same testbench that is used for the simulation can be used for the synthesized netlist as well.

![image](https://github.com/user-attachments/assets/6e56fdd0-c17e-4dad-b4c2-0b8c3828b904)


Synthesis has three steps: RTL to Gate level translation, The design is then converted into gates and the connections are made between the gates and the output is given out as a file called netlist

![image](https://github.com/user-attachments/assets/2922bb42-598d-4303-a9fc-697789ebace9)

**Liberty(.lib):** Its a collection of logical modules. It includes basic logic gates like And, Or, Not, etc... and it contains different variants of the same gate ike 2input, 3input, 4input, slow, fast, medium gates etc. Fast cells are used if only high performance is needed. Slower cells is used to address hold time issues. IThe selection of faster cells in digital circuit design can increase area and power consumption while potentially leading to hold time violations. Conversely, excessive use of slower cells can result in suboptimal performance. The optimal cell selection for synthesis is guided by constraints that balance area, power, and timing requirements.


The below is the Synthesis(Illustration)

![image](https://github.com/user-attachments/assets/6afc2127-2b77-4ab7-98ed-ee521977ec1c)

Use the below commands for synthesis:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verlog good_mux_netlist.v
write_verilog -noattr good_mux_netlist.v
```

Output:

![image](https://github.com/user-attachments/assets/65454f0d-109b-423a-a7e2-d15780aa1aab)

![image](https://github.com/user-attachments/assets/d0b5a95f-0c0a-4b68-982d-10006987aed3)

![image](https://github.com/user-attachments/assets/339d285b-8c78-4864-a795-030c012b6bd7)


### Day 2: Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

Run the below commands to view the contents inside the .lib file:

```
cd ASIC/sky130RTLDesignAndSynthesisWorkshop/lib/
vim sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://github.com/user-attachments/assets/d5dbfd3c-5f89-42b7-9505-2e5946717169)

The liberty(.lib) files store PVT parameters (Process, Voltage, Temperature). Variations in these parameters can significantly affect circuit performance. Manufacturing variations, voltage fluctuations, and temperature changes all contribute to this impact."

We can also find different versions of the same cell. For example, consider the AND gate

![image](https://github.com/user-attachments/assets/d9d6f28d-3a58-4323-87be-17d9a0255736)

![image](https://github.com/user-attachments/assets/562710e7-544f-4d3b-b22a-8f49e492ed7e)

![image](https://github.com/user-attachments/assets/8fb876cc-3b6f-4764-893d-5c17590a7ae3)

We can observe that:

* and2_0 -- taking the least area, more delay and low power.
* and2_1 -- taking more area, less delay and high power.
* and2_2 -- taking the largest area, larger delay and highest power.

Hierarchical vs Flat Synthesis:

Hierarchical synthesis involves synthesizing a complex design by breaking it down into various sub-modules, where each module is synthesized separately to generate gate-level netlists and then integrated. Hierarchical synthesis allows for better organization, reuse of modules, and incremental changes to the design without affecting the entire system. Flat synthesis, on the other hand, treats the entire design as a single, monolithic unit during the synthesis process and regardless of any hierarchical relations, it is synthesized into a single netlist. Flat synthesis can be useful for optimizing certain designs but it becomes challenging to maintain, analyze, and modify the design due to its lack of structural modularity.

Consider the verilog file `multiple_modules.v` which is given in the verilog_files directory

```
module sub_module2 (input a, input b, output y);
    assign y = a | b;
endmodule

module sub_module1 (input a, input b, output y);
    assign y = a&b;
endmodule


module multiple_modules (input a, input b, input c , output y);
    wire net1;
    sub_module1 u1(.a(a),.b(b),.y(net1));  //net1 = a&b
    sub_module2 u2(.a(net1),.b(c),.y(y));  //y = net1|c ,ie y = a&b + c;
endmodule
```

To perform **hierarchical synthesis** on the `multiple_modules.v` file type the following commands:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
write_verilog -noattr multiple_modules_hier.v
```

The following statistics are displayed:

![image](https://github.com/user-attachments/assets/52098879-b1b3-43c4-bba4-ca00e0603ed1)

Netlist:

![image](https://github.com/user-attachments/assets/9167285b-0f13-4c41-944f-0b6becfafd0a)

Hierarchical netlist code:

![image](https://github.com/user-attachments/assets/15c85939-1276-4893-82b0-a5894e9066a8)

To perform **flat synthesis** on the `multiple_modules.v` file type the following commands:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten
show
write_verilog -noattr multiple_modules_flat.v
```

The following statistics are displayed:

![image](https://github.com/user-attachments/assets/7dd6d1e3-2821-490a-b71a-c098b9654a7f)

Netlist:

![image](https://github.com/user-attachments/assets/538539a2-9358-444a-9bd3-7309a490a5b5)

Flat synthesis netlist code:

![image](https://github.com/user-attachments/assets/74b94d17-692c-41e1-a138-84a9376797f2)

To perform **sub module synthesis**. type the below commands:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog multiple_modules.v 
synth -top sub_module
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
```

The following statistics are displayed:

![image](https://github.com/user-attachments/assets/46762203-dd3a-45a5-925f-2d3f07bf51f3)

Netlist:

![image](https://github.com/user-attachments/assets/7d1fd148-bbf7-4128-88df-15e0e2fc755b)


Netlist code:

![image](https://github.com/user-attachments/assets/936aca6e-0ad8-4d3b-abbc-46197b490194)

**Flip-Flop Coding Styles and Optimizations**

Flip-Flops are an essential part of sequential logic in a circuit and here we explore the design and synthesis of various types of flip-flops. To prevent glitches in digital circuits, we use flip-flops to store intermediate values. This ensures that combinational circuit inputs remain stable until the clock edge, avoiding glitches and maintaining correct operation:

**Asynchronous Reset Flip-flop:**

Verilog Code:

```
module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```

Run the below code to view the simulation:

```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```

Waveform:

![image](https://github.com/user-attachments/assets/55bbcda4-4c31-4d51-8ee3-bd20faa7d153)

Run the below code to view the netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

Netlist:

![image](https://github.com/user-attachments/assets/70d7f947-f0e6-4921-b143-5f7419cf3ef6)

**Synchronous Reset Flip-flop:**

Verilog Code:

```
module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
	if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```

Run the below code to view the simulation:

```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```

Waveform:

![image](https://github.com/user-attachments/assets/8b80edd0-efdb-4ca7-9e4c-7db904655d20)

Run the below code to view the netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

Netlist:

![image](https://github.com/user-attachments/assets/00399402-3299-4fa0-b672-0e97a2009683)

**Asynchronous Set Flip-flop:**

Verilog Code:

```
module dff_async_set ( input clk ,  input async_set , input d , output reg q );
always @ (posedge clk , posedge async_set)
begin
	if(async_set)
		q <= 1'b1;
	else	
		q <= d;
end
endmodule
```

Run the below code to view the simulation:

```
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```

Waveform:

![image](https://github.com/user-attachments/assets/ec901aae-f8a9-4b23-8296-87dda912fc07)

Run the below code to view the netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

Netlist:

![image](https://github.com/user-attachments/assets/a6b6a03b-0b96-467b-9ad8-3367e746b676)


**Optimizations:**

Example 1:

Consider the verilog code 'mult_2.v' :

```
module mul2 (input [2:0] a, output [3:0] y);
assign y = a * 2;
endmodule
```

Truth Table:

| a2 | a1 | a0 | y3 | y2 | y1 | y0 |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 | 1 | 1 | 0 |

We can see the multiplication of a number by 2 doesnt really need any extra hardware we just need to append the LSB's with zeroes and the remaining bits are the input bits of same, It can be realised by grouding the LSB's and wiring the input properly to the output.


Run the below code to view the netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mult_2_net.v
```

Statistics:

![image](https://github.com/user-attachments/assets/4f5467de-821e-485d-a1ca-595fa438f000)

Netlist:

![image](https://github.com/user-attachments/assets/d2333712-d710-413c-bec9-ae71c415e3fb)

Netlist code:

![image](https://github.com/user-attachments/assets/895a9182-acb0-408f-a715-0b93122b1272)

Example 2:

Consider the verilog code 'mult_8.v' :

```
module mult8 (input [2:0] a , output [5:0] y);
	assign y = a * 9;
endmodule
```

In this design the 3-bit input number "a" is multiplied by 9 i.e (a*9) which can be re-written as (a*8) + a . The term (a*8) is nothing but a left shifting the number a by three bits. Consider that a = a2 a1 a0. (a*8) results in a2 a1 a0 0 0 0. (a*9)=(a*8)+a = a2 a1 a0 a2 a1 a0 = aa(in 6 bit format). Hence in this case no hardware realization is required. The synthesized netlist of this design is shown below:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_8.v
synth -top mult8
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mult_8_net.v
```

Statistics:

![image](https://github.com/user-attachments/assets/dc7480c5-f8f9-4186-b655-408a9381cdd6)

Netlist:

![image](https://github.com/user-attachments/assets/495a4cdf-7c6e-42a7-abd9-9d538c691cf6)

Netlist code:

![image](https://github.com/user-attachments/assets/bde3417b-dc61-4033-92f2-5ff0fae27367)

### Day 3: Combinational and sequential optimizations

There are two types of optimisations: Combinational and Sequential optimisations. These optimisations are done inorder to achieve designs that are efficient in terms of area, power, and performance.

**Combinational Optimization**

The techiniques used are:

- Constant Propagation (Direct Optimisation)
- Boolean Logic Optimisation (using K-Map or Quine McCluskey method)

**Constant Propagation:**

Consider the below circuit:

![image](https://github.com/user-attachments/assets/24fcec7b-7b46-4d73-b93d-a257883ef6e5)

The top circuit uses 6 transistors(3 nmos and 3 pmos). The bottom cicuit uses 2 transistors(1 nmos and 1 pmos) when we make A zero as the logic becomes invertor. 

**Boolean Logic Optimisation:**

Consider the below verilog code:

`assign y = a?(b?c:(c?a:0)):(!c);`

The ternary operator (?:) will realize a mux upon synthesis as shown below. 

![image](https://github.com/user-attachments/assets/22937fd8-8b2e-4da1-a19a-25563b92f5dd)

The circuit can be optimised as follows:

![image](https://github.com/user-attachments/assets/45a4b461-cc9b-4512-a0d1-7ecd123e09bf)

**Example 1:**

Verllog code:

```
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```

The above code infers a multiplexer and since one of the inputs of the multiplexer is always connected to the ground it will infer an AND gate on optimisation.

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v
synth -top opt_check
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr opt_check_net.v
```

![image](https://github.com/user-attachments/assets/c0b9561e-d5f6-4e60-a037-7388cec4a000)


![image](https://github.com/user-attachments/assets/18524e97-6028-4181-bfba-4bd6c447d0c4)

**Example 2:**

Verllog code:

```
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```

Since one of the inputs of the multiplexer is always connected to the logic 1 it will infer an OR gate on optimisation.The OR gate will be NAND implementation since NOR gate has stacked pmos while NAND implementation has stacked nmos.

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check2.v
synth -top opt_check2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr opt_check2_net.v
```

![image](https://github.com/user-attachments/assets/4aa3a255-c909-4786-bf65-760b816ffaaf)

![image](https://github.com/user-attachments/assets/38df1e9e-b935-4156-9db7-38a5da0fdd90)

**Example 3:**

Verilog code:

```
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```

On optimisation the above design becomes a 3 input AND gate.

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check3.v
synth -top opt_check3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr opt_check3_net.v
```

![image](https://github.com/user-attachments/assets/38a83f8b-73a8-4d44-b36d-84a716742514)


![image](https://github.com/user-attachments/assets/732b0264-fb2c-41c5-9027-68c70679cdbb)

**Example 4:**

Verilog code:

```
module opt_check4 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```

On optimisation the above design becomes a 2 input XNOR gate.

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check4.v
synth -top opt_check4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr opt_check4_net.v
```
![image](https://github.com/user-attachments/assets/199b9558-76e1-4022-8d0c-cc46542da246)


![image](https://github.com/user-attachments/assets/7df25146-326c-48f2-814f-7efebbe41906)

**Example 5:**

Verilog code:

```
module sub_module1(input a , input b , output y);
 assign y = a & b;
endmodule

module sub_module2(input a , input b , output y);
 assign y = a^b;
endmodule

module multiple_module_opt(input a , input b , input c , input d , output y);
wire n1,n2,n3;

sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
sub_module2 U3 (.a(b), .b(d) , .y(n3));

assign y = c | (b & n1); 

endmodule
```

On optimisation the above design becomes a AND OR gate

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_module_opt.v
synth -top multiple_module_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten
show
write_verilog -noattr multiple_module_opt_net.v
```

![image](https://github.com/user-attachments/assets/aeea3451-3cc9-406d-95a1-b5b35ca708a7)

![image](https://github.com/user-attachments/assets/10c83e53-9e4a-48e8-8dd6-253aad997879)

**Example 6:**

Verilog code:

```
module sub_module(input a , input b , output y);
	assign y = a & b;
endmodule

module multiple_module_opt2(input a , input b , input c , input d , output y);
		wire n1,n2,n3;
	sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
	sub_module U2 (.a(b), .b(c) , .y(n2));
	sub_module U3 (.a(n2), .b(d) , .y(n3));
	sub_module U4 (.a(n3), .b(n1) , .y(y));
endmodule
```

On optimisation the above design becomes Y=0 

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_module_opt2.v
synth -top multiple_module_opt2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten
show
write_verilog -noattr multiple_module_opt2_net.v
```

![image](https://github.com/user-attachments/assets/320f495c-3ea1-427b-94ee-352e36786fea)


![image](https://github.com/user-attachments/assets/725961e1-300f-42db-a3bf-fe7df6b29233)

**Sequential Logic Optimizations**

**Example 1:**

Verilog code:

```
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
```

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const1_net.v
```


![image](https://github.com/user-attachments/assets/080978a6-12a9-443c-8d25-e923d6560b9b)

![image](https://github.com/user-attachments/assets/b66b706b-cc36-4e8a-aeda-1b8a30480bd8)

GTKWave Output:

```
iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
```

![image](https://github.com/user-attachments/assets/f4e729c1-1130-40f3-ae69-99b1a2015d08)


**Example 2:**

Verilog code:

```
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
```

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const2_net.v
```

![image](https://github.com/user-attachments/assets/bb6d4ae1-0cf3-4186-bb6b-aca6476b1840)

![image](https://github.com/user-attachments/assets/3503d2c9-ac1b-4d1b-986e-5aaf494b9059)


GTKWave Output:

```
iverilog dff_const2.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd
```

![image](https://github.com/user-attachments/assets/c9147236-4f3a-4d12-b8fe-c506749b3890)

**Example 3:**

Verilog code:

```
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule
```

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const3_net.v
```

![image](https://github.com/user-attachments/assets/cdf64a91-3fad-429b-b91e-b2b563d16dc7)


![image](https://github.com/user-attachments/assets/3085e4f7-d89f-43e5-a26f-fb1a1fe8999e)


GTKWave Output:

```
iverilog dff_const3.v tb_dff_const3.v
./a.out
gtkwave tb_dff_const3.vcd
```

![image](https://github.com/user-attachments/assets/a6718736-a93a-4f3e-90f5-f3f85f22292c)


**Example 4:**

Verilog code:

```
module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b1;
	end
else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule
```

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const4_net.v
```
![image](https://github.com/user-attachments/assets/a10095c1-63f2-4343-9304-413d0f941465)


![image](https://github.com/user-attachments/assets/45dd36fd-035a-4adc-aad8-ffda9c2a3ee2)

 
GTKWave Output:

```
iverilog dff_const4.v tb_dff_const4.v
./a.out
gtkwave tb_dff_const4.vcd
```

![image](https://github.com/user-attachments/assets/790a1467-b14b-484d-8f1b-7212d66b051d)


**Example 5:**

Verilog code:

```
module dff_const5(input clk, input reset, output reg q);
reg q1;
always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b0;
			q1 <= 1'b0;
		end
	else
		begin
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const5.v
synth -top dff_const5
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const5_net.v
```

![image](https://github.com/user-attachments/assets/42cac623-761a-4a4d-9678-7ce0960b0377)


![image](https://github.com/user-attachments/assets/243df51b-d924-465f-9ddf-7523b9d42e60)


GTKWave Output:

```
iverilog dff_const5.v tb_dff_const5.v
./a.out
gtkwave tb_dff_const5.vcd
```

![image](https://github.com/user-attachments/assets/d695cd08-fc33-44d9-bfa2-ce27ae98e9c6)


**Sequential Logic Optimizations for unused outputs**

**Example 1:**

Verilog code:

```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];
always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end
endmodule
```

Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr counter_opt_net.v
```

![image](https://github.com/user-attachments/assets/b08e9a6a-0947-4a36-9c34-1e722a09303e)


![image](https://github.com/user-attachments/assets/b55ceee6-1bbc-4236-957e-3c0c90592573)


GTKWave Output:

```
iverilog counter_opt.v tb_counter_opt.v
./a.out
gtkwave tb_counter_opt.vcd
```

![image](https://github.com/user-attachments/assets/359ffb99-5980-459b-87d4-d153fa5f8da7)

Modified counter logic:

Verilog code:

```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = {count[2:0]==3'b100};
always @(posedge clk ,posedge reset)
begin
if(reset)
	count <= 3'b000;
else
	count <= count + 1;
end
endmodule
```
Run the below code for netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr counter_opt_net.v
```
![image](https://github.com/user-attachments/assets/6b0daf62-32e0-486e-adfd-71fd8c8edac6)


![image](https://github.com/user-attachments/assets/c8b04d5e-479c-42c5-9af9-b612d85064fb)


GTKWave Output:

```
iverilog counter_opt.v tb_counter_opt.v
./a.out
gtkwave tb_counter_opt.vcd
```
![image](https://github.com/user-attachments/assets/977035cf-fd8e-4432-8717-ca7f6966d993)

### Day 4: GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

Gate Level Simulation (GLS) is a crucial step in the verification process of digital circuits. It involves simulating the synthesized netlist, which is a lower-level representation of the design, using a testbench to verify its logical correctness and timing behavior. By comparing the simulated outputs to the expected outputs, GLS ensures that the synthesis process has not introduced any errors and that the design meets its performance requirements.

![image](https://github.com/user-attachments/assets/fa59f230-4a0d-4c8e-9353-a01a9209a6d6)

Sensitivity lists are crucial for accurate circuit behavior. If a sensitivity list is incomplete, it can lead to unexpected latches. Blocking and non-blocking assignments within always blocks have different execution behaviors. Incorrect use of blocking assignments can unintentionally create latches, causing synthesis and simulation mismatches. To avoid these issues, it's essential to carefully analyze circuit behavior and ensure that the sensitivity list and assignments align with the desired functionality.

**GLS Simulation**

**Example 1:**

Verilog code:

```
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
assign y = sel?i1:i0;
endmodule
```

Simulation:

```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

![image](https://github.com/user-attachments/assets/d3a37652-3674-4c31-a889-d7c1725d9464)

Netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr ternary_operator_mux_net.v
```

![image](https://github.com/user-attachments/assets/f5cd0b48-d658-45fb-8ad8-323e7f3adab4)


![image](https://github.com/user-attachments/assets/ede78147-5fae-4048-9b5e-8bf689e29468)

GLS:

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

![image](https://github.com/user-attachments/assets/53417306-60ce-4c04-9b88-0ca988cb055a)

In this case there is no mismatch between the waveforms before and after synthesis

**Example 2:**

Verilog code:

```
module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```

Simulation:

```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![image](https://github.com/user-attachments/assets/2f740d27-43c5-4202-b9b4-3a095ffaccf3)


Netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog bad_mux.v
synth -top bad_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr bad_mux_net.v
```

![image](https://github.com/user-attachments/assets/6fc0e220-875c-4162-a242-20d2842fbd0f)

![image](https://github.com/user-attachments/assets/03bd22e5-88c6-4d2b-a479-d2d7072131d9)

GLS:

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

![image](https://github.com/user-attachments/assets/fc08c299-d660-40f9-a821-3c8581d4d8b0)

In this case there is a synthesis and simulation mismatch. While performing synthesis yosys has corrected the sensitivity list error.

**Labs on Synthesis-Simulation mismatch for blocking statements**

Verilog code:

```
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
d = x & c;
x = a | b;
end
endmodule
```

Simulation:

```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```

![image](https://github.com/user-attachments/assets/9ea733b7-f353-4665-8e37-fb2a18a5c8cf)

Netlist:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog blocking_caveat.v
synth -top blocking_caveat
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr blocking_caveat_net.v
```

![image](https://github.com/user-attachments/assets/d692259c-29ea-4dff-8b4d-e7cc8878cc21)


![image](https://github.com/user-attachments/assets/da84e677-bc84-44ee-8ed2-a4ee9d91977d)


GLS:

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```

![image](https://github.com/user-attachments/assets/7b75b38c-70fb-444e-bbed-af5f7cd6b263)

In this case there is a synthesis and simulation mismatch. While performing synthesis yosys has corrected the latch error.

## Task-9: Synthesize RISC-V and compare output with functional simulations

Pre-synthesis:

```
cd VSDBabySoC
make pre_synth_sim
gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```

![image](https://github.com/user-attachments/assets/ec26e940-cdf6-4312-af80-6042d8063e0e)

![image](https://github.com/user-attachments/assets/7f4c4af2-1234-4286-9578-0cbafb8b3ec0)

![image](https://github.com/user-attachments/assets/8c76f4fd-6c6d-444a-862f-c73d6dc30dd2)

Post-synthesis:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog clk_gate.v
read_verilog rvmyth.v
synth -top rvmyth
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten
show
write_verilog -noattr rvmyth_net.v
!gedit rvmyth_net.v
exit
```

![image](https://github.com/user-attachments/assets/0f9769d3-593f-4296-ba7e-db7fca7d0d9e)

![image](https://github.com/user-attachments/assets/afe1354e-750b-4cbb-bf33-31797c21fe52)

![image](https://github.com/user-attachments/assets/191c0b84-88a1-4f50-8037-93f9e3413bee)

![image](https://github.com/user-attachments/assets/de5d893b-4e42-49cf-a328-6d0e916095b4)

![image](https://github.com/user-attachments/assets/61fd7855-bb94-4f0d-9fa5-adf907da48e3)




```
cd ~/VSDBabySoC
make post_synth_sim
gtkwave output/post_synth_sim/post_synth_sim.vcd
```

![image](https://github.com/user-attachments/assets/c4e1c701-025e-4feb-b52b-7dd5406134aa)

![image](https://github.com/user-attachments/assets/4197d6e0-e1b5-45ba-a75c-ec248cc02f9f)

![image](https://github.com/user-attachments/assets/6fdf6a3d-799d-40b7-a611-df719933b857)


## Task 10: Post Synthesis Static Timing Analysis using OpenSTA

The contents of VSDBabySoc/src/sdc/vsdbabysoc_synthesis.sdc:

```
set PERIOD 11.05

set_units -time ns
create_clock [get_pins {pll/CLK}] -name clk -period $PERIOD
set_clock_uncertainty -setup  [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_transition [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_uncertainty -hold [expr $PERIOD * 0.08] [get_clocks clk]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_CP]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_VCO]
set_input_transition [expr $PERIOD * 0.08] [get_ports REF]
set_input_transition [expr $PERIOD * 0.08] [get_ports VCO_IN]
set_input_transition [expr $PERIOD * 0.08] [get_ports VREFH]
```

Now, run the below commands:

```
cd VSDBabySoc/src
sta
read_liberty -min ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -min ./lib/avsdpll.lib
read_liberty -min ./lib/avsddac.lib
read_liberty -max ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max ./lib/avsdpll.lib
read_liberty -max ./lib/avsddac.lib
read_verilog ../output/synth/vsdbabysoc.synth.v
link_design vsdbabysoc
read_sdc ./sdc/vsdbabysoc_synthesis.sdc
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

The below is the snapshot:

![image](https://github.com/user-attachments/assets/c47bc808-33dc-4a18-8ed2-a4986fb69039)

Setup Time:

![image](https://github.com/user-attachments/assets/f1fe0921-2970-412a-97ce-f9e384a43de1)

Hold Time:

![image](https://github.com/user-attachments/assets/06bb5d89-164f-4dfd-aeac-2db1a04d33bd)


## Task 11: Post Synthesis Static Timing Analysis using OpenSTA for all the sky130 lib files

Snapshot of constraints file:

![image](https://github.com/user-attachments/assets/5a751dee-6dfa-40a5-acd5-d58c39aa735e)

Store all the `lib` files in a folder named `timing_libs`. Now, go to `VSDBabySoC/src` and create a file `sta_across_pvt.tcl` . The below consists of the contents of the tickle file:

```
set list_of_lib_files(1) "sky130_fd_sc_hd__ff_100C_1v65.lib"
set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v95.lib"
set list_of_lib_files(3) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v95.lib"
set list_of_lib_files(7) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part1"
set list_of_lib_files(8) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part2"
set list_of_lib_files(9) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part3"
set list_of_lib_files(10) "sky130_fd_sc_hd__ss_100C_1v40.lib"
set list_of_lib_files(11) "sky130_fd_sc_hd__ss_100C_1v60.lib"
set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
set list_of_lib_files(14) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
set list_of_lib_files(15) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
set list_of_lib_files(16) "sky130_fd_sc_hd__ss_n40C_1v60.lib"
set list_of_lib_files(17) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part1"
set list_of_lib_files(18) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part2"
set list_of_lib_files(19) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part3"
set list_of_lib_files(20) "sky130_fd_sc_hd__ss_n40C_1v76.lib"
set list_of_lib_files(21) "sky130_fd_sc_hd__tt_025C_1v80.lib"
set list_of_lib_files(22) "sky130_fd_sc_hd__tt_100C_1v80.lib"

for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
read_liberty ./timing_libs/$list_of_lib_files($i)
read_verilog ../output/synth/vsdbabysoc.synth.v
link_design vsdbabysoc
read_sdc ./sdc/vsdbabysoc_synthesis.sdc
check_setup -verbose
report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > ./sta_output/min_max_$list_of_lib_files($i).txt

}

```

![image](https://github.com/user-attachments/assets/a9cf7dfe-1ad8-4d72-8414-b3a75b96bc5b)

Now, run the following commands:

```
cd VSDBabySoC/src
sta
source sta_across_pvt.tcl
```

![image](https://github.com/user-attachments/assets/5c3742ee-ae81-4741-8bfd-604b02da392e)

Output:

![image](https://github.com/user-attachments/assets/0c2962ef-d883-4cec-807b-9ea069a7a00c)

Graphs:

![image](https://github.com/user-attachments/assets/c6a16309-d461-4bdf-a16c-0efda04b5225)

![image](https://github.com/user-attachments/assets/47a9c697-250f-497a-8072-e7c763ac494d)


## Task 12: Advanced Physical Design using OpenLane using Sky130

#### Day-1: Inception of open-source EDA, OpenLane and Sky130 PDK

**QFN-48 Package:** A Quad Flat No-leads (QFN) 48 package is a leadless IC package with 48 connection pads around the perimeter. It offers good thermal and electrical performance in a compact form, making it ideal for high-density applications.

![image](https://github.com/user-attachments/assets/2237a9ef-dc38-444f-97a5-ceb4e983c8f0)


**Chip:** An integrated circuit (IC) that contains various functional blocks like memory, processing units, and I/O in a silicon substrate, typically used for specific applications in electronics.

![image](https://github.com/user-attachments/assets/7503bcea-4654-4bc9-b77a-de9ced7929be)


**Pads:** Small metallic areas on a chip or package used to connect internal circuitry to external connections, enabling signals to be transferred to and from the IC.

**Core:** The central part of a chip containing the main processing unit and functional logic, often optimized for power and performance.

**Die:** The section of a silicon wafer containing an individual IC before it is packaged, housing all active circuits and elements for the chip's functions.

![image](https://github.com/user-attachments/assets/cfa2c482-59c5-4ad5-b74c-a027bfdf16b8)


**IPs (Intellectual Properties):** Pre-designed functional blocks or modules within a chip, such as USB controllers or memory interfaces, licensed for reuse across various designs to save time and cost.

![image](https://github.com/user-attachments/assets/1039a7d9-0286-42c7-8da7-17136c3da5aa)


**From Software Applications to Hardware Flow**

To run an application on hardware, several processes take place. First, the application enters a layer known as the system software, which prepares it for execution by translating the application program into binary format, understandable by hardware. Key components within system software include the Operating System (OS), Compiler, and Assembler.

The process starts with the OS, which breaks down application functions written in high-level languages such as C, C++, Java, or Visual Basic. These functions are passed to a suitable compiler, which translates them into low-level instructions. The syntax and format of these instructions are tailored to the specific hardware architecture in use.

Next, the assembler converts these hardware-specific instructions into binary format, known as machine language. This binary code is then fed to the hardware, enabling it to perform specific tasks as defined by the received instructions.

![image](https://github.com/user-attachments/assets/14788472-7c91-4860-82c6-2bccb49f91d2)

For example, consider a stopwatch app running on a RISC-V core. Here, the OS might generate a small function in C, which is then passed to a compiler. The compiler outputs RISC-V-specific instructions, tailored to the architecture. These instructions are subsequently processed by the assembler, which converts them into binary code. This binary code then flows into the chip layout, where the hardware executes the desired functionality.

![image](https://github.com/user-attachments/assets/cabbd8f7-f0c4-4a13-bf2e-d6d67392910e)

For the above stopwatch the below figure shows the input and output of the compiler and assembler.

![image](https://github.com/user-attachments/assets/63f2e771-eed8-4953-b501-dd9ff0d209f7)

The compiler generates architecture-specific instructions, while the assembler produces the corresponding binary patterns. To execute these instructions on hardware, an RTL (written in a Hardware Description Language) is used to interpret and implement the instructions. This RTL design is then synthesized into a netlist, represented as interconnected logic gates. Finally, the netlist undergoes physical design implementation to be fabricated onto the chip.

![image](https://github.com/user-attachments/assets/ae0a287d-8bb4-4535-b6b0-5b1baf09008d)

**Components of ASIC Design**

![image](https://github.com/user-attachments/assets/560b728b-8e75-4c9d-a3c8-5b640318c4aa)

- RTL IPs: Pre-designed, verified digital circuit blocks (like adders, flip-flops, memory) in HDL (e.g., Verilog, VHDL). They save design time by providing ready-to-use components for complex circuits.

- EDA Tools: Software that automates ASIC design tasks (e.g., synthesis, optimization, placement, timing analysis). Essential for improving productivity and ensuring performance and power requirements are met.

- PDK Data: A set of files and parameters from a semiconductor foundry, detailing its manufacturing process (e.g., transistor models, design rules). PDKs ensure ASIC designs are compatible with the foundry’s fabrication process.

**Simplified RTL to GDS flow**

![image](https://github.com/user-attachments/assets/1f2a5455-d83e-46fe-92e3-531ade2a9add)

- **RTL Design:** Describes the circuit's functional behavior using HDLs like Verilog or VHDL, defining its logic and data paths.

- **RTL Synthesis:** Converts RTL code to a gate-level netlist which is a collection of standard cells like AND gates, flip-flops, and multiplexers by mapping it to standard cells and optimizing for area, power, and timing. 

- **Floor and Power Planning:** Partitions chip area, places major components, and defines power grid and I/O placement to optimize area, power distribution, and signal flow. This step optimizes the physical layout, aiming to reduce power consumption and improve signal integrity by considering the placement of I/O pads and power distribution cells

- **Placement:** Assigns physical locations to cells, aiming to minimize wirelength, reduce signal delay, and meet design constraints. The placement tool carefully arranges the cells to balance the overall chip design for optimal performance and area utilization.

- **Clock Tree Synthesis (CTS):** Clock Tree Synthesis (CTS) is a critical step that focuses on creating an optimized clock distribution network. CTS ensures the clock is distributed evenly to all flip-flops and registers. It builds an optimized clock network to balance clock signal distribution and reduce clock skew.

- **Routing:** Connects components based on placement, optimizing wire paths to ensure signal integrity, minimize congestion, and meet design rules.

- **Sign-off:** Final verification stage, ensuring the design meets functionality, performance, power, and reliability targets. Timing analysis is performed to check setup and hold times, power analysis ensures the design doesn’t exceed power limits, and physical verification checks ensure that the layout meets manufacturing rules. This stage confirms the design is ready for fabrication.

- **GDSII File Generation:** Creates the GDSII file containing the complete layout details needed for chip fabrication. This file represents the final physical design and is used by manufacturers to create the photomasks required for chip production. The GDSII file serves as the blueprint for the actual fabrication of the chip.

**OpenLane ASIC Flow:**

![image](https://github.com/user-attachments/assets/cdd04b14-fbfe-44a3-8d4e-8fbfe443bd74)

1. RTL Synthesis, Technology Mapping, and Formal Verification: The tools used are Yosys (for RTL synthesis), ABC (for technology mapping and formal verification).
2. Static Timing Analysis: The tools used are OpenSTA (for static timing analysis).
3. Floor Planning: The tools used are init_fp (initial floorplanning), ioPlacer (I/O placement), pdn (power distribution network planning), tapcell (tap cell insertion).
4. Placement: The tools used are RePLace (global placement), Resizer (optional for resizing cells), OpenPhySyn (formerly used for placement), OpenDP (detailed placement).
5. Clock Tree Synthesis: The tools used are TritonCTS (for clock tree synthesis).
6. Fill Insertion: The tools used are OpenDP (for filler placement).
7. Routing: The tools used for global routing are FastRoute or CU-GR (formerly used) and for the detailed routing , we use TritonRoute (for detailed routing) or DR-CU (formerly used).
8. SPEF Extraction: The tools used are OpenRCX (or SPEF-Extractor, formerly used) for Standard Parasitic Exchange Format (SPEF) extraction.
9. GDSII Streaming Out: The tools used are Magic and KLayout (for viewing and editing GDSII files).
10. Design Rule Checking (DRC) Checks: The tools used are Magic and KLayout (for DRC checks).
11. Layout vs. Schematic (LVS) Check: The tools used are Netgen (for LVS checks).
12. Antenna Checks: The tools used are Magic (for antenna checks).

**OpenLANE Directory structure**

``` 
├── OOpenLane             -> directory where the tool can be invoked (run docker first)
│   ├── designs          -> All designs must be extracted from this folder
│   │   │   ├── picorv32a -> Design used as case study for this workshop
│   |   |   ├── ...
|   |   ├── ...
├── pdks                 -> contains pdk related files 
│   ├── skywater-pdk     -> all Skywater 130nm PDKs
│   ├── open-pdks        -> contains scripts that makes the commerical PDK (which is normally just compatible to commercial tools) to also be compatible with the open-source EDA tool
│   ├── sky130A          -> pdk variant made especially compatible for open-source tools
│   │   │  ├── libs.ref  -> files specific to node process (timing lib, cell lef, tech lef) for example is `sky130_fd_sc_hd` (Sky130nm Foundry Standard Cell High Density)  
│   │   │  ├── libs.tech -> files specific for the tool (klayout,netgen,magic...) 
```

**Synthesis in Openlane:**

Go to VSD Virtual Box and run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis

```

![image](https://github.com/user-attachments/assets/90ea6a96-5f1e-43e4-bf8e-27f2a5012dc3)

To view the netlist:

```
cd designs/picorv32a/runs/09-11_06-33/results/synthesis/
gedit picorv32a.synthesis.v
```

![image](https://github.com/user-attachments/assets/7e4a4b13-622a-44de-96c2-0a0162fecc7a)

Netlist code:

![image](https://github.com/user-attachments/assets/fa3e9692-0d30-42f3-bc45-c38b2f1d2894)

To view the yosys report:

```
cd ../..
cd reports/synthesis
gedit 1-yosys_4.stat.rpt
```

![image](https://github.com/user-attachments/assets/8dbe1a51-3198-41c0-b098-d657cf940746)

![image](https://github.com/user-attachments/assets/910e671a-2728-43b8-a677-cc7cc7e17d9d)


Report:

```
28. Printing statistics.

=== picorv32a ===

   Number of wires:              14596
   Number of wire bits:          14978
   Number of public wires:        1565
   Number of public wire bits:    1947
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:              14876
     sky130_fd_sc_hd__a2111o_2       1
     sky130_fd_sc_hd__a211o_2       35
     sky130_fd_sc_hd__a211oi_2      60
     sky130_fd_sc_hd__a21bo_2      149
     sky130_fd_sc_hd__a21boi_2       8
     sky130_fd_sc_hd__a21o_2        57
     sky130_fd_sc_hd__a21oi_2      244
     sky130_fd_sc_hd__a221o_2       86
     sky130_fd_sc_hd__a22o_2      1013
     sky130_fd_sc_hd__a2bb2o_2    1748
     sky130_fd_sc_hd__a2bb2oi_2     81
     sky130_fd_sc_hd__a311o_2        2
     sky130_fd_sc_hd__a31o_2        49
     sky130_fd_sc_hd__a31oi_2        7
     sky130_fd_sc_hd__a32o_2        46
     sky130_fd_sc_hd__a41o_2         1
     sky130_fd_sc_hd__and2_2       157
     sky130_fd_sc_hd__and3_2        58
     sky130_fd_sc_hd__and4_2       345
     sky130_fd_sc_hd__and4b_2        1
     sky130_fd_sc_hd__buf_1       1656
     sky130_fd_sc_hd__buf_2          8
     sky130_fd_sc_hd__conb_1        42
     sky130_fd_sc_hd__dfxtp_2     1613
     sky130_fd_sc_hd__inv_2       1615
     sky130_fd_sc_hd__mux2_1      1224
     sky130_fd_sc_hd__mux2_2         2
     sky130_fd_sc_hd__mux4_1       221
     sky130_fd_sc_hd__nand2_2       78
     sky130_fd_sc_hd__nor2_2       524
     sky130_fd_sc_hd__nor2b_2        1
     sky130_fd_sc_hd__nor3_2        42
     sky130_fd_sc_hd__nor4_2         1
     sky130_fd_sc_hd__o2111a_2       2
     sky130_fd_sc_hd__o211a_2       69
     sky130_fd_sc_hd__o211ai_2       6
     sky130_fd_sc_hd__o21a_2        54
     sky130_fd_sc_hd__o21ai_2      141
     sky130_fd_sc_hd__o21ba_2      209
     sky130_fd_sc_hd__o21bai_2       1
     sky130_fd_sc_hd__o221a_2      204
     sky130_fd_sc_hd__o221ai_2       7
     sky130_fd_sc_hd__o22a_2      1312
     sky130_fd_sc_hd__o22ai_2       59
     sky130_fd_sc_hd__o2bb2a_2     119
     sky130_fd_sc_hd__o2bb2ai_2     92
     sky130_fd_sc_hd__o311a_2        8
     sky130_fd_sc_hd__o31a_2        19
     sky130_fd_sc_hd__o31ai_2        1
     sky130_fd_sc_hd__o32a_2       109
     sky130_fd_sc_hd__o41a_2         2
     sky130_fd_sc_hd__or2_2       1088
     sky130_fd_sc_hd__or2b_2        25
     sky130_fd_sc_hd__or3_2         68
     sky130_fd_sc_hd__or3b_2         5
     sky130_fd_sc_hd__or4_2         93
     sky130_fd_sc_hd__or4b_2         6
     sky130_fd_sc_hd__or4bb_2        2

   Chip area for module '\picorv32a': 147712.918400
```

```
Flop ratio = Number of D Flip flops = 1613  = 0.1084
             ______________________   _____
             Total Number of cells    14876
```

#### Day-2: Good floorplan vs bad floorplan and introduction to library cells

**Utilization Factor and Aspect Ratio**: In IC floor planning, utilization factor and aspect ratio are key parameters. The utilization factor is the ratio of the area occupied by the netlist to the total core area. While a perfect utilization of 1 (100%) is ideal, practical designs target a factor of 0.5 to 0.6 to allow space for buffer zones, routing channels, and future adjustments. The aspect ratio, defined as height divided by width, indicates the chip’s shape; an aspect ratio of 1 denotes a square, while other values result in a rectangular layout. The aspect ratio is chosen based on functional, packaging, and manufacturing needs.

```
Utilisation Factor =  Area occupied by netlist
                     __________________________
                         Total area of core
                         

Aspect Ratio =  Height
               ________
                Width
```

**Pre-placed cells** : Pre-placed cells are essential functional blocks, such as memory, custom processors, and analog circuits, positioned manually in fixed locations. These blocks are crucial for the chip’s performance and remain fixed during placement and routing to preserve their functionality and layout integrity.

**Decoupling Capacitors** : Decoupling capacitors are placed near logic circuits to stabilize power supply voltages during transient events. Acting as local energy reserves, they help reduce voltage fluctuations, crosstalk, and electromagnetic interference (EMI), ensuring reliable power delivery to sensitive circuits.

**Power Planning**: A robust power planning strategy includes creating a power and ground mesh to distribute VDD and VSS evenly across the chip. This setup ensures stable power delivery, minimizes voltage drops, and improves overall efficiency. Multiple power and ground points reduce the risk of instability and voltage drop issues, supporting the design’s power needs effectively.

**Pin Placement**: Pin placement (I/O planning) is crucial for functionality and reliability. Strategic pin assignment minimizes signal degradation, preserves data integrity, and helps manage heat dissipation. Proper positioning of power and ground pins supports thermal management and enhances signal strength, contributing to overall system stability and manufacturability.

Floorplaning using OpenLANE:

Run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
```

![image](https://github.com/user-attachments/assets/afc31385-9905-40e8-adaa-35abf4005c3d)

![image](https://github.com/user-attachments/assets/ef3b3bab-0981-4786-a780-a6332fb9488e)

Now, run the below commands in a new terminal:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-11_07-10/results/floorplan
gedit picorv32a.floorplan.def
```
![image](https://github.com/user-attachments/assets/e80db02e-b7ff-4b08-9f40-e546b95d832d)

According to floorplan definition:

1000 Unit Distance = 1 Micron  

Die width in unit distance = 660685−0 = 660685 

Die height in unit distance = 671405−0 = 671405  

Distance in microns = Value in Unit Distance/1000  

​Die width in microns = 660685/1000 = 660.685 Microns  

Die height in microns = 671405/1000 = 671.405 Microns  

Area of die in microns = 660.685 × 671.405 = 443587.212425 Square Microns

To view the floorplan in magic. Open a new terminal and run the below commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-11_07-10/results/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

![image](https://github.com/user-attachments/assets/9f530208-b891-425d-95a6-a63382ef7f4a)

Decap and Tap Cells:

![image](https://github.com/user-attachments/assets/87f3202e-504c-4a9d-ac3e-4f4512348823)

Unplaced standard cells at origin:

![image](https://github.com/user-attachments/assets/ad0f9db1-a5b2-4237-ac47-1a2030ee9a54)

Command to run placement:

```
run_placement
```

![image](https://github.com/user-attachments/assets/97cfa678-2a83-4d8e-a3f4-bc5d4766174a)

To view the placement in magic:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![image](https://github.com/user-attachments/assets/02b468e4-bae6-4db1-8c9f-2a6489ba23ee)

![image](https://github.com/user-attachments/assets/46e5ece9-3289-406d-894a-0789cf980df9)

**Cell design and Characterization Flow**

Library is a place where we get information about every cell. It has differents cells with different size, functionality,threshold voltages. There is a typical cell design flow steps.

Inputs : PDKS(process design kit) : DRC & LVS, SPICE Models, library & user-defined specs.
Design Steps :Circuit design, Layout design (Art of layout Euler's path and stick diagram), Extraction of parasitics, Characterization (timing, noise, power).
Outputs: CDL (circuit description language), LEF, GDSII, extracted SPICE netlist (.cir), timing, noise and power .lib files

**Standard Cell Characterization Flow**

A typical standard cell characterization flow that is followed in the industry includes the following steps:

- Read in the models and tech files
- Read extracted spice Netlist
- Recognise behavior of the cells
- Read the subcircuits
- Attach power sources
- Apply stimulus to characterization setup
- Provide neccesary output capacitance loads
- Provide neccesary simulation commands
- Now all these 8 steps are fed in together as a configuration file to a characterization software called GUNA. This software generates timing, noise, power models. These .libs are classified as Timing characterization, power characterization and noise characterization.

**Timing parameters**

| Timing definition | Value |
|---|---|
| slew_low_rise_thr | 20% value |
| slew_high_rise_thr | 80% value |
| slew_low_fall_thr | 20% value |
| slew_high_fall_thr | 80% value |
| in_rise_thr | 50% value |
| in_fall_thr | 50% value |
| out_rise_thr | 50% value |
| out_fall_thr | 50% value |

**Propagation Delay**: It refers to the time it takes for a change in an input signal to reach 50% of its final value to produce a corresponding change in the output signal to reach 50% of its final value of a digital circuit.

```
rise delay =  time(out_fall_thr) - time(in_rise_thr)
```

**Transistion time**: The time it takes the signal to move between states is the transition time , where the time is measured between 10% and 90% or 20% to 80% of the signal levels.

```
Fall transition time: time(slew_high_fall_thr) - time(slew_low_fall_thr)
Rise transition time: time(slew_high_rise_thr) - time(slew_low_rise_thr)
```

#### Day-3: Design library cell using Magic Layout and ngspice characterization

**CMOS inverter ngspice simulations**

Creating a SPICE Deck for a CMOS Inverter Simulation

- Netlist Creation: Define the component connections (netlist) for a CMOS inverter circuit. Ensure each node is labeled appropriately for easy identification in the SPICE simulation. Typical nodes include input, output, ground, and supply nodes.
- Device Sizing: Specify the Width-to-Length (W/L) ratios for both the PMOS and NMOS transistors.For proper operation, the PMOS width should be larger than the NMOS width, usually 2x to 3x, to balance the drive strength
- Voltage Levels: Set gate and supply voltages, often in multiples of the transistor length. 
- Node Naming: Assign node names to each connection point around the components to clearly identify each element in the SPICE netlist (e.g., VDD, GND, IN, OUT). This helps SPICE recognize each component and simulate the circuit effectively.
  
![image](https://github.com/user-attachments/assets/b61efcf4-cd1f-4080-b4dc-4606afc3a2e5)


```
***syntax for PMOS and NMOS desription***
[component name] [drain] [gate] [source] [substrate] [transistor type] W=[width] L=[length]

 ***simulation commands***
.op --- is the start of SPICE simulation operation where Vin sweeps from 0 to 2.5 with 0.5 steps
tsmc_025um_model.mod  ----  model file which contains the technological parameters for the 0.25um NMOS and PMOS 
```
Commands to simulate in SPICE:

```
source [filename].cir
run
setplot 
dc1 
plot out vs in 
```

![image](https://github.com/user-attachments/assets/49f1ed28-c601-4954-a3aa-077a2c650650)

The switching threshold Vm is like a critical voltage level for a component called a CMOS inverter. It's the point at which this inverter switches between sending out a "0" or a "1" in a computer chip. This the point where both PMOS and NMOS is in saturation or kind of turned on, and leakage current is high. If PMOS is thicker than NMOS, the CMOS will have higher switching threshold (1.2V vs 1V) while threshold will be lower when NMOS becomes thicker.

At this point, both the transistors are in saturation region, means both are turned on and have high chances of current flowing directly from VDD to Ground called Leakage current.

To find the switching threshold:

```
Vin in 0 2.5
*** Simulation Command ***
.op
.dc Vin 0 2.5 0.05
```
![image](https://github.com/user-attachments/assets/61d07ded-adf6-4b6d-8e79-936512557edd)

Transient analysis is used for finding propagation delay. SPICE transient analysis uses pulse input shown below:

![image](https://github.com/user-attachments/assets/af0c7120-e946-4c8f-95c2-c66b130ef415)

The simulation commands:

```
Vin in 0 0 pulse 0 2.5 0 10p 10p 1n 2n 
*** Simulation Command ***
.op
.tran 10p 4n
```

Result of SPICE simulation for transient analysis:

![image](https://github.com/user-attachments/assets/e1ed922a-7ac4-4337-aa9e-8dc2f06f23e1)



Now, we clone the custom inverter

```
cd Desktop/work/tools/openlane_working_dir/openlane
git clone https://github.com/nickson-jose/vsdstdcelldesign
cd vsdstdcelldesign
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .
ls
magic -T sky130A.tech sky130_inv.mag &
```

![image](https://github.com/user-attachments/assets/07f803ca-8a02-48d1-80a4-67f2a1a56c69)

![image](https://github.com/user-attachments/assets/7bbdfed0-f2e7-4a08-9079-b63969d54975)


**Inception of Layout CMOS fabrication process**

The 16-mask CMOS design fabrication process:

1. Substrate Preparation: The process begins with preparing a silicon wafer as the foundational substrate for the circuit.
2. N-Well Formation: The N-well regions are created on the substrate by introducing impurities, typically phosphorus, through ion implantation or diffusion
3. P-Well Formation: Similar to the N-well formation, P-well regions are created using ion implantation or diffusion with boron or other suitable dopants.
4. Gate Oxide Deposition: A thin silicon dioxide layer is deposited to form the gate oxide, which insulates the gate from the channel.
5. Poly-Silicon Deposition: A layer of polysilicon is deposited on the gate oxide to serve as the gate electrode.
6. Poly-Silicon Masking and Etching: A photoresist mask defines areas where polysilicon should remain, and etching removes exposed portions.
7. N-Well Masking and Implantation: A photoresist mask is used to define the areas where the N-well regions should be preserved. Phosphorus or other suitable impurities are then implanted into the exposed regions.
8. P-Well Masking and Implantation: Similarly, a photoresist mask is used to define the areas where the P-well regions should be preserved. Boron or other suitable impurities are implanted into the exposed regions.
9. Source/Drain Implantation: Using photoresist masks, dopants are implanted to create source and drain regions (e.g., arsenic for NMOS, boron for PMOS).
10. Gate Formation: The gate electrode is defined by etching the poly-silicon layer using a photoresist mask.
11. Source/Drain Masking and Etching: A photoresist mask is applied to define the source and drain regions followed by etching to remove the oxide layer in those areas.
12. Contact/Via Formation: Contact holes or vias are etched through the oxide layer to expose the underlying regions, such as the source/drain regions or poly-silicon gates.
13. Metal Deposition: A layer of metal, typically aluminum or copper, is deposited on the wafer surface to form the interconnects.
14. Metal Masking and Etching: A photoresist mask is used to define the metal interconnects, and etching is performed to remove the exposed metal, leaving behind the desired interconnect patterns.
15. Passivation Layer Deposition: A protective layer, often made of silicon dioxide or nitride, is deposited to isolate and shield the metal interconnects.
16. Final Testing and Packaging: The fabricated wafer undergoes rigorous testing to ensure the functionality of the integrated circuits. The working chips are then separated, packaged, and prepared for use in various electronic devices.

![image](https://github.com/user-attachments/assets/d24e7009-a71a-437f-94c8-8233c633f775)

Inverter layout:

Identify NMOS:

![image](https://github.com/user-attachments/assets/49aef059-d3aa-4d0c-9259-cd60c7af940c)

Identify PMOS:

![image](https://github.com/user-attachments/assets/bd9c1596-a908-44ec-ba2d-f259acfbeb33)

Output Y:

![image](https://github.com/user-attachments/assets/efe0bc9f-43f6-4e22-9922-b579c6190daa)

PMOS source connected to VDD:

![image](https://github.com/user-attachments/assets/51599137-d1ff-45f1-8609-d5a49822b6b0)

NMOS source connected to VSS:

![image](https://github.com/user-attachments/assets/375df2f4-b388-40d9-9e3c-a971fd3e23b4)

Spice extraction of inverter in Magic. Run these in the tkcon window:

```
# Check current directory
pwd
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```

![image](https://github.com/user-attachments/assets/ed3c1850-db3c-412e-8947-41cc5d5f44df)

To view the spice file:

![image](https://github.com/user-attachments/assets/785a2dcd-1a9c-4726-9432-81d385e707f5)

![image](https://github.com/user-attachments/assets/efd09108-e2c4-4eeb-8c50-206b70d95b21)

The contents of spice file:

```
* SPICE3 file created from sky130_inv.ext - technology: sky130A

.option scale=10n

.subckt sky130_inv A Y VPWR VGND
X0 Y A VGND VGND sky130_fd_pr__nfet_01v8 ad=1.37n pd=0.148m as=1.37n ps=0.148m w=35 l=23
X1 Y A VPWR VPWR sky130_fd_pr__pfet_01v8 ad=1.44n pd=0.152m as=1.52n ps=0.156m w=37 l=23
C0 VPWR Y 0.11fF
C1 A Y 0.754fF
C2 A VPWR 0.277fF
C3 Y VGND 0.279fF
C4 A VGND 0.45fF
C5 VPWR VGND 0.781fF
.ends

```

Now modify the `sky130_inv.spice` file to find the transient respone:

```
* SPICE3 file created from sky130_inv.ext - technology: sky130A

.option scale=0.01u
.include ./libs/pshort.lib
.include ./libs/nshort.lib

//.subckt sky130_inv A Y VPWR VGND
M1000 Y A VGND VGND nshort_model.0 w=35 l=23
+  ad=1.44n pd=0.152m as=1.37n ps=0.148m
M1001 Y A VPWR VPWR pshort_model.0 w=37 l=23
+  ad=1.44n pd=0.152m as=1.52n ps=0.156m

VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)

C0 A VPWR 0.0774f
C1 VPWR Y 0.117f
C2 A Y 0.0754f
C3 Y VGND 2f
C4 A VGND 0.45f
C5 VPWR VGND 0.781f
//.ends

.tran 1n 20n
.control
run
.endc
.end
```

Now, simulate the spice netlist
```
ngspice sky130_inv.spice
```

![image](https://github.com/user-attachments/assets/4dca2d24-8a75-4087-9569-7cf6ecd03349)

To plot the waveform:

```
plot y vs time a
```

![image](https://github.com/user-attachments/assets/9cbaf59d-f58c-467f-b3b3-b945cbb615ee)

Using this transient response, we will now characterize the cell's slew rate and propagation delay:

Rise Transition: Time taken for the output to rise from 20% to 80% of max value
Fall Transition: Time taken for the output to fall from 80% to 20% of max value
Cell Rise delay: difference in time(50% output rise) to time(50% input fall)
Cell Fall delay: difference in time(50% output fall) to time(50% input rise)

```
Rise Transition : 2.24638 - 2.18242 =  0.06396 ns = 63.96 ps
Fall Transition : 4.0955 - 4.05536 =  0.0419 ns = 41.9 ps
Cell Rise Delay : 2.21144 - 2.15008 = 0.06136 ns = 61.36 ps
Cell Fall Delay : 4.07807 - 4.05 =0.02 ns = 20 ps
```

Magic Tool options and DRC Rules:

Now, go to home directory and run the below commands:

```
cd
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests
ls -al
gvim .magicrc
magic -d XR &
```

![image](https://github.com/user-attachments/assets/275769d8-e537-4a7c-b60a-2a37afe25506)

First load the poly file by load poly.mag on tkcon window.

![image](https://github.com/user-attachments/assets/dcd9372d-52f5-4600-8a38-3ce0cbd143ab)

We can see that Poly.9 is incorrect.

Add the below commands in the sky130A.tech

![image](https://github.com/user-attachments/assets/01e013f1-1e8b-43a6-8bc2-fc24bd500b06)

![image](https://github.com/user-attachments/assets/4c28de92-ca50-417f-8965-b7109ba4e5cc)

Run the commands in tkcon window:

```
tech load sky130A.tech
drc check
drc why
```

![image](https://github.com/user-attachments/assets/a3d859e7-c248-4ef1-837b-d0c509c21d5c)

![image](https://github.com/user-attachments/assets/d8431719-58d5-41cb-8086-3691eb6b54dc)

#### Day-4: Pre-layout timing analysis and importance of good clock tree

Commands to extract `tracks.info` file:

```
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
cd ../../pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd/
less tracks.info
```
![image](https://github.com/user-attachments/assets/13cb8a9b-0c9e-40f1-a020-c62cd0515980)

Commands for tkcon window to set grid as tracks of locali layer

```
grid 0.46um 0.34um 0.23um 0.17um
```

![image](https://github.com/user-attachments/assets/cd02da90-4a0a-4006-97ee-213bd7811734)

The grids show where the routing for the local-interconnet layer can only happen, the distance of the grid lines are the required pitch of the wire. Below, we can see that the guidelines are satisfied:

![image](https://github.com/user-attachments/assets/28a95f97-0330-4835-b762-4bd1c09167b0)

Now, save it by giving a custom name

```
save sky130_akainv.mag
```

![image](https://github.com/user-attachments/assets/3cc23fcf-d81e-4538-b5c2-b21e3e063bbc)

Now, open it by using the following commands:

```
magic -T sky130A.tech sky130_akainv.mag &
```

![image](https://github.com/user-attachments/assets/4f03c1dc-753c-4ad0-bb15-62d31d4c71a1)

Now, type the following command in tkcon window:

```
lef write
```
![image](https://github.com/user-attachments/assets/dfb03866-4a7f-42b1-b4ba-cb6ac847ed6f)

![image](https://github.com/user-attachments/assets/44adaa57-013d-4552-99fa-5034075df52f)

Modify config.tcl:

```
# Design
set ::env(DESIGN_NAME) "picorv32a"

set ::env(VERILOG_FILES) "./designs/picorv32a/src/picorv32a.v"
set ::env(SDC_FILES) "./designs/picorv32a/src/picorv32a.sdc"


set ::env(CLOCK_PERIOD) "5.000"
set ::env(CLOCK_PORT) "clk"

set ::env(CLOCK_NET) $::env(CLOCK_PORT) 


set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib "
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib "
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]   ## this is the new line added to the existing config.tcl file

set filename $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1 } {
  source $filename
}
```

Now, run openlane flow synthesis:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

![image](https://github.com/user-attachments/assets/497ae8ad-bf3c-4567-a578-c6ac20eb47bc)

![image](https://github.com/user-attachments/assets/dd7ada16-e796-4672-b27b-67236f8aca74)

![image](https://github.com/user-attachments/assets/318360ea-bb6b-4d6e-967f-298a4f70e779)

![image](https://github.com/user-attachments/assets/0d081b77-6f6e-46d7-bedb-1cd78c1d0fd8)

![image](https://github.com/user-attachments/assets/2c862a4f-d992-4710-804a-cdbe5e1a85c1)

**Delay Tables**

Delay plays a crucial role in cell timing, impacted by input transition and output load. Cells of the same type can have different delays depending on wire length due to resistance and capacitance variations. To manage this, "delay tables" are created, using 2D arrays with input slew and load capacitance for each buffer size as timing models. Algorithms compute buffer delays from these tables, interpolating where exact data isn’t available to estimate delays accurately, preserving signal integrity across varying load conditions.

![image](https://github.com/user-attachments/assets/095a59e1-158c-4870-88e3-b73cb3a3692c)

Fixing slack:

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a -tag 24-03_10-03 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"
echo $::env(SYNTH_BUFFERING
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```

![image](https://github.com/user-attachments/assets/f79fb04d-3753-493d-a765-aea3791fd471)

![image](https://github.com/user-attachments/assets/fe99a71a-9aba-400f-a9ce-5d42276e4a78)

![image](https://github.com/user-attachments/assets/05bf09d2-a00c-44f3-8db9-11717c81bb79)

Now, run floorplan

```
run_floorplan
```

![image](https://github.com/user-attachments/assets/474b7966-7f1f-4354-aa29-648b2a365e93)

![image](https://github.com/user-attachments/assets/03c178fe-d327-4242-a9c0-070ed48d0763)

Since we are facing unexpected un-explainable error while using run_floorplan command, we can instead use the following set of commands available based on information from `Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl` and also based on Floorplan Commands section in `Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md`

```
init_floorplan
place_io
tap_decap_or
```

Now, do placement

```
run_placement
```

![image](https://github.com/user-attachments/assets/b4e4d29e-f445-47ce-acb3-86c51661f16f)

![image](https://github.com/user-attachments/assets/292c8d10-aa72-4542-a0e7-e77f5a33dc7e)

Now, open a new terminal and run the below commands to load placement def in magic

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```

![image](https://github.com/user-attachments/assets/22efb80d-96ca-414b-9197-1e2e89ed2a78)

Custom inverter inserted in placement def

![image](https://github.com/user-attachments/assets/c339ff22-4e62-4b10-a2b0-98d711501db7)

Now, select the cell and type `expand` in tkcon window to view internal layers of cells

![image](https://github.com/user-attachments/assets/8682e469-2cb8-42af-b63e-fbad8182b285)

**Timing analysis with ideal clocks using openSTA**

Pre-layout STA will include effects of clock buffers and net-delay due to RC parasitics (wire delay will be derived from PDK library wire model).

![image](https://github.com/user-attachments/assets/a74af227-70dd-4812-930d-b6e9e787a27f)

Since we are getting 0 wns after improved timing run, we will be doing the timing analysis on initial run of synthesis which has lots of violations and no parameters added to improve timing.

Commands to invoke the OpenLANE flow include new lef and perform synthesis:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9set
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
run_synthesis
```

Go, to `Desktop/work/tools/openlane_working_dir/openlane` and create a file `pre_sta.conf`. The contents of the file are:

```
set_cmd_units -time ns -capacitance pF -current mA -voltage V -resistance kOhm -distance um
read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib
read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis.v
link_design picorv32a
read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc
report_checks -path_delay min_max -fields {slew trans net cap input_pin}
report_tns
report_wns
```

Contents of `my_base.sdc`:

```
set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 12.000
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 17.65
create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)
set IO_PCT  0.2
set input_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
puts "\[INFO\]: Setting output delay to: $output_delay_value"
puts "\[INFO\]: Setting input delay to: $input_delay_value"


set clk_indx [lsearch [all_inputs] [get_port $::env(CLOCK_PORT)]]
#set rst_indx [lsearch [all_inputs] [get_port resetn]]
set all_inputs_wo_clk [lreplace [all_inputs] $clk_indx $clk_indx]
#set all_inputs_wo_clk_rst [lreplace $all_inputs_wo_clk $rst_indx $rst_indx]
set all_inputs_wo_clk_rst $all_inputs_wo_clk


# correct resetn
set_input_delay $input_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst
#set_input_delay 0.0 -clock [get_clocks $::env(CLOCK_PORT)] {resetn}
set_output_delay $output_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] [all_outputs]

# TODO set this as parameter
set_driving_cell -lib_cell $::env(SYNTH_DRIVING_CELL) -pin $::env(SYNTH_DRIVING_CELL_PIN) [all_inputs]
set cap_load [expr $::env(SYNTH_CAP_LOAD) / 1000.0]
puts "\[INFO\]: Setting load to: $cap_load"
set_load  $cap_load [all_outputs]
```

Commands to run STA:

```
cd Desktop/work/tools/openlane_working_dir/openlane
sta pre_sta.conf
```

![image](https://github.com/user-attachments/assets/23bce842-bdd3-449c-ba66-da6b51c62a1e)

![image](https://github.com/user-attachments/assets/9a7c6501-475c-4361-b1f6-2d5c94e4b3d0)

We now try to optimise synthesis.

Go to new terminal and run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
prep -design picorv32a -tag 25-03_18-52 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
set ::env(SYNTH_MAX_FANOUT) 4
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```
![image](https://github.com/user-attachments/assets/21ea0cdb-e7a0-411c-981b-33ca528fbcc7)

Commands to run STA:

```
cd Desktop/work/tools/openlane_working_dir/openlane
sta pre_sta.conf
```

![image](https://github.com/user-attachments/assets/760b99e9-f70b-4bbb-b71e-a838abb52a3f)

![image](https://github.com/user-attachments/assets/3cd8817a-4764-411c-b665-ea526cc450dc)

**Basic timing ECO**

NOR gate of drive strength 2 is driving 5 fanouts

![image](https://github.com/user-attachments/assets/ec8dd4f0-4089-4d30-bf28-40f807171603)

Run the following commands to optimise timing:

```
report_net -connections _13111_
replace_cell _16171_ sky130_fd_sc_hd__nor3_2
report_checks -fields {net cap slew input_pins} -digits 4
```
![image](https://github.com/user-attachments/assets/49667f40-1eb1-42a8-ad22-0a287eb92de0)

We can observe that the tns has reduced to -402.45 from -403.54 and wns has reduced to -5.44 from -5.59

**Clock tree synthesis TritonCTS and signal integrity**

Clock Tree Synthesis (CTS) techniques vary based on design needs:

- Balanced Tree CTS: Uses a balanced binary-like tree for equal path lengths, minimizing clock skew but with moderate power efficiency.
- H-tree CTS: Employs an "H"-shaped structure, good for large areas and power efficiency.

   ![image](https://github.com/user-attachments/assets/d1b13f19-a87f-41b6-8f29-a4e00a8e7216)

- Star CTS: Distributes the clock from a central point, minimizing skew but requiring more buffers near the source.
- Global-Local CTS: Combines star and tree topologies, with a global tree for clock domains and local trees within domains, balancing global and local timing.
- Mesh CTS: Uses a grid pattern ideal for structured designs, balancing simplicity and skew.
- Adaptive CTS: Dynamically adjusts based on timing and congestion, offering flexibility but with added complexity.

**Crosstalk**

Crosstalk is interference from overlapping electromagnetic fields between adjacent circuits, causing unwanted signals. In VLSI, it can lead to data corruption, timing issues, and higher power consumption. Mitigation strategies include optimized layout and routing, shielding, and clock gating to reduce dynamic power and minimize crosstalk effects.

![image](https://github.com/user-attachments/assets/21df4ac0-57aa-492e-adfa-7e04ce385680)

**Clock Net Shielding**

Clock net shielding prevents glitches by isolating the clock network, using shields connected to VDD or GND that don’t switch. It reduces interference by isolating clocks from other signals, often with dedicated routing layers and clock buffers. Additionally, clock domain isolation helps prevent cross-domain interference, avoiding metastability and maintaining synchronization.

![image](https://github.com/user-attachments/assets/bf85dd84-dc29-4962-877a-ce4f535bab2c)

Now to insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist:

Run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/
ls
cp picorv32a.synthesis.v picorv32a.synthesis_old.v
ls
```

Commands to write verilog:

```
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis.v
exit
```
Verified that the netlist is overwritten

![image](https://github.com/user-attachments/assets/02b43f95-e067-425a-be03-3d81cbefed28)

Now, run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
prep -design picorv32a -tag 25-03_18-52 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1
run_synthesis
init_floorplan
place_io
tap_decap_or
run_placement
run_cts
```
![image](https://github.com/user-attachments/assets/7e329a64-2b8c-4006-a2b6-32d3b66ab790)

![image](https://github.com/user-attachments/assets/ec16844c-3c39-48b6-be93-a979503df7e7)

The cts is successful as shown below:

![image](https://github.com/user-attachments/assets/588fb2e5-917e-4a93-a3f4-38306f13b2fa)

![image](https://github.com/user-attachments/assets/f6b18d3a-a6a9-478e-9adb-521f2dc46fb5)

**Setup timing analysis using real clocks**

A real clock in timing analysis accounts for practical factors like clock skew and clock jitter. Clock skew is the difference in arrival times of the clock signal at different parts of the circuit due to physical delays, which affects setup and hold timing margins. Clock jitter is the variability in the clock period caused by power, temperature, and noise fluctuations, leading to uncertainty in clock edge timing. Both factors are crucial for accurate timing analysis, ensuring the design performs reliably in real-world conditions.

![image](https://github.com/user-attachments/assets/3526c927-e1a9-445a-9dae-22bc7e0446c7)

![image](https://github.com/user-attachments/assets/0c766405-5f9b-4700-a4cd-6fd19e9ea6cc)

Now, enter the following commands for Post-CTS OpenROAD timing analysis:

```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/25-03_18-52/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
exit
```

![image](https://github.com/user-attachments/assets/7c6b4604-6a86-4e24-a2a0-ec2bb4259aeb)

![image](https://github.com/user-attachments/assets/8d8d1a9b-187f-4680-8f9c-8d3bfab2976e)

![image](https://github.com/user-attachments/assets/ada3e13a-58d7-4363-a458-e7a67c3bce4d)

Now, enter the following commands for exploring post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST':

```
echo $::env(CTS_CLK_BUFFER_LIST)
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
echo $::env(CTS_CLK_BUFFER_LIST)
echo $::env(CURRENT_DEF)
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/placement/picorv32a.placement.def
run_cts
echo $::env(CTS_CLK_BUFFER_LIST)
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/25-03_18-52/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/cts/picorv32a.cts.def
write_db pico_cts1.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew transd net cap input_pins} -format full_clock_expanded -digits 4
report_clock_skew -hold
report_clock_skew -setup
exit
echo $::env(CTS_CLK_BUFFER_LIST)
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]
echo $::env(CTS_CLK_BUFFER_LIST)
```

![image](https://github.com/user-attachments/assets/3fcd48ab-1c5e-4c46-815b-87ce2cb3480b)

![image](https://github.com/user-attachments/assets/317f453b-8b56-4a3d-a4be-1d3609d70c85)

![image](https://github.com/user-attachments/assets/865ebf67-40b8-4c1e-9b4b-e9edf394b114)

### Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

**Maze Routing and Lee's algorithm**

Routing establishes a physical connection between pins, and algorithms like Maze Routing (e.g., the Lee algorithm) are used to find efficient paths on a routing grid. The Lee algorithm starts at a source pin, assigning incremental labels to neighboring cells until reaching the target pin, prioritizing L-shaped routes and using zigzag paths if needed. While effective for finding the shortest path between two pins, the Lee algorithm can be slow for large-scale designs, prompting the use of faster alternatives for handling complex routing tasks.

![image](https://github.com/user-attachments/assets/9016ae8d-1a9f-4b22-ba5f-a445af7bc92d)

**Design Rule Check**

Command to generate Power Distribution Network (PDN):

```
gen_pdn
```

Now, in a new terminal

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/tmp/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 18-pdn.def &
```
![image](https://github.com/user-attachments/assets/3cb4e182-7a3d-4eb0-b223-61f7d7a4d451)

![image](https://github.com/user-attachments/assets/97591be9-402e-4a0a-bf92-4e320f30ec70)

When the power distribution network (PDN) generation command is issued, the system creates the PDN using the design_cts.def file as input.

The PDN consists of power rings, straps, and rails:

- Power is initially drawn from the VDD and VSS pads to the power rings.
- Horizontal and vertical straps are connected to the rings to further distribute power, with these straps channeling power to the rails connected to standard cells.
- Rails are placed at standard cell height intervals, which align with multiples of the track pitch (2.72 in this design), allowing proper power delivery to all standard cells.

In this design:

-Straps are placed on metal layers 4 and 5, while standard cell rails are on metal layer 1.
-Vias are used to interconnect these layers, ensuring seamless power flow from pads to cells across the different metal levels.

![image](https://github.com/user-attachments/assets/1c9f164b-9414-4d71-a9f7-6eef3cb1fe5a)

Now, we perfrom detailed routing using TritonRoute:

```
echo $::env(CURRENT_DEF)
echo $::env(ROUTING_STRATEGY)
run_routing
```

![image](https://github.com/user-attachments/assets/dbbe20fc-dcd4-412a-8d56-b839a9576ca3)

Now, in a new terminal

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/routing/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```

![image](https://github.com/user-attachments/assets/31f6533e-ad22-4efe-94d9-b51a2518a2b1)

Expanded layout showing the custom inverter `sky130_akainv`

![image](https://github.com/user-attachments/assets/fc178a51-17e3-498b-be9b-7f6b273d3e68)

Fast route guide present in `openlane/designs/picorv32a/runs/25-03_18-52/tmp/routing` 

![image](https://github.com/user-attachments/assets/e3ece9df-c2a3-40fa-989a-09eb75755c8e)


**TritonRoute**

TritonRoute performs detailed routing by following pre-processed global route guides and using a MILP-based panel routing scheme. It supports intra-layer parallel routing (simultaneous routing within a layer) and inter-layer sequential routing (from bottom to top metal layers). TritonRoute respects each metal layer's preferred direction (e.g., met1 horizontal, met2 vertical) as defined in the LEF file, minimizing overlapping and potential capacitance issues for improved signal integrity.

![image](https://github.com/user-attachments/assets/25fb2a50-7080-4622-8222-42b49ab59a1f)

![image](https://github.com/user-attachments/assets/56a1e05b-e8dc-44f5-95eb-5a3224a2a7d4)

Feature:

- Pre-processed Route Guides : TritonRoute uses pre-processed route guides generated by the global router. These guides provide an initial path outline, helping TritonRoute achieve efficient, detailed routing by following these predefined paths while optimizing for connectivity and minimizing conflicts.

![image](https://github.com/user-attachments/assets/e4110bf2-ed04-45f5-a5fe-5bc2ef892178)

- Inter-guide Connectivity : In TritonRoute, inter-guide connectivity ensures seamless connections between adjacent route guides. This feature maintains continuity across guide boundaries, allowing signals to pass smoothly from one guide to the next, which helps to reduce routing gaps and improve overall connectivity throughout the design.

![image](https://github.com/user-attachments/assets/65e6a2aa-27f6-4924-829e-b1307c691773)

- Intra-layer Routing: Routing within a single metal layer, performed in parallel to optimize path efficiency.
  
- Inter-layer Routing: Sequential routing across metal layers, starting from the bottom, following layer direction rules to minimize interference.

![image](https://github.com/user-attachments/assets/b2698b8c-c2bc-476a-bc55-4507b44f2a2c)


**TritonRoute method to handle connectivity**

TritonRoute ensures robust connectivity by following global route guides and managing both intra-layer and inter-layer routing. It connects paths within each layer (intra-layer) in parallel and links them across layers (inter-layer) sequentially, from the bottom to the top. This structured approach helps avoid congestion and maintains consistent signal flow throughout the design.

![image](https://github.com/user-attachments/assets/dac5f965-d7a8-4cb4-b667-9d01ffcf36ec)

**Routing Topology Algorithm**

A routing topology algorithm defines the structure and path configuration of connections between pins in an integrated circuit. It aims to create an efficient, minimal-cost layout by determining the best routing paths and shapes.

![image](https://github.com/user-attachments/assets/5b921b96-da9e-4735-a6eb-51d5319bbfb0)


Commands for SPEF extraction Post-Route parasitic extraction using SPEF extractor

```
cd Desktop/work/tools/openlane_working_dir/openlane/scripts/spef_extractor
python3 main.py -l /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/tmp/merged.lef -d /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/routing/picorv32a.def
```

![image](https://github.com/user-attachments/assets/50df375e-a4bf-4c62-9d05-324594b05f2b)


Commands for Post-Route OpenSTA timing analysis with the extracted parasitics of the route:

```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/25-03_18-52/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/routing/picorv32a.def
write_db pico_route.db
read_db pico_route.db
read_verilog /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis_preroute.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
read_spef /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/routing/picorv32a.spef
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
exit
```

![image](https://github.com/user-attachments/assets/fc6175b6-2237-4343-af65-a5bafbdecd09)

![image](https://github.com/user-attachments/assets/eb91bd4f-443f-4e38-b927-5dcba9ff6476)

![image](https://github.com/user-attachments/assets/0c2d04bd-f641-45e2-8975-b9b633bd7734)

## Task-13: OpenRoad Physical Design

#### Path to Zetta-Scale Computing

**Introduction:**

- **Bombe:** The Bombe was an electro-mechanical machine designed during World War II to decrypt German Enigma-encrypted messages. It was refined and built by Alan Turing and Gordon Welchman at Bletchley Park, UK. The Bombe systematically tested possible rotor settings of the Enigma machine by exploiting known plaintext patterns. Its logical operations helped narrow down the vast number of possible keys, significantly accelerating the decryption process. The Bombe played a critical role in the Allied war effort.

- **ENIAC (Electronic Numerical Integrator and Computer):** It was developed during World War II by John Presper Eckert and John Mauchly at the University of Pennsylvania, was the first general-purpose, fully electronic digital computer. Completed in 1945, it was designed to compute artillery firing tables for the U.S. Army. ENIAC used vacuum tubes instead of mechanical or electromechanical components. However, it lacked a stored-program capability, requiring manual reconfiguration for each new task. ENIAC demonstrated the immense potential of electronic computing for large-scale numerical problems.

- **EDVAC (Electronic Discrete Variable Automatic Computer):** EDVAC, also developed by Eckert and Mauchly with conceptual input from John von Neumann, was one of the first computers to implement the stored-program concept. Completed in 1949, EDVAC represented a significant improvement over ENIAC by using binary representation instead of decimal and storing both data and instructions in memory. This innovation simplified programming and laid the groundwork for the modern von Neumann architecture.

**50 Years of Microprocessor Trend Data:**

![image](https://github.com/user-attachments/assets/04124b15-8ba2-4cd9-add6-fd003838fe6c)

**The Key metrics are:**

- **Transistors (Orange Triangles):** The number of transistors on a microprocessor chip (in thousands) has increased exponentially, following Moore's Law, which predicts a doubling approximately every two years. This growth enabled more complex and capable processors, reaching the range of billions of transistors by the 2020s.
- **Single-Thread Performance (Blue Circles):** It is measured using SpecINT. It indicates the computational ability of a single processor core. Performance grew steadily due to improvements in architecture, instruction-level parallelism, and clock speeds, but the growth rate slowed post-2005 due to physical limitations like power and heat.
- **Frequency (Green Diamonds):** Processor clock speed (in MHz) rose steadily until the early 2000s but then stagnated as increasing clock speeds became inefficient due to heat dissipation issues.
- **Typical Power (Red Triangles):** Power consumption increased with transistor density and frequency, becoming a critical design challenge around the mid-2000s.
- **Number of Logical Cores (Black Dots):** The transition to multi-core processors gained momentum in the mid-2000s as a response to the stagnation in single-thread performance. By increasing the number of cores, processors enabled more efficient parallel processing, leading to significant improvements in overall performance

**Key Milestones**

- **iPhone Release (~2007):** Signals the emergence of mobile computing, where power efficiency became as crucial as performance. This catalyzed innovations in low-power processor designs.
- **Datacenter-Scale Computing (Post-2010):** Marks the rise of cloud computing and large-scale data centers, where energy efficiency, scalability, and parallelism became central concerns.

**Path to zetta-scale computing**

![image](https://github.com/user-attachments/assets/7f0a1590-b0ca-4d90-8804-381b30bee78a)

The path to zetta-scale computing, tracing the evolution of computing performance (measured in FLOPS—floating-point operations per second) from the gigascale era in 1984 to the projected zettascale by 2035.

**Key Performance Levels**

- **Gigascale (10⁹ FLOPS):** The starting point in 1984, marking the capability of early supercomputers.
- **Terascale (10¹² FLOPS):** Achieved around 1997, a significant milestone where systems like Jaguar (Cray XT5) delivered teraflop performance with power consumption of 7 MW.
- **Petascale (10¹⁵ FLOPS):** Achieved in 2008 with systems like Titan (Cray XK6) at 27 petaflops, consuming 9 MW. This milestone represents the era of petascale high-performance computing (HPC).
- **Exascale (10¹⁸ FLOPS):** Reached by systems like Frontier (Cray Shasta) in 2021, delivering 1.5 exaflops using 4 AMD GPUs and 1 AMD CPU, consuming 29 MW of power. Exascale computing enables highly detailed simulations and large-scale AI workloads.
- **Zettascale (10²¹ FLOPS):** Projected to be achieved by around 2035. At this scale, systems will handle unprecedented computational workloads, such as advanced climate modeling, AI, and large-scale simulations. Power consumption is estimated to range between 50-100 MW for a single zettascale machine.

**CMOS Evolution and Next-Gen Candidates**

![image](https://github.com/user-attachments/assets/b621caad-384e-4c67-bb01-4504d153230a)

This diagram illustrates the evolving landscape of CMOS (Complementary Metal-Oxide-Semiconductor) technology and highlights emerging materials, structures, and processes being explored for next-generation semiconductor devices. These innovations aim to address the challenges of scaling CMOS technology down to the 1nm node and beyond.


- **Channel Material**
  - **Current Trends**: 
    - Silicon (Si) is the primary material used for the channel in traditional CMOS transistors, with **strained SiGe** (Silicon-Germanium) being used in some high-performance applications to enhance carrier mobility.
  
  - **Future Materials**: 
    - **2D materials** such as MoS₂ (Molybdenum Disulfide) are being explored due to their potential for better electrical characteristics at smaller scales.
    - **Germanium (Ge)** is gaining interest as it offers higher electron mobility, which could significantly boost transistor performance at small nodes.

- **Patterning**
  - **Current Techniques**: 
    - **Deep Ultraviolet (DUV)** lithography is the most commonly used technique for defining transistor features, with **ArF (Argon Fluoride)** and **KrF (Krypton Fluoride)** lasers operating at different wavelengths.
  
  - **Next-Gen**: 
    - **Extreme Ultraviolet (EUV)** lithography is expected to be a key technology for sub-7nm nodes. **High-NA (Numerical Aperture) EUV** will further improve the resolution for even smaller transistor nodes, pushing the boundaries of Moore's Law.

- **Gate Stack Material**
  - **Current Materials**: 
    - **High-K metal gates (HKMG)** are used in the gate stack of modern FETs to reduce gate leakage current and improve switching performance.
  
  - **Next-Gen Candidates**:
    - **NC-FET (Negative Capacitance FET)**: This is a promising transistor design that leverages ferroelectric materials to reduce power consumption by enabling lower voltage operation.
    - **TFET (Tunnel FET)**: TFETs use quantum tunneling to switch on and off, offering a significant reduction in power consumption compared to conventional FETs, especially for low-power applications.

- **Interconnection Material**
  - **Current Materials**: 
    - **Copper (Cu)** is the primary material used for interconnects due to its low resistivity, which helps in minimizing power loss and delays in transistor connections.
  
  - **Next-Gen Materials**:
    - **Ruthenium (Ru)** and **Compound metals** are being investigated for their potential to reduce resistance and improve performance in ultra-small transistors.
    - **Topological semi-metals** may offer unique properties, such as lower resistivity and increased performance at the atomic scale.


- **Device Structure**
  - **Current Architectures**: 
    - **FinFET** and **planar** transistors are used to maintain performance at smaller nodes. FinFETs, in particular, help improve control over short-channel effects by using a 3D structure.
  
  - **Next-Gen Architectures**:
    - **3DS-FET (3D Stacked FET)**: These are three-dimensional transistors where multiple layers of devices are stacked vertically, reducing footprint and improving performance.
    - **MBC-FET (Multi-Bridge Channel FET)**: This structure aims to enhance drive current by creating multiple channels within the same device.
    - **VFET (Vertical FET)**: VFETs utilize vertical channels to improve density and reduce power consumption.

- **Design Co-Optimization**
  - **DTCO (Design-Technology Co-Optimization)**: 
    - DTCO focuses on integrating new design techniques with advanced process technologies to maximize chip performance, often involving **backside interconnects (BSI)**, where interconnections are made at the back of the wafer for improved signal integrity and reduced latency.
  
  - **STCO (System-Technology Co-Optimization)**: 
    - This approach involves optimizing both the system architecture and the underlying technology. One example is the use of **chiplets**, which allow for modular, customized designs by integrating multiple smaller chips into one package, offering flexibility and reducing the complexity of scaling single-chip designs.

#### FinFETs

![image](https://github.com/user-attachments/assets/de21941f-7456-4522-b07f-a365cf9fe9b0)

This diagram illustrates the evolution of transistor technology from planar to more advanced architectures like FinFET and Gate-All-Around (GAA):

1. **Planar Transistor (Traditional)**:
   - Early transistor design with a flat channel and gate structure.
   - The gate controls the channel from one side only, leading to limited performance as scaling continues.

2. **FinFET (2011)**:
   - The channel is shaped like a vertical fin, allowing the gate to wrap around three sides of the channel.
   - Provides better control over the channel, reducing leakage and improving performance at smaller sizes.

3. **Gate-All-Around (GAA) Transistor (2025?)**:
   - The gate completely surrounds the channel, typically implemented using stacked nanosheets or nanowires.
   - Offers even better control over the channel compared to FinFET, allowing higher performance and efficiency with continued scaling.

Each step improves drive current capability and enhances control over the transistor's on/off states, critical for power efficiency and miniaturization in modern electronics.

**Why FinFETs and Gate-All-Around Transistors?**

![image](https://github.com/user-attachments/assets/067b362e-bd68-40e4-b83c-60f2c3ef5797)

This diagram explains the advantages of FinFETs and Gate-All-Around (GAA) transistors compared to traditional planar structures:

 1. **Planar Transistors:**
   - **Challenges:**
     - Sub-channel leakage occurs where current leaks underneath the gate.
     - Results in reduced efficiency.
     - Increases power consumption.

2. **FinFET Transistors:**
   - The gate wraps around the channel (fin) on three sides, providing better control over the channel.
   - **Benefits:**
     - Reduces sub-threshold leakage.
     - Enhances drive current (\(I_{ON}\)).
     - Allows a smaller transistor area while maintaining high performance.

3. **Gate-All-Around (GAA) Transistors:**
   - The gate completely surrounds the channel, offering superior electrostatic control.
   - **Advantages:**
     - Improves short-channel performance by reducing drain capacitance and enhancing gate capacitance.
     - Improves scaling efficiency as indicated by the formula \(S \propto (1 + C_d / C_{ox})\).
     - Provides reduced sub-threshold slope and better performance at smaller scales.

4. **Graph Comparison:**
   - Illustrates the performance advantages of FinFETs and GAA over planar transistors.
   - Shows better efficiency and reduced sub-threshold slope as dimensions shrink.

![image](https://github.com/user-attachments/assets/29504769-f396-4838-8ebb-abacfaf8a27f)

**Reduced Leakage:** Tri-Gate transistors exhibit significantly lower leakage current compared to planar transistors at the same gate voltage. Lower leakage results in both reduced off-current at the same on-current and lower power dissipation.

**Higher Drive Current:** Tri-Gate transistors provide higher drive current compared to planar transistors at the same off-current. This results in improved circuit performance and greater efficiency in modern electronic applications.

#### FEOL Innovations:

FEOL refers to the initial stages of semiconductor manufacturing where the active devices (e.g., transistors) are built on the silicon wafer. It involves creating components such as transistors, capacitors, and isolation structures before metal interconnects are added. FEOL Innovations help drive Moore's Law forward by enabling smaller, more efficient, and more powerful transistors.

**CMOS Technology Inflection Points**

![image](https://github.com/user-attachments/assets/66560a1e-fd66-40dc-94ed-9de5938f045c)

1. **Dennard Scaling**:
   - States that power density remains constant as transistors shrink.
   - Initially allowed voltage scaling with smaller gate lengths, shown in the bottom-left graph.

2. **Technology Nodes and Innovations**:
   - **~1 µm ("End of Scaling")**: Start of CMOS miniaturization.
   - **180 nm (Voltage Scaling)**: Start of drive voltage reduction.
   - **130 nm (Cu BEOL)**: Introduction of copper interconnects for better conductivity.
   - **90 nm (Uniaxial Strained Si NMOS)**: Strained silicon enhances electron mobility.
   - **65 nm (eSiGe CVD ULK)**: Embedded SiGe improves PMOS performance.
   - **45 nm (HK-first MG-last)**: High-k dielectrics and metal gates reduce leakage and improve gate control.
   - **32 nm (HKMG with Raised S/D NMOS)**: Advanced HKMG implementation and raised source/drain regions.

3. **SEM Images**

- **Left Image:** Shows the cross-sectional view of a transistor structure with High-k materials and embedded SiGe (Silicon-Germanium).It has high-k dielectric and metal gates are used to improve performance. SiGe regions enhance PMOS performance by applying strain to the silicon channel.

- **Right Image:** Demonstrates the raised source/drain (S/D) regions and gate channel in PMOS transistors at smaller nodes.

4. **Drive Voltage Scaling Graph (Bottom-left):** The graph shows the relationship between gate length (x-axis, logarithmic scale) and drive voltage (y-axis, logarithmic scale). The Ideal scaling behavior indicates that the voltage decreases linearly with shrinking gate length. Red and green markers show practical trends for low-power and high-performance devices, which deviate from ideal scaling due to challenges like leakage currents and increased power density.

![image](https://github.com/user-attachments/assets/10c7507f-19a8-422c-9ef3-4f044e900766)

**Key Technology Nodes and Innovations**

- **22 nm**:
  - Introduction of **FinFET (Tri-Gate)** transistors, which reduce leakage and improve gate control.
  - Use of **self-aligned contacts (SAC)** and **copper interconnects (Co+Cu BEOL)**.

- **14 nm**:
  - Transition to **unidirectional metal routing** for better density.
  - Implementation of **SADP (Self-Aligned Double Patterning)** and **SDB (Single Diffusion Break)** for precise layout.

- **10 nm**:
  - Adoption of **advanced patterning techniques** such as:
    - **SA-SDB** (Self-Aligned SDB)
    - **LELELE** (Litho-Etch-Litho-Etch-Litho-Etch)
    - **SAQP (Self-Aligned Quadruple Patterning)** for tighter geometries.

- **7 nm**:
  - Introduction of **Extreme Ultraviolet Lithography (EUV)** to simplify the patterning process and reduce overlay errors.

- **5 nm**:
  - Integration of **SiGe (Silicon-Germanium) channels** for PMOS to enhance hole mobility.
  - Use of **EUV SA-LELE** (Self-Aligned Litho-Etch-Litho-Etch).

- **3 nm / 2 nm / 1.4 nm**:
  - Transition to **Gate-All-Around (GAA)** nanosheet transistors for improved electrostatic control.
  - GAA stacks nanosheets or nanowires horizontally to maximize current drive.

- **Sub-1 nm**:
  - Development of **CFET (Complementary FET)**, which vertically stacks NMOS over PMOS to save area.
  - Use of **2D materials**, such as **MoS₂**, for atomic-scale channel thickness in **2D FETs**.

![image](https://github.com/user-attachments/assets/a8ad69be-9750-44f0-97b6-c39f1b58e18c)

The image illustrates how Samsung has scaled down the size of transistors in their successive generations of nodes (10nm, 8nm, 7nm, and 5nm) using a technique called Fin Depopulation. In FinFET transistors, the "fin" is the vertical channel that carries the current. Fin Depopulation involves reducing the number of fins per transistor while keeping the fin width constant. This allows for smaller transistors without compromising performance.

- 10nm (HD): The transistor has a fin height of 420nm and uses 10 fins.
- 8nm (UHD): The fin height is reduced to 378nm, and the number of fins is decreased to 9.
- 7nm (HD): The fin height remains at 27nm, but the number of fins is further reduced to 8.
- 5nm (UHD): The fin height is maintained at 27nm, and the number of fins is decreased to 7.

![image](https://github.com/user-attachments/assets/c6bc381c-f5de-4839-98a9-e61f56b61622)

- **Double Diffusion Break (DDB)**: Double Diffusion Break (DDB) involves creating a gap between the source and drain regions of a transistor. This gap is filled with an insulating material, which reduces the effective width of the transistor. By doing so, DDB enables the design of smaller cell sizes, allowing for higher transistor density and improved scalability. A cross-sectional view of a transistor with DDB highlights the insulating gap between the source and drain regions.

- **Single Diffusion Break (SDB)**: Single Diffusion Break (SDB) is similar to DDB but less aggressive. It involves introducing a gap on only one side of the transistor. This approach provides a balanced trade-off between size reduction and maintaining transistor performance. A cross-section of a transistor with SDB highlights the gap on one side, showcasing its simplicity compared to DDB.

- **Contact Over Field Gate (COFG)**: Contact Over Field Gate (COFG) places the gate contact directly over the field oxide region of a transistor. This design reduces lateral spacing between adjacent transistors, enabling smaller cell sizes without significant performance loss. A cross-sectional representation of a transistor with COFG illustrates the positioning of the gate contact over the field oxide.

- **Contact Over Active Gate (COAG)**: Contact Over Active Gate (COAG) is a more aggressive technique than COFG. Here, the gate contact is placed directly over the active gate region of the transistor. This approach enables even smaller cell sizes and higher transistor density, which are critical for advanced semiconductor nodes. A cross-sectional image of a transistor with COAG highlights the gate contact placement over the active gate.

- **Back-Side Power Delivery Network (BS-PDN)**: The Back-Side Power Delivery Network (BS-PDN) is an innovative approach where power supply rails are routed on the backside of the chip. This method reduces the height of the standard cell, creating space for more transistors and improving overall transistor density. Additionally, it enhances power delivery efficiency and reduces resistance, which is crucial for high-performance applications. A schematic of a standard cell with BS-PDN illustrates the positioning of power rails on the backside of the chip.

![image](https://github.com/user-attachments/assets/d8288063-a78a-40cb-a80b-7f9fe8d351bc)

- **Planar Technology**: In early planar technology nodes (100nm and above), the Vt variability is significantly high, around 130mV. This is due to various factors like process variations, temperature fluctuations, and line-edge roughness.

- **FinFET Technology**: With the advent of FinFET technology (around 22nm), the Vt variability reduces significantly to around 14mV. This improvement is attributed to the better control over the channel length and width in FinFETs compared to planar transistors.

- **NW Technology (Nanowire)**: In the latest nanowire technology (14nm and below), the Vt variability is even lower, around 7mV. This further reduction is due to the precise control over the nanowire dimensions and the reduced impact of process variations.

![image](https://github.com/user-attachments/assets/43ec16fc-dac1-4ac4-9492-ef7413e39ef6)

**Planar MOSFETs**  
Planar MOSFETs, the traditional architecture, have a simple structure where the gate sits above the channel. In this design, the contact width (\(W_C\)) and gate width (\(W_G\)) are nearly equal, resulting in a ratio of \(W_C / W_G \approx 1\). This leads to a low parasitic resistance, with \(R_{EXT}\) being much smaller than \(R_{ch}\) (\(R_{EXT} / R_{ch} < 1\)). As a result, planar MOSFETs suffer minimal performance degradation due to parasitic resistance.

**FinFETs**  
FinFETs, a 3D transistor design, introduce vertical fins with the gate wrapping around them for improved control. However, the effective contact width decreases relative to the gate width, leading to \(W_C / W_G \approx 1/3\). Consequently, the parasitic resistance becomes comparable to the channel resistance (\(R_{EXT} / R_{ch} \approx 1\)), which begins to impact the performance of the device as it scales.

**Gate-All-Around (GAA) FETs**  
Gate-All-Around (GAA) FETs, which use nanosheets or nanowires, offer even better electrostatic control by fully surrounding the channel with the gate. However, the contact width further decreases compared to the gate width, resulting in \(W_C / W_G \approx 1/6\). This causes a significant increase in parasitic resistance, with \(R_{EXT}\) being approximately three times the channel resistance (\(R_{EXT} / R_{ch} \approx 3\)). While GAA FETs improve transistor density, the higher parasitic resistance becomes a challenge for maintaining performance.

**Complementary FETs (CFETs)**  
Complementary FETs (CFETs) take transistor stacking to the next level by vertically integrating NMOS and PMOS transistors. This approach maximizes space efficiency in advanced nodes but inherits the high parasitic resistance of GAA FETs. With \(W_C / W_G\) remaining small, the \(R_{EXT} / R_{ch}\) ratio is around 3, posing similar challenges to those faced by GAA FETs.

**Explanation of Parasitic Resistance**

![image](https://github.com/user-attachments/assets/6ab0011f-36de-4821-ab59-74fa2ce2beda)

The image highlights the breakdown of parasitic resistance (\(R_{EXT}\)) and approaches for reducing it in transistors. Here is a detailed explanation:

1. **Components of Parasitic Resistance (\(R_{EXT}\))**
The leftmost diagram illustrates the various contributors to \(R_{EXT}\) in a transistor:
- **\(R_{CA-BEOL}\)**: Resistance from the contact in the Back-End-Of-Line (BEOL).
- **\(R_{CA}\)**: Resistance at the contact area.
- **\(R_{CA-TS}\)**: Resistance at the contact to the transition structure.
- **\(R_{TS}\)**: Resistance in the transition structure.
- **\(R_{MOL}\)**: Middle-Of-Line resistance (includes lateral and vertical contributions).
- **\(R_C\)**: Contact resistance at the metal-semiconductor interface.
- **\(R_{EPI}\)**: Epitaxial layer resistance (contributes to current spreading).
- **\(R_{FEOL}\)**: Front-End-Of-Line resistance from the source/drain extensions.

2. **Initial vs. Improved \(R_{EXT}\) Breakdown**
The two pie charts in the center show the contributions of different resistance components for NFETs and PFETs before and after improvements:
- **NFET**:
  - **Initial**: Majority of \(R_{EXT}\) comes from \(R_C\) (63%) and \(R_{CA-BEOL}\) (31%).
  - **Improved**: Significant reduction in \(R_C\) (48%) and \(R_{CA-BEOL}\) (12%).
- **PFET**:
  - **Initial**: \(R_{FEOL}\) (50%) and \(R_C\) (45%) dominate.
  - **Improved**: Major reduction in \(R_{FEOL}\) (78%) and \(R_C\) (16%).

3. **Improving Ohmic/Tunneling Contacts**
The right section discusses methods to improve the metal-semiconductor interface:
- **Key Objectives**:
  - **Low Schottky Barrier Height (SBH)** (\(\phi_b\)): Reduces the energy barrier for carrier injection, enabling better contact conductivity.
  - **High Doping Concentration (\(N_d\))**: Increases carrier density at the interface, reducing contact resistance.
- **Equation for Specific Contact Resistivity (\(\rho_c\))**:
  \[
  \rho_c \propto \exp\left(\frac{2\phi_b}{\hbar} \sqrt{\frac{\epsilon_s m_x}{N_d}}\right)
  \]
  This equation shows how lowering \(\phi_b\) and increasing \(N_d\) can reduce \(\rho_c\).

- **Metal-Semiconductor Energy Diagram**:
  - The energy diagram shows how a reduction in \(\phi_b\) (Schottky Barrier Height) facilitates easier carrier injection from the metal to the semiconductor.

![image](https://github.com/user-attachments/assets/ed9743a8-c9f0-43d5-9ccd-4b239f8718ac)

The bar chart on the left shows how the composition of \(C_{eff}\) evolves from 22nm to 7nm technology nodes:

- At **22nm**, the dominant contributor to \(C_{eff}\) is \(C_{fr}\) (56%), while parasitic capacitances \(C_{pc-ca}\) (25%) and \(C_{g}\) (19%) contribute less.
- At **14nm** and **10nm**, parasitic capacitances (\(C_{pc-ca}\) and \(C_{fr}\)) start dominating, with \(C_{fr}\) decreasing to 38% and 25%, respectively, while \(C_{pc-ca}\) increases.
- At **7nm**, \(C_{g}\) becomes the most significant contributor (45%), with \(C_{pc-ca}\) and \(C_{fr}\) still present but reduced. This highlights the increasing impact of parasitic capacitance as node sizes shrink.

Plot Descriptions:

- The first scatter plot shows a reduction in normalized delay for a ring oscillator when using SiBCN spacers instead of SiN spacers, indicating improved performance.
- The second scatter plot demonstrates an 8% reduction in \(C_{eff}\) with SiBCN spacers, which corresponds to the delay improvement observed in the first plot.
- The rightmost figure shows the evolution of spacer materials from SiOCN to SiCO. This material transition aims to significantly reduce the gate-contact capacitance across nodes. At 14nm and beyond, low-\(k\) spacers improve performance by decoupling parasitic effects and maintaining capacitance at manageable levels.
- The bottom middle image shows a cross-sectional TEM view of a transistor with air spacers around the gate: i) Air, with its extremely low dielectric constant (\(k \approx 1\)), significantly reduces parasitic capacitance. The adjacent plot quantifies this improvement, showing a 15% reduction in \(C_{eff}\) when using air spacers compared to solid spacers.

![image](https://github.com/user-attachments/assets/848c85f2-a2d5-4872-9690-b6eaf1a11dd2)

**Key Properties of 2D Layered Materials (Compared to Silicon):**

- **Uniform Atomic Scale Thickness:** A single layer of MoS₂ is approximately 0.65 nm thick, offering an ideal thickness for scaling compared to silicon. 
- **Higher Effective Mass (\( m^* \)):** MoS₂ has an effective mass of about 0.55 times the mass of a free electron (\( m_0 \)), whereas silicon’s effective mass is around 0.22 \( m_0 \).
- **Bandgap:** Additionally, 2D materials like MoS₂ possess favorable bandgaps for electronic devices, with a monolayer bandgap of ~1.85 eV, which reduces to ~1.5 eV for a bilayer.

![image](https://github.com/user-attachments/assets/957f8ce6-cd3d-4fd3-bd3e-c99909752cdf)

1. **Transistor Scaling**:  
   - To achieve smaller gate lengths, devices must address various physical and material constraints to ensure reliable operation.

2. **Challenges for Scaling**:
   - **Direct Source-to-Drain Tunneling**: As the gate length decreases, electrons can tunnel directly from the source to the drain, bypassing the gate control. To mitigate this, materials with a high effective mass (\( m^* \)) are needed.
   - **Surface Roughness and Thickness Variations**: Variability at atomic scales can cause performance issues. Uniform, atomically thin materials are essential for minimizing such variations.
   - **Capacitance Ratios (\( C_D \) and \( C_{ox} \))**: The capacitance of the depletion region (\( C_D \)) must remain low relative to the gate oxide capacitance (\( C_{ox} \)) to improve gate control. Materials with a low in-plane dielectric constant (\( \epsilon \)) are necessary for this.

3. **Diagrams**:  
   - The left shows the transistor structure with key components like the source, drain, gate, oxide, and silicon substrate.
   - The right illustrates two scenarios:  
     a. *Thermionic Emission*: Electrons cross the energy barrier as intended.  
     b. *Direct Tunneling*: At extremely small gate lengths, electrons tunnel directly from source to drain, leading to leakage.

4. **Key Takeaway**:  
   - New channel materials, such as 2D materials, are required to overcome these challenges while maintaining high performance and scalability.

![image](https://github.com/user-attachments/assets/716a2a87-2051-4de1-be37-aa4f70f73fa0)

Concept of Direct Source-to-Drain Tunneling: As the gate length (\(L_G\)) in MOSFETs decreases, direct tunneling of electrons from the source to the drain becomes significant, leading to increased leakage currents. This leakage is influenced by material properties, such as the effective mass (\(m^*\)) and the bandgap (\(E_G\)).

A higher \(m^*\) in MoS₂ suppresses tunneling leakage compared to silicon. The graph shows the leakage current (\(I_{SD, \text{leak}}\)) as a function of gate length (\(L_G\)) for various channel thicknesses (\(T_{CH}\)). MoS₂ exhibits lower leakage at smaller gate lengths compared to silicon, achieving up to 100x reduction in leakage due to its higher \(m^*\), larger \(E_G\), and lower dielectric constant (\(\epsilon\)).

The superior performance of MoS₂ in minimizing leakage currents results in significant energy savings, making it a promising material for future transistor scaling.

![image](https://github.com/user-attachments/assets/333769a9-e265-4e58-ba3a-47dffc7ac60e)

The MoS₂ transistor with a 1 nm gate length represents a breakthrough in miniaturization, featuring a thin MoS₂ channel for its excellent electronic properties. A single-walled carbon nanotube (SWCNT) serves as the ultra-small gate electrode, while Zirconium Dioxide (ZrO₂) acts as a high-k dielectric, reducing leakage and ensuring precise control. Built on a SiO₂ substrate with an n⁺ silicon back gate, the transistor uses the CNT gate to deplete a small region of the MoS₂ channel, enabling efficient modulation. This innovative design showcases the potential of 2D materials and nanoscale gates in advancing transistor technology.

![image](https://github.com/user-attachments/assets/e2eef453-2d6f-4a72-ae50-5aa6d36bdfeb)

The slide illustrates the structure and fabrication of an All-2D MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor), where all key components, including the channel, gate, and contacts, are made using two-dimensional materials. This device leverages the exceptional properties of 2D materials to improve performance and scalability. Below is a breakdown of the key components and the fabrication process:

**Graphene Contacts (S, D, G):** Graphene is used as the source, drain, and gate electrodes. Its high conductivity and 2D nature make it ideal for ensuring low-resistance electrical contacts.
MoS₂ Channel:

**Molybdenum Disulfide (MoS₂)** serves as the semiconductor channel. MoS₂ is widely used in 2D MOSFETs due to its excellent on/off current ratio and atomic-scale thickness.
h-BN Dielectric:

**Hexagonal Boron Nitride (h-BN)** acts as the insulating dielectric layer. It is a 2D material with excellent insulating properties and high thermal stability, making it suitable for separating the graphene gate from the MoS₂ channel.
Si/SiO₂ Substrate:

The device is fabricated on a silicon dioxide (SiO₂) layer on top of a silicon substrate, which provides mechanical support and a global back gate.
Fabrication Process:

- A layer of graphene is deposited on the SiO₂ substrate, which will later serve as the gate electrode.
- Graphene is patterned to define the source and drain regions, leaving gaps for the channel.
- A monolayer of MoS₂ is transferred onto the patterned graphene, forming the channel region.
- An h-BN layer is added on top of the MoS₂ as the gate dielectric.
- A top layer of graphene is deposited and aligned as the gate electrode.
- The completed device is contacted using metallic electrodes (Ni/Au) for testing.

![image](https://github.com/user-attachments/assets/2fc6e2ec-8754-42c5-af4a-7900be09703a)

The All-2D MOSFET exhibits excellent electrical performance:

- **Transfer Characteristics (I\(_D\) vs V\(_G\))**: Achieves a high on/off current ratio (>10⁵), demonstrating strong gate control for effective switching.
- **Output Characteristics (I\(_D\) vs V\(_{DS}\))**: Smooth current modulation with increasing V\(_G\) and V\(_{DS}\), indicating good output performance.
- **Mobility**: Field-effect mobility remains constant with increasing gate electric field, showing minimal scattering and high-quality interfaces in the 2D materials stack.

These results highlight the potential of 2D materials like MoS₂, graphene, and h-BN for scalable, high-performance transistor applications.

![image](https://github.com/user-attachments/assets/24936d7c-1d95-4150-adab-639feb54d0b0)

The diagram on the top left shows a non-planar transistor with key components:

- Gate: Controls the flow of current through the channel.
- Channel: Region where current flows between the source (S) and drain (D).
- Body: Underlying region connected to the substrate.
- STI (Shallow Trench Isolation): Insulates neighboring devices.

The biggest challenge is to form a single-crystalline semiconductors on a non-planar surface is difficult using conventional semiconductor fabrication techniques.

![image](https://github.com/user-attachments/assets/09db667f-dd86-4ba5-9357-29bc6124febb)

Single-Layer CMOS (a): This is the traditional CMOS design where NMOS and PMOS transistors are fabricated on a single silicon layer. Each transistor operates in the same planar layer, with devices connected laterally.

Monolithic 3D CMOS (b): In this design, NMOS and PMOS transistors are stacked in two separate layers, enabling higher density. The P-Channel (PMOS) is placed on top of the N-Channel (NMOS), separated by an oxide layer. This approach reduces the footprint and allows better performance due to shorter interconnects.

Single-Layer CMOS Logic (c): Shows logic gates (inverter, 2-input NAND, and 2-input NOR) built using traditional single-layer CMOS. Transistors are laid out horizontally, with interconnections taking more space.

Monolithic 3D CMOS Logic (d): Logic gates are constructed with two transistor layers (Layer 1 and Layer 2), reducing the area required for interconnections. Vertical integration improves performance and reduces delay by shortening signal paths.

![image](https://github.com/user-attachments/assets/a83936b9-267d-4e3f-a1b5-8539b156b712)


**Dual Damascene Cu**, used for the 7nm technology node with a 36nm pitch, combines vias (vertical connections) and lines (horizontal connections) in a single patterning step. It relies on copper (Cu) for interconnections; however, as dimensions shrink, challenges such as gap filling and maintaining reliability become increasingly significant.

**Single Damascene Cu**, used for the 5nm technology node with a 28nm pitch, involves splitting the creation of vias (vertical connections) and lines (horizontal connections) into separate steps. This approach addresses the challenges of smaller dimensions, with a primary focus on reducing resistance (R) in both lines and vias to maintain optimal performance.

**Barrier and via metal optimization**, introduced at the 3nm technology node with a 20-24nm pitch, focuses on reducing the thickness of barrier layers (insulating layers) to minimize resistance while maintaining robust and reliable via connections. This optimization is essential to meet the performance and scaling demands of advanced nodes.

At sub-18nm pitch, **subtractive RIE** and alternative metals like ruthenium (Ru) are introduced to address the reliability and scaling challenges faced by traditional copper interconnects. Subtractive Reactive Ion Etching (RIE) enables more precise patterning of interconnects, while the use of Ru provides improved performance and durability at such advanced dimensions.

For future nodes with pitches below 15nm, **post-Damascene interconnects** featuring tall, barrier-less designs are envisioned. This approach enhances electromigration (EM) reliability, ensuring durable and robust connections despite the continued shrinking of dimensions, thereby addressing key challenges in advanced interconnect scaling.

![image](https://github.com/user-attachments/assets/b0e1ee7f-3987-4ad4-b1ed-6030fcd2b1bf)

The image shows how a selective barrier, typically tantalum nitride (TaN), can improve copper interconnects in semiconductor manufacturing. This barrier reduces resistance, enhances reliability by preventing copper ion migration, and aids in controlling copper thickness. The process involves cleaning the copper surface, depositing TaN using atomic layer deposition (ALD), and removing sacrificial layers. This technique is crucial for advancing semiconductor technology and ensuring reliable, high-performance devices.

![image](https://github.com/user-attachments/assets/b1083105-a723-4f5f-aa37-5f3c5bf1a9be)

**Back-Side Power Delivery Network (BS-PDN)**

In advanced semiconductor manufacturing, efficient power delivery is critical to the performance and reliability of integrated circuits. Traditional Front-Side Power Delivery Networks (FS-PDNs) often suffer from high IR-drop, which can limit device performance and reliability. To address this challenge, Back-Side Power Delivery Networks (BS-PDNs) have emerged as a promising solution.

BS-PDNs involve routing power supply rails on the backside of the chip, enabling shorter and wider power lines. This configuration significantly reduces IR-drop, leading to improved power delivery efficiency. As a result, BS-PDNs offer several advantages:

- Reduced IR-drop: Lower voltage drops across the power network, leading to improved performance and reliability.
- Decreased standard cell area: More efficient power delivery allows for smaller standard cell sizes.
- Improved performance: Lower IR-drop leads to faster switching speeds and reduced power dissipation.

By adopting BS-PDNs, semiconductor manufacturers can develop high-performance and energy-efficient integrated circuits that meet the demands of modern electronics.


**Installing and setting up ORFS**

```
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
cd OpenROAD-flow-scripts
sudo ./setup.sh
```

![image](https://github.com/user-attachments/assets/bec63ae7-4659-42e3-9c01-159a380316a7)

![image](https://github.com/user-attachments/assets/45108685-7362-47ee-b148-e7d1a7552a18)

```
./build_openroad.sh --local
```

![image](https://github.com/user-attachments/assets/2108fc17-2bb9-40cb-a30c-36cc0490dc8a)

![image](https://github.com/user-attachments/assets/8cc97b6f-f231-4f19-9bd9-e2da6e5980b3)

**Verify Installation**

```
source ./env.sh
yosys -help
openroad -help
cd flow
make
```
![image](https://github.com/user-attachments/assets/168b53ca-fb2d-441d-8aa8-2b0178abbb54)

![image](https://github.com/user-attachments/assets/aaf920bb-12e3-4044-a0a9-930b3ef748e9)

```
make gui_final
```
![image](https://github.com/user-attachments/assets/a7b0cca8-5296-4805-88fd-485a720e1bd5)


**ORFS Directory Structure and File formats**

![image](https://github.com/user-attachments/assets/e4f741ad-3f48-4e9a-a799-c8ff95bc74cf)


``` 
├── OpenROAD-flow-scripts             
│   ├── docker           -> It has Docker based installation, run scripts and all saved here
│   ├── docs             -> Documentation for OpenROAD or its flow scripts.  
│   ├── flow             -> Files related to run RTL to GDS flow  
|   ├── jenkins          -> It contains the regression test designed for each build update
│   ├── tools            -> It contains all the required tools to run RTL to GDS flow
│   ├── etc              -> Has the dependency installer script and other things
│   ├── setup_env.sh     -> Its the source file to source all our OpenROAD rules to run the RTL to GDS flow
```

Now, go to flow directory

![image](https://github.com/user-attachments/assets/70cb9a6b-b48c-497e-a050-dd6a5b90ea1d)

``` 
├── flow           
│   ├── design           -> It has built-in examples from RTL to GDS flow across different technology nodes
│   ├── makefile         -> The automated flow runs through makefile setup
│   ├── platform         -> It has different technology note libraries, lef files, GDS etc 
|   ├── tutorials        
│   ├── util            
│   ├── scripts             
```

Automated RTL2GDS Flow for VSDBabySoC:

Initial Steps:

- We need to create a directory `vsdbabysoc` inside `OpenROAD-flow-scripts/flow/designs/sky130hd`
- Now create a directory `vsdbabysoc` inside `OpenROAD-flow-scripts/flow/designs/src` and include all the verilog files here.
- Now copy the folders `gds`, `include`, `lef` and `lib` from the VSDBabySoC folder in your system into this directory.
  - The `gds` folder would contain the files `avsddac.gds` and `avsdpll.gds`
  - The `include` folder would contain the files `sandpiper.vh`, `sandpiper_gen.vh`, `sp_default.vh` and `sp_verilog.vh`
  - The `gds` folder would contain the files `avsddac.lef` and `avsdpll.lef`
  - The `lib` folder would contain the files `avsddac.lib` and `avsdpll.lib`
- Now copy the constraints file(`vsdbabysoc_synthesis.sdc`) from the VSDBabySoC folder in your system into this directory.
- Now copy the files(`macro.cfg` and `pin_order.cfg`) from the VSDBabySoC folder in your system into this directory.
- Now, create a `config.mk` file whose contents are shown below:

```
export DESIGN_NICKNAME = vsdbabysoc
export DESIGN_NAME = vsdbabysoc
export PLATFORM    = sky130hd

# export VERILOG_FILES_BLACKBOX = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/IPs/*.v
# export VERILOG_FILES = $(sort $(wildcard $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/*.v))
# Explicitly list the Verilog files for synthesis
export VERILOG_FILES = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/vsdbabysoc.v \
                       $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/rvmyth.v \
                       $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/clk_gate.v

export SDC_FILE      = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/vsdbabysoc_synthesis.sdc

export vsdbabysoc_DIR = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)

export VERILOG_INCLUDE_DIRS = $(wildcard $(vsdbabysoc_DIR)/include/)
# export SDC_FILE      = $(wildcard $(vsdbabysoc_DIR)/sdc/*.sdc)
export ADDITIONAL_GDS  = $(wildcard $(vsdbabysoc_DIR)/gds/*.gds.gz)
export ADDITIONAL_LEFS  = $(wildcard $(vsdbabysoc_DIR)/lef/*.lef)
export ADDITIONAL_LIBS = $(wildcard $(vsdbabysoc_DIR)/lib/*.lib)
# export PDN_TCL = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/pdn.tcl

# Clock Configuration (vsdbabysoc specific)
# export CLOCK_PERIOD = 20.0
export CLOCK_PORT = CLK
export CLOCK_NET = $(CLOCK_PORT)

# Floorplanning Configuration (vsdbabysoc specific)
export FP_PIN_ORDER_CFG = $(wildcard $(DESIGN_DIR)/pin_order.cfg)
# export FP_SIZING = absolute

export DIE_AREA   = 0 0 1600 1600
export CORE_AREA  = 20 20 1590 1590

# Placement Configuration (vsdbabysoc specific)
export MACRO_PLACEMENT_CFG = $(wildcard $(DESIGN_DIR)/macro.cfg)
export PLACE_PINS_ARGS = -exclude left:0-600 -exclude left:1000-1600: -exclude right:* -exclude top:* -exclude bottom:*
# export MACRO_PLACEMENT = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/macro_placement.cfg

export TNS_END_PERCENT = 100
export REMOVE_ABC_BUFFERS = 1

# Magic Tool Configuration
export MAGIC_ZEROIZE_ORIGIN = 0
export MAGIC_EXT_USE_GDS = 1

# CTS tuning
export CTS_BUF_DISTANCE = 600
export SKIP_GATE_CLONING = 1

# export CORE_UTILIZATION=0.1  # Reduce this value to allow more whitespace for routing.
```

Now go to terminal and run the following commands:

```
cd OpenROAD-flow-scripts
source env.sh
cd flow
```

Commands for **synthesis**:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk synth
```

![image](https://github.com/user-attachments/assets/b61006cd-554c-425d-9bfb-6d6fa947118d)

![image](https://github.com/user-attachments/assets/353513a3-8272-4ddf-b178-eff0d70650a9)

Synthesis netlist:

![image](https://github.com/user-attachments/assets/c2464bd4-c95a-4917-b71d-4ffb7f031950)

Synthesis log:

![image](https://github.com/user-attachments/assets/9cd5f73d-a4cc-4174-889d-872eeff31fe0)

Synthesis Check:

![image](https://github.com/user-attachments/assets/aba75cdc-42ae-4989-b566-3f812ac5667d)

Synthesis Stats:

![image](https://github.com/user-attachments/assets/8553380f-abbb-4ea4-be61-5a59d092ed50)

![image](https://github.com/user-attachments/assets/b8bfc7c4-6a90-4697-8ad6-a3f33992f89d)

![image](https://github.com/user-attachments/assets/11ef305e-06b7-4124-a279-16198e18f120)

![image](https://github.com/user-attachments/assets/d1b7114f-8e88-465a-b4ba-c2f32a8bf312)

Commands for **floorplan**:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
```

![image](https://github.com/user-attachments/assets/46de8e09-36da-4678-b8a2-05a3623c8b34)

![image](https://github.com/user-attachments/assets/ce8cf1e2-ec77-4b8c-8de5-d60cbc16a8b9)

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_floorplan
```
![image](https://github.com/user-attachments/assets/9398bb6a-51a7-41c7-9df6-7e15cfc14c1d)

![image](https://github.com/user-attachments/assets/57b1075e-cb18-4922-b0f8-e055bf5661d8)

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place
```

![image](https://github.com/user-attachments/assets/33a6fe07-fd13-435f-9cf0-a4ebdc313842)

![image](https://github.com/user-attachments/assets/e165bdba-914e-417e-9578-630bd2b63514)

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_place
```

![image](https://github.com/user-attachments/assets/8df8d550-d1e7-447e-8e7d-3a56f8043f87)

![image](https://github.com/user-attachments/assets/1b2c60f4-cb75-405d-a2ba-0e200a48b299)

Heatmap:

![image](https://github.com/user-attachments/assets/08984176-1b8b-4326-ac68-8aeb3c9262b9)

![image](https://github.com/user-attachments/assets/f4297129-92d3-49ab-b993-ae70597a4891)

![image](https://github.com/user-attachments/assets/c0c8e9ca-7960-4cb0-bd36-b9601f0697db)


```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk cts
```

![image](https://github.com/user-attachments/assets/fbd2d4a2-248a-450f-bdcc-fd0ab0c9c2f4)

![image](https://github.com/user-attachments/assets/a17cd95d-cfb8-47f2-9e79-a2e71d0499d6)

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_cts
```

![image](https://github.com/user-attachments/assets/7a390b9d-90f1-406b-b397-254187828bfd)

![image](https://github.com/user-attachments/assets/b43cfb6a-f095-4c9f-adc2-b562b42142b4)

![image](https://github.com/user-attachments/assets/da5935db-358b-4edc-ade0-9823625ba062)

CTS final report:

![image](https://github.com/user-attachments/assets/d545c7f2-9514-4ee2-a76b-1fe5ee60c88e)


```

==========================================================================
cts final report_tns
--------------------------------------------------------------------------
tns 0.00

==========================================================================
cts final report_wns
--------------------------------------------------------------------------
wns 0.00

==========================================================================
cts final report_worst_slack
--------------------------------------------------------------------------
worst slack 5.55

==========================================================================
cts final report_clock_skew
--------------------------------------------------------------------------
Clock clk
   0.92 source latency core.CPU_result_a4[0]$_DFF_P_/CLK ^
  -0.82 target latency core.CPU_Dmem_value_a5[0][18]$_SDFFE_PP0P_/CLK ^
   0.55 clock uncertainty
   0.00 CRPR
--------------
   0.65 setup skew


==========================================================================
cts final report_checks -path_delay min
--------------------------------------------------------------------------
Startpoint: core.CPU_Xreg_value_a4[25][15]$_SDFFE_PP0P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_src2_value_a3[15]$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.10    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.00    0.00    0.00 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.23    0.24    0.26    0.26 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.24    0.00    0.26 ^ clkbuf_3_7_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     2    0.04    0.06    0.20    0.47 ^ clkbuf_3_7_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_3_7_0_CLK (net)
                  0.06    0.00    0.47 ^ clkbuf_4_14__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.17    0.18    0.24    0.71 ^ clkbuf_4_14__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_14__leaf_CLK (net)
                  0.18    0.00    0.71 ^ clkbuf_leaf_108_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    12    0.04    0.06    0.19    0.90 ^ clkbuf_leaf_108_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_108_CLK (net)
                  0.06    0.00    0.90 ^ core.CPU_Xreg_value_a4[25][15]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     2    0.01    0.06    0.32    1.22 ^ core.CPU_Xreg_value_a4[25][15]$_SDFFE_PP0P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_Xreg_value_a4[25][15] (net)
                  0.06    0.00    1.22 ^ _14708_/A1 (sky130_fd_sc_hd__a21oi_1)
     1    0.00    0.04    0.06    1.28 v _14708_/Y (sky130_fd_sc_hd__a21oi_1)
                                         _02012_ (net)
                  0.04    0.00    1.28 v _14712_/A (sky130_fd_sc_hd__nand4_1)
     1    0.01    0.13    0.12    1.40 ^ _14712_/Y (sky130_fd_sc_hd__nand4_1)
                                         _02016_ (net)
                  0.13    0.00    1.40 ^ _14729_/A1 (sky130_fd_sc_hd__o32ai_4)
     1    0.04    0.12    0.18    1.58 v _14729_/Y (sky130_fd_sc_hd__o32ai_4)
                                         _02033_ (net)
                  0.12    0.00    1.59 v _14731_/A2 (sky130_fd_sc_hd__o21ai_0)
     1    0.00    0.06    0.16    1.74 ^ _14731_/Y (sky130_fd_sc_hd__o21ai_0)
                                         core.CPU_src2_value_a2[15] (net)
                  0.06    0.00    1.74 ^ core.CPU_src2_value_a3[15]$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_2)
                                  1.74   data arrival time

                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.10    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.00    0.00    0.00 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.23    0.24    0.26    0.26 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.24    0.00    0.26 ^ clkbuf_3_6_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     2    0.04    0.06    0.21    0.47 ^ clkbuf_3_6_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_3_6_0_CLK (net)
                  0.06    0.00    0.47 ^ clkbuf_4_13__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    12    0.16    0.18    0.24    0.71 ^ clkbuf_4_13__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_13__leaf_CLK (net)
                  0.18    0.00    0.71 ^ clkbuf_leaf_70_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    12    0.04    0.06    0.18    0.89 ^ clkbuf_leaf_70_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_70_CLK (net)
                  0.06    0.00    0.89 ^ core.CPU_src2_value_a3[15]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_2)
                          0.88    1.78   clock uncertainty
                          0.00    1.78   clock reconvergence pessimism
                         -0.03    1.74   library hold time
                                  1.74   data required time
-----------------------------------------------------------------------------
                                  1.74   data required time
                                 -1.74   data arrival time
-----------------------------------------------------------------------------
                                  0.00   slack (MET)



==========================================================================
cts final report_checks -path_delay max
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_taken_br_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.10    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.00    0.00    0.00 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.23    0.24    0.26    0.26 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.24    0.00    0.26 ^ clkbuf_3_4_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     2    0.04    0.07    0.21    0.47 ^ clkbuf_3_4_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_3_4_0_CLK (net)
                  0.07    0.00    0.47 ^ clkbuf_4_8__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    11    0.15    0.16    0.23    0.70 ^ clkbuf_4_8__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8__leaf_CLK (net)
                  0.16    0.00    0.70 ^ clkbuf_leaf_149_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    15    0.04    0.06    0.18    0.88 ^ clkbuf_leaf_149_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_149_CLK (net)
                  0.06    0.00    0.88 ^ core.CPU_valid_taken_br_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.03    0.30    1.18 v core.CPU_valid_taken_br_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_taken_br_a5 (net)
                  0.03    0.00    1.18 v _07913_/A (sky130_fd_sc_hd__or4_4)
    19    0.22    0.35    0.83    2.01 v _07913_/X (sky130_fd_sc_hd__or4_4)
                                         _02930_ (net)
                  0.35    0.01    2.02 v _07915_/A (sky130_fd_sc_hd__clkinv_16)
    43    0.45    0.31    0.36    2.38 ^ _07915_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _02932_ (net)
                  0.31    0.02    2.39 ^ _09981_/C (sky130_fd_sc_hd__nor3_2)
     2    0.02    0.10    0.14    2.53 v _09981_/Y (sky130_fd_sc_hd__nor3_2)
                                         _04371_ (net)
                  0.10    0.00    2.53 v _09982_/B1 (sky130_fd_sc_hd__a21oi_4)
     6    0.10    0.70    0.57    3.10 ^ _09982_/Y (sky130_fd_sc_hd__a21oi_4)
                                         _04372_ (net)
                  0.70    0.00    3.10 ^ _09988_/A2 (sky130_fd_sc_hd__o21ai_4)
    16    0.12    0.33    0.38    3.47 v _09988_/Y (sky130_fd_sc_hd__o21ai_4)
                                         _04378_ (net)
                  0.33    0.00    3.48 v _13552_/A (sky130_fd_sc_hd__nor3_4)
    23    0.14    1.37    1.19    4.67 ^ _13552_/Y (sky130_fd_sc_hd__nor3_4)
                                         _07042_ (net)
                  1.37    0.00    4.67 ^ _13572_/B (sky130_fd_sc_hd__nand2_2)
     5    0.03    0.29    0.30    4.98 v _13572_/Y (sky130_fd_sc_hd__nand2_2)
                                         _07058_ (net)
                  0.29    0.00    4.98 v _13574_/B1 (sky130_fd_sc_hd__o221ai_1)
     1    0.00    0.20    0.24    5.22 ^ _13574_/Y (sky130_fd_sc_hd__o221ai_1)
                                         _01444_ (net)
                  0.20    0.00    5.22 ^ hold2174/A (sky130_fd_sc_hd__dlygate4sd3_1)
     1    0.00    0.05    0.57    5.79 ^ hold2174/X (sky130_fd_sc_hd__dlygate4sd3_1)
                                         net2283 (net)
                  0.05    0.00    5.79 ^ core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.79   data arrival time

                         11.05   11.05   clock clk (rise edge)
                          0.00   11.05   clock source latency
     1    0.10    0.00    0.00   11.05 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.00    0.00   11.05 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.23    0.24    0.26   11.31 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.24    0.00   11.31 ^ clkbuf_3_6_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     2    0.04    0.06    0.21   11.52 ^ clkbuf_3_6_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_3_6_0_CLK (net)
                  0.06    0.00   11.52 ^ clkbuf_4_13__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    12    0.16    0.18    0.24   11.76 ^ clkbuf_4_13__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_13__leaf_CLK (net)
                  0.18    0.00   11.76 ^ clkbuf_leaf_90_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    11    0.04    0.06    0.19   11.94 ^ clkbuf_leaf_90_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_90_CLK (net)
                  0.06    0.00   11.94 ^ core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.55   11.39   clock uncertainty
                          0.00   11.39   clock reconvergence pessimism
                         -0.05   11.34   library setup time
                                 11.34   data required time
-----------------------------------------------------------------------------
                                 11.34   data required time
                                 -5.79   data arrival time
-----------------------------------------------------------------------------
                                  5.55   slack (MET)



==========================================================================
cts final report_checks -unconstrained
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_taken_br_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.10    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.00    0.00    0.00 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.23    0.24    0.26    0.26 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.24    0.00    0.26 ^ clkbuf_3_4_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     2    0.04    0.07    0.21    0.47 ^ clkbuf_3_4_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_3_4_0_CLK (net)
                  0.07    0.00    0.47 ^ clkbuf_4_8__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    11    0.15    0.16    0.23    0.70 ^ clkbuf_4_8__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8__leaf_CLK (net)
                  0.16    0.00    0.70 ^ clkbuf_leaf_149_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    15    0.04    0.06    0.18    0.88 ^ clkbuf_leaf_149_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_149_CLK (net)
                  0.06    0.00    0.88 ^ core.CPU_valid_taken_br_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.03    0.30    1.18 v core.CPU_valid_taken_br_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_taken_br_a5 (net)
                  0.03    0.00    1.18 v _07913_/A (sky130_fd_sc_hd__or4_4)
    19    0.22    0.35    0.83    2.01 v _07913_/X (sky130_fd_sc_hd__or4_4)
                                         _02930_ (net)
                  0.35    0.01    2.02 v _07915_/A (sky130_fd_sc_hd__clkinv_16)
    43    0.45    0.31    0.36    2.38 ^ _07915_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _02932_ (net)
                  0.31    0.02    2.39 ^ _09981_/C (sky130_fd_sc_hd__nor3_2)
     2    0.02    0.10    0.14    2.53 v _09981_/Y (sky130_fd_sc_hd__nor3_2)
                                         _04371_ (net)
                  0.10    0.00    2.53 v _09982_/B1 (sky130_fd_sc_hd__a21oi_4)
     6    0.10    0.70    0.57    3.10 ^ _09982_/Y (sky130_fd_sc_hd__a21oi_4)
                                         _04372_ (net)
                  0.70    0.00    3.10 ^ _09988_/A2 (sky130_fd_sc_hd__o21ai_4)
    16    0.12    0.33    0.38    3.47 v _09988_/Y (sky130_fd_sc_hd__o21ai_4)
                                         _04378_ (net)
                  0.33    0.00    3.48 v _13552_/A (sky130_fd_sc_hd__nor3_4)
    23    0.14    1.37    1.19    4.67 ^ _13552_/Y (sky130_fd_sc_hd__nor3_4)
                                         _07042_ (net)
                  1.37    0.00    4.67 ^ _13572_/B (sky130_fd_sc_hd__nand2_2)
     5    0.03    0.29    0.30    4.98 v _13572_/Y (sky130_fd_sc_hd__nand2_2)
                                         _07058_ (net)
                  0.29    0.00    4.98 v _13574_/B1 (sky130_fd_sc_hd__o221ai_1)
     1    0.00    0.20    0.24    5.22 ^ _13574_/Y (sky130_fd_sc_hd__o221ai_1)
                                         _01444_ (net)
                  0.20    0.00    5.22 ^ hold2174/A (sky130_fd_sc_hd__dlygate4sd3_1)
     1    0.00    0.05    0.57    5.79 ^ hold2174/X (sky130_fd_sc_hd__dlygate4sd3_1)
                                         net2283 (net)
                  0.05    0.00    5.79 ^ core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.79   data arrival time

                         11.05   11.05   clock clk (rise edge)
                          0.00   11.05   clock source latency
     1    0.10    0.00    0.00   11.05 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.00    0.00   11.05 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.23    0.24    0.26   11.31 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.24    0.00   11.31 ^ clkbuf_3_6_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     2    0.04    0.06    0.21   11.52 ^ clkbuf_3_6_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_3_6_0_CLK (net)
                  0.06    0.00   11.52 ^ clkbuf_4_13__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    12    0.16    0.18    0.24   11.76 ^ clkbuf_4_13__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_13__leaf_CLK (net)
                  0.18    0.00   11.76 ^ clkbuf_leaf_90_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    11    0.04    0.06    0.19   11.94 ^ clkbuf_leaf_90_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_90_CLK (net)
                  0.06    0.00   11.94 ^ core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                         -0.55   11.39   clock uncertainty
                          0.00   11.39   clock reconvergence pessimism
                         -0.05   11.34   library setup time
                                 11.34   data required time
-----------------------------------------------------------------------------
                                 11.34   data required time
                                 -5.79   data arrival time
-----------------------------------------------------------------------------
                                  5.55   slack (MET)



==========================================================================
cts final report_check_types -max_slew -max_cap -max_fanout -violators
--------------------------------------------------------------------------
max capacitance

Pin                                    Limit     Cap   Slack
------------------------------------------------------------
_13743_/Y                               0.15    0.15   -0.00 (VIOLATED)
_13455_/Y                               0.15    0.15   -0.00 (VIOLATED)


==========================================================================
cts final max_slew_check_slack
--------------------------------------------------------------------------
0.02021305449306965

==========================================================================
cts final max_slew_check_limit
--------------------------------------------------------------------------
1.4951449632644653

==========================================================================
cts final max_slew_check_slack_limit
--------------------------------------------------------------------------
0.0135

==========================================================================
cts final max_fanout_check_slack
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
cts final max_fanout_check_limit
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
cts final max_capacitance_check_slack
--------------------------------------------------------------------------
-0.001024815021082759

==========================================================================
cts final max_capacitance_check_limit
--------------------------------------------------------------------------
0.1538189947605133

==========================================================================
cts final max_capacitance_check_slack_limit
--------------------------------------------------------------------------
-0.0067

==========================================================================
cts final max_slew_violation_count
--------------------------------------------------------------------------
max slew violation count 0

==========================================================================
cts final max_fanout_violation_count
--------------------------------------------------------------------------
max fanout violation count 0

==========================================================================
cts final max_cap_violation_count
--------------------------------------------------------------------------
max cap violation count 2

==========================================================================
cts final setup_violation_count
--------------------------------------------------------------------------
setup violation count 0

==========================================================================
cts final hold_violation_count
--------------------------------------------------------------------------
hold violation count 0

==========================================================================
cts final report_checks -path_delay max reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_taken_br_a5$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.26    0.26 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.21    0.47 ^ clkbuf_3_4_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.23    0.70 ^ clkbuf_4_8__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.18    0.88 ^ clkbuf_leaf_149_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.88 ^ core.CPU_valid_taken_br_a5$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.30    1.18 v core.CPU_valid_taken_br_a5$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
   0.83    2.01 v _07913_/X (sky130_fd_sc_hd__or4_4)
   0.36    2.38 ^ _07915_/Y (sky130_fd_sc_hd__clkinv_16)
   0.15    2.53 v _09981_/Y (sky130_fd_sc_hd__nor3_2)
   0.57    3.10 ^ _09982_/Y (sky130_fd_sc_hd__a21oi_4)
   0.38    3.47 v _09988_/Y (sky130_fd_sc_hd__o21ai_4)
   1.20    4.67 ^ _13552_/Y (sky130_fd_sc_hd__nor3_4)
   0.31    4.98 v _13572_/Y (sky130_fd_sc_hd__nand2_2)
   0.24    5.22 ^ _13574_/Y (sky130_fd_sc_hd__o221ai_1)
   0.57    5.79 ^ hold2174/X (sky130_fd_sc_hd__dlygate4sd3_1)
   0.00    5.79 ^ core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
           5.79   data arrival time

  11.05   11.05   clock clk (rise edge)
   0.00   11.05   clock source latency
   0.00   11.05 ^ pll/CLK (avsdpll)
   0.26   11.31 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.21   11.52 ^ clkbuf_3_6_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.24   11.76 ^ clkbuf_4_13__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.19   11.94 ^ clkbuf_leaf_90_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00   11.94 ^ core.CPU_Xreg_value_a4[7][13]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
  -0.55   11.39   clock uncertainty
   0.00   11.39   clock reconvergence pessimism
  -0.05   11.34   library setup time
          11.34   data required time
---------------------------------------------------------
          11.34   data required time
          -5.79   data arrival time
---------------------------------------------------------
           5.55   slack (MET)



==========================================================================
cts final report_checks -path_delay min reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_Xreg_value_a4[25][15]$_SDFFE_PP0P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_src2_value_a3[15]$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.26    0.26 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.21    0.47 ^ clkbuf_3_7_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.24    0.71 ^ clkbuf_4_14__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.19    0.90 ^ clkbuf_leaf_108_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.90 ^ core.CPU_Xreg_value_a4[25][15]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.32    1.22 ^ core.CPU_Xreg_value_a4[25][15]$_SDFFE_PP0P_/Q (sky130_fd_sc_hd__dfxtp_1)
   0.06    1.28 v _14708_/Y (sky130_fd_sc_hd__a21oi_1)
   0.12    1.40 ^ _14712_/Y (sky130_fd_sc_hd__nand4_1)
   0.18    1.58 v _14729_/Y (sky130_fd_sc_hd__o32ai_4)
   0.16    1.74 ^ _14731_/Y (sky130_fd_sc_hd__o21ai_0)
   0.00    1.74 ^ core.CPU_src2_value_a3[15]$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_2)
           1.74   data arrival time

   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.26    0.26 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.21    0.47 ^ clkbuf_3_6_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.24    0.71 ^ clkbuf_4_13__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.19    0.89 ^ clkbuf_leaf_70_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.89 ^ core.CPU_src2_value_a3[15]$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_2)
   0.88    1.78   clock uncertainty
   0.00    1.78   clock reconvergence pessimism
  -0.03    1.74   library hold time
           1.74   data required time
---------------------------------------------------------
           1.74   data required time
          -1.74   data arrival time
---------------------------------------------------------
           0.00   slack (MET)



==========================================================================
cts final critical path target clock latency max path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path target clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path source clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path delay
--------------------------------------------------------------------------
5.7921

==========================================================================
cts final critical path slack
--------------------------------------------------------------------------
5.5454

==========================================================================
cts final slack div critical path delay
--------------------------------------------------------------------------
95.740750

==========================================================================
cts final report_power
--------------------------------------------------------------------------
Group                  Internal  Switching    Leakage      Total
                          Power      Power      Power      Power (Watts)
----------------------------------------------------------------
Sequential             6.95e-03   9.72e-04   1.45e-08   7.92e-03  37.7%
Combinational          2.12e-03   4.52e-03   3.05e-08   6.64e-03  31.6%
Clock                  3.66e-03   2.76e-03   2.96e-09   6.42e-03  30.6%
Macro                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Pad                    0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
----------------------------------------------------------------
Total                  1.27e-02   8.25e-03   4.80e-08   2.10e-02 100.0%
                          60.7%      39.3%       0.0%
```

Route:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk route
```

![image](https://github.com/user-attachments/assets/6d3b1559-69e7-4a4d-889a-c213d037d6d4)

![image](https://github.com/user-attachments/assets/8f91a046-882d-40a3-8b8e-ebcb57f961fc)
