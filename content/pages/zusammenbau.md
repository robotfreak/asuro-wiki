# Zusammenbau


## 1.â€‚ Einleitung<vspace>

Diese Anleitung ersetzt **nicht** die Original Bauanleitung des ASUROs. Es ist vielmehr eine Ergänzung zur Bauanleitung. Es werden einige Tips für Modifikationen gegeben, um dem Anwender zu ermöglichen, spätere Erweiterungen einfacher durchzuführen. <vspace>

### 1.1â€‚ Wichtiger Hinweis<vspace>

Die Leiterplatte des Asuros besteht aus durchkontaktierten Lötaugen. Das Auslöten von falsch eingesetzten Bauteilen, selbst von einzelnen Widerständen ist sehr schwierig. Schnell wird dabei neben den Bauteilen auch die Platine beschädigt. Deshalb gründlich vorgehen, mehrmals überprüfen bevor man ein Bauteil einlötet. Alle Widerstände mit dem Ohmmeter durchmessen. Bei den Farbringen kann man oftmals orange und rot schlecht unterscheiden. Sehr hilfreich ist auch die [Sortierschablone][23] von Arexx-Henk zum Vorsortieren der Bauteile. <vspace>

## 2.â€‚ Vorbereitungen<vspace>

Folgendes Werkzeug wird zum Zusammenbau und evtl. Fehlersuche bzw. Reparatur des ASUROs benötig (empfohlen): <vspace>

*   Elektronik Lötkolben (regelbare Lötstation) 
*   Seitenschneider 
*   Flachzange, zum Biegen der Bauteildrähte 
*   flussmittelhaltiges Elektronik Lötzinn, entweder bleifreies oder bleihaltiges Lötzinn verwenden, keinesfalls Mischen. 
*   Schwämmchen um Lötzinnreste vom Lötkolben zu entfernen. 
*   feines Schleifpapier, zum Anrauhen der Achsen. 
*   Eine "helfende Hand" mit Lupe 
*   Multimeter mit Ohmmeter, Dioden Prüfer 
*   Entlötsaugpumpe, zum Entfernen von falsch eingelöteten Bauteilen 
*   Entlötlitze, zum Freimachen der Lötaugen, nachdm man falsch eingelötete Bauteile entfernt hat <vspace>

![][24]  
*Verschiedenes Werkzeug*<vspace>

![][25]  
*Lötstation ERSA Digital 2000A*<vspace>

![][26]  
*Die helfende Hand*<vspace>

## 3.â€‚ Zusammenbau<vspace>

![][27]  
*ASURO Platine von oben. Ein hochauflösendes Foto gibt es [hier][28]*<vspace>

![][29]  
*ASURO Platine von unten. Ein hochauflösendnes Foto gibt es [hier][30]*<vspace>

### 3.1â€‚ Teil 1, Befestigen der Achsen<vspace>

Man beginnt mit dem Festlöten der Getriebeachsen. Vor dem Festlöten sollte man die Achsen mit feinem Schleifpapier (400er Körnung) aufrauen. Aber nur das Stück, das festgelötet wird. Hier kann man bereits die erste Modifikation vornehmen. Die [Odometrie Modifikation][31] zur Verringerung des Achsenspiels. Dazu werden die kurzen Achsen nicht ganz in die Kerbe gesteckt, sondern mit 1-2mm Luft. Nach dem Ein löten sollte man die Zahnräder aufstecken und testen ob die sich leichtgängig drehen lassen. Wenn es klemmt, nochmal mit dem Lötkolben nachhelfen. Als Lötkolben empfielt dich hier ein möglichst kräftiger Lötkolben mit breiter Spitze. Bei einer geregelten Lötstation sollte man die Temperatur auf 420 Grad stellen. <vspace>

![][32]  
*Bestücken der Platine Teil 1, Achsen einlöten*<vspace>

### 3.2â€‚ Teil 2, Dioden und IC Sockel<vspace>

