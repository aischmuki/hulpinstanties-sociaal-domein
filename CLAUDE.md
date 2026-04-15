# CLAUDE.md — Hulpinstanties Sociaal Domein

Context voor AI-assistenten die aan dit project werken.

---

## Wat is dit project?

Een single-file HTML-tool (`index.html`) die het Nederlandse sociaal domein visualiseert: welke instanties en professionals bestaan er, wat doen ze, met wie werken ze samen, en in welke fase van multiproblematiek zijn ze actief.

Gebouwd voor en door Schmuki BV als kennistool voor consultancy en AI-toepassingen in het sociaal domein.

---

## Bestandsstructuur

```
index.html        # Alles — HTML, CSS en JS in één bestand
README.md         # Projectdocumentatie
CLAUDE.md         # Dit bestand
CHANGELOG.md      # Versiegeschiedenis
```

Er is geen build-stap, geen package manager, geen framework. Wijzigingen gaan direct in `index.html`.

---

## Architectuur van index.html

Het bestand is opgebouwd in drie blokken:

1. **`<style>`** — alle CSS, inclusief CSS-variabelen voor kleur en typografie
2. **HTML-body** — header, tabnav, filterbar, en vier tab-secties
3. **`<script>`** — alle JavaScript onderaan het bestand

### Tab-secties

| ID | Tabblad |
|----|---------|
| `#t-instanties` | Instanties & domeinen |
| `#t-rollen` | Individuele rollen |
| `#t-fases` | Tijdlijn fases |
| `#t-netwerk` | Netwerk (D3 graph) |

---

## Ontwerpsysteem

### CSS-variabelen

```css
--off: #f5f2ee     /* paginaachtergrond */
--warm: #faf8f5    /* kaartachtergrond */
--rose: #9b2a4a    /* primaire accentkleur */
--ink: #1e1418     /* donkerste tekst / graph-achtergrond */
--mu: #8a7078      /* muted tekst */
--bd: #ddd0d5      /* border */

/* ministerie-kleuren */
--vws: #9b2a4a  --szw: #2a5a7c  --jenv: #4a2a6a
--bzk: #2a6a4a  --ocw: #7c4a2a  --fin: #5a6a1a
```

### Ministerie-badges

```html
<span class="mt mv">VWS</span>      <!-- VWS -->
<span class="mt ms">SZW</span>      <!-- SZW -->
<span class="mt mj">JenV</span>     <!-- JenV -->
<span class="mt mb">BZK</span>      <!-- BZK -->
<span class="mt mo">OCW</span>      <!-- OCW -->
<span class="mt mf">Financiën</span><!-- Financiën -->
```

---

## Een kaart toevoegen (Instanties of Rollen)

Kopieer dit patroon en plak het in het juiste `<div class="grid" id="g-i">` of `<div class="grid" id="g-r">` blok:

```html
<div class="card" data-m="vws" data-rn="zoekwoord1 zoekwoord2" onclick="tc(this)">
  <div class="cb" style="background:var(--vws)"></div>
  <div class="ch">
    <div class="ctg">
      <div class="ct">Naam van de rol</div>
      <div class="cms"><span class="mt mv">VWS</span></div>
    </div>
    <div class="tog">+</div>
  </div>
  <div class="cp">Korte beschrijving — wat doet deze rol in één zin.</div>
  <div class="cbod">
    <div class="cs">
      <span class="cl">Wat doen zij?</span>
      <ul class="wl">
        <li>Taak één</li>
        <li>Taak twee</li>
      </ul>
    </div>
    <div class="cs">
      <span class="cl">Werkt samen met</span>
      <div class="rl">
        <span class="rc">Naam rol</span>
        <span class="rc">Naam rol</span>
      </div>
    </div>
    <div class="cs">
      <span class="cl">Observatie</span>
      <div class="ob">Praktijkobservatie in cursief.</div>
    </div>
  </div>
</div>
```

**Regels:**
- `data-m` bevat alle ministeries, spatie-gescheiden en lowercase (`"vws szw"`)
- `data-rn` bevat zoeksleutels voor de zoekfunctie (alleen nodig in `#g-r`)
- Bij meerdere ministeries: gradient kleurblok via `background:linear-gradient(90deg,var(--vws),var(--szw))`
- `data-rn` is niet nodig in `#g-i`

---

## Een node toevoegen aan de graph

### 1. Node toevoegen aan `_GN`

```js
{
  id: 'uniek-id',          // lowercase, koppeltekens, uniek
  label: 'Weergavenaam',
  m: ['vws'],              // array van ministerie-codes
  desc: 'Beschrijving.',   // optioneel, verschijnt in detail-panel
  obs: 'Observatie.'       // optioneel, verschijnt als citaatblok
}
```

### 2. Links toevoegen aan `_GL`

```js
{ source: 'uniek-id', target: 'bestaand-id' }
```

**Regels:**
- Elke relatie één keer opnemen (ongedirectioneerd)
- Alleen toevoegen als er een echte samenwerkingsrelatie is — niet speculeren
- `source` en `target` moeten bestaande node-IDs zijn

### Bestaande node-IDs

`wmo` `jeugdcons` `huisarts` `ambulant` `casemanager` `schuldhulp` `klantmanager` `werkcoach` `jeugdbesch` `veiligthuis` `verzarts` `pohggz` `clientond` `bewindv` `iber` `reclas` `raadslieden` `ggzbehand` `ggd` `politie` `veilhuis` `woningcorp` `ciz` `kinderrecht` `raadkb` `belasting` `uwv` `kredietbank` `jobcoach` `wgs` `bedrijfsarts` `kantonrecht` `smw` `leerplicht` `jeugdarts`

---

## Fasedescripties toevoegen of aanpassen

Fase-HTML staat in `#t-fases`. Elke fase heeft:

```html
<div class="php" id="p-N">
  <h3>Fase N — Naam</h3>
  <p>Beschrijving van de fase.</p>
  <div class="phm">
    <div><h4>Actieve domeinen</h4><ul><li>...</li></ul></div>
  </div>
  <span class="pht2">Kernspanning of interventiepunt</span>
</div>
```

En een bijbehorende knop in `.phg`:
```html
<div class="phi" onclick="tp(N,this)">
  <span class="phn">N</span>
  <span class="phnm">Naam</span>
</div>
```

---

## Inhoudelijke uitgangspunten

- **Bronnen:** gebaseerd op Nederlandse wetgeving (Wmo 2015, Jeugdwet, Participatiewet, Wlz), praktijkkennis en literatuur over multiproblematiek
- **Perspectief:** vanuit de inwoner met multiproblematiek — wie komt er in hun leven, wanneer en waarom
- **Toon:** zakelijk, observerend, niet normatief — observaties beschrijven de praktijk zoals die is, niet zoals die zou moeten zijn
- **Volledigheid:** bewust niet uitputtend — de nadruk ligt op de meest voorkomende rollen en relaties bij complexe multiproblematiek

---

## Wat je niet hoeft te doen

- Geen npm install, geen build
- Geen type-annotaties of JSDoc toevoegen
- Geen error handling voor onmogelijke situaties
- Niet refactoren wat niet gevraagd is — de minified CSS is bewust compact gehouden
