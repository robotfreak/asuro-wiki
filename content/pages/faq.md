# FAQ


Probleme mit dem Asuro und wie man sie in den Griff kriegt. In der Bedienungsanleitung sind ebenfalls eine Menge an Fehlerquellen erläutert. Unbedingt durchlesen!!! 

## 1.â€‚ Probleme bei der Inbetriebnahme

Vor der Inbetriebnahme sollte man eine sorgfältige Sichtkontrolle durchführen. Ein Multimeter zur Fehlersuche ist unbedingt empfehlenswert. 

### 1.1â€‚ Die Back LEDs leuchten nicht beim ersten Test ohne ICs 

*   Die LEDs glimmen nur ganz schwach. Evtl. muß man dazu den Raum abdunkeln. Wenn das nicht hilft Spannung mit dem Voltmeter nachmessen. 

### 1.2â€‚ Status LED leuchtet nicht gelb beim ersten Einschalten mit Prozessor.

*   vorausgesetzt, dass sich der Original ASURO Prozessor richtig herum im Sockel befindet, sollte die LED nahc dm Einschalten für 3 Sekunden gelb leuchten. 

## 2.â€‚ Probleme beim Flashen

Grundsätzlich sollte man erst versuchen, den ASURO zu flashen, wenn der Selbsttest nach der Inbetriebnahme fehlerfrei funktionierte. Mit fehlerfrei ist gemeint, dass alle Tests die mit der Infrarot Schnittstelle zu tun haben fehlerfrei laufen müssen. 

*   der weiße Blatt Test mit dem IR-RS232-Transceiver. Dieser testet den Transceiver selbst auf korrekte Funktion. 
*   der Zeichen Test am Ende des Selbsttests. Damit testet man den Empfänger auf ASURO Seite. Dabei sendet der ASURO die empfangenen Zeichen um eins erhöht zurück. TTTTTabTTTTTbcTTTTTcdTTTTTdeTTTTTefTTTTT 

Hier hat der Anwender z.B. nacheinander die Tasten 'abcde' gedrückt. Demzufolgende sendet der ASURO als Antwort zwischen den T's 'bcdef'. 

### 2.1â€‚ Fehler viele 'c' und 't' beim Flashen. Flashen funktioniert nicht mit dem IR-RS232-Transceiver

*   serielle Schnittstellen von Notebooks bringen oft zuwenig Pegel auf den Steuerleitungen. Zuwenig, um den IR-Transceiver mit Spannung zu versorgen. Manchmal reicht es für den Selbstest, aber beim Flashen geht es dann nicht mehr. 
*   USB zu Seriell Wandler gehen meißt nicht. Da hier die Steuerleitungen komplett fehlen, un damit der IR-Transceiver keine Versorgungsspannung hat. 
*   Die Reichweite ist nicht allzu hoch (<50cm). Beim Programmieren den IR-Transceiver am besten möglicht nahe direkt über den ASURO halten. 
*   Die Infrarotschnittstelle reagiert sehr empfindlich auf Fremdlichteinstreuung, z.B. durch Halogenstrahler o.ä. 
*   Widerstandswerte auf ASURO- oder IR-Transceiver Seite überprüfen 
*   IR-LEDs lassen sich mit einem Foto-Handy oder DigiCam überprüfen. 
*   Umbau des [IR RS232 Transceivers][35] durchführen 
*   R17 auf dem Asuro hat 470Ohm. Laut Datenblatt sollten dies 100Ohm sein. Wechseln. 

### 2.2â€‚ gelegentlich Fehler 'c' und 't' beim Flashen 

*   Eigentlich kein Fehler. Einzelne CRC Fehler 'c' und TimeOuts 't' passieren immer wieder. Solange alle Pages geflasht werden und nach dem Brennen die OK Meldung kommt, ist alles in Ordnung. In extrem wenigen Fällen (ist mir bisher 1x passiert) funktioniert das geflashte Programm trotz OK Meldung nicht. Dann sollte man einfach nochmal flashen. 

### 2.3â€‚ Fehler 'tttttttt' Flash damaged!

    Open COM1 --> OK !
     Bulding RAM --> OK !
     Connect to ASURO --> OK !
     Sending Page 000 of 085 --> tttttttttt
     TIMEOUT !
     ASURO dead --> FLASH damaged !! 
    

*   Möglicherweise hilft es nochmal vorsichtig am Poti zu drehen. Dabei zwischendurch immer wieder versuchen zu flashen. 
*   Das kann auch passieren, wenn man den ASURO einschaltet und dann erst beim Flasher Programm aud 'Program' klickt. Dazu muß sich das Selbsttest Programm auf dem ASURO befinden. 

Erklärung: Wenn der Selbsttest läuft, sendet der Asuro 

    -- ASURO Testing --
    

