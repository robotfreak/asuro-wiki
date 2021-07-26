# InfrarotRS232Transceiver

![][1]  
*Der Infrarot RS232 Transceiver*<vspace>

## Einleitung<vspace>

Über den Infrarot RS232 Transceicer wird die Kommunikation zwischen der [Infrarotschnittstelle][2] des ASURO und einem PC hergestellt. Damit lassen sich neue Programme auf den ASURO übertragen (flashen), oder man kann über ein Terminalprogramm mit dem ASURO kommunizieren. Der Infrarot RS232 Transceivcer gehört zum Asuro Bausatz dazu. Dieser muß aber genauso wie der ASURO erst noch zusammengelötet werden. Die Einstellung erfolgt über ein Poti. Eine recht fummlige Arbeit. Mit Notebooks funktioniert der Transceiver oft nicht. Dann hilft nur noch der [Infrarot USB Transceiver][3] oder der Umbau des Transceivers durch Anschluß an ein externes Netzteil. Aber auch an normalen Desktop PCs funktioniert der Transceiver schlecht bis gar nicht. Hier hilft evtl. die [IR Transceiver Modifikation][4]. <vspace>

## Tips<vspace>

*   Die neueste Flasher Software (Version 1.5.1) bei [Arexx][5] herunterladen 
*   Viele Flash Probleme lassen sich auch durch die [IR Transceiver Modifikation][4] beseitigen. Damit gibt es keine CRC Fehler mehr und der IR RS232 Transceiver funktoiniert genausogut wie der [Infrarot USB Transceiver][3]. <vspace>

**Update 15.06.2009:** Durch Bauteiltoleranzen kann es durchaus vorkommen, das die Timerfrequenz überhaupt nicht auf 36kHz eingestellt werden kann. Vielen Dank an M. Jacobs für diesen Hinweis. 

*   Der Empfängerchip SFH5110-36 erwartet als Signal mit Pulsfolgen mit einer Trägerfrequenz von 36kHz. Als Quelle für die 36kHz wird der Chip NE555P verwendet. An Pin 4 werden die Pulse freigegeben. Die Einstellung der richtigen Taktfrequenz mit TR1 ist erheblich einfacher (ein geeignetes Messgerät vorausgesetzt), wenn man einen frei laufenden Takt hat. Das kann durch eine (temporäre) Brücke zwischen Pin 4 und Pin 8 (VCC) des IC1 erreicht werden. Einfachste Realisierung, eine Drahtbrücke auf der Bestückungsseite in den IC-Sockel stecken. So kann man die richtige Frequenz einstellen, ohne die Datenübertragung mühsam mit Minicom oder Hyperterm testen zu müssen. 
*   Die Toleranzen des Kondensators C3 können (zusammen mit parasitären Kapazitäten in der Platine) zur Folge haben, dass die erforderlichen 36kHz nicht eingestellt werden können. Mögliche Maßnahmen (alternativ): 
    *   Verkleinern von C3, z.B. durch 560pF. 
    *   Verkleinern von R5 auf 15kOhm. <vspace>

## Probleme dem IR RS232 Transceiver und deren Lösung<vspace>

auch wenn der Selbsttest des IR RS232 Transceivers noch problemlos funktioniert gibt es doch des öfteren Probleme beim Flashen. <vspace>

### Fehler 'c' und 't' beim Flashen <vspace>

Eigentlich kein Fehler. Einzelne CRC Fehler 'c' und TimeOuts 't' passieren immer wieder. Solange alle Pages geflasht werden und nach dem Brennen die OK Meldung kommt, ist alles in Ordnung. In extrem wenigen Fällen (ist mir bisher 1x passiert) funktioniert das geflashte Programm trotz OK Meldung nicht. Dann sollte man einfach nochmal flashen. <vspace>

### Fehler 'tttttttt' Flash damaged!<vspace>

    Open COM1 --> OK !
     Bulding RAM --> OK !
     Connect to ASURO --> OK !
     Sending Page 000 of 085 --> tttttttttt
     TIMEOUT !
     ASURO dead --> FLASH damaged !! 
    <vspace>

*   Möglicherweise hilft es nochmal vorsichtig am Poti zu drehen. Dabei zwischendurch immer wieder versuchen zu flashen. 
*   Das kann auch passieren, wenn man den ASURO einschaltet und dann erst beim Flasher Programm aud 'Program' klickt. Dazu muß sich das Selbsttest Programm auf dem ASURO befinden. 

Erklärung: Wenn der Selbsttest läuft, sendet der Asuro 

    -- ASURO Testing --
    

Das Wort ASURO kann das Flasher Programm als Connect Meldung mißverstehen. 

*   Der Infrarot Empfänger des ASURO ist defekt. Dann dürfte allerdings auch der Zeichen-Selbsttest nicht funktionieren. (Asuro sendet TTTT und das am Terminal eingegene Zeichen+1 zurück) <vspace>

## Siehe auch <vspace>

*   [IR Transceiver Modifikation][4] - Austausch des Poti gegen Mehrgang Potentiometer. Zusätzlicher Elko am IR Empfänger. <vspace>

## Weblinks<vspace>

*   [Arexx][5] 
*   [Arexx-Henks Website][6] - PP Präsentationen ASURO Flashertool und IR Transceiver Error Finder <vspace>

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/rs232_ir_transeiver.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Infrarotschnittstelle
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/InfrarotUSBTransceiver
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/IRTransceiverModifikation
 [5]: http://www.arexx.com
 [6]: http://home.kpn.nl/h.van.winkoop/Asuro/Info/AsuInfPagFrm.htm