Im nächsten Schritt werden die Dioden der Motorbrücken eingelötet (auf Polung achten). Schwarzer Strich auf der Diode muß mit dem Bestückungsaufdruck übereinstimmen. Anschließend noch die IC-Sockel einlöten. Erst mal nur an 2 diagonal gegenüberliegenden Stellen anlöten, dann kontrollieren ob der Sockel plan liegt. Auch hier darauf achten, daß die Kerbe der Fassung mit dem Bestückungsaufdruck übereinstimmt. Dann die restlichen Lötpunkte setzen. Zum Schluß noch den Resonator (Polung ist egal) <vspace>

#### Achtung:

Es gibt noch eine Z-Diode, die ähnlich aussieht. Diese gehört zum IR Transceiver. 

![][33]  
*Bestücken der Platine Teil 2, Dioden und IC-Sockel*<vspace>

### 3.3â€‚ Teil 3, Transistoren und Kondensatoren<vspace>

Als nächstes sind die Transistoren der H-Brücke dran. Auch hier besteht Verwechslungsgefahr. Es gibt 3 verschiedene Transistortypen, deshalb aufpassen. Die Beschriftung ist manchmal nur unter der Lupe zu entziffern. Das nachträgliche auslöten von falschen Bauteilen ist auch für geübte Löter äußerst schwierig. <vspace>

*   4 x BC327 T1, T3, T5, T7 
*   4 x BC337 T2, T4, T6, T8 
*   1 x BC547 Q1 vom IR Tansceiver <vspace>

Dann folgen die kleineren Kondensatoren ohne Polung mit den Werten <vspace>

*   4 x 100nF C2..C5 Aufdruck 104 
*   2 x 4,7nF C6, C7 Aufdruck 472 <vspace>

![][34]  
*Bestücken der Platine Teil 3, Transistoren und Kondensatoren*<vspace>

### 3.4â€‚ Teil 4, Widerstände<vspace>

Auch bei den Widerständen sollte man sehr stark aufpassen. Nicht blind auf die aufgedruckten Farbringe vertrauen. Besser vor dem Einlöten alle Widerstände mit dem Multimeter nachmessen und die Widerstände dann mit der [Sortierschablone][23] von Arexx-Henk vorsortieren. <vspace>

Teilweise sitzen die Widerstände sehr eng zusammen. Beliebte Fehlerstelle ist der Bereich um R15. Es ist kein Problem 2 Drähte in ein Loch zusammen mit R23 oder R28 zu stecken. Also nie vom Lauf der Beschriftung in die Irre fürhen lassen, sondern nur auf die "Nase" am Kreis achten. R9 und R14 könnten ungewollten Kontakt zueinander aufnehmen, falls diese zu schräg eingelötet werden. <vspace>

#### Modifikationen:<vspace>

*   Es empfiehlt sich den Widerstand R11 durch eine Spule von 47..100µH zu ersetzen. Näheres siehe weiter unten bei [Modifikationen][35]. 
*   Der Widerstand R17 liegt in Reihe zur Versorgungsspannung auf dem Asuro hat 470Ohm. Laut Datenblatt sollten dieser Widerstand 100Ohm sein. Besser wechseln (z.B. gegen R11, wenn man die Spule verwendet). Dies verbessert die Empfangseigeneschaften der Infrarotschnittstelle insbesondere bei schwachen Akkus oder Batterien. 
*   Der Widerstand R24 ist im Bausatz ein 1%er (braun, schwarz, schwarz, braun, braun). Die Stückliste führt R24 jedoch (noch? Dez. 2007) unter den 5%ern auf, so das man beim Bestücken zunächst einen 1000Ohm Widerstand vermissen wird. <vspace>

![][36]  
*Bestücken der Platine Teil 4, Widerstände*<vspace>

### 3.5â€‚ Teil 5, Taster, LEDs und der ganze Rest<vspace>

Jetzt sind die Taster an der Reihe. Beim Einlöten darauf achten, das nicht zuviel Lötzinn durch die Durchkontaktierungen auf die Platinenoberseite läuft. Das kann zu Kurzschlüssen führen. Bei den LEDs ist wieder auf korrekte Polung zu achten. Abgefalchte Seite muß mit dem Bestückungsaufdruck übereinstimmen. Die Fototransistoren (farblos) und IR Dioden (rosafarbenes Gehäuse) der Odometrie Sensoren kann man leicht verwechseln. Der kleine ausgewölbte Pickel muß jeweils nach außen zu den Zahnrädern zeigen. <vspace>

