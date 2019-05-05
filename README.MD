-------------------
### Umgebung auf Notebook
Bewertungskriterien 1

#### Virtual Box
Virtual Box VM Applikation zeigen

#### Vagrant
Vagrant VM Starten ("vagrant up" in directory)

#### Visual Studio Code
VBS Zeigen

#### SSH Key Github
SSH Key auf GITHUB zeigen (Profile/Settings/SSH)

### Eigne Lernumgebung (PLE) ist eingerichtet
Bewertungskriterien 1

#### Github account
Github account zeigen

#### GIT Zeigen
GitHub struktur Zeigen

#### Dokumentation Zeigen
Doku in browser zeigen

#### Markdown Dokumentation Zeigen in VBS
Doku in VBS Zeigen

### VAGRANT
Bewertungskriterien 1

#### Vagrant Befehle auflisten
Vagrant Befehle Aufgelistet

<tab>    | <tab>
--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Befehle**   | Verwendung
vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64        | #Vagrant-Box
vagrant init ubuntu/xenial64       | #Vagrantfile erzeugen 
cd Pfad/zu/meiner/Vagrant-VM | #Zum Verzeichnis der VM wechseln
vagrant ssh| #SSH-Verbindung zur VM aufbauen
ls -l /bin| #Bin-Verzeichnis anzeigen
df -hdf -h| #Freier Festplattenspeicher
free -m| #Freier Arbeitsspeicher

#### Testing fälle zeigen
Kapitel Testfälle

#### Vagrant Cloud
Vagrant Cloud VM zeigen

#### Vorgefertigte VM
SSH Key auf GITHUB zeigen (Profile/Settings/SSH)

# Modul 300 Dokumentation
## Inhaltsverzeichnis

1. Login
2. Web-Server Installation mit Vagrant
   1. Vagrantfile
   2. Neuer Sudo User erstellen
      1. Sudo User Testen
   3. Firewall Regeln
   4. SSH Key erstellen
   5. MySQL, PhP und PhPMyAdmin Installation
3. Vagrant Box Release
1. Tests
    1. Testfall 1
    2. Testfall 2
    3. Testfall 3
4. Vergleich Vorwissen und Wissenszuwachs
   1. Vorwissen
   2. Wissenszuwachs
5.  Reflexion


# Web-Server Installation mit Vagrant
## Vagrantfile
Das Vagrantfile dient der Konfiguration der VM, bevor man sie das erste Mal aufstartet.

![Vagrantfile](lb2_screenshots/vagrantfile.PNG)

## Neuer Sudo User erstellen
Um das Usererstellen auszuprobieren habe ich einen neue Sudo User erstellt. Dies ging ganz einfach mit dem Kommando `sudo adduser m300admin`. "m300admin" ist dabei der Username. Anschliessend wird man noch nach einem Passwort gefragt. Dabei habe ich wieder dasselbe verwendet wie immer.

![NeuerSudoUser1](lb2_screenshots/usererstellen1.PNG)

Anschliessend benötigt der neue erstellte User noch die Berechtigungen um die Rolle als SuperUser zu erfüllen. Dies gint mit dem Kommando `sudo usermod -aG sudo testuser`

![NeuerSudoUser2](lb2_screenshots/usererstellen2.PNG)

### Sudo User testen

Um zu überprüfen, dass der neu erstellte User auch die richtigen Berechtigunen hat, habe ich mich auf ihm eingeloggt. Ganz einfach mit dem Befehl `su - testuser`. Und dann auf dem neuen Benutzer ein Befehl mit `sudo` ausgeführt. In diesem Fall habe ich die nummerierte Firewall-Regel Tabelle abgerufen. Weiter unten (im Bild) sieht man, dass der Befehl ohne `sudo` nicht funktioniert.

![NeuerSudoUserTest](lb2_screenshots/usertesten.PNG)

## Firewall Regeln

Ich habe mich für folgende Firewall Regeln entschieden. Diese hatten keinen besonderen Grund, einfach, dass ich beim installieren auf keine Probleme stosse.

![FirewallRegeln](lb2_screenshots/ubuntufirewall.PNG)

## SSH Key erstellen

Mit folgendem Befehl habe ich einen SSH Key erstellt um den abgesicherten SSH Zugriff zu sichern.

![SSHkeygen](lb2_screenshots/newsshkey.PNG)

## MySQL, PhP und PhPMyAdmin Installation
MySQL installieren.

![SSHkeygen](lb2_screenshots/installmysql.PNG)

PhP installieren.

