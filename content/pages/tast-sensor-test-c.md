# TastSensorTestC

Asuro Tastsensor Testprogramm. 



## Beschreibung

Die [Tastsensoren][1] des Asuro werden alle 1/2 Sekunde überprüft und das Ergebnis über die IR Schnittstelle zum PC gesendet. Dort kann das Ergebnis mithilfe eines Terminalprogramm überprüft werden. 



## Programmcode

Der Programmcode aller Beispiel- und Testprogramme kann im [Download Bereich][2] heruntergeladen werden, bzw. befinden sich im Examples Ordner der [Asuro Lib][3] unter [TasterTest][4]. 



Â   
/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\*\*  
Â *  
Â * File Name: Â  tastsensor.c  
Â * Project Â : Â  ASURO  
Â *  
Â * Description: Test der Tastensensoren  
Â *  
Â * Ver. Â  Â  Date Â  Â  Â  Â  Author Â  Â  Â  Â  Â  Comments  
Â * \---|\---|- Â \---|\---|\---|- Â  \---|\---|\---|\---|-- Â  \---|\---|\---|\---|\---|\---|\---|\---|\---|\---|  
Â * 1.0 Â  Â  Â 10.09.2005 Â  Peter Â  Â  Â  Â  Â  Â initial build  
Â * 1.1 Â  Â  Â 08.01.2006 Â  Peter Â  Â  Â  Â  Â  Â 2x PollSwitch + Vergleich, anstelle 8x PollSwitch  
Â *   
Â * benoetigt die modifizierte Asuro Bibliothek 'asuro.c'   
Â * von waste, stochri und andun. Zu finden bei www.roboternetz.de  
Â */  
/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\***|  
Â * Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  *  
Â * Â  This program is free software; you can redistribute it and/or modify Â *  
Â * Â  it under the terms of the GNU General Public License as published by Â *  
Â * Â  the Free Software Foundation; either version 2 of the License, or Â  Â  *  
Â * Â  any later version. Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â *  
Â \*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\***|/  
  
#include "asuro.h"  
  
int main(void)  
{  
Â  unsigned char t1, t2;  
  
Â  Init();  
Â  SerWrite("\r\nTastsensor Test\r\n",19);  
Â  while(1)  
Â  {  
Â  Â  t1 = PollSwitch();  
Â  Â  t2 = PollSwitch();  
Â  Â  if(t1 && t2 && t1 == t2) Â  Â  Â  Â  Â  Â  Â /* irgendeine Taste gedrueckt */   
Â  Â  {  
Â  Â  Â  PrintInt(t1); Â  Â  /* Tastenwert senden */  
Â  Â  Â  SerWrite("\r\n", 2); /* Zeilenvorschub */  
Â  Â  Â  Msleep(500); Â  Â  Â  Â  /* halbe Sekunde warten */  
Â  Â  }  
Â  }  
}

[[$[Get Code]]][5]



## Ausgabe

Funktionieren alle Tastsensoren korrekt, so sollte im Terminalprogramm folgende Ausgabe erscheinen, wenn nacheinander die Taster K1..K6 gedrückt werden. 



    Tastsensor Test
    32
    16
    8
    4
    2
    1
    
    

Falls die Werte K1, K2 o. K3 etwas abweichen, z.B. 33 statt 32 liefern hilft eine Modifikation der Bibliotheksfunktion PollSwitch(). Näheres siehe im [FAQ][6] unter Taster Probleme. 

Werden mehrere Tasten gleichzeitig gedrückt entspricht der ausgegebene Wert der Summe der gedrückten Tasten. 

Die Werte für die einzelnen Tasten sind nicht zufällig gewählt sondern entsprechen den 2er Potenzen 21, 22, 23, 24, 25, 26. Dadurch kann man in eigenen Programmen die gedrückte Tasten mit den gesetzten Bits (in Hexadezimal Schreibweise) abtesten. 



    t1 = PollSwitch();
    t2 = PollSwitch();
    if (t1 && t2 && t1 == t2)
    {
      if (t1 & 0x01)   // Taste K6 gedrückt
        do_K6();
      if (t1 & 0x02)   // Taste K5 gedrückt
        do_K5();
      if (t1 & 0x04)   // Taste K4 gedrückt
        do_K4();
      if (t1 & 0x08)   // Taste K3 gedrückt
        do_K3();
      if (t1 & 0x10)   // Taste K2 gedrückt
        do_K2();
      if (t1 & 0x20)   // Taste K1 gedrückt
        do_K1();
      if (t1 & 0x07)   // Taste K6, K5 und K4 gedrückt
        do_K6_K5_K4();

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Tasten
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Downloads
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [4]: http://www.asurowiki.de/pmwiki/pub/html/_taster_test_2test_8c.html
 [5]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/TastSensorTestC?action=sourceblock&num=1
 [6]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/FAQ