#### Achtung:<vspace>

Auch bei den beiden großen Kondensatoren muß man auf die Polung achten. Der Minuspol ist auf dem Kondensator markiert. Der längere Pin ist der Pluspol. Auf dem Bestückungsaufdruck ist jeweils der Pluspol markiert. <vspace>

#### Modifikationen:<vspace>

Die Front LED und die Fototransistoren auf der Unterseite sollte man nicht einlöten. Stattdessen die [Liniensensor Modifikation][37] vornehmen. Sonst hat man später den Ärger mit dem auslöten, wenn man eine [Erweiterung][38] einbauen möchte. <vspace>

![][39]  
*Bestücken der Platine Teil 5, Taster, LEDs und Sonstiges*<vspace>

### 3.6â€‚ Teil 6, Motorverkabelung, Batteriefach<vspace>

Nun müssen nur noch die Motoren verkabelt werden und das Batteriefach angeklemmt werden. Wichtig ist dabei das Verdrillen der Motoranschlußkabel um Störungen auf die Asuro Elektronik zu vermindern. <vspace>

#### Modifikationen<vspace>

*   Hier kann man als weitere Modifikation die [Motoranschluß][40] vornehmen 
*   ebenso die [Batterieanschluß][41] Modifikation. <vspace>

![][42]  
*Bestücken der Platine Teil 6*<vspace>

### 3.7â€‚ Teil 7, Tischtennisball<vspace>

Den Tischtennisball sollte man erst nach dem Test ohne Prozessor und Gatter IC festkleben. <vspace>

#### Modifikationen:<vspace>

*   [TT Ball Ersatz][43] ersetzen durch die halbierte Deoroller Kugel. Da diese Lösung angeschraubt und nicht geklebt wird, kann man sie jederzeit leicht wieder lösen. <vspace>

### 3.8â€‚ Erster Test ohne Prozessor und Gatter IC<vspace>

Wenn keine Bauteile mehr übrig sind hat man es fast geschafft. Zunächst sollte man aber erst noch eine sorgfältige Sichtprüfung von oben und unten durchführen. Am besten geht dies mit Hilfe einer Lupe und bei guter Beleuchtung. Schlechte Lötstellen und Kurzschlüsse kann man bereits damit feststellen und beseitigen. Hilfreich ist auch die Lötseite mit einem in Alkohol getränkten nicht fusselndes Tuch abzureiben und ggfl. noch mit einer alten Zahnbürste hartnäckige Zinnreste zu entfernen. Der Alkohol sollte reiner Alkohol sein, keinesfalls Wodka o.ä. Desinfektionsspray, Spiritus, Kassettenrecorder Reinigungsflüssigkeit, etc. geht genausogut. <vspace>

**Wichtig:** Der Prozessor und das Gatter IC werden noch nicht in den Sockel gesteckt. Wenn keine Auffälligkeiten mehr vorhanden sind, kann man die Batterien einlegen und dann den Schalter auf **ON** stellen. Falls jetzt alles korrekt aufgebaut wurde, sollten die beiden Back LEDs schwach leuchten. Evtl. muß man dazu die LEDs mit der Hand abdunkeln. Falls nichts leuchtet, sofort den Schalter wieder auf **OFF** stellen. <vspace>

### 3.9â€‚ Weiterer optionaler Test ohne Prozessor<vspace>

Ganz vorsichtige Gemüter können auch noch die Motorbrücken testen, ohne den Prozessor zu stecken. Dazu muß allerdings das Gatter IC eingesetzt werden. <vspace>

t.b.c <vspace>

### 3.10â€‚ Fehlersuche nach fehlgeschlagenem ersten Test<vspace>

t.b.c <vspace>

### 3.11â€‚ Der Selbsttest<vspace>

t.b.c <vspace>

### 3.12â€‚ Fehler beim Selbstest<vspace>

t.b.c <vspace>

![][44]  
*Der fertige Asuro*<vspace>

## 4.â€‚ Modifikationen<vspace>

Folgende Modifikationen lassen sich am besten schon beim Zusammenbau des ASUROs erledigen: <vspace>

