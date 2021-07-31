---
Title: I2C Port Erweiterung
Template: chapter
Toc: chapter
---

# I2CPorterweiterung

![][1]  
*ASURO Porterweiterung mit [I2C Bus][2]*



## Schaltung

Die Schaltung erweitert den ASURO um 8 digitale I/O Ports, und ist auf einer Standard ASURO Erweiterungsplatine aufgebaut. Die Schaltung ist dem I2C IO Board von Klaus Leidinger <http://www.mikrocontroller-projekte.de/> nachempfunden. 

Als I2C Chip wird der 8-Bit I2C Portbaustein von Philips verwendet. Ebenso kann der pin-kompatible verwendet werden. Die I2C Slave Adresse des ist die 0x40 (0x70 beim PCF 8574A). Über Jumper auf der Erweiterungsplatine können bis zu 8 Geräte (bis zu 16 Geräte beim PCF 8574AP) parallel an einem [I2C Bus][2] angeschlossen werden. 

Eine vereinfachte Version dieser Schaltung wird auch für die [LCD Erweiterung][3] verwendet. Dabei wird auf die Adressierung und INT0 verzichtet. Ebenso wurden die Serienwiederstände in den I2C Leitungen weggelassen. 

**Schaltplan** 



![][4]

Für den [I2C Bus][2] werden die Ports PB2(ADC2) als SCL und PB3(ADC3) als SDA benutzt. Optional kann noch INT0 als Interrupt Eingang verwendet werden (über Jumper). Mit kleinen Anpassungen lassen sich auch andere Ports benutzen. Mehrere Boards lassen sich übereinander stapeln (geeignete Pfosten/Buchsen Leiste vorrausgesetzt). 

Die I/O Ports sind auf Pfostenstecker geführt, und lassen sich über ein separates I/O Board verwenden. Als quasi bidirektionale Ports lassen sie sich ohne Richtungsumschaltung lesen oder schreiben. Es genügt ein I2C READ Befehl zum lesen der Daten, bzw ein I2C WRITE Befehl zum schreiben. Dem Anwender bleibt es frei, wie er die Pins benutzt. 

**Platine Vorderseite** 



![][5]

**Platine Rückseite** 



![][6]



### Stückliste

| **Anzahl** | **Bezeichnung** | **Beschreibung**                                                                                                 |
||
| 1          | IC1             | [PCF 8574P][7] o. AP, I2C Porterweitungs IC                                                                      |
| 3          | R1..3           | Widerstand, 10 kOhm, optional als I2C Abschluß Widerstände                                                          |
| 3          | R4..6           | Widerstand, 220 Ohm, Reihenwiderstände I2C Bus (nicht unbedingt erfoderlich)                                       |
| 3          | R7..9           | Widerstand, 1 kOhm, PullDown für Hardware Adressen (nicht unbedingt erfoderlich)                                 |
| 1          | C1              | Kondensator, 100 nF, Block Kondensator                                                                           |
| 1          | Â                | Leiterplatte, ASURO Erweiterungsplatine                                                                          |
| 1          | Â                | IC Sockel, 16polig                                                                                               |
| 2          | ST1..2          | Steckerleisten 2x3 polig, I2C Bus, Adress Jumper (Adress Jumper kann entfallen, dann Drahtbrücken direkt an GND) |
| 1          | ST3             | Steckerleiste, 7 polig, Port 0..3, VCC, GND                                                                      |
| 1          | ST4             | Steckerleiste, 6 polig, Port 4..7, VCC, GND                                                                      |
| 3          | ST5..7          | Steckerleisten, 2polig, Jumper für SCL, SDA, INT                                                                 |
| 2          | BU1..2          | Buchsenleisten, 3polig, Anschluß an Asuro Board                                                                   |
| 1          | BU3             | Buchsenleisten, 2polig, Anschluß an Asuro Board                                                                   |



## Software

Da die TWI Pins des ASURO belegt sind, wird der [I2C Bus][2] mit Software emuliert. Dazu wird die I2C Master Library von Peter Fleury <http://jump.to/fleury> benutzt. Die Bibliothek benötigt ca. 500 Bytes im Flash Speicher. 

Zum übersetzen der Bibliothek wird AVR-GCC ab Version 3.3 vorausgesetzt. Eine aktuelle Version von WinAVR gibt es bei <http://sourceforge.net/projects/winavr/> 

Seit Version 2.70 der [Asuro Bibliothek][8] wird I2C direkt unterstüzt. Die Fleury Lib wird nicht mehr benötigt. Allerdings unterschieden sich dort die Funktionen sowohl im Namen als auch in der Funktionalität. 



### Ein Beispielprogramm für die I2C Lib von P. Fleury 

