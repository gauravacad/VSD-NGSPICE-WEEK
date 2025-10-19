# Week 4 Part I objective
- Simulate an NMOS device, sweeping (Vds) for different (Vgs), to observe linear and saturation regions 
- Plot ( Id) vs. (Vds) curves

## Need of spice simulation 
Example of buffer with some values of output loads in femto farad (fF).

**Screenshot:** The example delay table for a Buffer 

<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/7a75921b-d91a-4975-a03d-8caf37159f0a" />

---

**Screenshot:** The table used to extract the delay value based on input slew i.e. 40 ps and assumed total cap at node A of a Buffer as 60 fF.

<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/9ce85898-3606-489c-b998-701aa914c63a" />

---
- Though the value are not taken exactly from row 2 and column 3-4. hence the exact delay is not available.
- So, we don’t need to run the spice simulation, as we have delay table that taking Input slew vs output load with the drive strengths / W/L ratios levels.
- 
### Some requirement of Spice simulation based on typical questions 
- What is the source of table, How the characterization is done and these number are coming from and are different?
- Are these delay models are accurate coz they are going in our chip circuit design and therefore we need to do the matching in simulaton?
- What ever we are doing in STA can be trusted or not? So need spice to verify?
- So it involves characterization of N-P mos transistor and derive the I and vds of transistor and delay of these N or P mos when connected in different fasions.
- 
### Circuit design and Spice Simulation 
- `Circuit design` : We try to understand that what king of N or P Mos transistor are connected in certain fasion resulting in a different Logic e.g. `And gate` etc.
- `Spice Simulation`: The above particlaur circuit posses certain characteristics i.e. NMos or PMos which actually decide the delay and decides W/L ratio and thereby drain current and the Vout-Vin curve.

**Ans** is `Spice Simulation`

## Basic Element of Circuit design 

**Screenshot:** The Basic NMos strucutre and PMos is just invert of it.

<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/47d0faf2-b430-49a0-979b-bab369a0ece0" />

---
### Thershold voltage 
- We first ground all the terminals and what we extract are PN juncition behaviour back to back connected
- Nothing is `ON`, Channel has high resistance , no conduction and this is called Source

 **Screenshot:** The Basic NMos strucutre and PMos is just invert of it.
 
 <img width="570" height="350" alt="image" src="https://github.com/user-attachments/assets/51471fcc-5d9c-40d6-8300-d7d3d24932d3" />

---

- Now we will apply small potential at the Gate, this essentially menas that all the ploysilicon area forms capacitor with +ve charge.

**Screenshot:** The Basic NMos strucutre and PMos is just invert of it.                                                                           

<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/fa878ef1-fd34-432f-ad81-fd89712268e4" />    </br>    

- Majority and Minority charges will be seen. Positive charged is pushed leaving behing the electron accumulation (-ve).
  
<img width="540" height="340" alt="image" src="https://github.com/user-attachments/assets/a91a905f-493b-4d04-8ccd-47f34540a0a8" />

- More and More gate potential will form a depletion region or a conduction channel between source and Drain.
- Formaltaion of delpetion region , means it has depleted its majority charge carrier due to reverse bias.
- The depletion region is similar to Pn junction
- Increase the gate voltage more and more positive charge particles get depleted and higher the thickness of depletion layer. At a certain point we observe a Inversion
- **Inversion** : `Gate Volate` at which `strong Inversion` happens is called `Threshold Voltage`. There are parameters on Which the `Threshold voltage` depends and that is used as model for Spice simulation.
 
<img width="330" height="320" alt="image" src="https://github.com/user-attachments/assets/5a97a1fd-766e-4d65-a573-4ade8305db2b" />

---

