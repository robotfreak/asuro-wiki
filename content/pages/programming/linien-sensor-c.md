# LinienSensorC

Asuro Liniensensor Programm in C. Das Beispiel wurde aus den Selbsttest Programm des Asuros entnommen, zu finden auf der Asuro CD ('LineDemo.c') und als eigenständiges Programm modifiziert. 



## Beschreibung

Die Motoren werden auf mittlere Fahrt vorwärts initialisiert. Die Front LED angeschaltet und die Liniensensoren kalibriert (dazu muß der Asuro auf einer einfarbigen Fläche stehen. Schwarz oder Weiß ist in diesem Fall egal. In einer Endlosschleife werden 

*   Die Liniensensor Daten zyklisch eingelesen 
*   Die Differenz zwischen linkem und rechtem Sensor gebildet, 
*   In Abhängigkeit der Differenz (positiv = links ist heller, negativ = rechts ist heller) wird die Geschwindigkeit korrigiert (Asuro fährt Kurve und die StatusLED ändert ihre Farbe 



## Programmcode

Der Programmcode aller Beispiel- und Testprogramme kann im [Download Bereich][1] heruntergeladen werden, bzw. befinden sich im Examples Ordner der [Asuro Lib][2]. 



Â   
/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\*  
*  
* File Name: Â  LineDemo.c  
* Project Â : Â  Demo  
*  
* Description: This file contains LineDemo features  
*  
* Ver. Â  Â  Date Â  Â  Â  Â  Author Â  Â  Â  Â  Â  Comments  
* \---|\---|- Â \---|\---|\---|- Â  \---|\---|\---|\---|-- Â  \---|\---|\---|\---|\---|\---|\---|\---|\---|\---|  
* 1.00Â  Â  Â 14.08.2003 Â  Jan Grewe Â  Â  Â  Â  Â  Â  Â  Â build  
* 2.00 Â  Â  22.10.2003 Â  Jan Grewe Â  Â  Â  Â angepasst auf asuro.c Ver.2.10  
*  
* Copyright (c) 2003 DLR Robotics & Mechatronics  
\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\*\*/  
/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\***|  
Â * Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  *  
Â * Â  This program is free software; you can redistribute it and/or modify Â *  
Â * Â  it under the terms of the GNU General Public License as published by Â *  
Â * Â  the Free Software Foundation; either version 2 of the License, or Â  Â  *  
Â * Â  any later version. Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â *  
Â \*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\***|/  
#include "asuro.h"  
  
#define SPEED Â 0x8F  
  
int speedLeft,speedRight;  
unsigned int lineData[2];  
int ADOffset;  
  
void LineLeft (void)  
{  
Â  speedLeft Â += 1; Â  Â  Â /* links mehr Gas geben */  
Â  if (speedLeft > 0xFE) speedLeft = 0xFF;  
}  
  
void LineRight (void)  
{  
Â  speedRight Â += 1; Â  Â  /* rechts mehr Gas geben */  
Â  if (speedRight > 0xFE) speedRight = 0xFF;   
}  
  
int Main(void)  
{  
Â  int i;  
Â  unsigned char j;  
  
Â  Init();  
  
Â  FrontLED(ON);  
Â  for (j = ; j < 0xFF; j++) LineData(lineData);  
Â  LineData(lineData);  
Â  ADOffset = lineData[LEFT] - lineData[RIGHT]; Â  Â  Â   
Â  speedLeft = speedRight = SPEED;  
Â  for(;;) {  
Â  Â  LineData(lineData);  
Â  Â  i = (lineData[LEFT] - lineData[RIGHT]) - ADOffset;  
Â  Â  if ( i > 4) {  
Â  Â  Â  StatusLED(GREEN);  
Â  Â  Â  LineLeft();  
Â  Â  }  
Â  Â  else if ( i < -4) {  
Â  Â  Â  StatusLED(RED);  
Â  Â  Â  LineRight();  
Â  Â  }  
Â  Â  else {  
Â  Â  Â  StatusLED(OFF);  
Â  Â  Â  speedLeft = speedRight = SPEED;  
Â  Â  }  
Â  Â  MotorSpeed(speedLeft,speedRight);  
Â  }   
Â  return ;  
}

[[$[Get Code]]][3]



## Probleme

Das Liniensensor Programm ist das Paradebeispiel für Frust beim Anwender. Es funktioniert in der vorliegenden Version leider so gut wie gar nicht. Die Hauptprobleme sind: 



*   Da die Räder immer nur beschleunigt werden, wird der Asuro immer schneller und fliegt irgendwann aus der Kurve. 
*   Die Fototransistoren sind sehr empfindlich gegen Streulicht. In einem abgedunkelten Raum erzielt man wohl noch die besten Ergebnisse. 
*   Der Asuro reagiert auf zu scharfe Kurven gar nicht und fährt geradeaus. 
*   die unterschiedlich starken Motoren führen dazu, dass der ASURO z.B. einer Linie mit Linkskurven noch folgen kann, nicht aber Rechtskurven. 



## Verbesserungen

Um die oben genannten Probleme zu beseitigen oder zumindest zu reduzieren, kann man einige Änderungen an der Software bzw. an der Hardware ändern. Folgende Änderungen empfehlen sich: 



### Software

*   Anstatt die einzelnen Räder beim Kurven fahren immer nur zu beschleunigen, ist es hilfreicher zudem das entgegengesetzte Rad abzubremsen (evtl. auch noch abhängig davon wie stark die Änderung zwischen links und rechts ist). Damit schafft der Asuro auch engere Kurven. 
*   Die Differenz zwischen den unterschiedlich starken Motoren läßt sich durch einen zusätzlichen Offset zwischen linken und rechtem Motorspeed Wert kompensieren. Dazu läßt den Asuro solange ein Stück geradeaus fahren und erhöht den Offset schrittweise, bis er einigermaßen geradeaus fährt. 
*   Den Offsetwert zwischen linken und rechtem Fototransistoren läßt sich durch Mittelwertbildung genauer bestimmen. Durch Aufsummieren der Werte und anschließendem Teilen durch die Anzahl der Durchläufe. Da Divisionen beim AVR sehr rechenintensiv sind, sollte man hier als Durchlaufzähler eine 2er Potenz wählen und anstelle der Division eine Shiftoperation durchführen (entspricht einer Division durch 2). 
*   Das Streulicht bzw. die Umgebungshelligkeit läßt sich dadurch kompensieren, indem man jede Liniensensor Abfrage 2 mal (oder mehrmals, wieder mit Mittelwertbildung) durchführt. Dabei die Messungen zuerst mit eingeschalteter Front LED und dann nochmal bei abgeschalteter Front LED durchführen. Die gemessene Differenz zwischen eingeschalteter und ausgeschalter LED entspricht der Umgebungshelligkeit. 
*   Mit einer Regelung für die Motoren durch einen PI oder PID Regler fährt der ASURO die Kurven sehr viel weicher. 



### Hardware

*   Die Fototransistoren mit Schrumpfschlauch überziehen, schützt einigermaßen gegen Streulicht. Siehe [Liniensensor Modifikation][4]. 



## verbesserter Programmcode 

t.b.d. 



## Weblinks

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Downloads
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LinienSensorC?action=sourceblock&num=1
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LiniensensorModifikation