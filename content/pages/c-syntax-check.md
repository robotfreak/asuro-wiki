# CSyntaxCheck

Zum (automatisierten) Auffinden von Syntax-Fehlern in C-Programmen á la *lint* gibt es viele Tools. 

*splint* ist frei verfügar für viele Plattformen, inklusive *Windows*, *Linux* und *Cygwin* (die *Windows*- und *Cygwin*-Versionen liefern identischen Output); Informationen und Download siehe unter *Weiterführende Links*. 

Die beiden typischen Zuweisungs-/Test-Fehler im C-Programm **aha.c** 

Â   
int main(void)  
{  
Â  int i=3;  
  
Â  if (i=5)  
Â  Â  i==4;  
  
Â  return ;  
}

[[$[Get Code]]][1]

werden mittels **splint aha.c** sofort aufgedeckt: 

    C:\ASURO_src>splint aha.c
    Splint 3.1.1 --- 02 May 2003
    
    aha.c: (in function main)
    aha.c:5:7: Test expression for if is assignment expression: i = 5
      The condition test is an assignment expression. Probably, you mean to use ==
      instead of =. If an assignment is intended, add an extra parentheses nesting
      (e.g., if ((a = b)) ...) to suppress this message. (Use -predassign to
      inhibit warning)
    aha.c:5:7: Test expression for if not boolean, type int: i = 5
      Test expression type is not boolean or int. (Use -predboolint to inhibit
      warning)
    aha.c:6:5: Statement has no effect: i == 4
      Statement has no visible effect --- no values are modified. (Use -noeffect to
      inhibit warning)
    
    Finished checking --- 3 code warnings
    



## Verwendung von splint für die Asuro-Programmierung

Um Probleme mit dem AVR-Compiler für den Asuro und irgendwelchen weiteren installierten Compilern zu vermeiden, geschieht die Syntax-Überprüfung in zwei Schritten: 

1.  Erzeugen einer (AVR-)C-präprozessierten Datei. 
2.  Aufruf von **splint** für diese Datei. 



## Asuro-Beispiel

Die folgende Funktion stammt aus einem Thread im RoboterNetz Asuro-Forum: 

Â   
void tastenCheck(void)  
{  
Â  Â static unsigned char pressed = ;  
Â  Â unsigned int t1,t2;  
Â  Â PrintInt(switched);  
Â  Â SerPrint("switched 1 \n\r");  
Â  Â  if(switched == TRUE && pressed == ) { // Tastendruck  
Â  Â  Â  pressed = 1;  
Â  Â  Â  Â  t1 = PollSwitch();  
Â  Â  Â  Â  t2 = PollSwitch();  
Â  Â  Â  taste = (t1+t2+1)/2;  
Â  Â  Â  PrintInt(taste);  
  
  
Â  Â  Â  PrintInt(switched);  
Â  Â  Â  SerPrint("switched 2 \n\r");  
Â  Â  }  
  
Â  Â if(pressed == 1 && switched == TRUE) {  
Â  Â  Â  StopSwitch();  
Â  Â  Â  switched == ;  
Â  Â  Â  PrintInt(switched);  
Â  Â  Â  SerPrint("switched 3 \n\r");  
Â  Â }  
  
Â  Â if(switched == ) {  
Â  Â  Â  pressed = ;  
Â  Â  Â  StartSwitch();  
Â  Â  Â  PrintInt(switched);  
Â  Â  Â  SerPrint("switched 4 \n\r");  
Â  Â }  
  
}

[[$[Get Code]]][2]

Damit **splint** damit Umgehen kann, muß noch die globale Variable *taste* definiert und die Asuro-Bibliothek eingebunden werden. Dies liefert das folgende C-Programm **sample.c**: 

Â   
#include "asuro.h"  
  
unsigned int taste;  
  
void tastenCheck(void)  
{  
Â  Â static unsigned char pressed = ;  
...  
  
...  
}

[[$[Get Code]]][3]

Wie oben beschrieben wird zuerst der AVR-C-Preprocessor aktiviert und die Datei **sample.E.c** erzeugt: 

    C:\ASURO_src>avr-gcc -mmcu=atmega8 -E sample.c >sample.E.c
    

