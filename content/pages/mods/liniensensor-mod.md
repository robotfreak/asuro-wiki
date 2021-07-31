---
Title: Liniensensor Modifikation
Template: section
---

# Liniensensor Modifikation

## Modifikation des Liniensensors

Nach der Original Bedienungsanleitung werden die Fototransistoren (T9 und T10) und die rote Front LED (D11) an der Unterseite angebracht und von oben her eingelötet. 

Will man später einmal den [Ultraschall Entfernungsmesser](extensions/ultraschhallenfernungsmesser), oder eine andere [Erweiterung](extensions/index) mit der ASURO Erweiterungsplatine benutzen, muß man die Fototransistoren und die Front LED wieder auslöten. Es ist also besser, wenn man diese Bauteile gleich steckbar macht. 

Hierzu werden anstelle der Bauteile WireWrap Buchsenleiste (Conrad Artikel Nr. 739111-62) eingelötet. Diese kann man recht einfach mit einem Seitenschneider in 3er und 2er Leisten aufteilen. man steck die Leisten von unten ein und lötet sie von oben fest. Die Liniensensor Bauteile lassen sich nun bequem von unten stecken oder abziehen. Auch für die Stromversorgung der Erweiterungsplatine verwendet man so eine 2polige WireWrap Buchsenleiste. 

Um die Liniensensoren besser gegen Fremdeinstrahlung abzuschirmen, kann man die beiden Fototransistoren zusätzlich noch mit einem Stück Schrumpfschlauch (4,8mm Durchmesser) abschirmen. 



### Vorteile:

*   Zusätzlicher Vorteil dieser Lösung: es läßt sich damit auch eine Erweiterung unter der ASURO Platine anbringen. So könnte man z.B. zwei I2C Erweiterungen gleichzeitig verwenden. 
*   Statt der roten Front LED könnte man auch eine Infrarot LED verwenden. Versuche mit einer SFH415 IR-LED (der gleiche Typ der für die Infratschnittstelle verwendet wird) und einer LD 274-3 (nahezu baugleich, aber höhere Leistung) verliefen erfolgreich. Der gemessene Unterschied zwischen Hell und Dunkel erhöht sich erheblich. 



### Wichtig:

Falls man diese Modifiktion durchführt muß man folgendes beachten. Da jetzt im ASURO die Steckerleisten sitzen und keine Buchsenleisten muß man die Erweiterungsplatinen mit Buchsenleisten zu versehen, nicht mit Steckerleisten, wie es in der Beschreibung vorgeschlagen wird. 



![](%assets_url%/mod_line.jpg) 
*Wire Wrap Buchsenleiste*



![](%assets_url%/mod_line3.jpg)
*Asuroplatine von unten mit Steckverbinder*



![](%assets_url%/mod_line1.jpg)
*Wire Wrap Buchsenleiste eingelötet*



![](%assets_url%/mod_line2.jpg)
*Liniensensor Bauteile aufgesteckt, mit Schrumpfschlauch über den Fototransistoren*



## Bezugsquellen

*   [Conrad][7] Buchsenleiste 36 polig Wire Wrap

 [1]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/UltraschallEntfernungsmesser
 [2]: http://www.asurowiki.de/pmwiki/pmwiki.php/Main/Erweiterungen
 [3]: http://www.asurowiki.de/pmwiki/uploads/Main/mod_line.jpg
 [4]: http://www.asurowiki.de/pmwiki/uploads/Main/mod_line3.jpg
 [5]: http://www.asurowiki.de/pmwiki/uploads/Main/mod_line1.jpg
 [6]: http://www.asurowiki.de/pmwiki/uploads/Main/mod_line2.jpg
 [7]: http://www.conrad.de/script/buchsenleiste_36_polig-37.sap