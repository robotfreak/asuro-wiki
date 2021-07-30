# Java

ASURO Programmierung in Java. 

Auch das ist möglich. NanoVM ist eine virtuelle Java Machine für den ATmega8/ATmega168. Leider funktioniert dies nicht mit dem Original Asuro Controller. Da der komplette Flash (8kB) für die NanoVM benötigt wird, sollte man sich einen neuen Controller besorgen, am besten gleiche einen ATmega168 (mit 16kB Flash). Zudem muß entweder die ISP Schnittstelle verkabelt sein, wie es z.B. beim [Asuro Eval Board][1] oder bei der [Asuro Erweiterung][2] gemacht ist, oder der Controller muß einmalig in einem anderem Board mit ISP Schnittstelle (z.B. STK500) mit der NanoVM programmiert werden. Auf der [NanoVM Homepage][3] wird auch ein Adaptersockel mit ISP für den Asuro vorgestellt. Auch kann man dort vorprogammierte Chips geordert werden. Das eigentliche Anwenderprogramm kann dann über die IR Schnittstelle programmiert (geladen) werden. 



## Weiterführende Links

*   [NanoVM][3] - Java for the Asuro 
*   [Sourceforge][4] - NanoVM 
*   [mikorocontroller.net][5] - NanoVM Artikel und Beispielcode. 
*   [www.ericengler.com][6] - NanoVM - Embedded Virtual Machine for the Asuro (in eglisch)

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroEvalBoard
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/AsuroErweiterung
 [3]: http://www.harbaum.org/till/nanovm/index.html
 [4]: http://sourceforge.net/projects/nanovm/
 [5]: http://www.mikrocontroller.net/articles/NanoVM
 [6]: http://www.ericengler.com/NanoVM.aspx