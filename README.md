# Bandgap-IP-Design-using-Sky130-technology-node
![image](https://user-images.githubusercontent.com/58599984/138215051-f7414ea3-dce7-4978-a5ab-fcb6a6ed25fe.png)
This repo contains documentation of the "VSD Open Tutorial Bandgap IP Design using Sky130 technology node".
________________________________________________________________________
# Day 1
## BGRSK1-Day1-Theory Lec0 Opening Lecture
![image](https://user-images.githubusercontent.com/58599984/138240411-597c24cf-4b01-4ed2-a6d6-7b89185598bf.png)

- Integrated Circuits need Linear rgulated voltage which are provided by LDO(Low-dropout linear regulators).
- These LDO's provide regulated voltage independent of temperature, supply voltage and the process.
- They have a temp. coeff. of 10-15ppm/ degree Celsius.
- PSRR=40-60dB
- Current to these circuits are provided by PVT(Process Voltage Temperature).
- Ways to gernerate ref. voltage:
  * Voltage Divider- Good Temp. Coeff.  but Sensitivity unity hence undesirable.
  * Forward biased pn junction- Better than Voltage Divider but still undersirable.
  * Base Emitter Voltage Referenced Circuit- Good Supply Rejection but temp. coef. needs to be improved.
  * Bandgap Reference- Best temp. coef and good sensitivity. Hence it is widely used.

## BGRSK1-Day1-Theory Lec1 Introduction to BGR
- Temperature, power supply and circuit changes independent voltage reference
- Produces constant voltage of 1.2V(close band energy gap of silicon)
- Why BGR?
  * Battery unsuitable as volatge drops with time
  * Power supply has ripple hnce unsuitable 
  * Zener diode is not used due to frequency and thermal noise constraints
  * A BGR can be integrated in bulk CMOS, bi CMOS without need for external components
  * Hence BGR is widely used
- Applications of BGR
  * LDO
  * DC to DC Buck  Converters
  * ADCs and DACs
  ![image](https://user-images.githubusercontent.com/58599984/138244144-c430e110-2a04-45a7-9daa-3195efe70a6b.png)
  ![image](https://user-images.githubusercontent.com/58599984/138244227-95bca0da-52b3-4355-953e-f3afc4a21967.png)
- BGR principle is based on complementary to absolute temperature (CTAT) and proportional to absolute temperature (PTAT)
- Types of BGR
  * Based on Architecture
    + Using Self Biased Current mirror
    + Using Operational Amplifier'
  * Based on Application
    + Low Voltage BGR
    + Low power BGR
    + High PSRR and low noise BGR
    + Curvature compensated BGR
-  Self Biased Current Mirror    
   * Advantages
       1. Simplest Topolgy
       2. Easy to design
       3. Always Stable
   * Limitations
       1. Low PSRR
       2. Cascode design to reduce PSRR
       3. Voltage head room issue
       4. Need start-up circuit
- BGR Components
  + CTAT Voltage generation Circuit
  + PTAT Voltage generation Circuit
  + Self Biased Current Mirror Circuit
  + Refernce branch Circuit
  + Start Up circuit
## BGRSK1-Day1-Theory Lec2 CTAT Voltage generation Circuit 
### CTAT Voltage Generation
![image](https://user-images.githubusercontent.com/58599984/138247274-5df9f425-209e-432e-a106-0182e4129c86.png)
- It is done in two ways:
1. Using Diode
2. Using BJT
### Why BJT is preferred na not diode
![image](https://user-images.githubusercontent.com/58599984/138248192-13df5133-67c2-4701-af1f-7fa6ca39ece9.png)
- Because as shown in fig. above it is difficult to connect P-substrate of diode to ground hence BJT is preferred.
### Analysis of CTAT Circuit
![image](https://user-images.githubusercontent.com/58599984/138248934-1a940235-0b7e-4d7f-92be-20bdfe82fb75.png)
- Temperature coefficient = -1.88 mV/degree Kelvin
### CTAT Voltage Generation in various cases
![image](https://user-images.githubusercontent.com/58599984/138249308-7fdf5073-89a4-469c-8f93-f530ab6f1061.png)
#### Case 1: Constant current and BJT units
#### Case 2: Increasing the BJT units
#### Case 3: Increasing Current

## BGRSK1-Day1-Theory Lec3 PTAT Voltage generation Circuit
### PTAT Voltage Genration Circuit
![image](https://user-images.githubusercontent.com/58599984/138253141-2bcb7aba-b725-4355-9b0e-b64330d6bce1.png)
### Characteristics of PTAT Circuit
![image](https://user-images.githubusercontent.com/58599984/138253301-955a502a-1fb4-4639-bad6-3ae4e2f75ea2.png)
<\br>
- As temperature increases, the current through Q2 shown above increases due to higher value of N. 
- As a result the slope of V1 Vs. T is more neagtive that than of V vs. T. 
- Hence the difference V-V1 increases with T.
### Design of Resistance
- Resistance value can be calculated by the formula R1=VT ln(N)/I
- For 10uA current and N=8, R1=5.4k ohms
## BGRSK1-Day1-Theory Lec4 Biased Current Mirror Circuit
### Current Mirror
#### Circuit Diagram
![image](https://user-images.githubusercontent.com/58599984/138254619-3465f988-970f-4fdd-a2cf-ccfd78eb5051.png)
#### Objective
- Independent of Supply
- Independent of Process
- Well Defined behavior with process
#### Issues
- Output current sensitive to VDD
- Solution- The circuit must bias itself

### Self Bias current mirror
#### Circuit Diagram
![image](https://user-images.githubusercontent.com/58599984/138255266-1797ed5a-15bb-4b8a-9d15-4ae601767617.png)
#### Objective
- The idea of Self bias is that Iout should be indepnedent of Iref
#### Issues
- Iout=K * Iref hence can support any amount of currnrt
- To define a current one more constraint to be added


### Self Bias current mirror with resistor

#### Circuit Diagram
![image](https://user-images.githubusercontent.com/58599984/138255965-d8783342-4832-407d-ae59-828a829b8f6e.png)
#### Advantages
- Rs defned the current uniquely
- Iout and Iref have less dependency on supply
- Loop Gain=1, hence stable
#### Limitations 
- Existence of degenerate bias point
- Start up problem

#### Summary
![image](https://user-images.githubusercontent.com/58599984/138256541-0b34736a-c218-4b02-8b18-1830b4abb6b4.png)

## BGRSK1-Day1-Theory Lec5 Reference Voltage branch Circuit
### Circuit Diagram
![image](https://user-images.githubusercontent.com/58599984/138256769-1c02bfac-4723-4f9d-b53d-7aea48e7cc44.png)
- I3 same as I1 and I2
- Voltage across C3 is CTAT type
- Voltage across R2 is PTAT type
- Vref is addition of CTAT and PTAT voltages

### Design of R2 Resistance
![image](https://user-images.githubusercontent.com/58599984/138257121-c384b9ea-7e97-4271-9331-0587bc8f207c.png)






## References
1.
2. https://www.ti.com/power-management/linear-regulators-ldo/overview.html
