# MakefileHowto

## Einleitung

Ein Makefile dient dazu, dem Programm **make** mitzuteilen, was es machen sollen (ein bestimmtes `'target'` erzeugen) und wie es das machen soll (die zu dem Target ensprechenden `'rules'` befolgen). Für den ASURO bedeutet dies: 



*   `'target'` ist ein Binär File (.hex File), welches man mit dem ASURO Flasher Tool auf den ASURO laden kann. 
*   `'target'` sind die Regeln um dieses `'target'` zu erzeugen. Das Erzeugen des Binär Files passiert in mehreren Schritten: 
    *   der Compiler (avr-gcc) `compiliert` den Quellcode (.c) in Objekt Files (.o). 
    *   der Linker (avr-ld) `linked` die Objekt Files mit der Laufzeitumgebung und zusätzlichen Libraries zu einem .elf File. 
    *   Schließlich wird aus dem .elf File mit dem Tool avr-ojcopy ein Binär File erzeugen. Dieses Binär File enthält dann den Prozessor spezifischen Maschinencode und die Adressen, in die der Maschinencode im FLASH Speicher abgelegt wird. Der Asuro Flasher benötigt dazu als Binär File Format das sogenannte Intel Hex Format. 



## Makefile Syntax

Das Makefile ist ein normales Textfile, das man sich mit jedem Texteditor anschauen und editieren kann. Die Syntax von Makefiles ist recht komplex, deshalb sollte man nur etwas ändern, wenn man weis, was man tut. 



### Kommentare

Alle Zeilen, die mit dem # Zeichen beginnen sind Kommentar Zeilen und werden vom Make Programm nicht ausgewertet. 



### Variablen

Zeilen mit dem Gleichheitszeichen = sind Zuweisugen zu Variablen. Ähnlich wie in C kann man Variablen verwenden und diesen Werte zuweisen. Variablen werden als Strings verwenden, d.h. man kann einer Variablen nur Text zuweisen. Damit das Make Programm die Variablen als solche erkennt, wird die Syntax `$(VARIABLENNAME)` verwendet. Wie z.B. die Variable `TARGET`. 



    TARGET = test
    

Das ist eine Zuweisung. Der Text test wird der Variablen `TARGET` zugewiesen. 



    SRC = $(TARGET).c
    

Hier wird auch wieder eine Variable (SRC) ein Text zugewiesen. In diesem Fall der Inhalt der Variable `TARGET` und dahinter `.c`. Die Variable SRC hat danach den Wert `test.c` 



### Targets und Regeln

So sieht z.B. die Regel zum erzeugen der Objekt Files aus. Das Make Programm erzeugt daraus rekursiv den Aufruf des AVR-GCC Compilers für alle C- Source Files. 



    # Compile: create object files from C source files.
    %.o : %.c
    	$(CC) -c $(ALL_CFLAGS) $< -o $@
    

Die umgewandelte Befehlszeile sieht dann für das Source File test.c so aus: 

    avr-gcc -c -mmcu=atmega8 -I. -g -Os -I../../lib/inc -funsigned-char -funsigned-b
    itfields -fpack-struct -fshort-enums -Wall -Wstrict-prototypes -Wa,-ahlms=test.l
    st test.c -o test.o
    



## Beispiel Makefile

