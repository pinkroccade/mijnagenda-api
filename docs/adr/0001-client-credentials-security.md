# 0001: OAuth2 Client Credentials (NL GOV profiel), identificatie op gevalideerd e-mailadres of telefoonnummer

## Status
Geaccepteerd (besluit opdrachtgever, 2026-11-23). De uitwerking per omgeving (token-endpoint, clientregistratie, mTLS) staat nog open, zie de issues.

## Context
De API wordt aangeroepen door een MijnOmgeving (zoals NL Portal). De eindgebruiker logt daar in; de Afsprakenbeheercomponent kent die gebruiker niet. Afspraken worden in het afsprakensysteem gemaakt op een unieke identificatie van de partij: een e-mailadres of telefoonnummer. BSN en KvK-nummer worden niet gebruikt. De API controleert niet of de meegestuurde identificatie van de eindgebruiker is.

## Beslissing
- De API gebruikt **OAuth2 Client Credentials** volgens het [NL GOV Assurance profile for OAuth 2.0 v1.1.0](https://gitdocumentatie.logius.nl/publicatie/api/oauth/v1.1.0/). Het token is een systeemtoken en bevat geen gebruikerscontext. Scope: `afspraken:lezen`.
- De identificatietypen voor de pilot zijn **e-mailadres en telefoonnummer**. BSN en KvK-nummer zijn uitgesloten. Daarom vallen ondernemers buiten de pilot.
- Het is een **implementatievereiste** dat alleen gevalideerde e-mailadressen en telefoonnummers als identificatie worden gebruikt. De consumerende partij is daar zelf verantwoordelijk voor.
- Het token endpoint, de clientregistratie en aanvullende transportmaatregelen (zoals mTLS) zijn deployment-specifiek en horen in een aansluitprofiel per omgeving.

## Consequenties
- De Afsprakenbeheercomponent kan niet nagaan of de aanvrager de rechtmatige eigenaar van de identificatie is. Dat vertrouwen ligt bij de consumer. Een gecompromitteerde consumer krijgt toegang tot de afspraken van elke identificatie.
- De spec kent alleen `email` als identificatietype. `telefoonnummer` moet nog worden toegevoegd (zie issue).
- Hoe de autorisatie van `GET /afspraken/{id}` door de Afsprakenbeheercomponent wordt afgedwongen is nog niet vastgesteld (zie issue).
- Een andere inzet, zoals rechtstreekse aanroep door minder vertrouwde partijen, vraagt om herziening richting user-delegation.
