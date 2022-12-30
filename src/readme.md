# API Library 

* [Mandatory Methods](#Mandatory-Methods) 
* [CallBack Functions](#CallBack-Functions) 
* [CV Manipulation](#CV-Manipulation) 
* [Class Destruction](#class-destruction) 
* [Data Types](#Data-Types) 

------------ 

# Mandatory Methods 
The following methods are **required** for the library to function properly. 

------------ 

```c 
Rcn600(CLK_pin, DATA_pin); 
``` 
Declaration of the library in which to insert the pins to which the SUSI Bus is connected. 

The CLK pin **must be** of type ***interrupt***, the data pin *can* be of any type (including analog). 

**OR** 
 
```c
Rcn600(EXTERNAL_CLOCK, DATA_pin);
``` 
Clock acquisition library declaration using **PortChangeInterrupt** 

The data pin *can* be of any type (including analog). 


------------ 

```c 
void init(void); 
``` 
***or*** 
```c 
void init(uint8_t SlaveAddress); 
``` 
**It is necessary** to invoke it in the 'setup' of the code: it starts the interrupt handling and initializes the internal counters. 

The method **without the parameter** uses, *if present*, the CVs reading method to determine the address of the module (*saved in the CV 897*), if the method *is absent* it uses the address **of defaults: 1**.

The method **with the parameter** *allows you to specify the address of the module*: **CAN HAVE VALUE**: 1, 2, 3. 

In case of a different value, the **default value will be used: 1**. 

------------ 

```c 
uint8_t process(void); 
``` 
**It is necessary to invoke it as many times as possible** in the code 'loop': decode the SUSI package. 
- Input: 
  - Nothing 
- Returns: 
  - -1 **Invalid Message** 
  - 0 No Message Queued For Decoding 
  - 1 **Valid Message** 

------------ 

# CallBack Functions
The following callback functions are **optional** (defined as 'extern' to the library), and allow the user to define the behavior to adopt in case of a particular command. 


------------ 

```c 
void notifySusiFunc(SUSI_FN_GROUP SUSI_FuncGrp, uint8_t SUSI_FuncState); 
``` 
*notifySusiFunc()* is invoked when: data is received from the master about a digital function group: 
* Input: 
  - the decoded Function group 
  - the function group status 
* Returns: 
  - nothing 

------ ------ 

```c 
void notifySusiBinaryState(uint16_t Command, uint8_t CommandState);
```
*notifySusiBinaryState()* is invoked when: data is received from the Master on the status of ONE specific function: 
- Input: 
  - the number of the function (from 1 to 32767) 
  - the status of the Function (enable = 1, disable = 0) 
- Returns: 
  - nothing 

------------ 

```c 
void notifySusiAux(SUSI_AUX_GROUP SUSI_auxGrp, uint8_t SUSI_AuxState); 
``` 
*notifySusiAux()* is invoked when: data is received from the Master on the status of ONE specific AUX: 
- Input: 
  - the number of the AUX 
  - the status of the output (enable = 1, disable = 0) 
- Returns: 
  - nothing 

------------ 

```c
void notifySusiTriggerPulse(uint8_t state); 
``` 
notifySusiTriggerPulse() is invoked when: the trigger (or pulse) command for any puffs of steam is received from the master 
- Input: 
  - state of the Trigger/Pulse command 
- Returns: 
  - nothing 

-------- ---- 

```c 
void notifySusiMotorCurrent(int8_t current); 
``` 
*notifySusiMotorCurrent()* is invoked when: Data on motor current consumption is received from the master 
- Input: 
  - Current consumption: from -128 to + 127 (already converted from the original 2's complement ) 
- Returns: 
  - nothing 

------------ 

```c 
void notifySusiRequestSpeed(uint8_t Speed, SUSI_DIRECTION Dir); 
```
*notifySusiRequestSpeed()* is invoked when: the data on Speed ​​and direction requested by the control panel from the master is received 
- Input: 
  - the speed (128 step) requested 
  - the requested direction 
- Returns: 
  - nothing 

----- ------- 

```c 
void notifySusiRealSpeed(uint8_t Speed, SUSI_DIRECTION Dir); 
``` 
*notifySusiRealSpeed()* is invoked when: real Speed ​​and direction data are received from the master 
- Input: 
  - real speed (128 steps) 
  - real direction 
- Returns: 
  - nothing 

---- -------- 
 
```c
void notifySusiMotorLoad(int8_t load); 
```
*notifySusiAnalogFunction()* is invoked when: data on motor load is received from the master 
- Input: 
  - Motor load: from -128 to + 127 (already converted from the original 2's Complement) 
- Returns: 
  - nothing 

-- ---------- 

```c 
void notifySusiAnalogFunction(SUSI_AN_GROUP SUSI_AnalogGrp, uint8_t SUSI_AnalogState); 
``` 
*notifySusiAnalogFunction()* is invoked when: Data is received from the master about a group of analog functions 
- Input: 
  - the decoded analog group 
  - the state of the group 
- Returns: 
  - nothing 

------------ 

```c
void notifySusiAnalogDirectCommand(uint8_t commandNumber, uint8_t Command);  
``` 
*notifySusiAnalogDirectCommand()* is invoked when: Data is received from the master direct commands for analog operation 
- Input: 
  - the command number: 1 or 2 
  - the command bits 
- Returns: 
  - nothing 

------------ 

```c 
void notifySusiMasterAddress(uint16_t MasterAddress); 
``` 
*notifySusiMasterAddress()* is invoked when: the digital address of the master is received 
- Input: 
  - the digital address of the master 
- Returns: 
  - nothing 

------------

```c
void notifySusiControllModule(uint8_t ModuleControll);
```
*notifySusiControlModule()* is invoked when: The command on the module control is received 
- Input: 
  - bytes containing the module control 
- Returns: 
  - nothing 

------------ 

**THE FOLLOWING CALL MAY ' BE USED FOR DEBUG OR TO PULL *RAW* DATA GET FROM THE LIBRARY** 

```c 
void notifySusiRawMessage(uint8_t firstByte, uint8_t secondByte); 
``` 
*notifySusiRawMessage()* is called whenever there is a message (2 Byte) to decode. It is NOT invoked for CVs manipulation messages. Show the message Raw: NOT DECODED. 
* Input: 
  - the first byte of the message 
  - second byte of message 
* Returns: 
  - nothing
 
------------ 

# CV Manipulation
The following functions are **optional** (defined as 'extern' to the library), but allow the library to talk to the master mecoder in case of *Reading/Writing CVs* 

The library **manages the ACK** which allows the decoder to know the outcome of the requested operation. 

------------ 

```c 
uint8_t notifySusiCVRead(uint16_t CV); 
``` 
*notifySusiCVRead()* is invoked when: the reading of a CV is requested 
- Input: 
  - the number of the CV to read 
- Returns: 
  - the value of the CV read 

----------- - 

```c
uint8_t notifySusiCVWrite(uint16_t CV, uint8_t Value); 
- Inputs:
```
*notifySusiCVWrite()* is invoked when: Writing a CV is required. 
- Input: 
  - the requested CV number 
  - the New value of the CV 
- Returns: 
  - the read (post-write) value of the CV to be written 

------------ 

RESET CVs, the *same is used Library function* [NmraDcc](https://github.com/mrrwa/NmraDcc): 

```c 
void notifyCVResetFactoryDefault(void); 
``` 
*notifyCVResetFactoryDefault()* Called when CVs must be reset. This is called when CVs must be reset to their factory defaults. 
  - None                                                                                                        
- Returns: 
  - None

------------ 

# Class Destruction 
It is possible to destroy the class if it is no longer needed. 
```c 
~Rcn600(void);	
``` 

Resources will be deallocated, pins will be put into **INPUT** state to avoid accidental damage. 
 
------------ 

# Data Types
The following data types are used by the methods/functions of the library, *they are symbolic types* defined via "#define" and serve to improve the readability of the code , correspond to the type *uint8_t* 


```c 
#define SUSI_DIRECTION uint8_t  
...
#define SUSI_FN_GROUP uint8_t 
... 
#define SUSI_AUX_GROUP uint8_t 
... 
#define SUSI_AN_GROUP uint8_t 
```

------------ 

```c 
SUSI_DIRECTION 
``` 
Identifies *symbolically* the direction transmitted by the Master Decoder: 

- SUSI_DIR_REV : *reverse* direction 
- SUSI_DIR_FWD : *forward* direction 

----- ------- 

```c 
SUSI_FN_GROUP 
``` 
Identifies *symbolically* the group of Digital Functions transmitted by the master decoder: 

- SUSI_FN_0_4 : Functions from 0 to 4 
- SUSI_FN_5_12 : Functions from 5 to 12 
- SUSI_FN_13_20 : Functions from 13 to 20  
- SUSI_FN_21_28 : Functions 21 to 28
- SUSI_FN_29_36 : Functions from 29 to 36 
- SUSI_FN_37_44 : Functions from 37 to 44 
- SUSI_FN_45_52 : Functions from 45 to 52 
- SUSI_FN_53_60 : Functions from 53 to 60 
- SUSI_FN_61_68 : Functions 61 to 68 

------------ 

```c 
SUSI_AUX_GROUP 
``` 
Identifies *symbolically* the group of AUXs transmitted by the master decoder: 

- SUSI_AUX_1_8 : AUX from 1 to 8 
- SUSI_AUX_9_16 : AUX from 9 to 16 
- SUSI_AUX_17_24 : AUX from 17 to 24 
- SUSI_AUX_25_32 : AUX from 25 to 32 

----------- - 

```c 
SUSI_AN_FN_GROUP 
``` 
Identifies *symbolically* the group of analogue functions transmitted by the master decoder: 

- SUSI_AN_FN_0_7 : Analogue Functions from 0 to 7
- SUSI_AN_FN_8_15 : Analog functions from 8 to 15  
- SUSI_AN_FN_16_23 : Analog functions from 16 to 23 
- SUSI_AN_FN_24_31 : Analog functions from 24 to 31
- SUSI_AN_FN_32_39 : Analog functions from 32 to 39 
- SUSI_AN_FN_40_47 : Analog functions from 40 to 47 
- SUSI_AN_FN_48_55 : Analog functions from 48 to 55 
- SUSI_AN_FN_56_63 : Analog functions from 56 to 63

-------