So sieht der Teil des ASURO Makefile aus, den man bei Bedarf anpassen kann: 



    # MCU name
    MCU = atmega8
    
    # Output format. (can be srec, ihex, binary)
    FORMAT = ihex
    
    # Target file name (without extension).
    TARGET = test
    
    # Optimization level, can be [0, 1, 2, 3, s]. 0 turns off optimization.
    # (Note: 3 is not always the best optimization level. See avr-libc FAQ.)
    OPT = s
    
    
    # List C source files here. (C dependencies are automatically generated.)
    SRC = $(TARGET).c
    
    # If there is more than one source file, append them above, or adjust and
    # uncomment the following:
    SRC += asuro.c
    
    # You can also wrap lines by appending a backslash to the end of the line:
    #SRC += baz.c \
    #xyzzy.c
    
    
    
    # List Assembler source files here.
    # Make them always end in a capital .S.  Files ending in a lowercase .s
    # will not be considered source files but generated files (assembler
    # output from the compiler), and will be deleted upon "make clean"!
    # Even though the DOS/Win* filesystem matches both .s and .S the same,
    # it will preserve the spelling of the filenames, and gcc itself does
    # care about how the name is spelled on its command-line.
    ASRC = 
    
    # Optional compiler flags.
    #  -g:        generate debugging information (for GDB, or for COFF conversion)
    #  -O*:       optimization level
    #  -f...:     tuning, see gcc manual and avr-libc documentation
    #  -Wall...:  warning level
    #  -Wa,...:   tell GCC to pass this to the assembler.
    #    -ahlms:  create assembler listing
    CFLAGS = -g -O$(OPT) -I../../lib/inc\
    	-funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums \
    	-Wall -Wstrict-prototypes \
    	-Wa,-ahlms=$(<:.c=.lst)
    
    VPATH=../../lib
    # Optional assembler flags.
    #  -Wa,...:   tell GCC to pass this to the assembler.
    #  -ahlms:    create listing
    #  -gstabs:   have the assembler create line number information; note that
    #             for use in COFF files, additional information about filenames
    #             and function names needs to be present in the assembler source
    #             files -- see avr-libc docs [FIXME: not yet described there]
    ASFLAGS = -Wa,-ahlms=$(<:.S=.lst),-gstabs 
    
    
    
    # Optional linker flags.
    #  -Wl,...:   tell GCC to pass this to linker.
    #  -Map:      create map file
    #  --cref:    add cross reference to  map file
    LDFLAGS = -Wl,-Map=$(TARGET).map,--cref
    LDFLAGS += -L../../lib
    
    
    # Additional libraries
    #
    # Minimalistic printf version
    #LDFLAGS += -Wl,-u,vfprintf -lprintf_min
    #
    # Floating point printf version (requires -lm below)
    #LDFLAGS +=  -Wl,-u,vfprintf -lprintf_flt
    #
    # -lm = math library
    LDFLAGS += -lm
    LDFLAGS += -lasuro
    
    



### Warum muß mein Quellcode immer test.c heißen?

Folgende Zeile legt den Namen des erzeugten targets fest. 



    # Target file name (without extension).
    TARGET = test
    

Dieser Name wird zudem verwendet um das File test.c in die Liste der Quellfiles aufzunehmen. 



    # List C source files here. (C dependencies are automatically generated.)
    SRC = $(TARGET).c
    



### Zusätzlichen Quellcode einbinden

Ganz einfach man fügt z.B. folgende Zeile ein um die Datei 'lcd.c' mit zu übersetzen. 



    # If there is more than one source file, append them above, or adjust and
    # uncomment the following:
    SRC += asuro.c
    
    # You can also wrap lines by appending a backslash to the end of the line:
    #SRC += baz.c \
    #xyzzy.c
    SRC += lcd.c
    



## Probleme mit Makefiles

### folgende Fehlermeldungen erscheinen nach dem Aufruf von make

    MAKE Version 5.2  Copyright (c) 1987, 2000 Borland
     Error makefile 223: Colon expected
     Error makefile 248: Too many rules for target '%.o'
     Error makefile 284: Command syntax error
     *** 3 errors during make ***
    

In diesem Fall stimmen die Pfadangaben der Windows Umgebung nicht. Anstatt des GNU-Make wird das Make Programm von Borland aufgerufen. Überprüfen Sie in diesem Fall die Pfadangeben von Windows. Der Pfad zum WinAVR Compiler `C:\<span class="wikiword">WinAVR</span>\bin` sollte am Anfang stehen. 



### folgende Fehlermeldung erscheinen nach dem Aufruf von make

    make: *** No rule to make target `../../lib/asuro.c', needed by `asuro.d'.  Stop.
    



*   Entweder stimmen die Pfadangaben nicht und die Quelldatei wird deshalb nicht gefunden. 
*   Falls die Pfadangaben korrekt sind und trotzdem die Fehlermeldung kommt hilft es meist die dependency Files von Hand aus dem entsprechenden Ordner loeschen. Diese wurden vielleicht aus einem anderen Ordner mitkopiert. del *.d 



## Weblinks

*   [microcontroller.net][1] - Makefile Beispiel 
*   [RN-Wissen][2] - AVR-GCC Interna 
*   [Makefile Tutorial][3] - Eine Einführung in Makefiles 
*   [Intel Hex Format][4]

 [1]: http://www.mikrocontroller.net/articles/Beispiel_Makefile
 [2]: http://www.roboternetz.de/wissen/index.php/Avr-gcc/Interna
 [3]: http://www.ijon.de/comp/tutorials/makefile.htm
 [4]: http://www.schulz-koengen.de/biblio/intelhex.htm