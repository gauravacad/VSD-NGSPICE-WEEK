# Objective 
- Build a CMOS inverter (PMOS + NMOS) 
- Sweep input, plot ( V{out} ) vs. ( V{in} ) 
- Identify the switching threshold ( Vm ) (point where ( V{in} = V{out} ))

## Spice deck 
- Give a Connectivity information about the netlist including NMOS and PMOS with the substrate unlike a single Device netlist we did in part 1 spice deck.
- Cout that is load capacitance we have theory behind it How the value is derived, but to make current things simple assuming we are in static chacteristics we assume    it to 10 pf. More relative details we will read in dynamic charcteristics.
- Further we make it simple assuming same W/L for both NMOS and PMOS unlike in practics the NMOS W/L is 2-3x bigger than NMOS.

  <img width="1000" height="350" alt="image" src="https://github.com/user-attachments/assets/f383d2fe-7257-4d15-9635-c1e1b0197d66" />

---
- Lets define the Netlist


<img width="419" height="412" alt="image" src="https://github.com/user-attachments/assets/afcdfa86-8df1-4411-b201-cd08cbf9eeff" />  <img width="419" height="412"  alt="image" src="https://github.com/user-attachments/assets/74729180-f0cd-41b3-ba34-76b54d57b84f" />







  <img width="993" height="531" alt="image" src="https://github.com/user-attachments/assets/e6b0a780-b698-42d7-a4df-fb50f17d7bda" />
