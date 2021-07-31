---
Title: Asuro Eval Board
Template: chapter
Toc: chapter
---

# AsuroEvalBoard

![](%assets_url%/asuro_eval.jpg)  
*Asuro mit Eval Board und Bluetooth Modem*



## Einleitung

Das Asuro Evaluation Board entstand aus der Idee heraus, den Asuro zu einer offenen Plattform auszubauen. Das Hauptmanko des Asuro ist nun mal seine sehr beschränkte Ausbaufähigkeit. Ein weiteres Manko ist das Fehlen einer geregelten Eingangsspannung für die Elektronik. Diese Einschränkungen können mit dem Eval Board aus der Welt geschafft werden. Das Eval Board ist zum leichteren Nachbau auf einer Streifenlochraster Platine mit den Abmaßen 50x80mm (1/4 Europaplatine) aufgebaut. Die Prozessor Ports können auf dem Evaluation Board jetzt mit Hilfe von Steckbrücken und Drähten beliebig mit der Peripherie des Asuros verbunden werden. So kann man zwischen 100% Original Asuro kompatibel und kompletten Neudesign ohne zu löten wählen. Damit kann man z.B. einen neuen Sensor ganz einfach mal am Asuro ausprobieren und bei Nichtgefallen wieder zurücktauschen. Diese Flexibilität muß natürlich auch in der Asuro Software berücksichtigt werden. 

Neben dem Original Atmega8 kann z.B auch ein Atmega168 eingesetzt werden. Dieser hat neben dem doppelten Speicher (16kB Flash) einige nützliche Verbesserungen, ist aber pinkompatibel zum Atmega8. 



## Umbau des Asuro

Wenn man beabsichtigt, den Asuro später wieder in den Originalzustand zurückzubauen, sollt man sich vorher genau überlegen ob man den Umbau vornimmt. 

Die Verbindung zum Asuro wird über den Mikrocontroller Sockel und der Stromversorgung hergestellt. Die notwendigen Änderungen auf der Asuro Platine sind bewußt minimalinvasiv gehalten. Es muß lediglich die Diode D1 und der Jumper JP1 entfernt werden, 2 Leiterbahnen durchtrennt werden und ein zusätzlicher Draht angelötet werden. Zudem ist ein neuer Batteriehalter notwendig, da die Stromversorgung von 4AA Zellen auf 5AA Zellen erhöht wurde. Durch diese Modifikation kann die Elektronik des Asuro jetzt durch einen Spannungsregler mit 5V versorgt werden, während die Motoren bzw. Motortreiber weiterhin direkt aus der Batteriespannung versorgt werden. Dadurch ist eine saubere Trennung gewährleistet. Die Motoren können die Elektronik nicht mehr stören. 

**Achtung!!! Nachtrag vom 24.08.2007:** 

Leider ist die Trennung der Motorbrücken vom Rest der Schaltung nicht ganz so einfach wie gedacht. Das Problem steckt in der Ansteuerung der H-Brücken. Da diese weiterhin mit 5V Pegel arbeiten, werden die Transistoren der Motorbrücken nicht mehr richtig durchgeschaltet bzw. gesperrt. Der vermeintliche Vorteil durch die Trennung der Stromversorgung ist damit dahin. Es kann passieren, dass durch diesen Umbau die Motorbrücken nicht mehr richtig funktioniern oder sogar beschädigt werden. Der einzige Ausweg der ohne größeren Aufwand machbar wäre, ist die Motorbrücken weiter mit über den Spannungsregler mit zu versorgen. 

Wer den Aufwand nicht scheut, kann aber auch die Vorwiderstände R1, R3, R5, R7 der Motorbrücke auslöten und eine Ersatzschaltung dafür aufbauen und einlöten. Im RN-Forum Thread [Asuro mit mehr als 10V auf den Motoren][2] wird von HermannSW erklärt wie das geht. Alternativ könnte man auch gleich die gesamte H-Brücke gegen einen Motortreiber IC wie den L293D ersetzen. 



![](%assets_url%/asuro_umbau2.jpg)
*Jumper und Diode werden ausgelötet*



## Aufbau des Eval Boards

Das Asuro Evaluation Board enthält den Prozessor (Original Asuro oder neuer Atmega8/88/168) mit einer Minimalgrundbeschaltung. Der Resetpin hängt nicht mehr direkt an VCC sondern ist jetzt über einen 10kOhm Pullup Widerstand angeschlossen. Der Prozessor kann entweder über einen eigenen Quarz oder intern mit Takt versorgt werden. Die Verwendung des Resonators vom Asuro Mainboard wäre zwar auch möglich, es empfiehlt sich aber nicht den Takt über so eine große Strecke mit fliegendem Aufbau zu verkabeln. Bei Verwendung des internen Taktes sind 2 weitere Ports zur freien Verwendung übrig. Alle Prozessor Ports sind auf Buchsenleisten geführt. Von dort kann man dann mit einen einfachen Draht eine Verbindung zum Asuro Sockel herstellen, oder den Port anderweitig verwenden. 



