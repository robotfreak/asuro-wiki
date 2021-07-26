# Bootloader

## Einleitung<vspace>

Ein Bootloader ist also ein kleines Programm, das den Controller und die Hardware soweit initialisiert, dass eine Kommunikation über die serielle Schnittstelle möglich ist und die Flash Bereiche geschrieben und gelesen werden können. Das Bootloaderprogramm wartet eine gewisse Zeit, ob über die serielle Schnittstelle eine bestimmte Zeichenfolge empfangen wird. Wird diese Zeichenfolge empfangen startet der Download Prozess zum Empfang und Flashen eines neuen Applikationsprogramm. Wird keine entsprechende Zeichenfolge empfangen startet der Bootloader das vorhandene Applikationsprogramm. <vspace>

Beim Power On des Prozessors sorgenn spezielle Fusebits (BOOTSZ0, BOOTSZ1, BOOTRST) dafür, ob der Prozessor mit der Verarbeitung ab Adresse 0x0000 beginnt (ohne Bootloader) oder zur Einsprungadresse des Bootloaders springt und dort das Bootloader Programm abarbeitet. BOOTSZ0 und BOOTSZ1 legen die Einsprungadresse für den Bootloader fest (256..1kWorte). Zu beachten ist, das in der Beschreibung der Fusebits im ATmega Datenblatt eine Wortadresse angegeben ist. ein Wort entspricht dabei einem 16Bit wert. Entsprechend muß man die angebebenen Wortadressen und Bootloader Größen mit 2 multiplizieren um auf die Byteadresse bzw. Bytegröße zu kommen. Die BOOTRST Fuse legt fest ob nach Power On bzw. Reset der Bootloader angesprungen wird, oder das Applikationsprogramm. <vspace>

Der Bootloader befindet sich am Ende des Flash Bereiches und belegt beim Asuro 1kB des Flashspeichers. 7kB sind somit für Anwenderprogramme frei. Wobei natürlich 7kB Binärprogramm gemeint sind und nicht Sourcecode Größe, auch die Größe des erzeugten [Hex-Files][1] sagt nicht viel über die Größe im Binärcode aus, weil das [Hex-File][1] in einem ASCII Format vorliegt ( ein Binärbyte entspricht dabei 2 ASCII Byte) und zusätzliche Informationen wie Adressen und Checksummen ebenfalls im ASCII Format darinstehen. <vspace>

## Asuro Bootloader<vspace>

Beim Asuro ist die Programmierung (Übertragen der [Hexfiles][1] in den Controller) nur über einen Bootloader möglich. Dazu wird das kompilierte und gelinkte Programm über die serielle Schnittstelle des Controllers in den Flash Bereich geschrieben. Das ist aber nur möglich weil sich der Bootloader bereits in einem speziell geschützten Bereichs des Controller Flash befindet. Deshalb ist es auch ohne weiteres nicht möglich, den Original Controller auf dem Asuro gegen eine neuen auszutauschen, da dort der Bootloader fehlt. Der vorhandene Bootloader läßt sich auch nicht auslesen. Falls der Original Prozessor des Asuros einmal seinen Geist aufgibt, bleiben nur die Möglichkeiten sich einen neuen Prozessor mit Bootloader bei Arexx zu bestellen, oder einen anderen Prozessor ohne Bootloader zu kaufen und mit einem alternativen Bootloader zu betreiben. Allerdings muß dazu der Bootloader zuert einmal mit einem ISP Programmer auf den Prozessor geladen werden. <vspace>

Die Größe des Applikationsprogramms läßt sich auf zwei Arten bestimmen: <vspace>

1. man kann im Hex-File nachschauen. Da dies ein ASCII File ist, läßt es sich mit jedem Editor öffnen und anzeigen. In der vorletzten Zeile lassen sich die gewünschten Informationen finden. <vspace>

    :0A1052006C20546573740A0D000051
     :00000001FF
    <vspace>

