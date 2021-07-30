# RC5DemoC

## Einleitung

Ein Programm zum Steuern des ASURO über eine Infrarot Fernbedienung. Dies ist eine verbesserte Version der IRDemo aus dem ASURO Selbsttest. Der Programmcode stammt ursprünglich vom c't-Bot und ist mit geringen Änderungen für den ASURO adaptiert worden. Das Originalprogramm funktioniert leider überhaupt nicht, da eine mir unbekannte Fernbedienung verwendet wurde. In dieser Version kann jede Fernbedienung verwendet werden, die RC5 Codes liefert. Dies sind praktisch alle Universalfernbedienungen. 



### RC5 Code

RC5 ist eine Erfindung von Philips und Marantz. Wer noch einen alten Philips Fernseher oder Videorecorder besitzt, kann es auch mit der Gerätefernbedienung versuchen. Neuere Geräte von Philips benutzen dagegen den RC6 Code. Dieser ist nicht kompatibel zu RC5. Auch die Fernbedienungen von Hauppauge, die bei deren TV Karten beiliegen, liefern RC5 Code. Wer es mit der Universalfernbedienung probiert sollte den Wahlschalter auf TV oder Videorecorder stellen und als Gerätecode Philips einstellen. 



| ![][1]                            | ![][2]                   |
||
| *Hauppauge TV Card Fernbedienung* | *Universalfernbedienung* |



## Programm

Der Programmcode aller Beispiel- und Testprogramme kann im [Download Bereich][3] heruntergeladen werden, bzw. befinden sich im Examples Ordner der [Asuro Lib][4]. Ab der Version 2.70RC3 der [Asuro Lib][4] sind die RC5 Funktionen bereits enthalten. Zur Verwendung muß lediglich das Makefile angepaßt werden und die Header-Datei [rc.h][5] eingebunden werden. Ein Beispielprojekt befindet sich im Examples Ordner der [Asuro Lib][4] unter [RC5Test][6] 



### Programmcode rc5.h

#include <inttypes.h>  
  
#define RC5_TOGGLE Â 0x0800 Â  Â /*!< Das RC5-Toggle-Bit */  
#define RC5_ADDRESS 0x07C0 Â  Â /*!< Der Adressbereich */  
#define RC5_COMMAND 0x103F Â  Â /*!< Der Kommandobereich */  
  
#define RC5\_MASK (RC5\_COMMAND)  
  
extern volatile uint16_t Â RC5data; Â  Â  /*!< letztes komplett gelesenes RC5-Paket */  
extern volatile uint8_t Â  enableRC5; Â  /*!< schaltet die RC5 Abfrage ein/aus */  
  
/*!  
Â * Init RC5  
Â */  
void InitRC5(void);  
  
/*!  
Â * RC5 Daten lesen  
Â * @return Wert von ir\_data, loescht anschliessend ir\_data  
Â */  
uint16_t ReadRC5(void);  
  
/*!  
Â * RC5 Interrupt Serviceroutine,  
Â * wird ca. alle 222.2 us aufgerufen  
Â */  
void IsrRC5(void);

[[$[Get Code]]][7]



### Programmcode rc5.c



// ========================================================================  
// RC5 Infrarot-Empfaenger  
// ========================================================================  
#include <avr/io.h>  
#include "rc5.h"  
  
  
// \---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|--  
// Timing  
// \---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|\---|--  
#define IR\_SAMPLES\_PER_BIT Â  Â  8 Â  /*!< 8 Samples per Bit */  
#define IR\_SAMPLES\_PER\_BIT\_EARLY 6 Â /*!< Flanke fruehestens nach 7 Samples */  
#define IR\_SAMPLES\_PER\_BIT\_LATE 10 Â /*!< Flanke spaetestens nach 9 Samples */  
#define IR\_SAMPLES\_PER\_BIT\_MIN Â  3 Â /*!< Flanke vor 3 Samples -> paket verwerfen */  
#define IR\_PAUSE\_SAMPLES Â  Â  Â  250 Â /*!< Startbit ist erst nach 200 Samples ohne */  
// Pegelaenderung gueltig -- eigentlich muesste  
// man rund 500 Samples abwarten (50 x  
// Bitzeit), doch weil der Samplezaehler ein  
// Byte ist, beschraenken wir uns hier auf ein  
// Minimum von 250 Samples  
  
