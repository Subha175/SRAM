# CMOS SRAM based on 0.18 μm technology
- Static Random Access Memory(SRAM) is a type of memory that store each bit on four transistors that form two cross coupled inverters. It retains data bits in its memory as long as power is being supplied. SRAM does not have to be periodically refreshed and it provides faster access to data compared to DRAM. The sizing of transistors in SRAM cell denotes to the alternation in transistor width to satisfy the conditions for reading and writing operations.

| ![BLOCKFIN drawio](https://github.com/Subha175/SRAM/assets/123578848/3bbc6799-6b06-4faa-a215-e9fd050b1600) | 
| :---: | 
| Fig 1: Block Diagram of SRAM |



# Table of Content
- [Introduction](#Introduction)
- [Description](#Description)
- [Specification](#Specification) 
- [SRAM Circuit](#SRAMCircuit)
  - [6T-SRAM Cell](#6T-SRAM-Cell)
    -  [Read](#Read)
    -  [Write](#Write)
    -  [Hold](#Hold)
  - [Pre-Charge Circuit](#Pre-ChargeCircuit)
  - [Sense Amplifier](#SenseAmplifier)
  - [Row Decoder](#Row-Decoder)
  - [Data Driver](#Data-Driver)
- [Schematic Design](#Schematic_Design)
- [Testbench](#Testbench)
- [Result](#Result)
  - [Process Corner Analysis](#Process_Corner_Analysis)
  - [SRAM RD/WR](#SRAM_RD/WR)
- [Conclusion](#Conclusion)
# Introduction
- SRAM (Static Random-Access Memory) is a memory component and is used in various VLSI chips due to its unique capability to retain datA. SRAM is a major data storage device due to its large storage density, less time to access and consumes less power. It does not require refreshing periodically which makes it the most popular memory cell among VLSI designers. Hence continuous workis going on for the better performance of SRAM cells.
- Each bit in SRAM is stored on two cross-coupled inverters formed by four transistors and has two stable states which are used to denote 0 and 1. Two additional access transistors serve to control a storage cell during reading and writing operations. Access to the cell is enabled by the word-line which controls the two access transistors. The cell also has two bit-lines that control both the input and output of the data from the cell. The bit-line, holds the same value that is stored in the cell and bit-line bar or bit-line not, holds the inverse of the value that is stored in the cell.



# Description
### Tools Used
- [Cadence Virtuoso Schematic Editor :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-schematic-editor.html) Virtuoso is Cadence's flagship platform for custom IC design. It is often used for SRAM cell design and simulate custom circuitry, including SRAM bit-cells and peripheral circuitry.

- [Cadence Spectre Circuit Stimulator :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-simulation/spectre-fmc-analysis.html?utm_campaign=Custom_Virtuoso_Studio_product_eu_google_search_june_2023&utm_source=google&utm_medium=search&utm_content=cdn_paid_media&utm_content=Circuit_Simulation&s_kwcid=AL!14272!3!662289232220!b!!g!!circuit%20simulation&gad=1&gclid=Cj0KCQjwpompBhDZARIsAFD_Fp8Z-SxLLihhZBFwTmCU69lX0z8FEUvoFW2uLaLdkUzkxbE_Gtb2_GUaAi4xEALw_wcB) Spectre is Cadence's analog and mixed-signal simulation tool. It is used for simulating the SRAM cell to ensure that it operates correctly under various conditions and meets performance specifications.

# Specification
- Menory Size ------------> 16-Byte
- Supply Voltage ---------> 1.8 V
- Operating Frequency ----> 50 MHz
- Power Consumption ------> 501.34μw to 887.34μw
- Operable Temperature----> -40°C to 85°C
  
# Design
## 6T-SRAM Cell
- 6T SRAM is a type of static random-access commonly used in modern integrated circuits for storing data. It gets its name from its basic storage cell, which consists of six transistors. These six transistors are arranged in a way that allows them to store a single binary bit of data.
- Transistors in a 6T SRAM cell: A 6T SRAM cell comprises two cross-coupled inverters and two access transistors for read and write operations.
- Cross-Coupled Inverters: These are composed of two n-type (NMOS) and two p-type (PMOS) transistors connected in a feedback loop. They store the data bit in a latched manner.
- Access Transistors: These are used to control the read and write operations. The access transistors connect the cross-coupled inverters to the bitlines (for reading/writing) and wordlines (for selecting the cell).
 
| ![6TOK--2 drawio](https://github.com/Subha175/SRAM/assets/123578848/31c5b188-7ac6-4825-961f-1a9fd3880c08) | 
| :---: | 
| Fig 2: 6T-SRAM Cell |
    


### Read Operation :-

| ![READCKT drawio](https://github.com/Subha175/SRAM/assets/123578848/b3f818c9-64ea-49a7-b6b3-6ade26ec437c) | 
| :---: | 
| Fig 3: Read Operation |

- Assume logic 0 at node (1) i.e. V1 = 0V (FIG.3). Hence M5 and M2 are OFF and M1 & M6 are ON.
- Therefore V1 = 0V and V2 = VDD. Word line is activated and data lines CC is pre-changed to VDD.
- When the access transistors (M3, M4) are turned on the voltage level of column BLB will not show any significant variation since no current will flow through M4 butthe node voltage of V1 will start increasing and the voltage level of column BL will begin to drop slightly i.e C is discharging through  M3 and M1 .
- If W/L ratio of access transistor M3 is large compared to the ratio of M1, the node voltage V1 may exceed the threshold voltage of M2 during this process, forcing an unintended change of the stored state. The key design issue for the data read operation is then to guararantee that the node voltage at V1 shouldn’t exceed the threshold voltage of M2 ,so that M2 remains turned off during the read phase i.e.,
  
   &emsp; **$V1_{(max)} \leq Vth_{(M2)}-------(1)$** <br>
- By taking $V_1 = 0.3$, We can find that M3 operates in saturation region while M1 operates in linear region.
  So the current equation will be ,<br>
  
  $$Id(M1) = \frac{k_{n,1}}{2} (\frac{W}{L}) \left(2(V_{GS} - V_{T,n})V_{DS} -V_{DS}^2\right)$$

  $$Id(M3) = \frac{k_{n,3}} {2} (\frac{W}{L}) (V_{GS} - V_{T,n})^2$$

 - As same current will flow through M1 and M3.<br>
 So, $Id(M3) = Id(M1)$
 - By putting the corresponding values to determine the size of the transisitors:
 $$\frac{k_{n,3}}{2}(V_{DD} - V_1 - V_{T,n})^2 =  \frac{k_{n,1}}{2}\left(2(V_{DD} - V_{T,n})V_1 - V_1^2\right)$$

 $$\frac{k_{n,3}}{k_{n,1}} = \frac{(W/L)3}{(W/L)1} \leq \frac{2(V_{DD} - V_{T,n})V_1 -V_1^2}{(V_{DD} - V_1 - V_{T,n})^2} ---------(2)$$ 
 - By putting the corresponding values of $V_{T,n} = 0.67V$ and $V_1 = 0.3V$,
 $$\frac{(W/L)_3}{(W/L)_1} \leq \frac{2(1.8 - 0.67)0.3 -0.3^2}{(1.8 - 0.67)^2}$$
 $$\frac{(W/L)_3}{(W/L)_1} \leq 0.85$$
 $${(W/L)_1} \leq 1.176{(W/L)_3}   ---------------(3)$$




![readgrapgh](https://github.com/Subha175/SRAM/assets/123578848/168a31e5-b0d0-44c0-a39e-269090946989)
| :---: | 
| Fig 3.1: Timing Diagram of Read Operation |


### Write Operation:-

| ![writeFINAL-Page-5 drawio](https://github.com/Subha175/SRAM/assets/123578848/84dfe164-9d63-4681-9f04-017a7bf7eb8b) | 
| :---: | 
| Fig 4: Write Operation |

- Now consider the write "0" operation, assuming that logic "1" is stored in the SRAM cell initially.
- Below figure shows the voltage levels in the CMOS SRAM cell at the beginning of the data-write operation.
- The transistors M1 and M6 are turned off, while the transistors M2 and M5 operate in the linear mode. Thus, the internal node voltages are V1 = VDD and V2 = 0V  before the pass transistors M3 and M4 are turned on. The column voltage VC is forced to logic "0" level by the data-write circuitry; thus, we may assume that VC  is approximately equal to 0 V.
- Once the pass transistors M3 and M4 are turned on by the row selection circuitry, we expect that the node voltage V2 remains below the threshold voltage of Ml, since M2 and M4 are designed according to condition(3). Consequently, the voltage level at node (2) would not be sufficient to turn on Ml. To change the stored information, i.e., to force V1, to 0 V and V2 to VDD, the node voltage V1, must be reduced below the threshold voltage of M2, so that M2 turns off first. When $$V_1 \leq (Vth)_M2$$ , the transistor M3 operates in the linear region while M5 operates in saturation.
- So the current equation will be ,<br>
 $$Id(M3) = \frac{k_{n,3}}{2} (\frac{W}{L}) \left(2(V_{GS} - V_{T,n})V_{DS} -V_{DS}^2\right)$$

 $$Id(M5) = \frac{k_{p,5}} {2} (\frac{W}{L}) (V_{GS} - V_{T,p})^2$$
 Since, $Id(M5) = Id(M3) -----------(1)$
 - By putting the corresponding values to determine the size of the transisitors:
 $$\frac{k_{p,5}}{2}(\frac{W}{L})(0 - V_{DD} - V_{T,p})^2 =  \frac{k_{n,3}}{2}(\frac{W}{L})\left(2(V_{DD} - V_{T,n})V_1 - V_1^2\right)$$

 $$\frac{(W/L)5}{(W/L)3} \leq \frac{μ_n {2(V_{DD} - V_{T,n})V_1 -V_1^2}}{μ_p{(V_{DD} - V_{T,p})^2}} ---------(3)$$ 
 - By putting the corresponding values of $V_{T,n} = 0.67V$ and $V_1 = 0.3V$,
 $$\frac{(W/L)_5}{(W/L)_3} \leq \frac{5 \cdot μ_p  \cdot {2(1.8 - 0.67)0.3 -0.3^2}}{μ_p {(1.8 - 0.67)^2}}$$
 $$\frac{(W/L)_5}{(W/L)_3} \leq \frac{{2(1.8 - 0.67)0.3 -0.3^2}}{5{(1.8 - 0.67)^2}}$$
 $$\frac{(W/L)_5}{(W/L)_3} \leq 2.36$$
 $${(W/L)_5} \leq 2.36{(W/L)_3}$$
 



| ![write_op](https://github.com/Subha175/SRAM/assets/123578848/b1138298-ff85-43b1-8c30-e49bc9d672b4) |
| :---: | 
| Fig 4.1: Timing Diagram of Write Operation |



 

## Pre-Charge Circuit 
- The pre-charge circuit is responsible for setting the bitlines (BL and BLB) to a stable state before reading or writing data.
- During read and write operations, SRAM cells are accessed via bitlines. By precharging we ensure that the bitlines are not left floating or in unknown state, which can lead to incorrect data  
retriveal or corruption. Here we are using  PMOS in precharge so when the PC signal is low, then the BL and BLB's capacitors will charged.

| ![PCFINALhai drawio](https://github.com/Subha175/SRAM/assets/123578848/ebb70987-8ed4-437c-9bd9-43b1b555a25e) | 
| :---: | 
| Fig 5: Pre-Charge Circuit |


| ![pcfinalgraph](https://github.com/Subha175/SRAM/assets/123578848/45bbdc84-9d67-4f50-ac7b-32b4294c9064) |
| :---: | 
| Fig 5.1: Timing Diagram of Pre-Charge Circuit |





## Sense Amplifier 
- The sense amplifier is used to sense the voltage difference between the bitlines and amplify it to drive the digital circuits. There are different types of sense amplifiers are present and used in the SRAM design depending upon the application which is typically a trade-off between area and power. In this work, an analog differential amplifier-based sense amplifier is implemented. As shown in the fig 6, during the read operation a small voltage difference between the bitlines ‘bl’ and ‘blb’ is amplified by the sense amplifier and the buffer converts the output to rail-to-rail CMOS voltage. 

- Sense Amplifier is the most critical circuits in the periphery of CMOS memory. The performance of SA’s strongly affects both memory access time, and overall memory power dissipation. CMOS memories are required to increase speed, improve capacity and maintain low power dissipation. These objectives are somewhat conflicting when it comes to sense amplifier in memories. With increased memory capacity usually comes increased bit line parasitic capacitance. This increased bit-line capacitance in turn slows down voltage sensing and makes bit-line capacitance swings energy expensive resulting in slower more energy needed memories. Due to their great importance in memory performance sense amplifiers have become a very large class of circuits. Their main function is to sense or detect stored data from a read-selected memory cell.
 
- We have designed this in such a way that current through transistor M0 and M1 are same i.e 1μA. So M1 and M2 are current mirror. Then the current across transistor M3 and M4 divided by half i.e 0.5μA across each transistor. As M5 and M6 are in series with M4 and M3 respectively so same current wil flow through them and M5 and M6 should be a current mirror.

- When both BL and BLB will precharge to VDD the node volatge at vout(fig 6) is set to 941.3 V. Whenever there is a voltage difference between BL and BLB it senses the change and give the output accordingly. 
| ![OKSAFINAL drawio](https://github.com/Subha175/SRAM/assets/123578848/759bc195-05ba-4f96-bf9a-25d45a091245) |
| :---: | 
| Fig 6: Sense Amplifier |


| ![invertersize drawio](https://github.com/Subha175/SRAM/assets/123578848/e48d5069-97e5-4eb8-9afd-48d9a18518f1) |
| :---: | 
| Sizing of Inverters |

| ![transistorsize drawio](https://github.com/Subha175/SRAM/assets/123578848/f26cacd0-34c3-4f83-a143-3c9d6d0b7647) |
| :---: | 
| Sizing of transistors in Sense-Amplifier |

| ![satb](https://github.com/Subha175/SRAM/assets/123578848/8f4fa827-02a9-4062-95ba-ed3ecc64f15b) |
| :---: | 
| Fig 6.1: Timing Digram of Sense Amplifier |






## Row Decoder 
A row decoder in SRAM is responsible for selecting and activating the wordline associated with a specific row of memory cells, allowing read and write operations to be performed on that row. The efficient operation of the row decoder is essential for the overall performance and power efficiency of the SRAM memory.

![ROWDecoderFINAL drawio](https://github.com/Subha175/SRAM/assets/123578848/447cc346-2ba8-453d-86a6-42cb292a6446)
| :---: | 
| Fig 7: Row Decoder |

## Data Driver
The driver circuit also known as a write driver is one of the basic components in the memory design circuit. The job of the driver is to bring the bit-line and bit-line bar to the ground potential which are initially being charged to maximum supply voltage VDD with pre-charge circuit. The driver gets enabled by the write enable signal. The function of the SRAM write driver is to write input data to the bit-lines when Write Enable signal is enabled; otherwise, the data is not written onto the bit-lines.

![DINdriver drawio](https://github.com/Subha175/SRAM/assets/123578848/53c93292-2c81-49f6-ab6f-6db0cc909c57)
| :---: | 
| Fig 8: Data Driver |

# Schematic Design
## SRAM
| ![insidesramtop](https://github.com/Subha175/SRAM/assets/123578848/dc52fa05-826a-44b7-a330-9cfa2f68ccd2) |
| :---: | 
| 16-byte SRAM |


## 6T_SRAM Block
| ![sram6tdesign](https://github.com/Subha175/SRAM/assets/123578848/b4d616b0-36f3-4b09-ae64-26af2abf95e3) |
| :---: | 
| 6T-SRAM Cell |


## Pre-Charge Block
| ![pcdeign](https://github.com/Subha175/SRAM/assets/123578848/29ead06a-5150-4433-b05f-881fa211302a) |
| :---: | 
| 8-bit Pre-Chrage Circuit |

## Sense-Amplifier Block
| ![senseampdesign](https://github.com/Subha175/SRAM/assets/123578848/93e12196-697f-43f6-83eb-aa56cd37c158) |
| :---: | 
| 8-bit Sense Amplifier |

## Write-Driver Block
| ![dindriverdesign](https://github.com/Subha175/SRAM/assets/123578848/f8fac4fd-2d87-4d03-b33a-1835cd580d54) |
| :---: | 
| 8-bit Write-Driver |

## RWN(Read-Write Enable)-Block
| ![rwndesign](https://github.com/Subha175/SRAM/assets/123578848/a685b321-ca9a-4fdb-92c2-8555476aa504) |
| :---: | 
| Read - Write Enable |

## Row-Decoder Block
| ![rowdecoderdesign](https://github.com/Subha175/SRAM/assets/123578848/c5b8a6d3-2369-4cc6-882e-7fc1f094c165) |
| :---: | 
| 4x16 Row Decoder |


## Testbench of SRAM
| ![testbencghoverall](https://github.com/Subha175/SRAM/assets/123578848/1cce0c78-545f-4600-ada2-5c70df668ae8) |
| :---: | 
| 16-byte SRAM testbench |


# Result

## Process Corner Analysis

- To check the performance of SRAM cell under different process corners.
- Process corners represent various manufacturing conditions that can affect the performance of integrated circuit.
- To calculate maximum Operating frequency of SRAM : Take the maximum delay of all the process corners for 1 to 0 and 0 to 1 and increase the PC signal ON time by +10%. For PC signal OFF time take the maximum time delay of Pre-charge delay of all the proccess corners and increase by +10%.

### Delays in SRAM
| ![read(0-- 1)delay](https://github.com/Subha175/SRAM/assets/123578848/c65daeef-7762-4d03-851d-3dc1c86c2403) |
| :---: | 
| Read Delay(0---->1) in SRAM |

| ![read(1---- 0)delay](https://github.com/Subha175/SRAM/assets/123578848/1fb44287-aa08-4dd3-b8ff-afceec9e6d3a) |
| :---: | 
| Read Delay(1---->0) in SRAM  |

| ![writedelaymeasure](https://github.com/Subha175/SRAM/assets/123578848/0513cb7c-43b3-4758-a76a-69d15f4a4476) |
| :---: | 
| Write Delay in SRAM  |

| ![pcdelaypicture](https://github.com/Subha175/SRAM/assets/123578848/87cf462e-8c21-498b-a390-b7c633947f49) |
| :---: | 
| Pre-Charge Delay in SRAM  |



| ![delaytable drawio](https://github.com/Subha175/SRAM/assets/123578848/44abeae2-5395-4885-bf93-cad35950bea1) |
| :---: | 
| Delays in SRAM |

| ![delaytable drawio](https://github.com/Subha175/SRAM/assets/123578848/44abeae2-5395-4885-bf93-cad35950bea1) |
| :---: | 
| Delays in SRAM |

| ![power drawio](https://github.com/Subha175/SRAM/assets/123578848/1531dbe0-e6c4-46be-9d56-424f7a54c068) |
| :---: | 
| Power Consumption in SRAM |


## Read/Write Operation

| ![FINALTABLE drawio (3)](https://github.com/Subha175/SRAM/assets/123578848/3aa86b64-6439-47dc-8b57-cdec178d6e16) |
| :---: | 
| Variables |

| ![finalllfinalll](https://github.com/Subha175/SRAM/assets/123578848/787fd61b-62c4-4046-9dea-3f206bf1e9bd) |
| :---: | 
| SRAM RD/WR |


















  





