# Bandgap-IP-Design-using-Sky130-technology-node
![image](https://user-images.githubusercontent.com/58599984/138215051-f7414ea3-dce7-4978-a5ab-fcb6a6ed25fe.png)
This repo contains documentation of the "VSD Open Tutorial Bandgap IP Design using Sky130 technology node".
________________________________________________________________________
# Day 1 Bandgap Design Theory
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

# BGRSK1-Day1-Theory Lec6 Start-up Circuit
## Start Up Circuit Issue
![image](https://user-images.githubusercontent.com/58599984/138257781-3c82b5b4-5bca-4198-a101-462a3c57c20f.png)

## Start Up Circuit Design
![image](https://user-images.githubusercontent.com/58599984/138257823-880e581a-920f-456b-a0ed-e14cbaaca989.png)

## BGRSK1-Day1-Theory Lec7 Complete BGR Circuit
Hence, this is the complete BGR circuit with all the blocks:
![image](https://user-images.githubusercontent.com/58599984/138258067-907c5d3e-a84a-46b2-9438-92305818e1b6.png)

_________________________________________________________________________________________________________________


# Day2 Bandgap design Labs using Sky130
## BGRSK2-Day2-Lab1 Tools and PDK Setup
### Installing Ngspice
ngspice is the open source spice simulator for electric and electronic circuits. 
ngspice offers a wealth of device models for active, passive, analog, and digital elements. Model parameters are provided by our collections, by the semiconductor device manufacturers, or from semiconductor foundries. The user adds her circuits as a netlist, and the output is one or more graphs of currents, voltages and other electrical quantities or is saved in a data file
For more details refer:</br>
http://ngspice.sourceforge.net/</br>
To install ngspice follow:</br>
https://sourceforge.net/projects/ngspice/files/ng-spice-rework/35/

### Setting up Sky130 Libraries
The SkyWater Open Source PDK is a collaboration between Google and SkyWater Technology Foundry to provide a fully open source Process Design Kit and related resources, which can be used to create manufacturable designs at SkyWater’s facility.
For more details refer:</br>
https://github.com/google/skywater-pdk</br>
https://skywater-pdk.readthedocs.io/en/latest/rules.html</br>

To setup skywater libraried follow these steps:
1. Open terminal in your working directory and run the following command:
```git clone https://github.com/google/skywater-pdk-libs-sky130_fd_pr.git```
2. Rename the folder as sky130_fd_pr (optional)
![image](https://user-images.githubusercontent.com/58599984/138348797-1b460169-b903-41f3-bec2-6a19a5a1e481.png)

### Running Magic for layout
Magic is an open source tool for layout design. For more details refer:</br>
http://opencircuitdesign.com/magic/</br>
Follow these steps to setup magic:</br>
1. Download Skywater PDK by running following commands:
 ```git clone git://opencircuitdesign.com/open_pdks
cd open_pdks
./configure --enable-sky130-pdk
make
sudo make install```
2. Install magic using following commands:
```git clone git://opencircuitdesign.com/magic
cd magic
sudo ./configure
sudo make
sudo make install
```
3. Run magic using the following command:</br>
![image](https://user-images.githubusercontent.com/58599984/138350095-60eba5f1-0c0a-46fa-a8b8-da33ac5ced17.png)

### Running netgen for netlist comparision
Netgen is a tool to compare two spice netlists. For more details refer:</br>
http://opencircuitdesign.com/netgen/</br>
To install netgen, run following in terminal:
```git clone https://github.com/RTimothyEdwards/netgen.git
./configure
make
make install
```
To compare the netlist, type **netgen** in the terminal and run this command in the tkcon window:
```
lvs <name of prelayout netlist> <name of postlayout netlist> sky130A_setup.tcl
```
For example:</br>
![image](https://user-images.githubusercontent.com/58599984/138354202-f94f3efa-69eb-4b1e-9cfc-277235ad7187.png)

## BGRSK2-Day2-Lab2 Design spec, Device data, Design Step
### Device Datasheet
![image](https://user-images.githubusercontent.com/58599984/138354969-f370e3ac-3718-43db-af2f-ed8edafcfafe.png)
For more details of the devices refer:
https://skywater-pdk.readthedocs.io/en/latest/rules/device-details.html

### Resistor
![image](https://user-images.githubusercontent.com/58599984/138355006-1044e94f-f9fd-4267-bd40-b1a027cfeb88.png)
### Circuit Design
![image](https://user-images.githubusercontent.com/58599984/138355068-a63d9003-c329-49f6-b305-218d677ff042.png)
![image](https://user-images.githubusercontent.com/58599984/138355122-8d83f2c9-00bb-4161-b667-e60d0603f27f.png)
![image](https://user-images.githubusercontent.com/58599984/138355189-4ef89b6b-45e2-41ec-80da-1225b21b568c.png)

### Bandgap Reference Circuit Design
![image](https://user-images.githubusercontent.com/58599984/138355263-e95d5a01-79f9-4755-9e46-674e89a46406.png)

## BGRSK2-Day2-Lab 3-7 Prelayout Simulation
### PTAT Simulation
#### Netlist
![image](https://user-images.githubusercontent.com/58599984/138356895-49351c64-1547-42bf-8f5f-0834ffd122b0.png)
#### Ngspice simulation
Run the following command in terminal:
```
ngspice ptat.cir
```
![image](https://user-images.githubusercontent.com/58599984/138357019-09214799-9792-4032-b885-1bde469b0c71.png)
#### Plots
![image](https://user-images.githubusercontent.com/58599984/138357165-24a84de7-8cd1-4e70-890a-97ce73de0c9f.png)
### CTAT Simulation
#### Netlist
![image](https://user-images.githubusercontent.com/58599984/138358301-a7b07e92-328a-4ce1-afbb-5b4df6bafa43.png)
#### Ngspice simulation
Run the following command in terminal:
```
ngspice ctat.cir
```
![image](https://user-images.githubusercontent.com/58599984/138358187-5580da00-a1eb-4f91-b4e6-8de66b19d724.png)
#### Plots
![image](https://user-images.githubusercontent.com/58599984/138358256-ae3ffc49-5e39-40ef-8f6f-3f242619b7dc.png)
#### For changing supply current
![image](https://user-images.githubusercontent.com/58599984/138358683-e81bce51-5214-48d7-bfb7-9eeab7d921c7.png)

### BGR using ideal Opamp Simulation
#### Netlist
![image](https://user-images.githubusercontent.com/58599984/138363392-79efb9c4-d285-4d5a-ad9f-5bc6b3d51c28.png)
![image](https://user-images.githubusercontent.com/58599984/138363416-67655224-e613-4d67-bb57-8bedd7787ee5.png)
#### Ngspice simulation
Run the following command in terminal:
```
ngspice BGR.cir
```
![image](https://user-images.githubusercontent.com/58599984/138363605-619bec34-1d5d-41cc-8327-34564e4a55af.png)
#### Plots
![image](https://user-images.githubusercontent.com/58599984/138363688-c42602e7-9742-43ba-8116-d8864cca54f4.png)
![image](https://user-images.githubusercontent.com/58599984/138363746-f3848025-5a53-4bab-9538-506e73e1bbc6.png)
![image](https://user-images.githubusercontent.com/58599984/138363870-81c7eefc-a15c-40f0-87f3-473d2a1a4be3.png)
![image](https://user-images.githubusercontent.com/58599984/138363945-b583ef6d-eb73-4b71-9715-d1463bb8db0b.png)
![image](https://user-images.githubusercontent.com/58599984/138364210-211fecb3-99f0-4fbb-bca0-2b0a9c5cc1ce.png)
![image](https://user-images.githubusercontent.com/58599984/138364309-edd2abd3-7e48-4b87-891b-1ad8fdaacd7b.png)
![image](https://user-images.githubusercontent.com/58599984/138364439-482ceda4-b419-47b9-ba32-80ad8ec372a8.png)
![image](https://user-images.githubusercontent.com/58599984/138364546-c5db630e-a2ac-4104-80c6-f64e73234963.png)
![image](https://user-images.githubusercontent.com/58599984/138364706-0da853d7-9d10-4a19-8f2a-42b45154e4eb.png)
![image](https://user-images.githubusercontent.com/58599984/138364848-e6b84a86-f444-46ef-9cd9-d52d18a8dde8.png)
![image](https://user-images.githubusercontent.com/58599984/138364886-6367965e-8b3a-4c71-87b5-f8089c0cd7bd.png)













# Acknowledgement
I would like to thank Mr. Kunal Ghosh, Mrs. Anagha Ghosh, Prof. Saroj Rout and Prof. Shantanu Sarangi for the tutorial explained in the simplest way possible. It helped me to learn more about the BandGap Reference in a very easy and structured manner. Also, the labs were very well explained. It will be very helpful for students to  learn working on Sky130 technology as well.



## References
1. VSD Open Tutorial Bandgap IP Design using Sky130 technology node
2. https://www.ti.com/power-management/linear-regulators-ldo/overview.html
3. https://github.com/google/skywater-pdk
4. https://skywater-pdk.readthedocs.io/en/latest/rules.html
5. 