Das Wort ASURO kann das Flasher Programm als Connect Meldung mißverstehen. 

*   Der Infrarot Empfänger des ASURO ist defekt. Dann dürfte allerdings auch der Zeichen-Selbsttest nicht funktionieren. (Asuro sendet TTTT und das am Terminal eingegene Zeichen+1 zurück) 

### 2.4â€‚ Fehler 'VL' beim Flashen 

Das bedeutet Voltage Low, und deutet auf eine zu niedrige Batteriespannung hin. Der ASURO Bootloader prüft beim Flashen über einen A/D Port die Batteriespannung, genauer gesagt die Spannung an einem Spannungsteiler gebildet durch die Widerstände R12 u. R13. 

*   als erstes also Batteriespannung VCC überprüfen. 
*   ist die Battereispannung i.O. liegt wohl noch eine Hardware Fehler vor. In diesem Fall die Widerstanswerte von R12 (12kOhm) u. R13 (10kOhm) überprüfen, die den Spannungsteiler bilden. Zudem kommt noch R11 (100Ohm) in Frage, der in Reihe zwischen VCC und V+ Spannung. Widerstände unbedingt bei ausgeschaltetem Bot messen. 

### 2.5â€‚ Fehler 'v' beim Flashen 

Ein 'v' beim Flashen bedeutet, dass ein Verify Fehler aufgetreten ist. Das Datenpaket wurde zwar fehlerfrei empfangen und in den Speicher geflasht. Beim anschließenden Vergleich wurde ein Unterschied festgestellt. 

*   meißt ein sehr schwer wiegender Fehler, wenn der Prozessor viele Male geflasht wurde. Da hilft nur Austausch des Prozessors. Tritt der Fehler bereits nach wenigen Flash Versuchen auf, ist das ein Fall für den Arexx Support. 
*   der fehler kann aber auch bei bestimmten Programmen auftreten. Evtl. führt eine längere Folge von 0-Bytes im Programm zu diesem Problem. So passierte dies auch schon bei meinen beiden Asuros. Ein anderes Programm ließ sich dann wieder problemlos flashen. 

### 2.6â€‚ Flashen funktioniert nicht mit dem IR-USB-Transceiver

*   neueste Version des Flasher Programms (V1.51) <http://www.arexx.com> und aktuelle USB-Treiber (V2.04) von <http://www.ftdichip.com> installieren. Die neuen USB-Treiber (CDM) enthalten nämlich beide Varianten von Treibern VCP und D2XX. Damit ist es nun möglich mit dem Flasher Tool über den D2XX Treiber zu flashen und bei Hyperterminal über den VCP Treiber (virtueller COM Port) mit dem ASURO zu kommunizieren. Allerdings nur 1 Anwendung gleichzeitig. 
*   Bei XP SP1 während der Installation des USB-Treiber die Internet Verbindung deaktivieren. 

### 2.7â€‚ Flashen funktioniert nicht mit einem USB-RS232 Wandler

*   Viele neue PCs und Notebooks besitzen keine serielle Schnittstelle. Sogenannte USB-RS232 Wandler aus dem Zubehör Handel versprechen Abhilfe. Leider funktioniert das mit den meisten USB-RS232 Wandler nicht, da diese die Steuerleitungen nicht umsetzen. Die Steuerleitungen werden vom IR-RS232 Adapter zur Stromversorgung benötigt. 
*   Wenn man Glück hat und einen USB-RS232 Wandler findet mit dem zwar das Terminalprogramm funktioniert, nicht aber das Asuro Flasher Tool, dann kann das AllInOne Flasher IDE Tool von Osser hilfreich sein. Damit klappt dann auch das Flashen. Das AllInOne Tool ist Bestandteil der aktuellen [Asuro Bibliothek][36] (Exe Version) 

## 3.â€‚ Odometrie Probleme

### 3.1â€‚ Odometrie A/D Wandler Werte schwanken zu stark

*   Fremdlichteinstreuung stören die Messung. Abhilfe gegen Umgebungslicht schafft das Anbringen einer Abdeckung aus Papier über IR-Led und Fototransistor. 
*   Die Zahnräderd haben zu viel Spiel auf der Achse, womit sich der Abstand zu den Sensoren ändert. Die Zahnräder kann man mit einer aufgeklebten Unterlegscheibe etwas stabilisieren. 

### 3.2â€‚ Ein Rad zählt überhaupt nicht, oder es gehen viele Werte verloren

*   Die Grenzwerte für Hell/Dunkel in der [Asuro Bibliothek][36] müssen angepaßt werden. 

### 3.3â€‚ PollSwitch Aufrufe stört die Encoder Abfrage im Interrupt Betrieb