#define IR_PORT Â  PORTD Â  Â  /*!< Port D */  
#define IR_DDR Â  Â DDRD Â  Â  Â /*!< DDR of Port D */  
#define IR_PINR Â  PIND Â  Â  Â /*!< Port D input */  
#define IR_PIN Â  Â PD0 Â  Â  Â  /*!< Pin 0 */  
  
  
static uint8_t Â  Â  RC5lastsample = ; Â /*!< zuletzt gelesenes Sample */  
static uint8_t Â  Â  RC5bittimer Â  = ; Â /*!< zaehlt die Aufrufe von ir_isr() */  
  
static uint16_t Â  Â RC5data_tmp = ; Â  Â /*!< RC5-Bitstream */  
static uint8_t Â  Â  RC5bitcount = ; Â  Â /*!< anzahl gelesener bits */  
  
volatile uint16_t Â RC5data = ; Â  Â  Â  Â /*!< letztes komplett gelesenes RC5-paket */  
volatile uint8_t Â  enableRC5 = ; Â  Â  Â /*!< schaltet die RC5 Abfrage ein/aus */  
  
/*!  
Â * Interrupt Serviceroutine  
Â * wird alle 222.2us aufgerufen  
Â */  
void IsrRC5 (void)  
{  
Â  // sample lesen  
Â  uint8_t sample = 1;  
  
Â  if ((IR_PINR & (1<<IR_PIN)) != )  
Â  {  
Â  Â  sample = ;  
Â  }  
  
Â  // bittimer erhoehen (bleibt bei 255 stehen)  
Â  if (RC5bittimer<255)  
Â  {  
Â  Â  RC5bittimer++;  
Â  }  
  
Â  // flankenerkennung  
Â  if ( RC5lastsample != sample)  
Â  {  
Â  Â  if (RC5bittimer<=IR\_SAMPLES\_PER\_BIT\_MIN)  
Â  Â  {  
Â  Â  Â  // flanke kommt zu frueh: paket verwerfen  
Â  Â  Â  RC5bitcount=;  
Â  Â  }  
Â  Â  else  
Â  Â  {  
Â  Â  Â  // Startbit  
Â  Â  Â  if (RC5bitcount==)  
Â  Â  Â  {  
Â  Â  Â  Â  if ( (sample==1) && (RC5bittimer>IR\_PAUSE\_SAMPLES) )  
Â  Â  Â  Â  {  
Â  Â  Â  Â  Â  // Startbit speichern  
Â  Â  Â  Â  Â  RC5data_tmp = 1;  
Â  Â  Â  Â  Â  RC5bitcount++;  
Â  Â  Â  Â  }  
Â  Â  Â  Â  else  
Â  Â  Â  Â  {  
Â  Â  Â  Â  Â  // error  
Â  Â  Â  Â  Â  RC5data_tmp = ;  
Â  Â  Â  Â  }  
  
Â  Â  Â  Â  // bittimer-reset  
Â  Â  Â  Â  RC5bittimer = ;  
  
Â  Â  Â  Â  // Bits 2..14: nur Flanken innerhalb des Bits beruecksichtigen  
Â  Â  Â  }  
Â  Â  Â  else  
Â  Â  Â  {  
Â  Â  Â  Â  if (RC5bittimer >= IR\_SAMPLES\_PER\_BIT\_EARLY)  
Â  Â  Â  Â  {  
Â  Â  Â  Â  Â  if (RC5bittimer<=IR\_SAMPLES\_PER\_BIT\_LATE)  
Â  Â  Â  Â  Â  {  
Â  Â  Â  Â  Â  Â  // Bit speichern  
Â  Â  Â  Â  Â  Â  RC5data_tmp = (RC5data_tmp<<1) | sample;  
Â  Â  Â  Â  Â  Â  RC5bitcount++;  
Â  Â  Â  Â  Â  }  
Â  Â  Â  Â  Â  else  
Â  Â  Â  Â  Â  {  
Â  Â  Â  Â  Â  Â  // zu spaet: paket verwerfen  
Â  Â  Â  Â  Â  Â  RC5bitcount = ;  
Â  Â  Â  Â  Â  }  
  
Â  Â  Â  Â  Â  // bittimer-reset  
Â  Â  Â  Â  Â  RC5bittimer = ;  
Â  Â  Â  Â  }  
Â  Â  Â  }  
Â  Â  }  
  
Â  }  
Â  else  
Â  {  
Â  Â  // keine flanke innerhalb bitzeit?  
Â  Â  if (RC5bittimer > IR\_SAMPLES\_PER\_BIT\_LATE)  
Â  Â  {  
Â  Â  Â  // 14 bits gelesen?  
Â  Â  Â  if (RC5bitcount==14)  
Â  Â  Â  {  
Â  Â  Â  Â  RC5data = RC5data_tmp;  
Â  Â  Â  }  
Â  Â  Â  // paket verwerfen  
Â  Â  Â  RC5bitcount = ;  
Â  Â  }  
Â  }  
  
Â  // sample im samplepuffer ablegen  
Â  RC5lastsample = sample;  
  
  
}  
  
  
/*!  
Â * IR-Daten lesen  
Â * @return wert von ir\_data, loescht anschliessend ir\_data  
Â */  
uint16_t ReadRC5 (void)  
{  
Â  uint16_t retvalue = RC5data;  
Â  RC5data = ;  
Â  return retvalue;  
}  
  
