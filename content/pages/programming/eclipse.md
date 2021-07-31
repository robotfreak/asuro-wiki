# Eclipse

## Einleitung 

Eclipse ist eigentlich eine Entwicklungsumgebung für Java. Durch das Plugin 'CDT' lassen sich aber auch C/C++ Projekte verwalten inkl. Syntax Highlighting. Durch das 'AVR Plugin for Eclipse' kann man letztendlich auch AVR Projekte mit dem integrierten managed Make von Eclipse erstellen und verwalten. 



## Features

Die großen Vorteile von Eclipse sind: 



*   Eclipse ist plattformunabhängig. Da Eclipse selbst in Java programmiert wurde, läuft es auf allen gängigen Plattformen wie Linux, Windows und sogar dem Mac. 
*   jede Menge Plugins zur Erweiterung und Einbindung von externen Tools 
*   Quelltext Editor mit Syntax Highlighting 
*   Projektverwaltung für Einzelprojekte und Projektgruppen. Auch Abhängigkeiten unter Projekten werden unterstützt 
*   Integrierte Projektverwaltung mit Managed Make. Man muß sich nicht groß um die Makefile Erstellung kümmern 
*   CVS und SVN Plugins. Zum direkten Abgleich mit CVS/SVN Repositorys 
*   Debugger Unterstützung für Gnu Debugger 
*   AVR Programmer (Flasher) Unterstützung über avrdude Einbindung 



## Einrichtung und Installation

Zur Installation werden folgende Pakete benötigt (bzw. wenn man bereits Eclipse verwendet, benötigt man nur das entsprechende CDT Plugin): 



*   [Java Runtime Environment][1] 
*   [Eclipse-IDE Classic][2] Version 3.1 - 3.3 
*   [Eclipse-CDT-Plugin][3]. **Achtung**! genau die Version überprüfen. Es funktioniert nur: 
    *   Version 3.0.0 für Eclipse 3.1, 
    *   Version 3.1.2 für Eclipse 3.2, 
    *   Version 4.0 für Eclipse 3.3 

Oder man benutzt gleich die folgende Version: 



*   [Eclipse IDE for C/C++ Developers][4]. Diese enthält Eclipse 3.3 und CDT 4.0 

Für die AVR Entwicklung selbst werden benötigt: 



*   [Eclipse-CDT-Addon for AVR][5] Version 20070623 oder neuer 
*   [WinAVR][6] Version 20070525 oder neuer wird natürlich auch benötigt 



### Installation

Eclipse selbst benötigt keine Installation. Einfach das Zip-Archiv in ein Verzeichnis mit allen Unterverzeichnissen auspacken, das wars. Die Plugins kann man zum einen über den Eclipse Plugin Manager installieren lassen, oder selbst die Plugins herunterladen und in das plugins Verzeichnis von Eclipse kopieren. 



## Projekterstellung mit Eclipse

### Asuro Library

1. Die Asuro Library läßt sich auch unter Eclipse übersetzen. Da Eclipse Abhängigkeiten zwischen mehreren Projekten berücksichtigen kann (Projekt muß neu übersetzt werden, weil ein anderes Projekt geändert wurde) ist es von Vorteil auch die Ausro Lib unter Eclipse zu verwalten. Nach dem Start von eclipse erscheint zunächst ein Dialog zur Eingabe des Workspace Verzeichnisses. Eclipse kann mehrere Workspaces verwalten. Zu einem Workspace können mehrere Projekte gehören. Bestehende Projekte lassen sich dann recht einfach in einen bestehenden Workspace importieren. Wenn man auf diese Abfrage beim Programmstart verzichten will, setzt man einfach das Häkchen vor 'Use this as the default and do not ask me again' 



![][7]

2. Ein neues Projekt erstellt man im Menü **'File**' **'New**' **'C-Project**'. Bei älteren Eclipse Versionen (<3.3) benutzt man dazu den Menüpunkt **'Managed C-Project**'. Ab Version 3.3 sind alle Projekte Managed C-Projekte. Die Einträge C oder C++ Projekte tauchen nur auf,wenn das [Eclipse-CDT-Plugin][3] installiert ist. 