*   Aufruf der PollSwitch Funktion führen zu falschen Ergebnissen bei den Encoder Werten, wenn diese im Interrupt Betrieb abgefragt werden. Leider noch keine Lösung in Sicht (known Bug der AsuroLib) 

## 4.â€‚ Taster Probleme

### 4.1â€‚ Es wird immer ein Wert ausgegeben, obwohl keine Taste gedrückt wurde oder

### 4.2â€‚ Es wird nach drücken einer Tasten noch ein paar mal der Wert 1 ausgegeben.

*   Hier hilft das mehrmalige (2x oder 3x) Abfragen der PollSwitch() Funktion und der anschließende Vergleich ob beides mal der 

gleiche Wert zurückgegeben wurde. 

*   Ansonsten liegt ein Kurzschluss an dem entsprechenden Taster oder dem zugehörigen Widerstand vor. 

### 4.3â€‚ Die ausgegebenen Werte sind vertauscht

*   Die den Tastern zugeordneten Widerständen wurden verwechselt. 

### 4.4â€‚ Die ausgegebenen Werte für K1, K2, K3 stimmen nicht

*   Manchmal werden abweichende Werte für K1 (31 oder 33) bzw K2 (15 oder 17) bzw. K3 (7 oder 9) beim Testprogramm ausgegeben. Das Problem läßt sich durch Anpassung der [Asuro Bibliothek][36] beheben. Die letzte Zeile in der PollSwitch() Funktion lautet: 

return ((10240000L/(long)i-10000L)*61L+5000L)/10000; Den Wert 61L probeweise mit 62L, 63L, 64L oder 65L ersetzen und jeweils damit das Testprogramm neu übersetzen und ausprobieren. 

*   In der aktuellen Asuro Bibliothek (ab V2.7) wird diese Änderung in der Datei myasuro.h vorgenommen. Anschließend muss die Asuro Bibliothek neu übersetzt werden. 

### 4.5â€‚ beim Selbsttest läuft beim Drücken der Taste K1 der linke Motor mit

Hier hilft ebenfalls die Anpassung der PollSwitch Funktion. Siehe oben. 

## 5.â€‚ Probleme beim Übersetzen

### 5.1â€‚ Fehlermeldung 'Colon expected...' erscheint nach dem Aufruf von make

*   folgende Fehlermeldungen erscheinen nach dem Aufruf von make 

    MAKE Version 5.2  Copyright (c) 1987, 2000 Borland
     Error makefile 223: Colon expected
     Error makefile 248: Too many rules for target '%.o'
     Error makefile 284: Command syntax error
     *** 3 errors during make ***
    

In diesem Fall stimmen die Pfadangaben der Windows Umgebung nicht. Anstatt des GNU-Make wird das Make Programm von Borland aufgerufen. Überprüfen Sie in diesem Fall die Pfadangaben von Windows. Der Pfad zum WinAVR Compiler `C:\WinAVR\bin` sollte am Anfang stehen. 

### 5.2â€‚ Fehlermeldung 'No rule to make target' erscheint nach dem Aufruf von make

    make: *** No rule to make target `../../lib/asuro.c', needed by `asuro.d'.  Stop.
    

*   Entweder stimmen die Pfadangaben nicht und die Quelldatei wird deshalb nicht gefunden. 
*   Falls die Pfadangaben korrekt sind und trotzdem die Fehlermeldung kommt hilft es meist die dependency Files von Hand aus dem entsprechenden Ordner löschen. Diese wurden vielleicht aus einem anderen Ordner mitkopiert. 

    del *.d
    

### 5.3â€‚ Fehlermeldung 'Der Befehl "make" ist entweder falsch geschrieben...' erscheint nach dem Aufruf von make

    make 
     Der Befehl "make" ist entweder falsch geschrieben oder
     konnte nicht gefunden werden.
     > Process Exit Code: 1 
    

*   In diesem Fall ist der WinAVR Compiler nicht oder nicht richtig installiert. Es fehlen die Pfadangaben in den Umgebungsvariablen. 
    *   Entweder WinAVR Setup nochmals starten, (mit Administrator Rechten). Bei der Installation darauf achten, das im Dialog 'Install Options' das Häkchen bei 'Add Directories to PATH' angeklickt ist. 
    *   Die Pfadangaben von Hand eingeben. Unter 'Systemsteuerung' 'System' den Reiter 'Erweitert' anwählen und auf 'Umgebungsvariablen' klicken. Dann unter Systemvariablen die Zeile 'Path' auswählen und auf 'Bearbeiten' klicken. Folgende Verzeichnisse am Anfang dazufügen (wenn WinAVR unter C:\WinAVR installiert wurde) 

    C:\WinAVR\bin;C:\WinAVR\utils\bin;
    

## 6.â€‚ Probleme mit der [Asuro Lib][36]