Nach der Anzahl der Datenbytes (0Ah, 10d) folgt die Adresse (1052Ch, 4178d). Das bedeutet das Programm (in diesem Beispiel der Selbsstest) belegt 4188 Bytes (4178 + 10) der maximal verfügbaren 7168 Bytes (7*1024) des Flashspeichers. <vspace>

2. Wesentlich eleganter ist es allerdings, die AVR-GCC Compiler Suite zu bemühen. Das entsprechende Tool heißt avr-size. Es läßt sich von der Kommandozeile aus starten oder in das makefile einbauen. <vspace>

So sieht z.B. die Ausgabe des belegten FLASH Speichers (Program) und des RAM Speichers (Data) anzeigen. Der EEPROM wird beim Asuro bisher nicht verwendet. Bei der Prozentangabe muß man allerdings berücksichtigen, das hier der komplette Speicher (8kByte) des ATmega8 als Maximalwert verwendet wird, ohne Berücksichtigung des Bootloaders. Beim RAM werden nur globale Daten berücksichtigt. Es fehlt dagegen der dynamische Speicher dessen Belegung durch den Heap und den Stack nur zur Laufzeit bekannt ist. <vspace>

    >avr-size --mcu=atmega8 -C main.elf
     AVR Memory Usage
     ----------------
     Device: atmega8
    
     Program:    4188 bytes (51.1% Full)
     (.text + .data + .bootloader)
    
     Data:        136 bytes (13.3% Full)
     (.data + .bss + .noinit)
    <vspace>

## Programmierung über Bootloader<vspace>

Zum Programmieren des Asuro mit Original Prozessor wird das Asuro FlashTool (Flash.exe unter Windows, asuroflash und asurocon unter Linux) verwendet. Es empfielt sich dabei, die aktuelle Version von der [Arexx Homepage][2] zu verwenden. <vspace>

## Alternative Bootloader<vspace>

### Arexx Bootloader Clone

Obwohl der Original Bootloader weder als Source noch in Binärform verfügbar ist, gibt es trotzdem die Möglichkeit einen anderen Prozessor ohne diesen Bootloader zu verwenden und einen alternativen Bootloader aufzuspielen. Allerdings ist diese Bootloader Version nicht kompatibel zum Asuro Flasher Tool, man benötigt dazu das OC-Console Programm. Sowohl Bootloader als auch Flashertool sind auf der Homepage von RN-User [arexx-henk][3] verfügbar. Der alternative Bootloader stammt von RN-User ronny10, das OC-Console Terminalprogramm von Uwe Altenburg. Zum einmaligen Aufspielelen des Bootloaders ist allerdings ein ISP Programmer notwendig und ein Board mit ISP Anschluß in den man den ATmega8 Prozessor zum einmaligen Programmieren stecken kann. <vspace>

### AsuroBoot

Der AsuroBoot Bootloader ist ein STK500v1 kompatibler Bootloader speziell optimiert für die Arduino IDE. Läßt sich aber ebenso über avrdude oder AVRStudio verwenden. Aufgrund der Größe (>1kB) empfielt sich der Einsatz nur bei gleichzeitiger Verwendung eines ATmega168 Controllers. Leider ist die IR Schnittstelle des ASUROs zu fehleranfällig um darüber den ASURO zu brennen. Eine [Modifikation][4] der Schnittstelle auf RS232 oder USB ist deshalb notwendig. Der AsuroBoot Bootloader ist bei [Sourceforge][5] zu bekommen. <vspace>

### Sonstige

Andere Bootloader wie der [Bootloader von Peter Fleury][6] oder der [chip45boot Bootloader][7] sollten sich problemlos für den Asuro adaptieren lassen, da diese im C-Quellcode vorliegen. Auch hier ist eine [Modifikation][4] der Schnittstelle auf RS232 oder USB ist notwendig. <vspace>

## Alternative Programmieren über ISP<vspace>