![SSHkeygen](lb2_screenshots/installphp.PNG)

phpmyadmin installieren.

![SSHkeygen](lb2_screenshots/installphpmyadmin.PNG)

Damit die index.php Seite über dem Apache2-Index priorisiert wird, muss man das dir.conf File so anpassen, dass in der zweiten Zeile index.php vor index.html vorkommt.

![SSHkeygen](lb2_screenshots/editdirconf2.PNG)

Als letztes muss man noch die phpmyadmin mods installieren.

![SSHkeygen](lb2_screenshots/enablephpmyadminmods.PNG)

# Vagrant Box Release

Nachdem alle Services auf dem Server installiert wurden kann man mithilfe des commands `vagrand packet --output <boxname>.box` die im aktuellen Verzeichnis laufende VM packetieren und ein .box File erstellen. 

Anschliessend muss man sich bei https://vagrantcloud.com anmelden und den Button "Create a new Vagrant Box" anwählen. Darin folgt man den einzelnen Schritten. Beim Feld "Provider" wählt man "virtualbox" aus, da alles auf dieser Software aufgesetzt wurde. Anschliessend kann man das eben erstellte .box File hochladen und die Vagrant Box Releasen.

![VagrantBoxRelease](lb2_screenshots/vagrantcloudrelease.PNG)

## Tests
### Testfall 1
__Titel:__ Start der Container

__Datum:__ 3.5.19

__Beschreibung:__ Die Container werden gestartet.

__Erwartetes Ergebnis:__ Die Erwartung ist, dass verschiedene Container erstellt werden.

__Eigenliches Ergebnis:__ Es sind zwei verschiedene Container erstellt worden. Einer mit dem Namen "docker_mariadb_1" und einer namens "docker_php-apache_1".

### Testfall 2
__Titel:__ PHP Index Seite

__Datum:__ 3.5.19

__Beschreibung:__ Verbindung auf Server via Browser.

__Erwartetes Ergebnis:__ Erfolgreiches Erreichen der Seite des Servers. Es sollte die PHP Index Seite angezeigt werden.

__Eigenliches Ergebnis:__ Erfolgreich auf die Seite gekommen. Bei verändern der index.php Datei hat sich auch direkt die Seit im Browser verändert.

### Testfall 3
__Titel:__ Überwachung

__Datum:__ 3.5.19

__Beschreibung:__ Verbindung auf Server via Browser und Überprüfung der Überwachung.

__Erwartetes Ergebnis:__ Eintrag in der Konsole, dass um diese Zeit ein Benutzer diese Seite aufgerufen hat. Mit dem Browser Google Chrome auf Windows.

__Eigenliches Ergebnis:__ Test war erfolgreich. Folgende Zeile wurde in der Konsole ausgegeben. `php-apache_1  | 212.203.120.1 - - [03/May/2019:11:02:45 +0000] "GET / HTTP/1.1" 200 23807 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36"`.

# Vergleich Vorwissen und Wissenszuwachs
## Vorwissen
Vor dem Modul hatte ich gerade Mal eine grundlegende Anhung was Virtualisierung anbelangt. Ich wusste wie man Virtuelle Maschinen aufbaut, was Cloud Services sind und ein wenig über Containerisierung.

Jedoch hatte ich noch nie von Vagrant oder Docker gehört, deshalb war alles, was die Konfiguartion angeht neu für mich.

## Wissenszuwachs
Ich konnte in diesem Projekt Vagrant sehr gut kennenlernen, und damit arbeiten. Ich hätte jedoch nicht so viel Zeit damit verschwenden sollen, da ich am Ende nicht mehr viel Zeit für die LB3 hatte. 

In der LB3 konnte ich mein Wissen in Docker sehr erweitern, da dies ebenfalls Neuland für mich war.

# Reflexion
Da ich persönlich noch nie mit Vagrant oder Docker gearbeitet habe, war alles neu für mich. Dass die einzelnen Arbeitsschritte grösstenteils bereits Dokumentiert waren, hat mir sehr geholfen.

Womit ich jedoch schwierigkeiten hatte, war der Auftrag selbst. Mir, und warscheinlich auch anderen aus meiner Klasse, war nicht klar was am Ende dieser LBs das Ziel war. 

Weiter stand ich lange an der Konfiguration bzw. Automatisierung der VMs an. Ich verstand anfangs nicht wie, wo und was.

Schlussendlich fand ich dieses Projekt sehr Interessant und ich habe sehr viel neues dazugelernt und ich konnte meine Fähigkeiten in Linux wieder einmal auffrischen.