/*!  
Â * Init IR-System  
Â */  
void InitRC5 (void)  
{  
Â  IR_DDR Â &= ~IR_PIN; Â  // Pin auf Input  
Â  IR_PORT |= IR_PIN; Â  Â // Pullup an  
Â  enableRC5 = 1;  
}

[[$[Get Code]]][8]



## Programmcode test.c

Das Testprogramm sendet die empfangenen RC5 Codes über den IR Transceiver an den PC. Das ist praktisch zum Feststellen, welche Taste welchen Code liefert. Entsprechend kann man die gefundenen Codes dann im Test Programm ändern oder neue dazufügen. Bisher werden nur 5 Befehle benutzt, die den ASURO vorwärts, rückwärts, links rechts und stoppen lassen. 



#include "asuro.h"  
#include "rc5.h"  
#include <stdlib.h>  
  
#define DIARWD Â  0x1008  
#define DIAFWD Â  0x1002  
#define DIALEFT Â 0x1004  
#define DIARIGHT 0x1006  
#define DIASTOP Â 0x1029  
  
#define TUNERRWD Â  0x1021  
#define TUNERFWD Â  0x1020  
#define TUNERLEFT Â 0x1011  
#define TUNERRIGHT 0x1010  
#define TUNERSTOP Â 0x1025  
  
#define OFFSETÂ  0x3F  
#define STEPÂ  Â  5  
  
int speedLeft,speedRight;  
  
void IRFwd(void)  
{  
Â  speedRight += STEP;  
Â  speedLeft Â += STEP;  
Â  if (speedLeft <  && speedLeft >= -OFFSET) speedLeft = 1;  
Â  if (speedRight <  && speedRight >= -OFFSET) speedRight = 1;  
Â  FrontLED(ON);  
Â  BackLED(OFF,OFF);  
}  
  
void IRRwd(void)  
{  
Â  speedRight -= STEP;  
Â  speedLeft Â -= STEP;  
Â  if (speedRight >  && speedRight <= OFFSET) Â speedRight = -1;  
Â  if (speedLeft >  && speedLeft <= OFFSET) Â speedLeft = -1;  
Â  FrontLED(OFF);  
Â  BackLED(ON,ON);  
}  
  
