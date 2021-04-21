# Raspberry VNC Setup

## Raspberry aufsetzen

1. Raspbian mit grafischer Oberfläche installieren
2. SSH einrichten
3. [VNC einrichten](https://www.raspberrypi.org/documentation/remote-access/vnc/)
4. Automatisch in GUI booten deaktivieren

## VNC configurieren

1. Verbinden über ssh
2. VNC config öffnen mit

```bash
~ $ nano .vnc/config
```

3. Folgenden Text hinzufügen und speichern

```bash
-randr 800x600,1024x768,1280x800,1280x960,1280x1024,1680x1050,1920x1080,3360x1050,1024x700,1200x740,1600x1000,3200x1000
```

4. VNC Server starten mit folgendem befehl

```bash
~ $ vncserver
...
New desktop is raspberry:1 (192.168.178.61:1)
```

5. Auflösung anpassen (Display bezeichnung ist `:1`)

```bash
~ $ xrandr -display <display> -s <auflösung>
```

3. Mit VNC verbinden über den [RealVNC Viewer](https://www.realvnc.com/de/connect/download/viewer/)

## GUI ändern

1. tasksel installieren

```bash
~ $ sudo apt install tasksel
```

2. [GUI installieren und starten](https://linoxide.com/linux-how-to/how-install-gui-ubuntu-server-guide/)

3. VNC display neu starten

```bash
~ $ vncserver <display> -kill
~ $ vncserver
```

### GUI ändern alternative

Siehe [hier](https://forum-raspberrypi.de/forum/thread/48950-tutorial-eine-unendliche-geschichte-raspberry-4b-und-usb-boot/?postID=453256#post453256)
