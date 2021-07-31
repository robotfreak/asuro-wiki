# Asurino

## Einleitung

[Arduino](http://www.arduino.cc/) ist eine Open-Source- Plattform, basierend auf einem Microcontroller-Board und einer Entwicklungsumgebung mit einer API für den Microcontroller. Als Microcontroller wird neben dem ATmega8 in neueren Boards der ATmega168 verwendet. Die Arduino Entwicklungumgebung ist in Java programmiert und läuft auf den gängigen PC Plattformen Windows/Linux/Mac. 

Der Microcontroller auf dem Board wird mit Hilfe der Arduino Programmiersprache programmiert. Diese basiert auf [Wiring](http://wiring.org.co/) mit der Syntax von C, bzw. C++. Die Entwicklungsumgebung baut auf [Processing]((http://www.processing.org/)) auf. 

Asurino ist eine Arduino Bibliothek für den Asuro. Die Idee dazu stammt aus dem [Arduino Playground](http://www.arduino.cc/playground), in dem Arduino Nutzer ihre Projekte vorstellen. Unter [Arduino and the Asuro Robot](http://www.arduino.cc/playground/Learning/Asuro) von Jakob Remin findet man neben einer Quick&Dirty Methode zur Modifikation des Asuros auch ein Arduino Sketch zur Ansteuerung dses Asuros. Einige Funktionen wurden auch aus der [Asuro Bibliothek](bibliothek) übernommen. 

Derzeit läuft das ganze mit Einschränkungen auf jedem Asuro. Die volle Funktionalität der Arduino IDE geht derzeit aber nur mit einem modifizierten Asuro, bei dem die UART Schnittstelle herausgeführt ist. Entweder über ein [RS232 Modul](rs232-wandler), oder einem USB Seriell Wandler Modul. Mit Einschränkungen auch mit dem [Bluetooth Modul](bluetooth-modem). 

## Was man benötigt

*   natürlich einen Asuro 
*   die [Arduino Umgebung](http://www.arduino.cc/en/Main/Software) (inklusive AVR Compiler) 
*   Die [Asurino Bibliothek](http://sourceforge.net/project/showfiles.php?group_id=155217), die Arduino Bibliothek für den Asuro auf Sourceforge 

Optional sind: 

*   einen neuen ATmega168 oder ATmega328 
*   ein ISP Programmer. Zum Programmieren oder zum einmaligen Programmieren des [AsuroBoot Bootloader](http://sourceforge.net/project/showfiles.php?group_id=155217) 
*   derzeit noch ein [RS232 Modul](rs232-wandler), USB/seriell Wandler Modul oder ein Arduino Board. Es funktioniert nicht über die Infrarotschnittstelle. Man kann allerdings die erzeugten Hex-Files wie bisher über das Asuro Flasher Tool 
*   einen modifizierte Asuro, wie z.B. in der [Asuro Erweiterung](asuro-erweiterung) oder wie bei [Arduino and the Asuro Robot](http://www.arduino.cc/playground/Learning/Asuro) beschrieben. 
*   Den [AsuroBoot Bootloader](http://sourceforge.net/project/showfiles.php?group_id=155217), angepaßt für den Asuro 

## Arduino IDE anpassen

### Original Asuro

Mit einem Original Asuro kann man immerhin die Skripte in der Arduino IDE schreiben und übersetzen lassen. Zum Flashen muß man dann aber wieder auf das normale Asuro Flasher Tool zurückgreifen. Den Terminalmode der Arduino IDE kann man ebenso nicht benutzen, da die Steuerleitungen der Schnittstelle falsch geschaltet werden. Damit fehlt dem Standard RS232/IR Transceiver die Stromversorgung (ein Umbau mit externer Stromversorgung könnte funktionieren). Derzeit muß man sich auch hier mit seinem gewohnten Terminalprogramm begnügen. 

Mit ein paar Änderungen in der Board Beschreibungsdatei hat man ein neues Board dazugefügt und dieses taucht nach dem Start der Arduino Oberfläche unter Tools | Boards aus. Die Board Beschreibungsdatei befindet sich im Arduino Ordner *Arduino-0010/hardware/boards.txt*. 

    ##############################################################
     asuro8.name=Asuro w/ ATmega8
     asuro8.upload.protocol=stk500
     asuro8.upload.maximum_size=7168
     asuro8.upload.speed=2400
     asuro8.bootloader.low_fuses=0xdf
     asuro8.bootloader.high_fuses=0xca
     asuro8.bootloader.path=atmega8asuro
     asuro8.bootloader.file=ATmegaBOOT_8_asuro.hex
     asuro8.bootloader.unlock_bits=0x3F
     asuro8.bootloader.lock_bits=0x0F
     asuro8.build.mcu=atmega8
     asuro8.build.f_cpu=8000000L
     asuro8.build.core=arduino
     asuro8.build.variant=standard
    

### Asuro mit ATmega168/ATmega328

Mit der [Asuro Erweiterung](asuro-erweiterung) und der damit vorhandenen RS232 Schnittstelle lassen sich auch sehr leicht Arduino Skripte laden und ausführen. Allerdings wird dazu auch ein neuer Prozessor mit einem Arduino kompatiblen Bootloader vorausgesetzt. Warum nicht gleich auf den ATmega168 umsteigen. Der bietet neben dem doppelten Speicher für Flash, EEPROM und RAM auch eine Debug Möglichkeit über DebugWire. 

So sehen die Änderungen in der Board Beschreibungsdatei für den Asuro mit ATmega168 aus. 

    ##############################################################
     asuro168.name=Asuro w/ ATmega168
     asuro168.upload.protocol=stk500
     asuro168.upload.maximum_size=14336
     asuro168.upload.speed=9600
     asuro168.bootloader.low_fuses=0xff
     asuro168.bootloader.high_fuses=0xdd
     asuro168.bootloader.extended_fuses=0x00
     asuro168.bootloader.path=atmega168asuro
     asuro168.bootloader.file=ATmegaBOOT_168_asuro.hex
     asuro168.bootloader.unlock_bits=0x3F
     asuro168.bootloader.lock_bits=0x0F
     asuro168.build.mcu=atmega168
     asuro168.build.f_cpu=8000000L
     asuro168.build.core=arduino
     asuro168.build.variant=standard
    

So sehen die Änderungen in der Board Beschreibungsdatei für den Asuro mit ATmega328 aus. 

    ##############################################################
     asuro328.name=Asuro w/ ATmega328
     asuro328.upload.protocol=stk500
     asuro328.upload.maximum_size=30720
     asuro328.upload.speed=9600
     asuro328.bootloader.low_fuses=0xff
     asuro328.bootloader.high_fuses=0xdd
     asuro328.bootloader.extended_fuses=0x00
     asuro328.bootloader.path=atmega328asuro
     asuro328.bootloader.file=ATmegaBOOT_328_asuro.hex
     asuro328.bootloader.unlock_bits=0x3F
     asuro328.bootloader.lock_bits=0x0F
     asuro328.build.mcu=atmega328
     asuro328.build.f_cpu=8000000L
     asuro328.build.core=arduino
     asuro328.build.variant=standard
    

Nach einstellen der Schnittstelle wird der Asuro auch gleich erkannt und das Beispiel Sketch kann übersetzt und geladen werden. Allerdings zeigte sich dabei der Effekt das beim Flashen bzw. beim Einschalten oder Reset des Asuros der rechte Motor für ca. 10sek losläuft. Das ist natürlcih unschön und liegt am Original Arduino Bootloader. Dort wird PB5 als Port für die Status LED verwendet. Beim Asuro ist dieser Port mit dem rechten Motor verbunden. 

## Bootloader anpassen

Der Original Asuro verfügt bereits über ienen Bootloader, derzum Flashen mit dem Asuro Flasher Tool verwendet werden kann. Für den ATmega168 benötigt man allerdings einen Bootloader. Damit lassen sich Programme direkt von der Arduino IDE in den Asuro laden. Da der Quellcode für den Bootloader als Open Source zur Verfügung steht, ist das Ändern der Status LED kein Problem. Allerdings blieb auch nach Änderung die recht lange Wartezeit von 10sek bis das Anwenderprogramm gestartet wird. Nach ein paar Internet Recherechen war auch für dieses Problem eine Lösung in Form des ADABOOT Bootloader gefunden. Dieser Bootloader bietet einige Vorteile gegenüber dem Original Arduino Bootloader. 

Allerdings klappt die Übertragung bisher nur über RS232. Bei [Bluetooth](bluetooth-modem) Anbindung gibt es keine Verbindung zwischen der Arduino IDE und dem Asuro. Man kan zwar in derBluetooth Umgebung die Verbindung manuell herstellen, dann klappt immerhin die Verbindung im Terminalmode. Versucht man aber ein Sketch zu laden, bricht die Verbindung wieder ab. Mit Hyper Teminal gibt es keine Probleme unter Bluetooth. Schade, aber man kann wohl nicht alles haben. Allerdings besteht noch Hoffnung. Auf der Chip45 Homepage, gibt es den Ur-Bootloader für die Arduino Boards. Dort gibt es auch ein kleines Tool zum Flashen von Programmen über den Bootloader. Dies ließe sich vielleicht anpassen, damit das Flashen auch unter Bluetooth funktioniert. Ein nettes Feature der Arduino Bootloader ist der automatische Reset des Boards, wenn ein neues Programm geflasht werden soll. Dazu muß lediglich ein 100nF Kondensator zwischen Reset Leitung und DTR Steuerleitung gelötet werden. Allerdings führt das auch dazu, dass der Asuro einen Reset ausführt, wenn man die Arduino IDE, bzw. das Terminalprogramm startet. 

Der Bootloader ließe sich eventuell so anpassen, das er auch über die Standard Infrarot Schnittstelle des ASUROs funktioniert. Leider sind alle Versuche bis dahin gescheitert. 

## Asurino - die Arduino Bibliothek für den Asuro

Aus dem bestehenden Sketch von Jakob Remin habe ich angefangen eine Arduino Bibliothek zu schreiben. Der Name Asurino ist ein Kunstwort zusammengefügt aus den beiden Worten **Asur**o und Ardu**ino**. Bibliotheken für Arduino werden in C++ geschrieben. Das hört sich erst mal nach viel Arbeit an, ist aber nicht sonderlich schwer. Es gibt eine sehr gute Anleitung zum Schreiben von Bibliotheken. Man braucht auch nicht bei Null anfangen, da man natürlich die vorhandenen Arduino Funktionen alle verwenden kann. Außerdem kann man sich an bereits existierenden Bibliotheken orientieren. 

### Referenz

Neben den [Standard Funktionen](http://www.arduino.cc/en/Reference/HomePage) von Arduino sind folgenden Funktionen in der Asurino Lib enthalten: 

void Init(void);  
void setTimer2(void);  
void setBackLED(unsigned char left, unsigned char right);  
void setStatusLED(unsigned char color);  
int readSwitches(void);  
int readBattery(void);  
void readOdometry(int *data);  
void readLinesensor(int *data);  
void setMotorDirection (int left, int right);  
void setMotorSpeed (int left, int right);  
void driveSquare(int size, int speed);  
void driveCircular(int length);

Normaler AVR C/C++ Code kann natürlich auch verwendet werden. 

### Asuro Beispiel Sketch

Ein Beispiel Sketch für den Asuro sieht z.B. so aus. Durch das 

    #include "Asuro.h"
    

wird die Bibliothek eingebunden. Makefiles müssen keine angepaßt werden, die werden von der Arduino IDE automatisch erzeugt. Auch die Bibliotheken werden automatisch übersetzt. 

Die Zeile 

    Asuro asuro = Asuro();
    

ist der Aufruf für den Konstruktor der Asuro Klasse. Die Setup Routine wird einmalig beim Start des Sketches ausgeführt und initialisiert lediglich die serielle Schnittstelle. Die Asuro spezifische Initialisierung passiert bereits im Konstruktor. Die loop Funktion wird dann zyklisch vom Hauptprogramm aufgerufen und durchlaufen. Das eigentliche Programm fragt die Tastsensoren ab. Falls eine Taste gedrückt wurde, wird der Tastenwert binär zum Terminalprogramm gesendet und die Status LED für eine Sekunde auf Rot gesetzt, dann wieder zurück auf Grün. 

### Beispiel für den Original Asuro 
```c
#include <Asuro.h>  
Asuro asuro = Asuro();  
  
  
void setup()  
{  
  Serial.begin(2400);  
  asuro.setTimer2(); /* 36kHz for IR communication */  
}  
  
  
void loop()  
{  
  int Switches;  
  /* front switch check */  
  Switches = asuro.readSwitches();  
  if (Switches) /* Key pressed? */  
  {  
    Serial.println("switches pressed");  
    Serial.println(Switches, BIN);  /* send key value in binary */  
    asuro.setStatusLED(RED);  /* status led red */  
    delay(1000);              /* wait 1sec */  
  }  
  asuro.setStatusLED(GREEN); /* status led green */  
}
```

## Weblinks

*   [www.arduino.cc](http://www.arduino.cc/) 
*   [www.wiring.org][2] 
*   [www.processing.org](http://www.processing.org/)
*   [Wikipedia][13] - Processing 
*   [Arduino Playground][4] 
*   [Arduino and the Asuro Robot][5] 
*   [Asurino - an Arduino library for the Asuro Robot][14] 
*   [Sourceforge][10] - Asurino Bibliothek und Asuro Bootloader

 [1]: http://www.arduino.cc/
 [2]: http://wiring.org.co/
 [3]: http://www.processing.org/
 [4]: http://www.arduino.cc/playground
 [5]: http://www.arduino.cc/playground/Learning/Asuro
 [6]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [7]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RS232Wandler
 [8]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/BluetoothModem
 [9]: http://www.arduino.cc/en/Main/Software
 [10]: http://sourceforge.net/project/showfiles.php?group_id=155217
 [11]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroErweiterung
 [12]: http://www.arduino.cc/en/Reference/HomePage
 [13]: http://de.wikipedia.org/wiki/Processing
 [14]: http://www.arduino.cc/playground/Learning/Asurino

