# Micropower 1.23V Bandgap Reference

This is an open-source, discrete, battery-powered bandgap reference PCB design and simulation project. The schematic of the bandgap reference core is based on the classic AN-106 application note from Analog Devices, which provides a very useful collection of op-amp application circuits. Due to the vintage nature of the original design, many components used are now obsolete and difficult to find. This project is intended as a hobbyist endeavor, and the PCB is not planned for manufacturing.

The circuit schematic and PCB layout were designed using Altium Designer. Simulations were carried out in NI Multisim, where various analyses, including interactive simulation, DC sweep, transient response, temperature sweep, and parameter sweep, were conducted to validate the design performance.

![Draftsman](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Project%20Outputs/Images/Draftsman.png)

# Contents
- [Used Tools](#Used-Tools)
- [Specs](#Specs)
- [Schematic](#Schematic)
- [Layout](#Layout)
  - [3D Views](#3D-Views)
- [Simulation](#PSimulation)
- [Future Work](#Future-Work)
- [References](#References)

# Used Tools

**Altium Designer**

![Altium Logo](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Project%20Outputs/Images/Altium_Designer_Logo.png)

   - Altium Designer (AD) is a software package for printed circuit board (PCB) design and electronic design automation. It is developed by the American software company Altium Limited. Altium Designer was formerly known under the brand Protel.

  **NI Multisim**

![Multisim Logo](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Project%20Outputs/Images/Multisim.jpeg)

  - NI Multisim (formerly MultiSIM ) is an electronic schematic capture and simulation program that is part of a suite of circuit design programs bundled with NI Ultiboard. Multisim is one of the few circuit design programs that use the original Berkeley SPICE-based software simulation. Multisim was created by a company called Electronics Workbench, a division of National Instruments.
 
# Specs

<table align="center">
<tr>
    <th>Parameters</th>
    <th>Value</th>
</tr>
<tr>
    <td>Supply Voltage</td>
    <td>+3V to +30V</td>
</tr>
<tr>
    <td>Vout</td>
    <td>~1.23V</td>
</tr>
<tr>
    <td>Output Current</td>
    <td>0 to 5mA</td>
</tr>
<tr>
    <td>Quiescent Current</td>
    <td>15uA at 5V and 20uA at 10V</td>
</tr>
<tr>
    <td>Vout Temp. Coe.</td>
    <td>20ppm/°C</td>
</tr>
<tr>
    <td>Line Regulation</td>
    <td>0.01%/V</td>
</tr>
  <tr>
    <td>Load Regulation</td>
    <td>0.001%/mA</td>
</tr>
</table>

# Schematic

![Schematic](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Project%20Outputs/Images/Schematic.png?raw=true)

- The schematic consists of two blocks: the battery voltage indicator circuit and the bandgap reference. The device is powered by a 9V alkaline battery; therefore, the indicator circuit was used. Its working principle is very simple: When the device turns on, if the battery voltage is greater than 6.9V, the green LED will turn on; otherwise, the red LED will turn on.

- The bandgap core generates a stable 1.23 V output, independent of temperature, supply, and load variations. The CTAT voltage comes from the base-emitter voltage (V_BE) of one NPN transistor in the MAT01GH pair, while the PTAT voltage is derived from the ΔV_BE difference between the two matched transistors. These components are summed using an op-amp (OP-22FZ) and a feedback loop to cancel temperature effects. The 2N2222 NPN transistor sets a constant current, and the 2N2907 PNP transistor acts as a current buffer to drive the output. The 1N914 diode ensures proper startup by pre-biasing the op-amp. Precision resistors set the voltage scaling, and the trimpot allows fine-tuning of the output voltage. This design achieves excellent line/load regulation and a typical temperature coefficient of 20 ppm/°C.

# Layout

![Layout](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Project%20Outputs/Images/PCB.png?raw=true)

- The layout was designed using a 4-layer stack-up (Signal–GND–Power–Signal). Analog signals were routed with 10 mil tracks, while power and ground lines were routed with 20 mil tracks. To minimize parasitic effects, analog signal traces were routed as symmetrically as possible. The main analog section is shielded; however, I initially forgot to add stitching vias. I plan to add them and update the design files here, as they are essential to maintain a low-impedance return path and reduce EMI.

## 3D Views

**Top 3D View**

![3D View Top](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Project%20Outputs/Images/3D%20view%20top.png?raw=true)

**Bottom 3D View**

![3D View Bottom](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Project%20Outputs/Images/3D%20view%20bottom.png)

- The final PCB dimensions are 45 mm in width, 75 mm in height, and 1.85 mm in thickness. The board includes 4 mounting holes with a 3.3 mm diameter, which are suitable for standard-sized screws used in most enclosures.

# Simulation

![Interactive Simulation](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Simulation/Interactive%20simulation.png?raw=true)

- The simulation was carried out in Multisim. It is an interactive simulation that shows the actual output results of the circuit. The result is a bit different from the expectation (1.23V). Because several components, such as MAT-01GH and OP-22FZ, are not available in Multisim, I used their alternatives; as a result, the output voltage was 1.198V. But if you want to achieve the exact 1.23V, you can calibrate the resistor values and get it. 

![DC Sweep](https://github.com/TechBlueprint-V/Micropower-1.23V-Bandgap-Reference/blob/main/Simulation/DC%20sweep.png)

- This DC sweep simulation shows the bandgap reference output voltage (V<sub>OUT</sub>) versus the supply voltage (V<sub>DD</sub>) from 0 V to 30 V. The output remains highly stable across the entire input range, with a slight negative slope indicating minimal line sensitivity. The total variation is less than 5 mV over a 30 V swing, confirming excellent line regulation performance (better than 0.02%/V), which is important for precision analog applications.

- For the remaining simulations, such as transient analysis, temperature sweep, or parameter sweep, you can simply open the schematic, select the desired simulation type from the toolbar, configure the simulation parameters, and plot the results accordingly.

# Future Work
- The PCB layout will be simulated using electromagnetic (EM) simulation tools such as ANSYS HFSS or CST Studio Suite to evaluate parasitics and signal integrity. 
- A precision trimming circuit will be added to fine-tune the output voltage during production or calibration.
- ESD protection and other circuit-level protection features will be integrated to improve robustness and reliability in practical applications.

# References
- https://www.analog.com/media/en/technical-documentation/application-notes/28080533an106.pdf
- https://www.youtube.com/watch?v=Xn9LNgVKdqI&t=2s
