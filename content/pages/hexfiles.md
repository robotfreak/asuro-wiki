# AsuroHexfiles

Ein Hexfile dient zum Speichern von binären Daten in einem Textfile. In Hexfiles beginnt jede Zeile mit einem ':' gefolgt von einer variablen Anzahl von hexadezimal kodierten Bytes. In den Hexfiles des Asuro treten nur 2 der 6 möglichen Typen aus der *Intel Hexadecimal Object File Format Specification* auf, *Datensatz* und *Dateiende*. 

## Datensatz

| Byte     | Wert  |
||
| 1        | L     | [Länge]                |
| 2..3     | A     | [Ladeadresse]        |
| 4        | '00'  | ["Datensatz"]        |
| 5..(4+L) | Daten | [für Adressen A..(A+L-1)] |
| (5+L)    | P     | [Prüfsumme]               |
| Â         | Â      |

Berechnung der Prüfsumme: uint8_t R[],P,L;Â  uint16_t u;  
  
for(P=,L=R[1],u=1; u<=(4+L); ++u)Â    
Â  P-=R[u];

## Dateiende

| Byte | Wert   |
||
| 1    | '00'   |
| 2..3 | '0000' |
| 4    | '01'   | ["Dateiende"] |
| 5    | 'FF'   | [Prüfsumme]        |

## Beispiel eines Asuro-Hexfiles

Ausschnitt eines Asuro-Hexfiles (links Original, rechts aufgeschlüsselt ohne Daten): 

    L    A  T Daten  P
                                                           -- ---- -- ----- --
    :1000000012C02BC01FC129C0ECC027C026C025C00C          : 10 0000 00 ..... 0C
    :1000100024C023C022C021C020C01FC02AC11DC0CF          : 10 0010 00 ..... CF
    ...
    
    ...
    :1006100038F450954095309521953F4F4F4F5F4F9F          : 10 0610 00 ..... 9F
    :100620000895F6F790958095709561957F4F8F4F5F          : 10 0620 00 ..... 5F
    :040630009F4F08953B                                  : 04 0630 00 ..... 3B
    :1006340020202020202052414D454E443A20000DD8          : 10 0634 00 ..... D8
    :100644000A0020202020205852414D454E443A2093          : 10 0644 00 ..... 93
    :1006540000202020202020204532454E443A20000E          : 10 0654 00 ..... 0E
    :1006640020202020464C415348454E443A20005314          : 10 0664 00 ..... 14
    :10067400504D5F5041474553495A453A20003A0D81          : 10 0674 00 ..... 81
    :020684000A006A                                      : 02 0684 00 ..... 6A
    :00000001FF                                          : 00 0000 01       FF
    
    

## Weiterführende Links

*   <http://en.wikipedia.org/wiki/Intel_HEX> - *Intel Hexadecimal Object File Format* 
*   <http://avr.jassenbaum.de/ja-tools/acxutil.html> - Ascii Coded heX Utility (*view, edit, compare and convert* für Hexfiles) 
*   <http://avr.jassenbaum.de/ja-tools/reavr.html> - Reassembler for AVR (Generiert asm-Quelltext direkt aus AVR-Hexfile)  ![][1]  

*Disassemblieren mittels Send To*

 [1]: http://www.stamm-wilbrandt.de/videos/SendTo_ReAVR.gif ""

