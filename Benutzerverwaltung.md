# Benutzerverwaltung

**Benutzer mit normalen Rechten erstellen**
	useradd -m -G audio,games,users,video [USERNAME]
	passwd [USERNAME]

**Passwort eines Benutzers ändern**
	passwd [USERNAME]

**Neue Gruppe erstellen**
	addgroup [GROUPNAME]

**Bestehenden Benutzer einer weiteren Gruppe hinzufügen**
	usermod -aG [GROUPNAME] [USERNAME]

**Ermitteln aller Gruppen welche einem Benutzer zugeteilt wurden**
	groups [USERNAME]

**Benutzer ohne Rechte erstellen**
	useradd -d /home/jail -g nogroup -s /usr/sbin/nologin [USERNAME]
	chown root:root /home/jail
	chmod -R 755 /home/jail

**Benutzername ändern und dessen Heimatverzeichnis anpassen**
	usermod -md /home/[NEW_NAME] -l [NEW_NAME] [OLD_NAME]

**Vor- und Nachname eines Benutzer ändern**
	chfn -f [FIRSTNAME_SURNAME] [USERNAME]

**Dem Benutzer seine UID ändern**
	usermod -u [NEW_UID] [USERNAME]
Dateien und Verzeichnisse auserhalb dem Heimatverzeichniss müssen manuell angepasst werden ...
	chown -R [USERNAME][:GROUPNAME] [PATH]

**Dem Benutzer seine GID ändren**
	groupmod -g [NEW_GID] [GROUPNAME]
Dateien und Verzeichnisse müssen manuell angepasst werden ...
	chgrp -R [GROUPNAME] [PATH]

**Login-Rechte von einem Benutzer entziehen, damit der Benutzer sich nur noch über andere Dienste anmelden kann**
	usermod -s /usr/sbin/nologin [USERNAME]

**Benutzer inkl. Heimatverzeichnis und Mailspool löschen**
	userdel -r [USERNAME]
Dateien und Verzeichnisse auserhalb dem Heimatverzeichnis müssen manuell angepasst werden ...
	rm -r [PATH]


