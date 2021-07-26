# Tasten

![][1]  
*Taster*<vspace>

## Funktionsweise<vspace>

Die Taster K1..K6 an der Vorderseite des ASURO gehen an den Prozessor Pin PC4. Dieser ist als A/D Port initialisiert. Durch die verschiedenen Widerstandswerte ergibt sich je nach gedrückter Tastenkombination ein anderer A/D Wert. Die Werte der Widerstände sind so gewählt, das sich der Widerstandswert sich von Taste zu Taste verdoppelt. Analog dazu verdoppelt sich die gemessene Spannung am A/D Port. Der Spannungsteiler wird nicht, wie man vielleicht vermuten könnte mit dem 1MOhm Widerstand R23 gebildet, sondern mit dem 1kOhm Widerstand R24. Dazu wird vor jeder Messung in der PollSwitch Funktion der Prozessor Pin PD3 auf HIGH und damit auf Versorgungsspannungs Pegel gelegt. <vspace>

Über den Prozessor Port PD2 kann durch das Drücken einer Taste auch ein Interrupt ausgelöst werden. Das ist normalerweise überflüssig, das Programm sollte die Taster genügend oft abfragen können. Genausogut gibt es die Möglichkeit den A/D-Wandler Interrupt zu nutzen, um bei erfolgter Wandlung den Wert der Taster in einer globalen Variable abzulegen. <vspace>

Die PollSwitch() Funktion der Asuro.c Bibliothek sollte folgende Werte für die einzelnen Tasten liefern. <vspace>

K1 = 32, K2 = 16, K3 = 8, K4 = 4, K5 = 2, K6 = 1 <vspace>

Aufgrund der Toleranzen können diese Werte von ASURO zu ASURO schwanken und sollten deshalb einmalig mit einem [Testprogramm][2] ausgelesen und die PollSwitch() Funktion entsprechend geändert werden. <vspace>

Ab der Version 2.70RC3 der [Asuro Lib][3] wird der Korrekturwert für die Tastsensoren in der Datei [myasuro.h][4] abgelegt. Mit Hilfe eines Testprogrammes von RN-User sternthaler kann dieser Wert nun auch automatisch ermittelt werden. Hierzu gibt es auch einen Thread im [Roboternetz Forum][5] mit den benötigten Testprogrammen. <vspace>

## Programmierung<vspace>

Eine gemittelte Messreihe der reinen A/D Werte für meine beiden Asuros sieht z.B. so aus: <vspace> 

| **Taste** | **Asuro 1** | **Asuro 2** | **Spannung** |
||
| keine     | 1023        | 1023        | 5,12V        |
| K6        | 1009        | 1009        | 5,04V        |
| K5        | 993         | 994         | 4,97V        |
| K4        | 964         | 963         | 4,81V        |
| K3        | 910         | 910         | 4,55V        |
| K2        | 816         | 815         | 4,07V        |
| K1        | 676         | 676         | 3,38V        |<vspace>

Hier unterscheiden sich die gemessenen Werte zwischen den beiden Asuros nur unerheblich. Die Werte bleiben auch bei sinkender Versorgungungsspannung stabil. <vspace>

### PollSwitch Funktion<vspace>

