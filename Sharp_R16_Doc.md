# Sharp R16

## This Document

This document  provides an exhaustive description of the system, Sharp R16: from a high-level overview, down to the circuit diagrams.

## Table of Contents

   * [This Document](#this-document)
   * [1 What is Sharp R16?](#1-what-is-sharp-r16)
   * [2 Architecture](#2-architecture)
      * [2.1 User Requirements](#21-user-requirements)
      * [2.2 Instruction Format](#22-instruction-format)
      * [2.3 Data Types](#23-data-types)
      * [2.4 Addressing Modes](#24-addressing-modes)
      * [2.5 Arithmetic Operations](#25-arithmetic-operations)
   * [3 Organization](#3-organization)
      * [3.1 Specifications](#31-specifications)
      * [3.2 Overview of System Design](#32-overview-of-system-design)
      * [3.3 CPU](#33-cpu)
         * [3.3.1 Control Unit](#331-control-unit)
            * [3.3.1.1 Instruction Cycles](#3311-instruction-cycles)
            * [3.3.1.2 Machine Cycles](#3312-machine-cycles)
            * [3.3.1.3 States](#3313-states)
            * [3.3.1.4 Flags](#3314-flags)
            * [3.3.1.5 Control Signals](#3315-control-signals)
            * [3.3.1.6 Schematic](#3316-schematic)
         * [3.3.2 ALU](#332-alu)
            * [3.3.2.1 Instruction Cycles](#3321-instruction-cycles)
            * [3.3.2.2 Machine Cycles](#3322-machine-cycles)
            * [3.3.2.3 States](#3323-states)
            * [3.3.2.4 Flags](#3324-flags)
            * [3.3.2.5 Control Signals](#3325-control-signals)
            * [3.3.2.6 Schematic](#3326-schematic)
         * [3.3.2 Registers](#332-registers)
            * [3.3.2.1 Instruction Cycles](#3321-instruction-cycles-1)
            * [3.3.2.2 Machine Cycles](#3322-machine-cycles-1)
            * [3.3.2.3 States](#3323-states-1)
            * [3.3.2.4 Flags](#3324-flags-1)
            * [3.3.2.5 Control Signals](#3325-control-signals-1)
            * [3.3.2.6 Schematic](#3326-schematic-1)
      * [3.4 DMA Module](#34-dma-module)
         * [3.4.1 Registers](#341-registers)
         * [3.4.2 Control Logic](#342-control-logic)
            * [3.4.2.1 Instruction Cycles](#3421-instruction-cycles)
            * [3.4.2.2 Machine Cycles](#3422-machine-cycles)
            * [3.4.2.3 States](#3423-states)
            * [3.4.2.4 Flags](#3424-flags)
            * [3.4.2.5 Control Signals](#3425-control-signals)
            * [3.4.2.6 Schematic](#3426-schematic)
      * [3.5 I/O Module](#35-io-module)
         * [3.5.1 Registers](#351-registers)
         * [3.5.2 I/O Logic](#352-io-logic)
            * [3.5.2.1 Instruction Cycles](#3521-instruction-cycles)
            * [3.5.2.2 Machine Cycles](#3522-machine-cycles)
            * [3.5.2.3 States](#3523-states)
            * [3.5.2.4 Flags](#3524-flags)
            * [3.5.2.5 Control Signals](#3525-control-signals)
            * [3.5.2.6 Schematic](#3526-schematic)
         * [3.5.3 Peripheral Interface Logic](#353-peripheral-interface-logic)
            * [3.5.3.1 Instruction Cycles](#3531-instruction-cycles)
            * [3.5.3.2 Machine Cycles](#3532-machine-cycles)
            * [3.5.3.3 States](#3533-states)
            * [3.5.3.4 Flags](#3534-flags)
            * [3.5.3.5 Control Signals](#3535-control-signals)
            * [3.5.3.6 Schematic](#3536-schematic)
      * [3.6 Peripherals](#36-peripherals)
         * [3.6.1 LCD Module](#361-lcd-module)
            * [3.6.1.1 Relationship with Machine](#3611-relationship-with-machine)
         * [3.6.2 Keypad](#362-keypad)
            * [3.6.2.1 Relationship with Machine](#3621-relationship-with-machine)
         * [3.6.3 Robotic Arm](#363-robotic-arm)
            * [3.6.3.1 Physical Structure](#3631-physical-structure)
            * [3.6.3.2 Instructions](#3632-instructions)
            * [3.6.3.3 Schematics](#3633-schematics)


## 1 What is Sharp R16? 

Sharp R16 is a 16-bit *highly sophisticated* computer that functions mainly as a simple text editor. It is composed of the computer itself and its peripherals such as a keypad, a dotted LCD screen, and a robotic arm. The machine provides the user with a tool to write and execute programs for both the computer itself and the robotic arm using the LCD screen to view and edit the source code and the keypad to write it in. 

## 2 Architecture

Computer architecture focuses on the elements of the system that is visible to the user. That is, the information about the system that would be useful to the user. Therefore, the scope of this section follows the definition of the focus exaclty.

### User Requirements

All that the user needs from this computer is a simple yet functional text editor to write and edit their source code on for the robotic arm. Therefore, the basic functionalities that the computer must include are the following:
- a text-based user interface from which the user can view their source code
- a writing tool such as a keypad
- the ability to render all the signals sent from the keypad onto the LCD screen instantaneosly (as seen by the user)
- support for scrolling up, down, left and right within the source code
- a cursor to enable the user to see which part they are editing
- the ability to save the source code into external storage for future use.

### Byte Ordering (Endianness)

Sharp R16 implements the big endian architecture rather than the little endian. That is, the data is stored in main memory with the most significant byte first (in the lowest address of that 16 bit word). The reasons for choosing big endian over little endian are 3 fold:
- since shifting is used frequently in this machine, employing big endianness makes the organization of the computer a lot simpler
- it is easier for the user to read data stored in big endian.
- since the CPU in this machine operates on the data in 16 it words, there is no longer a distinct advantage that little endian has over big endian in regards to arithmetic operations. Therefore, there is no major overhead for the CPU when implenting big endian compared to little endian in this case. 

### Instruction Format

Each instruction is made of 16 bits. The first 4 are allocated to the 16 different opcodes, the next 2 are allocated for the 4 different addressing modes, and the last 10 bits are for the source and destination with 5 bits allocated to each field. 



### Data Types

### Addressing Modes

### ISA

**Data Transfer**
**Arithmetic**
**Logical**
**Conversion**
**I/O**
**System Control**
**Transfer of Control**



## 3 Organization

### 3.1 Specifications

### 3.2 Overview of System Design

### 3.3 CPU

#### 3.3.1 Control Unit

##### 3.3.1.1 Instruction Cycles

##### 3.3.1.2 Machine Cycles

##### 3.3.1.3 States

##### 3.3.1.4 Flags

##### 3.3.1.5 Control Signals

##### 3.3.1.6 Schematic

#### 3.3.2 ALU

##### 3.3.2.1 Instruction Cycles

##### 3.3.2.2 Machine Cycles

##### 3.3.2.3 States

##### 3.3.2.4 Flags

##### 3.3.2.5 Control Signals

##### 3.3.2.6 Schematic

#### 3.3.2 Registers

##### 3.3.2.1 Instruction Cycles

##### 3.3.2.2 Machine Cycles

##### 3.3.2.3 States

##### 3.3.2.4 Flags

##### 3.3.2.5 Control Signals

##### 3.3.2.6 Schematic

### 3.4 DMA Module

#### 3.4.1 Registers

#### 3.4.2 Control Logic

##### 3.4.2.1 Instruction Cycles

##### 3.4.2.2 Machine Cycles

##### 3.4.2.3 States

##### 3.4.2.4 Flags

##### 3.4.2.5 Control Signals

##### 3.4.2.6 Schematic

### 3.5 I/O Module

#### 3.5.1 Registers

#### 3.5.2 I/O Logic

##### 3.5.2.1 Instruction Cycles

##### 3.5.2.2 Machine Cycles

##### 3.5.2.3 States

##### 3.5.2.4 Flags

##### 3.5.2.5 Control Signals

##### 3.5.2.6 Schematic

#### 3.5.3 Peripheral Interface Logic

##### 3.5.3.1 Instruction Cycles

##### 3.5.3.2 Machine Cycles

##### 3.5.3.3 States

##### 3.5.3.4 Flags

##### 3.5.3.5 Control Signals

##### 3.5.3.6 Schematic

### 3.6 Peripherals

#### 3.6.1 LCD Module

##### 3.6.1.1 Relationship with Machine

#### 3.6.2 Keypad

##### 3.6.2.1 Relationship with Machine

#### 3.6.3 Robotic Arm

##### 3.6.3.1 Physical Structure

##### 3.6.3.2 Instructions 

##### 3.6.3.3 Schematics









