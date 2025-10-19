# Given Objectives
- Build a CMOS inverter (PMOS + NMOS) 
- Sweep input, plot ( V{out} ) vs. ( V{in} ) 
- Identify the switching threshold ( Vm ) (point where ( V{in} = V{out} ))

## Static behavior evaluation – CMOS inverter robustness – Switching Threshold

### Let's Draw the Spice Model Load curve for Two Different W/L ratio 

- The first figure idicator (circle) is in middle of the axis whereas the other one it is shifted to right. What we Observe? Cmos is a robust-device
- We will observe the same in Day-3 Spice models. Let's Do that and later we write the observations
  
 <img width="1576" height="586" alt="image" src="https://github.com/user-attachments/assets/0dc5899e-3890-4fb5-b93b-753082333609" />

 ---
 
 **Screenshot** What we Observe? Cmos is a robust-device coz it maintain the same characteristics and therefore widely used to build any logic.
 
 <img width="1255" height="605" alt="image" src="https://github.com/user-attachments/assets/0e5f7398-fc42-456a-aa0f-e46bdfa8fb48" />

 **Screenshot** CMOS is a robust-device because of its parameter like Switching threshold.
  
<img width="1834" height="782" alt="image" src="https://github.com/user-attachments/assets/8886be61-138d-4337-a489-48d2ab02a14f" />

### observation 
- At this critical area when both are likely "ON" their is high possibility of leakage current too. But the Vm for the two different W/L is different.
- At this condition the current is equal but the direct is differnt **Vgs=Vds** or **Vin=Vout** , `Idsp=-IdsN` boundary condition.
- Want to calucalte or derive anlytic condition to observe early Vm or W/L to fetch either to achieve certain objective of (I,V)
- As we know that at this critical juncture the `Idsp= -Idsn` which means simply => `Idsp + Idsn =0` **(KCL)** Vm totally depends on these values.
- Our next analysis is we take `(1)` **W/L known values to approximate the Vm** and `(2)` **We take a Vm to approximate the ratio W/L**

``` bash
# MOSFET Current Equations
## Kirchhoff's Current Law
I_dsp + I_dsn = 0
## Drain Current Equations
### NMOS Drain Current
I_d = μn · C_ox · (W/L) · [[(V_gs - V_t) · V_dsat] - (V_dsat²/2)]
### NMOS (Body Effect) AS CMOS will have substitution of Vth for Both P and N Mos
I_dsn = k_n · [[(V_m - V_t) · V_dsatn] - (V_dsatn²/2)]
### PMOS (Body Effect)
I_dsp = k_p · [[(V_m - V_dd - V_t) · V_dsatp] - (V_dsatp²/2)]
### using KCL we will solve to evalate Vm
```

### First **W/L known values to approximate the Vm**
```
# Solving for V_m
V_m = R · V_dd / (1 + R)
Where: gain factor
R = (K_p · V_dsatp) / (K_n · V_dsatn) = [(W_p / L_p) · K_p' · V_dsatp] / [(W_n / L_n) · K_n' · V_dsatn]
```

### Conversely We derive the size of W and L of transistor from Vm

```
(W_p / L_p) / (W_n / L_n) = [K_n' · V_dsatn · [(V_m - V_t)] - (V_dsatn²/2)] / [K_p' · V_dsatp · [(-V_m + V_dd + V_t)] + (V_dsatp²/2)]
```
# ⚙️ CMOS Delay vs Sizing Trade-offs

This section will reveals design insights for **CMOS inverter sizing** — analyzing how transistor width ratios affect **rise/fall delays**, **switching threshold (Vm)**, and **overall circuit performance**.

---

## 🧮 Table 1: Delay vs Sizing Data

| **Wp/Lp** | **x·Wn/Ln** | **Rise Delay (ps)** | **Fall Delay (ps)** | **Vm (V)** |
|------------|--------------|----------------------|----------------------|-------------|
| Wp/Lp      | Wn/Ln        | 148                  | 71                   | 0.99        |
| Wp/Lp      | 2Wn/Ln       | 80                   | 76                   | 1.20        |
| Wp/Lp      | 3Wn/Ln       | 57                   | 80                   | 1.25        |
| Wp/Lp      | 4Wn/Ln       | 45                   | 84                   | 1.35        |
| Wp/Lp      | 5Wn/Ln       | 37                   | 88                   | 1.40        |

---

## ⚖️ Table 2: Comparative Observations & Design Guidelines

| **x (Wp/Lp : xWn/Ln)** | **Delay Balance** | **Vm Behavior** | **Use Case / Design Insight** |
|--------------------------|-------------------|------------------|-------------------------------|
| **1×** | Unbalanced — Fast **fall**, slow **rise** | Low (0.99 V) — favors PMOS | Smallest area, low power, suitable for **non-critical logic paths** |
| **2×** | **Balanced** — Rise ≈ Fall (80 ps ≈ 76 ps) | Mid (1.2 V ≈ Vdd/2) | Ideal for **clock buffers** (balanced delay, low jitter, minimal skew) |
| **3×** | Faster **rise**, slower **fall** | Higher (1.25 V) | Favorable when **rising edge** timing is critical |
| **4×** | Significantly faster **rise** | Higher (1.35 V) | Used for **rise-critical datapath** segments |
| **5×** | Fastest **rise**, slowest **fall** | Highest (1.4 V) | **Edge-case optimization** — large area/power penalty |

---

## 💡 Design Insight

- **x = 2** (`Wp/Lp = 2Wn/Ln`) offers the **best trade-off** between:
  - Performance (balanced rise/fall)
  - Power (moderate capacitance)
  - Area (reasonable transistor size)
- Ideal for:
  - **Clock buffers** in clock tree synthesis  
  - **Balanced logic gates** in high-speed designs  

<img width="1200" height="750" alt="image" src="https://github.com/user-attachments/assets/0ba87402-1595-4221-b09f-3905ce8546f2" />


---

## 📊 Summary of Trade-offs

| **Ratio (x)** | **Performance** | **Power/Area** | **Recommended Use** |
|----------------|------------------|----------------|----------------------|
| **1×** | Fast fall, slow rise | Lowest | Non-critical logic paths |
| **2×** | Balanced rise/fall | Moderate | Clock and balanced logic |
| **3–5×** | Fast rise, slow fall | High | Edge-critical data paths |

---

### 🧠 Key Takeaway
> The **2× sizing ratio** provides **optimal delay symmetry** and **Vm ≈ Vdd/2**, making it the most energy-efficient and timing-stable configuration for standard CMOS inverters.

---

# Reference 
- VSD Lecture
- All credits to VSD and @ Kunal Sir Lectures
- Enjoyed too much!!

