# Security-Checkliste

Hardening-Empfehlungen für den Produktiveinsatz.

## Netzwerk

- [ ] Open-WebUI **nicht** direkt auf Port 3000 ins Internet stellen
- [ ] Reverse Proxy (nginx, Caddy, Traefik) mit HTTPS davor
- [ ] Ollama-Port (11434) nur auf `127.0.0.1` binden (Default in diesem Setup)
- [ ] Firewall: eingehend nur 22, 80, 443 offen

## Authentifizierung

- [ ] `ENABLE_SIGNUP=false` (Default) — keine öffentliche Registrierung
- [ ] Admin-Account mit starkem Passwort + 2FA (in Open-WebUI aktivieren)
- [ ] Regelmäßige Überprüfung der Nutzerliste

## Secrets

- [ ] `WEBUI_SECRET_KEY` mit `openssl rand -hex 32` generieren, nicht Default belassen
- [ ] `.env` nicht ins Git-Repo committen (`.gitignore` prüfen)
- [ ] Bei Kompromittierung: Secret rotieren → alle Sessions werden ungültig

## Datensicherung

- [ ] Docker-Volumes `ollama` und `open-webui` regelmäßig sichern
- [ ] Backups verschlüsseln, Offsite-Kopie halten
- [ ] Restore-Verfahren mindestens einmal testen

## Betrieb

- [ ] Docker-Images regelmäßig aktualisieren (`docker compose pull && up -d`)
- [ ] Host-System (Kernel, Docker) patchen
- [ ] Log-Rotation für Container-Logs einrichten (journald / `max-size` in daemon.json)

## Compliance

- [ ] DSGVO-Checkliste durchgegangen (siehe [dsgvo-ki-checkliste](https://github.com/inntal-ki/dsgvo-ki-checkliste))
- [ ] Verarbeitungsverzeichnis ergänzt
- [ ] Nutzer geschult, was in die KI eingegeben werden darf

## Sicherheitslücken melden

Sicherheitsprobleme bitte **nicht** über öffentliche GitHub Issues melden,
sondern per E-Mail an **security@inntal-ki.com** mit Details zur
Reproduktion. Wir antworten innerhalb von 72 Stunden.
