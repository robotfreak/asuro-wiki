# Zusammenbau


## 1. Einleitung

Diese Anleitung ersetzt **nicht** die Original Bauanleitung des ASUROs. Es ist vielmehr eine Ergänzung zur Bauanleitung. Es werden einige Tips für Modifikationen gegeben, um dem Anwender zu ermöglichen, spätere Erweiterungen einfacher durchzuführen. 

### 1.1 Wichtiger Hinweis

Die Leiterplatte des Asuros besteht aus durchkontaktierten Lötaugen. Das Auslöten von falsch eingesetzten Bauteilen, selbst von einzelnen Widerständen ist sehr schwierig. Schnell wird dabei neben den Bauteilen auch die Platine beschädigt. Deshalb gründlich vorgehen, mehrmals überprüfen bevor man ein Bauteil einlötet. Alle Widerstände mit dem Ohmmeter durchmessen. Bei den Farbringen kann man oftmals orange und rot schlecht unterscheiden. Sehr hilfreich ist auch die [Sortierschablone]/http://home.kpn.nl/h.van.winkoop/Asuro/Assembling/AsuAsmPagFrm.htm) von Arexx-Henk zum Vorsortieren der Bauteile. 

## 2. Vorbereitungen

Folgendes Werkzeug wird zum Zusammenbau und evtl. Fehlersuche bzw. Reparatur des ASUROs benötig (empfohlen): 

*   Elektronik Lötkolben (regelbare Lötstation) 
*   Seitenschneider 
*   Flachzange, zum Biegen der Bauteildrähte 
*   flussmittelhaltiges Elektronik Lötzinn, entweder bleifreies oder bleihaltiges Lötzinn verwenden, keinesfalls Mischen. 
*   Schwämmchen um Lötzinnreste vom Lötkolben zu entfernen. 
*   feines Schleifpapier, zum Anrauhen der Achsen. 
*   Eine "helfende Hand" mit Lupe 
*   Multimeter mit Ohmmeter, Dioden Prüfer 
*   Entlötsaugpumpe, zum Entfernen von falsch eingelöteten Bauteilen 
*   Entlötlitze, zum Freimachen der Lötaugen, nachdm man falsch eingelötete Bauteile entfernt hat 

![Verschiedenes Werkzeug](%assets_url%/werkzeug1.jpg "Verschiedenes WerkzeugBots")

![Lötstation ERSA Digital 2000A](%assets_url%/werkzeug2.jpg "Lötstation ERSA Digital 2000A")

![Die helfende Hand](%assets_url%/werkzeug3.jpg "Die helfende Hand")

## 3. Zusammenbau

![ASURO Platine von oben](%assets_url%/platine_oben1.jpg "ASURO Platine von oben")
*ASURO Platine von oben. Ein hochauflösendes Foto gibt es [hier](%assets_url%/platine_oben.jpg)*

![ASURO Platine von unten](%assets_url%/platine_unten1.jpg "ASURO Platine von unten")
*ASURO Platine von unten. Ein hochauflösendnes Foto gibt es [hier](%assets_url%/platine_unten.jpg)*

### 3.1 Teil 1, Befestigen der Achsen

Man beginnt mit dem Festlöten der Getriebeachsen. Vor dem Festlöten sollte man die Achsen mit feinem Schleifpapier (400er Körnung) aufrauen. Aber nur das Stück, das festgelötet wird. Hier kann man bereits die erste Modifikation vornehmen. Die [Odometrie Modifikation](OdometrieModifikation) zur Verringerung des Achsenspiels. Dazu werden die kurzen Achsen nicht ganz in die Kerbe gesteckt, sondern mit 1-2mm Luft. Nach dem Ein löten sollte man die Zahnräder aufstecken und testen ob die sich leichtgängig drehen lassen. Wenn es klemmt, nochmal mit dem Lötkolben nachhelfen. Als Lötkolben empfielt dich hier ein möglichst kräftiger Lötkolben mit breiter Spitze. Bei einer geregelten Lötstation sollte man die Temperatur auf 420 Grad stellen.

![Bestücken der Platine Teil 1](%assets_url%/best_platine1.jpg "Bestücken der Platine Teil 1")
*Bestücken der Platine Teil 1, Achsen einlöten*

### 3.2 Teil 2, Dioden und IC Sockel

Im nächsten Schritt werden die Dioden der Motorbrücken eingelötet (auf Polung achten). Schwarzer Strich auf der Diode muß mit dem Bestückungsaufdruck übereinstimmen. Anschließend noch die IC-Sockel einlöten. Erst mal nur an 2 diagonal gegenüberliegenden Stellen anlöten, dann kontrollieren ob der Sockel plan liegt. Auch hier darauf achten, daß die Kerbe der Fassung mit dem Bestückungsaufdruck übereinstimmt. Dann die restlichen Lötpunkte setzen. Zum Schluß noch den Resonator (Polung ist egal) 

#### Achtung:

