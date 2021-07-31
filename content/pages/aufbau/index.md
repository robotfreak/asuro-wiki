---
Title: Aufbau
Template: section
---

# Aufbau

![Asuro von oben](%assets_url%/asuro_oben.jpg)


## ASURO Aufbau

Die Platine für die Elektronik dient gleichzeitig als Chassis und Fahrgestell. Je 2 Achsen für die Getriebe und die Räder werden direkt auf die Platine gelötet. Als Stützrad dient ein halber TT-Ball, der mit Superkleber von unten auf die Platine geklebt wird. 

*   [Prozessor](prozessor). Atmel AVR 8-Bit RISC [ATmega8L][7]. 
*   2 [Motorbrücken](motorbruecke). Diskret aufgebaut mit Transistoren. 
*   [Linienfolger](liniensensor) mit 2 Fototransistoren 
*   2 [Odometrie Sensoren](odometrie) an den Räder. 30 oder 40 Impulse pro Umdrehung, je nach verwendeter Encoderscheibe. 
*   6 [Tasten][(tasten.md) als Stoßschalter oder für Benutzereingaben an der Vorderseite. 
*   [Infrarotschnittstelle](infrarotschnittstelle) 2400Baud bidirektional zur PC Kommunikation und Programmierung. 
*   [Stromversorgung](stromversorgung) über 4 Micro Zellen AAA. Akkus können verwendet werden. Spannungsüberwachung über Widerstandsteiler. 
*   5 [LEDs](led-anzeigen) für Statusanzeigen. 

##  Zubehör

*   [Infrarot RS232 Transceiver](infrarot-rs232-transceiver) - Im ASURO Bausatz enthalten 
*   [Infrarot USB Transceiver](infrarot-usb-transceiver) - Optional erhältlich 

## Technische Daten

| **Allgemeines**                    |                                                                                             |
||
| Abmessungen (LxBxH):               | ca. 117x122x45mm                                                                              |
| Stromversorgung:                   | 4 x AAA/Micro-Batterien oder Akkus (4 x 1,5V -> 6V mit Batterien, 4 x 1,2V -> 4,8V mit Akkus) |
| **Motoren**                        |                                                                                             |
| Typ:                               | Igarashi 2025-02, Conrad Artikel-Nr.: 244414 -V3                                            |
| Abmessungen:                       | 25,0 mm Länge, 20,0 mm Durchmesser, 2,00 mm Wellendurchmesser                               |
| Gewicht:                           | 18g                                                                                           |
| Nennspannung:                      | 12V                                                                                           |
| Spannungsbereich:                  | 3..12V                                                                                        |
| Leerlaufdrehzahl:                  | 17500 Upm                                                                                     |
| Stromaufnahme:                     | 0,12 A (Leerlauf) 0,34 A (Nennbetrieb)                                                        |
| Wirkungsgrad:                      | 30%                                                                                           |
| Drehmoment:                        | 0,10 Ncm                                                                                      |
| Innenwiderstand:                   | Ri=ca. 16 Ohm, (Nominal Terminal Resistance)                                                  |
| Motorkonstanten:                   | ke=0,006087 Vs/rad (Back EMF constant), km=0.00654 Nm/A (Motor torque constant)               |
| **Reifen und Radstand**            | Â                                                                                              |
| Spurweite:                         | ca. 105mm                                                                                     |
| Reifendurchmesser:                 | ca. 38mm                                                                                      |
| Reifenumfang:                      | ca. 120mm                                                                                     |
| Reifengewicht:                     | ca. 15g                                                                                       |
| **Getriebe und Übersetzung**        | Â                                                                                              |
| Encoderscheibe:                    | 2 Varianten, grob 8 Ticks, fein 12 Ticks                                                      |
| Motorritzel:                       | 10 Zähne, Modul 0,5, 1,9mm Bohrung                                                              |
| Getrieberad 1:                     | 50/10 Zähne, Modul 0,5, 3,1mm Bohrung                                                           |
| Getrieberad 2:                     | 50/12 Zähne, Modul 0,5, 3,1mm Bohrung                                                           |
| Motor/Encoderscheibenuntersetzung: | 1:5                                                                                           |
| Motor/Rad Untersetzung:            | 1:25                                                                                          |
| Encoder/Weg-Auflösung:                | mit 8 Tick Encoderscheibe ~3mm, mit 12 Tick Encoderscheibe ~2mm                               |
| **Gewicht**                        | Â                                                                                              |
| Gewicht:                           | ca. 170g (mit Micro Akkus/Batterien), ca. 240g (mit Mignon Akkus/Batterien)                   |
| Gewichtsverteilung:                | Hinterrädern 65%, Ball 35%                                                                      |
| **Sonstiges**                      | Â                                                                                              |
| Reibungskoeffizient Ball:          | 0,3 (Gleitreibung)                                                                            |
| Haftung der Reifen:                | 0,7 (Haftreibung)                                                                             |

Quelle: Conrad Katalog bzw. Roboternetz. Angaben ohne Gewähr. 


