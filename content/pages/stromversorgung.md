# Stromversorgung

![][1] ![][2]

*Stromversorgung und Spannungsüberwachung* <vspace>

## Funktionsweise:<vspace>

Der ASURO wird mit 4 Mirco AAA Zellen betrieben. Akkus sind empfehlenswert, dazu muß dann der Jumper JP1 auf dem Mainboard gesetzt werden. Der Jumper überbrückt dann die Diode D1. Damit entfällt der Spannungsabfall von 0,6V, den die Diode verursacht. Die Betriebsspannung liegt dann bei 4,8V (bei Akku-Betrieb und gestecktem Jumper, bzw. 5,4V bei Batteriebetrieb. <vspace>

Die Spannungsüberwachung besteht aus einem einfachen Spannungsteiler der durch die Widerstände R12 und R13 gebildet wird. Darüber wird die mit V+ die Stromversorgung der A/D Wandler angelegt. Zwischen VCC und V+ liegt noch der Widerstand R11 in Reihe. Über den Prozessor Pin PC5, der als A/D Wandler Port konfiguriert ist, wird die Spannung gemessen. Im Bootloader wird die Batteriespannung überprüft. Liegt sie zu tief (< 4 Volt) startet der Asuro nicht mehr das geflashte Userprogramm. Statt dessen fängt die Status LED an gelb/rot zu blinken, und über den seriellen Port wird 'LV' gesendet. <vspace>

## Programmierung:<vspace>

In der [Asuro Lib][3] gibt es die Funktion *Battery()* zur Abfrage der Batteriespannung. Die Funktion liefert lediglich den A/D Wandler Wert. Welcher Spannung der gemessen Wert entspricht, ist leider exemplar abhängig. Als groben Richtwert kann gelten: Ein Wert über 800 Spannung ist noch ok. Eine gemittelte Messreihe für meine beiden Asuros sieht z.B. so aus: <vspace> 

| **Spannung** | **Asuro 1** | **Asuro 2** |
||
| 5,2          | 960         | 925         |
| 5,0          | 930         | 895         |
| 4,8          | 890         | 855         |
| 4,6          | 860         | 815         |
| 4,4          | 820         | 785         |
| 4,2          | 780         | 750         |
| 4,0          | 740         | 720         |
| 3,8          | 710         | 680         |
| 3,6          | 680         | 650         |
| 3,4          | 640         | 605         |
| 3,2          | 600         | 570         |<vspace>

Wie man sieht arbeitet der Asuro auch bei fast 3V noch und gibt seine Werte über die IR Schnittstelle aus. Allerdings würde er bei solch einer niedrigen Spannung nicht mehr die Applikation booten (s.o). Der verwendete Atmel AVR ATmega8L hat einen zulässigen Spannungsbereich von 2,7..5,5V. Im Asuro1 ist anstelle vom Widerstand R11 eine 100µH Spule eingebaut worden. Das erklärt die etwas höher gemessenen Werte, da an diesem Widerstand noch erwas mehr Spannung abfällt als an der Spule. <vspace>

### Battery Funktion<vspace>

int Battery(void)  
{  
Â  intÂ  Â ec_bak = autoencode;Â  Â  Â  Â  Â  Â  // Sichert aktuellen Zustand  
Â  intÂ  Â data;  
  
Â  /*  
Â  Â  Â Autoencode-Betrieb vom ADC-Wandler unterbinden.  
Â  */  
Â  autoencode = FALSE;  
  
Â  ADMUX = (1 << REFS0) | (1 << REFS1) | BATTERIE; // interne 2.56V Referenz  
Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  // Ref. mit ext. Kapazitaet  
Â  Sleep(5);Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // warten bis Referenzspannung stabil ist  
Â  ADCSRA |= (1 << ADSC);Â  Â  Â  Â  Â  Â  Â  Â  // Starte AD-Wandlung  
Â  while (!(ADCSRA & (1 << ADIF)))Â  Â  Â  Â // Ende der AD-Wandlung abwarten  
Â  Â  ;  
Â  ADCSRA |= (1 << ADIF);Â  Â  Â  Â  Â  Â  Â  Â  // AD-Interupt-Flag zuruecksetzen  
Â  data = ADCL + (ADCH << 8);Â  Â  Â  Â  Â  Â  // Ergebnis als 16-Bit-Wert  
Â  /*  
Â  Â  Â Autoencode-Betrieb vom ADC-Wandler wiederherstellen.  
Â  */  
Â  autoencode = ec_bak;  
Â  return data;  
}<vspace>

In der Battery Funktion wird im Gegensatz zu den anderen A/D Wandler Funktionen (PollSwitch, LineData u. OdometryData) als die interne 2,56V Referenzspannung verwendet. Die Versorgungsspannung als Referenz wäre sinnfrei, da man ja gerade die Versorgungsspannung messen will. Aus der Referenzspannung von 2,56V und der Auflösung des A/D Wandler (hier 10Bit, entsprechend 1024 Werte) ergibt das eine theoretische Auflösung des Wandlers von 2,5mV. <vspace>

### Achtung<vspace>

In der [Asuro Lib][3] bis einschließlich Version 2.71 steckt noch ein Fehler. Die Abfrage von Batterie liefert keine brauchbaren Werte, wenn im Programm noch andere A/D Wandler (Taster, Liniensensor, Odometrie) abgefragt werden. Der Grund liegt an der Umschaltung der Analog Refenzspannung von VCC auf die interne Referenzspannung von 2,56Volt. Dieser Vorgang braucht seine Zeit. Ein kleines Delay hinter dem Befehl zur Umschaltung *Sleep(5)* sollte genügen, damit die gelesenen Werte wieder stimmen. <vspace>

## Verbesserungsvorschläge:<vspace>

*   Mignon- statt Micro-Zellen verwenden. Das Batteriefach läßt sich problemlos gegen eines für Mignon AA Zellen austauschen. Dadurch hält der ASURO mit einem Batteriesatz länger durch. 
*   Spannungsregler einbauen. Derzeit ist die Spannung für die Steuerung ungeregelt. Das Anfahren der Motoren führt zu deutlichen Spannungseinbrüchen. Dies wiederrum führt zu Fehlern bei A/D Wandler Messungen. Allerdings wären für einen 5V Spannungsregler bei Akku-Betrieb mindestens 5 Mignon-/Micro Zellen notwendig. <vspace>

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/powersupply.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/powerwatch.jpg ""
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek

