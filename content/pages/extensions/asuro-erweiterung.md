---
Title: Asuro Erweiterung
Template: section
---

# AsuroErweiterung

## Einleitung

![][1]  
Asuro Erweiterung mit BT-Modul und ISP [Dieses Bild bei Flickr][2]

Die ASURO Erweiterung besteht zurzeit aus einem [RS232](rs232-wandler) bzw. [Bluetooth Modul](extensions/bluetooth-modem), einer ISP Schnittstelle(extensions/isp-erweiterung) und einem RESET Taster. Der Clou bei der Sache ist, die Erweiterung wird nicht, wie das LCD-Modul oder die [SnakeVision](extensions/snakevision) Erweiterung, von oben, sondern von unten aufgesteckt. D.h. man kann oben zusätzlich z.B. das [LCD-Modul stecken](extension/lcd-erweiterung). Zudem ist auf der Platine noch jede Menge Platz für weitere Features. 

## Durchführung

Durch die Erfahrungen, die ich mit dem ASURO Eval Board gemacht habe, war die Umsetzung nicht sehr schwierig. Dort war ja auch schon das RS232 Modul und das Bluetooth Modul sowie die ISP Schnittstelle vorhanden. Nur ist das ganze jetzt wesentlich kompakter, robuster und nicht so verbaut wie beim [Asuro Eval Board](extension/asuro-evalboard). 

Der ASURO muß allerdings etwas modifiziert werden, damit das ganze auch funktioniert. Wer es nachbauen möchte, sollte schon wissen, was er tut. Die Umbauten sind allerdings nicht so gravierend, dass man das Ganze nicht wieder zurückbauen könnte. Auch ist der einwandfreie Betrieb ohne die Erweiterungsplatine möglich. Es müssen lediglich 3 Jumper am Asuro gesetzt werden. 

![][8]  
Asuro Modifikation. RESET, RX und TX [Dieses Bild bei Flickr][9]

![][10]  
Asuro Modifikation. Leiterbahnen oben trennen [Dieses Bild bei Flickr][11]

![][12]  
Asuro Modifikation. ISP und UART [Dieses Bild bei Flickr][13]

Auf dem ASURO müssen ingesamt 4 Leitungen nachverdrahtet werden. Dies sind: 

1.  die TX Leitung von der IR Sende Diode (grüner Draht), 
2.  die RX Leitung vom IR Empfänger (gelber Draht), 
3.  die Versorgungspannung zur 3×2 poligen Steckerleiste (oranger Draht) 
4.  eine Versorgungsspannung Leitung zum Widerstand R11 (roter Draht), da dieser hinter der RESET Leitung an der Versorgungsspannung hing 

Dazu kommt eine 6-polige Leitung zur UART Schnittstelle und die 3polige Leitung zur ISP Schnittstelle. Versorgungsspannung und Masse kommen von den Erweiterungs Steckverbindern, die ebenfalls zur Erweiterungsplatine führen. 

![][14]  
Asuro Erweiterungs Platine [Dieses Bild bei Flickr][15]

### Schaltplan

