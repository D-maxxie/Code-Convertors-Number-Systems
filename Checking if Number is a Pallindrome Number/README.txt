# Palindrome Number Detector Using Function in Verilog HDL

## Overview

This project implements a **Palindrome Number Detector** in Verilog HDL using a **user-defined function**. The module accepts a **16-bit unsigned decimal number** as input and determines whether the number is a **palindrome**.

A palindrome number reads the same forward and backward. Examples include **121**, **1331**, and **12321**.

The design demonstrates the use of **functions**, **while loops**, **division**, and **modulus operators** in Verilog.

---

# Features

- 16-bit input number
- Function-based implementation
- Uses a `while` loop
- Reverses the decimal digits
- Detects palindrome numbers
- Displays simulation messages
- Combinational logic

---

# Module Description

## Module Name

```
Palindrome
```

The module reverses the decimal digits of the input number and compares the reversed value with the original number.

---

# Inputs and Outputs

## Input

| Signal | Width | Description |
|--------|------:|-------------|
| `number` | 16 bits | Input decimal number |

---

## Output

| Signal | Width | Description |
|--------|------:|-------------|
| `is_palindrome` | 1 bit | Indicates whether the number is a palindrome |

---

# Parameters

```verilog
parameter PALINDROME = 1'b1;
parameter Not_PALINDROME = 1'b0;
```

| Value | Meaning |
|-------|---------|
| `1` | Palindrome |
| `0` | Not Palindrome |

---

# Working Principle

Whenever the input changes, the module calls the function:

```verilog
check_palindrome(number)
```

The function performs the following steps:

1. Store the original number.
2. Extract the last decimal digit using the modulus operator (`% 10`).
3. Append the extracted digit to a reversed number.
4. Remove the last digit using integer division (`/ 10`).
5. Repeat until the temporary number becomes zero.
6. Compare the reversed number with the original number.
7. If both are equal, the number is a palindrome.

---

# Function Description

```verilog
function check_palindrome;
```

Internal variables:

```verilog
lastDigit
reverseNum
temp_num
```

Algorithm:

```
Reverse decimal digits

↓

Compare with original number

↓

Return PALINDROME or Not_PALINDROME
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
      reverse = 0
              |
              |
     temp_num > 0 ?
          /       \
        Yes        No
         |          |
 last = temp_num%10 |
 reverse=reverse*10+last
 temp_num=temp_num/10
         |
         |
       Repeat
         |
         |
 reverse == number ?
      /           \
    Yes           No
    |              |
Palindrome    Not Palindrome
```

---

# Example Operations

### Example 1

Input

```
number = 121
```

Reversal process

```
121 → 12 → 1 → 0

Reverse

1

12

121
```

Output

```
is_palindrome = 1
```

Console

```
121 is a palindrome number
```

---

### Example 2

Input

```
number = 1234
```

Reverse

```
4321
```

Since

```
1234 ≠ 4321
```

Output

```
is_palindrome = 0
```

Console

```
1234 is not a palindrome number
```

---

### Example 3

Input

```
number = 1331
```

Reverse

```
1331
```

Output

```
is_palindrome = 1
```

---

# Sample Results

| Number | Reverse | Output |
|--------:|--------:|:------:|
| 121 | 121 | 1 |
| 1331 | 1331 | 1 |
| 12321 | 12321 | 1 |
| 1221 | 1221 | 1 |
| 1234 | 4321 | 0 |
| 45654 | 45654 | 1 |
| 78987 | 78987 | 1 |
| 5678 | 8765 | 0 |

---

# Block Diagram

```
             +-----------------------------+
number ----->|   Palindrome Detector       |
             |   (Function Based)          |
             +-----------------------------+
                           |
                           |
                           v
                    is_palindrome
```

---

# Applications

## 1. Digital Systems

- Number classification
- Mathematical processing
- Educational demonstrations

---

## 2. FPGA Projects

- Arithmetic function examples
- Number property detection
- Hardware algorithm demonstrations

---

## 3. Embedded Systems

- Numeric validation
- Data processing
- Educational processors

---

# Advantages

- Demonstrates Verilog functions
- Uses `while` loop and arithmetic operators
- Simple combinational implementation
- Easy to understand and modify

---

# Limitations

- The algorithm performs **decimal arithmetic** (`/10` and `%10`), which synthesizes into relatively expensive hardware.
- `$display` statements are for simulation only and are ignored during synthesis.
- The `while` loop has a variable number of iterations, which many synthesis tools either do not support or optimize poorly.
- The design checks **decimal palindromes**, not binary palindromes.

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

### 2. Correct the Display Message

Replace

```verilog
"%d is not a palindrome odd number"
```

with

```verilog
"%d is not a palindrome number"
```

to remove the unintended word **"odd"**.

---

### 3. Use an Automatic Function

For safer local variable handling:

```verilog
function automatic check_palindrome;
```

or in SystemVerilog:

```systemverilog
function automatic logic check_palindrome(input logic [15:0] num);
```

---

### 4. Move `$display` to the Testbench

Simulation messages are better placed in the testbench, keeping the RTL synthesizable and reusable.

---

### 5. Consider Fixed-Iteration Logic

If synthesis is required, replace the variable-iteration `while` loop with a bounded implementation or another hardware-friendly algorithm.

---

# Project Files

```
Palindrome.v
```

---

## Author

**Dileep Kumar Maddineni**