![](%assets_url%//asuro_eval2.jpg) 
*Das Asuro Eval Board von oben*



![](%assets_url%/asuro_eval4.jpg)
*Das Asuro Eval Board von der Seite*



### Schnittstellen und Erweiterungen

*   I2C. Über Steckbrücken wird die I2C/TWI Schnittstelle des Prozessors auf eine Steckerleiste geführt (Steckverbinder K10). Die Belegung entspricht dem Devantech SRF08/10 Ultraschallsensor. Damit steht dann ein I2C Bus für Erweiterungen zur Verfügung. Daran können dann z.B. Porterweiterungen, I2C Ultraschallwander Modul, Kompass Modul, Co Prozessor, I2C LCD-Modul etc. angeschlossen werden. Bei der Verwendung derI2C Schnittstelle entfallen aber gleichzeitig die beiden A/D Ports für die Batterieabfrage und die Tastsensoren. 
*   UART. Die UART Pins RX und TX werden über Steckbrücken auf eine 4poligen Buchsenleiste geführt (Steckverbinder K3). Daran kann dann z.B. ein [RS232 Wandler](rs232-wandler), ein [USB-UART Wandler](usb-uart-wandler), ein Funkmodul oder ein [Bluetooth Modem](extensions/bluetooth-modem) angeschlossen werden. Durch den Wegfall der IR Schnittstelle, würde mit PB3 ein weiterer Port zur freien Verfügung. Über diesen Port wird beim Original Asuro die IR Sende LED mit dem 36kHz Trägersignal gepulst. 
*   ISP. Ein 10poliger ISP Steckverbinder ist auf dem Board vorhanden (Steckverbinder K13). ISP ist für den Original Asuro Prozessor ohne Belang, da bei diesem ISP deaktiviert ist, ein neuer Prozessor kann aber darüber programmiert werden. Die Prozessoren vom Typ Atmega88 und Atmeg168 besitzen aber zudem noch ein Debug Interface (DebugWire am Reset Pin) und könnten damit on Board über die ISP Schnittstelle debugged werden. Da an den Leitungen zum ISP Steckverbinder normalerweise nur Ausgänge hängen (Motorbrücke) stört der ISP nicht im normalen Betrieb nicht. 
*   SPI. Der ISP Port kann auch als SPI Port für Erweiterungen benutzt werden. Daran können dann z.B. Porterweiterungen mit Schieberegistern, serielle EEPROMs etc. angeschlossen werden. Dann würde allerdings die Verwendung der Ports als Motorbrücke entfallen. 
*   Frontbuchse. An der 6polige abgewinkelte Buchsenleiste vorne können Erweiterungsmodule, vorzugweise Hindernisdetektoren bzw. Abstandssensoren angebracht werden. Die Belegung der Frontbuchse ist für den Anschluß diverser [Ultraschallsensoren](ultraschall-sensoren) (z.B. Devantech SRFxx, Maxbotix EZ-Sonar EZ1) ausgelegt. Ebenso kann die Infrarot Schnittstelle, umgebaut zum [Infrarot Hindernisdetektor](extensions/infrarot-hindernis-detektor), angeschlossen werden. 
*   Hintere Buchse. An der 3-poligen Buchsenleiste hinten kann z.B ein Infrarot Empfänger angeschlossen werden, der die Signale einer [RC5 Fernbedienung](programmierung/rc5demo) empfangen und damit den Asuro steuern kann. 



### Stromversorgung

Die Original Stromversorgung des Asuro besteht aus 4 Microzellen. Bei der Verwendung von Akkus muß der Jumper JP1 gesteckt sein, damit die Diode D9 überbrückt wird. 4 Microzellen mit einer Zellenspannung von je 1,2V (bei Verwendung von Akkus) sind natürlich zu niedrig um einen Spannungsregler zu verwenden. Dies ergäbe gerade mal 4,8V Eingangsspannung. Deshalb werden beim Asuro Eval Board 5 Zellen benötigt. Dies ergibt eine Eingangsspannung von 6V (bei Verwendung von Akkus). Dazu muß ein spezieller Batteriehalter konstruiert werden. Dieser besteht aus einem 2-Zellen und einem 3-Zellen Mignon Halter, die mit Heisskleber zusammengeklebt werden. 

Die Stromversorgung besteht aus einem Linearregler vom Typ LM2940P (der 'beliebte' 7805 ist bei der niedrigen Eingangsspannung nicht zu empfehlen) und 2 Puffer Elkos. Ein optionaler P-Kanal FET oder eine Shottky Diode vor dem Linearregler schützt die Schaltung vor verpolter Versorgungsspannung. Eine optionale Z-Diode von 5.6V hinter dem Linearregler schützt die Schaltung vor Überspannung. 



![](%assets_url%/asuro_eval_power_schem4.png)
*Asuro Eval Power Supply Schaltplan*

Mit zwei Kabeln wird die Stromversorgung zwischen Asuro und dem Eval Board hergestellt. Über das 2-polige Kabel geht die Batteriespannung hinter dem On-Schalter auf dem Asuro zum Asuro Eval Board (Steckverbinder K9). Vom Eval Board führt dann der 3-polige Stecker (Steckverbinder K11) zurück zum Asuro mit der Batteriespannung (hinter FET bzw. Shottky Diode) die geregelte 5V Versorgung für die Asuro Elektronik (rotes Kabel). Die beiden Masseverbindungen sind mit der Asuro Platine an dem zusätzlichen Odometrie Lötpads angeschlossen. Das braune Kabel wird nicht angeschlossen (siehe Nachtrag vom 24.08.2007). 



![](%assets_url%/asuro_eval_power.jpg)
*Asuro Power Supply Verkabelung. Achtung!!! Fehler im Bild. Anleitung lesen*



### Mindestbeschaltung

Verwendet man den Original Asuro Prozessor, muß zumindest immer der Prozessor Port PC5 zum Asuro Sockel verbunden werden. Der Bootloader prüft über diesen Pin die Batteriespannung, ist diese zu niedrig oder nicht angeschlossen, gibt der Asuro nur 'VL' aus und läßt sich nicht neu programmieren. 



## Schaltplan

![](%assets_url%/asuro_eval_schem4.png)  
*Asuro Eval Board Schaltplan*



![](%assets_url%/asuro_socket_schem4.png) 
*Asuro Eval Socket Schaltplan*



## Bestückungsplan

![](%assets_url%/asuro_eval_front2.jpg)
*Asuro Eval Board Layout Vorderseite*



![](%assets_url%/asuro_eval_back2.jpg)
*Asuro Eval Board Layout Rückseite*



## Stückliste

    Beschreibung						Reichelt Artikel-Nr	Conrad Artikel-Nr
    
    R1	Widerstand 0204, 10k
    R2	Widerstand 0204, 4k7
    R3	Widerstand 0204, 4k7
    C1	Keramik RM2,5, 100nF
    C2	Keramik RM2,5, 100nF
    C3	Keramik RM2,5, 100nF
    C4	Elko 5,5mm, 220 µF
    C5	Elko 5,5mm, 100 µF
    C6	Keramik Kondensator, 22pF
    C7	Keramik Kondensator, 22pF
    D1	RB-100A Schottky  40V/1A, RB-100A Schottky  40V/1A
    Q1	Quarz, 8MHz
    IC1	IC Sockel DIL28 schmal
    IC2	Regler, positiv, LM2940 5V/1A
    IC3	IC Sockel DIL28 schmal
    -	IC-Sandwichleiste, 20-polig, einreihig, H:13,8mm	AW 226/20
    -	IC-Sandwichleiste, 20-polig, einreihig, H:13,8mm	AW 226/20
    
    
    US	Buchsenleiste gewinkelt, 6polig
    UART	Buchsenleiste gerade, 4polig
    IR	Buchsenleiste gerade, 3polig
    PC	Sockelleiste, 6-fach
    PB	Sockelleiste, 6-fach
    PA	Sockelleiste, 5-fach
    PD	Sockelleiste, 5-fach
    -	Sockelleiste, 4-fach
    PB-XTAL	Sockelleiste, 2-fach
    PC-I2C	Sockelleiste, 2-fach
    PD-UART	Sockelleiste, 2-fach
    US-GND	Sockelleiste, 2-fach
    
    I2C	Stiftleiste, 5-polig
    ISP	Stiftleiste, 2x5-polig
    
    UIN	Platinensteckverbinder, gerade 2-polig			PS 25/2G WS
    UOUT	Platinensteckverbinder, gerade 3-polig			PS 25/3G WS
    
    -	Abstandshalter M3 20mm lang Kunststoff
    -	Abstandshalter M3 20mm lang Kunststoff
    



## Software

Will man die flexible Architektur des Eval Boards voll ausnutzen, muß auch die Software entsprechend flexibel ausgelegt sein. Dazu wird die [Asuro Bibliothek](programming/bibliothek) angepaßt, damit Ports schnell umkonfiguriert werden können und einzelne Baugruppen enabled/disabled werden können. Spezielle Konfigurations Files können erzeugt und werden je nach verwendeter Konfiguration mitübersetzt. Für neue Sensoren müssen eigene Bibliotheksfunktionen geschrieben werden, die dann im Makefile dazugelinkt werden. Evtl. wäre ein Codegenerator nützlich, der aus den verschiedenen Konfigurations Files die passende Bibliothek generiert. 



## Downloads

*   [Attach:AsuroEvalBoard.zip][19] | *Asuro Eval Board Schaltplan, Layout, Stückliste und Lochmaster Projekt* 



## Weblinks

*   [RN Forum Tread][2] - Asuro mit mehr als 10V auf den Motoren

 [2]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=28762
 [19]: http://www.asurowiki.de/pmwiki/uploads/Main/AsuroEvalBoard.zip