Es gibt noch eine Z-Diode, die ähnlich aussieht. Diese gehört zum IR Transceiver. 

![Bestücken der Platine Teil 2](%assets_url%/best_platine2.jpg "Bestücken der Platine Teil 2")
*Bestücken der Platine Teil 2, Dioden und IC-Sockel*

### 3.3 Teil 3, Transistoren und Kondensatoren

Als nächstes sind die Transistoren der H-Brücke dran. Auch hier besteht Verwechslungsgefahr. Es gibt 3 verschiedene Transistortypen, deshalb aufpassen. Die Beschriftung ist manchmal nur unter der Lupe zu entziffern. Das nachträgliche auslöten von falschen Bauteilen ist auch für geübte Löter äußerst schwierig. 

*   4 x BC327 T1, T3, T5, T7 
*   4 x BC337 T2, T4, T6, T8 
*   1 x BC547 Q1 vom IR Tansceiver 

Dann folgen die kleineren Kondensatoren ohne Polung mit den Werten 

*   4 x 100nF C2..C5 Aufdruck 104 
*   2 x 4,7nF C6, C7 Aufdruck 472 

![Bestücken der Platine Teil 3](%assets_url%/best_platine3.jpg "Bestücken der Platine Teil 3")
*Bestücken der Platine Teil 3, Transistoren und Kondensatoren*

### 3.4 Teil 4, Widerstände

