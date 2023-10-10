# CMOS SRAM based on 0.18 um technology
- 6T SRAM is a type of static random-access commonly used in modern integrated circuits for storing data.It gets its name from its basic storage cell, which consists of six transistors. These six transistors are arranged in a way that allows them to store a single binary bit of data.

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

## Introduction
- SRAM (Static Random-Access Memory) is a memory component and is used in various VLSI chips due to its unique capability to retain data. This memory cell has become a subject of research to meet the demands for future digital electronics and  communication system. SRAM is a major data storage device due to its large storage density, less time to access and consumes less power. It does not require refreshing periodically which makes it the most popular memory cell among VLSI designers. Hence continuous workis going on for the better performance of SRAM cells. Each bit in SRAM is stored on two cross-coupled inverters formed by four transistors and has two stable states which are used to denote 0 and 1. Two additional access transistors serve to control a storage cell during reading and writing operations. Access to the cell is enabled by the word-line which controls the two access transistors M5 and M6. The cell also has two bit-lines that control both the input and output of the data from the cell. The bit-line, holds the same value that is stored in the cell and bit-line bar or bit-line not, holds the inverse of the value that is stored in the cell.



## Description
### Tools Used
- [Cadence Virtuoso Schematic Editor :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-schematic-editor.html) Virtuoso is Cadence's flagship platform for custom IC design. It is often used for SRAM cell design and simulate custom circuitry, including SRAM bit-cells and peripheral circuitry.

- [Cadence Spectre Circuit Stimulator :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-simulation/spectre-fmc-analysis.html?utm_campaign=Custom_Virtuoso_Studio_product_eu_google_search_june_2023&utm_source=google&utm_medium=search&utm_content=cdn_paid_media&utm_content=Circuit_Simulation&s_kwcid=AL!14272!3!662289232220!b!!g!!circuit%20simulation&gad=1&gclid=Cj0KCQjwpompBhDZARIsAFD_Fp8Z-SxLLihhZBFwTmCU69lX0z8FEUvoFW2uLaLdkUzkxbE_Gtb2_GUaAi4xEALw_wcB) Spectre is Cadence's analog and mixed-signal simulation tool. It is used for simulating the SRAM cell to ensure that it operates correctly under various conditions and meets performance specifications.


# Design
## 6T-SRAM Cell
- Transistors in a 6T SRAM cell: A 6T SRAM cell comprises two cross-coupled inverters and two access transistors for read and write operations.
- Cross-Coupled Inverters: These are composed of two n-type (NMOS) and two p-type (PMOS) transistors connected in a feedback loop. They store the data bit in a latched manner.
- Access Transistors: These are used to control the read and write operations. The access transistors connect the cross-coupled inverters to the bitlines (for reading/writing) and wordlines (for selecting the cell).
 

![6TOK--2 drawio](https://github.com/Subha175/SRAM/assets/123578848/31c5b188-7ac6-4825-961f-1a9fd3880c08)
    


### Read :-
Assume logic 0 at node (1) i.e. V1 = 0V. Therefore, M5 and M2 are OFF and M1 & M6 are ON (linear). Therefore V1 = 0V and V2 = VDD. Word line is activated and data lines CC is pre-changed to VDD.Therefore, M3 and M4 are turned ON.Since for M4, drain and source are at same potential therefore no current flows here.
But in LHS at M3 drain and source are at high differential potential therefore non-zero current flows through M3. Path  M3 >> M1 >> GND Voltage level at BL begins to drop which results in discharging of CC capacitor which causes V1 to increase.This is sensed by sense amplifier and amplified and read by data read circuit.Since V1 is increasing from 0V and it may turn on M2 if
<br> ![B7eqrW7](https://github.com/Subha175/SRAM/assets/123578848/733df1be-70b5-4e40-9171-3283b8b524a6)
<br> M3 is in saturation region and M1 is in linear region


![Read](https://github.com/Subha175/SRAM/assets/123578848/e28dd451-9c40-4231-aad7-27a1b2e80d29)

### Write :-
   <br> 1.Assume 1 to be stored at node 1.
   <br> 2.Therefore, M1 and M6 are OFF and M2 and M5 are ON.
   <br> 3.V1 = VDD and V2 = 0V before M2 and M4 are turned ON.
   <br> 4.WL is activated; M3 and M4 are turned ON.
   <br> 5.Since V2 < VT1, V2 cannot be used to turn ON M1.
   <br> 6.We need to turn ON M1 so that path is created from V1 to GND and voltage at V1 will decrease to zero since path is pull down to GND.
   <br> 7.Therefore we turn OFF M2. V1 < VT2 to turn OFF M2. When V1 = VT,n; M3 goes in linear region and M5 in saturation region.



![write](https://github.com/Subha175/SRAM/assets/123578848/69f31245-fee0-4549-914a-cd6e39699e50)
![write_op](https://github.com/Subha175/SRAM/assets/123578848/b1138298-ff85-43b1-8c30-e49bc9d672b4)



 

## Pre-Charge Circuit 
The pre-charge circuit is responsible for setting the bitlines (BL and BLB) to a stable state before reading or writing data. In the pre-charge phase, both bitlines are set to a logic high or low level, depending on the SRAM cell's design.

![PCFINALhai drawio](https://github.com/Subha175/SRAM/assets/123578848/ebb70987-8ed4-437c-9bd9-43b1b555a25e)
![image](https://github.com/Subha175/SRAM/assets/123578848/20327be9-6d13-477f-8480-1c54bf670af3)



## Sense Amplifier 
In SRAM cells, sense amplifiers are used to amplify and sense the small voltage difference between the bitlines (BL and BLB) during read operations. Sense amplifiers play a vital role in determining the stored data within the SRAM cell.

![salast drawio](https://github.com/Subha175/SRAM/assets/123578848/3c9fb618-9602-4416-959d-4b3469c3d711)

## Row Decoder 
A row decoder in SRAM is responsible for selecting and activating the wordline associated with a specific row of memory cells, allowing read and write operations to be performed on that row. The efficient operation of the row decoder is essential for the overall performance and power efficiency of the SRAM memory.

![ROWDecoderFINAL drawio](https://github.com/Subha175/SRAM/assets/123578848/447cc346-2ba8-453d-86a6-42cb292a6446)


## Data Driver
The driver circuit also known as a write driver is one of the basic components in the memory design circuit. The job of the driver is to bring the bit-line and bit-line bar to the ground potential which are initially being charged to maximum supply voltage VDD with pre-charge circuit. The driver gets enabled by the write enable signal. The function of the SRAM write driver is to write input data to the bit-lines when Write Enable signal is enabled; otherwise, the data is not written onto the bit-lines.
![DINdriver drawio](https://github.com/Subha175/SRAM/assets/123578848/53c93292-2c81-49f6-ab6f-6db0cc909c57)









  





