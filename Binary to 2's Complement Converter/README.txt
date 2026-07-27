# 4-Bit Two's Complement Generator in Verilog

## Overview

This project implements a **4-bit Two's Complement Converter** using Verilog HDL. The module converts a given 4-bit binary input into its corresponding **two's complement representation**.

Two's complement is the most commonly used method for representing signed binary numbers in digital systems. It allows both positive and negative numbers to be represented using the same binary arithmetic hardware.

The design generates the two's complement value by first calculating the **one's complement** (bit inversion) and then adding `1` to obtain the final result.

## Features

- Generates 4-bit two's complement output
- Implements the standard two's complement conversion method
- Uses combinational logic design
- No clock or sequential elements required
- Supports signed output representation
- Fully synthesizable for FPGA and ASIC implementations

## Module Description

### Two's Complement Module (`complement_2s`)

The module accepts a 4-bit binary input and produces its corresponding 4-bit two's complement value.

The conversion process:

```
Two's Complement = (One's Complement) + 1
```

For a 4-bit input:

```
One's Complement = 4'b1111 - data

Two's Complement = One's Complement + 1
```

## Inputs and Output

### Input

| Signal | Width | Description |
|--------|------:|-------------|
| `data` | 4 bits | Input binary value |

### Output

| Signal | Width | Description |
|--------|------:|-------------|
| `out` | 4 bits | Two's complement output |

## How It Works

The module first generates the one's complement of the input:

```verilog
assign temp = 4'b1111 - data;
```

Since subtracting a value from all ones produces the inverted bits:

Example:

```
data = 0101

1111
-0101
----
1010
```

Then `1` is added to generate the two's complement:

```verilog
assign out = temp + 4'b0001;
```

Final result:

```
1010 + 0001 = 1011
```

Therefore:

```
Two's Complement of 0101 = 1011
```

## Conversion Example

Example 1:

```
Input:
data = 0011 (+3)

One's Complement:
1100

Add 1:
1100 + 0001 = 1101

Output:
1101 (-3)
```

Example 2:

```
Input:
data = 0100 (+4)

Output:
1100 (-4)
```

## Truth Table

| Input (`data`) | Two's Complement (`out`) |
|:--------------:|:------------------------:|
| 0000 | 0000 |
| 0001 | 1111 |
| 0010 | 1110 |
| 0011 | 1101 |
| 0100 | 1100 |
| 0101 | 1011 |
| 0110 | 1010 |
| 0111 | 1001 |
| 1000 | 1000 |
| 1001 | 0111 |
| 1010 | 0110 |
| 1011 | 0101 |
| 1100 | 0100 |
| 1101 | 0011 |
| 1110 | 0010 |
| 1111 | 0001 |

## Project File

```
complement_2s.v
```

## Requirements

- Verilog HDL
- Any Verilog simulator such as:
  - Xilinx Vivado
  - ModelSim
  - Icarus Verilog

## Applications

- Signed arithmetic circuits
- Arithmetic Logic Units (ALU)
- Digital processors
- Microcontroller and CPU arithmetic operations
- FPGA-based mathematical operations
- Binary subtraction circuits

## Future Improvements

- Extend the design for parameterized N-bit two's complement conversion.
- Add signed input support.
- Implement using only basic logic gates.
- Add a testbench for automatic verification of all input combinations.
- Compare different implementation methods for area and timing optimization.

## Author

**Dileep Kumar Maddineni**