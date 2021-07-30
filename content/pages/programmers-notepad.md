# ProgrammersNotepad

## Einleitung

Programmers Notepad ist die Standard Entwicklungsumgebung, die bei [WinAVR][1] mitgeliefert wird. 



## Installation

Der Programmers Notepad wird optional zusammen mit [WinAVR][1] installiert 



## Features

*   Quelltext Editor mit Syntax Highlighting, 
*   Projektverwaltung für Einzelprojekte und Projektgruppen, allerdings ohne Makefile Erzeugung. Makefiles müssen von Hand angepaßt werden. 
*   Aufruf externer Tools, wie z.B. Make 
*   Folding (Zusammen-/ auseinanderfalten von Funktionen) 



## Projekt erstellen

Ein neues Projekt ist schnell erstellt. 

1. Man klickt auf den Menüpunkt **'File' | 'New' | 'Project**'. 



![][2] 

2. In dem sich öffnenden Dialog gibt man den Namen und das Verzeichnis für das Projekt an. 



![][3]

3. Im **'Projects**' Fenster kann man bestehende Quellcode Dateien mit einem Rechtsklick auf den Projektnamen und Auswahl von **'Add Files**' zu dem Projekt hinzufügen. Die ausgewählten Dateien werden mit Doppelklick auf den Namen zum Editieren öffnen. Die ausgewählten Dateien werden aber **nicht** automatisch zum Projekt dazugelinkt. Das wird ganz alleine durch das Makefile bestimmt. 



![][4]

4. Zum Übersetzen des Projektes und Erstellen des Hex-Files startet man den Make Prozess mit klick auf den Menüpunkt **'Tools' | '[WinAVR] Make all**'. 



![][5] 

5. Falls keine Syntax Fehler im Programmcode sind, sieht die Ausgabe etwa so aus. 



![][6]

6. Bei einem Syntax Fehler sieht man im Ausgabe Fenster die Fehlermeldung. Mit einem Klick auf die Fehlermeldung wird der Cursor auf die entsprechende Zeile im Quelltext positioniert. 



![][7]

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/WinAVR
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/pn1.jpg
 [3]: http://www.asurowiki.de/pmwiki/uploads/Main/pn2.jpg
 [4]: http://www.asurowiki.de/pmwiki/uploads/Main/pn3.jpg
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/pn4.jpg
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/pn5.jpg
 [7]: http://www.asurowiki.de/pmwiki/uploads/Main/pn6.jpg