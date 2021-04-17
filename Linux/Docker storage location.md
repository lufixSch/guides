# Speicherort von Docker Images ändern

Guide von [hier](https://evodify.com/change-docker-storage-location/)

## Config bearbeiten

Erstelle die Datei `/etc/docker/daemon.json` und füge folgenden Inhalt ein:

```json
{
  "data-root": "path/to/new/location"
}
```

Falls die Datei einen Element `"data-root"` beinhaltet kann der pfad dort überschrieben werden.

## Änderungen anwenden

Zuerst muss Docker neu gestartet werden

```bash
sudo systemctl restart docker
```

Als nächstes müssen alte Container von dem alten zum neuen Speicherort bewegt werde.
Dazu werden alle Container gelöscht:

```bash
docker system prune -a
```

Und wieder heruntergeladen werden:

```bash
docker pull <container-name>
```
