# Open WebUI Starter DE

**Ein fertiges Docker-Compose-Setup für Open WebUI + Ollama mit deutschen Vorgaben.**

[![Compose](https://github.com/inntal-ki/open-webui-starter-de/actions/workflows/compose.yml/badge.svg)](https://github.com/inntal-ki/open-webui-starter-de/actions/workflows/compose.yml)

**Stand:** Oktober 2026 · Version 1.1.0 · Open WebUI v0.12.3, Ollama 0.40.6 (geprüft am 18.10.2026)

Eine lokale Chat-Oberfläche auf Ihrer eigenen Hardware: Das Modell rechnet bei
Ihnen, **keine Eingabe geht an einen Cloud-Anbieter** — dazu Standard-Prompts
für typische Aufgaben in deutschsprachigen KMU.

## Was Sie bekommen

- **Open WebUI** — Chat-Oberfläche im Browser
- **Ollama** — Laufzeitumgebung für lokale Sprachmodelle
- **Optional LiteLLM-Proxy** — um weitere Modelle über eine OpenAI-kompatible Schnittstelle einzubinden
- **Prompt-Bibliothek** — 10 vorgefertigte Prompts für typische KMU-Aufgaben
- **Deutsche Vorgaben** — Oberfläche auf Deutsch, Registrierung nur durch den Admin, neue Nutzer müssen freigeschaltet werden
- **Feste Versionen** — alle Images gepinnt, keine beweglichen Tags wie `:latest`

## Voraussetzungen

- Linux-Server oder Workstation (Ubuntu 22.04+ empfohlen)
- Docker + Docker Compose v2
- **CPU-Betrieb:** 16 GB RAM für Modelle bis etwa 9B Parameter (langsam, aber brauchbar zum Ausprobieren)
- **GPU-Betrieb:** NVIDIA-Karte ab 12 GB VRAM mit NVIDIA Container Toolkit
- Ports 3000 (Open WebUI) und 11434 (Ollama) auf dem Host frei

## Schnellstart

```bash
git clone https://github.com/inntal-ki/open-webui-starter-de.git
cd open-webui-starter-de
cp .env.example .env
# In .env mindestens WEBUI_SECRET_KEY setzen: openssl rand -hex 32
docker compose up -d
```

Browser öffnen: `http://localhost:3000`

Beim ersten Aufruf legen Sie das Admin-Konto an — das erste Konto wird Admin.
Danach ist die Selbstregistrierung abgeschaltet (`ENABLE_SIGNUP=false`); weitere
Nutzer legt der Admin an.

Open WebUI ist in der Vorgabe nur auf diesem Rechner erreichbar (`127.0.0.1`).
Für den Zugriff aus dem Firmennetz `WEBUI_BIND=0.0.0.0` in `.env` setzen —
für den Dauerbetrieb besser einen Reverse Proxy mit HTTPS davorstellen
(siehe [`SECURITY.md`](SECURITY.md)).

## Erstes Modell laden

```bash
docker compose exec ollama ollama pull qwen3.5:9b
```

Eine Auswahl aus der Ollama-Bibliothek (Stand 18.10.2026; Lizenz laut
Modellkarte des Herstellers):

| Modell | Download | Speicher (Richtwert) | Lizenz | Eignung |
|--------|----------|----------------------|--------|---------|
| `qwen3.5:9b` | 6,6–7,6 GB | 12 GB VRAM / 16 GB RAM | Apache 2.0 | Einstieg, allgemeine Aufgaben |
| `gemma4:e4b` | 6,6–9,5 GB | 12 GB VRAM / 16 GB RAM | Apache 2.0 | Einstieg, Bilder als Eingabe |
| `gemma4:12b` | 7,7–8,0 GB | 12–16 GB VRAM | Apache 2.0 | Anspruchsvollere Texte |
| `gpt-oss:20b` | 14 GB | 16 GB VRAM | Apache 2.0 | Schrittweises Begründen |
| `mistral-small3.2:24b` | 15 GB | 24 GB VRAM | Apache 2.0 | Deutsch laut Modellkarte unterstützt, Bilder als Eingabe |
| `qwen3.6:35b` | 23–24 GB | 32 GB VRAM | Apache 2.0 | Größtes Modell der Auswahl, Mixture-of-Experts (3B aktiv) |
| `bge-m3` | 1,2 GB | wenig | MIT | Embeddings für Dokumente (RAG), mehrsprachig |

Der Richtwert ist die Dateigröße plus Reserve für den Gesprächskontext — bei
langen Dokumenten mehr. Wie gut ein Modell **Deutsch** schreibt, testen Sie am
besten mit eigenen Texten, bevor Sie sich festlegen.

> **Lizenzen:** Die Modelle oben stehen laut ihrer Modellkarte unter Apache 2.0
> bzw. MIT. Das gilt nicht für jede Familie: Llama hat eine eigene
> Community-Lizenz, ältere Gemma-Versionen (bis Gemma 3) eigene Nutzungsbedingungen.
> Prüfen Sie vor dem produktiven Einsatz die Lizenz des konkreten Modells —
> Ollama prüft das nicht. Siehe [NOTICE.md](NOTICE.md).

> **Achtung, Cloud-Modelle:** Die Ollama-Bibliothek enthält inzwischen auch
> Varianten mit `cloud` im Namen (z. B. `gpt-oss:20b-cloud`). Diese rechnen
> **nicht lokal**, sondern bei Ollama. Wer keine Daten aus dem Haus geben
> will, nutzt sie nicht.

## Prompt-Bibliothek

Im Ordner [`prompts/`](prompts/) finden Sie vorgefertigte Prompts für:

- Angebotstexte aus Stichpunkten erstellen
- Kundenmails höflich und präzise beantworten
- Protokolle aus Rohnotizen strukturieren
- Stellenausschreibungen entwerfen
- Produktbeschreibungen einheitlich formulieren
- LinkedIn-Posts aus Fachtexten destillieren
- Meetings zusammenfassen (mit vorab transkribiertem Text)
- Rechtliche Texte in Alltagssprache übersetzen
- Interne Dokumentation aus Code-Kommentaren
- Zahlungserinnerungen in angemessenem Ton

Diese können Sie in Open WebUI als „Prompts“ oder als eigene „Modelle“ mit
Systemprompt hinterlegen.

## Konfigurationsdateien

- [`docker-compose.yml`](docker-compose.yml) — Haupt-Compose
- [`docker-compose.gpu.yml`](docker-compose.gpu.yml) — Overlay für GPU-Betrieb
- [`docker-compose.litellm.yml`](docker-compose.litellm.yml) — Overlay für den LiteLLM-Proxy
- [`.env.example`](.env.example) — alle Einstellungen mit Kommentaren
- [`prompts/`](prompts/) — Markdown-Dateien mit Prompt-Vorlagen

### Mit GPU starten
```bash
docker compose -f docker-compose.yml -f docker-compose.gpu.yml up -d
```

### Mit LiteLLM starten
```bash
cp config/litellm.example.yaml config/litellm.yaml
# LITELLM_MASTER_KEY in .env setzen
docker compose -f docker-compose.yml -f docker-compose.litellm.yml up -d
```

Sobald Sie in `config/litellm.yaml` ein Cloud-Modell eintragen, verlassen
Anfragen an dieses Modell das Haus. Das kann eine bewusste Wahl sein — dann
aber als eigener, klar benannter Eintrag, nicht als stiller Ersatz für das
lokale Modell (siehe [dsgvo-ki-checkliste](https://github.com/inntal-ki/dsgvo-ki-checkliste),
Abschnitt 7).

## Sicherheit und Betrieb

- **Erreichbarkeit:** Vorgabe ist `127.0.0.1`. Für Produktivbetrieb Open WebUI
  hinter nginx/Caddy mit HTTPS betreiben, Port 3000 nicht direkt freigeben.
- **Backup:** Das Volume `open-webui` enthält Benutzer, Chats und Einstellungen.
  Regelmäßig sichern.
- **Updates:** Die Versionen stehen fest in den Compose-Dateien. Für ein Update
  die Image-Zeile ändern (Release Notes lesen), dann `docker compose pull` und
  `docker compose up -d`.

Siehe [`SECURITY.md`](SECURITY.md) für eine Hardening-Checkliste.

## Was dieses Repo **nicht** ist

- Kein fertiges Enterprise-Produkt — es ist ein Starter.
- Kein Ersatz für Anwaltskonsultation bei DSGVO-Fragen (siehe
  [dsgvo-ki-checkliste](https://github.com/inntal-ki/dsgvo-ki-checkliste)).
- Keine Konfiguration für hohe Last — für viele parallele Nutzer braucht es
  eine eigene Architektur.

## Lizenz

[MIT](LICENSE) — freie Nutzung auch kommerziell, keine Gewähr.

Open WebUI, Ollama und LiteLLM haben eigene Lizenzen — siehe [NOTICE.md](NOTICE.md).
Wichtig bei Open WebUI: Ab mehr als 50 Nutzern in 30 Tagen darf das
„Open WebUI“-Branding nicht entfernt oder ersetzt werden. Ein eigener
`WEBUI_NAME` wird deshalb als „KI-Assistent (Open WebUI)“ angezeigt.

---

Teil der [inntal-ki](https://github.com/inntal-ki) Open-Source-Familie — ein
persönliches, nicht kommerzielles Projekt · [inntal-ki.eu](https://inntal-ki.eu)
