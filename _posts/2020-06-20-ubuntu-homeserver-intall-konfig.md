---
categories: ['Linux']
tags: ['Linux', 'Ubuntu', 'install', 'HomeServer', 'NAS']
title: 'Homeserver mit (L)ubuntu einrichten'
---

_Dieser Artikel hilft Dir, wenn Du dir ebenfalls ein Raid1 unter einem Ubuntu-Derivat einrichten möchtest und ein paar wenige Grundlagen in Linux (Verzeichniswechsel, Umgang mit Editor im Terminal usw.) beherrscht._

**BITTE BEACHTE DAS DIESE ANLEITUNG AUS DEM JAHR 2020 STAMMT UND MÖGLICHE NEUERUNGEN NICHT BERÜCKSICHTIGT**

## Vorbereitungen

Als erstes müssen wir natürlich das OS downloaden, in meinem Fall Lubuntu. Um einen Bootfähigen USB-Stick zu erstellen, nutze ich das tolle Tool  [Etcher](https://www.balena.io/etcher/). Einfach den USB-Stick wählen, Distri wählen und los gehts.  
Im BIOS einmal checken, ob alles korrekt eingestellt ist und wo ich schon mal im BIOS bin, wurde auch das Wake-on-LAN aktiviert, was für einen Homeserver ganz praktisch ist.

Nachdem Lubuntu sauber installiert ist und auch alle Hardware out-of-the-box läuft, folgt erstmal ein:

``` shell
sudo apt-get update
```

### ssh installieren

Zukünftig sollen am Server nur 2 Kabel hängen. Strom- und Netzwerkkabel. Damit ich von meinem Notebook auf den Homeserver zugreifen kann, wird im nächsten Schritt SSH installiert.

``` shell
sudo apt-get install openssh-server
```

### Netzwerk-Manager installieren

Von Haus aus funktioniert der Netzwerkanschluss tadellos, jedoch fehlt mir bei der Netzwerkkonfiguration etwas der Komfort. Daher folgt die Installation eines Managers in dem ich die Netzwerk-Konfig einfach verwalten kann.

``` shell
sudo apt-get install network-manager network-manager-gnome
```

Um zukünftigen Netzwerkproblemen aus dem Weg zu gehen, habe ich dem Server eine feste IP zugewiesen.

``` shell
# Beispiel
NETMASK=255.255.255.0
IPADDR=192.168.2.100
GATEWAY=192.168.2.1
```

### Login per ssh

Der Login auf dem Homeserver funktioniert nun über  `ssh username@ip-adresse`  also z.B.  `ssh christian@192.168.2.100`. Nach der Passworteingabe steht die Verbindung zum Homserver.  **Nun alles Weitere per SSH…**

### mdadm und parted

Für die Konfiguration der Festplatten und des Raid benötigen wir  [MDADM](https://wiki.ubuntuusers.de/Software-RAID/){:target="_blank" rel="nofollow"}  und  [Parted](https://wiki.ubuntuusers.de/GNU_Parted/){:target="_blank" rel="nofollow"}.

``` shell
sudo apt-get install mdadm parted
```

## RAID1 einrichten

Mit  `sudo fdisk -l`  können wir alle Festplatten anzeigen um mehr Details zu erfahren. Weil beide Festplatten bereits testweise zu Testzwecken in einem Raid1 konfiguriert wurden, muss auf  `sdb`  und  `sdc`  die komplette Datenstruktur gelöscht werden. Die SSD mit dem Lubuntu-System läuft unter  `sda`, daher sollten wir diese natürlich nicht anfassen.

``` shell
dd if=/dev/zero of=/dev/sdb bs=512 count=1
```

Aufgrund der 4TB Größe verwende ich die GPT-Partitionstabelle. Bevor diese angelegt werden können, ist (zumindest in meinem Fall) ein Reboot notwendig. Und immer daran denken, alle Aktionen für  `sdb`  und  `sdc`  durchführen oder wie die Bezeichnung eben bei Dir ist… siehe  `sudo fdisk -l`

``` shell
sudo parted /dev/sdb mklabel gpt
```

Nun können wir mit dem Erstellen der Partitionen beginnen:

``` shell
sudo fdisk /dev/sdb
```

1.  mit  **n**  neue Partition erstellen
2.  Partitionsnummer festlegen (**1**)
3.  bei  _First sector_  **Enter**
4.  bei  _Last Sector_  **Enter**
5.  Erkennung der (alten) Signatur – Löschen bestätigen
6.  Typ der Partition festlegen mit  **t**.
7.  In meinem Fall benötige ich  _Linux RAID_  und habe die  _29_  gewählt (eine komplette Liste wird unter  **L**  angezeigt)
8.  Alle bisherigen Einstellungen überprüfen mit  **p**
9.  Wenn alles passt, können wir mit  **w**  alle Einstellungen übernehmen.  
    Anschließend noch das  **logische Laufwerk im Raid 1 erstellen**:

``` shell
mdadm --create /dev/md0 --bitmap=internal --level=mirror --raid-devices=2 /dev/sdb1 /dev/sdc
```

Nun können wir uns erstmal eine Pause gönnen, da die HDDs nun syncronisiert werden. wie weit der Fortschritt ist erfährst Du mit  `watch cat /proc/mdstat`. Bei 2x 4TB im Raid1 werden bei mir ca 330 Minuten angegeben. Ich habe diesen Vorgang einfach über Nacht laufen lassen.

Den Status und weitere Details des Laufwerks erfährt man durch:

``` shell
sudo mdadm --detail /dev/md0
```

Nachdem wir nun das Raid1 eingerichtet und syncronisiert haben, müssen wir die Partition noch im `EXT4` formatieren.

``` shell
sudo mkfs.ext4 /dev/md0
```

Um einfach auf unser Raid zugreifen zu können, müssen wir einen Mountpoint erstellen und das Raid1 darin mounten:

``` shell
sudo mkdir /mnt/raid1
sudo mount /dev/md0 /mnt/raid1
```

Die verfügbare Kapazitäten kannst Du überprüfen mit:

``` shell
df -h /mnt/raid1
```

**WICHTIG: Nun muss die Konfiguration unbedingt noch gespeichert werden.**

``` shell
sudo mdadm --detail --scan --verbose | sudo tee -a /etc/mdadm/mdadm.conf
```

Nun noch das  [initramfs](https://de.wikipedia.org/wiki/Initramfs){:target="_blank" rel="nofollow"}  updaten. Wird das initramfs nicht geupdated, kann es sein, dass dies Bootprobleme zur Folge hat. In dem Fall kann es helfen, während des GRUB-Bootloaders die  `SHIFT-Taste`  gedrückt zu halten und anschließend das zu bootende System manuell zu wählen.

``` shell
sudo update-initramfs -u
```

Um das Raid1 beim Boot automatisch zu mounten muss noch die  `/etc/fstab`  mit  `sudo nano /etc/fstab`  aktualisiert werden:

``` shell
# Standard
/dev/md0   /mnt/raid1   ext4   defaults   0   0
# mit Anzeige in Sidebar
/dev/md0  /mnt/raid1   ext4    defaults,x-gvfs-show   0   0
```

### Ruhemodus der Festplatten nach x-Minuten aktivieren

Man könnte die HDD-Konfiguration auch schnell über die Konsole regeln, aber für diverse Einstellungen ist ein grafisches Tool schon nicht verkehrt. Ich habe nun nachträglich eine Laufwerksverwaltung installiert:

``` shell
sudo apt-get install gnome-disk-utility
```

## Samba Fileshare einrichten

Zuerst muss der Samba-Server installiert werden.

``` shell
# Server und Pakete updaten
apt-get update && apt-get upgrade
# Samba installieren
apt-get install samba samba-common
```

Nachdem die Installation abgeschlossen ist, müssen wir nun die Konfiguration vornehmen. Um im Zweifelsfall die originale Konfig-Datei wiederherstellen zu können, legen wir zuerst ein Backup an.

``` shell
# Kopie erstellen
cp /etc/samba/smb.conf /etc/samba/smb.conf-old
```

Nachdem wir nun die  `smb.conf`  mit  `nano /etc/samba/smb.conf`  geöffnet und den gesamten Inhalt mit  `STRG + K`  gelöscht haben, können wir den Samba-Server konfigurieren.

``` shell
[global]
        workgroup = arbeitsgruppe
        server string = %h server (Samba %v)
        log file = /var/log/samba/log.%m
        max log size = 1000
        encrypt passwords = true
        invalid users = root
        socket options = TCP_NODELAY
        security = user
        unix extensions = yes
[share]
        comment = HomeServer Media
        path = /mnt/raid1/media
        writeable = yes
        guest ok = no
```

Mit  `service smbd start`  den  [Samba-Server](https://wiki.ubuntuusers.de/Samba_Server/){:target="_blank" rel="nofollow"}  
starten und einen Samba-User anlegen. Anschließend muss nur noch ein Passwort vergeben werden:

### neuen User anlegen

``` shell
adduser --disabled-login --shell /bin/false --home /mnt/raid1/media family
```

### neuen User in Samba-DB hinzufügen

`smbpasswd -a family`

### miniDLNA konfigurieren

Um Bilder, Videos und Musik auch über das Netzwerk auf dem TV anzeigen zu können, nutzen wir den DLNA-Standard. Unter Linux benötigen wir das Paket:

``` shell
sudo apt install minidlna
```

Sicherheitskopie anlegen und die Konfiguration anpassen:

``` shell
cp /etc/minidlna.conf /etc/minidlna-old.conf
sudo nano /etc/minidlna.conf
```

### Konfiguration

``` shell
#   * "A" for audio    (eg. media_dir=A,/var/lib/minidlna/music)
#   * "P" for pictures (eg. media_dir=P,/var/lib/minidlna/pictures)
#   * "V" for video    (eg. media_dir=V,/var/lib/minidlna/videos)
media_dir=V,/mnt/raid1/media/videos
media_dir=A,/mnt/raid1/media/musik
media_dir=P,/mnt/raid1/media/fotos

### Name that the DLNA server presents to clients.
Defaults to "hostname: username"
friendly_name= MiniDLNA-Server

### Automatic discovery of new files in the media_dir directory.
inotify=yes
```

Neustart des MiniDLNA-Server

``` shell
sudo service minidlna restart
```

Nun sind wir  **fertig.**   Diese Anleitung bietet natürlich keine Garantie, dass die beschriebenen Schritte bei Dir ebenfalls funktionieren. Im Zweifelsfall hilft das Forum von  [ubuntuusers](https://forum.ubuntuusers.de/){:target="_blank" rel="nofollow"}. Dort sind nicht nur viele sehr versierte Linuxer zu finden, sie sind auch noch äußerst hilfsbereit.