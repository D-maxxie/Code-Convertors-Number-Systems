# 8-Bit Binary to BCD Converter in Verilog

## Overview

This project implements an **8-bit Binary to Binary-Coded Decimal (BCD) Converter** using Verilog HDL. The module converts an 8-bit binary input value into its equivalent BCD representation.

BCD encoding represents each decimal digit of a number separately using 4-bit binary values. This design uses the **Double Dabble (Shift-Add-3) Algorithm**, which is a commonly used hardware-efficient method for converting binary numbers into BCD format.

The implementation is designed as a **combinational circuit** using behavioral modeling and can be synthesized for FPGA and ASIC applications.

## Features

- Converts 8-bit binary input into BCD format
- Implements the Double Dabble (Shift-Add-3) algorithm
- Supports binary values from 0 to 255
- Generates three BCD digits (hundreds, tens, and ones)
- Pure combinational logic design
- Fully synthesizable for FPGA and ASIC implementations

## Module Description

### Binary to BCD Converter (`binary2bcd`)

The module accepts an 8-bit binary input and converts it into a 12-bit BCD output.

The output consists of three 4-bit BCD digits:

```
BCD = Hundreds | Tens | Ones
```

Example:

```
Binary Input : 11111111 (255)

BCD Output:
0010 0101 0101

Hundreds = 2
Tens     = 5
Ones     = 5
```

## Inputs and Outputs

### Input

| Signal | Width | Description |
|--------|------:|-------------|
| `data` | 8 bits | Binary input value (0-255) |

### Outputs

| Signal | Width | Description |
|--------|------:|-------------|
| `bit2` | 4 bits | Hundreds digit in BCD |
| `bit1` | 4 bits | Tens digit in BCD |
| `bit0` | 4 bits | Ones digit in BCD |
| `BCD` | 12 bits | Combined BCD output |

## Conversion Algorithm

The converter uses the **Double Dabble Algorithm**, which works by shifting each binary bit into the BCD digits while adding 3 whenever a BCD digit becomes greater than 4.

### Algorithm Steps

1. Initialize all BCD digits to zero.
2. Process each binary input bit from MSB to LSB.
3. Before shifting:
   - Check each BCD digit.
   - If the digit value is greater than 4, add 3.
4. Shift the complete BCD register left.
5. Repeat until all input bits are processed.
6. Store the final BCD result.

## Implementation

The BCD adjustment operation is performed using:

```verilog
if(bit0 > 4)
    bit0 = bit0 + 3;

if(bit1 > 4)
    bit1 = bit1 + 3;

if(bit2 > 4)
    bit2 = bit2 + 3;
```

The shifting operation:

```verilog
{bit2, bit1, bit0} = {bit2, bit1, bit0, data[7-n]};
```

After all 8 bits are processed, the final BCD output is generated:

```verilog
BCD = {bit2, bit1, bit0};
```

## Example Conversion

### Example 1

Binary Input:

```
data = 8'b00011001
```

Decimal Value:

```
25
```

BCD Output:

```
0000 0010 0101
```

Representation:

```
Hundreds = 0
Tens     = 2
Ones     = 5
```

---

### Example 2

Binary Input:

```
data = 8'b11111111
```

Decimal Value:

```
255
```

BCD Output:

```
0010 0101 0101
```

Representation:

```
Hundreds = 2
Tens     = 5
Ones     = 5
```

## Project File

```
binary2bcd.v
```

## Input Range

| Binary Input | Decimal Value | BCD Output |
|:------------:|---------------:|:----------:|
| 00000000 | 0 | 0000 0000 0000 |
| 00001010 | 10 | 0000 0001 0000 |
| 01100100 | 100 | 0001 0000 0000 |
| 11111111 | 255 | 0010 0101 0101 |

## Requirements

- Verilog HDL
- Any Verilog simulator such as:
  - Xilinx Vivado
  - ModelSim
  - Icarus Verilog

## Applications

- Digital display systems
- Seven-segment display drivers
- Embedded systems
- Calculator circuits
- Digital measurement instruments
- FPGA-based arithmetic systems

## Advantages

- Efficient hardware implementation
- Avoids complex division and modulo operations
- Suitable for real-time binary-to-decimal conversion
- Scalable for larger input widths

## Future Improvements

- Create a parameterized binary-to-BCD converter supporting different bit widths.
- Add support for larger binary values.
- Implement a pipelined version for high-speed applications.
- Add a verification testbench covering all input combinations.
- Compare synthesis results with arithmetic-based conversion methods.

## Author

**Dileep Kumar Maddineni**