#include <avr/io.h>  
#include "i2cmaster.h"  
#include "asuro.h"  
  
  
#define Dev8574 Â  0x40 Â  Â  Â // device address of PCF 8574, see datasheet  
  
  
int main(void)  
{  
Â  unsigned char ret;  
Â  unsigned char val;  
  
Â  Init(); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // init Asuro  
Â  i2c_init(); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // init I2C interface  
Â  val = ;  
  
Â  SerWrite("I2C Demo", 8);  
Â  SerWrite("\r\n", 2);  
  
Â  while(1)  
Â  { Â  Â  Â  Â    
Â  Â  ret = i2c_start(Dev8574+I2C_WRITE); Â  Â  Â  // set device address and write mode  
Â  Â  if ( ret )   
Â  Â  {  
Â  Â  Â  /* failed to issue start condition, possibly no device found */  
Â  Â  Â  i2c_stop();  
Â  Â  Â  StatusLED(RED);  
Â  Â  }  
Â  Â  else   
Â  Â  {  
Â  Â  Â  /* issuing start condition ok, device accessible */  
Â  Â  Â  i2c_write(val); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  // write data  
Â  Â  Â  i2c_stop(); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  // set stop conditon = release bus  
Â  Â  Â  StatusLED(GREEN);  
Â  Â  Â  val++;  
Â  Â  }  
Â  Â  Msleep(500); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // wait a 1/2 second  
Â  }  
Â  return ;  
}

[[$[Get Code]]][9]

[i2cmaster.zip][10] - das komplette Beispielprojekt mit Bibliothek 



### Ein Beispielprogramm für die I2C Funktionen der aktuellen Asuro Bibliothek

#include "asuro.h"  
#include "i2c.h"  
  
  
#define Dev8574 Â  0x40 Â  Â  Â // device address of PCF 8574, see datasheet  
  
  
int main(void)  
{  
Â  unsigned char val;  
  
Â  Init(); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // init Asuro  
Â  InitI2C(); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  // init I2C interface  
Â  val = ;  
  
Â  SerPrint("I2C Demo\r\n");  
  
Â  while(1)  
Â  { Â  Â  Â  Â    
Â  Â  StartI2C(Dev8574+I2C_WRITE);  
Â  Â  WriteI2C(val);  
Â  Â  StopI2C();  
Â  Â  StatusLED(GREEN);  
Â  Â  val++;  
Â  Â  Msleep(500); Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // wait a 1/2 second  
Â  }  
Â  return ;  
}

[[$[Get Code]]][11]

} 



## Anwendungen

Was kann man mit den neu hinzugekommenen Ports anfangen? 



*   Ein LCD anschliessen, siehe [LCDErweiterung][3], 
*   Einen Deluxe Linienverfolger, 
*   Zusätzliche Tasten, LEDs, Sensoren 
*   ... 



## Bezugsquellen

*   [Ja-Ri-TEC][12] - ASURO Erweiterungsplatine 
*   [Reichelt][13] - I2C Bauteile. Nach PCF suchen. 



## weiterführende Links

*   <http://jump.to/fleury> - I2C Master Library 
*   [www.klaus-leidinger.de][14] - I2C IO Board mit PCF 8574 
*   [Roboternetz Wissen][15] - I2C 
*   [sprut-de][16] - Die Nutzung des I2C Interfaces 
*   [eseo.de][17] - I2C Infos 
*   [the-starbearer.de][18] - Der I2C Bus 
*   [datasheetcatalog.com][19] - PCF8574 Datenblatt 
*   [World Of Electronics][20] - I2C IO. Anschlussbeispiel für LEDs und Taster am PCF8574 
*   [GoBlack Digitaltechnik][21] - I2C LCD/Tastatur. Anschlussbeispiel für ein LCD Modul und einer Tastaturmatrix am PCF8574. 
*   [Roboternetz Thread][22] - Minimal-Projekt, LED-7segment-Anzeige über i2c-bus

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/i2c_ext.gif
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/I2CBus
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LCDErweiterung
 [4]: http://www.asurowiki.de/pmwiki/uploads/Main/asuro_i2c_expansion.png
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/i2c_ext_front.jpg
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/i2c_ext_back.jpg
 [7]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/PCF8574
 [8]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [9]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/I2CPorterweiterung?action=sourceblock&num=1
 [10]: http://www.asurowiki.de/pmwiki/uploads/Main/i2cmaster.zip
 [11]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/I2CPorterweiterung?action=sourceblock&num=2
 [12]: http://www.ja-ri-tec.com/
 [13]: http://www.reichelt.de
 [14]: http://www.klaus-leidinger.de/mp/Mikrocontroller/I2C-Boards/I2C-IOBoard.html
 [15]: http://www.roboternetz.de/wissen/index.php/I2C
 [16]: http://www.sprut.de/electronic/pic/grund/i2c.htm
 [17]: http://www.eseo.de/i2c.htm
 [18]: http://www.the-starbearer.de/Roboterelektronik/i%B2c/I2C_Index.htm
 [19]: http://www.datasheetcatalog.com/datasheets_pdf/P/C/F/8/PCF8574.shtml
 [20]: http://www.woe.onlinehome.de/projekte.htm#i2cio
 [21]: http://www.goblack.de/desy/digitalt/l_modelle/i2c-lcd-tast/
 [22]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=27395