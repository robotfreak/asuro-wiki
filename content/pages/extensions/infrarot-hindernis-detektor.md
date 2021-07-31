# InfrarotHindernisdetektor

![][1]  
*Infrarot Range Detector von 'HermannSW*'



## Einleitung

Von Hause aus besitzt der ASURO außer den Taster Sensoren keine weiteren Hindernisdetektoren. Die vorhandene Infarot Schnittstelle läßt sich aber ohne große Probleme zu einem Hindernisdetektor umbauen. Ein Beispielprogramm befindet sich im Examples Ordner der [Asuro Lib][2] unter [IRCollisionTest][3]. 



### Nachtrag vom Juli 2007

Mittlerweile wurde im Roboternetz von RN-User radbruch noch ein einfachere Möglichkeit des Umbaus mit Hilfe eines Reflektors entwickelt. So muß kein Bauteil ausgelötet werden, und der Umbau ist damit komplett reversibel. Hier gibt es den Thread dazu im [RN-Forum][4] 



## IR Range Detector am [Asuro Eval Board][5]

![][6]  
*Infrarot Range Detector am Asuro Eval Board*

An der 6poligen Frontbuchse des [Asuro Eval Board][5] kann sehr einfach die Infrarot Schnittstelle umgebaut als Infrarot Hindernissdetektor angebracht werden. 3 Pins (PD0 RxD, PD1 TxD und PB3) werden dazu benötigt. 



![][7]  
*Infrarot Range Detector*



### IR Range Detector Pinout 

![][8]  
*Infrarot Range Detector Pinbelegung*

Das Pinout des IR Range Detector: 



| **Front Pin** | **Port** | **mega8 Pin** | **Funktion**            |
||
| 1             | GND      |               | Masse                   |
| 2             | VCC      |               | Versorgungsspannung     |
| 3             | PB3 OC2  | 17            | 36kHz Modulation IR LED |
| 4             | PD1 TXD  | 3             | UART senden             |
| 5             | PD0 RXD  | 2             | UART empfangen          |
| 6             | n.c.     |               | nicht belegt            |



### IR Range Detector Schaltplan

![][9]  
*Infrarot Schnittstelle*

**Anmerkung:** R17 (im Layout als R1 bezeichnet) hat nur 100Ohm, nicht 470Ohm, 



### IR Range Detector Layout

![][10]  
*Infrarot Range Detector Layout Bestückungsseite*



![][11]  
*Infrarot Range Detector Layout Lötseite*

Die IR Diode wird als einziges Bauteil unten eingelötet. Durch die Leiterplatte wird ein direktes Übersprechen zwischen IR Sender und Empfänger vermieden. Evtl. kann man die Leiterplatte zusätzlich noch mit farbigem Klebeband abkleben, um auch ein Einstreuen durch die Löcher der Lochrasterplatine zu verhindern. 



## Weiterführende Links:

*   [Roboternetz Thread][12] - Asuro: Umbau der IR-Schnittstelle zur Hinderniserkennung 
*   [Roboternetz Thread][13] - Asuro: IR-Schnittstelle als Abstandsdetektor? 
*   [Roboternetz Thread][14] - TSOP zur Hinderniserkennung: Lösung 

[Roboternetz Thread][4] - Minimallösung: IR-Abstandsmessung

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/asuroir_small.jpg
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [3]: http://www.asurowiki.de/pmwiki/pub/html/_i_r_collision_test_2test_8c.html
 [4]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=27013
 [5]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroEvalBoard
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/ir-range-detector_eval.jpg
 [7]: http://www.asurowiki.de/pmwiki/uploads/Main/ir-range-detector.jpg
 [8]: http://www.asurowiki.de/pmwiki/uploads/Main/ir-range-detector_pinout.jpg
 [9]: http://www.asurowiki.de/pmwiki/uploads/Main/ir_interface.jpg
 [10]: http://www.asurowiki.de/pmwiki/uploads/Main/ir-range-detector_front.jpg
 [11]: http://www.asurowiki.de/pmwiki/uploads/Main/ir-range-detector_back.jpg
 [12]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11114
 [13]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=10026
 [14]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?p=29471