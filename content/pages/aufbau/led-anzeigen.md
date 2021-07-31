# LEDAnzeigen

![][1] ![][2] 

*ASURO Anzeigen* 

## Funktionsweise

### Status LED

Die Status LED ist eine sogenannte DUO LED. Das sind einfach zwei LEDs in einem Gehäuse. Der hier verwendete Typ hat 3 Pins. Somit können beide LEDs einzeln sowie zusammen ein-/ausgeschaltet werden. Das ergibt neben den beiden Grundfarben rot und grün der Einzel-LEDS einen gelben Farbton, wenn beide LEDs leuchten. Die rote LED wird mit PD2 gesteuert, die grüne mit PB0. 

### Front LED

Die Front LED ist Teil des [Linien Sensors][3] und sitzt vorne unter dem ASURO. Gesteuert wird die Front LED über den Port DP6. 'HIGH' Pegel schaltet die LED an, 'LOW' Pegel aus. 

### Back LEDs

Die beiden Back LEDs werden über PC0 und PC1 gesteuert. PD7 dient zusätzlich noch als Enable Signal. Während der [Odometrie][4] Messung sind die Prozessor Ports PC0, PC1 als Eingang und PD7 als Ausgang geschaltet. Deshalb können die beiden Back-LEDs nicht benutzt werden. Umgekehrt gilt: Schaltet man die Back LEDs an, werden die Ports PC0 und PC1 als Ausgang und PD7 als Eingang geschaltet und die Odometrie Messung ist nicht mehr möglich. 

## Programmierung

Um die LEDs anzusteuern gibt es in der [Asuro Bibliothek][5] fertige Funktionen und Definitionen. Einige Beispiele dazu: 

/* Die Status LED (dreifarbige LED) */  
Â  StatusLED(OFF);Â  Â  /* Schaltet die Status LED aus */  
Â  StatusLED(GREEN);Â  /* Schaltet die Status LED auf Grün */  
Â  StatusLED(YELLOW); /* Schaltet die Status LED auf Gelb */  
Â  StatusLED(RED);Â  Â  /* Schaltet die Status LED auf Rot */

/* Die Back LEDs (hinten) */  
Â  BackLED(OFF,OFF);Â  /* Schaltet die beiden hinteren LEDs aus */  
Â  BackLED(ON,OFF);Â  Â /* Schaltet die linke hintere LED an, die rechte aus */  
Â  BackLED(OFF,ON);Â  Â /* Schaltet die linke hintere LED aus, die rechte an */  
  
/* Hinweis: Der Aufruf der Funktion BackLED schaltet die Odometrie Messung ab! da diese die selben Ports verwendet! */

/* Die Front LED (des Liniensuchers */  
Â  FrontLED(OFF);Â  Â  Â /* Schaltet die Front LED aus */  
Â  FrontLED(ON);Â  Â  Â  /* Schaltet die Front LED an */

## Verbesserungsvorschlag

Um den Stromverbrauch des ASURO zu verringern, tauscht man die LEDs gegen sogenannte LowCurrent LEDs aus. Dabei müssen aber ebenfalls die LED Vorwiderstände getauscht werden. Mind. 1,5kOhm als Vorwiderstand wählen. Leider gibt es wohl noch keine stromsparenden DUO-LEDs, es könnte aber auch eine rote und eine grüne LowCurrent LED verwendet werden.

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/leds.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/odometrie.jpg ""
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Linienfolger
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Odometrie
 [5]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek

