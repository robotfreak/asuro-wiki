# UltraschallEntfernungsmesser

![][1]  
*Ultraschall Entfernungsmesser*

Der Bau des Ultraschall Entfernungsmessers wird ausführlich im Buch ['Mehr Spass mit Asuro Band 1'][2] erläutert. Bei [Arexx][3]} gibt es auch eine ausführliche Anleitung von RN-User luma zum Download. Ebenso gibt es auch die Möglichkeit fertige [Ultraschallsensoren][4] wie den SRF04 oder SRF05 von [Devantech][5] oder der MaxSonar-EZ1 von [Maxbotix][6] an den ASURO anzuschließen. Wie bei anderen Erweiterungen auch, muss man auf die Funktion des [Liniensensors][7] verzichten, d.h. die [Liniensensor][7] Bauteile müssen ausgelötet werden, und dafür der Steckverbinder für die Erweiterungsplatine eingelötet werden. Es empfiehlt sich also einmal mehr, die [Liniensensor Modifikation][8] durchzuführen. 



![][9]  
*Platine Vorderseite*



![][10]  
*Platine Rückseite*



### Update April 2010

Fehlerteufel im Layout. es fehlt eine Verbindung zwischen R4 und C3. Vielen Dank an [Corpsman][11] für den Hinweis. Die fehlende Verbindung ist rot markiert. 



## Video

Das folgende Video zeigt den Ultraschall Entfernungsmesser in Aktion. Der Sensor erkennt (fast alle) Hindernisse in einer Entfernung von bis zu 30 cm. Den Programmcode dazu findet man [hier][12]. 

(:youtube q-itL4t2TcM:) 



## Probleme mit dem Ultraschall Entfernungsmesser

Der Ultraschall Entfernungsmesser funktioniert nicht mit der [erweiterten ASURO Bibliothek][13]. Man muss mit der Original Bibliothek von der CD arbeiten. 



### Update Juli 2007

Ein angepasster Programmcode für die [erweiterte ASURO Bibliothek][13] wurde von RN-User dopez erstellt und kann aus dem [gna.org SVN-Repository][14] bezogen werden. Allerdings ist dieser Code bisher ungetestet. Ab der Version 2.80 der [Asuro Lib][13] wird die Ultraschallerweiterung wieder unterstützt. 



## Stückliste

    1x Ultraschall-Senderkapsel UST-40T
     1x Ultraschall-Empfängerkapsel UST-40R
     1x TS912N Doppel OPV 
     1x BC574 B oder C Transistor
     1x 1N4148 Diode
     6x 100nF keramisch
     4x 10K 1/4W
     1x 100 1/4W
     1x 1K 1/4W
     1x 100K 1/4W
     1x 20K 1/4W
     1x 470K 1/4W
     1x Trimmer 1M
     1x Lochrasterplatine 
     1x Stiftleiste 10pol 
     1x Buchsenleiste 10pol 
    



## Bezugsquellen:

*   [Conrad][15] - Erweiterungsplatine, Bauteile 
*   [eBay - Gammels-KALAUMES-Shop][16] - Bausatz ULTRASCHALL Sensor für ASURO mit Platine 
*   [Ja-Ri-TEC][17] - Erweiterungsplatine, US Erweiterung als Bausatz und Buch ['Mehr Spass mit Asuro Band 1'][2] 
*   [Reichelt][18] - Bauteile 
*   [Wissenschaft Online][19] - Buch ['Mehr Spass mit Asuro Band 1'][2] 



## Weiterführende Links:

*   [Roboternetz Forum Thread][20] - Asuro Ultraschallortung Bauplan und Bibliothek 
*   [Roboternetz Forum Thread][21] - Ultraschall Interface mit gesteuerter Verstärkung und Analogausgang von Manf 
*   [Roboterwelt][22] - Ultraschall Modul 
*   <http://www.arexx.com/> - Bauanleitung und Quellcode für die Ultraschall Erweiterung zum Download

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/ultraschall_exp.jpg
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MehrSpassMitAsuroBand1
 [3]: http://www.arexx.com
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/UltraschallsensorenAmEvalBoard
 [5]: http://www.robot-electronics.co.uk/
 [6]: http://www.maxbotix.com/
 [7]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Linienfolger
 [8]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LiniensensorModifikation
 [9]: http://www.asurowiki.de/pmwiki/uploads/Main/us_ext_front3.jpg
 [10]: http://www.asurowiki.de/pmwiki/uploads/Main/us_ext_back3.jpg
 [11]: http://www.corpsman.de
 [12]: http://www.asurowiki.de/pmwiki/uploads/Main/USCollision.zip
 [13]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [14]: http://svn.gna.org/viewcvs/asuro-tools/trunk/lib/ultrasonic.c?rev=10&view=log
 [15]: http://www.conrad.de
 [16]: http://stores.ebay.de/Gammels-KALAUMES-Shop
 [17]: http://www.ja-ri-tec.com/
 [18]: http://www.reichelt.de
 [19]: http://www.science-shop.de/
 [20]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=10907
 [21]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=5261
 [22]: http://roboterwelt.de/info/schalt/usmodul/index.htm