# Traffic Light Controller Using Finite State Machine (FSM) in Verilog HDL

## Overview

This project implements a **Traffic Light Controller** using a **Finite State Machine (FSM)** in Verilog HDL. The controller manages traffic flow between a **highway** and a **small road** using a vehicle **sensor**.

The highway is given higher priority. When a vehicle is detected on the small road, the controller safely transitions the traffic lights through **green**, **yellow**, and **red** states before allowing traffic from the small road to proceed.

The design demonstrates **FSM design**, **state transitions**, **parameterized states**, and **traffic light sequencing**.

---

# Features

- Finite State Machine (FSM)
- Five operating states
- Highway priority control
- Vehicle sensor input
- Green, Yellow, and Red traffic signals
- Configurable transition delays using macros
- Synchronous state transitions
- Asynchronous reset (clear)

---

# Module Description

## Module Name

```
traffic_light_control
```

The controller continuously monitors the vehicle sensor and changes the traffic signals accordingly.

---

# Inputs and Outputs

## Inputs

| Signal | Width | Description |
|--------|------:|-------------|
| `clk` | 1 bit | System clock |
| `clr` | 1 bit | Reset signal |
| `sensor` | 1 bit | Vehicle detected on small road |

---

## Outputs

| Signal | Width | Description |
|--------|------:|-------------|
| `highway` | 2 bits | Highway traffic light |
| `small_road` | 2 bits | Small-road traffic light |

---

# Traffic Light Encoding

```verilog
parameter RED    = 2'd0;
parameter YELLOW = 2'd1;
parameter GREEN  = 2'd2;
```

| Value | Light |
|------:|-------|
| 0 | Red |
| 1 | Yellow |
| 2 | Green |

---

# FSM States

```verilog
S0
S1
S2
S3
S4
```

| State | Highway | Small Road | Description |
|--------|---------|------------|-------------|
| S0 | Green | Red | Normal highway traffic |
| S1 | Yellow | Red | Highway preparing to stop |
| S2 | Red | Red | Safety transition |
| S3 | Red | Green | Small road traffic allowed |
| S4 | Red | Yellow | Small road preparing to stop |

---

# Delay Parameters

```verilog
`define G2YDELAY 3
`define Y2RDELAY 2
```

These macros are intended to represent transition delays.

| Macro | Purpose |
|--------|---------|
| `G2YDELAY` | Green-to-Yellow delay |
| `Y2RDELAY` | Yellow-to-Red delay |

---

# Working Principle

### 1. Reset

When

```verilog
clr = 1
```

the FSM returns to

```
S0
```

where

```
Highway → Green

Small Road → Red
```

---

### 2. Highway Operation

If no vehicle is detected:

```
sensor = 0
```

the controller remains in

```
S0
```

---

### 3. Vehicle Detection

When

```
sensor = 1
```

the controller transitions

```
S0

↓

S1

↓

S2

↓

S3
```

allowing the small road to receive a green signal.

---

### 4. Small Road Operation

As long as

```
sensor = 1
```

the FSM remains in

```
S3
```

keeping the small road green.

---

### 5. Returning to Highway

Once

```
sensor = 0
```

the controller transitions

```
S3

↓

S4

↓

S0
```

restoring highway priority.

---

# State Transition Diagram

```
             sensor=0
          +------------+
          |            |
          v            |
        +-----+        |
        | S0  |--------+
        +-----+
           |
     sensor=1
           |
           v
        +-----+
        | S1  |
        +-----+
           |
           v
        +-----+
        | S2  |
        +-----+
           |
           v
        +-----+
        | S3  |
        +-----+
        |     ^
sensor=0|     |sensor=1
        v     |
      +-----+ |
      | S4  |-+
      +-----+
           |
           v
          S0
```

---

# Output Table

| State | Highway | Small Road |
|--------|----------|------------|
| S0 | Green | Red |
| S1 | Yellow | Red |
| S2 | Red | Red |
| S3 | Red | Green |
| S4 | Red | Yellow |

---

# Example Operation

Initial state

```
Sensor = 0

Highway = Green

Small Road = Red
```

A vehicle arrives

```
Sensor = 1
```

Sequence

```
S0

↓

S1

↓

S2

↓

S3
```

Lights

```
Highway

Green

↓

Yellow

↓

Red

Small Road

Red

↓

Green
```

Vehicle leaves

```
Sensor = 0
```

Sequence

```
S3

↓

S4

↓

S0
```

Lights

```
Small Road

Green

↓

Yellow

↓

Red

Highway

Green
```

---

# Block Diagram

```
               +-------------------------+
 Sensor ------>|                         |
 Clock ------->| Traffic Light FSM       |
 Reset ------->|                         |
               +-------------------------+
                 |                   |
                 |                   |
                 v                   v
            Highway Light     Small Road Light
```

---

# Applications

## 1. Road Intersections

- Highway crossings
- Rural intersections
- Smart junctions

---

## 2. FPGA Projects

- FSM demonstrations
- Digital design laboratories
- Traffic control prototypes

---

## 3. Embedded Systems

- Intelligent transportation systems
- Adaptive traffic controllers
- Smart city infrastructure

---

# Advantages

- Simple FSM-based implementation
- Highway receives priority by default
- Easy to understand and extend
- Parameterized state and signal definitions

---

# Limitations

- The statements

```verilog
repeat (`G2YDELAY)
```

and

```verilog
repeat (`Y2RDELAY)
```

inside the combinational next-state logic **do not create real-time delays in synthesizable hardware**. They repeatedly execute assignments during simulation but do not wait for clock cycles.
- The FSM relies on a single sensor and does not account for multiple lanes, pedestrian crossings, or emergency vehicle priority.
- The reset (`clr`) is synchronous because it is checked only on `posedge clk`.

---

# Coding Improvements

### 1. Replace `repeat` with Clock Counters

Use a counter that increments on each clock cycle to implement actual timing delays instead of:

```verilog
repeat (`G2YDELAY)
```

This makes the design synthesizable and provides predictable timing.

---

### 2. Use `always @(*)`

Replace

```verilog
always @(state)
```

and

```verilog
always @(state or sensor)
```

with

```verilog
always @(*)
```

for cleaner combinational logic.

---

### 3. Add Default Assignments

Assign a default value to `next_state` at the beginning of the combinational block to reduce the risk of unintended latches if the FSM is modified later.

---

### 4. Use Nonblocking Assignments for Sequential Logic

The sequential state register already uses nonblocking assignments (`<=`), which is good practice. Keep combinational assignments as blocking (`=`) for clarity.

---

### 5. Enhance the Controller

Possible extensions include:

- Pedestrian crossing support
- Emergency vehicle override
- Adjustable green-light durations
- Countdown timers
- Multiple traffic sensors
- Left-turn signal control

---

# Project Files

```
traffic_light_control.v
```

---

## Author

**Dileep Kumar Maddineni**