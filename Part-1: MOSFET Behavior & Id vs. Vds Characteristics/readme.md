- Simulate an NMOS device, sweeping (Vds) for diAerent (Vgs), to observe linear and saturation regions 
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

<img width="350" height="220" alt="image" src="https://github.com/user-attachments/assets/fa878ef1-fd34-432f-ad81-fd89712268e4" />

---

**Screenshot:** The Basic NMos strucutre and PMos is just invert of it.

<img width="570" height="350" alt="image" src="https://github.com/user-attachments/assets/a91a905f-493b-4d04-8ccd-47f34540a0a8" />

