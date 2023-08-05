# Raspberry Pi boot from SSD

## Möglichkeit 1

Guide von [hier](https://forum-raspberrypi.de/forum/thread/48950-tutorial-eine-unendliche-geschichte-raspberry-4b-und-usb-boot/)

### Vorbereitung

Zuerst benötigt man Buster auf eine SD-Karte.

Ein Image davon auf die SD-Karte flashen und ohne SSD erstmal booten.
Ein kleines bißchen einrichten (Sprache und Tastatur) und dann erstmal ein:
sudo apt update && sudo apt full-upgrade
Warscheinlich ist dann erstmal ein reboot fällig.

### Updaten übers Betriebssystem

Dann überprüft ihr ob der Bootloader aktuell ist:

```bash
$ sudo rpi-eeprom-update
BCM2711 detected
Dedicated VL805 EEPROM detected
BOOTLOADER: up-to-date
CURRENT: Do 16. Apr 17:11:26 UTC 2020 (1587057086)
LATEST: Do 16. Apr 17:11:26 UTC 2020 (1587057086)
FW DIR: /lib/firmware/raspberrypi/bootloader/critical
VL805: up-to-date
CURRENT: 000137ad
LATEST: 000137ad
```

Dieser ist es nicht, er sollte auf "**stable**" (hier "**critical**") stehen, also müsst ihr ihn aktualisieren.

Dazu muss der Eintrag in einer Datei geändert werden:

```bash
sudo nano /etc/default/rpi-eeprom-update
```

Dort ändert ihr die Zeile von: `FIRMWARE_RELEASE_STATUS="critical"` in `FIRMWARE_RELEASE_STATUS="stable"`

Der Bootloader wird aktualisiert, wenn ihr folgenden Befehl ausführt:

```bash
sudo rpi-eeprom-update -d -f /lib/firmware/raspberrypi/bootloader/stable/pieeprom-2020-07-31.bin
```

oder

```bash
sudo rpi-eeprom-update -a
```

_Anmerkung_: Der Name des Bootloaders `pieeprom-2020-07-31.bin` könnte sich nach diversen Upgrades geändert haben.

Jetzt wäre ein weiteres reboot angebracht und danach solltet ihr das Ergebnis überprüfen:

```bash
$ sudo rpi-eeprom-update
BCM2711 detected
Dedicated VL805 EEPROM detected
BOOTLOADER: up-to-date
CURRENT: Fr 31. Jul 13:43:39 UTC 2020 (1596203019)
LATEST: Fr 31. Jul 13:43:39 UTC 2020 (1596203019)
FW DIR: /lib/firmware/raspberrypi/bootloader/stable
VL805: up-to-date
CURRENT: 000138a1
LATEST: 000138a1
```

Wie man sieht, ist jetzt der Bootloader "**up-to-date**" und steht auf "**stable**".

Jetzt kommt noch ein Check ob die Bootkonfiguration richtig ist:

```bash
vcgencmd bootloader_config
[all]
BOOT_UART=0
WAKE_ON_GPIO=1
POWER_OFF_ON_HALT=0
DHCP_TIMEOUT=45000
DHCP_REQ_TIMEOUT=4000
TFTP_FILE_TIMEOUT=30000
ENABLE_SELF_UPDATE=1
DISABLE_HDMI=0
BOOT_ORDER=0xf41
```

Die Boot-Order findet man [hier](https://www.raspberrypi.org/do…2711_bootloader_config.md)

Ab jetzt ist der Raspberry für den USB-Boot vorbereitet.

Nun kommt der nächste Schritt:
Flasht dasselbe Image auf die SSD, entfernt die SD-Karte und versucht von SSD zu booten.
Sollte das klappen, müßt ihr Buster neu einrichten.

_Wichtig_: Den Eintrag: `/etc/default/rpi-eeprom-update auf` "**stable**" auf der SSD überprüfen.

### Von der SD-Karte auf die SSD

Man nehme einfach den SD Card Copier des Betriebssystems.

1. _Von Gerät kopieren_: Hier die SD-Karte auswählen
2. _Auf Gerät kopieren_: Hier die SSD auswählen
3. New Partition UUID ankreuzen

Und dann auf Start klicken.

Das wars, das Programm kopiert die SD-Karte auf die SSD, passt nebenbei die `/boot/cmdline` und die `/etc/fstab`
auf die neue PARTUUID an und resized die root-Partition.

Das klappte sogar aus dem laufenden Betriebssystem (Buster64, light mit Mate-Desktop) heraus.
Und bootete sofort von SSD. Ich würde sagen, DAU-Geeignet, einfacher geht es kaum.
Eine weitere Beschreibung findet sich hier: [RE: Raspberry Pi4 4GB SSD Boot](https://forum-raspberrypi.de/forum/thread/48413-raspberry-pi4-4gb-ssd-boot/?postID=446208#post446208)

### Das Geheimnis der leeren SD-Karte

![Performance Graph](https://forum-raspberrypi.de/attachment/28007-raspi31-raspi-cpu-day-png/)

Einfach die kleinste MicroSD-Karte mit (Gparted) fat32 formatieren und in den Kartenslot stecken. Wirkt sogar beim RPi3B(+)

## Möglichkeit 2 (Ungetestet)

Guide von [hier](https://forum-raspberrypi.de/forum/thread/48950-tutorial-eine-unendliche-geschichte-raspberry-4b-und-usb-boot/?postID=446954#post446954)

### Backgrouninformationen

Ab Juni gab es ein Beta-USB-rpi-boot-eeprom-recovery und mittlerweile seit Ende Juli ein stable [rpi-boot-eeprom-recovery für USB Boot](https://github.com/raspberrypi/rpi-eeprom/releases/tag/v2020.07.31-138a1).

### Umsetzung

Dieses wird auf eine Fat32 formatierte mSD entpackt, in den Raspi 4 damit und Spannungsversorgung einschalten.
Blinkt die grüne LED dann gleichmäßig schnell hintereinander ist das recovery beendet und man kann ganz ohne Umweg über eine mSD Karte gleich auf die Festplatte/ SSD / USB oder was auch immer sein BS Flashen, anstecken und es bootet.
