# VSD Hardware Design Program - NGSPICE for WEEK4
---

# ⚙️ CMOS Inverter Characterization and SPICE Simulation Summary

This repository documents a detailed exploration of **CMOS inverter behavior** using **Sky130 PDK**, covering both **device-level** and **circuit-level** simulations.  
Each section (Part 1–6) investigates a key design aspect, from **MOSFET characteristics** to **robustness under variations**, with SPICE decks, observations, and analytical insights.

---

## 📘 Contents
1. [Part 1: MOSFET Behavior & Id–Vds Characteristics](#part-1-mosfet-behavior--id-vs-vds-characteristics)  
2. [Part 2: Threshold Voltage Extraction & Velocity Saturation](#part-2-threshold-voltage-extraction--velocity-saturation)  
3. [Part 3: CMOS Inverter: Voltage Transfer Characteristic (VTC)](#part-3-cmos-inverter-voltage-transfer-characteristic-vtc)  
4. [Part 4: Transient Behavior: Rise–Fall Delays](#part-4-transient-behavior-rise---fall-delays)  
5. [Part 5: Noise Margin & Robustness Analysis](#part-5-noise-margin---robustness-analysis)  
6. [Part 6: Power Supply and Device Variation Studies](#part-6-power-supply-and-device-variation-studies)

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

🔗 **Reference:** [Part 1: MOSFET Behavior (link)](https://example.com/part1)

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

🔗 **Reference:** [Part 2: Threshold Voltage (link)](https://example.com/part2)

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

🔗 **Reference:** [Part 3: CMOS Inverter VTC (link)](https://example.com/part3)

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

🔗 **Reference:** [Part 4: Transient Analysis (link)](https://example.com/part4)

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

🔗 **Reference:** [Part 5: Noise Margin (link)](https://example.com/part5)

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

🔗 **Reference:** [Part 6: Power & Variation (link)](https://example.com/part6)

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

    
