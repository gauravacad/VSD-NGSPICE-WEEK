# Targeted Given Objectives to achieve
- From the VTC plot, determine ( V{IL}, V{IH}, V{OL}, V{OH} ) 
- Compute ( NML = V{IL} - V{OL} ) and ( NMH = V{OH} - V{IH} )

# Noise Margin for a basic CMOS Inverter Case:
### Overview
- This session is focused on CMOS inverter noise margin analysis. 
- Voltage levels VOH, VIH, VIL, and VOL define noise margins. The  noise margins high is (NMH = VOH - VIH) and noise margin low (NML = VIL - VOL), which determine    a circuit's tolerance to noise variations.
- Noise margin is critical for identifying crosstalk noise and glitches that commonly occur in lower   technology nodes, which can be identified beforehand through   proper noise margin evaluation.
- Further we will discuss and covers the relationship between CMOS inverter switching thresholds and noise robustness across different inverter sizes. 
- A head we will see few figures illustrating voltage thresholds and output logic states.

🔹 Noise Margins

| Type | Expression | Meaning |
|------|-------------|----------|
| **Noise Margin High (NM<sub>H</sub>)** | `NMH = VOH - VIH` | Maximum noise a logic ‘1’ can tolerate without being misinterpreted |
| **Noise Margin Low (NM<sub>L</sub>)** | `NML = VIL - VOL` | Maximum noise a logic ‘0’ can tolerate without being misinterpreted |

>[!tip]
> **Note:** Larger noise margins indicate better noise immunity and more robust digital performance.

### Basic Inverter Operation and Noise margin
The foundation for understanding noise margins by plotting voltage levels VOH, VIH, VIL, and VOL on a scale. VOH represents the highest voltage level, positioned close to VDD, followed by VIH. The critical relationship VOH > VIH ensures proper logic 1 detection at the next stage. Similarly, VIL > VOL relationship ensures logic 0 detection, with VOL being the lowest output voltage. An undefined region exists between VIH and VIL where voltage levels cannot be reliably classified as logic 1 or 0. These voltage specifications become part of chip specifications and define the operational boundaries for digital circuits

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

### Glitch Classification Based on Noise Margins
A more realistic voltage transfer curve was presented showing curved transitions instead of straight lines due to inverter non-idealities. The curve maintains negative slope in the transition region but exhibits gradual changes rather than sharp transitions. The practical curve demonstrates how real device characteristics affect the switching behavior and create margins around the ideal switching points.
Design Constraints and Next Stage Considerations

<img width="760" height="479" alt="image" src="https://github.com/user-attachments/assets/b9b32c1f-0fdc-472e-94d2-809484cedb4c" />


| Case | Noise Bump Level | Output Logic Behavior |
|------|------------------|------------------------|
| (a) **Bump < V<sub>IL</sub>** | Within `VOL–VIL` | Still considered **logic ‘0’** |
| (b) **Bump in Undefined Region** | Between `VIL–VIH` | Output becomes **undefined or unstable** |
| (c) **Bump > V<sub>IH</sub>** | Within `VIH–VOH` | Considered **logic ‘1’** |

> In real circuits, **noise bumps** or **glitches** may temporarily alter the signal voltage
> ⚠️ **Glitches** crossing into the undefined region can cause false triggering, metastability, or unpredictable circuit states.

## PMOS Width Variation Analysis w.r.t noise margin
- Through systematic analysis of PMOS width variations from 1x to 5x NMOS width, CMOS inverter robustness with noise margin variations remaining within acceptable     ranges despite fabrication imperfections.
- We observe increasing PMOS width improves noise margin high , while noise margin low remains relatively stable as NMOS is responsible for that.
- **Pmos is responsible for charge of capacitance and when we increase the size it can retain the charge for longer time**
- **If you increase the Width of Pmos high margin whereas no change in lower margin because NMOS cannot hold output zero.** 
- **Same time stronger PMOS limits the NMOS hold ability and thereby NMOS noise margin values gets deminssed.** 

<img width="1881" height="895" alt="image" src="https://github.com/user-attachments/assets/85e9a1c6-89e9-427a-9e49-3ba446e7ccac" />

---

## Digital vs Analog Design Applications
The analysis concluded that CMOS inverters excel in digital design applications where logic 1 and logic 0 detection is paramount. The well-defined noise margin ranges ensure reliable digital operation even with fabrication variations. For analog applications requiring voltage amplification, the transition region with high gain characteristics provides the optimal operating point. This distinction helps designers choose appropriate operating regions based on application requirements, whether for digital logic gates or analog amplification circuits.

<img width="450" height="350" alt="image" src="https://github.com/user-attachments/assets/58e5ed5d-b5bf-48cd-8cbd-85c5c9e05698" />

---

### LAB 4 Plotting Noise Margin in NGSPICE
- Evaluating the Noise margin witht the script below.
  
``` bash
*Model Description
.param temp=27
*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt
*Netlist Description
XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15
Cload out 0 50fF
Vdd vdd 0 1.8V
Vin in 0 1.8V
*simulation commands
.op
.dc Vin 0 1.8 0.01
.control
run
setplot dc1
display
.endc
.end
```

**Screenshot:**  Plot Vout vs Vin

<img width="709" height="623" alt="image" src="https://github.com/user-attachments/assets/d65f6037-8644-4bc8-8143-73568ad0a3bd" />

--- 

**Screenshot:**  Plot for noise margin estimation, observing the right point at slopes.

<img width="709" height="623" alt="image" src="https://github.com/user-attachments/assets/5d7b3afb-cd36-4007-a6c8-f5ff9e0ed5b1" />

---
<img width="699" height="259" alt="image" src="https://github.com/user-attachments/assets/3818baf0-9f28-41bc-8ad7-146447f32233" />

## 🔍 CMOS Inverter Noise Margin Analysis

| Parameter | Description | Value (V) | Formula / Relation |
|------------|--------------|-----------|--------------------|
| **ViL** | Input voltage at transition (low → high) | 0.741758 | x0 |
| **ViH** | Input voltage at transition (high → low) | 0.991209 | x0 |
| **VoL** | Output voltage (logic 0) | 0.08636 | Y0 |
| **VoH** | Output voltage (logic 1) | 1.74545 | Y0 |
| **NMH** | Noise Margin High | **0.754** | `VoH − ViH` |
| **NML** | Noise Margin Low | **0.655** | `ViL − VoL` |

---

> 🧠 **Observation:**  
> Both **NMH** and **NML** are well-balanced (~0.65–0.75 V), indicating **good noise immunity** and **robust logic level separation** for the given CMOS inverter.

### ✅ Summary

- **Logic ‘0’**: Stable between VOL–VIL  
- **Logic ‘1’**: Stable between VIH–VOH  
- **Undefined Region**: Unstable and to be avoided  
- **Noise Margins (NMH, NML)** define tolerance against external disturbances

## Next session is Power Supply Scaling Transition
The scaling discussion represents a natural progression from noise margin analysis, as smaller technology nodes introduce new challenges related to power supply voltages, noise immunity, and circuit robustness that build upon the fundamental noise margin concepts are learned.
