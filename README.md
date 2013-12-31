-AU3--Serial-HWID-System
========================

Volles funktionsfähiges HWID-System mit Seriennummern zur Aktivierung




README:

Glosar:
HWID / HWID-Schutz
Ein HWID-Schutz soll verhindern dass das entsprechende Programm einfach weitergegeben werden kann.
Um die HWID zu ermitteln ließt man z.B. die Seriennummer der Festplatte aus und noch ein paar andere Details wie Windows Key o.ä. ein. 
Danach wird alles zusammengepackt und gehasht so dass ein Wert entsteht welcher sich auf jedem Computer unterscheiden sollte.


Funktionsweise:
	Programm	<>	PHP-Server	<>	MySQL-Datenbank

Das Programm generiert die HWID des Rechners auf dem es läuft und schickt diese an ein PHP-Script.
Sollte diese regisitriert sein startet das Programm.
Ist sie nicht regisitriert erscheint eine "RegistrierungsGUI" und fordert eine Seriennummer.
Wird diese eingegeben und ist richtig, dann wird die HWID in der Datenbank hinterlegt.
Ist diese falsch wird eine Meldung angezeigt: MsgBox(16, "Fehler", "Der angegebene Aktivierungscode ist falsch.")
Wird diese bereits verwendet wird eine Meldung angezeigt: MsgBox(16, "Fehler", "Der angegebene Aktivierungscode ist bereits aktiviert.")


///// AutoIt Scripte  '.\Scripte'
HWID.au3 = Generiert die HWID, erstellt eine GUI falls nicht aktiviert und überprüft den Aktivierungsvorgang.
Serialgen.au3 = Generiert automatisch verschiedene Serials und trägt diese automatisch in die Datenbank ein.

///// PHP Scripte  '.\Upload\PHP\'
check_hwid.php = Nimmt HWID von Script entgegen und prüft diese.
register.php = Nimmt HWID und Serial entgegen, prüft beide und trägt sie ein.
db_config.php = Enthält die MySQL Verbindungsdaten  <-- Müssen eingetragen werden
insert_serial.php = Nimmt Serials von dem Serialgen.au3 entgegen und trägt diese ein.  <-- Sollte wieder vom Server entfernt werden


ToDo:
1.	/Scripte/HWID.au3
	
	nachfolgende Variablen anpassen

	$sCryptKey = "Verschlüsselungscode"
	$sAlgo = $CALG_AES_256
	$sTitle = "Programmtitel"
	$sURL = "http://www.deineseite.de"
	#endregion parameters



2.	/Scripte/HWID.au3
	
	nachfolgende Variablen anpassen
	
	$sAddSerialURL = "http://www.deineseite.de/insert_serial.php?serial="
	


3.	/Upload/PHP/db_config.php
	
	nachfolgende Variablen anpassen
	
	<?php
	$host = "localhost";
	$user = "";
	$pass = "";
	$dbase = "";
	?>



4.	/Upload/DB.sql

	per phpMyAdmin in die in Schritt 3. gewählte Datenbank einladen. Importieren, Datei auswählen, fertig)



5.	Uploaden der Daten
	
	per FTP o.ä. auf den Server verbinden und den Inhalt des Ordners '/Upload/PHP/' dort ablegen.



6.	/Scripte/Serialgen.au3

	über das Script eine bestimmte Anzahl an Seriennummern generieren lassen.



7. 	/Upload/PHP/insert_serial.php

	diese Datei wieder vom Server löschen!



8.	/Scripte/HWID.au3

	starten und überprüfen ob das ganze System funktioniert. Wenn bei der Eingabe einer eingetragenen Seriennummer
	die Meldung "Die Aktivierung war erfolgreich.Das Programm startet jetzt automatisch." kommt, hat alles 	funktioniert.



Fehlerbehebung:
die URL's überprüfen, ob die Unterverzeichnise/Domain stimmt.



Hoffe das hilft dem einen oder anderen von euch weiter.

lg Fl00d3R
