# Gray-to-Binary Converter ASIC

## Project Overview

This project implements a **4-bit Gray-to-Binary Converter** following the ASIC design flow from **Front-end to Back-end**.

The complete design flow includes:

**RTL Design → Functional Verification → Logic Synthesis → Formal Verification → Floorplan → Placement → Routing → DRC/LVS → Post-layout Verification**

---

## Project Objectives

* Design a 4-bit Gray-to-Binary Converter.
* Describe the design using Verilog RTL.
* Perform functional verification.
* Synthesize the RTL design into standard cells.
* Perform formal equivalence verification.
* Implement the physical design.
* Perform DRC and LVS checks.
* Evaluate timing and physical design results.

---

## 🔌 Design Specification

| Signal   | Direction | Width | Description        |
| -------- | --------- | ----: | ------------------ |
| `gray`   | Input     | 4-bit | Gray Code input    |
| `binary` | Output    | 4-bit | Binary Code output |

### Gray-to-Binary Conversion

The conversion is performed according to:

```text
B3 = G3
B2 = B3 ^ G2
B1 = B2 ^ G1
B0 = B1 ^ G0
```

where:

* `G[3:0]` is the Gray Code input.
* `B[3:0]` is the Binary Code output.
* `^` represents the XOR operation.

---

## ASIC Design Flow

### 1. RTL Design

The Gray-to-Binary Converter is described using Verilog RTL.

### Simulation Waveform
![Simulation Waveform](img/simulation.png)

The RTL design is verified using test vectors to ensure that the Gray Code is correctly converted to Binary Code.

### 3. Logic Synthesis

The RTL is synthesized using **Synopsys Design Compiler**.

The synthesis process generates a mapped netlist using standard cells from the technology library.

### 4. Formal Verification

Formal equivalence checking is performed using **Synopsys Formality** to verify that the synthesized netlist is functionally equivalent to the original RTL design.
![Formal Verification](img/formal.png)

### 5. Floorplan

The physical design is initialized with a target core utilization of 60%.

Due to placement site and grid constraints, the final core utilization is:

```text
Core Utilization = 81.03%
```
![Floorplan](img/reportutilazation.png)

### 6. Placement

Standard cells are placed inside the core area and legalization is performed.

Result:
![Flacement](img/placement.png)

```text
Placement Legality = PASS
Placement Violations = 0
```


### 7. Routing

The design is routed using the available metal layers.

Result:
![Routing](img/rout.png)

```text
Routing Overflow = 0%
```

### 8. DRC / LVS

Design Rule Check and Layout Versus Schematic checks are performed after physical implementation.

Results:

![DRC / LVS](img/drc.png)
![DRC / LVS](img/lvs1.png)

```text
DRC Violations = 0
LVS = MATCH
```

---

## Synthesis Results

| Parameter                  |    Result |
| -------------------------- | --------: |
| Standard Cells             |         4 |
| Leaf Cell Count            |         4 |
| Combinational Cells        |         4 |
| Sequential Cells           |         0 |
| Critical Path              |   0.30 ns |
| TNS                        |      0 ns |
| Design Area                | 12.913265 |
| Cell Area                  | 11.944768 |
| Net Area                   |  0.968496 |
| Max Transition Violations  |         0 |
| Max Capacitance Violations |         0 |

---

## Formal Verification

Formal verification result:
![Formal Verification](img/formal1.png)

```text
Verification: SUCCEEDED
Passing Compare Points: 4
Failing Compare Points: 0
```

The synthesized implementation is functionally equivalent to the original RTL design.

---

##  Back-end Results

| Parameter        |       Result |
| ---------------- | -----------: |
| Core Utilization |       81.03% |
| Cell Area        |    11.94 µm² |
| Physical Area    |    11.95 µm² |
| Total Area       |    14.74 µm² |
| Standard Cells   |            4 |
| Nets             |           10 |
| Routing Overflow |           0% |
| DRC              | 0 Violations |
| LVS              |        Match |
| Setup Timing     |         PASS |
| Hold Timing      |         PASS |
| Timing Sign-off  |         PASS |

---

## Timing Results

| Parameter         |    Result |
| ----------------- | --------: |
| Clock Period      |     20 ns |
| Frequency         |    50 MHz |
| Critical Path     |   0.30 ns |
| WNS (Setup Slack) | +19.70 ns |
| TNS               |      0 ns |
| Timing Sign-off   |      PASS |


## Final Result

The 4-bit Gray-to-Binary Converter successfully completed the ASIC design flow from RTL to physical implementation.

Final verification results:

```text
RTL Simulation       : PASS
Functional Verification : PASS
Logic Synthesis      : PASS
Formal Verification  : PASS
Placement            : PASS
Routing              : PASS
DRC                  : PASS
LVS                  : PASS
Setup Timing         : PASS
Hold Timing          : PASS
Timing Sign-off      : PASS
```

