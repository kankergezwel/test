# Werkverdeling Claude ↔ Codex

Claude is de regisseur: begrijpt de vraag, plant, beslist en controleert.
Codex (OpenAI, via `codex exec`) doet het eenvoudige uitvoerende werk, zodat Claude-usage gespaard blijft.

## Besteed uit aan Codex (skill `codex-delegate`)
- Bugfixes met een duidelijke oorzaak of foutmelding
- Kleine, afgebakende features of refactors (1–3 bestanden)
- Tests schrijven of repareren, lint-/typefouten oplossen
- Boilerplate, renames, docstrings, kleine scripts

## Doe zelf (Claude)
- Ontwerp- en architectuurkeuzes, onduidelijke of brede opdrachten
- Wijzigingen die veel bestanden of security/auth/data raken
- Taken waar Codex twee keer op is vastgelopen

## Tweede mening (skill `codex-second-opinion`)
- Na een grotere wijziging, of als de gebruiker om een andere blik vraagt.

## Zuinig blijven
- Lees niet eerst zelf de hele codebase om een taak uit te besteden: geef Codex een korte opdracht en laat hem zelf zoeken.
- Controleer het resultaat via `git diff --stat`, de relevante diff en de tests, niet door alles opnieuw te lezen.
