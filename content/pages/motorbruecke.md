# Motorbruecke

![][1]  
*Motor Brücke*<vspace>

## Funktionsweise<vspace>

Der ASURO besitzt für jeden seiner beiden Motoren eine diskret aufgebaute H-Brücke. Zur Steuerung des linken Motors werden die Prozessor Pins PB1, PD4 und PD5 verwendet (PB2, PB4 und PB5 für den rechten Motor) An PB1 (bzw. PB2) liegt das PWM Signal für die Motor Geschwindigkeit an. PD4 und PD5 (bzw. PB4 und PB5) bestimmen die Drehrichtung des Motors. Die beiden UND-Gatter verknüfen Geschwindigkeit und Drehrichtung miteinander und führen das resultierende Signal zu den Transistoren T2 und T4. <vspace>

### Motor links dreht vorwärts<vspace>

Hier ist der Transistoren T1 durchgeschaltet. Transistor T4 ist in Abhängigkeit von dem angelegten PWM Signal durchgeschaltet oder gesperrt. Dadurch wird die Geschwindigkeit des Motors geregelt. T2 und T3 sperren. Der Strom kann über T1 durch den Motor über T4 nach GND fliessen. <vspace>

![][2]<vspace>

### Motor links dreht rückwärts<vspace>

Hier sind die Transistoren T2 und T3 durchgeschaltet. Transistor T3 ist in Abhängigkeit von dem angelegten PWM Signal durchgeschaltet oder gesperrt. Dadurch wird die Geschwindigkeit des Motors geregelt. T1 und T4 sperren. Der Strom kann über T2 in der anderen Richtung durch den Motor über T3 nach GND fliessen. <vspace>

![][3]<vspace>

### Motor links bremsen<vspace>

Die Transistoren T1 und T3 sind durchgeschaltet. Es wird ein Gegenstrom durch den Motor geleitet. Der Motor wird dadurch gebremst. <vspace>

### Motor links im Leerlauf<vspace>

Die Transistoren T1 und T3 sperren. Kein Strom fließt durch den Motor. <vspace>

### Wahrheits Tabelle für Drehrichtung<vspace> 

| **Funktion** | **PD5 (PB5)** | **PD4 (PB4)** |
||
| vorwärts       | 1             | 0             |
| rückwärts         | 0             | 1             |
| bremsen      | 0             | 0             |
| leerlauf     | 1             | 1             |<vspace>

## Programmierung<vspace>

Um die Motoren anzusteuern gibt es in der [Asuro Bibliothek][4] die fertigen Funktionen MotorDir() und MotorSpeed () und die Definitionen FWD, RWD, BREAK, FREE. Einige Beispiele dazu: <vspace>

/* Asuro vorwärts fahren lassen */  
Â  MotorDir(FWD,FWD);Â  Â /* Beide Motoren Drehrichtung vorwärts */  
Â  MotorSpeed(255,255); /* Beide Motoren Geschwindigkeit maximal */<vspace>

/* Asuro rückwärts fahren lassen */  
Â  MotorDir(RWD,RWD);Â  Â /* Beide Motoren Drehrichtung rückwärts */  
Â  MotorSpeed(255,255); /* Beide Motoren Geschwindigkeit maximal */<vspace>

/* Asuro auf der Stelle rechts drehen lassen */  
Â  MotorDir(FWD,RWD);Â  Â /* Motoren Drehrichtung links vorwärts, rechts rückwärts */  
Â  MotorSpeed(255,255); /* Beide Motoren Geschwindigkeit maximal */<vspace>

/* Asuro eine Rechtskurve fahren lassen */  
Â  MotorDir(FWD,FWD);Â  Â /* Beide Motoren Drehrichtung vorwärts */  
Â  MotorSpeed(255,);Â  Â /* Motoren Geschwindigkeit links maximal, rechts stop */<vspace>

/* Asuro eine Linkskurve fahren lassen */  
Â  MotorDir(FWD,FWD);Â  Â /* Beide Motoren Drehrichtung vorwärts */  
Â  MotorSpeed(, 255);Â  Â /* Motoren Geschwindigkeit links stop, rechts maximal */<vspace>

/* Asuro schnell abbremsen lassen */  
Â  MotorDir(BREAK,BREAK);Â  Â /* Beide Motoren bremsen */  
Â  MotorSpeed(, );Â  Â  Â  Â  /* Beide Motoren stop */<vspace>

## Besondere Verwendung der Motorbrücken<vspace>

### Soundausgabe<vspace>

Tatsächlich kann man die Ansterung der Motoren über die Motorbrücken dazu 'mißbrauchen', dem ASURO Töne zu entlocken. Die PWM Frequenz wird zur Lautstärke Regelung benutzt. Die hörbare Frequenz wird durch schnelles Umpolen der Motorrichtung erreicht. Der Thread zur Soundfunktion aus dem [Roboternetz][5]. Damit ist aber lediglich Monosound realisiert. Aber auch Stereosound, bzw. polyphone Klänge sind möglich, da der ASURO ja zwei Motren besitzt, können diese auch getrennt voneinander angesteuert werden. Auch hierzu gibt es einen Thread im [Roboternetz][6]. Seit der Version 2.70RC3 ist die Monosound Funktion in der [Asuro Lib][4] enthalten. Mit der Release 2.80 auch die Stereosound Funktion. <vspace>

## Weiterführende Links:<vspace>

*   [H-Bridge demystified][7]

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/motorbridge.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/motorbridge_forw.jpg ""
 [3]: http://www.asurowiki.de/pmwiki/uploads/Main/motorbridge_back.jpg ""
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [5]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=23716
 [6]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=31867
 [7]: http://www.barello.net/Papers/H-Bridge.pdf

