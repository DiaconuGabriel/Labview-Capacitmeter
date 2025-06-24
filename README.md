
# Virtual Capacitmeter with Schmitt-Trigger Oscillator

This project details the development of a virtual capacitmeter using a 74HC14 Schmitt-Trigger inverter as an oscillator and an NI USB-6008 Data Acquisition (DAQ) board. The core of this capacitmeter is an RC oscillator circuit. An unknown capacitor (C) and a known resistor (R) determine the oscillation frequency. By measuring this frequency with the NI USB-6008, the capacitance can be calculated. This method was chosen over the charge/discharge method due to the NI USB-6008's analog input frequency limitations, which would require impractically large resistors for small capacitors.

# Hardware Design

<div align="center">

![image](https://github.com/user-attachments/assets/0236510f-4084-49c9-a664-ff0ef1ce86bb)

</div>

For the oscilator to work pins 3, 5, 9, 11, 13 need to be connected to 5V.

This circuit generates a square wave signal whose frequency is determined by the formula:

<p align="center">
  $\Large f = \frac{1}{K \cdot R \cdot C}$
</p>

K factor is from the datasheet.

The oscillator's output signal is connected to the PFI 0 digital input of the NI USB-6008 DAQ board for frequency measurement. Different resistor values are used to cover various capacitance ranges, aiming for operating frequencies between 1KHz and 10KHz.


<div align="center">

| Capactior raange | Frequency range | Resistor values |
| :-------------: | :-------------: | :-------------: |
| 10pF – 100 pF | 10KHz– 1KHz | 8.3 MΩ |
| 100pF – 1 nF | 10KHz– 1KHz | 833 KΩ |
| 1 nF – 10 nF | 10KHz– 1KHz | 83.3 KΩ |
| 10 nF – 100 nF | 10KHz– 1KHz | 8.3 KΩ |

</div>

# LabVIEW Application

The LabVIEW application handles the capacitance measurement and display. It configures the NI USB-6008 to count pulses (falling edges) on the PFI 0 channel. The frequency is then calculated by dividing the pulse count by the measurement time. Finally, the capacitance is determined using the formula:

<p align="center">
  $\Large C = \frac{K}{\text{Frequency}}$
</p>

<div align="center">

![image](https://github.com/user-attachments/assets/26623588-bea4-4881-a553-39e80bdbe5d0)

</div>

<div align="center">

![image](https://github.com/user-attachments/assets/97870850-1510-41de-82cb-c3d005045303)

</div>
