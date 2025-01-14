# Prozessor

![](%assets_url%/processor.jpg)  
*AVR ATmega8*

Das 'Gehirn' des ASURO ist der AVR 8-Bit RISC Prozessor [ATmega8L](http://www.atmel.com/dyn/products/product_card.asp?part_id=2004) von [Atmel](http://www.atmel.com). 

*   8 kByte Flash Programmspeicher. Bis zu 10000 mal beschreibbar. (1 kByte vom [Bootloader](bootloader) belegt. 7 kByte sind für Anwenderprogramme verfügbar.) 
*   1 kByte SRAM. 
*   512 Byte EEPROM. Bis zu 100000 mal beschreibbar. 
*   6 10-bit A/D-Wandler. 
*   Bis zu 8 MIPS Durchsatz bei 8 Mhz Takt. 
*   2.7 - 5.5 Volt Betriebsspannung. 
*   28-Pin PDIP Gehäuse. 

## ATmega8 Pinbelegung

![][5]  
*AVR ATmega8 Pinbelegung*

## ATmega8 Blockschaltbild

![][6]  
*AVR ATmega8 Blockdiagramm*

## ASURO Portbelegung

Der AVR ATmega8 Prozessor verfügt über insgesamt 23 verfügbare Ein-/Ausgabe Ports, davon können 6 A/D Wandler Ports. Alle Ports sind in 8er Gruppen zusammengefaßt zu Port B, C und D. Viele der Ports haben dabei neben der Funktion als Ein-/ Ausgang auch Sonderfunktionen, wie z.B. UART, PWM, I2C oder SPI Funktionen. So werden beim Asuro 2 Ports für den externen Quarz benötigt, dazu kommt noch der Reset Pin, der zu nichts anderem verwendet werden kann. Dadurch reduziert sich die vefügbare Portanzahl auf 20. Alle verfügbaren Ports sind beim Asuro belegt. Um Erweiterungen benutzen zu können, muß man deshalb auf etwas vorhandenes verzichten. Im konkreten Fall auf den [Liniensensor](liniensensor). Läßt man dazu die beiden Fototransistoren und die Front LED weg, hat man 2 A/D Ports und 1 Digitalport frei. Zudem liegen noch die rote Status LED und das 36kHz Trägersignal für die IR Sende LED auf einem Steckverbinder, und können mit Einschränkungen für Erweiterungen verwendet werden. 

| **Port** | ** Pin** | **I/O**      | **Funktion**                     | **Anmerkung**                 |
||
| PB0      | 14       | Output       | Status LED grün                   |                               |
| PB1      | 15       | OC1A         | PWM für linken Motor                  |                               |
| PB2      | 16       | OC1B         | PWM für rechten Motor                 |                               |
| PB3      | 17       | OC2          | 36kHz Modulation IR LED          | Sleep Timer, CON1 Erweiterung |
| PB4      | 18       | Output       | vorwärts/rückwärts rechter Motor        |                               |
| PB5      | 19       | Output       | vorwärts/rückwärts rechter Motor        |                               |
| PB6      | 9        | XTAL1        | 8 Mhz Quarz                      |                               |
| PB7      | 7        | XTAL2        | 8 Mhz Quarz                      |                               |
|          |
| PC0      | 23       | ADC0/Output  | Odometrie links/ Back LED rechts | nicht gleichzeitig            |
| PC1      | 24       | ADC1/Output  | Odometrie rechts/ Back LED links | nicht gleichzeitig            |
| PC2      | 25       | ADC2         | Fototransistor unten links       | für Erweiterung*                   |
| PC3      | 26       | ADC3         | Fototransistor unten rechts      | für Erweiterung*                   |
| PC4      | 27       | ADC4         | Auswertung des Tasten            |                               |
| PC5      | 28       | ADC5         | Batteriespannungs Messung        |                               |
| PC6      | 1        | Reset        | \---|                            |                               |
|          |
| PD0      | 2        | RXD          | UART empfangen                   |                               |
| PD1      | 3        | TXD          | UART senden                      |                               |
| PD2      | 4        | Output       | Status LED rot                   | CON2 Erweiterung INT0         |
| PD3      | 5        | INT1         | Interrupt für Taster                  |                               |
| PD4      | 6        | Output       | vorwärts/rückwärts linker Motor         |                               |
| PD5      | 11       | Output       | vorwärts/rückwärts linker Motor         |                               |
| PD6      | 12       | Output       | Front LED unten                  | für Erweiterung*                   |
| PD7      | 13       | Output/Input | Umschaltung Odometrie/Back LED   |                               |

(*) bei Verwendung dieser Ports auf der Erweiterungsplatine, muß auf den Linienverfolger verzichtet werden. Man kann aber die entsprechenden Bauteile entfernen und für das [Linienverfolger Modul](liniensensor-modul) alternativ zur Erweiterungsplatine verwenden. 

## Weiterführende Links:

*   [Atmel](http://www.atmel.com)
*   [ATmega8L](http://www.atmel.com/dyn/products/product_card.asp?part_id=2004) 
*   [ATmega8 Datasheet][9]

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/processor.jpg ""
 [2]: http://www.atmel.com/dyn/products/product_card.asp?part_id=2004
 [3]: http://www.atmel.com
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bootloader
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/mega8pinout.png ""
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/mega8block.png ""
 [7]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Linienfolger
 [8]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LinienverfolgerModul
 [9]: http://www.atmel.com/dyn/resources/prod_documents/doc2486.pdf