- After certain we don't have majority carrier and then What will happen?
- The gate potential forms a strong magnet and it will attract from nearby area heavily doped `n+` source region.
- It increase the channel width. The gap is covered with  between source to Drain which was initally had High resistance.
- Positive V-SB (Source to Body) Additional reverse Bias to this Pn will additional increase the channel width.
- Here, we observe in the figure that due to +Vsb few -ve charges are pulled from channel towards source `S` area.
- Logically, what will go wrong ? As a result of that Vbs there is slant surface inversion.
- This define a Vto (when Vbs=0) surface inverion happened when Vbs =0.

<img width="330" height="320" alt="image" src="https://github.com/user-attachments/assets/8660c0c3-7b10-4f3d-b06e-17bdc16a273b" />




---

## Term V(x) gate-to-channel Voltage

The threshold voltage (Vt) is affected by the body bias voltage (Vsb) through the body effect coefficient (γ). This relationship is crucial in MOSFET operation, especially when the source-to-body voltage is non-zero.

<img width="540" height="540" alt="image" src="https://github.com/user-attachments/assets/e506a714-0614-4168-b194-707dc1653bbc" />

---
- When Vds is present with Vgs higher than the Vthreshold. There will be inversion but here Vds will be considerable.
- Now we will calucalte the V(x) a voltage at a point 'x' along the channel as Vgs - V(x) called gate-to-channel Voltage.

<img width="540" height="450" alt="image" src="https://github.com/user-attachments/assets/e09c0e2c-6110-4a8c-9670-e85675bcb01c" />

