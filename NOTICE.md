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
| [Open-WebUI](https://github.com/open-webui/open-webui) | Chat-Oberfläche | BSD-3-Clause | github.com/open-webui/open-webui |
| [Ollama](https://ollama.com) | Modell-Runtime | MIT | github.com/ollama/ollama |
| [LiteLLM](https://www.litellm.ai/) | LLM-Proxy (optional) | MIT | github.com/BerriAI/litellm |

## Hinweis zu Modell-Lizenzen

Dieses Setup **lädt keine Modelle automatisch**. Welche Modelle der Betreiber
einsetzt, entscheidet der Betreiber — und muss deren Lizenzbedingungen
selbst einhalten. Eine Auswahl:

| Modell | Lizenz | Einschränkungen für kommerzielle Nutzung |
|--------|--------|-----------------------------------------|
| Qwen 2.5 / 3 | Apache 2.0 | Keine |
| Mistral (Base, Nemo) | Apache 2.0 | Keine |
| Llama 3.x | Llama Community License | Ja: ab 700 Mio. MAU eigene Lizenz von Meta nötig |
| Gemma | Gemma Terms of Use | Ja: eigene Bedingungen von Google |
| Phi | MIT | Keine |

**Prüfen Sie vor produktivem Einsatz die Lizenz des konkreten Modells.**
Ollama selbst prüft das nicht.

## Keine redistribuierte Software

Die eigentliche Software (Open-WebUI, Ollama, LiteLLM) wird **nicht** in
diesem Repository mitgeliefert. Docker pullt sie zur Installationszeit direkt
von den Upstream-Registries.
