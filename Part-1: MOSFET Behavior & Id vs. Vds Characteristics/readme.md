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
<img width="3423" height="482" alt="image" src="https://github.com/user-attachments/assets/922a0d57-b183-473b-b94b-2dec07d39256" />

