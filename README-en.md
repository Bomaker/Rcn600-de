![GitHub release (latest by date)](https://img.shields.io/github/v/release/TheFidax/Rcn600)
![GitHub Release Date](https://img.shields.io/github/release-date/TheFidax/Rcn600?color=blue&label=last%20release)<br/>
![GitHub commits since latest release (by date)](https://img.shields.io/github/commits-since/TheFidax/Rcn600/latest?color=orange)
[![GitHub stars](https://img.shields.io/github/stars/TheFidax/Rcn600)](https://github.com/TheFidax/Rcn600/stargazers)<br/>
[![arduino-library-badge](https://www.ardu-badge.com/badge/Rcn600.svg)](https://www.ardu-badge.com/Rcn600)
[![License](https://img.shields.io/github/license/TheFidax/Rcn600)](#)

# Inhalt
* [Introduction Rcn600 SUSI](#Rcn600-SUSI)
* [Presentation video](#Video-Presentazione)
* [Library API](#API-Libreria)
* [Examples of Use](#Esempi-di-Utilizzo)

------------

# Rcn600 SUSI
This library allows you to use an Arduino board (or a microcontroller via Arduino IDE) as a Slave for the SUSI interface.
Library tested on Arduino UNO, Arduino NANO (ATmega328P) and ATmega128 (MegaCore).</br>

**ATTENTION: Some Arduino boards work at 3.3v, the SUSI interfaces, if not specified otherwise, ARE AT 5 VOLTS!** 

To work you need 2 resistors of 470Ω in series on the SUSI lines (Clock and Data).<br/>
<img src="https://github.com/TheFidax/Rcn600/blob/master/wiring.png" width="1280">

Read more about the specification in [RCN-600.pdf](https://github.com/TheFidax/Rcn600/blob/master/RCN-600.pdf).

------------

# Video Presentation
[![Video Presentation](https://img.youtube.com/vi/VzgkDouOvCY/0.jpg)](http://www.youtube.com/watch?v=VzgkDouOvCY)

------------

# Library API
The APIs for the library are in the [readme.md](https://github.com/TheFidax/Rcn600/blob/master/src/readme.md) file available under the '[src](https://github.com/TheFidax/Rcn600/tree/master/src)' folder.</br>

------------

# Examples of Use
Examples of using the library are available under the folder [examples](https://github.com/TheFidax/Rcn600/tree/master/examples) </br>
They are subdivided according to the acquisition mode of the Clock signal:</br>
- [Clock Via *Interrupt-Pins*](https://github.com/TheFidax/Rcn600/tree/master/examples/Slave_Interrupt)
- [Clock Via *PortChangeInterrupt*](https://github.com/TheFidax/Rcn600/tree/master/examples/Slave_PortChangeInterrupt)

An [Anwendungsbeispiel](https://github.com/TheFidax/Rcn600/tree/master/examples/Slave_Rcn600_to_NmraDcc) is available to interface the *Rcn600 - Bibliothek mit der [NmraDcc](https://github.com/mrrwa/NmraDcc)* </br>

------------