### 6.1â€‚ Asuro Lib V2.60 oder älter. Warnung beim Übersetzen 

Beim Compilieren von Programmen kommt immer folgende Warnung: 

    avr/include/avr/signal.h:36:2: warning: #warning "This header file is obsolete. Use <avr/interrupt.h>."
    

Bei neueren WinAVR Versionen wurde die Headerdatei 'signal.h' durch 'interrupt.h' ersetzt. Deshalb die Warnung. Die Datei 'signal.h existiert zwar noch, sollte aber nicht mehr verwendet werden. Einfach im File 'asuro.h' Die Zeile #include <avr/signal.h>  Durch folgende ersetzen. 

#include <avr/interrupt.h>  Ab der Asuro Lib V2.61 ist diese Änderung bereits gemacht. 

### 6.2â€‚ Asuro Lib 2.70RC3. Fehlermeldung 'WinAVR is not installed' 

Beim Installieren der Asuro Lib über die setup.exe kommt die Fehlermeldung 'WinAVR is not installed'. Das Setup Programm sucht bei der Installation der Asuro Lib nach dem Registry Eintrag 

    "Software\Free Software Foundation\WinAVR" "GCC"
    

Falls dieser Eintrag nicht vorhanden ist, kommt die obige Fehlermeldung. Trotzdem kann die Installation erfolgreich abgeschlossen werden. Allerdings muss danach das Makefile für die Lib von Hand umbenannt und evtl angepaßt werden. 

*   Die Datei 'Makefile.orig' im Ordner 'C:\ASURO_SRC\AsuroLib\lib' muß in Makefile umbenannt werden. 
*   Falls WinAVR in einem anderen Verzeichnis als C:\WinAVR installiert wurde, muß dieser Verzeichnisname im Makefile an folgender Stelle geändert werden. 

    DIRAVR = C:/WinAVR
    

### 6.3â€‚ Asuro Lib 2.70RC3. Fehlermeldung beim Compilieren

Beim Compilieren von Programmen kommt die Fehlermeldung 

    ..\..\..\avr\bin\ld.exe: cannot find -lasuro  
    

In diesem Fall ist die Asuro Lib nicht korrekt übersetzt und installiert worden. 

*   Im Ordner 'C:\ASURO_SRC\AsuroLib\lib' die Batch-Datei make_lib.bat ausführen. Dadurch sollte die Asuro Lib neu übersetzt und in das WinAVR Lib Verzeichnis 'C:\WinAVR\avr\lib' kopiert werden. 

## 7.â€‚ Probleme mit dem LCD Modul 

### 7.1â€‚ Keine oder sehr schwache Anzeige.

Im Asuro Buch II ist in der Stückliste zum LCD Modul ein falscher Widerstandwert für R11 angegeben. 15kOhm anstelle von 22 kOhm wie richtigerweisde im Schaltplan. Das kann dazu führen, das das Display nichts, oder fast nichts anzeigt. Trotz Drehen am Poti bekommt man keine ausreichende Kontrasspannung. 

### 7.2â€‚ Kontaktprobleme

Man sollte das LCD Mosul aus dem Asuro Buch II auf einem Sockel mit Präzisionsstiften setzen, sonst kann es zu Kontaktproblemen führen. 

### 7.3â€‚ Die Beispiel aus dem Asuro Buch II funktionieren nicht (Fehlerhafte Anzeigen)

Die [[[Attach:LCDexamples.zip][37]| LCDexamples.zip] aus dem Asuro Buch funktionieren nicht mit mit aktuellen WinAVR Version (ab 2008). Es kommt zu Anzeigefehlern (kryptische oder falsche Zeichen). Wahrscheinlich irgendein Optimierungs Problem. Die LCD Beispiele der AsuroLib funktionieren ohne Probleme.

 [1]: javascript:toggle('tocid');
 [2]: #toc1
 [3]: #toc2
 [4]: #toc3
 [5]: #toc4
 [6]: #toc5
 [7]: #toc6
 [8]: #toc7
 [9]: #toc8
 [10]: #toc9
 [11]: #toc10
 [12]: #toc11
 [13]: #toc12
 [14]: #toc13
 [15]: #toc14
 [16]: #toc15
 [17]: #toc16
 [18]: #toc17
 [19]: #toc18
 [20]: #toc19
 [21]: #toc20
 [22]: #toc21
 [23]: #toc22
 [24]: #toc23
 [25]: #toc24
 [26]: #toc25
 [27]: #toc26
 [28]: #toc27
 [29]: #toc28
 [30]: #toc29
 [31]: #toc30
 [32]: #toc31
 [33]: #toc32
 [34]: #toc33
 [35]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/IRTransceiverModifikation
 [36]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [37]: http://www.asurowiki.de/pmwiki/uploads/Main/LCDexamples.zip