![][8]

3. In dem sich öffnenden Dialog gibt man den Projektnamen ein und gibt als Projekt Typ **'AVR Cross-Target Project**' an. Dieser Eintrag taucht nur auf, wenn das [Eclipse-CDT-Addon for AVR][5] installiert ist. Ein Klick auf 'Next' führt zum nächsten Schritt. 



![][9]

4. Als Konfiguration gibt es nur Standard. Andere Konfigurationen (bestimmter AVR Typ, Library oder Hex-File...) kann man sich später erzeugen und dann als eigene Konfiguration speichern. Leider funktioniert der **'Next**' Schalter unter Eclipse 3.3 nicht, hier muß man die weiteren Schritte manuell machen, indem man die Projekterstellung mit **'Finish**' abschließt. Unter Eclipse <3.3 erscheint hier noch ein weiterer Dialogschritt zur Eingabe von AVR Prozessor Typ (ATmega8) und der Prozessor Frequenz (8MHz). 



![][10]

5. Anschließend werden die C-Quellen der Asuro Lib importiert. Dies geschieht durch einen Rechtsklick im Project Explorer Fenster auf den Projektnamen. Dann wählt man in dem Popup Menü den Punkt 'Import' aus. Im Import Dialog wählt man unter General Filesystem aus und klickt auf 'Next'. 



![][11]

6. Im nächsten Schritt klickt man auf Browse und wählt den Ordner mit den Asuro Lib Quellen aus (defaultmäßig C:\ASURO_SCR\AsuroLib\lib) aus. Dann selektiert man alle C-Dateien und alle H-Dateien aus dem inc Unterordner. Mit 'Finish' schließt man den Vorgang ab, und alle angewählten Dateien werden in den Projektordner des Eclipse Workspace kopiert. Die Verzeichnisstruktur wird dabei beibehalten. 



![][12]

7. Im Projekt Explorer Fenster erscheinen nun alle Dateien, die zur Asuro Lib gehören. Mit Doppelklick auf den Dateinamen kann man diese öffnen und bearbeiten. 



![][13]

8. Als nächstes müssen die Projekt Eigenschaften eingestellt werden. Dazu klickt man im Menü 'Project' auf 'Properties' und wählt im Properties Dialog den Eintrag 'C/C++ Build' 'Settings' aus. 



![][14]



![][15]



![][16]



![][17]



![][18]



![][19]



![][20]



![][21]



![][22]



![][23]



### Asuro Examples



## Weblinks

*   <http://www.eclipse.org> 
*   [Eclipse-CDT-Plugin][3] 
*   [Eclipse-CDT-Addon for AVR][5] 
*   [www.mikrocontroller.net][24] - AVR Eclipse

 [1]: http://www.eclipse.org/downloads/moreinfo/jre.php
 [2]: http://www.eclipse.org/downloads/index.php
 [3]: http://www.eclipse.org/cdt/
 [4]: http://www.eclipse.org/downloads/moreinfo/c.php
 [5]: http://sf.net/projects/avr-eclipse
 [6]: http://winavr.sourceforge.net/
 [7]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse.jpg
 [8]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse1.jpg
 [9]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse2.jpg
 [10]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse3.jpg
 [11]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse4.jpg
 [12]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse7.jpg
 [13]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse8.jpg
 [14]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse9.jpg
 [15]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse10.jpg
 [16]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse11.jpg
 [17]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse12.jpg
 [18]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse13.jpg
 [19]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse14.jpg
 [20]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse15.jpg
 [21]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse16.jpg
 [22]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse17.jpg
 [23]: http://www.asurowiki.de/pmwiki/uploads/Main/eclipse18.jpg
 [24]: http://www.mikrocontroller.net/articles/AVR_Eclipse