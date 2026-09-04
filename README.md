# schulrecht-content

Modul-Content für **Schulrecht Trainer AT** (Android, Kotlin+Compose, offline-first).

App lädt Inhalte batch-weise von hier via Raw-URL, kein App-Update nötig für neue Fragen.

- Basis: SchUG + LDG + Tiroler Schulorganisationsgesetz, Stand 04.09.2026
- Prinzip: **Immer Praxis-Fall, nie Paragrafen-Abfrage. § nur in Auflösung zum Nachlesen.**
- Typen: `single` (1 aus 4), `multiple` (5-6 Optionen, 2-3 richtig, Teilpunkte), `tf` (richtig/falsch, max. 10%, nur Mythen)
- Level pro Modul: `L1 Basis`, `L2 Handlung`, `L3 Experte`, je 8-10 Fragen

## Laden in der App

```
manifest: https://raw.githubusercontent.com/damessner/schulrecht-content/main/manifest.json
modul:    https://raw.githubusercontent.com/damessner/schulrecht-content/main/modules/<modul-id>/L1.json
```

`manifest.json` ist Single Source of Truth für Version + Dateipfade. App cacht alles in Room.

## Struktur

```
manifest.json
schema/question.schema.json
batches/batch-01-mvp.json ... batch-08.json
modules/<modul-id>/module.json
modules/<modul-id>/L1.json
modules/<modul-id>/L2.json
modules/<modul-id>/L3.json
```

`module.json`:
```json
{
  "id": "A14",
  "titel": "Prüfungen auf Verlangen",
  "saeule": "A-SchUG",
  "status": "fertig",
  "quelle": ["SchUG"],
  "levels": ["L1.json","L2.json","L3.json"]
}
```

Frage-Objekt (siehe `schema/question.schema.json`):
`id, modul_id, level, typ, schulart[], situation, optionen[], richtig[], pro_option_feedback[], aufloesung, hauptquelle, zusatzquellen[], stand`

## Batches

- Batch 01 MVP: A01, A08, A12, A13, A14, B22
- Batch 02-08: siehe `batches/*.json` + Plan in `SCHUG` Arbeitsordner

## Mitarbeit

1. Nur einen Batch auf einmal befüllen.
2. Jede Frage braucht Auflösung + Feedback pro Option + genau 1 Hauptquelle.
3. Kein § im Fragetext.
4. `stand` immer `04.09.2026` bis Novelle kommt.

Lern-App, keine Rechtsberatung.
