# Energieverbrauch eines Raspberry Pi's reduzieren

## Allgemein

| Maßname             | Reduzierter Strom |
| ------------------- | ----------------- |
| HDMI deaktivieren   | $25mA$            |
| USB deaktivieren    |                   |
| LEDs deaktivieren   | $5mA$ pro LED     |
| Zubehör reduzieren  | $>50mA$           |
| Software reduzieren | $>100mA$          |

## HDMI deaktivieren

Läuft der Raspberry Pi im headless Betrieb kann der HDMI Ausgang mit folgendem Befehl deaktiviert werden:

```shell
/usr/bin/tvservice -o
```

Mit der option `-p` kann der Port auch wieder aktiviert werden.

Um den HDMI Port beim starten des Raspberry Pi's zu deaktivieren, muss der Befehl in die Datei `/etc/rc.local` geschrieben werden

## USB deaktivieren

## LEDs deaktivieren

Um die verschiedenen LEDs am Raspberry Pi zu deaktivieren muss die Datei `/boot/config.txt` editiert werden. Die Befehle unterscheiden sich jedoch je nach Version.

### Raspberry Pi 2

Der Raspberry Pi 2 hat zwei LEDs: Die rote Power LED und die Grüne Act LED. Mit folgenden Befehlen können die LEDs deaktiviert werden:

```sh
# Disable the ACT LED.
dtparam=act_led_trigger=none
dtparam=act_led_activelow=off

# Disable the PWR LED.
dtparam=pwr_led_trigger=none
dtparam=pwr_led_activelow=off
```

### Raspberry Pi 3

### Raspberry Pi 4

```sh
# Disable 
#led1 => Power led red
#led0 => Stauts led green
$ echo none | sudo tee /sys/class/leds/led0/trigger
$ echo gpio | sudo tee /sys/class/leds/led1/trigger

#Enable
#led1 => Power led red
#led0 => Stauts led green
$ echo mmc0 | sudo tee /sys/class/leds/led0/trigger
$ echo input | sudo tee /sys/class/leds/led1/trigger

```

### Raspberry Pi Zero W

Der Raspberry Pi Zero besitzt nur eine LED, welche wie folgt deaktiviert werden kann:

```sh
# Disable the ACT LED on the Pi Zero.
dtparam=act_led_trigger=none
dtparam=act_led_activelow=on
```
