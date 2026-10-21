---
name: codex-second-opinion
description: Vraag OpenAI Codex om een onafhankelijke review of een tweede mening over code, een diff of een plan. Gebruik dit na grotere wijzigingen of als de gebruiker om een andere blik vraagt ("wat vindt Codex/ChatGPT ervan?").
---

# Tweede mening van Codex

Codex mag hier alleen lezen, niets aanpassen.

```bash
codex exec --sandbox read-only -o /tmp/codex-review.txt "$(cat <<'PROMPT'
Je bent een kritische reviewer met een frisse blik.
Onderwerp: <bijv. de huidige wijzigingen (`git diff`), bestand X, of dit plan: ...>
Zoek naar: bugs, randgevallen, security-problemen, en simpelere alternatieven.
Geef per punt: ernst (hoog/midden/laag), waar, waarom, en een voorstel.
Wees eerlijk: als iets goed is, zeg dat kort; verzin geen problemen.
PROMPT
)"
cat /tmp/codex-review.txt
```

Gebruik de uitkomst zo:
- Controleer elk punt zelf voordat je het overneemt. Codex kan zich ook vergissen.
- Laat de gebruiker zien waar Codex en jij het eens en oneens zijn, met jouw oordeel erbij.
- Voer alleen fixes door die de gebruiker wil, of die duidelijk kloppen en binnen de taak vallen.
