# CMOS SRAM based on 0.18 um technology
6T SRAM is a type of static random-access commonly used in modern integrated circuits for storing data.It gets its name from its basic storage cell, which consists of six transistors. These six transistors are arranged in a way that allows them to store a single binary but of data.

# Table of Content
- [About](#section-1)
- [Description](#section-2) 
- [Design](#section-2)
  - [Pre-Charge Circuit](#subsection-1-1)
  - [Sense Amplifier](#subsection-1-2)
  - [Row Decoder](#subsection-1-3)
  - [Data Driver](#subsection-1-4)

## About
The 6T SRAM cell is one of the most common and fundamental structures used to store a single bit of data. It consists of six transistors arranged in a way that  it can hold its state as long as power is supplied.

## Description
### Tools Used
[Cadence Virtuoso Schematic Editor :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-schematic-editor.html) Virtuoso is Cadence's flagship platform for custom IC design. It is often used for SRAM cell design and simulate custom circuitry, including SRAM bit-cells and peripheral circuitry.

[Cadence Spectre Circuit Stimulator :](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-simulation/spectre-fmc-analysis.html?utm_campaign=Custom_Virtuoso_Studio_product_eu_google_search_june_2023&utm_source=google&utm_medium=search&utm_content=cdn_paid_media&utm_content=Circuit_Simulation&s_kwcid=AL!14272!3!662289232220!b!!g!!circuit%20simulation&gad=1&gclid=Cj0KCQjwpompBhDZARIsAFD_Fp8Z-SxLLihhZBFwTmCU69lX0z8FEUvoFW2uLaLdkUzkxbE_Gtb2_GUaAi4xEALw_wcB) Spectre is Cadence's analog and mixed-signal simulation tool. It is used for simulating the SRAM cell to ensure that it operates correctly under various conditions and meets performance specifications.


## Design
- 6T-SRAM Cell -
Transistors in a 6T SRAM cell: A 6T SRAM cell comprises two cross-coupled inverters and two access transistors for read and write operations.

Cross-Coupled Inverters: These are composed of two n-type (NMOS) and two p-type (PMOS) transistors connected in a feedback loop. They store the data bit in a latched manner.

Access Transistors: These are used to control the read and write operations. The access transistors connect the cross-coupled inverters to the bitlines (for reading/writing) and wordlines (for selecting the cell).

![6T_STAM](https://github.com/Subha175/SRAM/assets/123578848/2110c37b-c0a0-4f65-8847-c8f29f71fee5)

- Pre-Charge Circuit -
 The pre-charge circuit is responsible for setting the bitlines (BL and BLB) to a stable state before reading or writing data. In the pre-charge phase, both bitlines are set to a logic high or low level, depending on the SRAM cell's design.
![Screenshot from 2023-10-06 15-10-19 (2)](https://github.com/Subha175/SRAM/assets/123578848/6921211c-5133-4213-b052-3e8a6ecd2fad)

- Sense Amplifier -
In SRAM cells, sense amplifiers are used to amplify and sense the small voltage difference between the bitlines (BL and BLB) during read operations. Sense amplifiers play a vital role in determining the stored data within the SRAM cell.
![Screenshot from 2023-10-06 16-31-06 (2)](https://github.com/Subha175/SRAM/assets/123578848/15daa025-257a-449b-aa9e-9a894105fc0a)

- Row Decoder -
A row decoder in SRAM is responsible for selecting and activating the wordline associated with a specific row of memory cells, allowing read and write operations to be performed on that row. The efficient operation of the row decoder is essential for the overall performance and power efficiency of the SRAM memory.
![Screenshot from 2023-10-06 15-12-20 (2)](https://github.com/Subha175/SRAM/assets/123578848/04183ac3-8080-4dda-9091-da67748e78d3)



  