## Drift current theory 
- channel Voltage is not constant but it is gradient.
- The charge induce int he channel is Vgx-V(x) voltage.
- Q=CV = induced charge = - Cox ([vgs - V(x)] -Vt
 ### First Order Analysis
- Charge Density Equation
```
Qi(x) ∝ -([Vgs - V(x)] - Vt)
Qi(x) = -Cox ([Vgs - V(x)] - Vt)
```
### Gate Oxide Capacitance
```
Cox = εox / tox
## Parameters
- **Cox**: Gate oxide capacitance
- **εox**: Oxide permittivity
  - = 3.97 × εo (relative permittivity)
  - = 3.5 × 10e-11 F/m
- **tox**: Oxide thickness
```
`Physical Interpretation`
The charge density Qi(x) at any point x in the channel is proportional to the difference between the gate-to-source voltage and the local channel voltage, minus the threshold voltage. This relationship is scaled by the gate oxide capacitance (Cox).
**Notes**
- The negative sign indicates that for n-channel MOSFETs, the induced charge is negative (electrons)
- Cox depends on the oxide material properties and thickness
- Thinner oxides result in higher capacitance and better gate control

### Drift and Diffusion Current 

- Diffusion current is there due to carrier concentration or charge carrier. `Like` Water Flow due to level difference. Same analogy works for carrier current.
- The Drift current is due to potential differnce that is Zero and Vds points across the depletion channel ends.
- Drift current is measures as velocity of charge carrier availabe over the channel width.

 <img width="350" height="450" alt="image" src="https://github.com/user-attachments/assets/68094cf6-f938-4a83-afaf-4c8031d256c1" />

### Drain current and Model or Equation used for Spice Engine.
- Basic Behing Spice Simulations
``` bash
Id = -Vn(x)* Qi(x)*W
Vn(x) = Mobility * Electric Field
      = μn * dV/dx
By supstituting and integration we will get the final expression as
Id = μn.Cox * (W/L) [Vgs - Vt]Vds - Vds²/2
# technology parameter = gain factor = kn=k1n *(W/L)
```
Here 
``` bash
Id= kn * [(1 - 0.45)*0.05-(0.05)²/2]
  = kn * [0.0275-`0.00125`]
    if `0.00125` = 0 for Vds <= (Vgs-Vt)
Id= kn
```
## Region of Operation
This equation is valid in the **Linear (Triode) Region** when:
```
Vds < (Vgs - Vt)
```
## Saturation Region
When `Vds ≥ (Vgs - Vt)`, the MOSFET enters saturation, and:
```
Id = (kn/2)(Vgs - Vt)²
```
## Special Cases
### 1. Small Vds (Deep Linear Region)
When `Vds << (Vgs - Vt)`, the equation simplifies to:
```
Id ≈ kn(Vgs - Vt)Vds
```
This represents a **resistive behavior** where Id is approximately linear with Vds.
### 2. Channel Resistance
```
Rch = 1 / [kn(Vgs - Vt)]
```
## Key Points
- The drain current has a quadratic dependence on Vds
- Maximum current in linear region occurs at `Vds = (Vgs - Vt)`
- The `-Vds²/2` term accounts for the non-uniform channel charge distribution
- This equation assumes long-channel behavior and neglects velocity saturation

### Thresholf Voltage Equation -> base equation for Spice Model
- As we know the Threshold Voltage Equation
```
Vt = Vto + γ(√|−2φf + Vsb| − √|−2φf|)
```
## Body Effect Coefficient (γ)
```
γ = √(2qNAεsi) / Cox

## Fermi Potential (φf)
φf = −φT · ln(NA / ni)

## Here Parameters
- **Vt**: Threshold voltage (V)
- **Vto**: Threshold voltage at Vsb = 0 (V)
- **γ** (gamma): Body effect coefficient (V^0.5)
- **φf** (phi_f): Fermi potential (V)
- **Vsb**: Source-to-body voltage (V)
- **q**: Electronic charge = 1.6 × 10⁻¹⁹ C
- **NA**: Acceptor doping concentration (cm⁻³)
- **εsi**: Permittivity of silicon
- **Cox**: Gate oxide capacitance per unit area (F/m²)
- **φT**: Thermal voltage = kT/q ≈ 26 mV at room temperature (300K)
- **NA**: Acceptor doping concentration (cm⁻³)
- **ni**: Intrinsic carrier concentration of silicon ≈ 1.5 × 10¹⁰ cm⁻³ at 300K
- **k**: Boltzmann constant = 1.38 × 10⁻²³ J/K
- **T**: Absolute temperature (K)
```
- Here the parameters better the Model to approximate the delays.
  
## Physical Interpretation

### Body Effect
The threshold voltage increases when the source-to-body voltage (Vsb) is positive (for n-channel MOSFET):
- When **Vsb = 0**: Vt = Vto (no body effect)
- When **Vsb > 0**: Vt > Vto (threshold voltage increases)
This phenomenon is called the **body effect** or **back-gate effect**.
### Fermi Potential
- φf represents the difference between the intrinsic Fermi level and the actual Fermi level in the doped substrate
- Higher doping concentration (NA) leads to larger |φf|
- The negative sign indicates this is for p-type substrate (n-channel MOSFET)
## Key Points
- The body effect coefficient γ depends on substrate doping and oxide capacitance
- Thinner gate oxide (higher Cox) reduces the body effect
- Higher substrate doping increases both γ and |φf|
- The body effect is important in circuits where source and body are not at the same potential
- This effect is particularly significant in stacked transistor configurations and analog circuits

### MOSFET Drain Current Equations
- Linear Region
```
Id = kn · [(Vgs - Vt)Vds - Vds²/2]
```
- Saturation Region
```
Id = (Kn'/2) · (W/L) · (Vgs - Vt)² [1 + λVds]
```
`We provide these model paramters called Technology parameter Viz { kn`, Vto, γ} carefully and the other file as Netlist`

<img width="250" height="290" alt="image" src="https://github.com/user-attachments/assets/13eeba38-50ed-41cd-9957-14e1b5a148f7" />

- Spice has been feed with certain Syntax , its like c/c++ language.

### Writing the Spice Syntax
- We first make a linear model and assign some typical values.
- Second define the Nodes and then write the same figure as a Spice Netlist.
 
**Screenshot:** Showing Model and assigned typical Values.
  
<img width="943" height="277" alt="image" src="https://github.com/user-attachments/assets/1f9a824c-a33d-4958-9563-3e1255427597" />

**Screenshot:** Spice Netlist generation from circuit diagram representation.

<img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/0742cae2-e7ee-46ea-a983-d384f4315603" />

### `Line-by-Line Breakdown`
```
M1 vdd n1 0 0 nmos W=1.8u L=1.2u
R1 in n1 55
Vdd vdd 0 2.5
Vin in 0 2.5
```
---

### **1. MOSFET Definition: `M1 vdd n1 0 0 nmos W=1.8u L=1.2u`**
```
M<name> <drain> <gate> <source> <bulk> <model> [W=<width>] [L=<length>]
M1 vdd n1 0 0 nmos W=1.8u L=1.2u
│  │   │  │ │  │    │       │
│  │   │  │ │  │    │       └─ Length = 1.2 microns
│  │   │  │ │  │    └───────── Width = 1.8 microns
│  │   │  │ │  └────────────── Model name (NMOS transistor)
│  │   │  │ └───────────────── Bulk/Substrate (connected to ground/0)
│  │   │  └─────────────────── Source (connected to ground/0)
│  │   └────────────────────── Gate (connected to node n1)
│  └────────────────────────── Drain (connected to vdd)
└───────────────────────────── Component name (M1)
```
### **2. Resistor Definition: `R1 in n1 55`**
```
R<name> <node1> <node2> <resistance_value>
R1 in n1 55
│  │  │  │
│  │  │  └─ Resistance value = 55 ohms
│  │  └──── Node 2 (n1)
│  └─────── Node 1 (in)
└────────── Component name (R1)
```
### **3. Supply Voltage: `Vdd vdd 0 2.5`**
```
V<name> <positive_node> <negative_node> <DC_value>
Vdd vdd 0 2.5
│   │   │  │
│   │   │  └─ Voltage value = 2.5V
│   │   └──── Negative terminal (ground/node 0)
│   └──────── Positive terminal (node vdd)
└──────────── Voltage source name (Vdd)
```
### **4. Input Voltage: `Vin in 0 2.5`**
```
Vin in 0 2.5
│   │  │  │
│   │  │  └─ Voltage value = 2.5V
│   │  └──── Negative terminal (ground/node 0)
│   └─────── Positive terminal (node in)
└─────────── Voltage source name (Vin)

