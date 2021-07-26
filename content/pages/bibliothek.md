# Bibliothek


## Einleitung<vspace>

Die erweiterte ASURO Bibliothek ist eine Sammlung von Funktionen zur Vereinfachung der Programmierung des ASURO. Die Originalbibliothek auf der Installations CD wurde im Roboternetz u.a. von Weja, Waste, Stochri und Andun weiterentwickelt. Diese Version beinhaltet alle Änderungen und wurde im wesentlichen nur um Kommentare erweitert. Für die Bibliothek wurde ein Projekt auf [Sourceforge][22] und bei [gna.org][23] eingerichtet. <vspace>

*   [gna.org][24] - Die Asuro Bibliothek auf gna.org 
*   [Asuro Bibliothek][25] - Die Asuro Bibliothek auf Sourceforge 
*   <http://asuro.svn.sourceforge.net/viewvc/asuro/trunk/> - Subversion (SVN) Repository der Asuro Bibliothek 
*   [AsuroLib Online Dokumentation][26] <vspace>

## Features<vspace>

Die Features der Asuro Lib im Überblick: <vspace>

*   A/D Wandler Funktionen für die [Liniensensoren][27], die [Batterieabfrage][28] und die [Rad Encoder][29] im Pollingbetrieb 
*   Benutzerspezifische Definitionen für Korrekturwerte in der [myasuro.h][30] 
*   [Motor][31] Steuerungsfunktionen 
*   Navigieren (Drehen und Geradeaus fahren mit Odometrie Abfrage) 
*   [Rad Encoder][29] Abfrage im Interrupt Betrieb 
*   [Tastsensoren][32] Abfrage im Polling und Interrupt Betrieb 
*   [UART][33] Funktionen Pollingbetrieb 
*   [I2C][34] Master Emulation 
*   [LCD Ansteuerung][35] über I2C 
*   [RC5 Empfänger][36] für Infrarot Fernbedienungen 
*   Soundausgabe in Mono <vspace>

## Roadmap<vspace>

Ein Ausblick auf die Features kommender Versionen der Asuro Lib: <vspace>

*   interruptgesteuerte A/D Wandler Abfrage 
*   interruptgesteuerte UART Sende Empfangs Funktionen 
*   Kommando Parser mit Callback Funktionsaufruf 
*   Funktionen zur [Ultraschall Erweiterung][37] aus dem 1 Asuro Buch 
*   Soundausgabe in Stereo <vspace>

## bekannte Fehler<vspace>

###  PollSwitch Aufrufe stört die Encoder Abfrage im Interrupt Betrieb<vspace>

*   Aufruf der PollSwitch Funktion führen zu falschen Ergebnissen bei den Encoder Werten, wenn diese im Interrupt Betrieb abgefragt werden. Leider noch keine Lösung in Sicht. <vspace>

## Versions History 

###  Version 2.8.0rc1

Datum 29.03.2008 

*   Unterstützung von ATmega168 Prozessoren 
*   neue Funktion ReadADC zur A/D Wandler Abfrage 
*   neue Funktion PrintLCD_p zur Ausgabe von Strings aus dem Programmspeicher 
*   neue Funktion SetCharLCD zum Setzen von Sonderzeichen 
*   neue Funktion PollSwitchLCD zur Abfrage der Tasten des Arexx LCD 
*   neue Funktion MyMotorSpeed die Korrekturwerte aus der myasuro.h berücksichtigt. 
*   neue Funktion SerPrint_p zur Ausgabe von Strings aus dem Programmspeicher 
*   UART Baudrate einstellbar durch Define 
*   Interrupt User Funktionen für Timer und A/D Wandler 
*   AVR Studio Projektfiles für alle Beispielprojekte <vspace>

###  Version 2.7.1

Datum 17.11.2007 [asuro_libv271.zip][38] 

*   Installationsprogramm vereinfacht (ohne Abfrage ob WinAVR installiert ist) (Autor: m.a.r.v.i.n) 
*   Pfadangaben in Makefiles geändert (Autor: m.a.r.v.i.n) 
*   Projekt Files für AVR Studio und Programmers Notepad (Autor: m.a.r.v.i.n) 
*   PrintFloat Funktion (Autor: M1.R) 
*   Unterstützung der [Ultraschall Erweiterung][37] (Autor: dopez) 
*   kleinere Bugfixes (Variablen volatile gemacht, falls diese in Interruptfunktionen verändert werden) (Autoren: Sternthaler, m.a.r.v.i.n) <vspace>

