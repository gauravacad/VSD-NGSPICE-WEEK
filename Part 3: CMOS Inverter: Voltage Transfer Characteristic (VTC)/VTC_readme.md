# ⚡ CMOS Inverter – SPICE Simulation and Design Analysis

A complete exploration of **CMOS inverter design**, simulation, and characterization using **Sky130 PDK**.  
This lab walks through SPICE simulations, **VTC**, **transient response**, **switching threshold**, and **delay vs sizing trade-offs**.

---

## 📚 Table of Contents
1. [Objectives](#-given-objectives)
2. [SPICE Deck & Netlist](#-spice-deck)
3. [VTC Simulation (DC Sweep)](#-day3-lab-vtc-by-sweeping-input-voltage)
4. [Transient Analysis](#-transient-analyis)
5. [Static Behavior & Robustness](#-static-behavior-evaluation--cmos-inverter-robustness--switching-threshold)
6. [Analytical Vm Derivation](#-first-wl-known-values-to-approximate-the-vm)
7. [Delay vs Sizing Trade-offs](#️-cmos-delay-vs-sizing-trade-offs)
8. [References](#-reference)

---

## 🎯 Given Objectives
- Build a **CMOS inverter (PMOS + NMOS)**
- Sweep input and plot **Vout vs Vin**
- Identify the **Switching Threshold (Vm)** — the point where **Vin = Vout**

---

## ⚙️ SPICE Deck

### Connectivity Overview
- Includes both **NMOS** and **PMOS** devices with **substrate connections**
- Adds a **load capacitance (Cout = 10 pF)** (simplified assumption for static characteristics)
- Uses **equal W/L for PMOS and NMOS** for simplicity (though practically PMOS ≈ 2–3× NMOS)

<img width="1000" height="350" alt="image" src="https://github.com/user-attachments/assets/f383d2fe-7257-4d15-9635-c1e1b0197d66" />

### Netlist Representation
<img width="419" height="412" alt="image" src="https://github.com/user-attachments/assets/74729180-f0cd-41b3-ba34-76b54d57b84f" />  
<img width="419" height="412" alt="image" src="https://github.com/user-attachments/assets/afcdfa86-8df1-4411-b201-cd08cbf9eeff" />

---

## 🧪 Day3 Lab: VTC by Sweeping Input Voltage

- **Parameters:** W = 0.84 μm, L = 0.36 μm, Load = 50 fF  
- **Switching region:** around **0.88 – 0.90 V**

```spice
*Model Description
.param temp=27
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description
XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15
Cload out 0 50fF
Vdd vdd 0 1.8V
Vin in 0 1.8V

*Simulation Commands
.op
.dc Vin 0 1.8 0.01
.control
run
setplot dc1
display
.endc
.end
