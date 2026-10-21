---
name: codex-delegate
description: Besteed een eenvoudige codeertaak (bugfix, kleine feature, tests, lint/typefouten, refactor in 1-3 bestanden) uit aan OpenAI Codex via `codex exec`, om Claude-usage te sparen. Gebruik dit standaard voor zulke taken, of als de gebruiker zegt "laat Codex dit doen".
---

# Taak uitbesteden aan Codex

## 1. Schrijf een korte opdracht (geen codebase-onderzoek vooraf)
Alleen wat je al weet: doel, foutmelding/symptoom, vermoedelijke bestanden, hoe het te checken is.
Lees niet eerst zelf bestanden door om de opdracht "compleet" te maken: Codex zoekt zelf.

## 2. Draai Codex
```bash
git status --short   # noteer of er al wijzigingen waren
codex exec --full-auto -o /tmp/codex-last.txt "$(cat <<'PROMPT'
Taak: <wat er moet gebeuren>
Context: <foutmelding / symptoom / relevante bestanden>
Klaar als: <bijv. `npm test` slaagt, bug X reproduceert niet meer>
Regels: blijf binnen de taak, geen ongevraagde refactors, niet committen.
Eindig met een korte samenvatting: wat je hebt veranderd en hoe je het hebt getest.
PROMPT
)"
```
- `--full-auto` = Codex mag bestanden in deze map aanpassen en commando's draaien in zijn sandbox.
- Duurt het lang? Zet een ruime Bash-timeout (max. 10 min) of draai het op de achtergrond.
- Lukt het niet omdat `codex` ontbreekt of niet is ingelogd? Meld dat aan de gebruiker (`npm i -g @openai/codex` en `codex login`) en doe de taak niet stilletjes zelf.

## 3. Controleer zuinig
1. `cat /tmp/codex-last.txt`: de samenvatting van Codex
2. `git diff --stat`: raakt het alleen wat het moest raken?
3. Bekijk alleen de diff van de relevante bestanden.
4. Draai de tests of check uit "Klaar als".

## 4. Afronden
- Goed: meld kort aan de gebruiker wat Codex deed en dat jij het hebt gecontroleerd.
- Klein probleem: herstel het zelf of geef Codex één gerichte vervolgopdracht.
- Twee keer mislukt: stop met uitbesteden, zeg dat tegen de gebruiker en pak het zelf op.
