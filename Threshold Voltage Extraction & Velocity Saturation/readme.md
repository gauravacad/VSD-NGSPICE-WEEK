# Objective 
- Sweep (Vgs) vs. ( Id ) and extract threshold ( Vt ) (e.g. by linear extrapolation) 
- Observe eAects of velocity saturation in short-channel regime

## CMOS voltage transfer characteristics (VTC) 
- Naming conventions for simplicity and model design
- Complementary to each other hence CMOS.
### With few observation:
- `Vgsn = Vin-Vss(=0)` = `Vin` restricitng to Nmos discussion for our understanding and lowering the PMos complexity.
-  `Vdsn = `Vout`
-  Vgsp= `Vin-vdd`
-  Vdsp= `Vout-Vdd`
  
**Screentshot:** Showing naming convetion for study and (II) figure showing when the Nmos will be `ON`

<img width="350" height="350" alt="image" src="https://github.com/user-attachments/assets/5e1f68b5-26ae-4391-bcb5-0b43c5ce6f35" />   <img width="400" height="350" alt="image" src="https://github.com/user-attachments/assets/1aba54cd-2322-4903-bf29-892d4c504e84" />

---


<img width="350" height="280" alt="image" src="https://github.com/user-attachments/assets/0df81f13-95a6-418f-9793-9588b15017e3" />

**Screentshot:**

<img width="500" height="281" alt="image" src="https://github.com/user-attachments/assets/56cc9461-5589-417b-91d2-d61c167824b2" />


- **Observation** Current is negative due to direction in prospective/reference of NMos device.
-  Idsp= -Idsn these paremeters are enough to define the **N/Pmos IdsN  vs VdsN** curve

<img width="605" height="381" alt="image" src="https://github.com/user-attachments/assets/f9e71432-bf8c-4037-9f56-a4ff2d0ae58b" />

## Load curve and simulations 
- We will look inverter in form such that it is function of two voltages i.e. Vin and Vout and get rib of Vgs etc and try to find/modify a way such that transfer characteristic of Cmos Inverter are function of Vin and Vout will be there
- Example Static Cmos Inverter
- We assume it is long device channel and we take Vdd=2v
- First step is we will fill the tables as per Equations with IdsN current as    IdsP= -IdsN 
  
<img width="277" height="188" alt="image" src="https://github.com/user-attachments/assets/8c06a1fc-ed6f-4fb4-ab86-b04f7ab5bde6" />  <img width="281" height="187" alt="image" src="https://github.com/user-attachments/assets/ec7a1f24-12e5-4f7e-938f-519d7800eb5e" />

<img width="281" height="187" alt="image" src="https://github.com/user-attachments/assets/c8007661-8600-4992-ac79-2990a7a28711" />

## Discussion on deriving the load curves for PMOs and NMOs. 
### Overview
- This technical session focused on deriving load curves for PMOS and NMOS transistors in CMOS inverter circuits. The discussion covered the conversion of node voltages, specifically transforming VGS (gate-to-source voltage) of PMOS as a function of V, and converting VDSP as a function of output voltage. 
- Further we study the relationship where Vout equals VdsP plus VDD, demonstrating how curve shifting occurs by adding VDD to convert VdsP into output voltage function. 
- Key examples included VDSP values of negative 2 volts resulting in zero output voltage, representing completely discharged output capacitor requiring charging current. The session covered differences between analyzing PMOS independently versus within CMOS inverter context, emphasizing that NMOS analysis is simpler due to direct relationships where VGSN equals VIN and VDSN equals V out. 

**The ultimate goal is merging PMOS and NMOS load curves to derive complete CMOS voltage transfer characteristics.**
- Take the two derived load curves and merge them in the right fashion to get voltage transfer characteristics
- Remove unnecessary equations from the load curves before merging
- Complete the final step of deriving voltage transfer characteristics for the CMOS inverter

### PMOS Load Curve Derivation
The discussion began with step one completion where all node voltages were converted, specifically VGS with gate-to-source voltage of PMOS as a function of V. The next critical step involved converting VDSP as a function of output voltage since this represents the remaining voltage parameter. The process requires having output voltage, input voltage, and common drain current to derive the PMOS load curve. The conversion uses the equation V out equals VDSP plus VDD, which represents a simple shift of VDD towards the left-hand side of the curve.
### Voltage Conversion and Curve Shifting
The conversion process involves adding VDD to VDSP to transform the complete curve into output voltage function. Using specific examples, when VDSP is negative 2 volts and VDD is positive 2 volts, the resulting V out becomes zero volts. At this point with VIN at 1.5 volts, a finite current flows representing the charging current needed for the completely discharged output capacitor. When VDSP equals zero, adding VDD results in V out becoming 2 volts, showing the same current values at corresponding shifted positions.

### Output Capacitor Charging Analysis
At V out equal to zero, the output capacitor is completely discharged, requiring charging current to flow. When V out reaches 2 volts, the current becomes zero because the output capacitor is completely charged, eliminating the need for charging current. At intermediate values like V out equal to 1 volt (when VDSP is negative 1 volt), the capacitor is half-charged and requires some current for complete charging. This analysis applies specifically to PMOS in combination with NMOS forming a CMOS inverter, not as an independent device.
### NMOS Load Curve Derivation
The NMOS load curve derivation is significantly simpler than PMOS due to circuit positioning. VGSN equals V minus VSS, where VSS represents ground potential, making VGSN directly equal to V. Similarly, VDSN directly equals V out. This simplicity results from NMOS placement at the bottom of the circuit, making it equivalent to an independent NMOS with drain connected to varying V out, gate connected to varying V in, and source connected to ground. This contrasts with PMOS which has different node potentials for source and drain, making its analysis more complicated.

### Final Integration Process
The final step involves merging the two derived load curves for PMOS and NMOS to obtain voltage transfer characteristics of the CMOS inverter. Both curves now function in terms of Vin and Vout, eliminating dependencies on VGSP, VDSP, or IDSP parameters. The process requires removing unnecessary equations and merging the curves in the appropriate fashion. This integration will be demonstrated in the subsequent video session to complete the voltage transfer characteristics derivation for the CMOS inverter circuit.