*   [Batterieanschluß][41] 
*   [Liniensensor Modifikation][37] 
*   [Motor Modifikation][40] - Motoranschluß 
*   [Odometrie Modifikation][31] - Achsenspiel verringern <vspace>

### 4.1â€‚ Modifikation der Analog Spannungsversorgung<vspace>

Die Analoge Spannungsversorgung des Mikrocontrollers (AVCC) und der analog angeschlossenen Sensoren, wird lediglich durch einen 100 Ohm Widerstand (R11) von der restlichen Versorgungssapnnung getrennt. Hier ist es nach Atmel Vorgaben günstiger eine Spule statt eines Widerstandes zu benutzen. Hierzu wird R11 durch ein 47..100µH Spule ersetzt. <vspace>

## 5.â€‚ Zusätzliche benötigte Bauteile<vspace>

Um die oben genannten Modifikationen durchführen zu können, werden einige zusätzliche Bauteile benötigt, die nicht zum Lieferumfang des ASUROs gehören. <vspace> 

| **Modifikation**              | **Bauteil**                                 | **Reichelt Artikelnr.** | **Conrad Artikelnr.** |
||
| Analog Spannungsvers. AVCC    | Drosselspule, Festinduktivität, axial, 100µ   | SMCC 100µ               |                       |
| Motoranschluß/Batterieanschluß | Platinensteckverbinder gerade, weiß, 2-polig | PS 25/2G WS             |                       |
| Liniensensor/Erweiterung      | BUCHSENLEISTE 36 POLIG WIRE WRAP            |                         | 739111 - 62           |<vspace>

## 6.â€‚ Siehe auch<vspace>

*   [Modifikationen][45] - Weitere Modifikationen des ASUROs <vspace>

## 7.â€‚ Weblinks

 [1]: javascript:toggle('tocid');
 [2]: #toc1
 [3]: #toc2
 [4]: #toc3
 [5]: #toc4
 [6]: #toc5
 [7]: #toc6
 [8]: #toc7
 [9]: #toc8
 [10]: #toc9
 [11]: #toc10
 [12]: #toc11
 [13]: #toc12
 [14]: #toc13
 [15]: #toc14
 [16]: #toc15
 [17]: #toc16
 [18]: #toc17
 [19]: #toc18
 [20]: #toc19
 [21]: #toc20
 [22]: #toc21
 [23]: http://home.kpn.nl/h.van.winkoop/Asuro/Assembling/AsuAsmPagFrm.htm
 [24]: http://www.asurowiki.de/pmwiki/uploads/Main/werkzeug1.jpg ""
 [25]: http://www.asurowiki.de/pmwiki/uploads/Main/werkzeug2.jpg ""
 [26]: http://www.asurowiki.de/pmwiki/uploads/Main/werkzeug3.jpg ""
 [27]: http://www.asurowiki.de/pmwiki/uploads/Main/platine_oben1.jpg ""
 [28]: http://www.asurowiki.de/pmwiki/uploads/Main/platine_oben.jpg
 [29]: http://www.asurowiki.de/pmwiki/uploads/Main/platine_unten1.jpg ""
 [30]: http://www.asurowiki.de/pmwiki/uploads/Main/platine_unten.jpg
 [31]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/OdometrieModifikation
 [32]: http://www.asurowiki.de/pmwiki/uploads/Main/best_platine1.jpg ""
 [33]: http://www.asurowiki.de/pmwiki/uploads/Main/best_platine2.jpg ""
 [34]: http://www.asurowiki.de/pmwiki/uploads/Main/best_platine3.jpg ""
 [35]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Zusammenbau#Modifikationen
 [36]: http://www.asurowiki.de/pmwiki/uploads/Main/best_platine4.jpg ""
 [37]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LiniensensorModifikation
 [38]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Erweiterungen
 [39]: http://www.asurowiki.de/pmwiki/uploads/Main/best_platine5.jpg ""
 [40]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MotorModifikation
 [41]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/BatteriefachModifikation
 [42]: http://www.asurowiki.de/pmwiki/uploads/Main/best_platine6.jpg ""
 [43]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/TTBallErsatz
 [44]: http://www.asurowiki.de/pmwiki/uploads/Main/asuro_komplett.jpg ""
 [45]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Modifikationen

