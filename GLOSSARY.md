# Glossary: MijnAgenda API

Begrippen volgen waar mogelijk het [informatiemodel MijnAgenda](https://vng-realisatie.github.io/MijnAgenda-Respec/).

## Agenda-afspraak
Een gepland contactmoment waarop een gesproken interactie plaatsvindt tussen een burger, bedrijf of instelling en een overheidsorganisatie. Heeft een `afspraakIdentificatie`, een gepland aanvangs- en eindmoment en betreft een of meer activiteitsoorten. Het model kent drie vormen: online, fysiek en telefonisch.

## Afsprakenbeheercomponent
Het systeem dat de afspraken beheert en deze API aanbiedt. Per gemeente is er één afsprakensysteem; een converterlaag voor meerdere systemen valt buiten scope. Aanmaken, wijzigen en annuleren gebeurt in dat systeem zelf.

## MijnOmgeving
De omgeving waarin een ingelogde inwoner zijn afspraken ziet, bijvoorbeeld NL Portal. De MijnOmgeving is de consumer van deze API en verantwoordelijk voor de identiteit van de eindgebruiker.

## Partij
Persoon of organisatie met wie de gemeente een relatie heeft (klantinteractiemodel). Een agenda-afspraak heeft precies één partij, in het model geïdentificeerd via een geverifieerd e-mailadres.

## Identificatie
Een paar `type` en `waarde` waarmee een partij wordt opgezocht. Voor de pilot zijn dat het e-mailadres en het telefoonnummer. BSN en KvK-nummer worden niet gebruikt: afspraken worden op e-mailadres of telefoonnummer gemaakt.

## Gevalideerd e-mailadres of telefoonnummer
Een e-mailadres of telefoonnummer waarvan het eigendom door de consumer is aangetoond. Dit is een implementatievereiste: alleen gevalideerde gegevens mogen als identificatie worden gebruikt, en de implementerende partij is hier zelf verantwoordelijk voor. De API controleert het niet.

## Activiteitsoort
De soort activiteit waarvoor de klant een afspraak heeft (waar iemand voor komt), bijvoorbeeld paspoort verlengen. Heeft een naam en optioneel een aanduiding van wat de klant moet meenemen (markdown toegestaan). Op de afspraak staat per activiteitsoort een aantal.

## Locatie
De fysieke plek van een fysieke afspraak, met naam en adres. Niet per se het adres van de contactinformatie.

## Contactinformatie
Gegevens van de gemeente (naam, e-mailadres, telefoonnummer, adres) voor het managen van de afspraak, vaak van het gemeentehuis of stadsdeelkantoor. Zit in het model, nog niet in de spec.

## Aanmeldkenmerk
Het kenmerk waarmee de klant zich meldt voor de afspraak: alfanumeriek, QR-code of mobiel (wallet).

## Systeemtoken
Het OAuth2-token (client credentials) waarmee de MijnOmgeving de API aanroept. Bevat geen gebruikerscontext.

## Provisional (`x-provisional`)
Veld of schema dat nog niet definitief is vastgesteld en zonder aankondiging kan wijzigen.
