# Conformiteit met het informatiemodel

Toets van `mijnagenda-openapi.yaml` (`0.1.0-concept`) tegen het [informatiemodel MijnAgenda](https://vng-realisatie.github.io/MijnAgenda-Respec/)
(bron: `SIM-MijnAgenda.respec.html`). Stand 2026-11-23. Bij elke wijziging van model of spec opnieuw uitvoeren.

Legenda: ✅ gedekt, ⚠️ afwijkend, ❌ ontbreekt.

| Model | Kard. | Spec | |
|---|---|---|---|
| AGENDA-AFSPRAAK.Identificatie | 1 | `afspraakIdentificatie` (verplicht) | ✅ |
| AGENDA-AFSPRAAK.Onderwerp | 0..1 | `onderwerp` | ✅ |
| AGENDA-AFSPRAAK.Gepland aanvangsmoment | 1 | `geplandAanvangsmoment`, niet verplicht | ⚠️ |
| AGENDA-AFSPRAAK.Gepland eindmoment | 1 | `geplandEindmoment`, niet verplicht | ⚠️ |
| AGENDA-AFSPRAAK.Referentie | 0..1 | ontbreekt | ❌ |
| AGENDA-AFSPRAAK.Aanmeldkenmerk alfanumeriek, mobiel, QR-code | 0..1 | alle drie aanwezig | ✅ |
| Subtypen ONLINE, FYSIEKE, TELEFONISCHE AGENDA-AFSPRAAK | n.v.t. | één `locatie` met `type` (`fysiek`, `telefonisch`, `video`, `onbekend`) | ⚠️ "video" heet in het model "online"; `onbekend` bestaat niet |
| ONLINE AGENDA-AFSPRAAK.Online adres | 1 | `locatie.onlineAdres`, niet verplicht | ⚠️ |
| TELEFONISCHE AGENDA-AFSPRAAK.Telefoonnummer agenda-afspraak | 0..1 | ontbreekt | ❌ |
| FYSIEKE AGENDA-AFSPRAAK vindt plaats op LOCATIE | 0..1 | `locatie` | ✅ |
| LOCATIE.Naam | 1 | `locatie.naam`, niet verplicht | ⚠️ |
| LOCATIE.Adres | 0..1 | `locatie.bezoekadres` | ✅ (andere naam) |
| Adres gestructureerd niet conform BAG: regel 1 tot 3 | 0..1 | aanwezig | ✅ |
| Adres.Land | 0..1, referentielijst Land (BRP) | vrije tekst | ⚠️ |
| CONTACTINFORMATIE (naam 1, e-mailadres, telefoonnummer, adres) | 0..1 per afspraak | ontbreekt | ❌ |
| ACTOR (naam) | 0..1 per afspraak | ontbreekt | ❌ |
| ACTIVITEITSOORT (naam 1, aanduiding wat mee te nemen 0..1, markdown) | 0..* | `activiteiten[]`, `minItems: 1` | ⚠️ minimum wijkt af |
| ACTIVITEITSOORT OP AGENDA-AFSPRAAK.Aantal | 1 | `aantal` | ✅ |
| PARTIJ.Geverifieerd e-mailadres | 1 | `identificaties[type=email]`, niet gecontroleerd | ⚠️ zie [ADR 0001](adr/0001-client-credentials-security.md) |

## Buiten het model, wel in de spec

- Zoekverzoek met periodefilter (`van`, `tot`) en identificaties.
- Foutstructuur (RFC 7807) en rate limiting (`429`).

## Ontbreekt in model en spec

- Status van een afspraak (geannuleerd, verplaatst, afgerond).
- URL voor wijzigen of annuleren, en een terugkeer-URL.
- Paginering, sortering en totaal aantal.
