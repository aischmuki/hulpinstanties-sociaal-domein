# Changelog

Alle noemenswaardige wijzigingen aan dit project worden hier bijgehouden.
Formaat gebaseerd op [Keep a Changelog](https://keepachangelog.com/nl/1.0.0/).
Versienummering via [Semantic Versioning](https://semver.org/lang/nl/).

---

## [1.1.1] — 2026-04-22

### Toegevoegd
- **LICENSE** — auteursrechtelijk beschermd onder Creative Commons BY-NC-ND 4.0
- **Copyright in footer** — © 2025 Schmuki BV met klikbare link naar de licentietekst

---

## [1.1.0] — 2026-04-15

### Toegevoegd
- **Netwerk-tab** met interactieve force-directed graph (D3.js v7)
  - 35 nodes — alle rollen uit de Rollen-tab plus ondersteunende instanties
  - 57 links — samenwerkingsrelaties gebaseerd op "Werkt samen met"-data
  - Nodegrootte schaalt op verbindingsgraad (hogere centraliteit = groter)
  - Klik op een node: markeert samenwerkingen in roze, toont detailpanel
  - Filter per ministerie: overige domeinen dimmen weg
  - Slepen van nodes en zoomen/pannen ondersteund
  - D3 wordt lazy geladen — alleen bij eerste bezoek aan het tabblad

### Technisch
- CSS-klassen toegevoegd voor graph-container en detailpanel (`#graph-wrap`, `#g-detail`)
- Graph-data in `_GN` (nodes) en `_GL` (links) arrays bovenaan het script-blok
- Lazy loader via dynamische `<script>`-tag

---

## [1.0.0] — 2026-04-15

### Toegevoegd
- **Instanties & domeinen** — 14 kaarten per beleidsdomein met betrokken rollen, wanneer betrokken en observatie
- **Individuele rollen** — 17 kaarten per professional met taken, samenwerkingen en observaties; doorzoekbaar
- **Tijdlijn fases** — 7-fasig model van multiproblematiek (signalering → nazorg), klikbare faseselector
- **Filterbalken** per ministerie (VWS, SZW, JenV, BZK, OCW, Financiën)
- Inzichtkaarten onderaan elke tab met strategische observaties
- Volledig responsief ontwerp (mobiel-vriendelijk)
- Ministerie-kleurcode legenda in de navigatiebalk

### Ontwerp
- Typografie: Cormorant Garamond (koppen) + DM Sans (tekst)
- Kleurpalet: warm gebroken wit met bordeauxrood accent
- CSS-variabelen voor ministerie-kleuren en basispalet
- Uitklapbare kaarten met animatie

---

## Methode & bronnen

### Inhoudsverantwoording

De inhoud is gebaseerd op:

- Nederlandse wetgeving: Wmo 2015, Jeugdwet, Participatiewet, Wet langdurige zorg (Wlz), Wet schuldsanering natuurlijke personen (WSNP)
- Beleidsdocumenten van VWS, SZW, JenV, BZK, OCW en Ministerie van Financiën
- Praktijkliteratuur over multiproblematiek en domeinoverstijgende samenwerking
- Praktijkervaring van Schmuki BV in het sociaal domein

### Keuzes in het datamodel

**Rollen vs. instanties:** het tool maakt onderscheid tussen *domeinen/instanties* (organisatorische eenheden) en *rollen* (individuele professionals). Een domein als "GGZ" bevat meerdere rollen; een rol als "Huisarts" valt binnen een domein maar werkt zelfstandig.

**Samenwerkingsrelaties in de graph:** relaties zijn opgenomen als er sprake is van structurele, directe samenwerking in de uitvoering. Indirecte relaties (bv. via wetgeving of financiering) zijn niet opgenomen. Elke relatie wordt één keer gedefinieerd.

**Fasering:** het 7-fasenmodel is een analytisch hulpmiddel, geen normatief protocol. In de praktijk bewegen mensen niet-lineair door fases, met name tussen fase 3 (crisis), 4 (stabilisatie) en 5 (herstel).

**Bewust niet uitputtend:** het tool richt zich op de meest voorkomende rollen bij complexe multiproblematiek. Specifieke doelgroepen (bv. dak- en thuislozen, ex-gedetineerden met ernstige psychiatrie) kunnen aanvullende rollen kennen die hier niet zijn opgenomen.
