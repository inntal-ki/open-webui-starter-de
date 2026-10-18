# Changelog

## 1.1.0 — 2026-10-18

Versionen und Lizenzen geprüft am 18.10.2026.

### Geändert
- **Feste Versionen statt beweglicher Tags:** Open WebUI `v0.12.3`
  (vorher `:main`), Ollama `0.40.6` (vorher `:latest`), LiteLLM `v1.105.1`
  (vorher `:main-stable`).
- **Open WebUI standardmäßig nur lokal erreichbar:** Port-Bindung an
  `127.0.0.1` (vorher alle Schnittstellen). Für den Zugriff aus dem LAN
  `WEBUI_BIND=0.0.0.0` setzen — besser hinter Reverse Proxy mit HTTPS.
- **Keine voreingestellte Cloud-Verbindung:** `ENABLE_OPENAI_API=false`.
  Ohne diese Einstellung trägt Open WebUI eine Verbindung zu
  `api.openai.com` ein. Das LiteLLM-Overlay schaltet die Verbindung zum
  eigenen Proxy ein.
- **Modelltabelle neu:** nur Modelle, die heute in der Ollama-Bibliothek
  stehen (Qwen 3.5/3.6, Gemma 4, gpt-oss, Mistral Small 3.2, BGE-M3), mit
  Download-Größe und Lizenz laut Modellkarte. Hinweis auf `cloud`-Varianten,
  die nicht lokal rechnen.
- **Lizenzangaben korrigiert:** Open WebUI steht seit 2025 unter der
  „Open WebUI License“ (BSD-3-Clause plus Branding-Klausel), nicht unter
  BSD-3-Clause bzw. Apache 2.0. Gemma 4 steht unter Apache 2.0.
- **„ohne US-Anbieter“ präzisiert:** keine Eingabe geht an einen
  Cloud-Anbieter — es geht um den Betriebsort, nicht um die Herkunft.
- `WEBUI_SECRET_KEY` und `LITELLM_MASTER_KEY` sind Pflicht; ohne sie bricht
  `docker compose` mit einer klaren Meldung ab.
- SECURITY.md: Hinweis auf 2FA entfernt (Open WebUI bringt keine eigene mit),
  Update-Weg für gepinnte Versionen, Kontakt auf inntal-ki.eu.
- Abschnitt „Brauchen Sie Hilfe bei der Einführung?“ entfernt.
- Prompts: echte Umlaute statt Ersatzschreibung („für“ statt „fuer“).

### Neu
- GitHub Action: `docker compose config` für alle Kombinationen, Prüfung auf
  bewegliche Image-Tags und auf die lokale Bindung.

## 1.0.0 — 2026-04-20

Erste Fassung.