Normalerweise werden die Prozessoren der AVR Familie über einen ISP (In System Programmer) programmiert. Dazu ist eine kleine Elektronik notwendig die am Parallelport des PC angeschlossen wird und über einen ISP Steckverbinder mit dem AVR Controller verbunden wird. Am ISP Steckverbinder müssen nur einige Signale des Controllers (MISO, MOSI, SCLK und RESET) und die Stromversorgung angeschlossen werden. Mit einer geeigneten Programmier Software z.B. Ponyprog, AVRDude (in WinAVR enthalten) oder dem AVRStudio kann dann das übersetzte Hexfile in den Controler Flash geschrieben werden. <vspace>

### LPT ISP Programmer<vspace>

Die Elektronik für solch einen LPT ISP Programmer kann man sehr leicht auch selbst zusammenlöten, als Bausatz kaufen oder ein Fertiggerät beziehen. Diese Programmer werden als STK200 kompatibel bezeichnet. Der Name bezieht sich dabei auf das Atmel Evaluation Kit STK200. Bei diesem Evaluation Kit war so ein Programmer beigefügt. <vspace>

Einige STK 200 kompatible Fertiggeräte und Bauanleitungen: <vspace>

*   [www.chip45.com][8] - CrispAVR-200 
*   [www.myavr.de][9] - myMultiProg LPT 
*   [www.robotikhardware.de][10] - ISP-Programmierkabel (ISP Dongle) 
*   [www.heise.de][11] - BlueMP3 ISP Programmer aus dem BlueMP3 Projekt der Zeitschrift c't. <vspace>

### USB ISP Programmer<vspace>

Da neuere PC nicht mehr über einen Parallelport verfügen, benötigt man hier einen USB ISP Programmer. Ein solcher USB ISP Programmer ist aber wesentlich komplizierter als ein LPT ISP Programmer, weil hier neben einem USB Seriell Wandler noch ein Atmel Prozessor benötigt wird, der die Befehle über die serielle Schnittstelle in ISP Signale für den zu programmierenden Zielprozessor umsetzen muß. Die Firmware für diesen Programmer sollte zudem aktualisiert werden können, damit auch neuere Atmel Prozessoren unterstützt werden. Diese Programmer werden als STK500 oder AVR910 kompatibel bezeichnet. Der Name bezieht sich dabei auf das Atmel Evaluation Kit STK500 bzw. die Atmel Application Note AVR910. Beim STK500 Evaluation Kit ist auf dem Board ein USP ISP Programmer mit eigenem Atmel Prozessor integriert. <vspace>

Einige USB ISP Programmer: <vspace>

*   [www.atmel.com][12] - STK500 Evaluation Board zu beziehen z.B bei [www.elmicro.com][13] oder 
*   [www.chip45.com][14] - CrispAVR-USB Programmer. STK500 kompatibel 
*   [www.myavr.de][15] - mySmartUSB Programmer. STK500 kompatibel 
*   [www.robotikhardware.de][16] - Bascom USB-ISP-Programmer (Programmierkabel) [usb_isp]. Achtung nicht STK500 kompatibel <vspace>

### Asuro über ISP programmieren<vspace>

