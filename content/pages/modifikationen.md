---
Title: Modifikationen
Template: section
Toc: section
---

# Modifikationen

![ASURO Modifikationen](%assets_url%/collage_mod.jpg)  
*ASURO Modifikationen*

## Siehe auch

*   [Asuro Eval Board](asuro-evalboard)
*   [Batteriefach Modifikation](batteriefachmod) 
*   [Liniensensor Modifikation](liniensensormod) 
*   [Motor Modifikation](motormod) 
*   [Odometrie Modifikation](odometriemod) 
*   [IR Transceiver Modifikation](irtransceivermod) 
*   [Tischtennisball Ersatz](ttersatz) 
*   [Zusammenbau](zusammenbau) - Modifikationen, die man bereits beim Zusammenbau des ASUROs durchführen kann 

## Weblinks

*   [Roboternetz Thread](http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11656) - Motorsatz Austausch Modul 
*   [Roboternetz Thread](http://www.roboternetz.de/phpBB2/viewtopic.php?t=15307) - Balancierender ASURO 
*   [www.ulrichc.de](http://www.ulrichc.de/project/cu-test-bot/index_de.html) CU-Test-Bot, Asuro mit Kettenantrieb vom CCRP5 
*   [Roboternetz Thread](http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=31572) - asuro mit Kettenantrieb und 3.Getriebestufe 
*   [Roboternetz Thread](http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=27486) - case modding: Ein neues Kleidchen für meinen asuro 
*   [Roboternetz Thread]( http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11114) - Umbau der IR-Schnittstelle zur Hinderniserkennung 
*   [Roboternetz Thread](http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=27013) - Minimallösung: IR-Abstandsmessung 

![Asuro IR](%assets_url%/asuroir_small.jpg)

*   schon ab *Asuro Library v261* in **examples/IRCollisionTest** unterstützt 
*   ab *Asuro Library v270rc3* sogar mit wechselseitiger Ausgabe über *SerPrint()*, siehe folgenden Ausschnitt aus dem Quellcode aus *v270rc3*: 

```c
static unsigned char ocr2 = 0x91;  
  
void InitIRDetect(void)  
{    
  UCSRB = ;  
  DDRD |= (1 << DDD1);  // Port D1 als Ausgang  
  PORTD &= ~(1 << PD1); // PD1 auf LOW  
  OCR2 = ocr2;  
}  
  
void InitUart(void)  
{  
  OCR2  = 0x91;  // duty cycle fuer 36kHz  
}  
```

