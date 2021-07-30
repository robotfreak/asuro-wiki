# Portbelegung

ASURO Portbelegung. 



| **Port** | ** Pin** | **I/O**      | **Funktion**                      | **Anmerkung**                 |
||
| PB0      | 14       | Output       | Status LED grün                   | Â                              |
| PB1      | 15       | OC1A         | PWM für linken Motor              | Â                              |
| PB2      | 16       | OC1B         | PWM für rechten Motor             | Â                              |
| PB3      | 17       | OC2          | 36kHz Modulation IR LED           | Sleep Timer, CON1 Erweiterung |
| PB4      | 18       | Output       | vorwärts/rückwärts rechter Motor      | Â                              |
| PB5      | 19       | Output       | vorwärts/rückwärts rechter Motor      | Â                              |
| PB6      | 9        | XTAL1        | 8 Mhz Quarz                       | Â                              |
| PB7      | 7        | XTAL2        | 8 Mhz Quarz                       | Â                              |
| Â         |
| PC0      | 23       | ADC0/Output  | Odometrie links/ Back LED links   | nicht gleichzeitig            |
| PC1      | 24       | ADC1/Output  | Odometrie rechts/ Back LED rechts | nicht gleichzeitig            |
| PC2      | 25       | ADC2         | Fototransistor unten links        | für Erweiterung*              |
| PC3      | 26       | ADC3         | Fototransistor unten rechts       | für Erweiterung*              |
| PC4      | 27       | ADC4         | Auswertung des Tasten             | Â                              |
| PC5      | 28       | ADC5         | Batteriespannungs Messung         | Â                              |
| PC6      | 1        | Reset        | \---|                             | Â                              |
| Â         |
| PD0      | 2        | RXD          | UART empfangen                    | Â                              |
| PD1      | 3        | TXD          | UART senden                       | Â                              |
| PD2      | 4        | Output       | Status LED rot                    | CON2 Erweiterung INT0         |
| PD3      | 5        | INT1         | Interrupt für Taster              | Â                              |
| PD4      | 6        | Output       | vorwärts/rückwärts linker Motor       | Â                              |
| PD5      | 11       | Output       | vorwärts/rückwärts linker Motor       | Â                              |
| PD6      | 12       | Output       | Front LED unten                   | für Erweiterung*              |
| PD7      | 13       | Output/Input | Umschaltung Odometrie/Back LED    | Â                              |

(*) bei Verwendung dieser Ports auf der Erweiterungsplatine, muß auf den Linienverfolger verzichtet werden. Man kann aber die entsprechenden Bauteile entfernen und für das [Linienverfolger Modul][1] alternativ zur Erweiterungsplatine verwenden.

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LinienverfolgerModul