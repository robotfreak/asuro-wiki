# Ultraschallsensoren

## Einleitung

Fertige Ultraschallsensoren sind sehr zuverlässig, haben eine große Reichweite und geben die gemessene Distanz zu einem Objekt zurück. Es gibt diverse verfügbare Module zu Preisen von 19€ bis zu 44€, mit unterschiedlichen Interfaces. Die Frontbuchse am [Asuro Eval Board][1] ist so gestaltet, dass alle gängigen Ultraschallsensoren daran angeschlossen werden können. Ebenso kann auch eine normale ASURO Erweiterungsplatine verwendet werden. Wie bei anderen Erweiterungen auch, muß man auf die Funktion des Liniensensors verzichten, d.h. die Liniensensor Bauteile müssen ausgelötet werden, und dafür der Steckverbinder für die Erweiterungsplatine eingelötet werden. 



## Devantech SRF04/05

![][2]

Beide Module arbeiten mit digital Interface. Ein Triggerimpuls startet die Messung und über den Echo Eingang wird die gemessene Distanz in Form eines Impulses zurückgeliefert. Die Länge des Impulse entspricht der gemessenen Distanz. Beim SRF04 werden 2 Prozessor Pins benötigt, der SRF05 dagegen kann auch mit nur einem Prozessor Pin betrieben werden. 



### Features

*   5V Stromversorgung 
*   Messbereich 3..400cm 
*   Triggereingang (10µs auf Low) startet die Messung 
*   Digitalausgang (148µs pro Inch, 58µs pro cm) 
*   50ms, 20Hz Messzyklus 
*   Preis 22€ SRF05, 25€ SRF04 



### Pinbelegung

![][3]

Beim Anschluß an das Asuro Eval Board wird Pin 1 der Frontbuchse freigelassen. Die Pinbelegung des SRF04 am [Asuro Eval Board][1]: 



| **Front Pin** | **Port** | **mega8 Pin** | **Funktion**             |
||
| 1             | \---|    |               | freilassen               |
| 2             | VCC      |               | Versorgungsspannung      |
| 3             | Echo     |               | Echo Ausgang             |
| 4             | Trigger  |               | Trigger Eingang          |
| 5             | n.c.     |               | nicht belegt ||          |
| 6             | GND      |               | Masse (über Drahtbrücke) |

Die Pinbelegung des SRF05 am [Asuro Eval Board][1]: 



| **Front Pin** | **Port** | **mega8 Pin** | **Funktion**                                                                                  |
||
| 1             | \---|    |               | freilassen                                                                                    |
| 2             | VCC      |               | Versorgungsspannung                                                                           |
| 3             | Echo     |               | Echo Ausgang (wenn Modepin offen), wenn Modepin auf GND gelegt nicht belegt                   |
| 4             | Trigger  |               | Trigger Eingang (wenn Modepin offen) wenn Modepin auf GND gelegt auch Echo Ausgang            |
| 5             | Mode     |               | Modepin offen ->SRF04 kompatibel, Modepin mit GND verbunden -> Echo und Trigger auf einem Pin |
| 6             | GND      |               | Masse (über Drahtbrücke)                                                                      |



### SRF04/05 am [Asuro Eval Board][1]

![][4]



## Devantech SRF08/10

Beide Module unterscheiden sich lediglich in den Abmessungen. Angesteuert werden beide über den I2C Bus. Damit ist es auch möglich mehrere Module an einem Bus zu betreiben. 



### Features 

*   5V Stromversorgung 
*   Messbereich 4..600cm 
*   I2C Ansteuerung 
*   50ms, 20Hz Messzyklus 
*   Ausgabe in µs, mm oder Zoll 
*   einstellbare Analogverstärkung 
*   Abmessungen 43x20x17mm BxHxT SRF08, 32x15x10mm BxHxT SRF10 
*   bis zu 16 Module an einem I2C Bus 
*   Preis 44€ 



### Pinbelegung

Beim Anschluß an das Asuro Eval Board wird Pin 1 der Frontbuchse freigelassen. Die Pinbelegung des SRF08/10 am [Asuro Eval Board][1]: 



| **Front Pin** | **Port** | **mega8 Pin** | **Funktion**             |
||
| 1             | \---|    |               | freilassen               |
| 2             | VCC      |               | Versorgungsspannung      |
| 3             | SDA      |               | I2C Daten                |
| 4             | SCL      |               | I2C Takt                 |
| 5             | n.c.     |               | nicht belegt             |
| 6             | GND      |               | Masse (über Drahtbrücke) |



## Devantech SRF02

Der neueste Ultraschallsensor von Devantech besitzt nur noch eine Ultraschallkapsel, die als Sender und Empfänger dient. Die Ansteuerung erfolgt über I2C oder RS232. 



### Features 

*   5V Stromversorgung 
*   Messbereich 15..600cm 
*   I2C oder RS232 Ansteuerung 
*   50ms, 20Hz Messzyklus 
*   Ausgabe in µs, mm oder Zoll 
*   Abmessungen 24x20x17mm BxHxT 
*   bis zu 16 Module an einem I2C Bus 
*   Preis 19€ 



### Pinbelegung

Beim Anschluß an das Asuro Eval Board wird Pin 1 der Frontbuchse freigelassen. Die Pinbelegung des SRF02 am [Asuro Eval Board][1]: 