unsigned char PollSwitch (void)  
{  
Â  unsigned int i;  
Â  int ec_bak = autoencode;Â  Â  Â  Â  Â  Â  Â  // Sichert aktuellen Zustand  
  
Â  /*  
Â  Â  Â Autoencode-Betrieb vom ADC-Wandler unterbinden.  
Â  */  
Â  autoencode = FALSE;  
  
Â  DDRD |= SWITCHES;Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // Port-Bit SWITCHES als Output  
Â  SWITCH_ON;Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  // Port-Bit auf HIGH zur Messung  
Â  ADMUX = (1 << REFS0) | SWITCH;Â  Â  Â  Â  // AVCC reference with external capacitor  
Â  Sleep (10);  
  
Â  ADCSRA |= (1 << ADSC);Â  Â  Â  Â  Â  Â  Â  Â  // Starte AD-Wandlung  
Â  while (!(ADCSRA & (1 << ADIF)))Â  Â  Â  Â // Ende der AD-Wandlung abwarten  
Â  Â  ;  
Â  ADCSRA |= (1 << ADIF);Â  Â  Â  Â  Â  Â  Â  Â  // AD-Interupt-Flag zuruecksetzen  
  
Â  i = ADCL + (ADCH << 8);Â  Â  Â  Â  Â  Â  Â  Â // Ergebnis als 16-Bit-Wert  
  
Â  SWITCH_OFF;Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // Port-Bit auf LOW  
Â  Sleep (5);  
  
Â  /*  
Â  Â  Â Autoencode-Betrieb vom ADC-Wandler wiederherstellen.  
Â  */  
Â  autoencode = ec_bak;  
  
Â  /*  
Â  Â  Die Original Umrechenfunktion von Jan Grewe - DLR wurder ersetzt durch  
Â  Â  eine Rechnung ohne FLOAT-Berechnungen.  
Â  returnÂ  ((unsigned char) ((( 1024.0/(float)i - 1.0)) * 61.0 + 0.5));  
  
Â  Â  Wert 61L evtl. anpasssen, falls fuer K1 falsche Werte zurueckgegebn werden.  
Â  */  
Â  return ((10240000L / (long)i - 10000L) * MY\_SWITCH\_VALUE + 5000L) / 10000;  
}<vspace>

In der PollSwitch Funktion wird die Versorgungsspannung als Referenzspannung verwendet. Aus der Referenzspannung von 5V und der Auflösung des A/D Wandler (hier 10Bit, entsprechend 1024 Werte) ergibt das eine theoretische Auflösung des Wandlers von ca. 5mV. <vspace>

## Probleme mit Tastern und deren Lösung<vspace>

Stimmt die Ausgabe nicht mit den o. a. Werten überein liegt evtl. ein Fehler vor. <vspace>

### Es wird immer ein Wert ausgegeben, obwohl keine Taste gedrückt wurde<vspace>

Wichtig ist das zweimalige Abfragen der PollSwitch() Funktion und der anschließende Vegleich ob beidesmal der gleiche Wert zurückgegeben wurde. Ansonsten liegt ein Kurzschluß an dem entsprechenden Taster oder dem zugehörigen Widerstand vor. <vspace>

### Die ausgegebenen Werte sind vertauscht<vspace>

Die den Tastern zugeordneten Widerständen wurden verwechselt. <vspace>

### Die ausgegebenen Werte für K1, K2, K3 stimmen nicht<vspace>

Manchmal werden abweichende Werte für K1 (31 oder 33) bzw K2 (15 oder 17) bzw. K3 (7 oder 9) beim Testprogramm ausgegeben. Das Problem läßt sich durch Anpassung der asuro.c Bibliothek beheben. Die letzte Zeile in der PollSwitch() Funktion lautet: <vspace>

return ((10240000L/(long)i-10000L)*MY\_SWITCH\_VALUEL+5000L)/10000;<vspace>

Den Wert MY\_SWITCH\_VALUE in der myasuro.h probeweise mit 62L, 63L, 64L oder 65L ersetzen und jeweils damit die Asuro Lib und dann das Testprogramm neu übersetzen und ausprobieren. Einfacher geht es mit dem Tool von Sternthaler aus dem [Roboternetz Forum][5]. Allerdings nur für Windows. Der Asuro kann den Wert aber auch gleich selbst ermitteln wie im folgenden [Kalibrier Testprogramm][6]. <vspace>

### Es wird nach drücken einer Tasten noch ein paar mal der Wert 1 ausgegeben.<vspace>

Die PollSwitch() Funktion wird im obigen Programm insgesamt 8x ausgeführt. Das sollte normalerweise reichen den Kondensator C7 vollständig zu entladen und genau dieses Problem verhindern. Eventuell muß die PollSwitch() Funktion noch öfter aufgerufen werden. <vspace>

## Weiterführende Links:<vspace>

*   [Roboternetz Thread][7] - Asuro Schalterproblem gelöst 
*   [Roboternetz Thread][5] - ASURO emittelt Werte für Lib V2.70 myasuro.h selber

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/switches.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/TastSensorTestC
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MyasuroH
 [5]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=31073
 [6]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/TastenKalibrierungC
 [7]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=9420