void IRLeft (void)  
{  
Â  speedLeft Â -= STEP;  
Â  if (speedLeft >  && speedLeft <= OFFSET) speedLeft = -1;  
Â  speedRight += STEP;  
Â  if (speedRight <  && speedRight >= -OFFSET) speedRight = 1;  
Â  FrontLED(OFF);  
Â  BackLED(ON,OFF);  
}  
  
void IRRight (void)  
{  
Â  speedLeft Â += STEP;  
Â  if (speedLeft <  && speedLeft >= -OFFSET) speedLeft = 1;  
Â  speedRight -= STEP;  
Â  if (speedRight >  && speedRight <= OFFSET) speedRight = -1;  
Â  FrontLED(OFF);  
Â  BackLED(OFF,ON);  
}  
  
  
void IRStop(void)  
{  
Â  speedRight = speedLeft = ;  
Â  FrontLED(OFF);  
Â  BackLED(OFF,OFF);  
}  
  
int main(void)  
{  
  
Â  static unsigned int cmd;  
Â  unsigned char leftDir = FWD, rightDir = FWD;  
Â  char text[7];  
  
Â  Init();  
Â  InitRC5();  
  
Â  SerPrint("RC5 Test\r\n");  
Â  while (1)  
Â  {  
Â  Â  cmd = ReadRC5();  
Â  Â  if (cmd)  
Â  Â  {  
Â  Â  Â  cmd &= RC5_MASK;  
Â  Â  Â  itoa(cmd, text, 16);  
Â  Â  Â  SerPrint(text);  
Â  Â  Â  SerPrint("\r\n");  
  
Â  Â  Â  switch (cmd)  
Â  Â  Â  {  
Â  Â  Â  Â  case TUNERRWD :  
Â  Â  Â  Â  case DIARWD :  
Â  Â  Â  Â  Â SerPrint("rwd\r\n");  
Â  Â  Â  Â  Â IRRwd();  
Â  Â  Â  Â  break;  
Â  Â  Â  Â  case TUNERFWD :  
Â  Â  Â  Â  case DIAFWD :  
Â  Â  Â  Â  Â  SerPrint("fwd\r\n");  
Â  Â  Â  Â  Â  IRFwd();  
Â  Â  Â  Â  break;  
Â  Â  Â  Â  case TUNERLEFT :  
Â  Â  Â  Â  case DIALEFT:  
Â  Â  Â  Â  Â  SerPrint("lft\r\n");  
Â  Â  Â  Â  Â  IRLeft();  
Â  Â  Â  Â  break;  
Â  Â  Â  Â  case TUNERRIGHT :  
Â  Â  Â  Â  case DIARIGHT:  
Â  Â  Â  Â  Â  SerPrint("rgt\r\n");  
Â  Â  Â  Â  Â  IRRight();  
Â  Â  Â  Â  break;  
Â  Â  Â  Â  case TUNERSTOP :  
Â  Â  Â  Â  case DIASTOP :  
Â  Â  Â  Â  Â  SerPrint("stp\r\n");  
Â  Â  Â  Â  Â  IRStop();  
Â  Â  Â  Â  break;  
Â  Â  Â  }  
Â  Â  }  
Â  Â  if (speedLeft >  && speedLeft < Â OFFSET) speedLeft += OFFSET;  
Â  Â  if (speedLeft <  && speedLeft > -OFFSET) speedLeft -= OFFSET;  
Â  Â  if (speedRight >  && speedRight < Â OFFSET) speedRight += OFFSET;  
Â  Â  if (speedRight <  && speedRight > -OFFSET) speedRight -= OFFSET;  
  
Â  Â  leftDir = rightDir = FWD;  
Â  Â  if (speedLeft < ) Â leftDir = RWD;  
Â  Â  if (speedRight < ) rightDir = RWD;  
  
Â  Â  if (speedLeft > Â  255) speedLeft Â = Â 255;  
Â  Â  if (speedLeft < Â -255) speedLeft Â = -255;  
Â  Â  if (speedRight > Â 255) speedRight = Â 255;  
Â  Â  if (speedRight < -255) speedRight = -255;  
  
Â  Â  MotorDir(leftDir,rightDir);  
Â  Â  MotorSpeed(abs(speedLeft),abs(speedRight));  
Â  Â  Msleep(100);  
Â  }  
Â  return ;  
}

