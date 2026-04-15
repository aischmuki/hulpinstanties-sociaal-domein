# Hulpinstanties — Sociaal Domein

Interactief referentietool voor het Nederlandse sociaal domein. Bedoeld voor professionals, consultants en AI-tools die moeten begrijpen wie wat doet, wanneer ze betrokken zijn, en hoe het systeem samenhangt.

**Live:** [aischmuki.github.io/hulpinstanties-sociaal-domein](https://aischmuki.github.io/hulpinstanties-sociaal-domein)

---

## Inhoud

Het tool heeft vier tabbladen:

| Tab | Inhoud |
|-----|--------|
| **Instanties & domeinen** | Kaarten per beleidsdomein (VWS, SZW, JenV, BZK, OCW, Financiën) met betrokken rollen, wanneer ze worden ingeschakeld en een praktijkobservatie |
| **Individuele rollen** | Kaarten per professional — wat doen zij, met wie werken ze samen, wat is de praktijkspanning |
| **Tijdlijn fases** | 7-fasig model van multiproblematiek: van signalering via crisis en stabilisatie naar participatie en nazorg |
| **Netwerk** | Force-directed graph van alle 35 rollen en 57 samenwerkingsrelaties — filteerbaar per ministerie, klikbaar voor details |

---

## Gebruik

Dit is een **single-file HTML-app** — open `index.html` direct in een browser. Geen installatie, geen build-stap, geen server nodig.

```bash
open index.html
```

Of host het via GitHub Pages (root van de `main` branch).

---

## Datamodel

### Kaarten (Instanties & Rollen)

Elke kaart is een `<div class="card">` met:

- `data-m` — ministerie(s), spatie-gescheiden (bv. `"vws szw"`)
- `data-rn` — zoeksleutels voor de zoekfunctie (alleen Rollen-tab)
- Kleurblok bovenaan (`<div class="cb">`) met ministerie-kleur
- Uitklapbare body (`<div class="cbod">`) met rollen, wanneer betrokken en observatie

### Graph (Netwerk-tab)

De graph is gedefinieerd in twee JavaScript-arrays in `index.html`:

**`_GN`** — nodes (rollen/instanties):
```js
{ id: 'schuldhulp', label: 'Schuldhulpverlener', m: ['szw','fin'],
  desc: 'Korte beschrijving', obs: 'Praktijkobservatie' }
```

**`_GL`** — links (samenwerkingsrelaties):
```js
{ source: 'schuldhulp', target: 'bewindv' }
```

Links zijn ongedirectioneerd — elke relatie wordt één keer opgenomen.

---

## Ministerie-kleurcodes

| Ministerie | CSS-variabele | Kleur | Badge-class |
|-----------|---------------|-------|-------------|
| VWS | `--vws` | `#9b2a4a` | `.mv` |
| SZW | `--szw` | `#2a5a7c` | `.ms` |
| JenV | `--jenv` | `#4a2a6a` | `.mj` |
| BZK | `--bzk` | `#2a6a4a` | `.mb` |
| OCW | `--ocw` | `#7c4a2a` | `.mo` |
| Financiën | `--fin` | `#5a6a1a` | `.mf` |

---

## Technologie

- Vanilla HTML/CSS/JavaScript — geen framework, geen bundler
- [D3.js v7](https://d3js.org) voor de force-directed graph (lazy geladen via CDN)
- [Cormorant Garamond + DM Sans](https://fonts.google.com) via Google Fonts

---

## Bijdragen

Nieuwe rol of instantie toevoegen? Zie [CLAUDE.md](CLAUDE.md) voor de exacte datastructuur en conventies.
