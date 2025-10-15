- Simulate an NMOS device, sweeping (Vds) for diAerent (Vgs), to observe linear and saturation regions 
-  Plot ( Id) vs. (Vds) curves

# Need of spice simulation 
Example of buffer with some values of output loads in femto farad (fF).


- We don’t need to run the spice simulation, as we have delay table that taking Input slew vs output load with the drive strengths / W/L ratios levels.
- What is the source of table, How the characterization is done and these number are coming from and are different.
- Ans is spice simulation
- Are these delay models are accurate coz they are going in our chip circuit design and therefore we need to do the matching in simulaton.
- What ever we are doing in STA can be trusted or not? So need spice to verify.
- So it involves characterization of N-P mos transistor and derive the I and vds of transistor and delay of these N or P mos when connected in different fasions.

**Screenshot:** The example delay table for a Buffer 

<img width="533" height="701" alt="image" src="https://github.com/user-attachments/assets/7a75921b-d91a-4975-a03d-8caf37159f0a" />

---

**Screenshot:** The table used to extract the delay value based on input slew i.e. 40 ps and assumed total cap at node A of a Buffer as 60 fF.
- Though the value are not taken exactly from row 2 and column 3-4. hence the exact delay is not available.

<img width="616" height="754" alt="image" src="https://github.com/user-attachments/assets/9ce85898-3606-489c-b998-701aa914c63a" />

---

