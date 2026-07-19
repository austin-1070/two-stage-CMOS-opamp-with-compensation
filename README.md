<h1 align="center">Two-Stage CMOS OTA with Miller Compensation</h1>

<p align="center">
  <img src="images/schematic-with-miller.png" width="700">
</p>

## Project Overview

I completed this project to gain additional experience in analog IC design outside school. 
My goal was to design a two-stage CMOS operational transconductance amplifier using 
LTspice with the TSMC 0.18 μm CMOS model while 
also meeting a set of performance specifications.

I first used hand calculations with IC design equations to estimate 
transistor dimensions, bias currents, and the compensation network. 
The circuit was then implemented in LTspice and refined through iterative 
simulation until all design targets were achieved. During this process, I 
gained a deeper understanding of differential amplifiers, pole-zero behavior, and the 
tradeoffs involved in analog circuit design.

The design methodology presented here was developed using concepts 
from *CMOS Analog Circuit Design* by Allen and Holberg along with 
several IEEE publications on two-stage CMOS operational amplifiers. 
These references served as learning resources throughout the
project, while the circuit implementation, simulation, optimization, 
and verification were completed independently.

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
The transistor model used was ...

unCox = 
upCox = 


<img width="583" height="358" alt="image" src="https://github.com/user-attachments/assets/a725f57c-d3ee-4e3a-827c-2960c43a8946" />

The design was completed as follows:

### 1. Design Specifications

These specifications were established before beginning the hand analysis and served as benchmarks throughout the design process.

| Specification | Target |
|:--------------|-------:|
| Supply Voltage | 1.8 V |
| CMOS Technology | 0.18 μm |
| DC Gain | ≥ 60 dB |
| Gain-Bandwidth Product | ≥ 50 MHz |
| Phase Margin | ≥ 60° |
| Slew Rate | ≥ 20 V/μs |
| Input Common-Mode Range | −1.0 V to 1.6 V |
| Load Capacitance | 1 pF |
| Power Dissipation | ≤ 2 mW |

---

### 2. Compensation Network


<p align="center">
  <img width="505" height="245" alt="Screenshot 2026-07-18 003012" src="https://github.com/user-attachments/assets/7f3ea582-2877-423b-845b-e05d4abc377d" />
</p>
The compensating capacitor was calculated assuming the 
zero of the system is placed at 10 times higher the unity gain bandwidth 
(GBW). Then using the slew rate and Miller capacitor, the bias current was calculated as 20 μA.

---

### 3. Differential Input Stage (M1–M2)
<p align="center">
  <img width="505" height="255" alt="image" src="https://github.com/user-attachments/assets/89201e1d-0c95-4ff1-95aa-d36e5e71ab4a" />
</p>

From the unity-gain bandwidth and the bias current, the transconductance and drain current of M1 
was calculated. These values were then used to calculate the aspect ratio W/L of M1 as 21.363. The same aspect ratio was used for M2 in order to mirror both legs of the differential amplifier stage.

---

### 4. Current Mirror Load and Tail Current Source (M3–M5)
<p align="center">
  <img width="343" height="229" alt="image" src="https://github.com/user-attachments/assets/5f714e91-5895-4e17-b4ef-d2ce4fbaba88" />
</p>
The aspect ratio of M3 was found based off the maximum input common range. Since M3 and M4 form a 1:1 current mirror, M4 was given the same transistor dimensions.


---

### 5. Second Gain Stage (M6–M7)
<p align="center">
  <img width="699" height="270" alt="image" src="https://github.com/user-attachments/assets/c1cb9d26-6ba1-47e4-9105-1da74584709f" />
</p>
To further increase gain, M6 and M7 form a common-source amplifier that also mirrors the current from stage one.

---

### 6. Bias Network (M8)

The diode-connected reference transistor establishes the reference current of 20 uA.

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

<p align="center">
  <img src="images/bode-with-miller.png" width="700">
</p>



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
