# Square Root and Cube Root Calculator using Verilog

## 📖 Overview

This project implements a **Square Root and Cube Root Calculator** using Verilog HDL. Given a **32-bit unsigned input number**, the module computes both its square root and cube root using Verilog arithmetic operators inside user-defined tasks.

The design demonstrates the use of:

- User-defined **tasks**
- Real-number exponentiation
- Arithmetic operations
- Procedural blocks
- Simulation-oriented mathematical modeling

Whenever the input value changes, the module calculates the square root and cube root and displays the results using `$display`.

> **Note:** This implementation is intended primarily for **simulation and educational purposes**, as it relies on real-number exponentiation, which is generally **not synthesizable**.

---

## ✨ Features

- Computes square root and cube root
- 32-bit input and output
- Uses Verilog tasks
- Automatic calculation on input change
- Console output using `$display`
- Demonstrates exponentiation operator (`**`)
- Suitable for simulation and learning

---

## 📋 Specifications

| Parameter | Description |
|-----------|-------------|
| Language | Verilog HDL |
| Module Name | `root` |
| Input Width | 32 bits |
| Output Width | 32 bits |
| Operations | Square Root, Cube Root |
| Trigger | Input value change |
| Implementation | User-defined Tasks |

---

## 🏗️ Block Diagram

```
                  +---------------------------+
number[31:0] ---->|                           |
                  |    Root Calculator        |
                  |                           |
                  |  Square Root Task         |
                  |  Cube Root Task           |
                  +------------+--------------+
                               |
                 +-------------+-------------+
                 |                           |
           sq_root[31:0]             cube_root[31:0]
```

---

## ⚙️ Functional Description

The module monitors changes to the input:

```verilog
always @(number)
```

Whenever the input changes:

1. The square root task is executed.
2. The cube root task is executed.
3. Both results are assigned to the outputs.
4. The values are printed to the simulation console.

---

## 📌 Square Root Task

```verilog
res = num ** (0.5);
```

This computes:

```
√number
```

---

## 📌 Cube Root Task

```verilog
res = num ** (0.33);
```

This approximates:

```
³√number
```

using an exponent of **0.33**.

---

## 🔢 Example Calculations

| Input | Square Root | Cube Root (Approx.) |
|--------|-------------|---------------------|
| 1 | 1 | 1 |
| 4 | 2 | 1 |
| 8 | 2 | 2 |
| 9 | 3 | 2 |
| 27 | 5 | 3 |
| 64 | 8 | 4 |
| 125 | 11 | 5 |

> Since the outputs are 32-bit integers, fractional values are truncated.

---

## ⏱️ Timing Behavior

- No clock is required.
- The module is purely event-driven.
- Calculations occur immediately when the input changes.
- Results are updated and printed during simulation.

---

## 💡 Applications

- Verilog task demonstration
- Arithmetic operator learning
- Simulation-based mathematical modeling
- Digital design education
- Functional verification experiments
- Testbench utility functions

---

## ✅ Advantages

- Demonstrates reusable Verilog tasks
- Simple implementation
- Easy to understand
- Automatic computation on input change
- Good educational example
- No complex iterative algorithms required

---

## 🧪 Simulation

### Recommended Simulators

- Xilinx Vivado Simulator
- ModelSim
- QuestaSim
- Icarus Verilog
- GTKWave

### Sample Test Cases

| Input Number | Expected Square Root | Expected Cube Root (Approx.) |
|--------------|----------------------|-------------------------------|
| 1 | 1 | 1 |
| 16 | 4 | 2 |
| 25 | 5 | 2 |
| 64 | 8 | 4 |
| 125 | 11 | 5 |
| 256 | 16 | 6 |

Simulation console example:

```
Square Root of 64 is 8
Cube Root of   64 is 4
```

---

## 🔧 Synthesis

- Simulation Only ⚠️
- Not Intended for FPGA/ASIC Synthesis ❌
- Uses real-number arithmetic and exponentiation
- Demonstrates Verilog procedural constructs

> **Note:** This implementation is **not synthesizable** because it uses real-valued exponents (`0.5` and `0.33`) with the `**` operator. Additionally, using `0.33` is only an approximation of \(1/3\), so cube root results may be inaccurate for some values. Hardware implementations typically use iterative algorithms such as **Newton-Raphson**, **binary search**, or **CORDIC** for square-root and cube-root calculations.

---

## 📁 Project Structure

```text
root_calculator/

├── rtl/
│   └── root.v
│
├── tb/
│   └── root_tb.v
│
├── docs/
│   ├── block_diagram.png
│   ├── simulation_output.png
│   └── waveform.png
│
└── README.md
```

---

## 🚀 Future Improvements

- Implement synthesizable square-root algorithms
- Implement accurate cube-root algorithms
- Support floating-point outputs
- Add parameterized input width
- Develop a self-checking SystemVerilog testbench
- Compare iterative and lookup-table-based implementations
- Improve cube-root precision using `1.0/3.0` in simulation

---

## 👨‍💻 Author

**Maddineni Dileep Kumar**

---
