# Standaarden-toetsing: MijnAgenda API

Dit document legt vast tegen welke standaarden `mijnagenda-openapi.yaml` is getoetst, en hoe.
De structuur is gebaseerd op de TOGAF Standards Information Base (SIB), aangevuld met de velden
`Datum getoetst` en `Rationale` voor traceerbaarheid.

| Standaard | Versie | Status | Conformiteitstoets | Datum getoetst | Rationale |
|---|---|---|---|---|---|
| Informatiemodel MijnAgenda (VNG Realisatie) | [MijnAgenda-Respec](https://vng-realisatie.github.io/MijnAgenda-Respec/) | Verplicht (normatief) | Handmatige review, zie [`docs/informatiemodel-conformiteit.md`](docs/informatiemodel-conformiteit.md) | 2026-11-23 | De API moet het conceptuele informatiemodel volgen. Het model is MIM-compliant. |
| OpenAPI Specification | 3.0.3 | Verplicht | Automatisch, CI: `.github/workflows/oas3-validatie.yml` (`mise run validate-oas-spec`, Redocly CLI `lint`) | Elke CI-run | Machineleesbaar contract. De conceptspec noemt in de tekst 3.2.0; het bestand is 3.0.3 (open punt). |
| NL API Design Rules (Logius) | `ADR_VERSION` in [`mise.toml`](mise.toml) | Verplicht voor overheids-API's | Automatisch, CI: `.github/workflows/api-design-rules.yml` (`mise run validate-nl-api-design-rules`, DON Checker). **Voldoet nu niet**, zie hieronder. | 2026-11-23 | Aansluiting bij de Nederlandse API-strategie. De conceptspec noemt versie 2.1.0. |
| NL GOV Assurance profile for OAuth 2.0 | v1.1.0 | Verplicht | Handmatige review, zie [ADR 0001](docs/adr/0001-client-credentials-security.md) | 2026-11-23 | Client credentials (system-to-system), zonder gebruikerscontext. |
| RFC 7807 Problem Details | n.v.t. | Verplicht (via NL API Design Rules) | Handmatige review en ruleset-toets | 2026-11-23 | Uniforme foutafhandeling met `application/problem+json`. |
| Digikoppeling REST-API | 3.0.1 | Indien van toepassing | Niet getoetst | nog niet | De conceptspec noemt het als optioneel per inzet. |

## Bekende afwijkingen (stand 2026-11-23)

De DON Checker (`adr@2.2.0`) geeft drie fouten op de conceptspec (`info.contact` en twee keer de versieheader), Redocly-lint geeft één waarschuwing (`info.license`):

- `info.contact` mist het veld `email` (naam en url zijn aanwezig).
- Beide `200`-responses missen de response-header met het volledige versienummer (`API-Version`) (twee fouten).
- `info.license` mist een `url` (waarschuwing van Redocly).

Deze zijn als issue vastgelegd. Tot ze zijn opgelost is de design-rules-workflow niet blokkerend.

## Workflows

| Workflow | Doel | Tool |
|---|---|---|
| `.github/workflows/oas3-validatie.yml` | Is de spec een geldig OpenAPI 3.0-document? | [Redocly CLI](https://redocly.com/docs/cli/) (`lint`) |
| `.github/workflows/api-design-rules.yml` | Voldoet de spec aan de NL API Design Rules? Faalt ook op waarschuwingen. | [DON Checker](https://developer.overheid.nl/kennisbank/api-ontwikkeling/tools/api-design-rules-linter) |
| `.github/workflows/publiceer-documentatie.yml` | Publiceert de Redoc-documentatie naar GitHub Pages. | Redocly CLI (`build-docs`) |

### Versiebeheer van tools en standaarden

- Alle versies staan vastgepind in [`mise.toml`](mise.toml); lokaal en in CI gelden dezelfde taken.
- [Renovate](renovate.json) opent wekelijks een PR voor nieuwe tool- en regelversies. Minor en patch
  mergen automatisch bij groene checks; major handmatig. Renovate wijzigt nooit de spec zelf.

## Open punten

- De NL API Design Rules linter dekt niet 100% van de regels af; een periodieke handmatige steekproef blijft aan te raden.
- Het informatiemodel is zelf nog een concept; de conformiteitstoets moet bij elke modelwijziging opnieuw.
