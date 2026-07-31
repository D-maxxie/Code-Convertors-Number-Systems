# BCD to 7-Segment Display Decoder using Verilog

## 📖 Overview

This project implements a **BCD (Binary-Coded Decimal) to 7-Segment Display Decoder** using Verilog HDL. The decoder converts a 4-bit BCD input into the corresponding seven control signals required to display decimal digits (0–9) on a seven-segment display.

The design uses **combinational Boolean logic expressions** for each segment (`a` through `g`) instead of lookup tables or case statements. This approach demonstrates logic minimization and gate-level implementation of digital decoders.

The module is fully synthesizable and suitable for FPGA and ASIC applications.

---

## ✨ Features

- Converts 4-bit BCD input to 7-segment output
- Supports decimal digits **0–9**
- Pure combinational logic implementation
- Uses minimized Boolean expressions
- No clock required
- Fully synthesizable Verilog HDL
- FPGA and ASIC compatible

---

## 📋 Specifications

| Parameter | Description |
|-----------|-------------|
| Language | Verilog HDL |
| Module Name | `BCD_to_7segment` |
| Input Width | 4 bits |
| Output Width | 7 bits |
| Logic Type | Combinational |
| Supported Digits | 0–9 |

---

## 🏗️ Block Diagram

```
                 +----------------------------+
BCD[3:0] ------->|                            |
                 |  BCD to 7-Segment Decoder  |
                 |                            |
                 +------------+---------------+
                              |
                              |
                      segment7[6:0]
```

---

## 🏗️ Seven-Segment Display

```
      ---a---
     |       |
     f       b
     |       |
      ---g---
     |       |
     e       c
     |       |
      ---d---
```

Each output controls one LED segment:

| Output | Segment |
|---------|---------|
| a | Top |
| b | Upper Right |
| c | Lower Right |
| d | Bottom |
| e | Lower Left |
| f | Upper Left |
| g | Middle |

---

## ⚙️ Functional Description

The module accepts a 4-bit BCD input representing decimal digits:

```
0000 → 0

0001 → 1

...

1001 → 9
```

Using Boolean expressions, the decoder determines which segments should be activated to display the corresponding decimal digit.

The final output is:

```verilog
segment7 = {a, b, c, d, e, f, g};
```

---

## 📊 BCD Truth Table

| Decimal | BCD Input |
|-----------|-----------|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |

Inputs from `1010` to `1111` are **invalid BCD values** and are not explicitly handled by this implementation.

---

## 🔢 Example Outputs

| BCD | Decimal | Display |
|------|---------|----------|
| 0000 | 0 | 0 |
| 0001 | 1 | 1 |
| 0010 | 2 | 2 |
| 0011 | 3 | 3 |
| 0100 | 4 | 4 |
| 0101 | 5 | 5 |
| 0110 | 6 | 6 |
| 0111 | 7 | 7 |
| 1000 | 8 | 8 |
| 1001 | 9 | 9 |

---

## ⏱️ Timing Behavior

- Pure combinational circuit
- No clock or reset required
- Output updates immediately when the BCD input changes
- Propagation delay depends only on combinational logic depth

---

## 💡 Applications

- Digital clocks
- Calculator displays
- Embedded systems
- FPGA display interfaces
- Digital counters
- Scoreboards
- Measurement instruments
- Educational digital electronics projects

---

## ✅ Advantages

- Simple gate-level implementation
- Fast combinational response
- No sequential elements
- Fully synthesizable RTL
- Low hardware complexity
- Suitable for FPGA and ASIC designs

---

## 🧪 Simulation

### Recommended Simulators

- Xilinx Vivado Simulator
- ModelSim
- QuestaSim
- Icarus Verilog
- GTKWave

### Sample Test Cases

| BCD Input | Expected Digit |
|------------|----------------|
| 0000 | 0 |
| 0001 | 1 |
| 0010 | 2 |
| 0011 | 3 |
| 0100 | 4 |
| 0101 | 5 |
| 0110 | 6 |
| 0111 | 7 |
| 1000 | 8 |
| 1001 | 9 |

---

## 🔧 Synthesis

- FPGA Compatible ✅
- ASIC Compatible ✅
- Fully Synthesizable RTL ✅
- Pure combinational implementation
- Gate-level Boolean logic

> **Note:** The output polarity depends on the type of seven-segment display being used. This implementation assumes a specific segment activation convention. For a **common-anode** display, the outputs may need to be inverted, while for a **common-cathode** display, the current logic may be used directly depending on the hardware. Additionally, invalid BCD inputs (`1010–1111`) are not explicitly decoded and may produce undefined segment patterns.

---

## 📁 Project Structure

```text
BCD_to_7segment/

├── rtl/
│   └── BCD_to_7segment.v
│
├── tb/
│   └── BCD_to_7segment_tb.v
│
├── docs/
│   ├── seven_segment_layout.png
│   ├── truth_table.png
│   ├── timing_diagram.png
│   └── waveform.png
│
└── README.md
```

---

## 🚀 Future Improvements

- Add support for hexadecimal digits (A–F)
- Parameterize output polarity (common-anode/common-cathode)
- Implement decoder using a `case` statement for readability
- Add don't-care optimization for invalid BCD inputs
- Develop a self-checking SystemVerilog testbench
- Integrate with a multiplexed multi-digit display controller

---

## 👨‍💻 Author

**Maddineni Dileep Kumar**

---
