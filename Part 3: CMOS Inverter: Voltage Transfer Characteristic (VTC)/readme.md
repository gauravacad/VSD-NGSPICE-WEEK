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

<img width="419" height="412"  alt="image" src="https://github.com/user-attachments/assets/74729180-f0cd-41b3-ba34-76b54d57b84f" /> 
<img width="419" height="412" alt="image" src="https://github.com/user-attachments/assets/afcdfa86-8df1-4411-b201-cd08cbf9eeff" /> 



## Let's Draw the Spice Model Load curve for Two Different W/L ratio 

- The first figure idicator (circle) is in middle of the axis whereas the other one it is shifted to right. What we Observe?
- We will observe the same in Day-3 Spice models. Let's Do that and later we write the observations
  
 <img width="1576" height="586" alt="image" src="https://github.com/user-attachments/assets/0dc5899e-3890-4fb5-b93b-753082333609" />

### Day3 Lab: VTC by sweeping Input Voltage. Here W=0.84 micron and L is 0.36 Load as 50 fF.
- Common curve area is around 0.8 to 0.9 so we are switching area round 0.88 - 0.90.

``` bash
*Model Description
.param temp=27
*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt
*Netlist Description
XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15
Cload out 0 50fF
Vdd vdd 0 1.8V
Vin in 0 1.8V
*simulation commands
.op
.dc Vin 0 1.8 0.01
.control
run
setplot dc1
display
.endc
.end
```

**Screenshot** Figure Plot `out vs in` "Showing the VTC characteristic of CMOS"

<img width="707" height="578" alt="image" src="https://github.com/user-attachments/assets/28eafb74-3a53-4f7b-973e-bc748e19f4b0" />

---
**Screenshot** Vth around 0.87

<img width="616" height="547" alt="image" src="https://github.com/user-attachments/assets/263da8ba-e49c-4fa2-8de9-bd66d689d1bc" />

---
- By zooming we can say switching threshold for W/L ration around 0.87. We learn how to plot the switching threshold.
- For transinet analysis we will using typical corner and nfet adn Pfet ratio as same. Total time period for 4nsec.

  
- 


