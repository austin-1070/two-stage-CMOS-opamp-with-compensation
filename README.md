<h1 align="center">Two-Stage CMOS OTA with Miller Compensation</h1>

<p align="center">
  <img src="images/schematic-with-miller.png" width="700">
</p>

## Project Overview

I completed this project to gain additional experience in analog IC design outside of school. My goal was to design a two-stage CMOS operational amplifier using LTspice and the TSMC 0.18 μm CMOS process while also meeting a set of performance specifications.

I first used hand calculations with IC design equations to estimate transistor dimensions, bias currents, and the compensation network. The circuit was then implemented in LTspice and refined through iterative simulation until all design targets were achieved. During this process, I gained a much deeper understanding of differential amplifiers, current mirrors, frequency compensation, pole-zero behavior, and the tradeoffs involved in analog circuit design.

The design methodology presented here was developed using concepts from *CMOS Analog Circuit Design* by Allen and Holberg along with several IEEE publications on two-stage CMOS operational amplifiers. These references served as learning resources throughout the project, while the circuit implementation, simulation, optimization, and verification were completed independently.

## Final Results

| Parameter | Target | Measured |
|-----------|:------:|:--------:|
| Supply Voltage | ±1.8 V | ±1.8 V |
| Load Capacitance | 1 pF | 1 pF |
| DC Gain | ≥ 60 dB | **78 dB** |
| Unity-Gain Bandwidth | ≥ 50 MHz | **55 MHz** |
| Phase Margin | ≥ 60° | **61.2°** |
| Slew Rate | ≥ 20 V/µs | **36.26 V/µs** |
| Power Dissipation | ≤ 2 mW | **0.67 mW** |
| Input Common-Mode Range | Wide | **−1.8 V to +1.7 V** |

## Design Methodology
<img width="383" height="308" alt="image" src="https://github.com/user-attachments/assets/a725f57c-d3ee-4e3a-827c-2960c43a8946" />

The design was completed using the following workflow:

### 1. Design Specifications

These specifications were established before beginning the hand analysis and served as benchmarks throughout the design process.

| Specification | Target |
|:--------------|-------:|
| Supply Voltage | 1.8 V |
| CMOS Process | TSMC 0.18 μm |
| DC Gain | ≥ 60 dB |
| Gain-Bandwidth Product | ≥ 50 MHz |
| Phase Margin | ≥ 60° |
| Slew Rate | ≥ 20 V/μs |
| Input Common-Mode Range | −1.0 V to 1.6 V |
| Load Capacitance | 1 pF |
| Power Dissipation | ≤ 2 mW |


### 2. Compensation Network

The compensation capacitor was selected first based on the desired bandwidth and
load capacitance. The required slew rate was then used to determine the minimum
bias current needed to charge and discharge the Miller capacitor.


<img width="465" height="163" alt="Screenshot 2026-07-18 003012" src="https://github.com/user-attachments/assets/7f3ea582-2877-423b-845b-e05d4abc377d" />

---

### 3. Differential Input Stage (M1–M2)

The input differential pair was sized to provide the required transconductance
while maintaining saturation over the desired input common-mode range.

*(Show gm, Id, VOV, W/L calculations.)*

---

### 4. Current Mirror Load and Tail Current Source (M3–M5)

The PMOS current mirror was designed to convert the differential signal into a
single-ended output while establishing the desired bias current. The tail current
source was then sized to maintain the calculated operating point.

*(Show W/L calculations.)*

---

### 5. Second Gain Stage (M6–M7)

The second stage was sized to provide additional voltage gain and sufficient
transconductance for the desired gain-bandwidth product while driving the output
load.

*(Show calculations.)*

---

### 6. Bias Network (M8)

The diode-connected reference transistor establishes the reference current used
to bias the remaining current mirrors.

*(Show mirror ratio calculations.)*

---

### 7. Simulation and Optimization

The complete circuit was implemented in LTspice using the TSMC 0.18 μm BSIM3
model library. DC operating-point analysis was first used to verify that all
transistors remained in saturation. Device dimensions, bias currents, the Miller
compensation capacitor, and the series nulling resistor were then iteratively
adjusted until the target gain, bandwidth, phase margin, slew rate, and power
consumption were achieved.

Finally, AC, transient, DC sweep, and operating-point simulations were performed
to verify the completed design.




### 7. Final Design

Show final schematic.

One paragraph explaining the completed OTA.

## Simulation Results
    AC Response
    Slew Rate
    ICMR
    Operating Point

## Design Tradeoffs

## References

[1] P. E. Allen and D. R. Holberg, *CMOS Analog Circuit Design*, 2nd ed. Oxford University Press, 2002.

[2] M. Abdullah-Al-Kaiser and I. Jarin, "High Gain Low Offset Faster Two Stage CMOS Op-Amp and Effects of Aspect Ratios on Gain," *2017 IEEE International WIE Conference on Electrical and Computer Engineering (WIECON-ECE)*, Dehradun, India, 2017, pp. 253–256, doi:10.1109/WIECON-ECE.2017.8468913.

[3] C. L. Kavyashree, M. Hemambika, K. Dharani, A. V. Naik, and M. P. Sunil, "Design and Implementation of Two Stage CMOS Operational Amplifier Using 90 nm Technology," *2017 International Conference on Inventive Systems and Control (ICISC)*, Coimbatore, India, 2017, pp. 1–4, doi:10.1109/ICISC.2017.8068601.

[4] Y. Hao, M. Gandara, S. Mitra, S. Cochran, and B. Liu, "Design of a Two-Stage Miller-Compensated Operational Amplifier Using an EDA Tool-Centered Approach," *2024 20th International Conference on Synthesis, Modeling, Analysis and Simulation Methods and Applications to Circuit Design (SMACD)*, Volos, Greece, 2024, pp. 1–4, doi:10.1109/SMACD61181.2024.10745468.
