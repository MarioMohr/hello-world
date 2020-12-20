#GNU Privacy Guard (GnuPG)

Um Dateien oder E-Mails mit GnuPG signieren oder verschlüsseln zu können, benötigt man ein eigenes Schlüsselpaar.
Ein Schlüsselpaar besteht immer aus einem privaten Schlüssel und einem öffentlichen Schlüssel.

**Den privaten Schlüssel muß man immer sicher aufbehwahren und geheim halten!**
Der private Schlüssel wird benötigt um Daten zu entschlüsseln bzw. zu signieren.
Den öffentlichen Schlüssel kann man weitergeben, um Daten verschlüsseln zu lassen,
oder um die Signatur auf echtheit zu überprüfen.

Als erstes sollte man die GnuPG Version ermitteln.
		`gpg --version`

Alte Versionen (<2.2.x) sollen nicht verwendet werden!
		`sudo apt install gnupg2 gnupg-doc`


##Erzeugen eines neuen Schlüsselpaares
Mit GnuPG muß der primäre Schlüssel immer Unterschriften liefern können,
daher werden nur drei Möglichkeiten aufgelsitet um Schlüsselpaare zu erstellen.
- **RSA** und **RSA**	(Standard bei Gnu/Linux)	
- **DSA** und **ELGamal** (Standard für OpenGPG)
- **DSA**

Der **DSA-Schlüssel** wird ausschließlich für **Signaturen** verwendet.
Bei **OpenGPG** wird zum _verschlüsseln von Daten_ ein **ELGamal-Schlüsselpaar** benötigt.
Zusätzlich kann man mit einem ELGamal-Schlüsselpaar auch Signaturen erstellen.

Mit dem folgenden Kommando werden Schlüsselpaare erstellt.
		`gpg --gen-key`

Wichtig ist auch eine Wiederrufurkunde nach dem erstellen eines Schlüsselpaares zu erstellen.
Die Wiederrufurkunde wird automatisch mit erstellt wenn man die Option `--full-gen-key` verwendet.
		`gpg --full-gen-key`


##Erzeugen einer Widerrufurkunde
Die Wiederrufurkunde wird benötigt wenn man das Passwort (bzw. Mantra) von seinem Schlüsselpaar nicht mehr hat.
		`gpg --output revoke.asc --gen-revoke mykey`

**Die Wiederrufurkunde sollte wie der private Schlüssel sicher aufbewahrt werden und geheim gehalten werden.**

##Auflisten aller privaten Schlüssel
		`gpg --list-secret-keys`


##Auflisten aller öffentlichen Schlüssel
		`gpg --list-keys`


##Exportieren eines öffentlichen Schlüssel
		`gpg --output user.gpg --export user@mail.xyz`


##Importieren eines öffentlichen Schlüssel
		`gpg --import pubkey.gpg`

**Wenn ein Schlüssel importiert wird, sollte man auch dessen Authentizität überprüfen!**


##Die Authentizität von einem Schlüssel überprüfen
Mit der Option `--fingerprint` wird der Fingerabdruck von einem Schlüssel aufgelistet.
		`gpg --fingerprint user@mail.xyz`

##Authentizität von einer Signatur prüfen
Um die Authentizität einer Verschlüsselung zu prüfen verwendet man `--verify`.
Will man zugleich die Nachricht lesen, dann wird zusätzlich die Option `--decrypt` benötigt.
		`gpg --output example.file --decrypt example.sig`

===== Authentizität von einer abgetrennten Signatur prüfen =====
Für dieses Verfahren benötigt man die verschlüsselte Datei und extra eine Datei welche die Signatur enthält.
		`gpg --verify example.sig example.txt`

##Einen Schlüssel signieren
Um einen Schlüssel zu signieren und damit seine Gültigkeit zu bestätigen
muß man den Schlüssel mit der Option `--edit-key` bearbeiten.
		`gpg --edit-key user@mail.xyz
		> fpr
		> sign
		> check`


##Intigrität via digitaler Signatur erstellen
Durch dieses Verfahren lässt sich ein nachträgliche Manipulation feststellen.
		`gpg --output example.sig --sign example.txt`

##Intigrität via Signatur im Klartext erstellen
Der Vorteil dieser Methode ist dass der Empfänger die Daten auch ohne Prüfung einsehen kann.
		`gpg -clearsign example.txt`

##Intigrität via abgetrennter Signatur erstellen
Hierdurch bleiben die Daten im Originalzustand und die Signatur wird in eine extra Datei geschrieben.
Damit die Daten nicht vom Empfänger im nachhinein bearbeitet werden müssen.
		`gpg --output example.sig --detach-sig example.txt`

##Daten verschlüsseln
Man kann Dateien verschlüsseln, oder wenn man den Pfad der Quelle nicht angibt dann wird die _Standard-Eingabe_ verschlüsselt.
Wenn man die Option `--output` NICHT benutzt, dann wird das Endprodukt der _Standard-Ausgabe_ übergeben.
Mit der Option `--recipient` wird der zu verwendende Schlüssel bestimmt.
		`gpg --output example.gpg --encrypt --recipient user@mail.xyz example.txt`


##Daten Entschlüsseln
Genau wie beim verschlüsseln kann man `--output` und oder den Pfad der Quelle weg lassen,
um die _Standard-Ausgabe_ bzw. _Standard-Eingabe_ zu benutzen.
		`gpg --output example.file --decrypt example.gpg`


##Symetrisches Verschlüsselungsverfahren
Bei dieser Methode wird kein öffentlicher Schlüssel benötigt,
sondern nur ein Passwort (bzw. Mantra) verwendet um Daten zu verschlüsseln.
_Das Mantra darf dabei NICHT das gleiche sein welches zum erzeugen von Schlüsselpaaren verwendet wurde._
Genau wie beim verschlüsseln und entschlüsseln kann man die Option `--output` weg lassen
und oder den Pfad der Quelle weg lassen um die _Standard-Ausgabe_ bzw. _Standard-Eingabe_ zu nutzen.
		`gpg --output example.gpg --symmetric example.txt`

===== Editieren von Schlüsseln =====
		`gpg --edit-key user@mail.xyz
		> toggle
		> check
		> key 2
		> revkey
		> revsig
		> expire
		> trust
		> quit`


##Weitergabe von Schlüsseln
		`gpg --keyserver wwwkeys.de.pgp.net --recv-key 8075ACEE01E0317DF616B364E9E147301A06ACE0`
		`gpg --keyserver wwwkeys.de.pgp.net --send-key beispiel@mail.xyz`


##Exportieren vom privaten Schlüssel
	`gpg --export $PUB_FINGERPRINT -a > public.key`
	
##Exportieren vom privaten Schlüssel
	`gpg --export-secret-keys $SEC_FINGERPRINT -a > private.key`


##Links
- [Das Gnu-Handbuch zum Schutze der Privatsphäre](https://www.gnupg.org/gph/de/manual/index.html)
- [GnuPG Gentoo-Wiki](https://wiki.gentoo.org/wiki/GnuPG)
- [GnuPG Arch-Wiki](https://wiki.archlinux.org/index.php/GnuPG)
- [GnuPG Ubuntu-Wiki](https://wiki.ubuntuusers.de/GnuPG/)
