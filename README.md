# CMOS SRAM based on 0.18 um technology
6T SRAM is a type of static random-access commonly used in modern integrated circuits for storing data.It gets its name from its basic storage cell, which consists of six transistors. These six transistors are arranged in a way that allows them to store a single binary bit of data.

# Table of Content
- [About](#About)
- [Description](#Description) 
- [Design](#Design)
  - [6T-SRAM Cell](#6T-SRAM-Cell)
    -  [Read](#Read)
    -  [Write](#Write)
    -  [Hold](#Hold)
  - [Pre-Charge Circuit](#Pre-ChargeCircuit)
  - [Sense Amplifier](#sense-amplifier)
  - [Row Decoder](#Row-Decoder)
  - [Data Driver](#Data-Driver)

## About
The 6T SRAM cell is one of the most common and fundamental structures used to store a single bit of data. It consists of six transistors arranged in a way that  it can hold its state as long as power is supplied.

## Description
### Tools Used
[Cadence Virtuoso Schematic Editor :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-schematic-editor.html) Virtuoso is Cadence's flagship platform for custom IC design. It is often used for SRAM cell design and simulate custom circuitry, including SRAM bit-cells and peripheral circuitry.

[Cadence Spectre Circuit Stimulator :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-simulation/spectre-fmc-analysis.html?utm_campaign=Custom_Virtuoso_Studio_product_eu_google_search_june_2023&utm_source=google&utm_medium=search&utm_content=cdn_paid_media&utm_content=Circuit_Simulation&s_kwcid=AL!14272!3!662289232220!b!!g!!circuit%20simulation&gad=1&gclid=Cj0KCQjwpompBhDZARIsAFD_Fp8Z-SxLLihhZBFwTmCU69lX0z8FEUvoFW2uLaLdkUzkxbE_Gtb2_GUaAi4xEALw_wcB) Spectre is Cadence's analog and mixed-signal simulation tool. It is used for simulating the SRAM cell to ensure that it operates correctly under various conditions and meets performance specifications.


# Design
## 6T-SRAM Cell
<br> Transistors in a 6T SRAM cell: A 6T SRAM cell comprises two cross-coupled inverters and two access transistors for read and write operations.
Cross-Coupled Inverters: These are composed of two n-type (NMOS) and two p-type (PMOS) transistors connected in a feedback loop. They store the data bit in a      latched manner.
 Access Transistors: These are used to control the read and write operations. The access transistors connect the cross-coupled inverters to the bitlines (for       reading/writing) and wordlines (for selecting the cell).
 

    
![6TFINAL drawio](https://github.com/Subha175/SRAM/assets/123578848/2cfa00fd-bd36-421f-9592-90c35eed4ca3)

![6T_STAM](https://github.com/Subha175/SRAM/assets/123578848/2110c37b-c0a0-4f65-8847-c8f29f71fee5)

- Read :-
 <br> 1.Assume logic 0 at node (1) i.e. V1 = 0V.
 <br> 2.Therefore, M5 and M2 are OFF and M1 & M6 are ON (linear).
 <br> 3.Therefore V1 = 0V and V2 = VDD.
 <br> 4.Word line is activated and data lines CC
is pre-changed to VDD.
 <br> 5.Therefore, M3 and M4 are turned ON.
 <br> 6.Since for M4, drain and source are at same potential therefore no current flows here.
 <br> 7.But in LHS at M3 drain and source are at high differential potential therefore non-zero current flows through M3. Path  M3 >> M1 >> GND
Voltage level at BL begins to drop which results in discharging of CC
capacitor which causes V1 to increase.
 <br> 8.This is sensed by sense amplifier and amplified and read by data read circuit.
 <br> 9.Since V1 is increasing from 0V and it may turn on M2 if 
  
![Read](https://github.com/Subha175/SRAM/assets/123578848/e28dd451-9c40-4231-aad7-27a1b2e80d29)

- Write :-
   <br> 1.Assume 1 to be stored at node 1.
   <br> 2.Therefore, M1 and M6 are OFF and M2 and M5 are ON.
   <br> 3.V1 = VDD and V2 = 0V before M2 and M4 are turned ON.
   <br> 4.WL is activated; M3 and M4 are turned ON.
   <br> 5.Since V2 < VT1, V2 cannot be used to turn ON M1.
   <br> 6.We need to turn ON M1 so that path is created from V1 to GND and voltage at V1 will decrease to zero since path is pull down to GND.
   <br> 7.Therefore we turn OFF M2. V1 < VT2 to turn OFF M2. When V1 = VT,n; M3 goes in linear region and M5 in saturation region.



![write](https://github.com/Subha175/SRAM/assets/123578848/69f31245-fee0-4549-914a-cd6e39699e50)


 

## Pre-Charge Circuit 
The pre-charge circuit is responsible for setting the bitlines (BL and BLB) to a stable state before reading or writing data. In the pre-charge phase, both bitlines are set to a logic high or low level, depending on the SRAM cell's design.

![PCFINAL drawio](https://github.com/Subha175/SRAM/assets/123578848/28380285-89c0-443e-870a-033021312c4a)
![image](https://github.com/Subha175/SRAM/assets/123578848/20327be9-6d13-477f-8480-1c54bf670af3)



## Sense Amplifier 
In SRAM cells, sense amplifiers are used to amplify and sense the small voltage difference between the bitlines (BL and BLB) during read operations. Sense amplifiers play a vital role in determining the stored data within the SRAM cell.

![SAFINAL drawio](https://github.com/Subha175/SRAM/assets/123578848/864d1569-161c-414d-b71f-39e195edd017)





## Row Decoder 
A row decoder in SRAM is responsible for selecting and activating the wordline associated with a specific row of memory cells, allowing read and write operations to be performed on that row. The efficient operation of the row decoder is essential for the overall performance and power efficiency of the SRAM memory.

![ROWDECODER drawio](https://github.com/Subha175/SRAM/assets/123578848/5b6b5a15-57aa-42e4-b809-63b567d2e23e)




  





