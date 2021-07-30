# AVRStudio

AVR Studio ist die Entwicklungsumgebung vom AVR Hersteller [Atmel][1] für Windows, die man sich leider nur nach einer kostenlosen Registrierung von der [Atmel][2] Seite herunter laden kann. Wer die Registrierung umgehen möchte, kann die Datei auch direkt herunterladen, wenn man den Link kennt ;) siehe [hier][3]. Die Projektverwaltung ist ähnlich wie beim Programmers Notepad. Hinzu kommt noch ein Simulator, bzw. die Unterstützung verschiedener Emulatoren und Programmer. Mit dem Paket wird nur der Atmel AVR Assembler installiert. Über ein Plugin wird aber auch der AVR-GCC C/C++Compiler unterstützt. Deshalb sollte man vor der Installation von AVR-Studio zuerst WinAVR installieren. 



## Features

*   Quelltext Editor mit Syntax Highlighting 
*   Projektverwaltung für Einzelprojekte 
*   Integrierte Projektverwaltung (automatische Makefiles Generierung oder Verwendung externer Makefiles) 
*   AVR-GCC (WinAVR) und AVR Assembler Unterstützung 
*   Debugger Unterstützung für AVR Simulator und Emulator 
*   AVR Programmer (Flasher) Unterstützung für STK200, STK500 kompatible u.a. 



## Installation

Die Installation funktioniert problemlos. Einfach die herunter geladene Datei aStudio4bxxx.exe ausführen. 



## Projekt erstellen

Ein Projekt unter AVR Studio ist mit wenigen Schritten erstellt: 

1. Man startet den Project Wizard in dem man unter dem Menüpunkt **'Project**' den Menü Unterpunkt **'Project Wizard**' selektiert. 



![][4]

2. In dem Project Wizard Dialog wählt man **'New project**' aus und klickt auf den Schalter **'Next**'. 



![][5]

3. Dann wählt man als **'Project Type:**' 'ACR-GCC' aus und gibt als Projektnamen **'test**' an. Diesem Namen sollte man wählen, wenn man ein vorhandenes Makefile aus dem Asuro Examples Ordner verwenden will. Wenn man ein komplett neues Projekt erstellen will setzt man die Haken bei **'Create initial file**' und **'Create Folder**' und wählt unter 'Location:' den entprechenden Zielordner aus. Ebenso kann man aber auch ein neues Projekt anzulegen, indem man die Dateien 'test.c' und 'Makefile' aus dem 'FirstTry' Ordner einfach in einen neuen Ordner kopiert und dann fortfährt wie bei einem bestehendem Projekt. Will man ein bestehendes Projekt im AVR Studio bearbeiten, läßt man einfach die Haken bei **'Create initial file**' und **'Create Folder**' weg und wählt nur den entsprechenden Projektordner aus. Mit einem Klick auf **'Next**' schließt man den Project Wizard und das neue Projekt wird angelegt. 



![][6]

4. Im Fenster **'AVR-GCC**' kann man mit einem Rechtsklick bestehende Dateien zum Projekt hinzufügen. Dazu wählt man den Punkt **'Add existing Source File(s)...**' mit einem Rechtsklick auf den Projektnamen aus. Dadurch werden diese Dateien allerdings nur zum Editieren zu dem bestehenden Projekt hinzugefügt. Sie werden **nicht** mit dem bestehenden Projekt compiliert oder gelinkt. Um weitere C-Dateien zu einem Projekt hinzuzufügen, nmuß das Makefile geändert werden. 



![][7]

5. Die Projekt Eigenschaften kann man ebenfalls im **'AVR-GCC**' Fenster mit einem Rechtsklick auf den Punkt **'Edit Configuration Options...**' ändern. Dieses öffnet den **'Project Options**' Dialog. 



![][8]

6. Im **'Project Options**' Dialog muß man lediglich unter **'General**' den Haken vor **'Use external Makefile**' setzen und das vorhandene Makefile auswählen (Button '...' drücken und Makefile auswählen). Weitere Einstellungen sind nicht notwendig. . 



![][9]

7. Ein Klick auf den Menüpunkt **'Build**' und Untermenüpunkt **'Build**' bzw. die Funktionstaste **F7** startet den Build Prozess und erzeugt dann entweder das Hexfile, oder gibt Fehlermeldungen aus, falls etwas nicht in Ordnung ist 



## Weblinks

*   [www.atmel.com][2] - AVR Studio 
*   [mikrocontroller.net][3] - AVR-Studio Artikel

 [1]: http://www.atmel.com
 [2]: http://www.atmel.com/dyn/products/tools_card.asp?tool_id=2725
 [3]: http://www.mikrocontroller.net/articles/AVR-Studio
 [4]: http://www.asurowiki.de/pmwiki/uploads/Main/avrstudio.jpg
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/avrstudio1.jpg
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/avrstudio2.jpg
 [7]: http://www.asurowiki.de/pmwiki/uploads/Main/avrstudio3.jpg
 [8]: http://www.asurowiki.de/pmwiki/uploads/Main/avrstudio4.jpg
 [9]: http://www.asurowiki.de/pmwiki/uploads/Main/avrstudio5.jpg