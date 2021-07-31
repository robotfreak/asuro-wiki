# Infrarotschnittstelle

![][1]  
*Infrarot Schnittstelle*

## Funktionsweise:

Die Infrarot Schnittstelle beim ASURO wird über IC2 und die IR-LED D10 gebildet. IC2 ist der Infrarot Empfänger Chip SFH 510-36. Der Ausgang des Chips geht an Prozessor Port PD0, der als UART RxD konfiguriert ist. Die IR-LED hängt zwischen Pin PD1 und PB3. PD1 ist als UART TxD konfiguriert, während über PB3 ein 36kHz Signal als IR-Trägersignal dem gesendeten Signal zugemischt wird. 

Über die Infrarot Schnittstelle kann der ASURO mit einem PC kommunizieren. Auf PC Seite ist dazu ein [Infrarot RS232 Transceiver][2] (gehört zum Bausatz) oder ein [Infrarot USB Transceiver][3] (optionales Zubehör) notwendig. Leider ist die Reichweite der IR-Schnittstelle mit ca. 50cm nicht allzu hoch. 

Durch die IR-Schnittstelle wird der ASURO auch programmiert. Die Prozessor Ports der ISP (**I**n **S**ystem **P**rogramming) Schnittstelle sind beim ASURO leider nicht auf einen ISP Stecker geführt und zudem ist die ISP Scnittstelle über die Fuse Bits disabled. Die Programmierung über die IR-Schnittstelle wird durch das [Bootloader][4] Programm ermöglicht. Dieses Programm liegt in einem geschützten Bereich des ASURO und wird nach dem Einschalten gestartet. 

## Einstellungen

*   2400 Baud 
*   no Parity 
*   8 Databit 
*   1 Stoppbit 

## Besondere Verwendung der IR Schnittstelle

### RC5 Empfänger

Die Infrarotschnittstelle kann auch zum Empfang von RC5 Signalen benutzt werden, wie sie z.B. einige Infrarot Fernbedienungen aussenden. So läßt sich der Asuro bequem fernsteuern, da die Reichweite einer IR Fernbedienung sehr viel weiter als die PC Schnittstelle (einige Meter gegenüber wenigen cm bei der PC Schnittstelle). Näheres hierzu siehe unter [RC5DemoC][5]. 

### Kollisionserkennung

Die Infrarotschnittstelle läßt sich auch zur [Kollisionserkennung][6] einsetzen. Dazu ist eine Modifikation des ASURO notwendig. 

### Näherungsschalter

Die Infrarotschnittstelle läßt sich auch als Näherungsschalter benutzt werden. Bringt man seine Hand oder einen Gegenstand in die Nähe der ASURO Infrarotschnittstelle, kann dies der ASURO feststellen und darauf reagieren. Bei einem [ASURO Rätsel][7] aus dem Roboternetz wird dies z.B. eindrucksvoll gezeigt. 

## Probleme mit der IR-Schnittstelle:

*   Die Reichweite ist nicht allzu hoch. Beim Programmieren den IR-Transciever am besten direkt über den ASURO halten. 
*   Empfindlich für Fremdlichteinstreuung. Z.B. durch Halogenstrahler o.ä. 

## Verbesserungsvorschläge:

*   Reichweiten Erhöhung der IR Schnittstelle durch einen Reflektor für die IR-LED. 
*   Besser noch den Strom durch die IR-LED mit einem Transistor erhöhen. Da das Signal gepulst ist, verträgt die IR-LED auch ein paar hundert mA. 
*   Eventuell eine oder mehrere IR-LEDs parallel schalten. 
*   Das Standard Poti auf dem RS232 IR Transceiver durch ein Präzisions Poti ersetzen. Siehe hierzu . 

## Weiterführende Links:

*   [Roboternetz Thread][8] - Asuro - IR323 problem 
*   [Roboternetz Thread][9] - Bug in Flash-Progr für Asuro und Win98 
*   [Roboternetz Thread][10] - Umbau der IR-Schnittstelle zur Hinderniserkennung 
*   [SFH5110 Datenblatt][11] 

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/ir_interface.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/InfrarotRS232Transceiver
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/InfrarotUSBTransceiver
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bootloader
 [5]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RC5DemoC
 [6]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/InfrarotHindernisdetektor
 [7]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=23614
 [8]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=10804
 [9]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?p=71762
 [10]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11114
 [11]: http://www.ortodoxism.ro/datasheets/infineon/2-SFH5110.pdf