### Version 2.7.0rc3

Datum 09.04.2007 [v270rc3.zip][39], [v270rc3.exe][40], 

*   I2C Funktionen. I2C Master Emulation (Autor raid_ox) 
*   LCD Funktionen. LCD Modul Anschluss ueber I2C Port Erweiterungs Chip PCF8574 (Autor raid_ox) 
*   RC5 Funktionen. Fernbedienung ueber RC5 kompatibel Fernbedienungen (Autoren: Benjamin Benz, m.ar.v.i.n) 
*   SelfTest Demomode wieder mit IRDemo und RechteckDemo. Demomode startet, wenn nach dem Einschalten eine Taste gedrückt wurde. 
*   teilweise englische Dokumentation (Autoren: MadMan2k, m.ar.v.i.n, raid_ox) <vspace>

### Version 2.7.0rc2

Datum: 20.02.2007 [v270rc2.zip][41], [v270rc2doc.zip][42], 

*   Kommentare zur Doku ueber Doxygen in print.c (Autor Sternthaler) 
*   Funktion PrintLong dazu (Autor HermannSW) 
*   Bugfix: PrintInt für negative Werte (Bugreport HermannSW) 
*   Kommentare zur Doku ueber Doxygen in leds.c, motor.c (Autor Sternthaler) 
*   Kommentare zur Doku ueber Doxygen in encoder.c (Autor Sternthaler) 
*   intro.c fuer Doxygen HTML Doku mainpage (Autor m.a.r.v.i.n) 
*   Kommentare zur Doku ueber Doxygen in adc.c, uart.c, globals.c (Autor Sternthaler) <vspace>

### Version 2.7.0rc1

Datum: 19.01.2007 

*   Umstellung der Asuro Lib auf eine Objekt Library (Autor m.a.r.v.i.n) <vspace>

### Version 2.7.0beta

Datum: 07.01.2007 

*   void Go(int distance, int power) mm Einheit als Wegstreckenangabe (Autor stochri) 
*   void SetMotorPower(int8\_t leftpwm, int8\_t rightpwm ) (Autor stochri) 
*   Funktion zum setzen der PWM Werte, negative Zahlen für Rückwärtsgang. 

Vorteil MotorDir muss nicht getrennt aufgerufen werden, der Entwurf von Reglern vereinfacht sich. 

*   void SerPrint(unsigned char *data) 0-terminierte Strings ausgeben 

man muss nicht mehr die Buchstaben von Hand zählen 

*   void Sound(uint16\_t freq, uint16\_t duration\_msec, uint8\_t amplitude) Einführung einer Sound Funktion (Autor stochri) <vspace>

### Version 2.6.1<vspace>

Datum: 20.11.2006 Bugfixes: (Autor: m.a.r.v.i.n) 

*   PrinInt Funktion: evtl. Fehler beim Flashen mit RS232/IR Transceiver, wg. Folge von 0-Bytes im erzeugten Hex-File. Bug report von francesco 
*   SIGNAL (SIG\_ADC): static Variable toggle initialisiert. Bug report von Rolf\_Ebert. 
*   Warnings entfernt wg. obsolete Header File bei neueren WinAVR Versionen. <vspace>

### Version 2.6<vspace>

Datum 28.09.2005 (Autor: m.a.r.v.i.n) 

*   Doxygen Kommentare. <vspace>

### Version 2.5<vspace>

Datum: 31.07.2005 (Autor: Andun) 

*   Turn() Funktion mit speed Parameter. <vspace>

### Version 2.4<vspace>

Datum: 30.07.2005 Erweiterungen, (Autoren: stochri, Andun) 

*   Go() Funktion 
*   Turn() Funktion. <vspace>

### Version 2.3<vspace>

Datum: 10.06.2005 Anpassungen wg. Umbau der Infrarot Schnittstelle als Kollisionsdetektor (Autor: waste) 

*   count36kHz ersetzt count72kHz. Timer2 geändert. <vspace>

### Version 2.2<vspace>

