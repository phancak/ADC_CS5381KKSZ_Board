# 24-bit High-Fidelity Data Acquisition System
### High-SNR Analog Front-End & Mixed-Signal Instrumentation Platform

## 📑 Quick Access
* [**📂 View Project Schematics (PDF)**](./Schematics/ADC_CS5381KKSZ_Board_Schematics.pdf)

## 🚀 Overview
This project is a custom-designed, high-precision Analog-to-Digital Conversion (ADC) board optimized for professional audio and precision instrumentation. It utilizes a fully differential signal chain to maximize dynamic range and minimize common-mode noise, making it suitable for high-EMI environments.

## 🛠 Core Component Selection
* **ADC:** **CS5381K-KSZ** (120dB Dynamic Range, 24-bit, 192kHz sampling). A flagship Delta-Sigma converter.
* **Front-End Driver:** **ADA4940-2** Ultra-low noise, fully differential amplifier.
* **Sensors:** 2x **ICS-40730** Bottom-Port MEMS Microphones with 74dB SNR for high-definition acoustic capture.

---

## 🏗 Key Engineering Challenges & Solutions

### 1. Differential Signal Integrity
To leverage the 120dB SNR of the CS5381, I implemented a fully differential path from the amplifier to the ADC.
* **The Challenge:** Converting single-ended sensor signals while maintaining a -122dB SFDR.
* **The Solution:** Used the **ADA4940-2** to provide a stable common-mode voltage and high linearity, ensuring the ADC inputs stay within the optimal swing range.



### 2. Precision Length Matching (Via Compensation)
In high-speed mixed-signal design, phase coherency between channels is critical.
* **Via Propagation Delay:** One of my analog traces required two vias (unavoidable). To prevent phase shift, I calculated the vertical travel distance through the 1.6mm PCB stackup and compensated the "via-free" traces by adding **3.2mm of serpentine meanders**.
* **Tolerance:** Achieved sub-0.5mm effective electrical length matching across all high-priority analog traces.



### 3. Power Integrity & EMI Shielding
* **Copper Pours:** Utilized large 3.3V and 5V copper polygons on the top layer to minimize **IR drop** and **loop inductance**. 
* **Isolation:** Strategically distanced power pours from high-speed digital lines to prevent capacitive crosstalk. 
## 🏗 Grounding & Power Integrity Strategy
Unlike traditional "Split Plane" designs, this board utilizes a **Solid Ground Plane** strategy on internal layers 2 and 3 to ensure the lowest possible impedance for return currents.

* **Low-Inductance Return Paths:** By maintaining a continuous ground plane under the analog and digital sections, I minimized the loop area for high-speed I2S signals, preventing ground-bounce and radiated emissions.
* **Component Partitioning:** Rather than a physical split in the copper, I used **Spatial Isolation**. Analog components (ADA4940, CS5381 input stage) are physically grouped on one side of the board, while digital I/O and the STM32 interface are on the opposite side, ensuring digital return currents do not traverse the sensitive analog "quiet zone."
* **Layer Stackup:**
    * Layer 1: Signal / Power Pours
    * Layer 2: **GND (Solid Reference)**
    * Layer 3: **GND (Solid Reference)**
    * Layer 4: Signal / Power Pours
---

## 👨‍💻 About Me
I am an Engineering Graduate from the **University of British Columbia (UBC)**. I specialize in the intersection of Embedded Systems and Data Engineering. Whether it's designing 6-DoF robotic arms or high-fidelity ADC boards, I focus on "First Principles" engineering—calculating via delays, optimizing power pours, and ensuring data integrity from the sensor to the report.

---