``` 
| **Convention** | **Meaning** |
|----------------|-------------|
| Node 0 | Always ground reference |
| **M** prefix | MOSFET device |
| **R** prefix | Resistor |
| **V** prefix | Voltage source |
| **C** prefix | Capacitor |
| **L** prefix | Inductor |
| **Units** | u = micro (10⁻⁶), m = milli (10⁻³), p = pico (10⁻¹²) |

- Third we need the technology file and parameters e.g 130 nm comes in a package.
- `Important here` is the `technology name` of `component` must match with described in Netlist to evaluate properly.
  
<img width="399" height="291" alt="image" src="https://github.com/user-attachments/assets/0f84a63a-c767-4ebb-8921-92ee30e67d4b" />

- Lastly the `Vds` must be sweeped from `0 to typical values` and that is where **`SPICE Simulation`** will come to evaluate the `Id` for different values of `Vgs` sweeping the Vds    till `Vgs-Vt` value.

## First Simulation DC simulation to observe transistor behavior `DC sweep` and `operating point`

<img width="600" height="450" alt="image" src="https://github.com/user-attachments/assets/22ef1a36-b8a0-4a82-9d08-44b4a5cd59b9" />

- We will use to cells `nfet_018` and `pfet_018` through out the Lab experiments.
- Inside these `nfet_018` we have all the model library files describing parameters for that cell. Like `$less` `corner` spice file we have`W/L ratios` etc pre-characteised    to get proper simulation.
- Likewise in Models -> Lib.spice contains for library files for N and P fet for different PVT corners
- SPICE Netlist – Sky130 Example
- This SPICE file simulates a simple NMOS circuit using the **Sky130 PDK**.  
- It performs **DC sweep** and **operating point** analyses to observe transistor behavior.

---
## SPICE Code with Explanation
```spice
*---------------------------------------------
* Model Description
*---------------------------------------------
.param temp=27                                  ## Sets simulation temperature to 27°C
*---------------------------------------------
* Including Sky130 library files
*---------------------------------------------
.lib "sky130_fd_pr/models/sky130.lib.spice" tt  ## Loads Sky130 transistor models (typical corner)
*---------------------------------------------
* Netlist Description
*---------------------------------------------
XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=5 l=2  ## NMOS transistor: drain=Vdd, gate=n1, source=0, body=0, W=5µm, L=2µm
R1 n1 in 55                                     ## 55Ω resistor between nodes n1 and in
Vdd vdd 0 1.8V                                  ## DC supply voltage of 1.8V
Vin in 0 1.8V                                   ## Input voltage source of 1.8V
*---------------------------------------------
* Simulation Commands
*---------------------------------------------
.op                                             ## Operating point analysis
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2                 ## DC sweep: Vdd from 0→1.8 V (step 0.1 V) and Vin from 0→1.8 V (step 0.2 V)
*---------------------------------------------
* Control Section
*---------------------------------------------
.control
run
display
setplot dc1
.endc                                          ## Runs simulation and displays DC results
.end                                           ## Hault
```
**ScreenShot:** Showing the command to Runt the DC analysis of Day `ngspice <file_name>`

<img width="750" height="680" alt="image" src="https://github.com/user-attachments/assets/670a665f-99f0-4346-82e8-bc27c0b923ff" />

**ScreenShot:** `Error` in result if we Plot without `-ve sign` e.g. **`plot vdd#branch`** else we get figure (b) **`plot -vdd#branch`**

