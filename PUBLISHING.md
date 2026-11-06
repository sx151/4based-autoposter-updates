# Release-Publishing (Publisher-Anleitung)

## Einmalige Einrichtung auf dem Windows-Publisher-PC

1. Quelle **v8.7.2 oder neuer** in einen neuen Ordner entpacken.
2. `UPDATEKANAL_STARTEN_WINDOWS.bat` ausführen und als Manifestadresse exakt eingeben:

   `https://raw.githubusercontent.com/sx151/4based-autoposter-updates/main/updates/stable.json`

3. Das Skript erzeugt den privaten Ed25519-Schlüssel lokal unter `%USERPROFILE%\.4based-publisher\release-signing.pem`. Sichere davon ein offline aufbewahrtes Backup. **Niemals weitergeben oder hochladen.**
4. `RELEASE_BUILD_WINDOWS.bat` ausführen und den erzeugten Installer aus `dist\installer` einmalig über die bestehende Installation installieren. Die neue App muss den öffentlichen Schlüssel und die feste Manifest-URL enthalten. Die alten Creator-Daten in `%LOCALAPPDATA%\4basedAutoPoster` bleiben bestehen.
5. Update- und Rückrollfunktion auf einem Windows-Testgerät prüfen, bevor das Update für Benutzer freigegeben wird.

## Jede folgende Version (Beispiel 8.7.3 nach 8.7.2)

1. Versionsangaben in `update_config.py`, `4basedAutoPoster.iss` und den Build-Skripten synchron erhöhen.
2. `RELEASE_BUILD_WINDOWS.bat` ausführen und die lokale EXE testen.
3. Über das GitHub-Webinterface in diesem Repository ein **Release** für diese Version erstellen, mit einem eindeutigen Tag (z. B. `v8.7.3`). Die gewünschte ZIP-Asset-URL muss bekannt sein.
4. Lokal `UPDATE_SIGNIEREN_WINDOWS.bat` ausführen und die **exakte HTTPS-URL** des später hochgeladenen Release-ZIPs eingeben. Das Skript erzeugt `signed_release\4basedAutoPoster-8.7.3.zip` und die signierte `signed_release\stable.json`.
5. Das **signierte ZIP** als GitHub Release Asset hochladen, Release veröffentlichen und sicherstellen, dass der URL-Download ohne GitHub-Anmeldung funktioniert.
6. **Erst danach** das signierte `stable.json` nach `updates/stable.json` in diesem Repo hochladen bzw. die Datei aktualisieren.
7. Auf einer vorhandenen, signaturfähigen Windows-Installation testen: Update gefunden, SHA-256/Signatur geprüft, Download, Neustart, Daten- und Installer-Erhalt, Rollback im Fehlerfall.

## Wichtig

- **Keine** unsignierte Platzhalter-`stable.json` veröffentlichen.
- **Keine** `release-signing.pem`, Datenbanken, Cookies, Sitzungen, Token, Logdateien oder persönliche Konfigurationen hochladen.
- Niemals nur das Manifest ohne das bereits erreichbare ZIP veröffentlichen.
- Ein öffentlicher GitHub-Kanal allein bedeutet **nicht**, dass die automatische Updatefunktion bereits aktiv ist.
- Der Ed25519-Schlüssel für App-Updates ersetzt keine separate Windows-Authenticode-Signierung.