Beim Asuro ist die Programmierung über ISP nicht vorgesehen. Die ISP Schnittstelle ist sogar deaktiviert (über die sogenannten Fuses) und die notwendigen ISP Signale sind auch nicht auf einen ISP Steckverbinder herasugeführt. Trotzdem kann der Asuro natürlich auf ISP Programmierung umgestellt werden, wenn man nicht den Original ASURO Controller verwendet, sondern einen neuen ATmega8 kauft und einen kleinen Umbau am Asuro vornimmt. Beim [Asuro Eval Board][17] ist dieser Umbau z.B. vorgenommen worden. Es ist deshalb sicher einfacher den Prozessor zum einamligen Programmieren des Bootloaders in ein anderes Board mit ISP Anschluß zu stecken. Wichtig ist dabei auch die Fusebits des neuen Prozessors richtig zu setzen. Zum einen muß der Quarz auf extern gestellt werden (sonst läuft der Asuro nur mit 1MHz internem Takt und die Baudrate der UART stimmt dann nicht). Nach Aufspielen des Bootloaders muß man zudem die Fusebits für die Verwendung des Bootloaders richtig setzen (BOOTSIZ0 und BOOTSIZ1 für die Größe des Bootloaders und BOOTRST zum starten des Bootloaders nach einem Reset. <vspace>

Das Tool zum Finden der richtigen Fusebits Einstellungen ist der [AVR Fuse Calculator][18] <vspace>

Für die Verwendung eines externe Quarzes und eines Bootloaders mit 512Worten und Bootloader Enabled sind die Fusebit Einstellungen: [AVR Fuses: Mega8 Low=0xbf, High=0xda][19] <vspace>

Die Befehlszeile für Avrdude zum Setzen dieser Fusebits lautet (bei Verwendung eines LPT ISP Programmers): 

    avrdude -p atmega8 -P lpt1 -c stk200-u -U lfuse:w:0xbf:m -U hfuse:w:0xda:m
    <vspace>

## Weblinks<vspace>

### Bootloader<vspace>

*   [www.mikrocontroller.net][20] - Bootloader 
*   [Elektronik Projekte][21] - AVR Bootloader Artikel 
*   [AsuroBoot][5] - Bootloader bei Sourceforge 
*   <http://jump.to/fleury> - STK500v2 kompatibler Bootloader 
*   [www.chip45.com][7] - chip45boot, ebenfalls ein STK500 kompatibler Bootloader 
*   <http://www.microsyl.com/> - MegaLoad Bootloader und Programmer Software

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroHexfiles
 [2]: http://www.arexx.com
 [3]: http://home.kpn.nl/h.van.winkoop/
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroErweiterung
 [5]: http://downloads.sourceforge.net/asuro/AsuroBoot-v001.zip?modtime=1200183966&big_mirror=0
 [6]: http://jump.to/fleury
 [7]: http://www.chip45.com/index.pl?page=chip45boot&lang=de
 [8]: http://www.chip45.com/index.pl?page=CrispAVR-200&lang=de
 [9]: http://www.myavr.de/shop/artikel.php?artID=64
 [10]: http://www.shop.robotikhardware.de/shop/catalog/product_info.php?cPath=73&products_id=41
 [11]: http://www.heise.de/ct/Redaktion/cm/klangcomputer/index1.htm
 [12]: http://www.atmel.com/dyn/products/tools_card.asp?tool_id=2735
 [13]: http://elmicro.com/de/stk500.html
 [14]: http://www.chip45.com/index.pl?page=CrispAVR-USB&lang=de
 [15]: http://www.myavr.de/shop/artikel.php?artID=42
 [16]: http://www.shop.robotikhardware.de/shop/catalog/product_info.php?cPath=73&products_id=161
 [17]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroEvalBoard
 [18]: http://palmavr.sourceforge.net/cgi-bin/fc.cgi?P_PREV=ATmega8&P=ATmega8
 [19]: http://palmavr.sourceforge.net/cgi-bin/fc.cgi?P_PREV=ATmega8&P=ATmega8&V_LOW=BF&V_HIGH=DA&O_HEX=Apply+user+values&M_LOW_0x3F=0x01&M_LOW_0x40=&M_LOW_0x80=0x80&M_HIGH_0x01=&M_HIGH_0x06=0x00&M_HIGH_0x08=&M_HIGH_0x10=&M_HIGH_0x20=0x00&M_HIGH_0x40=0x00&M_HIGH_0x80=&B_WTDON=P&B_SUT1=P&B_SPIEN=P&B_SUT0=P&B_CKSEL3=P&B_CKSEL2=P&B_BOOTSZ1=P&B_CKSEL1=P&B_BOOTSZ0=P
 [20]: http://www.mikrocontroller.net/articles/Bootloader
 [21]: http://s-huehn.de/elektronik/bootloader/bootloader.htm