![]((%assets_url%/asuro_erweiterung_m.png)

## UART Schnittstelle

Die UART Schnittstelle am ASURO ist normalerweise über eine Infrarot Schnittstelle realisiert. Leider ist die Reichweite dieser Lösung nicht besonders (max. 50cm). Zudem wird auf PC Seite ebenfalls ein Infrarot Transceiver benötigt. Um die UART Schnittstelle zur Erweiterungs Platine zu führen, müssen die beiden Signale RX und TX vom Prozessor zur IR Schnittstelle durchtrennt werden. Zusätzlich werden die durchtrennten Signale von der IR Schnittstelle ebenfalls zur Erweiterungsplatine geführt. Zweckmäßigerweise werden alle Signal auf einen doppelreihigen Steckerleiste geführt. Die untere Reihe wird an die Prozessor Pins gelötet. an die obere Reihe kommen die Signale von der IR Schnittstelle. Da gleich neben den UART ins der RESET Pin hängt, wird dieser ebenfalls auf die insgesamt 2×3 poligen Steckerleiste geführt (gehört aber eigentlich zur ISP Schnittstelle). Da der RESET Pin direkt an der Versorgungsspannung hängt, wird diese Verbindung ebenfalls durchtrennt und die Versorgungsspannung an die obere Reihe geführt. So ist gewährleistet, das durch Stecken von 3 Jumpern auf die Steckerleiste, die original Funktion des ASUROs wiederhergestellt ist. 

### RS232 Modul

Das [RS232 Modul](rs232-wandler) besteht aus einem normalen RS232 Pegelwandler Chip, hier ist das der MAX202. Die Steckerbelegung des 6poligen Steckbverbinders ist diesselbe wie beim [Bluetooth Modul](extensions/bluetooth-modem). 

![][17]  
Asuro RS232-Modul [Dieses Bild bei Flickr][18]

Der ASURO mit dem [RS232 Modul][3]. Mit den beiden grünen Jumper rechts neben dem RS232 Modul kann man zwischen RS232 und IR Schnittstellen Betrieb umschalten. 

### Bluetooth Modul

Als [Bluetooth Modul](extensions/bluetooth-modem) kommt das BlueSmiRF von Sparkfun zum Einsatz. Dies ist noch die Version 1.0. Neuere Module verwenden einen Bluegiga Transceiver. 

![][19]  
Asuro mit BT-Modul [Dieses Bild bei Flickr][20]

## ISP Schnittstelle

Die ISP Schnittstelle ist beim Original ASURO Prozessor abgeschaltet und kann nur durch einen Chip Erase wieder eingeschaltet werden. Leider ist durch den Chip Erase aber auch der Bootloader weg. Deshalb sollte man Experimente mit der ISP Schnittstelle nur mit einem anderen Prozessor durchgeführt werden und der Original Prozessor gut aufgehoben werden. Zur ISP Schnittstelle gehört neben RESET, Versorgungsspannung und Masse die 3 Prozessor Signale MISO, MOSI und SCK. Diese 3 Signale liegen beim Mega8 glücklicherweise direkt nebeneinander auf Pin 17,18 u. 19. So reicht eine 3polige abgewinkelte Steckerleiste aus, die an die entsprechenden Prozessor Pins gelötet werden. Leiterbahnen müssen keine aufgetrennt werden. 

Die ISP Schnittstelle benötigt keine weiteren Bauteile, lediglich der RESET Pin bekommt den üblichen 10kOhm Pullup Widerstand. Als ISP Steckverbinder wurde ein 10poliger Pfostensteckverbinder mit KANDA/STK200 Steckerbelegung verwendet. Rechts daneben befindet sich noch ein Kurzhubtaster als RESET Knopf. 

## Ausblick

Es fehlen derzeit noch die Liniensensoren. Diese werden dann, wie die Infrarot Schnittstelle, über Jumper steckbar sein. Geplant ist weiterhin eine I2C Porterweiterung mit ein paar IS471 als IR Kollisionsdetektoren. Auch ein I2C A/D Wandler wäre eine sinnvolle Erweiterung. Eventuell wäre auch ein Co-Prozessor (als I2C Slave) besser als die I2C Chips. Anstelle des ATmega8 bietet sich der pinkompatible, aber nicht codekompatible ATmega168 als Ersatz Typ an. 

## Weblinks

*   [Roboterclub Freiburg][21] - Bluetooth ASURO 
*   [Roboterclub Freiburg][22] - ASURO Prozessoradapter mit ISP und IR Abstandssensor

 [1]: http://farm3.static.flickr.com/2201/2129839498_1121858e85_b.jpg ""
 [2]: http://www.flickr.com/photos/hmblgrmpf/2129839498/
 [8]: http://farm3.static.flickr.com/3224/2364059188_23b25f64a1.jpg ""
 [9]: http://www.flickr.com/photos/hmblgrmpf/2364059188/
 [10]: http://farm3.static.flickr.com/2114/2364059014_96c7077cfb.jpg ""
 [11]: http://www.flickr.com/photos/hmblgrmpf/2364059014/
 [12]: http://farm3.static.flickr.com/3068/2364054602_53a4e547ea.jpg ""
 [13]: http://www.flickr.com/photos/hmblgrmpf/2364054602/
 [14]: http://farm3.static.flickr.com/2009/2129053755_ee7e836835_b.jpg ""
 [15]: http://www.flickr.com/photos/hmblgrmpf/2129053755/
 [17]: http://farm3.static.flickr.com/2355/2129059453_2875df5fe3_b.jpg ""
 [18]: http://www.flickr.com/photos/hmblgrmpf/2129059453/
 [19]: http://farm3.static.flickr.com/2255/2129833192_06fb5463b6_b.jpg ""
 [20]: http://www.flickr.com/photos/hmblgrmpf/2129833192/
 [21]: http://www.roboterclub-freiburg.de/asuro/hardware/bluetooth/bluetooth.html
 [22]: http://www.roboterclub-freiburg.de/asuro/hardware/chAtmegaAdapter/SumoAdapter.html

