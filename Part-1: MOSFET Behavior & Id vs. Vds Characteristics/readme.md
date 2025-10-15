- Simulate an NMOS device, sweeping (Vds) for different (Vgs), to observe linear and saturation regions 
-  Plot ( Id) vs. (Vds) curves

# Need of spice simulation 
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
## Some requirement of Spice simulation based on typical questions 
- What is the source of table, How the characterization is done and these number are coming from and are different.
- Are these delay models are accurate coz they are going in our chip circuit design and therefore we need to do the matching in simulaton.
- What ever we are doing in STA can be trusted or not? So need spice to verify?
- So it involves characterization of N-P mos transistor and derive the I and vds of transistor and delay of these N or P mos when connected in different fasions.
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



