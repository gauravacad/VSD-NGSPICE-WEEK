# Targeted Given Objectives to achieve
- From the VTC plot, determine ( V{IL}, V{IH}, V{OL}, V{OH} ) 
- Compute ( NML = V{IL} - V{OL} ) and ( NMH = V{OH} - V{IH} )

# Noise Margin for a basic CMOS Inverter Case:
### Overview
- This session is focused on CMOS inverter noise margin analysis. Noise margin is critical for identifying crosstalk noise and glitches that commonly occur in lower   technology nodes, which can be identified beforehand through proper noise margin evaluation. The session covered the relationship between CMOS inverter switching    thresholds and noise robustness across different inverter sizes. 
- Key voltage parameters were introduced including VIL (input low voltage around 1/4 of VDD), VIH (input high voltage around 3/4 of VDD), VOL (output low voltage),    and VOH (output high voltage). Using a 1-volt VDD example, VIL was demonstrated at 250 millivolts and VIH at 750 millivolts.
- The presentation progressed from ideal inverter characteristics with infinite slope at VDD/2 switching point to more practical scenarios with finite slopes due to   real device resistances and capacitances.
### Key Points
-Plot voltage levels (VIH, VIL, VOH, VOL) on a single voltage axis in Ngspice

### Noise Margin Introduction and Importance
Noise margin is a critical parameter related to crosstalk noise and glitches, which are typical issues in lower technology nodes. Noise margin helps identify potential problems beforehand by evaluating the robustness of logic circuits. we aim to understand how CMOS inverter switching thresholds relate to noise margin performance across different inverter sizes?

### Basic Inverter Operation and Characteristics
The fundamental inverter operation was explained where logic low input produces logic high output and vice versa. A voltage transfer characteristic graph was plotted with Vout on y-axis and Vin on x-axis, showing that when input is 0, output is VDD, and when input is high, output drops to zero. The switching occurs around VDD/2 due to PMOS and NMOS transistor behavior.

<img width="773" height="563" alt="image" src="https://github.com/user-attachments/assets/36f42c35-9930-425c-854b-538052a6c002" />

---

### Ideal vs Practical Slope Analysis
In ideal conditions, the inverter shows infinite slope at the switching point (VDD/2) because output changes from VDD to zero with no change in input voltage, creating a slope of VDD/0 = infinite. However, practical scenarios involve real resistances and capacitances in NMOS and PMOS devices, resulting in finite slopes and gradual transitions rather than instantaneous switching.

<img width="773" height="563" alt="image" src="https://github.com/user-attachments/assets/ed252b9f-11cb-4e57-a4ea-063374ed033d" />

---

### Voltage Level Definitions and Ranges
Key voltage parameters were defined: VIL represents the maximum input voltage recognized as logic 0 (approximately 1/4 of VDD or 250mV for 1V VDD), while VIH represents the minimum input voltage recognized as logic 1 (approximately 3/4 of VDD or 750mV for 1V VDD). Input voltages between 0 and VIL produce high outputs (VOH), while voltages between VIH and VDD produce low outputs (VOL).
### Practical Curve Analysis and Non-Idealities
A more realistic voltage transfer curve was presented showing curved transitions instead of straight lines due to inverter non-idealities. The curve maintains negative slope in the transition region but exhibits gradual changes rather than sharp transitions. The practical curve demonstrates how real device characteristics affect the switching behavior and create margins around the ideal switching points.
Design Constraints and Next Stage Considerations



