# Open-WebUI Starter DE

**Ein fertiges Docker-Compose-Setup für Open-WebUI + Ollama mit deutschen Defaults.**

In 15 Minuten eine lokale ChatGPT-Alternative auf Ihrer Hardware — ohne Cloud,
ohne US-Anbieter, mit sinnvollen Standard-Prompts für deutsche KMU.

## Was Sie bekommen

- **Open-WebUI** — moderne Chat-Oberfläche (vergleichbar ChatGPT)
- **Ollama** — Modell-Runtime für lokale LLMs
- **Optional LiteLLM-Proxy** — um zusätzlich externe APIs (z.B. Azure, Mistral) einzubinden
- **Prompt-Bibliothek** — 10 vorgefertigte Prompts für typische KMU-Aufgaben
- **Deutsche UI-Defaults** — Sprache, Datumsformat, Tonalität

## Voraussetzungen

- Linux-Server oder Workstation (Ubuntu 22.04+ empfohlen)
- Docker + Docker Compose v2
- **Für CPU-Betrieb:** 16 GB RAM (nutzbar für Modelle bis ~7B Parameter)
- **Für GPU-Betrieb:** NVIDIA-Karte ab 12 GB VRAM (RTX 3060 aufwärts) mit NVIDIA Container Toolkit
- Port 3000 (Open-WebUI) und 11434 (Ollama) frei

## Schnellstart

```bash
git clone https://github.com/inntal-ki/open-webui-starter-de.git
cd open-webui-starter-de
cp .env.example .env
# .env nach Bedarf anpassen (Hostname, Ports, Secret)
docker compose up -d
```

Browser öffnen: `http://localhost:3000`

Beim ersten Start legt Open-WebUI automatisch einen Admin-Account an — der
erste registrierte Nutzer wird Admin.

## Erstes Modell laden

Nach dem Start einmal ausführen:

```bash
docker compose exec ollama ollama pull qwen2.5:7b
```

Empfohlene Modelle für den Anfang (alle deutsch-fähig):

| Modell | Größe | VRAM/RAM | Eignung |
|--------|-------|----------|---------|
| `qwen2.5:7b` | 4.4 GB | ~8 GB | Allgemeine Aufgaben, guter Kompromiss |
| `qwen2.5:14b` | 9 GB | ~16 GB | Anspruchsvollere Texte |
| `llama3.3:70b` | 43 GB | 48 GB+ | Top-Qualität, nur mit großer GPU |
| `mistral-nemo:12b` | 7 GB | ~14 GB | Gut für strukturierte Ausgaben |
| `nomic-embed-text` | 274 MB | wenig | Embeddings für RAG-Funktion |

> **Hinweis zu Modell-Lizenzen:** Nicht alle Modelle sind kommerziell
> uneingeschränkt nutzbar. Llama hat eine eigene Community-Lizenz,
> Gemma eigene Terms of Use. Qwen, Mistral und Phi sind Apache 2.0 / MIT.
> Siehe [NOTICE.md](NOTICE.md) für Details.

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
- Rechnungs-Reminder in angemessenem Ton

Diese können Sie in Open-WebUI als "Custom Prompts" oder "Models" hinterlegen.

## Konfigurationsdateien

- [`docker-compose.yml`](docker-compose.yml) — Haupt-Compose
- [`docker-compose.gpu.yml`](docker-compose.gpu.yml) — Overlay für GPU-Support
- [`docker-compose.litellm.yml`](docker-compose.litellm.yml) — Overlay für LiteLLM-Proxy
- [`.env.example`](.env.example) — Alle Einstellungen mit Kommentaren
- [`prompts/`](prompts/) — Markdown-Dateien mit Prompt-Vorlagen

### Mit GPU starten
```bash
docker compose -f docker-compose.yml -f docker-compose.gpu.yml up -d
```

### Mit LiteLLM starten
```bash
docker compose -f docker-compose.yml -f docker-compose.litellm.yml up -d
```

## Sicherheit und Betrieb

- **Reverse Proxy:** Für Produktivbetrieb Open-WebUI hinter nginx/Caddy mit
  HTTPS betreiben. Nicht direkt Port 3000 freigeben.
- **Backup:** Volume `open-webui` enthält Benutzer, Chats, Einstellungen.
  Regelmäßig sichern.
- **Updates:** `docker compose pull && docker compose up -d` aktualisiert Images.

Siehe [`SECURITY.md`](SECURITY.md) für eine Hardening-Checkliste.

## Was dieses Repo **nicht** ist

- Kein fertiges Enterprise-Produkt — es ist ein Starter.
- Kein Ersatz für Anwaltskonsultation bei DSGVO-Fragen (siehe
  [dsgvo-ki-checkliste](https://github.com/inntal-ki/dsgvo-ki-checkliste)).
- Keine Produktions-Konfiguration für hohe Last — für >10 parallele Nutzer
  ist eine dedizierte Architektur nötig.

## Brauchen Sie Hilfe bei der Einführung?

Die Software ist kostenlos. Die Einführung in Ihrem Betrieb
(Hardware-Auswahl, Integration in bestehende Systeme, Schulung, laufender Support)
ist eine Dienstleistung von [Inntal-KI](https://inntal-ki.com).

## Lizenz

[MIT](LICENSE) — freie Nutzung auch kommerziell, keine Gewähr.

Open-WebUI und Ollama haben eigene Lizenzen (Apache 2.0 / MIT), die für
dieses Setup eingehalten werden.

---

Teil der [inntal-ki](https://github.com/inntal-ki) Open-Source-Familie.
