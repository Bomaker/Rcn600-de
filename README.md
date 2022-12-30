![GitHub release (latest by date)](https://img.shields.io/github/v/release/Bomaker/Rcn600-de)
![GitHub Release Date](https://img.shields.io/github/release-date/Bomaker/Rcn600-de?color=blue&label=last%20release)<br/>
![GitHub commits since latest release (by date)](https://img.shields.io/github/commits-since/Bomaker/Rcn600-de/latest?color=orange)
[![GitHub stars](https://img.shields.io/github/stars/Bomaker/Rcn600-de)](https://github.com/Bomaker/Rcn600-de0/stargazers)<br/>
[![arduino-library-badge](https://www.ardu-badge.com/badge/Rcn600.svg)](https://www.ardu-badge.com/Rcn600)
[![License](https://img.shields.io/github/license/TheFidax/Rcn600)](#)

See English file here: [README-en.de](https://github.com/Bomaker/Rcn600-de/tree/master/Readme-en.de)
**Work in Progress!! Not yet tested. Thanks to TheFidax for the cool software!**

# Inhalt
* [Einführung Rcn600 SUSI](#Rcn600-SUSI)
* [Demonstrationsvideo](#Demonstrationsvideo)
* [Bibliotheks-API](#Bibliotheks-API)
* [Anwendungsbeispiele](#Anwendungsbeispiele)

------------

# Rcn600-SUSI
Mit dieser Bibliothek können Sie ein Arduino-Board (oder einen Mikrocontroller über Arduino IDE) als Slave für die SUSI-Schnittstelle verwenden.
Bibliothek getestet auf Arduino UNO, Arduino NANO (ATmega328P) und ATmega128 (MegaCore).</br>

**ACHTUNG: Einige Arduino-Boards arbeiten mit 3,3V, die SUSI-Schnittstellen, falls nicht angegeben, ARBEITEN AUF 5V!** 

Für den Anschluss benötigen Sie 2 Widerstände von 470Ω in Reihe auf den SUSI-Leitungen (Clock und Data).<br/>
<img src="https://github.com/Bomaker/Rcn600-de/blob/master/wiring.png" width="1280">

Weitere informationen finden Sie in der Susi-Spezifikation [RCN-600.pdf](https://github.com/Bomaker/Rcn600-de/blob/master/RCN-600.pdf).

------------

# Demonstrationsvideo
[![Demonstrationsvideo](https://img.youtube.com/vi/VzgkDouOvCY/0.jpg)](http://www.youtube.com/watch?v=VzgkDouOvCY)

------------

# Bibliotheks-API
Die APIs für die Bibliothek sind in der Datei [readme.md](https://github.com/Bomaker/Rcn600-de/blob/master/src/readme.md) im Ordner '[src](https://github.com/Bomaker/Rcn600-de/tree/master/src)'.</br>

------------

# Anwendungsbeispiele
Beispiele für die Verwendung der Bibliothek sind im Ordner [examples](https://github.com/Bomaker/Rcn600-de/tree/master/examples) verfügbar.</br>
Sie sind nach dem Erfassungsmodus des Taktsignals unterteilt:</br>
- [Taktung über *Interrupt-Pins*](https://github.com/Bomaker/Rcn600-de/tree/master/examples/Slave_Interrupt)
- [Taktung über *PortChangeInterrupt*](https://github.com/Bomaker/Rcn600-de/tree/master/examples/Slave_PortChangeInterrupt)

Ein [Anwendungsbeispiel](https://github.com/Bomaker/Rcn600-de/tree/master/examples/Slave_Rcn600_to_NmraDcc) ist verfügbar, um die *Rcn600 - Bibliothek mit der [NmraDcc](https://github.com/mrrwa/NmraDcc)* zu verbinden.</br>

------------
