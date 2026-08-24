16-bit ALU using Verilog

A simple 16-bit Arithmetic Logic Unit (ALU) designed using Verilog HDL.
This project performs 16-bit addition and generates important arithmetic status flags.

Project Overview

The ALU takes two 16-bit inputs, "X" and "Y", and performs:

X + Y

The design produces a 16-bit result along with five status flags:

- Sign Flag (S)
- Zero Flag (ZR)
- Carry Flag (CY)
- Parity Flag (P)
- Overflow Flag (V)


Inputs and Outputs

Signal| Direction| Width| Description
"X"| Input| 16-bit| First operand
"Y"| Input| 16-bit| Second operand
"Z"| Output| 16-bit| Addition result
"Sign"| Output| 1-bit| Indicates sign of result
"Zero"| Output| 1-bit| Indicates whether result is zero
"Carry"| Output| 1-bit| Indicates carry from MSB
"Parity"| Output| 1-bit| Even parity of result
"Overflow"| Output| 1-bit| Indicates signed arithmetic overflow

 Flag Descriptions

1. Carry Flag

assign {Carry, Z} = X + Y;

The addition produces 17 bits. The extra MSB is stored in "Carry".

For example:

FFFF + 0001 = 1_0000
              ↑
            Carry

2. Sign Flag

assign Sign = Z[15];

The MSB of the result represents the sign in signed 2's-complement arithmetic.

- "Sign = 0" → Positive result
- "Sign = 1" → Negative result

3. Zero Flag

assign Zero = ~|Z;

This is a reduction NOR operation.

- "Zero = 1" → Result is "0000"
- "Zero = 0" → Result is non-zero

4. Parity Flag

assign Parity = ~^Z;

This calculates even parity.

- "Parity = 1" → Even number of 1s
- "Parity = 0" → Odd number of 1s

5. Overflow Flag

assign Overflow = (X[15] & Y[15] & ~Z[15]) |
                  (~X[15] & ~Y[15] & Z[15]);

Overflow occurs when two numbers having the same sign are added and the result has the opposite sign.

📂 Project Files

16-bit-ALU-Verilog/
│
├── alu.v
├── alutest.v
└── README.md

"alu.v"

Contains the main 16-bit ALU design.

"alutest.v"

Contains the testbench used to simulate and verify the ALU.

"README.md"

Project documentation.

 Test Cases

The testbench checks the ALU using three test cases:

Test| X| Y| Purpose
1| "8FFF"| "8000"| Tests signed overflow
2| "FFFE"| "0002"| Tests carry and zero result
3| "AAAA"| "5555"| Tests zero and parity

Expected Results

Test 1

X = 8FFF
Y = 8000
Z = 0FFF
CY = 1
V = 1

Two negative signed numbers produce a positive result, so signed overflow occurs.

Test 2

X = FFFE
Y = 0002
Z = 0000
CY = 1
ZR = 1

The result is zero and a carry is generated.

Test 3

X = AAAA
Y = 5555
Z = FFFF
CY = 0

The result is "FFFF".

 Simulation

This project can be simulated using Icarus Verilog and viewed using GTKWave.

Compile

iverilog -o alu_sim alu.v alutest.v

Run Simulation

vvp alu_sim

This generates:

alu.vcd

Open Waveform

gtkwave alu.vcd

The waveform can be used to observe:

- "X"
- "Y"
- "Z"
- "S"
- "ZR"
- "CY"
- "P"
- "V"

🛠️ Tools Used

- Verilog HDL
- Icarus Verilog
- GTKWave
- Git
- GitHub

🎯 Learning Objectives

This project demonstrates:

- 16-bit binary addition
- Verilog module design
- Testbench creation
- Reduction operators
- Carry generation
- Sign detection
- Zero detection
- Parity generation
- Signed overflow detection
- RTL simulation
- Waveform analysis
- GitHub project management

 Future Improvements

The ALU can be extended to support additional operations such as:

- Addition
- Subtraction
- AND
- OR
- XOR
- NOT
- Increment
- Decrement
- Shift operations
- Rotate operations

An operation-select input can also be added to create a complete multi-function ALU.


16-bit ALU using Verilog HDL

This project is developed as a digital design / VLSI learning project.