Auch bei den Widerständen sollte man sehr stark aufpassen. Nicht blind auf die aufgedruckten Farbringe vertrauen. Besser vor dem Einlöten alle Widerstände mit dem Multimeter nachmessen und die Widerstände dann mit der [Sortierschablone](http://home.kpn.nl/h.van.winkoop/Asuro/Assembling/AsuAsmPagFrm.htm) von Arexx-Henk vorsortieren. 

Teilweise sitzen die Widerstände sehr eng zusammen. Beliebte Fehlerstelle ist der Bereich um R15. Es ist kein Problem 2 Drähte in ein Loch zusammen mit R23 oder R28 zu stecken. Also nie vom Lauf der Beschriftung in die Irre fürhen lassen, sondern nur auf die "Nase" am Kreis achten. R9 und R14 könnten ungewollten Kontakt zueinander aufnehmen, falls diese zu schräg eingelötet werden. 

#### Modifikationen:

*   Es empfiehlt sich den Widerstand R11 durch eine Spule von 47..100µH zu ersetzen. Näheres siehe weiter unten bei [Modifikationen](modifikationen). 
*   Der Widerstand R17 liegt in Reihe zur Versorgungsspannung auf dem Asuro hat 470Ohm. Laut Datenblatt sollten dieser Widerstand 100Ohm sein. Besser wechseln (z.B. gegen R11, wenn man die Spule verwendet). Dies verbessert die Empfangseigeneschaften der Infrarotschnittstelle insbesondere bei schwachen Akkus oder Batterien. 
*   Der Widerstand R24 ist im Bausatz ein 1%er (braun, schwarz, schwarz, braun, braun). Die Stückliste führt R24 jedoch (noch? Dez. 2007) unter den 5%ern auf, so das man beim Bestücken zunächst einen 1000Ohm Widerstand vermissen wird. 

![Bestücken der Platine Teil 4](%assets_url%/best_platine4.jpg "Bestücken der Platine Teil 4")
*Bestücken der Platine Teil 4, Widerstände*

### 3.5 Teil 5, Taster, LEDs und der ganze Rest

Jetzt sind die Taster an der Reihe. Beim Einlöten darauf achten, das nicht zuviel Lötzinn durch die Durchkontaktierungen auf die Platinenoberseite läuft. Das kann zu Kurzschlüssen führen. Bei den LEDs ist wieder auf korrekte Polung zu achten. Abgefalchte Seite muß mit dem Bestückungsaufdruck übereinstimmen. Die Fototransistoren (farblos) und IR Dioden (rosafarbenes Gehäuse) der Odometrie Sensoren kann man leicht verwechseln. Der kleine ausgewölbte Pickel muß jeweils nach außen zu den Zahnrädern zeigen. 

#### Achtung:

Auch bei den beiden großen Kondensatoren muß man auf die Polung achten. Der Minuspol ist auf dem Kondensator markiert. Der längere Pin ist der Pluspol. Auf dem Bestückungsaufdruck ist jeweils der Pluspol markiert. 

#### Modifikationen:

Die Front LED und die Fototransistoren auf der Unterseite sollte man nicht einlöten. Stattdessen die [Liniensensor Modifikation](liniensensormod) vornehmen. Sonst hat man später den Ärger mit dem auslöten, wenn man eine [Erweiterung](erweiterungen) einbauen möchte. 

![Bestücken der Platine Teil 5](%assets_url%/best_platine5.jpg "Bestücken der Platine Teil 5")
*Bestücken der Platine Teil 5, Taster, LEDs und Sonstiges*

### 3.6 Teil 6, Motorverkabelung, Batteriefach

Nun müssen nur noch die Motoren verkabelt werden und das Batteriefach angeklemmt werden. Wichtig ist dabei das Verdrillen der Motoranschlußkabel um Störungen auf die Asuro Elektronik zu vermindern. 

#### Modifikationen

*   Hier kann man als weitere Modifikation die [Motoranschluß](motormod) vornehmen 
*   ebenso die [Batterieanschluß](batteriefachmod) Modifikation. 

![Bestücken der Platine Teil 6](%assets_url%/best_platine6.jpg "Bestücken der Platine Teil 6")
*Bestücken der Platine Teil 6*

### 3.7 Teil 7, Tischtennisball

Den Tischtennisball sollte man erst nach dem Test ohne Prozessor und Gatter IC festkleben. 

#### Modifikationen:

*   [TT Ball Ersatz][43] ersetzen durch die halbierte Deoroller Kugel. Da diese Lösung angeschraubt und nicht geklebt wird, kann man sie jederzeit leicht wieder lösen. 

### 3.8 Erster Test ohne Prozessor und Gatter IC

Wenn keine Bauteile mehr übrig sind hat man es fast geschafft. Zunächst sollte man aber erst noch eine sorgfältige Sichtprüfung von oben und unten durchführen. Am besten geht dies mit Hilfe einer Lupe und bei guter Beleuchtung. Schlechte Lötstellen und Kurzschlüsse kann man bereits damit feststellen und beseitigen. Hilfreich ist auch die Lötseite mit einem in Alkohol getränkten nicht fusselndes Tuch abzureiben und ggfl. noch mit einer alten Zahnbürste hartnäckige Zinnreste zu entfernen. Der Alkohol sollte reiner Alkohol sein, keinesfalls Wodka o.ä. Desinfektionsspray, Spiritus, Kassettenrecorder Reinigungsflüssigkeit, etc. geht genausogut. 

**Wichtig:** Der Prozessor und das Gatter IC werden noch nicht in den Sockel gesteckt. Wenn keine Auffälligkeiten mehr vorhanden sind, kann man die Batterien einlegen und dann den Schalter auf **ON** stellen. Falls jetzt alles korrekt aufgebaut wurde, sollten die beiden Back LEDs schwach leuchten. Evtl. muß man dazu die LEDs mit der Hand abdunkeln. Falls nichts leuchtet, sofort den Schalter wieder auf **OFF** stellen. 

### 3.9 Weiterer optionaler Test ohne Prozessor

Ganz vorsichtige Gemüter können auch noch die Motorbrücken testen, ohne den Prozessor zu stecken. Dazu muß allerdings das Gatter IC eingesetzt werden. 

t.b.c 

### 3.10 Fehlersuche nach fehlgeschlagenem ersten Test

t.b.c 

### 3.11 Der Selbsttest

t.b.c 

### 3.12 Fehler beim Selbstest

t.b.c 

![][44]  
![Der fertige Asuro](%assets_url%/asuro_komplett.jpg "Der fertige Asuro")
*Der fertige Asuro*

## 4. Modifikationen

Folgende Modifikationen lassen sich am besten schon beim Zusammenbau des ASUROs erledigen: 

*   [Batterieanschluß](batteriefachmod) 
*   [Liniensensor Modifikation](liniensensormod) 
*   [Motor Modifikation](motormod) - Motoranschluß 
*   [Odometrie Modifikation](odometriemod) - Achsenspiel verringern 

### 4.1 Modifikation der Analog Spannungsversorgung

Die Analoge Spannungsversorgung des Mikrocontrollers (AVCC) und der analog angeschlossenen Sensoren, wird lediglich durch einen 100 Ohm Widerstand (R11) von der restlichen Versorgungssapnnung getrennt. Hier ist es nach Atmel Vorgaben günstiger eine Spule statt eines Widerstandes zu benutzen. Hierzu wird R11 durch ein 47..100µH Spule ersetzt. 

## 5. Zusätzliche benötigte Bauteile

Um die oben genannten Modifikationen durchführen zu können, werden einige zusätzliche Bauteile benötigt, die nicht zum Lieferumfang des ASUROs gehören.  

| **Modifikation**              | **Bauteil**                                 | **Reichelt Artikelnr.** | **Conrad Artikelnr.** |
||
| Analog Spannungsvers. AVCC    | Drosselspule, Festinduktivität, axial, 100µ   | SMCC 100µ               |                       |
| Motoranschluß/Batterieanschluß | Platinensteckverbinder gerade, weiß, 2-polig | PS 25/2G WS             |                       |
| Liniensensor/Erweiterung      | BUCHSENLEISTE 36 POLIG WIRE WRAP            |                         | 739111 - 62           |

## 6. Siehe auch

* [Modifikationen](modifikationen) - Weitere Modifikationen des ASUROs 

## 7. Weblinks

* [Sortierschablone](http://home.kpn.nl/h.van.winkoop/Asuro/Assembling/AsuAsmPagFrm.htm)
 
