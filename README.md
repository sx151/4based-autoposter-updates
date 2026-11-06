# 4based AutoPoster — offizieller Updatekanal

Dieses **öffentliche Repository** dient ausschließlich zur Verteilung signierter Updates der Windows-App „4based AutoPoster“. Es enthält **keinen** Quellcode der App, keine Creator-Daten, keine Passwörter, keine Cookies, keine Browserprofile und keinen privaten Signaturschlüssel.

## Status

**Updatekanal vorbereitet, aber noch nicht aktiviert.** Bis ein signiertes Release veröffentlicht ist, darf unter `updates/stable.json` kein erfundenes oder unsigniertes Update-Manifest bereitgestellt werden.

Feste Manifestadresse (sobald aktiv):

`https://raw.githubusercontent.com/sx151/4based-autoposter-updates/main/updates/stable.json`

## Sicherheit

- Jeder veröffentlichte Versionshinweis (`stable.json`) wird mit dem privaten Ed25519-Publisher-Schlüssel signiert; die Windows-App prüft ihn mit dem eingebauten öffentlichen Schlüssel.
- Der private Schlüssel wird ausschließlich auf dem Publisher-PC erzeugt und gespeichert, **niemals in diesem Repository**.
- Die App kontrolliert außerdem SHA-256 und Dateigröße des ZIP-Pakets.
- Release-ZIPs werden als **GitHub Release Assets** veröffentlicht. Nicht in das Git-Repository einchecken.
- Veröffentlichungsreihenfolge: **zuerst** ZIP hochladen und öffentlich prüfen, **danach** signiertes `updates/stable.json` veröffentlichen.
- Installierte v8.7.1-Apps haben noch keinen öffentlichen Prüfschlüssel. Deshalb ist **eine einmalige Neuinstallation** der mit Trust Anchor gebauten neueren Version erforderlich.

Details siehe [PUBLISHING.md](PUBLISHING.md).