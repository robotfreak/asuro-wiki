---
Title: Odometrie Modifikation
Template: section
---

# Odometrie Modifikation

### Auflösung der Odometrie erhöhen

Auf dem Mainboard des Asuro sind die Pins für die Reflexlichtschranken noch einmal neben den Motorritzeln vorhanden. 

Durch Umlöten der Bauteile (T11, T12, D13 und D14) und aufkleben der Geberscheiben direkt auf das Motorritzel, kann man die Impulse pro Radumdrehung von 40(60) auf 200(300) erhöhen. 



 ![](%assets_url%/odometrie_mod.jpg)  
*Odometrie Modifikation*



### Achsenspiel verringern

Die Odometriesensoren des ASUROs liefern ziemlich schwankende Werte für den linken und rechten Sensor. Teilweise lassen sich die Unterschiede durch Abdeckung der Sensoren beseitigen. Ein Grundübel aber bleibt. Der unterschiedliche Abstand des Getrieberades mit den Encoderscheiben zu den Fotosensoren/IR LEds. Teilsweise beträgt das Spiel auf der Welle mehrere Millimeter. Laufen die Motoren, dann rutschen die Getrieberäder auf der Achse hin und her. 

Um diesen Fehler auszugleichen, lötet man die kurzen Achsen nicht vollständig in die Kerbe auf der Platine ein, sondern 2-3mm weiter nach außen. Dadurch ist es möglich einen Spannring oder eine Unterlegscheibe auf der Achse zu befestigen, um damit dass Spiel der Getriebescheibe zu reduzieren. 



![](%assets_url%/mod_odo.jpg)  
*Achse weiter außen eingelötet*



![](%assets_url%/mod_odo1.jpg)
*Montierte Getrieberäder*



### Sensoren abdecken

Die Fototransistoren sind empfindlich gegen Streulicht. Dagegen helfen Abdeckungen, die man sich aus dunklen Fotokarton zurechtschneidet und zusammenklebt. Die Abdeckungen stülpt man über Fototransistor und IR LED und klebt sie an der Platine fest. 



![](%assets_url%/mod_odo2.jpg)
*Sensorabdeckung*



## Weitere Modifikationen

*   [Roboternetz Thread][5] - Asuro Odometrie Fehler. Zahnrad Spiel verringern. 
*   [Roboternetz Thread][6] - Asuro und Odometrie. Fremdlichteinstrahlung abschirmen.

 [5]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=8153
 [6]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=12488