# Command Line Interpreter Grundwissen - (CLI basics)  


## Suche und Hilfe  

**In einer Verzeichnishierarchie nach Dateien suchen (search in directory tree for filename)**  
	$ find [PATH] -name [NAME]  

**Anleitung zu einem Programm betrachen (show manual pages of programm)**  
	$ man [NAME]

**Ermitteln des Pfades von einem Programm (print path of programm)**  
	$ which [NAME]  

**Programmtyp ermitteln (get type of programm)**  
	$ type [NAME]  


## Bewegen in der Verzeichnishierarchie (browsing the directory-tree)  

**Ermitteln der aktuellen Position im Verzeichnissbaum (print working directory)**  
	$ pwd  

**Auflisten vom Inhalt eines Verzeichnis (listing content of a directory)**  
	$ ls [PATH]  
_Wenn kein Pfad angegeben wird, dann wird der Inhalt vom aktuellen Verzeichnis aufgelistet (list content of used path when no path is set)._  

**Gehe zu einem bestimmten Verzeichnis (go to directory)**  
	$ cd [PATH]  
_Wenn kein Pfad angegeben wird, dann wird zu deinem Heimatverzeichnis gewechselt (Change to your home-directory when no path is set)._  

**Gehe ins übergeortnete Verzeichnis (go to to parent directory)**  
	$ cd ..  

**Wechsel zurück ins vorherige Verzeichnis (go back to the former working directory)**  
	$ cd -  



## Dateien verwalten (managing files)  

**Ein neues Verzeichnis erstellen (create new direcoty)**  
	$ mkdir [PATH]  

**Ein leeres Verzeichnis löschen (remove an exsisting and empty directory)**  
	$ rmdir [PATH]  

**Lösche Datei(en) (remove files)**  
	$ rm [FILENAMES]  

**Lösche Verzeichnisse und dessen Inhalt (remove paths and its content)**  
	$ rm -r [PATHS]  

**Verschiebe Datei(en) und Verzeichnis(se), oder benenne einzellne Dateien/Verzeichnisse um (moving or renaming files and directories)**  
	$ mv [FILES/PATHS] [DESTINATION]  



## Anzeigen und und verändern von Text-Dateien (display and modifying text-files)  

**Inhalt von Text-Datei(en) anzeigen lassen (display content of text-files)**  
	$ cat [FILES]  

**Inhalt einer Text-Datei seitenweise anzeigen lassen (display content of text-file in a pager)**  
	$ less [FILE]  

**Nur Zeilen aus Datei(en) auslesen, welche mit dem Suchmuster übereinstimmen**  
	$ grep [SEARCHSTRING] [FILES]  

**Text-Editor öffnen (open text-editor)**  
	$ editor [FILE]  
_Wenn keine Datei angegeben wird, dann wird eine leere Instanz gestartet (open a empty session when no file is set)._  

**Kommandos in den Text-Editor schreiben und dann ausführen (write and run commands from text-editor)**  
	<STRG>-x-e  

**letztes Kommando im Text-Editor bearbeiten und dann ausführen (edit last command in text-editor and run it)**  
	$ fc  

**Ausgabe von einem Kommando in eine Datei anhängen (add command output to a file)**  
	$ echo "Hello World!" >> [FILE]  
_Falls die Datei noch nicht exsistiert wird diese erstellt (file will be create if not exsist already)._  

**Ausgabe von einem Kommando in eine Datei schreiben (write command output into file)**  
	$ echo "Hello World!" > [FILE]  
WICHTIG: Falls die Datei schon exsistieren sollte dann wird diese überschrieben (IMPORTANT: an exsisting file will be overwrite).  

**Datei erstellen (create file)**  
	$ touch [FILE]  
_Falls die Datei schon exsistiert dann wird nur die Zugriffszeit angepasst (only the timestamp will be updated if the file exsist already)._  



## Umgebungsvariablen in der "Bourne again Shell" (enviroment variables of bash)  

**Ermitteln von allen aktiven Umgebungsvariablen (list all enviroment variables)**  
	$ printenv  

**Fehlercode vom letzten verwendeten Kommando ermitteln (get error-code of last used command)**  
	$ echo "$?"  



## Prozess-Verwaltung (Managing Processes)  

**Auflistung der aktiven Prozesse, inkl. Identifikationsnummer (List active processes, incl. PID)**  
	$ ps ax  

**Bestimmten Prozess anhand dessen Identifikationsnummer auflisten**  
	$ ps -f [PID]  

**aktive Prozesse anzeigen lassen, inkl. CPU- und Speicher-Auslastung (show active processes, incl. workload of cpu and memory)**  
	$ top  
_Mit Taste 1 kann die Anzeige der einzelnen CPU-Kerne ein- und ausgeschaltet werden (activate and deactivate single core listing with key 1)._  

**Auflisten von Prozessen welche unterbrochen wurden und Kommandos die im Hintergrund laufen (list suspend commands and commands runnig in the background)**  
	$ jobs  

**Unterbrochenes Kommando, oder Kommando im Hintergrund, wieder in den Vordergrund bringen (bring back to foreground suspended commands and background commands)**  
	$ %[JOBNUMBER]  

**Unterbrochenes Kommando im Hintergrund ausführen (run suspended command in the background)**  
	$ %[JOBNUMBER] &  

**CLI beenden aber alle Prozesse weiter laufen lassen**  
	$ disown -a && exit  

**SIGTSTP: Kommando unterbrechen (SIGTSTP: suspend command)**  
	<STRG>-z  
oder  
	$ kill -20 [PID]  

**SIGCONT: Unterbrochenes Kommando wieder ausführen (SIGCONT: resume suspended command)**  
	$ kill -18 [PID]  

**SIGTERM: Prozess beenden (SIGTERM: kill process)**  
	<STRG>-c  

**SIGTERM: Prozess beenden anhand der Identifikationsnummer (SIGTERM: kill process with help of PID)**  
	$ kill [PID]  
_Wenn kein Signal bestimmt wurde dann wird kill mit SIGTERM ausgeführt (kill will run with SIGTERM if no other signal is specified)._  
_Wenn SIGTERM den Prozess nicht beendet kann man SIGINIT versuchen (you can try SIGINIT if SIGTERM didn't work)._  
_Wenn auch SIGINIT nichts bewirkte dann probiert man es mit SIGHUP (you can try SIGHUP if also SIGINIT didn't work)._  
_Die letzte Möglichkeit die man verwenden sollte um einen Prozess zu beenden ist SIGKILL (Last option you should use to end a job is SIGKILL)._  

**SIGTERM: Prozess beenden anhand des Namen (SIGTERM: kill process with help of its name)**  
	$ pkill [NAME]  
WARNUNG: Dieses Kommando beendet alle Prozesse die den gleichen Namen beinhalten (WARNING: this command ends all processes with the same name in it).  
_Ansonsten gelten die gleichen Regeln wie bei "kill" (apart frin that it has the same rules as the kill command)._  

**Auflisten aller Signale**  
	$ kill -l  





