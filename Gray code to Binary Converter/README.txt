# 4-Bit Gray Code to Binary Converter in Verilog

## Overview

This project implements a **4-bit Gray Code to Binary Converter** using Verilog HDL. The purpose of this circuit is to convert a 4-bit Gray code input into its equivalent binary representation.

Gray code is commonly used in digital systems where reducing transition errors is important because only one bit changes between consecutive values. This converter is useful for converting Gray-coded data back into standard binary format for processing and computation.

The design is implemented using **gate-level modeling** with basic logic gates such as **Buffer** and **XOR gates**.

## Features

- Converts 4-bit Gray code input into 4-bit binary output
- Uses gate-level Verilog modeling
- Implements conversion using XOR logic
- Pure combinational circuit design
- No clock or sequential elements required
- Fully synthesizable for FPGA and ASIC implementations

## Module Description

### Gray to Binary Converter (`gray2binary`)

The module accepts a 4-bit Gray code input and generates the corresponding 4-bit binary output.

The conversion follows the Gray-to-Binary conversion rule:

```
Binary[3] = Gray[3]

Binary[2] = Gray[2] XOR Binary[3]

Binary[1] = Gray[1] XOR Binary[2]

Binary[0] = Gray[0] XOR Binary[1]
```

Each binary bit is obtained by XORing the current Gray code bit with the previously calculated binary bit.

## Inputs and Output

### Input

| Signal | Width | Description |
|--------|------:|-------------|
| `gray_in` | 4 bits | 4-bit Gray code input |

### Output

| Signal | Width | Description |
|--------|------:|-------------|
| `binary_out` | 4 bits | Corresponding binary output |

## How It Works

The most significant bit of the binary output is directly copied from the Gray input:

```verilog
buf buf1(binary_out[3], gray_in[3]);
```

The remaining binary bits are generated using XOR operations:

```verilog
xor xor1(binary_out[2], gray_in[2], binary_out[3]);

xor xor2(binary_out[1], gray_in[1], binary_out[2]);

xor xor3(binary_out[0], gray_in[0], binary_out[1]);
```

The conversion is performed sequentially from the most significant bit to the least significant bit.

## Conversion Example

Example:

```
Gray Input = 1111
```

Conversion:

```
Binary[3] = 1

Binary[2] = 1 XOR 1 = 0

Binary[1] = 1 XOR 0 = 1

Binary[0] = 1 XOR 1 = 0
```

Output:

```
Binary Output = 1010
```

## Truth Table

| Gray Input | Binary Output |
|:----------:|:-------------:|
| 0000 | 0000 |
| 0001 | 0001 |
| 0011 | 0010 |
| 0010 | 0011 |
| 0110 | 0100 |
| 0111 | 0101 |
| 0101 | 0110 |
| 0100 | 0111 |
| 1100 | 1000 |
| 1101 | 1001 |
| 1111 | 1010 |
| 1110 | 1011 |
| 1010 | 1100 |
| 1011 | 1101 |
| 1001 | 1110 |
| 1000 | 1111 |

## Project File

```
gray2binary.v
```

## Requirements

- Verilog HDL
- Any Verilog simulator such as:
  - Xilinx Vivado
  - ModelSim
  - Icarus Verilog

## Applications

- Rotary encoder interfaces
- Position and angle measurement systems
- Digital communication systems
- Error reduction circuits
- State machine decoding
- FPGA and ASIC digital designs

## Future Improvements

- Implement a parameterized Gray-to-Binary converter supporting different bit widths.
- Add Binary-to-Gray and Gray-to-Binary conversion in a single module.
- Create a self-checking testbench for automatic verification.
- Compare gate-level, dataflow, and behavioral implementations.

## Author

**Dileep Kumar Maddineni**