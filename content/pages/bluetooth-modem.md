# BluetoothModem

![][1]<vspace>

## Einleitung<vspace>

Bluetooth ist eine von der Firma [Ericsson][2] entwickelter Schnittstelle zur drahtlosen Vernetzung von Geräten über kurze Distanz. Der Name Bluetooth entstammt vom dänischen Wikingerkönig Harald Blauzahn (engl. Bluetooth). <vspace>

## BlueSMiRF Bluetooth Modem<vspace>

Das BlueSMiRF Bluetooth Modem der Firma BlueRadios ist ein Class 1 Bluetooth Gerät mit einer Reichweite von 100m im Freien (50m in Gebäuden). Der Anschluß an das [Asuro Eval Board][3] bzw. die [Asuro Erweiterung][4] gestaltet sich einfach, da der UART Steckverbinder auf dem Eval Board/ Erweiterungsboard schon die richtige Pin Belegung hat. In der Stromversorgung erweist sich das Modem sehr flexibel. 3-10V Eingangsspannung genügen, der Stromverbrach liegt bei 40mA im Sendebetrieb und 2mA im Standby Mode. <vspace>

Das BlueSMiRF Modem stellt als Profil in der Bluetooth Umgebung das **S**erial **P**ort **P**rofile (SPP) zur Verfügung. Dadurch stellt sich die Bluetooth Verbindung zwischen PC und dem Asuro wie eine Kabelverbindung dar. Zwei LEDs auf dem BlueSMiRF zeigen den Betriebszustand an. Grün blinkend heißt, keine Verbindung. Rot dauerleuchtend bedeutet, Verbindung OK. <vspace>

Leider gibt es bisher keinen Distributor in Deutschland für das BlueSMiRF Modem. Ich selbst habe mein Exemplar in USA bei [SparkFun][5] bestellt. Mit einem Preis von 60$ ist das Bluetooth Modem nicht gerade billig, und damit sogar teuerer als der komplette Asuro Bausatz. <vspace>

## Inbetriebnahme<vspace>

Das BlueSMiRF arbeitet grundsätzlich mit Hardware Handshake. Deshalb sind auf dem Steckverbinder neben VCC, GND TX und RX auch die Steuerleitungen CTS und RTS herausgeführt. Werden die Steuerleitungen nicht benötigt, kann man diese auch einfach auf der Lötseite der Platine (JP1) mit einem Lötklecks zusammen verbinden. <vspace>

### Steckerbelegung<vspace>

| **Pin** | **Name** | **Beschreibung**                           |
||
| 1       | CTS      | Clear To Send                              |
| 2       | PWR      | Power VCC 3..10V                           |
| 3       | GND      | Ground                                     |
| 4       | TX       | Transmit. Verbunden mit RX des Controllers |
| 5       | RX       | Receive. Verbunden mit TX des Controllers  |
| 6       | RTS      | Ready To Send                              |<vspace>

Vor der Erstinbetriebnahme muß die Baudrate des BlueSMiRF Modems eingestellt werden. Dies geschieht über AT Befehle, ähnlich den Einstellungen gängiger Modems. Damit die Einstellungen auch nach dem Abschalten erhalten bleiben, müssen diese in den Flash programmiert werden. <vspace>

### AT Befehlsübersicht<vspace>

Die wichtigsten AT Befehle des BlueSMiRF Modems. Gültige Befehle quittiert das Modem mit OK. 

    '+++<cr>' - So gelangt man in den Eingabe Modus (Eingabe ohne Hochkommas). Das Bluetooth Modem quittiert mit 'OK'.
     'ATVER,ver1<cr>' - Das Modem liefert seine Firmware Version zurück 'Ver 3.5.1.1.0' bei meinem Modem
     'ATSI,<n><cr>' - System Informationen. n ist eine Zahl zwischen 0..20.
     'ATSI,1<cr>' liefert z.B. den Product ID Code, bzw. die Bluetooth Adresse
     'ATSW20,,<baudrate>,<parity>,<stopbits>,<store><cr> - UART Einstellungen. Die Anazhl der Datenbits ist 8 und kann nicht 
     geändert werden. Wenn man als letzte Zahl eine 1 angibt, werden die Einstellungen permanet gespeichert. Gibt man eine 0 an,
     bleiben die Einstellungen nur bis zum Ausschalten aktiv. Ändert man die Baudrate bekommt man kein 'OK'. 
     Die Einstellungen werden sofort aktiv, man muß jetzt die Baudrate im Terminalprogramm entsprechend ändern.
     'ATSW20,10,0,0,0<cr> schaltet das Modem auf 2400Baud, no parity, 1 Stopbit, temporär auf die Standard Einstellungen des ASUROs. 
     'ATSW20,10,0,0,1<cr> schaltet das Modem auf 2400Baud, no parity, 1 Stopbit, permanent auf die Standard Einstellungen des ASUROs. 
     'ATMD<cr> schaltet das Modem zurück in den Daten Modus.
    <vspace>

### Verbindungsaufbau<vspace>

Ein Click auf die Bluetooth-Umgebung zeigt die vorhandenen Bluetooth Geräte. Falls das BlueSMiRF Modem nicht angezeigt wird, hilft eine erneute 'Suche nach Geräten in Reichweite'. <vspace>

![][6]  
*Bluetooth Übersicht der angeschlossenen Geräte*<vspace>

Ein Doppelclick auf das BlueRadio Symbol zeigt die verfügbaren Diensate an. Das BlueSMiRF verfügt lediglich über den Dienst 'COM-Schnittstelle' Beim Allerersten Connect mit dem BlueSMiRF muß ein Passwort eingegeben werden. Dieses lautet **'default**'. Danach kann man sich mit dem Modem verbinden. Beim Starten einer Applikation wie z.B. 'Hyperterminal' wird die Verbindung dann automatisch aufgebaut. Die rote LED am BlueSMiRF zeigt eine bestehende Verbindung an. <vspace>

![][7]  
*BlueSMiRF ohne Verbindung*<vspace>

![][8]  
*BlueSMiRF mit Verbindung*<vspace>

## Programme flashen über Bluetooth<vspace>

Das Programmieren über Bluetooth ist mit dem Original Asuro Bootloader derzeit nicht möglich. Zum einen reicht die Zeit von 1 Sekunde nach dem einschalten nicht, das Bluettoth Modem zu initialisieren. Man müßte also einen Reset Schalter vorsehen, um den Asuro zu reseten (damit er den Bootlader anspringt), ohne die Spannung wegzunehmen. Ob das Timing generell zum Programmieren ausreicht, muß noch untersucht werden. <vspace>

## Links<vspace>

*   [Wikipedia][9] 
*   [BlueRadios Herstellersite][10] 
*   [BlueSMiRF Datenblatt][11] 
*   [SparkFun - BlueSMiRF Distributor][5] 
*   [www.roboterclub-freiburg.de][12] - Bluetooth Asuro

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/bluesmirf1.jpg ""
 [2]: http://www.ericsson.com
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroEvalBoard
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroErweiterung
 [5]: http://www.sparkfun.com
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/bluetooth4.jpg ""
 [7]: http://www.asurowiki.de/pmwiki/uploads/Main/bluetooth5.jpg ""
 [8]: http://www.asurowiki.de/pmwiki/uploads/Main/bluetooth6.jpg ""
 [9]: http://de.wikipedia.org/wiki/Bluetooth
 [10]: http://www.BlueRadios.com
 [11]: http://www.sparkfun.com/datasheets/RF/BlueSMiRF_v1.pdf
 [12]: http://www.roboterclub-freiburg.de/asuro/hardware/bluetooth/bluetoot

