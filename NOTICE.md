# NOTICE

Dieses Repository enthält eigene Konfigurations- und Dokumentationsdateien
unter [MIT-Lizenz](LICENSE).

Die Docker-Compose-Dateien **referenzieren** (pullen zur Laufzeit) fremde
Container-Images, redistribuieren jedoch keinen Fremdcode. Eine
Lizenzerhaltungspflicht für dieses Repository besteht daher nicht.

## Referenzierte Upstream-Projekte

Wir danken folgenden Projekten, auf denen dieses Setup aufbaut. Ihre Lizenzen
werden mit den jeweiligen Container-Images ausgeliefert.

| Projekt | Zweck | Lizenz | URL |
|---------|-------|--------|-----|
| [Open WebUI](https://github.com/open-webui/open-webui) | Chat-Oberfläche | Open WebUI License (BSD-3-Clause plus Branding-Klausel) | github.com/open-webui/open-webui |
| [Ollama](https://ollama.com) | Modell-Runtime | MIT | github.com/ollama/ollama |
| [LiteLLM](https://www.litellm.ai/) | LLM-Proxy (optional) | MIT (ohne den Enterprise-Ordner) | github.com/BerriAI/litellm |

**Open WebUI License:** Seit 2025 gilt für Open WebUI eine eigene Lizenz auf
Basis von BSD-3-Clause mit einer zusätzlichen Branding-Klausel: Bei mehr als
50 Endnutzern in 30 Tagen darf das „Open WebUI“-Branding (Name, Logo,
Kennzeichen) nicht entfernt oder ersetzt werden — außer mit schriftlicher
Erlaubnis oder Enterprise-Lizenz. Ältere Versionen unterliegen ihren
ursprünglichen Lizenzen (siehe `LICENSE_HISTORY` im Open-WebUI-Repository).
Geprüft am 18.10.2026 an der LICENSE-Datei von v0.12.3.

## Hinweis zu Modell-Lizenzen

Dieses Setup **lädt keine Modelle automatisch**. Welche Modelle der Betreiber
einsetzt, entscheidet der Betreiber — und muss deren Lizenzbedingungen
selbst einhalten. Eine Auswahl (Lizenz laut Modellkarte, geprüft 18.10.2026):

| Modell | Lizenz | Einschränkungen für kommerzielle Nutzung |
|--------|--------|-----------------------------------------|
| Qwen 3.5 / 3.6 | Apache 2.0 | Keine |
| Gemma 4 | Apache 2.0 | Keine (Gemma bis Version 3: eigene Gemma-Nutzungsbedingungen) |
| Mistral Small 3.2 | Apache 2.0 | Keine |
| gpt-oss | Apache 2.0 | Keine |
| BGE-M3 (Embeddings) | MIT | Keine |
| Llama 3.x / 4 | Llama Community License | Ja: u. a. eigene Lizenz von Meta ab 700 Mio. monatlich aktiven Nutzern |

**Prüfen Sie vor produktivem Einsatz die Lizenz des konkreten Modells.**
Ollama selbst prüft das nicht.

## Keine redistribuierte Software

Die eigentliche Software (Open WebUI, Ollama, LiteLLM) wird **nicht** in
diesem Repository mitgeliefert. Docker pullt sie zur Installationszeit direkt
von den Upstream-Registries.
