---
Title: Mine Sweeper
Template: chapter
Toc: chapter
---

# MineSweeper

## Einleitung

Der Minesweeper Bausatz ist die neuste Erweiterung für den Asuro. Damit wird der Asuro zum Schatzsucher und kann Münzen bzw. Metall detektieren. 



![][1]  
*Minesweeper Erweiterung*



## Schaltung

Der Bausatz besteht aus einer Erweiterungsplatine, in den Abmessungen der bisherigen [Erweiterungen][2]. Dazu kommt noch der Metalldetektor, der in den TT Ball geklebt werden muß. Der Detektor besteht aus einer Spule und einem Kondensator, die einen [Schwingkreis][3] bilden. Nähert sich dem Schwingkreis ein Metallstück wird die Frequenz des Schwingkreises geändert. Der Schwingkreis wird durch einen Operationsverstärker (OPV) in Schwingung versetzt. Ein weiterer OPV, der als Komparator arbeitet, dient als Detektor. Eine LED zeigt dann an ob Metall gefunden wurde, oder nicht. 



![][4]  
*Minesweeper Platine*



![][5]  
*Minesweeper Metall Sensor*



## Software

Damit das ganze funktioniert muß erst mal der Schwingkreis über einen Trimmer Widerstand abgeglichen werden. Dazu wird das folgende Programm übersetzt und in den Asuro geladen. Zum Abgleich muß der Asuro zunächst auf einer nicht metallenen Oberfläche stehen. Dann wird solange am Trimmer gedreht, bis die LED ausgeht. Legt man nun ein Metallstück z.B. eine Münze unter den TT ball sollte die LED leuchten. Tut es das ist alles in Ordung, wenn nicht ist Fehlersuche angesagt. 



Â   
#include "asuro.h"  
  
extern volatile unsigned char count36kHz;  
  
int main(void)  
{  
Â  unsigned char oscillation;  
Â  Init();  
Â  DDRD &= ~(1<<2); // Change Port D Pin2 to input  
Â  StatusLED(OFF); Â  Â  Â  Â    
Â  while (1)  
Â  {  
Â  Â  count36kHz = ;  
Â  Â  oscillation = FALSE;  
Â  Â  while (count36kHz<200)  
Â  Â  {  
Â  Â  Â  if ((PIND & (1<<2)) == ) oscillation = TRUE;  
Â  Â  } Â  Â  Â  Â    
Â  Â  if (oscillation) FrontLED(OFF); else FrontLED(ON);  
Â  }  
Â  return ;  
}  
Â 

[[$[Get Code]]][6]

[MinesweeperKalibration.zip][7] 



## Weblinks

*   [RN-Thread zum Minesweeper Bausatz][8] 
*   [Minesweeper Fotoalbum auf Flickr][9]

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/minesweeper1.jpg
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Erweiterungen
 [3]: http://de.wikipedia.org/wiki/Schwingkreis
 [4]: http://www.asurowiki.de/pmwiki/uploads/Main/minesweeper2.jpg
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/minesweeper3.jpg
 [6]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MineSweeper?action=sourceblock&num=1
 [7]: http://www.asurowiki.de/pmwiki/uploads/Main/MinesweeperKalibration.zip
 [8]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=55272
 [9]: http://www.flickr.com/photos/hmblgrmpf/5215439108/