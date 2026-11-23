# MijnAgenda API

OpenAPI-specificatie voor het opvragen van agenda-afspraken van een inwoner bij een
afsprakensysteem (Afsprakenbeheercomponent), ten behoeve van de "mijnomgeving" van NL Portal
en de MijnAfspraken-service binnen de MijnServices-architectuur.

> **Status: concept (`0.1.0-concept`).** Het datamodel is nog in ontwikkeling; alleen
> `afspraakIdentificatie` is definitief. Er wordt nog niet tegen gebouwd. Zie [Open punten](#open-punten).

## Inhoud

- [`mijnagenda-openapi.yaml`](mijnagenda-openapi.yaml): de API-specificatie (OpenAPI 3.0.3).
- [`GLOSSARY.md`](GLOSSARY.md): domeinbegrippen.
- [`STANDARDS.md`](STANDARDS.md): welke standaarden zijn gebruikt en hoe getoetst.
- [`docs/informatiemodel-conformiteit.md`](docs/informatiemodel-conformiteit.md): per element van het informatiemodel of de spec het dekt.
- [`docs/patronen.md`](docs/patronen.md): gebruikspatronen (raadplegen, later wijzigen/annuleren).
- [`docs/kwaliteitseisen.md`](docs/kwaliteitseisen.md): kwaliteitseisen aan de spec en het beheer ervan.
- [`docs/adr/`](docs/adr/): architectuurbeslissingen.

## Herkomst en referenties

- **Informatiemodel (normatief):** [MijnAgenda-Respec](https://vng-realisatie.github.io/MijnAgenda-Respec/),
  broncode op [VNG-Realisatie/MijnAgenda-Respec](https://github.com/VNG-Realisatie/MijnAgenda-Respec).
  Deze API moet daaraan voldoen.
- **Conceptspec:** de OpenAPI-specificatie van 13 april 2026 (`0.1.0-concept`) is het uitgangspunt. De
  `info.contact` verwijst naar `github.com/camieleggermont/vng-mijnafspraken`; die repo is niet
  vindbaar. Deze repo is daarom de werkkopie. Zie het bijbehorende issue.
- **Gebruikscontext:** "MijnAfspraken: Algemeen afspraken" (Eerste Concept), zie [`docs/patronen.md`](docs/patronen.md).

## Validatie (CI)

Elke wijziging aan de spec wordt gevalideerd:

- [`oas3-validatie.yml`](.github/workflows/oas3-validatie.yml): geldig OpenAPI 3.0?
- [`api-design-rules.yml`](.github/workflows/api-design-rules.yml): voldoet het aan de
  [NL API Design Rules](https://developer.overheid.nl/kennisbank/api-ontwikkeling/standaarden/api-design-rules/)?
  Deze check is tijdelijk niet blokkerend: de conceptspec voldoet er nog niet aan (zie issues).
- [`publiceer-documentatie.yml`](.github/workflows/publiceer-documentatie.yml): Redoc-documentatie.

Tool- en standaardversies staan vast in [`mise.toml`](mise.toml); Renovate houdt ze bij.

```shell
mise run validate-all
```

## Open punten

De open punten staan als issues in deze repo. Ze moeten zijn uitgewerkt voordat een
implementatie (zoals in NL Portal) kan beginnen.

## Licentie

EUPL-1.2, zie [`LICENSE.md`](LICENSE.md).
