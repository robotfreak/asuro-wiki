# KollisionsTestC

ASURO Kollisions Test mittels Abfrage der [Tastsensoren][1]. 

Solange der ASURO auf keine Hindernis trifft: 

*   fährt er geradeaus 
*   macht die grüne Status LED an und die Bremslichter aus, 

Trifft er links auf ein Hindernis (Tasten K4..6): 

*   stoppt er, 
*   macht das linke Bremslicht an und die Status LED aus, 
*   fährt für 1 Sekunde eine Linkskurve zurück. 

Trifft er rechts auf ein Hindernis (Tasten K1..3): 

*   stoppt er, 
*   macht das rechte Bremslicht an und die Status LED aus, 
*   fährt für 1 Sekunde eine Rechtskurve zurück. 



## Programm

Der Programmcode aller Beispiel- und Testprogramme kann im [Download Bereich][2] heruntergeladen werden, bzw. befinden sich im Examples Ordner der [Asuro Lib][3] unter [KollisionTest][4]. 



/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\**  
Â *  
Â * File Name: Â  kollisiontest.c  
Â * Project Â : Â  ASURO  
Â *  
Â * Description: Kollisionstest mit Hilfe der Tastensensoren  
Â *  
Â * Ver. Â  Â  Date Â  Â  Â  Â  Author Â  Â  Â  Â  Â  Â  Â  Comments  
Â * \---|\---|- Â \---|\---|\---|- Â  \---|\---|\---|\---|\---|-- Â  Â \---|\---|\---|\---|\---|\---|\---|\---|\---|--  
Â * 1.0 Â  Â  Â 10.09.2005 Â  Peter Â  Â  Â  Â  Â  Â  Â  Â initial build  
Â * 1.1 Â  Â  Â 08.01.2006 Â  Peter Â  Â  Â  Â  Â  Â  Â  Â 2x PollSwitch + Vergleich,   
Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  anstelle 8x PollSwitch  
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
  
/* Um eventuelle Unterschiede zwischen linken und rechtem Motor auszugleichen   
Â * definieren wir 2 Werte für fullspedd links und rechts  
Â */  
#define FULL_L 250 Â  Â /* Fullspeed linker Motot */  
#define FULL_R 220 Â  Â /* Fullspeed rechter Motor */  
  
/* Motor vorwärts */  
void MotorFwd(void)  
{  
Â  MotorDir(FWD,FWD);  
Â  MotorSpeed(FULL_L,FULL_R);  
}  
  
/* Motor rückwärts */  
void MotorRwd(void)  
{  
Â  MotorDir(RWD,RWD);  
Â  MotorSpeed(FULL_L,FULL_R);  
}  
  
/* Motor rückwärts Links */  
void MotorRwdL(void)  
{  
Â  MotorDir(RWD,RWD);  
Â  MotorSpeed(FULL_L,);  
}  
  
/* Motor rückwärts Rechts */  
void MotorRwdR(void)  
{  
Â  MotorDir(RWD,RWD);  
Â  MotorSpeed(, FULL_R);  
}  
  
/* Motor stop */  
void MotorStop(void)  
{  
Â  MotorSpeed(,);  
}  
  
int main(void)  
{  
Â  unsigned char t1, t2;  
  
Â  Init();  
Â  while(1)  
Â  {  
Â  Â  t1 = PollSwitch();  
Â  Â  t2 = PollSwitch();  
Â  Â  if(t1 ==  && t2 == ) Â  Â  Â  Â  /* keine Taste */  
Â  Â  {  
Â  Â  Â  MotorFwd(); Â  Â  Â  Â  Â /* vorwärts fahren */  
Â  Â  Â  FrontLED(ON);  
Â  Â  Â  BackLED(OFF,OFF);  
Â  Â  }  
Â  Â  else if (t1 && t2 && t1 == t2)  
Â  Â  {  
Â  Â  Â  MotorStop();  
Â  Â  Â  if(t1 & 0x07) /* Tasten links gedrückt? */  
Â  Â  Â  {  
Â  Â  Â  Â  MotorRwdL(); Â  Â  Â  /* Rückwärtskurve links fahren */  
Â  Â  Â  Â  FrontLED(OFF);  
Â  Â  Â  Â  BackLED(ON,OFF);  
Â  Â  Â  }  
Â  Â  Â  if (t1 & 0x38) /* Tasten rechts gedrückt? */  
Â  Â  Â  {  
Â  Â  Â  Â  MotorRwdR(); Â  Â  Â  /* Rückwärtskurve rechts fahren */  
Â  Â  Â  Â  FrontLED(OFF);  
Â  Â  Â  Â  BackLED(OFF,ON);  
Â  Â  Â  }  
Â  Â  Â  Msleep(1000); Â  Â  Â  Â /* 1 Sekunde fahren */  
Â  Â  }  
Â  }  
Â  return ;  
}

[[$[Get Code]]][5]

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Tasten
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Downloads
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [4]: http://www.asurowiki.de/pmwiki/pub/html/_kollision_test_2test_8c.html
 [5]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/KollisionsTestC?action=sourceblock&num=1