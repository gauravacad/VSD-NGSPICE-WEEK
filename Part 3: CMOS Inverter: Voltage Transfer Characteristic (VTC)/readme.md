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

---

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
**Screenshot** Vth around 0.87 (Vin=Vout)

<img width="616" height="547" alt="image" src="https://github.com/user-attachments/assets/376d245f-4b3b-4af8-8576-6cf7c3b34390" />


---
- By zooming we can say switching threshold for W/L ration around 0.87. We learn how to plot the switching threshold.

### Transient Analyis 
- Script for transient analysis we give pulse width of 2 nsec and rise-fall time as 0.1 ns
- To calculate the rise and fall delay consider 50% of Vdd.
- Plot out vs time
  
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
*Giving Pulse with pulsewidth of 2ns and risetime and fall time as 0.2nsec period 4ns
Vin in 0 PULSE(0V 1.8V 0 0.1ns 0.1ns 2ns 4ns)
*simulation commands
.tran 1n 10n
.control
run
.endc
.end
```

<img width="707" height="628" alt="image" src="https://github.com/user-attachments/assets/3beb29eb-10e3-4e00-93a9-77268f0444f1" />

---
### To calculate the Plots of Rise and Fall consider Vdd as 0.9 and then right click on plot to extract the values 

**Screenshot** Figure Plot Rise time calcuataion observed as ~0.33ns

<img width="1365" height="553" alt="image" src="https://github.com/user-attachments/assets/1544d602-a876-46ab-a570-ff8ce31770d7" />

---

**Screenshot** Figure Plot Fall time calcuataion observed as ~0.285 ns

<img width="1318" height="552" alt="image" src="https://github.com/user-attachments/assets/463220be-3a83-43aa-889f-85564a2e92c3" />


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