<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/2abe2621-7149-4c21-9f19-067a8f094232" />    <img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/90b2fc1b-1d1a-4831-851b-54d1333466bc" />

### Spice Simulation for lower Nodes 
- W/L is constant but the curve `XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8` **w=1.8 l=1.2** and  **w=0.375 l=0.25** all in `micron`.
- It can be clearly observe that current values in first reaching above 200 and in other it is below 140.
- That is current in saturation and adjacent curves appear different though the `W/L` = `1.5` ratio is same.
- Observation **Drain current has Quadratic dependence Vgs proven from above curves**
  
<img width="350" height="280" alt="image" src="https://github.com/user-attachments/assets/90a01b40-1259-4902-a222-c1b4c419d407" />          <img width="350" height="280" alt="image" src="https://github.com/user-attachments/assets/2161c7cf-0466-4709-b16d-861d458fc3c4" />

### Drain Current vs Voltage for Long and short channel device
- Drain current has Quadratic increases with gate voltage Vgs
- For short channel we observe short channel affects at lower nodes due to velocity saturation device (below 0.2 micron).
- **Velocity Saturation Effect** a single constant voltage by changing the file   `.dc Vdd 0 1.8 0.1 Vin 0 1.8 1.8`

**Screen Shot:** Long Channel **w=1.8 l=1.2**  vs Short channel **w=0.375 l=0.15** at constant voltage of Vgs.

 <img width="350" height="280" alt="image" src="https://github.com/user-attachments/assets/05df4290-0bd3-4b07-939c-c7f12584bf55" />
       <img width="350" height="280" alt="image" src="https://github.com/user-attachments/assets/9d446aa0-1647-48f7-9982-728321ef07cd" />
 
  
### Velocity Saturation Effect
- At lower field it is linear function and at higher field it is constatnt due to scattering effect.
- Vn(x) = mobility * electric field.
-  Case Vgt = minimum value: Cutoff region
-  Case Vds= minimum value , Lower value is resistive region of operation where our device operates. 
-  Case Vdsat = minimum = velocity saturation where short channel device works
- **Observation peak current trend is not maintained at lower nodes that is due to velocity saturation**   

## Define delay -: CMOS Voltage-Transfer Characteristics (VTC) 
-- In upcoming Sections.
