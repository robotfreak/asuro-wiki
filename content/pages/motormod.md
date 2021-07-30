# MotorModifikation

### Austausch der Motoren

Die Igarashi Originalmotoren des Asuros sind nicht besonders kraftvoll. Der Austausch gestaltet sich insofern etwas schwierig, geeignete Motoren zu finden, die entsprechend kleine Abmessungen haben. 

Bei obigem Beispiel kommen 2 [Faulhaber][1] DC-Motoren der Baureihe 2224 zum Einsatz. Die bringen zwar zunächst mehr Gewicht auf die Waage (96g statt 25g der Original Motoren), gleichen das aber locker durch besseres Drehmoment ud Wirkungsgrad aus. 

Da auch der Durchmesser der Motoren größer ist, muß eine geeignete Motorhalterung her. Diese werden aus einem Stück Aluwinkel (30x30x1,5mm) aus dem Baumarkt gesägt und gebohrt. Leider ist die Verbindung mit der Leiterplatte mit dem Aluwinkeln nicht ganz optimal. 



| ![][2] | ![][3] | ![][4] |
||



### Modifikation der Motoranschlüsse

Die Anschlüsse der Motoren werden nach der Original Bauanleitung direkt auf der Platine angelötet. Das ist meiner Meinung nach etwas unpraktisch. Deshalb lautet mein Vorschlag hier, die Motoren steckbar anzuschließen. 

Hierzu bieten sich PSK Steckverbinder an. Diese sind verpolungssicher kodiert und bieten zudem eine Arretierung für den Steckverbinder. PSK Steckverbinder gibt es zum einen einzeln (Stecker, Crimpkontakte Leergehäuse) zum selber crimpen (Crimpzange PSK erforderlich). Oder fertig gecrimpt mit ca. 20cm Kabel. 

Da das Rastermaß auf der Platine nicht für einen normalen 2poligen PSK Steckverbinder (Reichelt Artikel PS 25/2G WS) paßt, wird zudem noch als Adapter ein kleiner Streifen Lochraster benötigt. Darauf wird der PSK Steckverbinder eingelötet. Der Adapter wiederum wird dann auf die Platine gelötet. Evtl. muß man dazu die Transistoren vorsichtig zur Seite biegen. Wichtig ist in jedem Fall, die beiden Leitungen miteinander zu verdrillen, um Störungen auf die Asuro Elektronik u vermindern. 



![][5]  
*Motor Anschlüsse mit PSK Steckverbindern*



![][6]  
*Lochraster Adapter für PSK Steckverbinder *



## Bezugsadressen

*   <http://www.reichelt.de> - PS 25/2G WS Platinensteckverbinder gerade, weiß, 2-polig 



## Weblinks

*   [Datenblatt der Faulhaber Serie 2224][7]

 [1]: http://www.faulhaber-group.com
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/motor_mod.jpg
 [3]: http://www.asurowiki.de/pmwiki/uploads/Main/motor_halter.jpg
 [4]: http://www.asurowiki.de/pmwiki/uploads/Main/faulhaber.jpg
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/mod_motor2.jpg
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/mod_motor1.jpg
 [7]: http://www.faulhaber-group.com/uploadpk/d_2224SR_DFF.pdf