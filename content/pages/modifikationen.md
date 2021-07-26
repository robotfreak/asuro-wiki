# Modifikationen

![][1]  
*ASURO Modifikationen*<vspace>

## Siehe auch<vspace>

*   [Asuro Eval Board][2] 
*   [Batteriefach Modifikation][3] 
*   [Liniensensor Modifikation][4] 
*   [Motor Modifikation][5] 
*   [Odometrie Modifikation][6] 
*   [IR Transceiver Modifikation][7] 
*   [Tischtennisball Ersatz][8] 
*   [Zusammenbau][9] - Modifikationen, die man bereits beim Zusammenbau des ASUROs durchführen kann <vspace>

## Weblinks<vspace>

*   [Roboternetz Thread][10] - Motorsatz Austausch Modul 
*   [Roboternetz Thread][11] - Balancierender ASURO 
*   [www.ulrichc.de][12] CU-Test-Bot, Asuro mit Kettenantrieb vom CCRP5 
*   [Roboternetz Thread][13] - asuro mit Kettenantrieb und 3.Getriebestufe 
*   [Roboternetz Thread][14] - case modding: Ein neues Kleidchen für meinen asuro 
*   [Roboternetz Thread][15] - Umbau der IR-Schnittstelle zur Hinderniserkennung 
*   [Roboternetz Thread][16] - Minimallösung: IR-Abstandsmessung 

![][17]

*   schon ab *Asuro Library v261* in **examples/IRCollisionTest** unterstützt 
*   ab *Asuro Library v270rc3* sogar mit wechselseitiger Ausgabe über *SerPrint()*, siehe folgenden Ausschnitt aus dem Quellcode aus *v270rc3*: <vspace>

...  
static unsigned char ocr2 = 0x91;  
  
void InitIRDetect(void)  
{Â    
Â  UCSRB = ;  
Â  DDRD |= (1 << DDD1);Â  // Port D1 als Ausgang  
Â  PORTD &= ~(1 << PD1);Â // PD1 auf LOW  
Â  OCR2 = ocr2;  
}  
  
void InitUart(void)  
{  
Â  OCR2Â  = 0x91;Â  Â  Â  Â  Â // duty cycle fuer 36kHz  
}  
...

 [1]: http://www.asurowiki.de/pmwiki/uploads/Main/collage_mod.jpg ""
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroEvalBoard
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/BatteriefachModifikation
 [4]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/LiniensensorModifikation
 [5]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/MotorModifikation
 [6]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/OdometrieModifikation
 [7]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/IRTransceiverModifikation
 [8]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/TTBallErsatz
 [9]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Zusammenbau
 [10]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11656
 [11]: http://www.roboternetz.de/phpBB2/viewtopic.php?t=15307
 [12]: http://www.ulrichc.de/project/cu-test-bot/index_de.html
 [13]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=31572
 [14]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=27486
 [15]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=11114
 [16]: http://www.roboternetz.de/phpBB2/zeigebeitrag.php?t=27013
 [17]: http://www.asurowiki.de/pmwiki/uploads/Main/asuroir_small.jpg ""

