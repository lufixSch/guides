# Flash Sonoff Device

## Schaltung

- 3,3V -> 3,3V
- GND -> GND
- RX -> TX
- TX -> RX

Widerstand von TX des Sonoff-Geräts zu 3,3V.

## Flashen

Flashen mit `esptool.py` mit folgendem Befehl:

```zsh
esptool.py --port <port> --baud 115200 write_flash 0x0000 <firmware>.bin
```
