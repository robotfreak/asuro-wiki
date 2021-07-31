# MyasuroH

## Einleitung 

Die Datei [myasuro.h][1] enthält Benutzerspezifische Definitionen für Korrekturwerte. Da jeder ASURO geringe Abweichungen bestimmter Werte durch Bauteiletoleranzen etc. besitzt, werden diese Korrekturwerte in einer eigenen Headerdatei gesammelt. Diese Korrekturwerte können mit Hilfe eines Windows Programms und einem entsprechenden Testprogramm auf dem ASURO weitestgehend automatisch bestimmt werden (Dank an RN-User sternthaler). Danach kann die ASURO Lib mit den gefunden Werten neu übersetzt werden. Tut man das nicht, haben die Änderungen in der Datei myasuro.h keine Auswirkung. 



## Programmcode



Â   
/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\**\*|\*/  
/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\***|  
* Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  *  
* Â  This program is free software; you can redistribute it and/or modify Â *  
* Â  it under the terms of the GNU General Public License as published by Â *  
* Â  the Free Software Foundation; either version 2 of the License, or Â  Â  *  
* Â  any later version. Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â *  
\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\***|/  
  
#ifndef MYASURO_H  
#define MYASURO_H  
  
/* Tastaturabfrage */  
#define MY\_SWITCH\_VALUE Â  Â  Â  Â  Â  61L Â    
/* Odometrie / Encoder */  
  
#define MY\_ODO\_LIGHT\_VALUE\_L Â  Â  160 Â  Â   
#define MY\_ODO\_DARK\_VALUE\_L Â  Â  Â 140 Â  Â   
#define MY\_ODO\_LIGHT\_VALUE\_R Â  Â  160 Â  Â   
#define MY\_ODO\_DARK\_VALUE\_R Â  Â  Â 140 Â  Â   
/* Werte für 12 Segmente Encoder */  
  
#define MY\_GO\_ENC\_COUNT\_VALUE Â 19363L Â    
#define MY\_TURN\_ENC\_COUNT\_VALUE Â 177L Â    
/* Werte zum ausgleichen unterschiedlicher Motoren */  
  
#define MY\_MOTOR\_DIFF Â  Â  Â  Â  Â  Â  Â 0 Â  Â   
#endif /* MYASURO_H */

[[$[Get Code]]][2]



## Weblinks

*   [Roboternetz Thread][3] - ASURO emittelt Werte für Lib V2.70 myasuro.h selber 
*   [PCSensoreV200.zip][4] - Download des Windowsprogramms 
*   [ASSensorenV205.zip][5] - Download des ASURO Testprogramms

 [1]: http://www.asurowiki.de/pmwiki/pub/html/myasuro_8h.html
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MyasuroH?action=sourceblock&num=1
 [3]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=31073
 [4]: http://members.surfeu.de/sternthaler/ASURO/PCSensorenV200.zip
 [5]: http://www.roboternetz.de/phpBB2/download.php?id=10676