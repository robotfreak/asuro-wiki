# Odometrie

![](%assets_url%/irleds.jpg) ![](%assets_url%/odometrie.jpg)

*Odometrie* 

## Funktionsweise

Mit dem Asuro Bausatz werden auch je 2 Encoder Scheiben mit 8 bzw. 12 Sektoren zum Aufkleben mitgeliefert. Damit erhält man 40 bzw. 60 Impulse pro Reifenumdrehung. 

Die Encoder Scheiben werden von IR_Leds (D13, D14) angestrahlt. Die Foto-Transistoren (T11, T12) messen das reflektierte Licht. Der Prozessor mißt über die Analog/Digital Wandler Ports die Spannung an den Foto- Transistoren und vergleicht diese mit vorgegeben Referenzwerten für Hell/Dunkel. Die Wechsel zwischen Hell/Dunkel werden gezählt und können vom Benutzer Programm ausgewertet werden. Die Odometrie Messung kann vom Benutzer Programm manuell abgefragt werden, über die Funktion OdometrieData(unsigned int *data) oder automatisch im Hintergrund (Interruptgesteuert) durch die Funktion EncoderInit(void). Diese Funktion ist nur in der [erweiterten Asuro Bibliothek](bibliothek) vorhanden. 

Während der Odometrie Messung sind die Prozessor Ports PC0, PC1 als Eingang und PD7 als Ausgang geschaltet. Deshalb können die beiden Back-LEDs nicht benutzt werden. Umgekehrt gilt: Schaltet man die Back LEDs an, werden die Ports PC0 und PC1 als Ausgang und PD7 als Eingang geschaltet und die Odometrie Messung ist nicht mehr möglich. 

## Probleme mit der Odometrie

Die Odometrie Daten des Asuro sind leider nicht sehr brauchbar. Sie sind zum einen vom Umgebungslicht abhängig, zudem hat das Zahnrad zu viel Spiel auf der Achse, womit sich der Abstand zu den Sensoren ändert. 

Abhilfe gegen Umgebungslicht schafft das Anbringen einer Abdeckung aus Papier über IR-Led und Fototransistor. Die Zahnräder kann man mit einer aufgeklebten Unterlegscheibe etwas stabilisieren. 

Eventuell müssen die Grenzwerte für Hell/Dunkel in der [Asuro Bibliothek](bibliothek) angepaßt werden. 

Um den Asuro zum Geradeausfahren zu bewegen, ist es auch möglich den Unterschied zwischen den beiden Antrieben empirisch zu ermitteln und als feste Größe in seine Programme einzubauen. 

## Weiterführende Links:

*   [Wikipedia](http://de.wikipedia.org/wiki/Odometrie) 
*   [Roboternetz Thread](http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=12194) - Odometrie von Asuro 

