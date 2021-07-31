# Spannungsueberwachung

| ![][1]                 |
||
| *Spannungsüberwachung* |



## Funktionsweise:

Die Spannungsüberwachung besteht aus einem einfachen Spannungsteiler. Über den Prozessor Pin PC6, der als A/D Wandler Port konfiguriert ist, wird die Spannung gemessen. Im Bootloader wird die Battereispannung überprüft. Liegt sie zu tief fängt die Status LED an, gelb zu blinken, und über den seriellen Port wird 'VL' gesendet.

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/powerwatch.jpg