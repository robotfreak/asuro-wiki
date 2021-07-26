# InfrarotUSBTransceiver

![][1]  
*Der Infrarot USB Transceiver*<vspace>

Der Infrarot USB Transceiver ist optional als Fertigmodul erhältlich. Bei Notebooks deren RS232 Schnittstelle u. U. zu wenig Pegel liefert die einzige Wahl um Programme in den Asuro zu flashen. Funktioniert sehr viel zuverlässiger als der [Infrarot RS232 Transceiver][2]. Das Modul basiert auf dem FTDI232BM Chip von [FTDI][3] <vspace>

Zum Flashen unbedingt die aktuelle Flasher Version (1.5.1) verwenden, zu finden auf der [Arexx Homepage][4] unter Downloads. Diese neue Version verwendet nicht mehr die VCP Treiber (Virtual Com Port) sondern die D2XX Treiber. Deshalb ist es damit auch nicht mehr möglich, über ein normales Terminalprogramm mit dem ASURO zu kommunizieren. <vspace>

Es gibt inzwischen neue Treiber von [FTDI][3] die beide Treibermodelle (VCP und D2XX) unterstützen. Damit kann man dann über den D2XX Treiber mit dem Flasher Tool kommunizieren und über den VCP Treiber mit einem Terminalprogramm (z.B. Hyperterminal). Allerdings darf weiterhin nur eine Applikation gleichzeitig auf die Schnittstelle zugreifen. <vspace>

Ein Terminalprogramm das im D2XX Treibermode funktioniert gibt es weiterhin [hier][5]. <vspace>

### Installations Probleme unter Windows XP<vspace>

Bei der Installation unter Windows XP SP1 kann es u.U. zu Fehlern bei der Installation kommen. Abhilfe schafft hier vor der Installation die Internetverbindung zu schließen. Bei Windows XP SP2 tritt dieses Problem nicht mehr auf. <vspace>

## Bezugsquellen:<vspace>

*   [Conrad][6] 
*   [ELV][7] 
*   [Ja-Ri-TEC][8] 
*   [Wissenschaft Online][9] <vspace>

## Weiterführende Links:<vspace>

*   [FTDI Hersteller des USB Chips][3] <vspace>

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/usb_ir_transceiver.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/InfrarotRS232Transceiver
 [3]: http://www.ftdichip.com/
 [4]: http://www.arexx.com
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/d2xxapp.zip
 [6]: http://www.conrad.com
 [7]: http://www.elv.de
 [8]: http://www.ja-ri-tec.com/
 [9]: http://www.science-shop.de/

