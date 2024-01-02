# Sharp R16 Doc

# Control Unit

## Functional Requirements

- ********************Operations********************
    1. LD
    2. STR
    3. ADC 
        1. R, R
        2. R, $123
    4. SUBB
        1. R, R
        2. R, $123
    5. INC 
    6. DEC
    7. JMPZ
        1. Address, R
        2. (Address), R
    8. JMP 
        1. $123
        2. Address, R
        3. (Address), R
    9. JMPE 
        1. $123
        2. Address, R
        3. (Address), R
    10. JMPN
        1. $123
        2. Address, R
        3. (Address), R
    11. POP
    12. PUSH
    13. RET
    14. PRNTR
    15. PRNTI
    16. HLT
    

## Instruction Cycle

- ********************************Addressing Modes********************************
    - no addressing mode
    - immediate
    - direct
    - indirect
- ****Registers****
    - Register A
    - Register B
    - Register C
    - Register D
- ******I/O Module Interface******
    - I/O module to system bus (parallel)
    - I/O module to external device
        - keypad (parallel)
        - LCD module
        - stepper motor (serial)
- ******************************Memory Module Interface******************************
- ****************Interrupt Processing Structure****************

### Machine Cycles

Each instruction is broken down into machine cycles which are in turn, broken down into micro-operations (or states). The number of machine cycles per instruction depends on how many times the CPU needs to access the system bus. Therefore, one machine cycle is defined as the sequence of instructions needed to read/write data from the system bus.

### Micro-Operations

Each micro-operation (aka. states) lasts one clock cycle long and multiple micro-operations make up one machine cycle. 

**********************Fetch Cycle**********************

*reference: William Stalling’s COA 6th edition

```jsx
t1: MAR <-- (PC)
t2: MBR <-- Memory
		PC <-- (PC) + I
t3: IR <-- (MBR)
```

The addition needed in state t2 can be calculated by the ALU in order to avoid duplicate circuitry

**Indirect Cycle**

*reference: William Stalling’s COA 6th edition

```jsx
t1: MAR <-- (IR(Address))
t2: MBR <-- Memory
t3: IR(Address) <-- (MBR(Address))
```

**Interrupt Cycle**

*reference: William Stalling’s COA 6th edition

```jsx
t1: MBR <-- (PC)
t2: MAR <-- Save_Address
		PC <-- Routine_Address
t3: Memory <-- (MBR)
```

**Execute Cycle** 

- LD
    
    ```jsx
    t1: Rx <-- Memory
    ```
    
- STR
    
    ```jsx
    t1: Memory <-- Rx
    ```
    
- 

### Keypad

**The keypad includes the following keys:** 

- A, B, C, D, E, H, I, J, L, N, O, P, R, S, T, Z,
- 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
- Execute
- Enter
- Space
- Delete
- left, right, up and down arrows

**Keypad to LCD**

- Step 1: signal is sent from keypad to its own logic
- Step 2: in logic, the signal is an address in the Character ROM and the corresponding data is read and stored in register ready to be sent to LCD
- Step 3: the data along with its other required control signals is sent to LCD driver to show character
- Step 4: an automatic spacing in the LCD module also appears before the next character can be displayed

### LCD

- 5110 Nokia datasheet: [https://datasheetspdf.com/pdf-file/1418219/Nokia/5110/1](https://datasheetspdf.com/pdf-file/1418219/Nokia/5110/1)
- Whatever key is pressed on the keypad will generate certain signals for the LCD driver so that the corresponding character will appear.

******************************Source code to LCD****************************** 

Only when the PRNTR or PRNTI opcodes are encountered will the CPU control the LCD. 

- PRINTR
    - Step 1: the CPU’s control unit takes the contents of the register and sends it to the ‘integer to character decoder’ (I might have to be make it myself)
    - Step 2: each character signal sent to the Character ROM as an address
    - Step 3: the data from that address is sent to the LCD driver along with its other required control signals to control the LCD
- PRINTI
    - Step 1: enter the required data inputs for the LCD driver to display the image/character
    - Step 2: the contents is directly sent to the LCD driver along with the control signals to display the image

### Memories

The memories in the machine are not memory mapped. All of them are implicitly addressed depending on what the machine needs to do at any given time. 

**************************Memory Banks**************************

- Main RAM
- Stack RAM
- Interrupt RAM
- Character ROM
- Assembler ROM
- Look-up table ROM for Assembler
- Program ROM

******************Registers (8-bit)******************

- General Purpose
    - 00: GP register
    - 01: GP register
    - 10: GP register
    - 11: GP register
- Special Purpose (implicit)
    - Program Counter (PC)
    - Memory Address Register (MAR)
    - Memory Buffer Register (MBR)
    - Instruction Register (IR)
    - Stack Pointer
- Flags
    - Carry Flag
    - Borrow Flag
    - Equal Flag
    - Zero Flag
- Status
    - Error
    - Overflow
    - 

### Assembler

- Example assembler from Gary Sims: [https://github.com/garyexplains/examples/blob/master/vASM.py](https://github.com/garyexplains/examples/blob/master/vASM.py)