[[$[Get Code]]][9]



## Anpassungen asuro.c

Die RC5 Empfangsroutine wird vom Timer Interrupt aus alle 222,2µs angesprungen. Dazu reicht es aus, nur auf jeden 8. Timer Interrupt zu reagieren. Damit die RC5 Service Funktion nicht unnötig in allen Projekten eingebunden wird, wird der Aufruf bedingt eingebunden. Dazu dient die #ifdef Abfrage. Der Programmcode zwischen #ifdef und dem #endif wird nur mitübersetzt, wenn RC5_AVAILABLE definiert ist. Definiert wird RC5_AVAILABLE allerdings nicht im Sourcecode, sondern im Makefile. Dadurch gibt es keine Fehlermeldungen wegen undeklarierter Variablen und Funktionen. Da RC5_AVAILABLE in anderen Projekten nicht definiert ist, wird auch die RC5 Service Funktion nicht eingebunden. 



SIGNAL (SIG_OVERFLOW2)  
{  
Â  TCNT2 += 0x25;  
Â  count36kHz ++;  
Â  if (!count36kHz)  
Â  Â  timebase ++;  
#ifdef RC5_AVAILABLE  
Â  if (enableRC5 && !(count36kHz % 8))   
Â  Â  IsrRC5(); // wird alle 222.2us aufgerufen  
#endif Â   
}

[[$[Get Code]]][10]



## Anpassungen Makefile

Das Makefile für das Testprogrammm bedarf einiger Anpassungen. SO muß das zusätzliche Sourcefile rc5.c eingebunden werden und RC5_AVAILABLE definiert werden. Mit der Option -D bei den CFLAGS (Compiler-Optionen) kann man ein Define im Makefile definieren. Dies bewirkt dasselbe wie ein #define RC5_AVAILABLE in einem C-Sourcefile. 



  
**GeSHi Error:** GeSHi could not find the language makefile (using path /hp/aa/ad/zd/www/asurowiki/pmwiki/cookbook/geshi/geshi/) (code 2)  


[[$[Get Code]]][11]



## Weblinks

*   [c't-Bot Wiki][12] - Fernbedienübersicht 
*   [www.spettel.de][13] - AVRGCC Code für RC5 IR-Fernbedinungen 
*   [Roboternetz Wissen][14] - RC5-Decoder für ATMega 
*   [www.sprut.de][15] - Elektronik: IR-Fernbedienung, RC-5 
*   [www.heise.de/ct][16] - c't 23/2005, S. 222: Zeitschaltuhr mit Netzwerkanschluss

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/hauppauge_mvp.jpg
 [2]: http://www.asurowiki.de/pmwiki/uploads/Main/univers29.jpg
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Downloads
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Bibliothek
 [5]: http://www.asurowiki.de/pmwiki/pub/html/rc5_8h.html
 [6]: http://www.asurowiki.de/pmwiki/pub/html/_r_c5_test_2test_8c.html
 [7]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RC5DemoC?action=sourceblock&num=1
 [8]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RC5DemoC?action=sourceblock&num=2
 [9]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RC5DemoC?action=sourceblock&num=3
 [10]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RC5DemoC?action=sourceblock&num=4
 [11]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/RC5DemoC?action=sourceblock&num=5
 [12]: http://wiki.ctbot.de/index.php/Fernbedienungen_%C3%9Cbersicht
 [13]: http://www.spettel.de/ralf/index_reload.html?http://www.spettel.de/ralf/projekte/avr_rc5/index.shtml
 [14]: http://www.roboternetz.de/wissen/index.php/Codesammlung_avr-gcc
 [15]: http://www.sprut.de/electronic/ir/rc5.htm
 [16]: http://www.heise.de/ct/05/23/222/