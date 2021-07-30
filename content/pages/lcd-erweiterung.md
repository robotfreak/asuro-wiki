# LCDErweiterung

![][1]  
*DOGM162 LCD (beleuchtet)*



## LCD Anschluss über I2C mit dem [PCF8574][2]

Der Anschluss eines LCD-Moduls über den I2C Bus ist eine preiswerte und vor allem Port sparende Möglichkeit, den ASURO mit einer zusätzlichen Ausgabemöglichkeit zu versehen. Neben dem Display und evtl. zugehöriger Kontrastregelung ist nur noch ein [PCF8574][2] notwendig. Dies ist der gleiche IC, der auch für die [I2C Porterweiterung][3] verwendet wird. Natürlich kann das Display auch direkt an die [I2C Porterweiterung][3] angeschlossen werden. Der Aufbau erfolgt ganz einfach auf Lochraster. Zum Anschluss an den ASURO ist die ASURO Erweiterungsplatine nicht unbedingt notwendig. Im folgenden wird der Anschluss von zwei verschiedenen Displays gezeigt. Zum einen ein Standard LC Display mit HD44xxx kompatiblen Controller und zum anderen ein DOGM162 Display von [Electronic Assembly][4]. 

**Wichtig:** Der Anschluss an den ASURO erfolgt wie bei der [I2C Porterweiterung][3] über die beiden A/D Ports ADC2 und ADC3 an denen auch die Fototransistoren des Liniensensors sitzen. Die Fototransistoren stören aber nicht weiter und müssen dazu **nicht** entfernt werden, allerdings funktioniert der Liniensensor nicht, solange das LCD-Modul steckt. Benötigt werden zudem noch die I2C Bus Pullup Widerstände an den beiden Leitungen SDA und SCL. Jeweils ein 4,7kOhm Widerstand muss dazu nach VCC verbunden werden. 



## HD44xxx kompatibles LCD Modul

![][5]  
*EADIPS082 LCD mit PCF8574*

Bei einem HD44xxx kompatiblen LCD Modul ist eine Kontrastspannung erforderlich. Achtung, es gibt auch LCD Module mit negativer Kontrastspannung. Hier reicht ein Potentiometer nicht aus, man braucht zudem noch einen Spannungswandler, der die positive Versorgungsspannung in eine negative Spannung wandelt. Ob das Display eine Hintergrundbeleuchtung hat oder nicht erkennt man normalerweise an der Anzahl der Anschlüsse. Displays ohne Beleuchtung haben 14 Pins. Displays mit Beleuchtung 16 Pins. Auch hier muss beim Abschluss der Beleuchtung das Datenblatt studiert werden: 

*   wo liegt Anode und Kathode (ist leider nicht genormt). Die Anode schließt man an Plus (VCC) an, die Kathode an Minus (GND). 
*   ist der Vorwiderstand eingebaut bzw. muss ein externer Vorwiderstand angeschlossen werden 
*   wie hoch muss evtl der Vorwiderstand sein. Bei Anschluss des Displays ohne Vorwiderstand kann das Display zerstört werden. 



### Schaltplan 

![][6]  
*Schaltplan HD44xxx am PCF8574*



### Stückliste 

| **Anzahl** | **Bezeichnung** | **Beschreibung**                                                 |
||
| 1          | IC1             | [PCF 8574P][2] o. AP, I2C Porterweitungs IC                      |
| 3          | R1..2           | Widerstand, 4,7 kOhm, I2C Abschluss Widerstände                    |
| 1          | C1              | Kondensator, 100 nF, Block Kondensator                           |
| 2          | BU1..2          | Buchsenleisten, 1polig, Anschluss an Asuro Board ADC2 u. ADC3    |
| 1          | BU3             | Buchsenleisten, 2polig, Anschluss an Asuro Board Stromversorgung |
| 1          | Â                | IC Sockel, 16polig                                               |
| 1          | Â                | Lochraster Platine ca 80x50mm                                    |



## LCD-Modul aus dem Buch [Mehr Spass Mit Asuro Band 2][7]

![][8]  
*EADIPS082 LCD mit PCF8574 aus dem Buch "Mehr Spaß mit Asuro Band II"*

Im aktuellen [2. Band][7] der Serie 'Mehr Spaß mit dem Asuro' wird ebenfalls das EADIPS082 Modul für die LCD-Erweiterung verwendet. Die Platine liegt dem Bausatz bei. Nur die Bauteile muss man sich selbst besorgen. Der Aufbau ist aufgrund der fertigen Platine natürlich besonders einfach. Auch hier wird das LCD-Modul über einen PCF8574 angeschlossen. Zudem sind 3 Taster verfügbar, die über die restlichen IO-Ports an den Asuro angeschlossen werden. Allerdings entfallen dadurch weitere Funktionen. 