Damit **splint** nicht durch die **#line**-Anweisungen in **sample.E.c** gestört wird, wird die Option *-preproc* verwendet, und zur Vermeidung von Problemen mit anderen installierten Compilern wird noch die Option *-nolib* verwendet. Dies liefert erst einmal eine ganze Menge an Meldungen: 

    C:\ASURO_src>splint -preproc -nolib sample.E.c
    Splint 3.1.1 --- 02 May 2003
    
    C:/WinAVR/avr/include/stdlib.h: (in function atol)
    C:/WinAVR/avr/include/stdlib.h:253:31: Null storage passed as non-null param:
                                              strtol (..., (char **)0, ...)
      A possibly null pointer is passed as a parameter corresponding to a formal
      parameter with no /*@null@*/ annotation.  If NULL may be used for this
      parameter, add a /*@null@*/ annotation to the function parameter declaration.
      (Use -nullpass to inhibit warning)
    sample.c: (in function tastenCheck)
    sample.c:7:35: Variable pressed initialized to type int, expects unsigned char:
                      0
      Types are incompatible. (Use -type to inhibit warning)
    sample.c:10:13: Function SerPrint expects arg 1 to be unsigned char * gets char
                       *: "switched 1 \n\r"
      To ignore signs in type comparisons use +ignoresigns
    sample.c:11:25: Operands of == have incompatible types (unsigned char, int):
                       pressed == 0
    sample.c:12:7: Assignment of int to unsigned char: pressed = 1
      To make char and int types equivalent, use +charint.
    sample.c:13:9: Assignment of unsigned char to unsigned int: t1 = PollSwitch()
    sample.c:14:9: Assignment of unsigned char to unsigned int: t2 = PollSwitch()
    sample.c:16:16: Function PrintInt expects arg 1 to be int gets unsigned int:
                       taste
    sample.c:20:16: Function SerPrint expects arg 1 to be unsigned char * gets char
                       *: "switched 2 \n\r"
    sample.c:23:7: Operands of == have incompatible types (unsigned char, int):
                      pressed == 1
    sample.c:25:7: Statement has no effect: switched == 0
      Statement has no visible effect --- no values are modified. (Use -noeffect to
      inhibit warning)
    sample.c:27:16: Function SerPrint expects arg 1 to be unsigned char * gets char
                       *: "switched 3 \n\r"
    sample.c:31:7: Assignment of int to unsigned char: pressed = 0
    sample.c:34:16: Function SerPrint expects arg 1 to be unsigned char * gets char
                       *: "switched 4 \n\r"
    C:/WinAVR/avr/include/stdlib.h:94:24:
        Function exported but not used outside stdlib: abort
      A declaration is exported, but not used outside this module. Declaration can
      use static qualifier. (Use -exportlocal to inhibit warning)
       C:/WinAVR/avr/include/stdlib.h:103:1: Definition of abort
    C:/WinAVR/avr/include/stdlib.h:249:24:
        Function exported but not used outside stdlib: atol
       C:/WinAVR/avr/include/stdlib.h:254:1: Definition of atol
    sample.c:3:14: Variable exported but not used outside sample: taste
    
    Finished checking --- 17 code warnings
    

Um nun ein bißchen den Überblick zu gewinnen (und erstmal die Anzahl der Warnungen zu drücken) kann man folgende Optionen dazuschalten (diese Optionen kann man dem Manual, **splint -help** oder aber dem obigen Output entnehmen): 



*   *+charint* (macht *char-* and *int-Typen* äquivalent) 
*   *+ignoresigns* (ignoriert *signed/unsigned*-Probleme in Vergleichen) 
*   *-exportlocal* (ignoriert Export-Warnungen) 

Dies reduziert die Warnungen auf 2, eine Ungenauigkeit in der Datei **stdlib.h** des AVR-Compilers und den echten Fehler: 

    C:\ASURO_src>splint -preproc -nolib +charint +ignoresigns -exportlocal sample.E.
    c
    Splint 3.1.1 --- 02 May 2003
    
    C:/WinAVR/avr/include/stdlib.h: (in function atol)
    C:/WinAVR/avr/include/stdlib.h:253:31: Null storage passed as non-null param:
                                              strtol (..., (char **)0, ...)
      A possibly null pointer is passed as a parameter corresponding to a formal
      parameter with no /*@null@*/ annotation.  If NULL may be used for this
      parameter, add a /*@null@*/ annotation to the function parameter declaration.
      (Use -nullpass to inhibit warning)
    sample.c: (in function tastenCheck)
    sample.c:25:7: Statement has no effect: switched == 0
      Statement has no visible effect --- no values are modified. (Use -noeffect to
      inhibit warning)
    
    Finished checking --- 2 code warnings
    



## Weiterführende Links

<http://www.splint.org/> - *Secure Programming Lint* Homepage 

<http://www.roboternetz.de/phpBB2/viewtopic.php?t=29987> - RoboterNetz-Thread zum Thema

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/CSyntaxCheck?action=sourceblock&num=1
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/CSyntaxCheck?action=sourceblock&num=2
 [3]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/CSyntaxCheck?action=sourceblock&num=3