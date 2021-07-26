# Linienfolger

![][1] ![][2]

*Linienfolger* <vspace>

## Funktionsweise<vspace>

Die Front LED beleuchtet den Untergrung auf dem der ASURO fährt. Die beiden Fototransistoren T9 und T10 fangen das reflektierte Licht auf. Die Prozessor Ports PC2 und PC3 sind als A/D Wandler Ports initialisiert und messen die Spannung an den Fototransistoren. Über dunklem Untergrund wird weniger Licht reflektiert als über hellem Untergrund. Entsprechend ändert sich die Spannung an den Fototransistoren und damit der gemessene A/D Wert. <vspace>

## Besondere Verwendung des Liniensensors<vspace>

### Abgrunderkennung<vspace>

Der Liniensensor kann so programmiert werden, dass der Asuro einen Abgrund erkennen kann und zurückweicht, ohne in die Tiefe zu stürzen. Ein Video dazu gibt es bei Youtube <http://www.youtube.com/watch?v=ibAttdmQ02w> <vspace>

### Balancierender Asuro<vspace>

Von RN-User waste stammt die Idee, den Liniensensor dafür zu benutzen, dass der ASURO auf Hinterrädern balancieren kann, ohne mit dem Tischtennisball den Boden zu berühren. Allerdings sind dazu einige Umbaumaßnahmen erforderlich. Näheres siehe im [Roboternetz][3]. Ein Video gibt es ebenfalls <http://www.youtube.com/watch?v=V0VxL2VqIWQ> <vspace>

## Programmierung <vspace>

Um die Motoren anzusteuern gibt es in der [Asuro Bibliothek][4] die fertige Funktion LineData() und einige Definitionen. Ein Code Schnipsel dazu: <vspace>

  
Â  unsigned int ldata[2];Â  Â /* Speichervariablen für Liniensensor Daten */Â    
Â  int diff, offset;  
  
Â  FronLED(ON);Â  Â  Â  Â  Â  Â  Â /* Front LED an */   
Â  for (j = ; j < 0xFF; j++) LineData(lineData);Â  /* Warten bis Werte stabil sind */  
Â  LineData(ldata);Â  Â  Â  Â  Â /* Einlesen der Liniensensor Daten */  
Â  offset = ldata[LINKS] - ldata[RECHTS];Â  /* Grundoffset zwischen linkem und rechtem Sensor feststellen */  
Â  while(1)  
Â  {  
Â  Â  LineData(ldata);Â  Â  Â  Â /* Einlesen der Liniensensor Daten */  
Â  Â  diff = (ldata[LINKS] - ldata[RECHTS]) - offset;Â  /* Differenz feststellen */  
Â  Â  if (diff > 4)Â  Â  Â  Â  Â  /* links heller als rechts */  
Â  Â  Â  BackLED(ON,OFF);Â  Â  Â /* linke hintere LED an */  
Â  Â  elseÂ  (if (diff < -4)Â  /* rechts heller als links */  
Â  Â  Â  BackLED(OFF,ON);Â  Â  Â /* rechte hintere LED an */  
Â  }<vspace>

Ein komplettes Beipiel zum Liniensensor findet sich [hier][5]. <vspace>

## Verbesserungsvorschläge:<vspace>

*   Die beiden Fototransistoren mit Schrumpfschlauh besser gegen seitlich empfangenes Fremdlicht abschirmen. 
*   Beim Auswerten der Helligskeitswerte nicht mit Absolutwerten rechnen sondern mit Differenzen. So können Fremdlicht Einflüsse verringert werden 
*   Die rote Frant LED ist nicht besonders lichtstark. Zudem sind die Fototransistoren mehr empfindlicher für Infrarot Licht. Statt der roten LED könnte man auch eine Infrarot LED verwenden. Allerdings ist Infrarot Licht nicht sichtbar. Man könnte auch eine lichtstarke weiße LED nehmen. Allerdings muß man dabei beachten, daß der Maximalstrom des Prozessor Ports (20mA) nicht überschritten wird, und ob der LED Vorwiderstand (R9) richtig dimensioniert ist. 
*   Wenn man später einmal eine Erweiterungsplatine einsetzen möchte, sollte man die Bauteile des Liniensensor steckbar machen, wie unter [Liniensensor Modifikation][6] beschrieben. Sonst muß man erst mühsam die Bauteile wieder auslöten. <vspace>

## Weiterführende Links:<vspace>

*   [Linienfolger mit PD-Regler][7]

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/frontled.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/linefollow.jpg ""
 [3]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=15307
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [5]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LinienSensorC
 [6]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LiniensensorModifikation
 [7]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11818

