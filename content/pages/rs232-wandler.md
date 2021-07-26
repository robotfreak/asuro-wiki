# RS232Wandler

![][1]  
RS232-Modul [Dieses Bild bei Flickr][2]<vspace>

Für das Asuro Eval Board und die Asuro Erweiterung kann dieses RS232 Pegelwandler Modul verwendet werden. Es wandelt die 5Volt TTL Signale der Mikroprozessor UART in RS232 kompatible Signalbereiche von -12V..+12V. Über dieses Modul kann der ASURO mit der COM Schnittstelle eines PCs verbunden werden. (Auf keinen Fall sollte man dies ohne Pegelwandler Modul durchführen) Das RS232 Modul besteht aus dem üblichen MAX232/202 Pegelwandler Chip. Die Werte für die Kondensatoren C1..C4 hängen vom verwendeten Wandler Chip ab. Beim MAX202 reichen z.B. schon 0.1µF Kondensatoren aus. <vspace>

### Schaltplan <vspace>

![][3]<vspace>

### Steckerbelegung<vspace>

Die Steckerbelegung des 6poligen Steckbverbinders ist diesselbe wie beim [Bluetooth Modul][4]. <vspace>

| **Pin** | **Name** | **Beschreibung**                                             |
||
| 1       | CTS      | Clear To Send                                                |
| 2       | PWR      | Power VCC 3..10V                                             |
| 3       | GND      | Ground                                                       |
| 4       | RX-O     | Transmit Output. TTL Pegel. Verbunden mit RX des Controllers |
| 5       | TX-I     | Receive Input. TTL Pegel. Verbunden mit TX des Controllers   |
| 6       | RTS      | Ready To Send                                                |<vspace>

Der 3polige PSK Stecker führt neben RxD und TxD mit RS232 Pegel nur noch GND als Massesignal. <vspace>

| **Pin** | **Name** | **Beschreibung**                                                        |
||
| 1       | TX-O     | Transmit Output. RS232 Pegel. Verbunden mit Pin2 (RxD) der D-SUB Buchse |
| 2       | GND      | Ground. Verbunden mit Pin5 der D-SUB Buchse                             |
| 3       | RX-I     | Receive Input. RS232 Pegel. Verbunden mit Pin3 (TxD) der D-SUB Buchse   |<vspace>

Zum Anschluß an den PC ist zudem noch ein 3adriges Kabel notwendig. Auf der einen Seite wird die 3polige PSK Buchse angecrimpt (oder eine 3polige Buchsenleiste angelötet). Auf der anderen Seite wird an das Kabel dann eine 9-polige D-SUB Buchse angelötet. <vspace>

![][5]<vspace>

## Weblinks<vspace>

*   [Wikipedia][6] EIA-RS232 Artikel 
*   [RN-Wissen][7] - RS232 Artikel <vspace>

 [1]: http://farm3.static.flickr.com/2275/2129824702_93e4c68df2_b.jpg ""
 [2]: http://www.flickr.com/photos/hmblgrmpf/2129823200/
 [3]: http://www.asurowiki.de/pmwiki/uploads/Main/rs232-adapter_m.png ""
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/BluetoothModem
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/rs232-kabel.png ""
 [6]: http://de.wikipedia.org/wiki/EIA-232
 [7]: http://www.roboternetz.de/wissen/index.php/RS232

