# Factorial Calculator Using Recursive Function in Verilog HDL

## Overview

This project implements a **Factorial Calculator** in Verilog HDL using a **recursive user-defined function**. The module accepts a **4-bit unsigned input** and computes its factorial.

The factorial of a non-negative integer **n** is defined as:

```
n! = n × (n−1) × (n−2) × ... × 2 × 1
```

Special case:

```
0! = 1
```

The design demonstrates the use of **recursive functions**, **automatic functions**, and combinational logic in Verilog.

---

# Features

- 4-bit input number
- Recursive function implementation
- Automatic function
- Combinational logic
- Supports factorial calculation from 0 to 15
- Easy to understand and modify

---

# Module Description

## Module Name

```
factorial
```

The module computes the factorial of the input number using recursion and outputs the result as a 32-bit value.

---

# Inputs and Outputs

## Input

| Signal | Width | Description |
|--------|------:|-------------|
| `n` | 4 bits | Input number |

---

## Output

| Signal | Width | Description |
|--------|------:|-------------|
| `result` | 32 bits | Factorial of the input |

---

# Function Description

```verilog
function automatic integer fact(input integer i);
```

The recursive function works as follows:

1. If `i > 1`
   - Return:

```verilog
i * fact(i - 1)
```

2. Otherwise

```verilog
return 1;
```

Thus,

```
5!

↓

5 × 4!

↓

5 × 4 × 3!

↓

5 × 4 × 3 × 2!

↓

5 × 4 × 3 × 2 × 1

↓

120
```

---

# Working Principle

Whenever the input `n` changes,

```verilog
always @(n)
```

the module executes

```verilog
result = fact(n);
```

The recursive function repeatedly calls itself until it reaches the base case:

```
i <= 1
```

Then it returns upward through the recursion, multiplying each value.

---

# Flow Diagram

```
             Start
               |
               |
          Read Input n
               |
               |
          fact(n)
               |
        ----------------
        |              |
      i > 1 ?         No
        |              |
       Yes          Return 1
        |
 Return i × fact(i−1)
        |
     Recursive Call
        |
        |
     Return Result
```

---

# Example Operations

### Example 1

Input

```
n = 4
```

Recursive evaluation

```
4!

↓

4 × 3!

↓

4 × 3 × 2!

↓

4 × 3 × 2 × 1

↓

24
```

Output

```
result = 24
```

---

### Example 2

Input

```
n = 5
```

Calculation

```
5 × 4 × 3 × 2 × 1

= 120
```

Output

```
result = 120
```

---

### Example 3

Input

```
n = 0
```

Base case

```
0! = 1
```

Output

```
result = 1
```

---

# Sample Results

| Input (n) | Factorial |
|-----------:|----------:|
| 0 | 1 |
| 1 | 1 |
| 2 | 2 |
| 3 | 6 |
| 4 | 24 |
| 5 | 120 |
| 6 | 720 |
| 7 | 5040 |
| 8 | 40320 |
| 9 | 362880 |
| 10 | 3628800 |

---

# Block Diagram

```
          +---------------------------+
n -------->|   Recursive Factorial    |
           |       Function           |
           +---------------------------+
                        |
                        |
                        v
                    result
```

---

# Applications

## 1. Educational Projects

- Learning recursive functions in Verilog
- Understanding recursion
- Function-based design

---

## 2. FPGA Design

- Demonstrating recursive algorithms (primarily for simulation)
- Arithmetic computation examples
- Mathematical processing

---

## 3. Embedded Systems

- Numeric computations
- Educational processors
- Algorithm demonstrations

---

# Advantages

- Demonstrates recursive functions in Verilog
- Compact and easy-to-read implementation
- Uses an automatic function with local variables
- Good example for learning recursion

---

# Limitations

- **Not synthesizable on many FPGA/ASIC tools:** Recursive functions are generally intended for simulation and are often unsupported for hardware synthesis.
- **Output overflow:** Although the input is 4 bits (0–15), a 32-bit output can only represent factorials up to **12!** correctly.
  - `12! = 479001600` (fits in 32 bits)
  - `13! = 6227020800` (overflows 32 bits)
- The function returns an `integer`, which is typically a 32-bit signed value, limiting the maximum correct result.

---

# Coding Improvements

### 1. Use `always @(*)`

Replace

```verilog
always @(n)
```

with

```verilog
always @(*)
```

for proper combinational coding style.

---

### 2. Prevent Overflow

Limit the input range:

```verilog
if (n > 12)
    result = 32'd0;
else
    result = fact(n);
```

or use a wider output bus if larger factorials are required.

---

### 3. Consider an Iterative Implementation

For synthesizable hardware, replace recursion with a bounded `for` loop inside a combinational or sequential process.

---

### 4. Use SystemVerilog Types (Optional)

In SystemVerilog:

```systemverilog
function automatic int fact(input int i);
```

or use `longint` if larger values are needed.

---

# Project Files

```
factorial.v
```

---

## Author

**Dileep Kumar Maddineni**