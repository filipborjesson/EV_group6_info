# Adafruit LSM6DSOX (IMU)

Status: Candidate — not finalized.

Assigned member: Ian Dosani

Add datasheets and manuals to `documents/`, connection diagrams to `wiring/`, code to `firmware/`, and test procedures and results to `tests/`. Document power requirements, interfaces, proposed pins, and compatibility concerns.

## <b>Purpose and Planned Use</b>  

Tracking the Linear Acceleration and the Angular Velocity of the Car. Used to  
track the Turning, Braking, Vibration and Tilt.

## <b> Datasheet Pinout and Schematics </b>

Primary Use Guide (Contains Pinout, and Basic Use Cases, and Datasheet):  
https://cdn-learn.adafruit.com/downloads/pdf/lsm6dsox-and-ism330dhc-6-dof-imu.pdf

Official Datasheet (More in-depth on the function of the pins, and Useful info):  
https://adafru.it/HFw

Board Git (Contains the PCB board files):  
https://github.com/adafruit/Adafruit-LSM6DSOX-PCB

## <b>Supply Voltage, Signal Voltage, and Communication Protocol (I2C)</b>

### Supply Voltage:  

Max: <b>3.6V</b> (Both IO, and Supply)
Min:  
  IO: <b> 1.62 </b>
  Core: <b> 1.71 </b>  

### Signal Voltage:  

Input:  
  High: <b> 70% the IO Voltage </b>  
  Low: <b> 30% the IO Voltage </b>
  
Output:  
  High: <b>IO Voltage - 0.2V </b>  
  Low: <b>20% the IO Voltage</b>

### IO/Communication Protocol:  

The LSM6DSOX supports I3C and SPI for communication protocols.
In particular if the other components support I3C we could wire them all 
in parallel which could simplify the wiring.

## <b>Proposed Setup and Additional Hardware </b>

- Currently, I would propobe 