**Achtung:** 

Die Belegung der Ports und der Anschluss an den I2C Bus sind hier gegenüber den anderen Modulen vertauscht, ebenso ist die Pinbelegung des PCF8574 anders. Als SDA wird ADC2 verwendet, das SCL Signal ist mit ADC3 verbunden. Das lässt sich aber einfach in der Software (Datei 'i2c.h' und 'lcd.h') anpassen. Danach muss die AsuroLib neu übersetzt werden. 

So müssten die Änderungen im i2c.h File aussehen: 



    #define SDA     PC2
     #define SCL     PC3
    

So müssten die Änderungen im lcd.h File aussehen: 



    ////// PCF8574p PINS
    
     #define LD4         4            // Pin to Data Bus 4
     #define LD5         5            // Pin to Data Bus 5
     #define LD6         6            // Pin to Data Bus 6
     #define LD7         7            // Pin to Data Bus 7
    
     #define LRS         0            // Pin to RS Pin (Register Select)
     #define LRW         1            // Pin to Read/Write Pin
     #define LEN         2            // Pin to Enable Pin
     #define LBL         3            // Backlight Pin
    



### Stückliste 

Die Stückliste der benötigten Bauteile aus dem Buch '[Mehr Spass mit Asuro Band 2][7]'. Die benötigten Platinen liegen dem Buch bei. 



*   1 x Kondensator 100 nF keramisch Raster 5,08 mm 
*   3 x Kondensator 1n nF keramisch Raster 2,54 mm 
*   3 x Widerstand 4,7 kOhm, R1, R2, R13 (oder NTC 5kOhm) 
*   1 x Widerstand 1 kOhm, R3 
*   3 x Widerstand 20 kOhm, R4, R5, R6 
*   3 x Widerstand 100 Ohm, R7,R8, R9 
*   1 x Widerstand 22 kOhm, R11(Achtung! Fehler in der Stückliste im Buch) 
*   1 x Widerstand 15 Ohm, R12 
*   1 x Widerstand 220 Ohm, R14 
*   1 x MINI Trimmer stehend PT 6 - 5 KOhm 
*   1 x NTC Widerstand 4,7 KOhm (alternativ zu R13) 
*   1 x LCD Display EA DIPS 082 - HNLED 
*   1 x I/O Expander PCF 8574 P 
*   1 x Transistor BC 547 C 
*   1 x Transistor BC 557 C 
*   1 x Printtaster 8 mm rot Conrad Artikel Nr. 707678-J7 
*   1 x Printtaster 8 mm gelb Conrad Artikel Nr. 707686-J7 
*   1 x Printtaster 8 mm blau Conrad Artikel Nr. 707694-J7 
*   2 x 7 polige Buchsenleiste für LCD Display 
*   2 x 2 polige Buchsenleiste 
*   2 x 3 polige Buchsenleiste 
*   2 x 2 polige Stiftleiste (wird nicht benötigt, wenn die [Liniensensor Modifikation][9] bereits durchgeführt wurde) 
*   2 x 3 polige Stiftleiste (wird nicht benötigt, wenn die [Liniensensor Modifikation][9] bereits durchgeführt wurde) 

[LCDexamples.zip][10] - Die LCD Beispielprojekte aus dem Buch '[Mehr Spass mit Asuro Band 2][7]' angepasst an aktuelle WinAVR Versionen. 



## Video

Ein kleines Video zeigt das LCD Modul in Aktion. Sorry, die Videoqualität lässt sehr zu wünschen übrig. Energiesparlampen als Videoleuchten, das geht gar nicht :-( 

(:youtube j0ZdoW-6a0U:) 



## DOGM LCD Modul

![][11]  
*DOGM162 LCD an der I2C Erweiterung*

Das hier verwendete DOGM Modul von Electronic Assembly benötigt keine Kontrastspannung. Der Kontrast ist über die Software einstellbar. Die 4-Bit Ansteuerung des Displays über den I2C Portbaustein [PCF8574][2] benötigt insgesamt 7 Ports (4 Datenleitung D4..D7, RS, E und RW). Über den letzten freien Port kann deshalb auch die LED Hinterleuchtung über die Software nicht nur ein-und ausgeschaltet, sondern auch gedimmt werden. Zum Dimmen ist allerdings wie bei den Motoren ein PWM Signal erforderlich. Dieses müsste von der Software dann emuliert werden. Die DOGM Modulreihe wird in verschiedenen Farben angeboten, zudem gibt es verschiedene LED Beleuchtungen. Bei dem hier verwendeten weißen Display funktioniert mit und ohne LED Hinterleuchtung. Beim blauen Display z.B. ist eine LED Beleuchtung immer notwendig, da es ohne Beleuchtung nicht ablesbar ist. Welche Kombinationen möglich sind, steht im Datenblatt. Ebenfalls im Datenblatt findet man eine Tabelle, in der steht, wie hoch der Vorwiderstand für die LED Beleuchtung sein muß (hängt von der Farbe ab, und wie man die LEDs beschaltet, parallel oder seriell). Bei Anschluss des Displays ohne Vorwiderstand wird das Display zerstört. Für die hier verwendete Amber-farbene LED Beleuchtung wird ein Vorwiderstand von mind. 32 Ohm bei Parallelschaltung und 5 Ohm bei Serienschaltung empfohlen. 

Da der [PCF8574][2] die LED Beleuchtung nicht direkt treiben kann, wird diese über einen FET geschaltet. der hier verwendete P-FET BS250 schaltet bei LOW Signal durch und sperrt bei HIGH Signal. 



### Schaltplan 

![][12]  
*Schaltplan DOGMxxx am PCF8574*



## Software

Für die Ansteuerung eines LCD Moduls über I2C mit dem PCF8574 gibt es eine fertige Sourcecode Bibliothek von RN-User raid_ox. Andere Displays können durch Ändern der Initialisierungsroutine ebenfalls angesprochen werden. Hier hilft der Blick in das jeweilige Datenblatt. Wie bei der [I2C Porterweiterung][3] wird auch hier der I2C Bus mit Hilfe der i2cmaster Lib von P. Fleury simuliert. 



### Features der LCD Library:

*   Unterstützt [PCF8574P][2] 
*   Flexiblere Pinbelegung (Veränderbar in der AsuroLib) 
*   HD447XX kompatibel und veränderbare Init für nicht HD447xx kompatible Displays 
*   Kein Zeilensprünge mehr bei längeren String 
*   ClearLCD() - zum Löschen des Displays 
*   SetIOLCD(command, bits) - zum direkten Setzen der LCD Steuerleitungen 
*   GetIOLCD() - zum Rücklesen z.B. des BusyFlags 
*   SetCursorLCD(cursor, line) - zum Positionieren des Cursors an eine bestimmte Position 
*   BacklightLCD(state) - zum Ein- und abschalten der LED Hinterleuchtung 
*   PrintIntLCD(value) - zur Ausgabe von Integer Zahlen 
*   PrintSetLCD( cursor, line, string ) - zur Ausgabe eines Strings an einer bestimmten Position 
*   PrintAlignLCD( alignment, line, string ) - gibt einen String links, rechts oder zentriert aus 
*   PrintWrapLCD - gibt einen längeren String über mehrere Zeilen aus 



### Programm Beispiel

Ein Beispielprogramm zur Ansteuerung des LCD Moduls. 



#include "asuro.h"  
#include "i2cmaster.h"  
#include "lcd.c"  
  
#define DELAY 1500  
  
int main(void)  
{  
Â  Â Init();  
Â  Â i2c_init();  
Â  Â InitLCD();  
  
Â  Â PrintLCD("LCD Testing...");  
Â  Â Msleep(DELAY);  
  
Â  Â while(1)  
Â  Â {  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintLCD("Normal");  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintSetLCD(3, , "Set Cursor");  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintSetLCD( , 1, "Set Line");  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintSetLCD(1 , 1, "Set Cursor Line");  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintSetLCD( , , "Test Int");  
Â  Â  Â  SetCursorLCD(9, );  
Â  Â  Â  PrintIntLCD(10);  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintAlignLCD(LEFT , , "LEFT");  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintAlignLCD(CENTER , , "CENTER");  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  PrintAlignLCD(RIGHT , , "RIGHT");  
Â  Â  Â  Msleep(DELAY);  
  
Â  Â  Â  ClearLCD();  
Â  Â  Â  SetCursorLCD(1,);  
Â  Â  Â  PrintWrapLCD("WRAPWRAPWRAPWRAPWRAP WRAP");  
Â  Â  Â  Msleep(DELAY);  
Â  Â }  
  
Â  Â return ;  
}

[[$[Get Code]]][13]

[i2clcd.zip][14] - Das komplette Beispielprojekt mit I2C, LCD und ASURO Bibliothek. 



## LCD Erweiterung mit dem AVR Butterfly Board

![][15]  
*LCD Erweiterung für den ASURO*

Verwendet wird dazu ein [AVR Butterfly Board][16]. Dieses Board hat neben dem LCD Modul noch viele weitere nützliche Features. Benutzt wird es hier lediglich als Eingabe-/Ausgabe- Medium, d.h. der ASURO funktioniert weiterhin autonom. Mit ca. € 30.- ist das Modul gemessen an der Ausstattung sehr preiswert. 

Die Erweiterung ist konform mit dem [Ultraschall Entfernungsmesser][17], d.h. es kann dieselbe Erweiterungsplatine benutzt werden. 

Die Kommunikation zwischen ASURO und dem [AVR Butterfly Board][16] soll später mal über den [I2C Bus][18] erfolgen. Da die entsprechenden Ports beim ASURO belegt sind, wird der [I2C Bus][18] mit 2 freien Ports simuliert. Der ASURO übernimmt hierbei die Rolle des Bus Masters, während das [AVR Butterfly Board][16] als Slave fungiert. Der ASURO schickt zyklisch seine Sensor Daten, die vom [AVR Butterfly Board][16] ausgewertet und angezeigt werden. Umgekehrt liest der ASURO Kommandos vom [AVR Butterfly Board][16] die dort mittels Joystick eingegeben werden. 

Derzeit ist die I2C Bus Kommunikation noch nicht realisiert. Das AVR Butterfly Board wird nur als Nutzlast vom ASURO transportiert. Aufgrund der guten Erfahrungen mit dem I2C LCD Modul wird dieses Projekt nicht mehr weiterentwickelt. 



## Probleme mit dem LCD Modul 

*   Im Asuro Buch II ist in der Stückliste zum LCD Modul ein falscher Widerstandswert für R11 angegeben. 15kOhm anstelle von 22 kOhm wie richtigerweise im Schaltplan. Das kann dazu führen, das das Display nichts, oder fast nichts anzeigt. Trotz Drehen am Poti bekommt man keine ausreichende Kontrastspannung. 
*   Man sollte das LCD Modul aus dem Asuro Buch II auf einem Sockel mit Präzisionsstiften setzen, sonst kann es zu Kontaktproblemen führen. 
*   Die [LCDexamples.zip][10] aus dem Asuro Buch funktionieren nicht mit mit aktuellen WinAVR Version (ab 2008). Es kommt zu Anzeigefehlern (kryptische oder falsche Zeichen). Wahrscheinlich irgendein Optimierungs Problem. Die LCD Beispiele der AsuroLib funktionieren ohne Probleme. 



## Bezugsquellen:

*   [Ja-Ri-TEC][19] - ASURO Erweiterungsplatine 
*   [Reichelt Elektronik][20] - I2C Bauteile, LC- Displays 
*   [ELV][21] - DOG-M Module Übersicht 



## Weiterführende Links:

*   [Atmel Application Note][22] - Using the USI module as a I2C slave (pdf) 
*   <http://jump.to/fleury> - I2C Master Library 
*   [www.mikrocontroller.net][23] - Artikel über den I2C Bus 
*   [Roboternetz Wiki][24] - I2C 
*   [Roboternetz Wiki][25] - LCD Modul am AVR über I2C ansteuern 
*   [Roboternetz Forum][26] - AsuroLCD Library (BETA) released!!!! v0.2 
*   [lcd-module.de][27] - Datenblatt DOG-M LCD Module

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/i2c_lcd2.jpg
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/PCF8574
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/I2CPorterweiterung
 [4]: http://www.lcd-module.de
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/i2c_diplcd.jpg
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/asuro_i2c_hd44xx_schem.png
 [7]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MehrSpassMitAsuroBand2
 [8]: http://www.asurowiki.de/pmwiki/uploads/Main/i2c_diplcd3.jpg
 [9]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LiniensensorModifikation
 [10]: http://www.asurowiki.de/pmwiki/uploads/Main/LCDexamples.zip
 [11]: http://www.asurowiki.de/pmwiki/uploads/Main/i2c_lcd.jpg
 [12]: http://www.asurowiki.de/pmwiki/uploads/Main/asuro_i2c_dogm_schem.png
 [13]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LCDErweiterung?action=sourceblock&num=1
 [14]: http://www.asurowiki.de/pmwiki/uploads/Main/i2clcd.zip
 [15]: http://www.asurowiki.de/pmwiki/uploads/Main/asuro_lcd.gif
 [16]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AVRButterflyBoard
 [17]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/UltraschallEntfernungsmesser
 [18]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/I2CBus
 [19]: http://www.ja-ri-tec.com/
 [20]: http://www.reichelt.de
 [21]: http://shop.elv.de/output/controller.aspx?cid=74&detail=10&detail2=15973
 [22]: http://www.atmel.com/dyn/resources/prod_documents/doc2560.pdf
 [23]: http://www.mikrocontroller.net/articles/I2C
 [24]: http://www.roboternetz.de/wiki/pmwiki.php?n=Main.I2C
 [25]: http://www.roboternetz.de/wissen/index.php/LCD-Modul_am_AVR#Ansteuerung_.C3.BCber_I.C2.B2C
 [26]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=27717
 [27]: http://www.lcd-module.de/deu/pdf/doma/dog-m.pdf