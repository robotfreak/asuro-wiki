# TastenKalibrierungC

## Programmcode

Das Kalibrier Programm für die Tastsensoren benötigt eine eigene PollSwitch Funktion, da wir zur Errechnung der MY\_SWITCH\_VALUE Konstante die reinen A/D Wandler Werte brauchen. Deshalb wird hier die MyPollSwitch Funktion verwendet. 

Die SwitchTest Funktion wird in der Hauptscheife der Main Funktion endlos ausgeführt und prüft nacheinander alle Taster durch, die der Anwender nach Aufforderung des Programmes drücken muß. Der Test beginnt mit dem Taster K6 (von vorne auf den ASURO gesehen, links außen beim Ein Schalter) und endet bei K1 (rechts außen am IR Receiver). Der gemessene Wert wird in die Formel aus der Original PollSwitch Funktion zur Berechnung eingesetzt und mit dem Wertebereich 65..74 überprüft ob der geforderte Wert dabei herauskommt. Stimmt der Wert, wird dieser zum Terminalprogramm gesendet. Stimmt der Wert nicht, so werden statt dessen Leerzeichen gesendet. So sollte bei einem korrekt aufgebauten Asuro nach Drücken von K1 der Wert (eventuell auch 2 Werte) für die MY\_SWITCH\_VALUE Konstante gefunden sein. 



Â   
#include <stdlib.h>  
#include "asuro.h"  
  
  
uint16_t MyPollSwitch(void)  
{  
Â  uint16_t i;  
  
Â  DDRD |= SWITCHES; Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  // Port-Bit SWITCHES als Output  
Â  SWITCH_ON; Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â // Port-Bit auf HIGH zur Messung  
Â  ADMUX = (1 << REFS0) | SWITCH; Â  Â  Â  Â // AVCC reference with external capacitor  
Â  Sleep (10);  
  
Â  ADCSRA |= (1 << ADSC); Â  Â  Â  Â  Â  Â  Â  Â // Starte AD-Wandlung  
Â  while (!(ADCSRA & (1 << ADIF))) Â  Â  Â  // Ende der AD-Wandlung abwarten  
Â  Â  ;  
Â  ADCSRA |= (1 << ADIF); Â  Â  Â  Â  Â  Â  Â  Â // AD-Interupt-Flag zuruecksetzen  
  
Â  i = ADCL + (ADCH << 8); Â  Â  Â  Â  Â  Â  Â  // Ergebnis als 16-Bit-Wert  
  
Â  SWITCH_OFF; Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  Â  // Port-Bit auf LOW  
Â  Sleep (5);  
  
Â  return ADC;  
}  
  
  
void SwitchTest(void)  
{  
Â  uint8_t i, j, mval;  
Â  uint16_t adval;  
  
Â  for(i=; i<6; i++)  
Â  {  
Â  Â  SerPrint("\r\nPress Key ");  
Â  Â  PrintInt(6-i);  
Â  Â  SerPrint("\r\n");  
Â  Â  while (MyPollSwitch() == 1023); Â   
Â  Â  adval = MyPollSwitch();  
Â  Â  adval = MyPollSwitch();  
Â  Â  adval = MyPollSwitch();  
Â  Â  adval = MyPollSwitch();  
Â  Â  // testet den Wertebereich von 55..74 mit dem gemessenen A/D Wert  
Â  Â  for(j=50; j<75;j++)  
Â  Â  {  
Â  Â  Â  mval = ((10240000L / (long)adval - 10000L) * (long)(j) + 5000L) / 10000;  
Â  Â  Â  if (mval == (1<<i)) Â  // Wert passt  
Â  Â  Â  Â  PrintInt(j);  
Â  Â  Â  else Â  Â  Â  Â  Â  Â  Â  Â  Â // Wert passt nicht  
Â  Â  Â  Â  SerPrint(" Â ");  
Â  Â  Â  SerPrint(" ");  
Â  Â  }   
Â  Â  Msleep(2000);  
Â  } Â    
}  
  
  
int main(void)  
{  
  
Â  Init();  
Â  SerPrint("\r\nTastsensor Kalibration\r\n");  
Â  while (1)  
Â  {  
Â  Â  SwitchTest();  
Â  }  
}

[[$[Get Code]]][1]

[TasterKalibration.zip][2] 



## Auswertung

So sieht dann die Ausgabe des Programmes im Terminalprogramm aus: 



    Tastsensor Kalibration
    
     Press Key 6
     50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 
     Press Key 5
     50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 
     Press Key 4
                          57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72       
     Press Key 3
                                   60 61 62 63 64 65 66 67                      
     Press Key 2
                                      61 62 63 64                               
     Press Key 1
                                         62 63                                  
     Press Key 6
    

Wie man leicht sieht ist, hat die Taste K1 den engsten Spielraum. Der ermittelte Wert für die MY\_SWITCH\_VALUE Konstante für diesen Asuro liegt hier bei 62 oder 63. Da mein anderer Asuro hier 61 und 62 als mögliche Werte errechnet, entschließe ich mich spontan für den Wert 62. Sollte eine Taste aus dem Schema abweichen, bzw. der gefundene Wert nicht bei allen Tastern gefunden werden, liegt wahrscheinlich ein Fehler bei den Widerstandswerten vor. Eventuell wiederholt man erst den Test. Vielleicht hat man ja nur die Taste nicht fest genug gedrückt. Bleibt das Kalibrierprogramm bei einer Taste hängen, liegt eine Unterbrechung im Signalweg vor. Läuft das Testprogramm durch, ohne das eine Taste gedrückt wurde, liegt ein Kurzschluß vor.

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/TastenKalibrierungC?action=sourceblock&num=1
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/TasterKalibration.zip