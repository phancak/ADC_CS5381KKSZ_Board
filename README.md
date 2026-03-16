# 24-bit High-Fidelity Data Acquisition System
### High-SNR Analog Front-End & Mixed-Signal Instrumentation Platform

## 📑 Quick Access
* [**📂 View Project Schematics (PDF)**](./Schematics/ADC_CS5381KKSZ_Board_Schematics.pdf)

## 🚀 Overview
This project is a custom-designed, high-precision Analog-to-Digital Conversion (ADC) board optimized for professional audio and precision instrumentation. It utilizes a fully differential signal chain to maximize dynamic range and minimize common-mode noise, making it suitable for high-EMI environments like robotic arm control or industrial monitoring.

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
* **Tolerance:** Achieved sub-0.1mm effective electrical length matching across all high-priority analog traces.



### 3. Power Integrity & EMI Shielding
* **Copper Pours:** Utilized large 3.3V and 5V copper polygons on the top layer to minimize **IR drop** and **loop inductance**. 
* **Isolation:** Strategically distanced power pours from high-speed digital lines to prevent capacitive crosstalk. 
* **Star Grounding:** Separated AGND and DGND planes, tied at a single point, to prevent digital switching noise from the I2S clock lines from contaminating the analog front-end.

---

## 📊 Data Pipeline & Testing
Leveraging my background in **Data Integration Engineering**, I developed a verification suite for this hardware:
* **Firmware:** STM32H7 based I2S DMA driver to capture 24-bit packets without CPU overhead.
* **Analysis:** Python-based ETL pipeline to process raw binary data and generate **FFT Power Spectral Density** plots.
* **RF Optimization:** Identified and mitigated a 1.7dB insertion loss in the Bluetooth telemetry chain by analyzing parasitic pad capacitance and retuning the low-pass filter impedance.



---

## 📂 Repository Structure
* `/Hardware`: KiCad 8.0 Schematics, 4-layer PCB Layout (FR4, 1.6mm), and BOM.
* `/Firmware`: STM32H7 C-based drivers for I2S/SAI communication.
* `/Python_Tools`: Data visualization and SNR/THD+N calculation scripts.

---

## 👨‍💻 About Me
I am an Engineering Graduate from the **University of British Columbia (UBC)**. I specialize in the intersection of Embedded Systems and Data Engineering. Whether it's designing 6-DoF robotic arms or high-fidelity ADC boards, I focus on "First Principles" engineering—calculating via delays, optimizing power pours, and ensuring data integrity from the sensor to the report.

---