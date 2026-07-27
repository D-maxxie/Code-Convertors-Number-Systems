# Armstrong Number Detector Using Function in Verilog HDL

## Overview

This project implements an **Armstrong Number Detector** in Verilog HDL using a **user-defined function**. The module accepts a **9-bit unsigned decimal number** as input and determines whether the number is an **Armstrong number**.

An **Armstrong number** (also called a **Narcissistic number**) is a number that is equal to the sum of the cubes of its digits (for 3-digit numbers).

Examples:

- 153 = 1³ + 5³ + 3³
- 370 = 3³ + 7³ + 0³
- 371 = 3³ + 7³ + 1³
- 407 = 4³ + 0³ + 7³

---

# Features

- 9-bit input number
- Function-based implementation
- Uses a `while` loop
- Extracts decimal digits
- Calculates the sum of digit cubes
- Detects Armstrong numbers
- Displays simulation messages
- Combinational logic

---

# Module Description

## Module Name

```
armstrong
```

The module checks whether the input number is equal to the sum of the cubes of its decimal digits.

---

# Inputs and Outputs

## Input

| Signal | Width | Description |
|--------|------:|-------------|
| `number` | 9 bits | Input decimal number (0–511) |

---

## Output

| Signal | Width | Description |
|--------|------:|-------------|
| `is_armstrong` | 1 bit | Indicates whether the number is an Armstrong number |

---

# Parameters

```verilog
parameter ARMSTRONG = 1'b1;
parameter Not_ARMSTRONG = 1'b0;
```

| Value | Meaning |
|-------|---------|
| `1` | Armstrong Number |
| `0` | Not Armstrong Number |

---

# Working Principle

Whenever the input changes, the module calls the function:

```verilog
check_armstrong(number)
```

The function performs the following operations:

1. Copy the input number to a temporary variable.
2. Extract the last decimal digit using the modulus operator (`% 10`).
3. Compute the cube of the extracted digit.
4. Add the cube to an accumulated sum.
5. Remove the last digit using integer division (`/ 10`).
6. Repeat until all digits are processed.
7. Compare the accumulated sum with the original number.
8. If they are equal, the number is an Armstrong number.

---

# Function Description

```verilog
function check_armstrong;
```

Internal variables:

```verilog
temp_num
remainder
result
```

Algorithm:

```
Extract each digit

↓

Cube the digit

↓

Add to result

↓

Repeat for all digits

↓

Compare with original number
```

---

# Flow Diagram

```
             Start
               |
               |
      Read Input Number
               |
               |
      temp_num = number
      result = 0
               |
               |
      temp_num != 0 ?
          /          \
        Yes          No
         |
 remainder = temp_num % 10
 result = result + remainder³
 temp_num = temp_num / 10
         |
         |
      Repeat Loop
         |
         |
 result == number ?
      /           \
    Yes           No
    |              |
Armstrong     Not Armstrong
```

---

# Example Operations

### Example 1

Input

```
number = 153
```

Calculation

```
1³ + 5³ + 3³

= 1 + 125 + 27

= 153
```

Output

```
is_armstrong = 1
```

Console

```
153 is a armstrong number
```

---

### Example 2

Input

```
number = 371
```

Calculation

```
3³ + 7³ + 1³

= 27 + 343 + 1

= 371
```

Output

```
is_armstrong = 1
```

---

### Example 3

Input

```
number = 250
```

Calculation

```
2³ + 5³ + 0³

= 8 + 125 + 0

= 133
```

Since

```
133 ≠ 250
```

Output

```
is_armstrong = 0
```

Console

```
250 is not a armstrong number
```

---

# Sample Results

| Number | Sum of Cubes | Output |
|--------:|-------------:|:------:|
| 0 | 0 | 1 |
| 1 | 1 | 1 |
| 153 | 153 | 1 |
| 370 | 370 | 1 |
| 371 | 371 | 1 |
| 407 | 407 | 1 |
| 123 | 36 | 0 |
| 250 | 133 | 0 |
| 500 | 125 | 0 |

---

# Block Diagram

```
             +------------------------------+
number ----->|  Armstrong Number Detector   |
             |     (Function Based)         |
             +------------------------------+
                          |
                          |
                          v
                    is_armstrong
```

---

# Applications

## 1. Digital Systems

- Number classification
- Mathematical computation
- Educational demonstrations

---

## 2. FPGA Projects

- Arithmetic algorithm implementation
- Function-based hardware design
- Number property verification

---

## 3. Embedded Systems

- Numeric analysis
- Data validation
- Educational processors

---

# Advantages

- Demonstrates Verilog functions
- Uses arithmetic operators and loops
- Simple combinational implementation
- Easy to understand and modify

---

# Limitations

- This implementation correctly identifies **3-digit Armstrong numbers**, but it is **not a general Armstrong number detector**. A true Armstrong number requires raising each digit to the power of the **number of digits**, not always to the third power.
- The use of decimal division (`/10`) and modulus (`%10`) results in relatively expensive hardware.
- The `while` loop has a variable number of iterations, which may not be supported efficiently by all synthesis tools.
- `$display` statements are for simulation only and are ignored during synthesis.

---

# Coding Improvements

### 1. Use `always @(*)`

Replace

```verilog
always @(number)
```

with

```verilog
always @(*)
```

for proper combinational logic.

---

### 2. Use an Automatic Function

Declare the function as:

```verilog
function automatic check_armstrong;
```

or in SystemVerilog:

```systemverilog
function automatic logic check_armstrong(input logic [8:0] num);
```

to ensure local variables are re-entrant.

---

### 3. Improve Console Messages

For grammatically correct output, replace:

```verilog
"%d is a armstrong number"
```

with

```verilog
"%d is an Armstrong number"
```

and

```verilog
"%d is not an Armstrong number"
```

---

### 4. Move `$display` to the Testbench

Simulation messages should be placed in the testbench, keeping the RTL clean and synthesizable.

---

### 5. Generalize the Algorithm

To detect Armstrong numbers with any number of digits, first determine the digit count, then raise each digit to that power instead of always cubing it.

---

# Project Files

```
armstrong.v
```

---

## Author

**Dileep Kumar Maddineni**