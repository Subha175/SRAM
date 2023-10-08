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

# 6T-SRAM Cell
![Screenshot from 2023-10-06 15-09-14 (2)](https://github.com/Subha175/SRAM/assets/123578848/b6b991b8-07eb-4c6e-b3ef-06f04df5b324)

## About
The 6T SRAM cell is one of the most common and fundamental structures used to store a single bit of data. It consists of six transistors arranged in a way that  it can hold its state as long as power is supplied.

## Description
Transistors in a 6T SRAM cell: A 6T SRAM cell comprises two cross-coupled inverters and two access transistors for read and write operations.

Cross-Coupled Inverters: These are composed of two n-type (NMOS) and two p-type (PMOS) transistors connected in a feedback loop. They store the data bit in a latched manner.

Access Transistors: These are used to control the read and write operations. The access transistors connect the cross-coupled inverters to the bitlines (for reading/writing) and wordlines (for selecting the cell).

## Design

- 6T-SRAM Cell -
![Screenshot from 2023-10-06 15-09-14 (2)](https://github.com/Subha175/SRAM/assets/123578848/b6b991b8-07eb-4c6e-b3ef-06f04df5b324)

- Pre-Charge Circuit -
 The pre-charge circuit is responsible for setting the bitlines (BL and BLB) to a stable state before reading or writing data. In the pre-charge phase, both bitlines are set to a logic high or low level, depending on the SRAM cell's design.
![Screenshot from 2023-10-06 15-10-19 (2)](https://github.com/Subha175/SRAM/assets/123578848/6921211c-5133-4213-b052-3e8a6ecd2fad)

- Sense Amplifier -
In SRAM cells, sense amplifiers are used to amplify and sense the small voltage difference between the bitlines (BL and BLB) during read operations. Sense amplifiers play a vital role in determining the stored data within the SRAM cell.
![Screenshot from 2023-10-06 16-31-06 (2)](https://github.com/Subha175/SRAM/assets/123578848/15daa025-257a-449b-aa9e-9a894105fc0a)

- Row Decoder -
A row decoder in SRAM is responsible for selecting and activating the wordline associated with a specific row of memory cells, allowing read and write operations to be performed on that row. The efficient operation of the row decoder is essential for the overall performance and power efficiency of the SRAM memory.
![Screenshot from 2023-10-06 15-12-20 (2)](https://github.com/Subha175/SRAM/assets/123578848/04183ac3-8080-4dda-9091-da67748e78d3)



  





