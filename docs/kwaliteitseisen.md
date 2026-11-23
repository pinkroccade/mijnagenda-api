# Kwaliteitseisen

Eisen aan de specificatie en het beheer ervan. Een implementatie begint pas als de spec aan deze eisen voldoet.

| # | Eis | Toets |
|---|---|---|
| K1 | De spec is een geldig OpenAPI 3.0-document zonder waarschuwingen. | CI: `oas3-validatie` |
| K2 | De spec voldoet aan de NL API Design Rules (versie in `mise.toml`) zonder fouten of waarschuwingen. | CI: `api-design-rules` |
| K3 | Elk element van het informatiemodel is gedekt of heeft een gedocumenteerde, onderbouwde afwijking. | Review, [`informatiemodel-conformiteit.md`](informatiemodel-conformiteit.md) |
| K4 | Elk voorlopig veld is gemarkeerd met `x-provisional` en verdwijnt daar pas na een expliciet besluit. | Review |
| K5 | Elke operatie heeft voorbeelden voor succes en voor elke foutrespons; voorbeelden bevatten geen echte persoonsgegevens (alleen `example.nl`). | Review |
| K6 | Foutresponses zijn `application/problem+json` met een stabiele `code`. | CI en review |
| K7 | Verplichte velden in de spec komen overeen met de kardinaliteit in het informatiemodel. | Review |
| K8 | Privacy: identificaties staan alleen in de request body; het loggen van de body is minimaal. | Review, [ADR 0001](adr/0001-client-credentials-security.md) |
| K9 | Wijzigingen verlopen via een PR. Een architectuurbesluit krijgt een ADR in `docs/adr/`. | Review |
| K10 | `info.version` volgt semantische versionering. Zolang er geen client is aangesloten geldt `0.x`. | Review |
| K11 | De documentatie (Redoc) is gepubliceerd en past bij de spec op `main`. | CI: `publiceer-documentatie` |
| K12 | Een mock volgt de spec en dekt de scenario's (lege lijst, fouten, periodegrenzen, elke vorm van afspraak). | CI (zodra de mock er is) |
| K13 | De spec noemt per open punt expliciet dat het open is, en verwijst naar het issue. | Review |
