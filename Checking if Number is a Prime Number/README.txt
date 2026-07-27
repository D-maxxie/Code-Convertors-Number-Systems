# Prime Number Detector Using Function in Verilog HDL

## Overview

This project implements a **Prime Number Detector** in Verilog HDL using a **user-defined function**. The module accepts an **8-bit unsigned number** as input and determines whether the number is **prime** or **not prime**.

The design demonstrates the use of **automatic functions**, loops, conditional statements, and arithmetic operators in Verilog.

---

# Features

- 8-bit input number
- Function-based implementation
- Automatic function
- Uses loop to check divisibility
- Displays whether the number is prime
- Combinational logic
- Educational example for Verilog functions

---

# Module Description

## Module Name

```
prime
```

The module evaluates the input number and returns whether it is prime.

---

# Inputs and Outputs

## Input

| Signal | Width | Description |
|--------|------:|-------------|
| `number` | 8 bits | Input number (0–255) |

---

## Output

| Signal | Width | Description |
|--------|------:|-------------|
| `is_prime` | 1 bit | Prime status |

---

# Parameters

```verilog
parameter PRIME = 1'b1;
parameter Not_PRIME = 1'b0;
```

| Value | Meaning |
|-------|---------|
| `1` | Prime Number |
| `0` | Not Prime |

---

# Working Principle

Whenever the input changes, the module calls the function:

```verilog
check_prime(number)
```

The function checks whether the input has any divisor other than **1** and itself.

If a divisor is found,

```
Not Prime
```

Otherwise,

```
Prime
```

The function returns the result to:

```verilog
is_prime
```

---

# Function Description

```verilog
function automatic integer check_prime;
```

The function performs the following steps:

1. Initialize a divisor counter.
2. Iterate from `2` to `num/2 - 1`.
3. Check:

```verilog
num % i == 0
```

4. If divisible, increment the counter.
5. After the loop:
   - Counter = 0 → Prime
   - Counter > 0 → Not Prime

---

# Flow Diagram

```
           Start
              |
              |
        Read Input Number
              |
              |
        num = 2 to num/2
              |
      -------------------
      |                 |
 num%i==0 ?          No Divisor
      |                 |
 Count++                |
      |                 |
      -------Loop--------
              |
              |
      Count == 0 ?
       /          \
     Yes          No
     |             |
 Prime        Not Prime
```

---

# Example Operations

### Example 1

Input

```
number = 13
```

Divisors checked:

```
2
3
4
5
6
```

None divide 13.

Output

```
is_prime = 1
```

Console

```
13 is a prime number
```

---

### Example 2

Input

```
number = 20
```

Divisors checked

```
2
```

Since

```
20 % 2 = 0
```

Output

```
is_prime = 0
```

Console

```
20 is not a prime number
```

---

# Truth Table (Sample)

| Number | Prime | Output |
|---------:|:----:|:------:|
| 2 | Yes | 1 |
| 3 | Yes | 1 |
| 4 | No | 0 |
| 5 | Yes | 1 |
| 6 | No | 0 |
| 7 | Yes | 1 |
| 8 | No | 0 |
| 9 | No | 0 |
| 10 | No | 0 |
| 11 | Yes | 1 |
| 12 | No | 0 |
| 13 | Yes | 1 |

---

# Block Diagram

```
             +-------------------------+
number ----->|     Prime Detector      |
             |    (Function Based)     |
             +-------------------------+
                        |
                        |
                        v
                    is_prime
```

---

# Applications

## 1. Educational Projects

- Learning Verilog functions
- Loop implementation
- Arithmetic operators

---

## 2. FPGA Design

- Number property checker
- Mathematical processing
- Hardware demonstrations

---

## 3. Embedded Systems

- Data validation
- Numerical classification
- Control applications

---

# Advantages

- Demonstrates reusable Verilog functions
- Uses an automatic function for local variables
- Easy to understand and modify
- Suitable for simulation and learning

---

# Limitations

The current implementation has a few logical issues:

- **Incorrect handling of 0 and 1:** Both `0` and `1` are incorrectly reported as prime because the loop never executes and `count` remains zero.
- **Incorrect handling of 2:** The loop condition `i < num/2` means the loop does not execute for `num = 2`, which happens to return prime correctly, but only by coincidence.
- **Inefficient algorithm:** Checking divisibility up to `num/2` performs more iterations than necessary. Checking up to the square root of the number is sufficient.
- `$display` statements are for simulation only and are ignored during synthesis.
- The function is declared as `integer` even though it returns only a 1-bit logical value.

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

for better combinational coding style.

---

### 2. Handle Special Cases

```verilog
if (num < 2)
    check_prime = Not_PRIME;
else if (num == 2)
    check_prime = PRIME;
```

This correctly classifies `0`, `1`, and `2`.

---

### 3. Reduce Loop Iterations

Instead of

```verilog
for(i = 2; i < num/2; i = i + 1)
```

use

```verilog
for(i = 2; i*i <= num; i = i + 1)
```

This significantly improves efficiency.

---

### 4. Return a 1-Bit Value

Since only a logical result is needed, the function can be declared as:

```verilog
function automatic check_prime;
```

or in SystemVerilog:

```systemverilog
function automatic logic check_prime(input logic [7:0] num);
```

---

### 5. Move `$display` to the Testbench

Printing messages is a simulation task and should ideally be performed in the testbench rather than in synthesizable RTL.

---

# Project Files

```
prime.v
```

---

## Author

**Dileep Kumar Maddineni**