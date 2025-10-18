# Targeted Given Objectives to achieve
- From the VTC plot, determine ( V{IL}, V{IH}, V{OL}, V{OH} ) 
- Compute ( NML = V{IL} - V{OL} ) and ( NMH = V{OH} - V{IH} )

# Noise Margin for a basic CMOS Inverter Case:
### Overview
- This session is focused on CMOS inverter noise margin analysis. Noise margin is critical for identifying crosstalk noise and glitches that commonly occur in lower   technology nodes, which can be identified beforehand through proper noise margin evaluation. The session covered the relationship between CMOS inverter switching    thresholds and noise robustness across different inverter sizes. 
- Key voltage parameters were introduced including VIL (input low voltage around 1/4 of VDD), VIH (input high voltage around 3/4 of VDD), VOL (output low voltage),    and VOH (output high voltage). Using a 1-volt VDD example, VIL was demonstrated at 250 millivolts and VIH at 750 millivolts.
- The presentation progressed from ideal inverter characteristics with infinite slope at VDD/2 switching point to more practical scenarios with finite slopes due to   real device resistances and capacitances.

# 🧠 Noise Margin Summary

This document summarizes the concept of **Noise Margins**, **Logic Levels**, and how **glitches** or **noise spikes** affect digital logic outputs. The discussion is based on the two diagrams illustrating voltage thresholds and output logic states.

---



---

## 🔹 Noise Margins

| Type | Expression | Meaning |
|------|-------------|----------|
| **Noise Margin High (NM<sub>H</sub>)** | `NMH = VOH - VIH` | Maximum noise a logic ‘1’ can tolerate without being misinterpreted |
| **Noise Margin Low (NM<sub>L</sub>)** | `NML = VIL - VOL` | Maximum noise a logic ‘0’ can tolerate without being misinterpreted |

> **Note:** Larger noise margins indicate better noise immunity and more robust digital performance.

---

## 🔹 Noise and Glitches

In real circuits, **noise bumps** or **glitches** may temporarily alter the signal voltage:



---

## 🔹 Design Insights

- Keep signals **within NM<sub>L</sub>** and **NM<sub>H</sub>** ranges to maintain **reliable logic levels**.
- **Undefined regions** should be avoided in practical circuit design.
- Proper **noise margin design** improves immunity against voltage fluctuations, crosstalk, and switching noise.

---

### 📘 Reference Equations

\[
NM_H = V_{OH} - V_{IH}
\]
\[
NM_L = V_{IL} - V_{OL}
\]

---

### ✅ Summary

- **Logic ‘0’**: Stable between VOL–VIL  
- **Logic ‘1’**: Stable between VIH–VOH  
- **Undefined Region**: Unstable and to be avoided  
- **Noise Margins (NMH, NML)** define tolerance against external disturbances  

> _Any signal in the undefined region will be of indefinite logic level._

---



### Key Points
-Plot voltage levels (VIH, VIL, VOH, VOL) on a single voltage axis in Ngspice

### Noise Margin Introduction and Importance
Noise margin is a critical parameter related to crosstalk noise and glitches, which are typical issues in lower technology nodes. Noise margin helps identify potential problems beforehand by evaluating the robustness of logic circuits. we aim to understand how CMOS inverter switching thresholds relate to noise margin performance across different inverter sizes?

### Basic Inverter Operation and Characteristics
The fundamental inverter operation was explained where logic low input produces logic high output and vice versa. A voltage transfer characteristic graph was plotted with Vout on y-axis and Vin on x-axis, showing that when input is 0, output is VDD, and when input is high, output drops to zero. The switching occurs around VDD/2 due to PMOS and NMOS transistor behavior.

<img width="773" height="563" alt="image" src="https://github.com/user-attachments/assets/36f42c35-9930-425c-854b-538052a6c002" />

---

### Ideal vs Practical Slope Analysis
In ideal conditions, the inverter shows infinite slope at the switching point (VDD/2) because output changes from VDD to zero with no change in input voltage, creating a slope of VDD/0 = infinite. However, practical scenarios involve real resistances and capacitances in NMOS and PMOS devices, resulting in finite slopes and gradual transitions rather than instantaneous switching.

<img width="773" height="563" alt="image" src="https://github.com/user-attachments/assets/ed252b9f-11cb-4e57-a4ea-063374ed033d" />

---
### Voltage Level Definitions and Ranges
Key voltage parameters were defined: VIL represents the maximum input voltage recognized as logic 0 (approximately 1/4 of VDD or 250mV for 1V VDD), while VIH represents the minimum input voltage recognized as logic 1 (approximately 3/4 of VDD or 750mV for 1V VDD). Input voltages between 0 and VIL produce high outputs (VOH), while voltages between VIH and VDD produce low outputs (VOL).


<img width="1522" height="435" alt="image" src="https://github.com/user-attachments/assets/2c4a30d2-f6ae-4798-861c-754cc6dc249f" />

---

<img width="773" height="563"  alt="image" src="https://github.com/user-attachments/assets/41253979-cf1b-47c5-9609-27689717a7e7" />

## 🔹 Logic Levels

| Logic Level | Voltage Range | Description |
|--------------|----------------|--------------|
| **Logic ‘1’ (High)** | Between **V<sub>IH</sub>** and **V<sub>OH</sub>** | Recognized as a valid high-level logic signal |
| **Logic ‘0’ (Low)** | Between **V<sub>OL</sub>** and **V<sub>IL</sub>** | Recognized as a valid low-level logic signal |
| **Undefined Region** | Between **V<sub>IL</sub>** and **V<sub>IH</sub>** | Not clearly identified as ‘0’ or ‘1’; may cause metastability or unpredictable behavior |

### Practical Curve Analysis and Non-Idealities: Undefined and Glitches.
A more realistic voltage transfer curve was presented showing curved transitions instead of straight lines due to inverter non-idealities. The curve maintains negative slope in the transition region but exhibits gradual changes rather than sharp transitions. The practical curve demonstrates how real device characteristics affect the switching behavior and create margins around the ideal switching points.
Design Constraints and Next Stage Considerations

<img width="760" height="479" alt="image" src="https://github.com/user-attachments/assets/b9b32c1f-0fdc-472e-94d2-809484cedb4c" />


| Case | Noise Bump Level | Output Logic Behavior |
|------|------------------|------------------------|
| (a) **Bump < V<sub>IL</sub>** | Within `VOL–VIL` | Still considered **logic ‘0’** |
| (b) **Bump in Undefined Region** | Between `VIL–VIH` | Output becomes **undefined or unstable** |
| (c) **Bump > V<sub>IH</sub>** | Within `VIH–VOH` | Considered **logic ‘1’** |

> ⚠️ **Glitches** crossing into the undefined region can cause false triggering, metastability, or unpredictable circuit states.
