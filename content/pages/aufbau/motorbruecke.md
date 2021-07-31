# Motorbruecke

![](%assets_url%/motorbridge.jpg)  
*Motor Brücke*

## Funktionsweise

Der ASURO besitzt für jeden seiner beiden Motoren eine diskret aufgebaute H-Brücke. Zur Steuerung des linken Motors werden die Prozessor Pins PB1, PD4 und PD5 verwendet (PB2, PB4 und PB5 für den rechten Motor) An PB1 (bzw. PB2) liegt das PWM Signal für die Motor Geschwindigkeit an. PD4 und PD5 (bzw. PB4 und PB5) bestimmen die Drehrichtung des Motors. Die beiden UND-Gatter verknüfen Geschwindigkeit und Drehrichtung miteinander und führen das resultierende Signal zu den Transistoren T2 und T4. 

### Motor links dreht vorwärts

Hier ist der Transistoren T1 durchgeschaltet. Transistor T4 ist in Abhängigkeit von dem angelegten PWM Signal durchgeschaltet oder gesperrt. Dadurch wird die Geschwindigkeit des Motors geregelt. T2 und T3 sperren. Der Strom kann über T1 durch den Motor über T4 nach GND fliessen. 

![](%assets_url%/motorbridge_forw.jpg)

### Motor links dreht rückwärts

Hier sind die Transistoren T2 und T3 durchgeschaltet. Transistor T3 ist in Abhängigkeit von dem angelegten PWM Signal durchgeschaltet oder gesperrt. Dadurch wird die Geschwindigkeit des Motors geregelt. T1 und T4 sperren. Der Strom kann über T2 in der anderen Richtung durch den Motor über T3 nach GND fliessen. 

![](%assets_url%/motorbridge_back.jpg)

### Motor links bremsen

Die Transistoren T1 und T3 sind durchgeschaltet. Es wird ein Gegenstrom durch den Motor geleitet. Der Motor wird dadurch gebremst. 

### Motor links im Leerlauf

Die Transistoren T1 und T3 sperren. Kein Strom fließt durch den Motor. 

### Wahrheits Tabelle für Drehrichtung 

| **Funktion** | **PD5 (PB5)** | **PD4 (PB4)** |
||
| vorwärts       | 1             | 0             |
| rückwärts         | 0             | 1             |
| bremsen      | 0             | 0             |
| leerlauf     | 1             | 1             |

## Programmierung

Um die Motoren anzusteuern gibt es in der [Asuro Bibliothek]((http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek)) die fertigen Funktionen MotorDir() und MotorSpeed () und die Definitionen FWD, RWD, BREAK, FREE. Einige Beispiele dazu: 

```c
/* Asuro vorwärts fahren lassen */  
  MotorDir(FWD,FWD);   /* Beide Motoren Drehrichtung vorwärts */  
  MotorSpeed(255,255); /* Beide Motoren Geschwindigkeit maximal */

/* Asuro rückwärts fahren lassen */  
  MotorDir(RWD,RWD);   /* Beide Motoren Drehrichtung rückwärts */  
  MotorSpeed(255,255); /* Beide Motoren Geschwindigkeit maximal */

/* Asuro auf der Stelle rechts drehen lassen */  
  MotorDir(FWD,RWD);   /* Motoren Drehrichtung links vorwärts, rechts rückwärts */  
  MotorSpeed(255,255); /* Beide Motoren Geschwindigkeit maximal */

/* Asuro eine Rechtskurve fahren lassen */  
  MotorDir(FWD,FWD);   /* Beide Motoren Drehrichtung vorwärts */  
  MotorSpeed(255,);    /* Motoren Geschwindigkeit links maximal, rechts stop */

/* Asuro eine Linkskurve fahren lassen */  
  MotorDir(FWD,FWD);   /* Beide Motoren Drehrichtung vorwärts */  
  MotorSpeed(, 255);   /* Motoren Geschwindigkeit links stop, rechts maximal */

/* Asuro schnell abbremsen lassen */  
  MotorDir(BREAK,BREAK);  /* Beide Motoren bremsen */  
  MotorSpeed(0, 0);       /* Beide Motoren stop */
```  

## Besondere Verwendung der Motorbrücken

### Soundausgabe

Tatsächlich kann man die Ansterung der Motoren über die Motorbrücken dazu 'mißbrauchen', dem ASURO Töne zu entlocken. Die PWM Frequenz wird zur Lautstärke Regelung benutzt. Die hörbare Frequenz wird durch schnelles Umpolen der Motorrichtung erreicht. Der Thread zur Soundfunktion aus dem [Roboternetz](http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=23716). Damit ist aber lediglich Monosound realisiert. Aber auch Stereosound, bzw. polyphone Klänge sind möglich, da der ASURO ja zwei Motren besitzt, können diese auch getrennt voneinander angesteuert werden. Auch hierzu gibt es einen Thread im [Roboternetz](http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=31867). Seit der Version 2.70RC3 ist die Monosound Funktion in der [Asuro Lib](http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek) enthalten. Mit der Release 2.80 auch die Stereosound Funktion. 

## Weiterführende Links:

* [H-Bridge demystified](http://www.barello.net/Papers/H-Bridge.pdf)