| **Front Pin** | **Port** | **mega8 Pin** | **Funktion**                                        |
||
| 1             | \---|    |               | freilassen                                          |
| 2             | VCC      |               | Versorgungsspannung                                 |
| 3             | SDA      |               | I2C Daten                                           |
| 4             | SCL      |               | I2C Takt                                            |
| 5             | Mode     |               | unbeschaltet I2C mode, mit GND verbunden RS232 Mode |
| 6             | GND      |               | Masse (über Drahtbrücke)                            |



## Maxbotix EZ_Sonar EZ1

![][5]  
Maxbotix EZ-Sonar EZ1

Wie der SRF02 von Devantech besitzt der EZ-Sonar EZ1 von Maxbotix nur eine Ultraschallkapsel. Die Ansteuerung ist über RS232, analog oder digital. möglich. Über den Digitalausgang PW und dem RX Eingang des Sensors ist es möglich, mehrere Sensoren parallel zu betreiben. Die RS232 Ausgang TX arbeitet zwar mit einem TTL Pegel von 5V, gibt das UART Signal aber invertiert aus, so daß man den Sensor direkt an den RXD Pin des COM-Ports eines PC anschließen kann. Die Baudrate beträgt 9600Baud. Der Analogausgang AN gibt eine analog zur Entfernung ansteigende Spannung aus (10mV pro Inch). 



### Features

*   5V Stromversorgung 
*   Messbereich 15..600cm 
*   Objekte im Abstand 0..15cm werden wie 15cm entfernte Objekte betrachtet 
*   RS232 Ausgang (invertiert) 0..5V Pegel, 9600Baud 8,n,1 
*   Analogausgang (10mV pro inch) 
*   Digitalausgang (154µs pro Inch, 61µs pro cm) 
*   alle Ausgänge sind gleichzeitig aktiv 
*   50ms, 20Hz Messzyklus 
*   mehrere Sensoren über RX Eingang und Digitalausgang kaskadierbar. 
*   Abmessungen 22x20x17mm BxHxT 
*   Preis 25$ Lieferung aus USA 



### Maxbotix EZ-Sonar Pinbelegung

![][6]  
Maxbotix EZ-Sonar EZ1 Pinbelegung

Die Pinbelegung des EZ-Sonar am [Asuro Eval Board][1] bei Verwendung des Analogausgangs: 



| **Front Pin** | **Port** | **mega8 Pin** | **Funktion**                                |
||
| 1             | GND      |               | Masse (über Drahtbrücke)                    |
| 2             | VCC      |               | Versorgungsspannung                         |
| 3             | TX       |               | RS232 Ausgang                               |
| 4             | RX       |               | RS232 Eingang, Triggereingang               |
| 5             | AN       | 28            | Analogausgang an ADC0 (Batterie) des Asuros |
| 6             | PW       |               | Digitalausgang                              |



### Maxbotix EZ-Sonar Anschluß am [Asuro Eval Board][1]

![][7]  
Maxbotix EZ-Sonar EZ1 am Eval Board



## Fazit

Am besten geeignet für das [Asuro Eval Board][1] ist wohl der Devantech SRF05. Er ist preiswert, benötigt nur 1 Digitalpin und hat mit 1..400cm den idealen Messbereich. Auch der EZ-Sonar ist durch seinen Analogausgang (einfache Auswertung) geeignet, allerdings schwer zu beschaffen, ist teurer und hat einen schlechteren Messbereich als der SRF05. Der SRF02 ist der billigste Sensor, benötigt aber auch wie der SRF04 2 Prozessor Pins (für I2C Emulation) oder den I2C Bus zu Ansteuerung. Der SRF04 ist teurer als der SRF05 und benötigt zudem zwei Digitaleingänge. SRF08 und SRF10 sind die teuersten Module und benötigen 2 Prozessorpins bzw. den I2C Bus zur Ansteuerung. 



## Weblinks

*   [SRF04 Technical specification in engl.][8] 
*   [SRF05 Technical specification in engl.][9] 
*   [SRF08 Technical specification in engl.][10] 
*   [SRF10 Technical specification in engl.][11] 
*   [SRF02 Technical specification in engl.][12] 
*   [Maxbotix EZ-Sonar EZ1 Datasheet (pdf)][13] 
*   [Maxbotix EZ-Sonar EZ1 FAQ][14]

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroEvalBoard
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/srf04.jpg
 [3]: http://www.asurowiki.de/pmwiki/uploads/Main/srf04_pinout.jpg
 [4]: http://www.asurowiki.de/pmwiki/uploads/Main/srf04_eval.jpg
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/ezsonar.jpg
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/ezsonar_pinout.jpg
 [7]: http://www.asurowiki.de/pmwiki/uploads/Main/ezsonar_eval.jpg
 [8]: http://www.robot-electronics.co.uk/htm/srf04tech.htm
 [9]: http://www.robot-electronics.co.uk/htm/srf05tech.htm
 [10]: http://www.robot-electronics.co.uk/htm/srf08tech.shtml
 [11]: http://www.robot-electronics.co.uk/htm/srf10tech.htm
 [12]: http://www.robot-electronics.co.uk/htm/srf02tech.htm
 [13]: http://www.maxbotix.com/uploads/MaxSonar-EZ1-Datasheet.pdf
 [14]: http://www.maxbotix.com/MaxSonar-EZ1__FAQ.html