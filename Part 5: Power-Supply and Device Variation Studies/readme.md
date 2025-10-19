# Objective Target 
- Vary supply voltage ( Vdd ) and re-plot VTCs to observe how switching threshold shifts 
- Modify transistor sizing (e.g. W/L of PMOS or NMOS) to simulate device variation, and observe affects on VTC, noise margins, delays


# 📘  Introduction to CMOS Gain, Energy, and Delay Trade-offs

- This section explores how **supply voltage, gain, and dynamic behavior** impact the performance of CMOS circuits.  
- The discussion combines theoretical insights that will later be validated through **SPICE simulations**.

---

## ⚙️ Key Concepts

- **Gain and Slope Relationship**
  - A **sharper VTC (Voltage Transfer Characteristic) slope** corresponds to a **higher gain**.
  - Higher gain improves **noise margins** and **signal integrity** in digital circuits.
  - However, extremely steep slopes can lead to **stability issues** and **slower transient response**.

- **Supply Voltage and Gain Trade-off**
  - **Lowering the supply voltage (VDD)** can sometimes **increase gain by ~50%** in analog regions.
  - This occurs because transistors operate closer to their threshold voltage.
  - However, operating near threshold may **degrade switching speed** or even **cause functional failure**.

- **Power Dissipation Dependency**
 - The **dynamic power** in CMOS is given by:

  **P = ½ × C × V² × f**

- Reducing supply voltage from **5 V to 2.5 V** results in about **96 % reduction in dynamic power** (since *P ∝ V²*).

- Example:

  **(2.5 / 5)² = 0.25 → 75 % less power per transition**
- When combined with lower switching activity, the **total energy saving can reach up to ~96%**.

- **Impact on Delay and Performance**
  - Lower VDD leads to **slower transistor switching** due to reduced drive current.
  - This increases **rise and fall times**.
  - In extreme cases, the circuit **may fail to switch completely**, causing **logic errors**.

- **Key Takeaway**
  - ⚡ *Sharper slope → Higher gain*  
  - 🔋 *Lower VDD → Lower energy consumption*  
  - 🐢 *But → Longer rise/fall times → Slower or unstable operation*

---

## 🧠 Summary Table

| Parameter            | Effect of Lower VDD | Observation                        |
|----------------------|--------------------:|------------------------------------|
| **Gain**             | ↑ ~50%             | Sharper transition slope           |
| **Energy Dissipation** | ↓ ~96%           | Lower dynamic power consumption    |
| **Delay (Rise/Fall)** | ↑                 | Slower switching                   |
| **Performance**       | ↓                 | May affect logic levels            |
| **Reliability**       | ⚠️                | May fail near threshold operation  |

---

> **Takeaway:**  
> Sharper slope gives higher gain, and lower voltage reduces energy —  
> but both can degrade switching speed and device reliability.  
> These trade-offs form the foundation of CMOS analog and digital design optimization.


### Calculating Gain Factor
- Sharper the slope higher the Gain but it has other limitations we will study in Lab
- Lower the supply can be advantageous that is incrrease of 50 % increase in gain or amplification for analog designs
- About energy consumption say operating on 5V or 2.5 , so powerdissipation = 1/2 cv^2
- The capacitance the inverter want to charge at 2.5 V and 0.5 V so the values will be 96% reduction but have limitations.
- Thought the factor of improvement in gain about 50% and energy reduction about 96% but the rise or fall delay will be worst than earlier.
- Take away point is Sharper the slope the lower the rise and fall time to charge the capacitor and impact on the performance , may the device even wont  work.
- So higher gain and lesser energy but it take longer time to operate or may not operate that is basic discussion topic of this part.
- lets have spice simulations and observe these phenomenons in details.
- though we need more study on dynamic behaviour of CMOS:- device variations and its behaviour.
- 
  ### LAB day 5: varioation of supply voltage and behavious of CMOS

```bash
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
.control
let powersupply = 1.8
alter Vdd = powersupply
	let voltagesupplyvariation = 0
	dowhile voltagesupplyvariation < 6
	dc Vin 0 1.8 0.01
	let powersupply = powersupply - 0.2
	alter Vdd = powersupply
	let voltagesupplyvariation = voltagesupplyvariation + 1
end
plot dc1.out vs in dc2.out vs in dc3.out vs in dc4.out vs in dc5.out vs in dc6.out vs in xlabel "input voltage(V)" ylabel "output voltage(V)" title "Inveter dc characteristics as a function of supply voltage"
.endc
.end
```

**Screenshot:** Plotting the graph with varying supply voltage 


<img width="705" height="592" alt="Image" src="https://github.com/user-attachments/assets/32a92e02-b24c-4499-a121-87228ff3e040" />



**Screenshot:** To find the gain we need to take ratio of two points where the graph is changing as marked yellow line.
-  Gain = X02 -X01 / Y02- Y01 

<img width="705" height="592" alt="Image" src="https://github.com/user-attachments/assets/7746280f-56ad-4d7a-8b91-18523fac8a1c" />




<img width="705" height="592" alt="image" src="https://github.com/user-attachments/assets/81c8d556-0b5d-46ef-a93d-fdd1933575ae" />


## 🔬 Next Steps: SPICE Simulation Studies

To validate these concepts, SPICE simulations will be conducted to observe:

- Voltage Transfer Characteristics (VTC) for various supply voltages  
- Gain calculation from VTC slope  
- Delay variation with different VDD values  
- Dynamic power estimation from switching activity  

---

## 📚 Further Study Topics

- **Dynamic behavior of CMOS** under:
  - Device parameter variations  
  - Process, Voltage, and Temperature (PVT) fluctuations  
  - Short-channel and leakage effects in deep submicron technologies  


### Etching Process variations 
- Device Variation Sources Introduction
- Etching process identified as primary fabrication-related variation source
- Etching defines transistor structure dimensions including width and height
- Process variations directly impact cell delay and performance characteristics
- CMOS inverter robustness testing planned against device parameter variations

### Oxidation variation and device variation 
