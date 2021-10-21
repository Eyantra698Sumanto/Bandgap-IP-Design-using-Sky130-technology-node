# Bandgap-IP-Design-using-Sky130-technology-node
![image](https://user-images.githubusercontent.com/58599984/138215051-f7414ea3-dce7-4978-a5ab-fcb6a6ed25fe.png)
This repo contains documentation of the "VSD Open Tutorial Bandgap IP Design using Sky130 technology node".
________________________________________________________________________
# Day 1
## Theory Lec0 Opening Lecture
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
- Because as shown in fig. above it is difficult to connect P-substrate of diode to ground hence BJT is preffered.
### Analysis of CTAT Circuit
![image](https://user-images.githubusercontent.com/58599984/138248934-1a940235-0b7e-4d7f-92be-20bdfe82fb75.png)
- Temperature coefficient = -1.88 mV/degree Kelvin
### CTAT Voltage Generation in various cases
![image](https://user-images.githubusercontent.com/58599984/138249308-7fdf5073-89a4-469c-8f93-f530ab6f1061.png)
#### Case 1: Constant current and BJT units
#### Case 2: Increasing the BJT units
#### Case 3: Increasing Current

## References
1.
2. https://www.ti.com/power-management/linear-regulators-ldo/overview.html
