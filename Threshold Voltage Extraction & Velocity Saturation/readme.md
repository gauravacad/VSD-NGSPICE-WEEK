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

<img width="402" height="382" alt="image" src="https://github.com/user-attachments/assets/c8007661-8600-4992-ac79-2990a7a28711" />


