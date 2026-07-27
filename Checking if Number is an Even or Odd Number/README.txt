# Even or Odd Number Detector Using Function in Verilog HDL

## Overview

This project implements an **Even or Odd Number Detector** in Verilog HDL using a **user-defined function**. The circuit accepts a **4-bit binary number** as input and determines whether the number is **even** or **odd**.

The design demonstrates the use of **functions** in Verilog to perform reusable combinational logic.

---

# Features

- 4-bit input number
- Function-based implementation
- Combinational logic
- Displays whether the number is even or odd
- Synthesizable RTL (excluding `$display` statements)
- Simple and reusable design

---

# Module Description

## Module Name

```
even_or_odd
```

The module evaluates the input number and sets the output signal according to its parity.

---

# Inputs and Outputs

## Input

| Signal | Width | Description |
|--------|------:|-------------|
| `number` | 4 bits | Binary input number |

---

## Output

| Signal | Width | Description |
|--------|------:|-------------|
| `even_odd` | 1 bit | Indicates whether the number is even or odd |

---

# Parameters

```verilog
parameter EVEN = 1'b1;
parameter ODD  = 1'b0;
```

| Value | Meaning |
|-------|---------|
| `1` | Even Number |
| `0` | Odd Number |

---

# Working Principle

Whenever the input number changes, the module calls the function:

```verilog
check_even_odd(number)
```

The function checks:

```verilog
num % 2
```

If the remainder is zero,

```
Even
```

Otherwise,

```
Odd
```

The returned value is assigned to:

```verilog
even_odd
```

---

# Function Description

```verilog
function check_even_odd;
```

Input:

```verilog
num
```

Operation:

```verilog
if(num % 2 == 0)
```

Return:

```
EVEN
```

Else:

```
ODD
```

---

# Truth Table

| Decimal | Binary | Output | Result |
|---------:|:------:|:------:|--------|
| 0 | 0000 | 1 | Even |
| 1 | 0001 | 0 | Odd |
| 2 | 0010 | 1 | Even |
| 3 | 0011 | 0 | Odd |
| 4 | 0100 | 1 | Even |
| 5 | 0101 | 0 | Odd |
| 6 | 0110 | 1 | Even |
| 7 | 0111 | 0 | Odd |
| 8 | 1000 | 1 | Even |
| 9 | 1001 | 0 | Odd |
| 10 | 1010 | 1 | Even |
| 11 | 1011 | 0 | Odd |
| 12 | 1100 | 1 | Even |
| 13 | 1101 | 0 | Odd |
| 14 | 1110 | 1 | Even |
| 15 | 1111 | 0 | Odd |

---

# Example Operation

### Example 1

Input:

```
number = 4'b0110
```

Decimal:

```
6
```

Output:

```
even_odd = 1
```

Console:

```
6 is an even number
```

---

### Example 2

Input:

```
number = 4'b1011
```

Decimal:

```
11
```

Output:

```
even_odd = 0
```

Console:

```
11 is an odd number
```

---

# Block Diagram

```
             +---------------------------+
number ----->|                           |
             | Even/Odd Detector         |
             | (Function Based)          |
             +---------------------------+
                         |
                         |
                         v
                    even_odd
```

---

# Simulation Output

Example console messages:

```
6 is an even number

11 is an odd number

14 is an even number

5 is an odd number
```

---

# Applications

## 1. Digital Systems

- Number classification
- Control logic
- Arithmetic preprocessing

---

## 2. Embedded Systems

- Input validation
- Decision-making circuits
- Data filtering

---

## 3. FPGA and ASIC Designs

- Educational function examples
- Combinational logic modules
- Reusable utility blocks

---

# Advantages

- Demonstrates the use of Verilog functions
- Simple and readable implementation
- Fully combinational logic
- Easy to integrate into larger designs

---

# Limitations

- The `%` (modulus) operator is more hardware-intensive than necessary for checking parity.
- `$display` statements are for simulation only and are ignored during synthesis.

---

# Coding Improvements

### 1. Use `always @(*)`

Replace:

```verilog
always @(number)
```

with:

```verilog
always @(*)
```

for a more robust combinational block.

---

### 2. Simplify the Even/Odd Check

Since a binary number is even when its least significant bit (LSB) is `0`, the function can avoid the modulus operator:

```verilog
function check_even_odd;
    input [3:0] num;
    begin
        check_even_odd = ~num[0];
    end
endfunction
```

This produces simpler hardware.

---

### 3. Modern Function Declaration (Verilog-2001)

For improved readability:

```verilog
function check_even_odd;
    input [3:0] num;
    begin
        check_even_odd = ~num[0];
    end
endfunction
```

or in SystemVerilog:

```systemverilog
function automatic logic check_even_odd(input logic [3:0] num);
    check_even_odd = ~num[0];
endfunction
```

---

### 4. Separate Simulation Messages

Keep `$display` statements in the testbench instead of the synthesizable design module. This keeps the RTL clean and portable.

---

# Project Files

```
even_or_odd.v
```

---

## Author

**Dileep Kumar Maddineni**