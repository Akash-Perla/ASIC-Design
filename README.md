# ASIC-Design

# Task-1

We first create a new file named `sum1ton.c` which prints the sum of all numbers upto 'n'.

![image](https://github.com/user-attachments/assets/c27a1b39-7817-43a6-9f4b-570350ef50e6)

The following is the C code for the same

![image](https://github.com/user-attachments/assets/96ceaa26-146c-41e3-867d-60923823f02b)

The code is compiled using the GCC compiler, producing an output file named a.out. Below is the output of the program

![image](https://github.com/user-attachments/assets/15a83abf-13fb-4822-ac38-754fba4dff68)

# Task-2

Now, the parameter 'n' in `sum1ton.c` is changed from 5 to 100

![image](https://github.com/user-attachments/assets/cf321036-15cc-422c-84a3-c039fbb1798a)

Now, we compile the C program using RISC - V compiler using O1 optimization

![image](https://github.com/user-attachments/assets/fa20235e-a636-4ae1-9e7e-03d58c1f8d85)

Now, we create the object file `sum1ton.o`

![image](https://github.com/user-attachments/assets/08c9d699-5237-4020-808b-5d19ccd24250)

As soon as we press the Enter Key, a huge list opcodes are displayed on terminal. But our focus is on the main section of the program. Type :/main to hover to that portion.

v![image](https://github.com/user-attachments/assets/e72e313c-bb12-4928-b743-0de1567e74ad)

For the "main" section, we can determine the number of instructions by subtracting the address of the first instruction in the next section from the address of the first instruction in the main section, then dividing the difference by 4 (since each instruction is 4 bytes)

![image](https://github.com/user-attachments/assets/1913fb35-806c-475e-9737-1d890058ada2)
![image](https://github.com/user-attachments/assets/74d36fdc-4051-462c-bb76-830c059ed420)

The total number of instructions are 15

Now, we compile the C program using RISC - V compiler using Ofast optimization

![image](https://github.com/user-attachments/assets/3de390ef-3f7d-4a14-99ad-56ce6a19216d)

Now, we create the object file `sum1ton.o`

![image](https://github.com/user-attachments/assets/08c9d699-5237-4020-808b-5d19ccd24250)

As soon as we press the Enter Key, a huge list opcodes are displayed on terminal. But our focus is on the main section of the program. Type :/main to hover to that portion.

![image](https://github.com/user-attachments/assets/95410174-0e12-47f4-a6bd-a3060ada6416)

For the "main" section, we can determine the number of instructions by subtracting the address of the first instruction in the next section from the address of the first instruction in the main section, then dividing the difference by 4 (since each instruction is 4 bytes)