Datum: 31.03.2005 Erweiterte Funktionen (Autor: weja - Robotrixer Buxtehude) Kurzbeschreibung der Funktionen in der neuen asuro.h, asuro.c vom 31.03.05 Leider konnten die neuen Funktionen nicht mehr in einer Extradatei untergebracht werden, weil mehrere "alte" Funktionen verändert wurden, damit z.B. die Systemzeit integriert werden konnte. Auch wurde die PollSwitch Funktion vom Ballast der Fließkomma-berechnung befreit. Nun ist wieder mehr Platz für eigenen Code vorhanden. <vspace>

*   Encoder_Init() Dieser Befehl installiert die Interrupt Funktion für den automatischen Wegzähler. 
*   Encoder_Start() Startet die automatische Zählung nach 
*   Encoder_Stop() neu. Diese Stopp Funktion hält den Zähler an 
*   Encoder\_Set(int,int) Setzt die Variablen encoder[0] und encoder[1]. Z.B.: Encoder\_Set(0,0) setzt beide Variablen auf Null. 
*   switches ist eine Variable, die, wenn Startswitch() gestartet wurde, auf wahr gesetzt wird, sobald eine Taste gedrückt wurde. gleichzeitig wird die Tastenüberwachung wieder abgeschaltet. Beispiel: <vspace>

Start_Switch();  
while (!switches){;} //wartet auf Tastendruck  
// an dieser Stelle kann mit Pollswitch geprüft werden  
// welche Taste gedrückt wurde, wenn nötig.  
switches=FALSE;Â  // für eine neuen Aufruf von Startswitch() <vspace>

*   Msleep(int) wartet die angegebene Zeit in ms. Z.B warte 10 Sekunden: Msleep(10000); 
*   Gettime() Gibt die Zeit, die seit dem letzten Start des Asuro vergangen ist als unsigned long zurück. Die Angabe erfolgt auch hier in Millisekunden. 
*   PrintInt(int) Eine kleine Ausgabehilfe für Integerwerte. Beispiel Zeilenweise Ausgabe der encoder Werte: <vspace>

PrintInt(encoder[]);  
SerWrite("Â  Â ",3);  
PrintInt(encoder[1]);  
SerWrite("\n\r",2);<vspace>

### Version 2.1<vspace>

Datum: 10.11.2003 

*   Original Version von der ASURO CD (Autor: Jan Grewe - DLR) <vspace>

## Weiterführende Links<vspace>

*   [Roboternetz Thread][43] - ASURO Lib-Erweiterung von Weja 
*   [Roboternetz Thread][44] - ASURO Lib-Erweiterung von Waste (IR) 
*   [Roboternetz Thread][45] - ASURO Lib-Erweiterung von Storchi und Andun (Motorsteuerung) 
*   [Roboternetz Thread][46] - neue Asuro Lib V2.70 (Release Candidate 3) 
*   [Roboternetz Thread][47] - So wird die Asuro-LIB installiert und in Betrieb genommen

 [22]: http://www.sourceforge.net
 [23]: http://www.gna.org
 [24]: https://gna.org/projects/asuro-tools
 [25]: http://sourceforge.net/projects/asuro
 [26]: http://www.asurowiki.de/pmwiki/pub/html/index.html
 [27]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Linienfolger
 [28]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Stromversorgung
 [29]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Odometrie
 [30]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MyasuroH
 [31]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Motorbruecke
 [32]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Tasten
 [33]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Infrarotschnittstelle
 [34]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/I2CPorterweiterung
 [35]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LCDErweiterung
 [36]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RC5DemoC
 [37]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/UltraschallEntfernungsmesser
 [38]: http://www.asurowiki.de/pmwiki/uploads/Main/asuro_libv271.zip
 [39]: http://www.asurowiki.de/pmwiki/uploads/Main/v270rc3.zip
 [40]: http://www.asurowiki.de/pmwiki/uploads/Main/v270rc3.exe
 [41]: http://www.asurowiki.de/pmwiki/uploads/Main/v270rc2.zip
 [42]: http://www.asurowiki.de/pmwiki/uploads/Main/v270rc2doc.zip
 [43]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=7571
 [44]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11114
 [45]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11256
 [46]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=26594
 [47]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=33149

