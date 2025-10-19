# VSD Hardware Design Program - NGSPICE for WEEK4
---

# ⚙️ CMOS Inverter Characterization and SPICE Simulation Summary

This repository documents a detailed exploration of **CMOS inverter behavior** using **Sky130 PDK**, covering both **device-level** and **circuit-level** simulations.  
Each section (Part 1–6) investigates a key design aspect, from **MOSFET characteristics** to **robustness under variations**, with SPICE decks, observations, and analytical insights.

---
## 📘 Table of Contents
1. [Part 1: MOSFET Behavior & Id–Vds Characteristics](https://github.com/gauravacad/VSD-NGSPICE-WEEK/tree/main/Part-1%3A%20MOSFET%20Behavior%20%26%20Id%20vs.%20Vds%20Characteristics)
2. [Part 2: Threshold Voltage Extraction & Velocity Saturation](https://github.com/gauravacad/VSD-NGSPICE-WEEK/tree/main/Part-2%3AThreshold%20Voltage%20Extraction%20%26%20Velocity%20Saturation)
3. [Part 3: CMOS Inverter: Voltage Transfer Characteristic (VTC)](https://github.com/gauravacad/VSD-NGSPICE-WEEK/tree/main/Part%203%3A%20CMOS%20Inverter%3A%20Voltage%20Transfer%20Characteristic%20(VTC))
4. [Part 4: Transient Behavior: Rise–Fall Delays](https://github.com/gauravacad/VSD-NGSPICE-WEEK/tree/main/Part%203%3A%20CMOS%20Inverter%3A%20Voltage%20Transfer%20Characteristic%20(VTC))
5. [Part 5: Noise Margin & Robustness Analysis](https://github.com/gauravacad/VSD-NGSPICE-WEEK/tree/main/Part%205%3A%20Noise%20Margin%20-%20Robustness%20Analysis)
6. [Part 6: Power-Supply and Device Variation Studies](https://github.com/gauravacad/VSD-NGSPICE-WEEK/tree/main/Part%206%3A%20Power-Supply%20and%20Device%20Variation%20Studies)
---

## 🧩 Part 1: MOSFET Behavior & Id vs. Vds Characteristics

**Objective:**  
To simulate and understand the **I–V characteristics** of NMOS and PMOS devices under various gate voltages using **Sky130 models**.

**Key Aspects:**
- Observe **linear**, **saturation**, and **cutoff** regions.  
- Verify **channel modulation** behavior.  
- Extract **transconductance (gm)** and **output resistance (ro)**.  
- Validate simulation with theoretical Shockley equations.  

**Learning Outcome:**  
Established a clear foundation on **MOSFET operation** and its regions — essential for CMOS circuit understanding.

🔗 **Reference:** [Part 1: MOSFET Behavior](https://www.udemy.com/course/vlsi-academy-circuit-design/?srsltid=AfmBOorIsNySPoeoUeR6sxZ3ZHzTM2YOlGLkyDa0r9rz445OUdjEL9ot)

---

## ⚡ Part 2: Threshold Voltage Extraction & Velocity Saturation

**Objective:**  
To determine **threshold voltage (Vth)** and analyze **velocity saturation** effects for short-channel MOSFETs.

**Key Aspects:**
- Extract `Vth` from **Id–Vgs transfer curve**.  
- Analyze **subthreshold slope** and **body effect**.  
- Observe **mobility degradation** at higher fields.  
- Compare **long vs. short channel** behavior.  

**Learning Outcome:**  
Understood that **Vth shifts** with channel length and body bias, and that **velocity saturation** limits drive current at nanoscale dimensions.

🔗 **Reference:** [Part 2: Threshold Voltage](https://www.udemy.com/course/vlsi-academy-circuit-design/?srsltid=AfmBOorIsNySPoeoUeR6sxZ3ZHzTM2YOlGLkyDa0r9rz445OUdjEL9ot)

---

## 🧠 Part 3: CMOS Inverter — Voltage Transfer Characteristic (VTC)

**Objective:**  
To build a CMOS inverter and analyze its **Voltage Transfer Characteristics (VTC)**.

**Key Aspects:**
- Use **Sky130_fd_pr__pfet_01v8** and **nfet_01v8** models.  
- Sweep input voltage (`Vin`) from 0 → 1.8 V.  
- Plot `Vout` vs. `Vin` to identify **switching threshold (Vm)**.  
- Vm observed ≈ **0.87 V** — where **Vin = Vout**.  

**Learning Outcome:**  
Demonstrated how **W/L ratios** influence **switching threshold** and how the inverter achieves **rail-to-rail logic levels**.

🔗 **Reference:** [Part 3: CMOS Inverter VTC (link)](https://www.udemy.com/course/vlsi-academy-circuit-design/?srsltid=AfmBOorIsNySPoeoUeR6sxZ3ZHzTM2YOlGLkyDa0r9rz445OUdjEL9ot)

---

## ⏱️ Part 4: Transient Behavior — Rise & Fall Delays

**Objective:**  
To perform **transient analysis** of the CMOS inverter by applying a **pulse input** and measuring **rise/fall times**.

**Key Aspects:**
- Input pulse: 0 → 1.8 V, period = 4 ns.  
- Measure output delay at **50% VDD**.  
- Rise time ≈ **0.33 ns**, Fall time ≈ **0.285 ns**.  
- Delay asymmetry due to **mobility differences** between PMOS and NMOS.  

**Learning Outcome:**  
Established understanding of **propagation delay**, **asymmetric switching**, and **impact of load capacitance** on speed.

🔗 **Reference:** [Part 4: Transient Analysis](https://www.udemy.com/course/vlsi-academy-circuit-design/?srsltid=AfmBOorIsNySPoeoUeR6sxZ3ZHzTM2YOlGLkyDa0r9rz445OUdjEL9ot)

---

## 📉 Part 5: Noise Margin & Robustness Analysis

**Objective:**  
To calculate **Noise Margins (NML & NMH)** and examine **robustness** under process and sizing variations.

**Key Aspects:**
- Extract `ViH`, `ViL`, `VoH`, `VoL` from the VTC curve.  
- Compute:
  - **NML = ViL – VoL**
  - **NMH = VoH – ViH**  
- Observe undefined region and identify **glitch tolerance**.  
- Analyze **impact of Wp/Wn ratio** on stability.  

**Learning Outcome:**  
Demonstrated that CMOS inverters maintain stable logic levels despite variations, proving **robustness** across conditions.

🔗 **Reference:** [Part 5: Noise Margin](https://www.udemy.com/course/vlsi-academy-circuit-design/?srsltid=AfmBOorIsNySPoeoUeR6sxZ3ZHzTM2YOlGLkyDa0r9rz445OUdjEL9ot)

---

## 🔋 Part 6: Power-Supply and Device Variation Studies

**Objective:**  
To evaluate inverter performance under **supply voltage** and **device parameter** variations.

**Key Aspects:**
- Sweep `VDD` from **5 V → 2.5 V → 1.8 V**.  
- Observe corresponding **Vm**, **gain**, and **energy-delay** changes.  
- Validate that **dynamic power (P ∝ V²f)** decreases drastically with lower VDD.  
- Examine **device strength mismatch** (Strong NMOS vs. Weak PMOS).  

**Learning Outcome:**  
Confirmed that CMOS inverters are **scalable and energy-efficient**, and that **switching threshold shifts** minimally with device variation.

🔗 **Reference:** [Part 6: Power & Variation](https://www.udemy.com/course/vlsi-academy-circuit-design/?srsltid=AfmBOorIsNySPoeoUeR6sxZ3ZHzTM2YOlGLkyDa0r9rz445OUdjEL9ot)

---

## 🧾 Summary

| Part | Focus | Key Takeaway |
|------|--------|--------------|
| 1 | MOSFET I–V Characteristics | Foundation for understanding current flow and device operation |
| 2 | Threshold & Velocity Saturation | Short-channel and high-field effects awareness |
| 3 | CMOS Inverter VTC | Relationship between input and output logic levels |
| 4 | Transient Behavior | Rise/fall delay measurement and propagation timing |
| 5 | Noise Margin | Robustness and logic stability assessment |
| 6 | Power & Variation | Power optimization and tolerance verification |

---

## 📚 References

- [VSD Lecture Series](https://example.com/vsd)  
- [SkyWater Sky130 PDK Documentation](https://example.com/sky130)  
- [CMOS Theory Notes](https://example.com/notes)  
- [Kunal Sir’s CMOS Design Tutorials](https://example.com/tutorials)

---

> 💡 **Tip:** Each part is self-contained — you can navigate directly using the reference links above and replace them with your actual GitHub or documentation URLs later.

    
