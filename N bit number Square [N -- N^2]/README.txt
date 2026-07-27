# N-Bit Square Calculator in Verilog

## Overview

This project implements an **N-bit Square Calculator** using Verilog HDL. The module takes an N-bit binary input value and calculates its square, producing a result with a width of **2N bits** to store the complete squared value.

The design uses Verilog's arithmetic multiplication operator to perform the squaring operation and is implemented using **behavioral modeling** with an `always @(*)` block. The parameterized structure allows the module to support different input widths without modifying the core design.

## Features

- Calculates the square of an N-bit input number
- Parameterized input width for flexible design
- Generates a 2N-bit output to prevent data loss
- Uses combinational logic implementation
- No clock or sequential elements required
- Fully synthesizable for FPGA and ASIC implementations

## Module Description

### N-Bit Square Module (`n_bit_square`)

The module accepts an N-bit unsigned input and produces its squared value as a 2N-bit output.

The default configuration:

```
Input width  = 4 bits
Output width = 8 bits
```

The parameter `n` can be modified to support different input sizes.

## Inputs and Output

### Input

| Signal | Width | Description |
|--------|------:|-------------|
| `num` | N bits | Binary input number to be squared |

### Output

| Signal | Width | Description |
|--------|------:|-------------|
| `result` | 2N bits | Square of the input value |

## How It Works

The multiplication operation is performed inside the combinational block:

```verilog
tmp = num * num;
result = tmp;
```

The input value is multiplied by itself:

```
Result = num × num
```

The intermediate register `tmp` stores the multiplication result before assigning it to the output.

For example, with a 4-bit input:

```
num = 4'b0011

3 × 3 = 9

result = 8'b00001001
```

## Parameter Configuration

The module uses a parameter to define the input size:

```verilog
parameter n = 4;
```

Changing the parameter automatically adjusts the input and output widths.

Example:

| Parameter | Input Width | Output Width |
|----------:|------------:|-------------:|
| 4 | 4 bits | 8 bits |
| 8 | 8 bits | 16 bits |
| 16 | 16 bits | 32 bits |

## Project File

```
n_bit_square.v
```

## Example Operation

For a 4-bit input:

| Input (`num`) | Decimal Value | Square (`result`) |
|:-------------:|--------------:|------------------:|
| `0000` | 0 | 0 |
| `0001` | 1 | 1 |
| `0010` | 2 | 4 |
| `0011` | 3 | 9 |
| `0100` | 4 | 16 |
| `1111` | 15 | 225 |

## Requirements

- Verilog HDL
- Any Verilog simulator such as:
  - Xilinx Vivado
  - ModelSim
  - Icarus Verilog

## Applications

- Arithmetic Logic Unit (ALU) design
- Digital signal processing systems
- Mathematical accelerator circuits
- FPGA-based computation modules
- Learning arithmetic hardware implementation

## Future Improvements

- Implement a multiplier-based gate-level architecture.
- Add signed number support.
- Optimize the design for area and timing.
- Create a pipelined version for high-speed applications.
- Add a testbench for automatic verification.

## Author

**Dileep Kumar Maddineni**