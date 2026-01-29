# Financiële planningstool (NL)

Dit project is een **client-side financiële planningstool** (React + Tailwind via CDN) die je direct kunt hosten via **GitHub Pages**. Geen build‑stappen, geen terminal, geen imports — alles draait in één `index.html`.

De tool is ontworpen als **leerbaar én uitbreidbaar fundament** voor FIRE‑planning, met focus op Nederland.

---

## Architectuur in het kort

* **Single-page app** (`index.html`)
* **React 18 (UMD via CDN)**
* **Tailwind CSS (CDN)**
* **Pure functies** voor alle financiële berekeningen
* Geen backend, geen opslag (bewust)

---

## Overzicht van alle stappen (1 t/m 21)

Onderstaand overzicht laat zien **waar elke besproken stap inhoudelijk terugkomt in de code**. Niet elke stap is een aparte functie — sommige zijn samengevoegd om de code robuust en begrijpelijk te houden.

---

## 🧠 Core engine & berekeningen

### Stap 1 — NL inkomstenbelasting (vereenvoudigd)

**Bestand:** `index.html`

Functie:

* `calculateIncomeTaxNL`

Wat doet dit:

* Box 1 belasting (2 schijven)
* Algemene heffingskorting
* Arbeidskorting
* Ondersteunt `single` en `fiscal-partner` (verzamelinkomen)

> ⚠️ Indicatief model, geen volledige fiscale simulatie

---

### Stap 2 — Toeslagen (vereenvoudigd)

Functie:

* `calculateToeslagen`

Inbegrepen:

* Kinderbijslag
* Kindgebonden budget
* Afbouw op basis van inkomen
* Rekening houdend met huishoudenstype

---

### Stap 3 — Financial engine (cashflow)

Functie:

* `calculateAnnualCashflow`

Logica:

* Filtert actieve inkomens en uitgaven
* Past groei (inkomen) en inflatie (uitgaven) toe
* Bruto → belasting → toeslagen → netto
* Berekent jaarlijkse besparing

👉 **Alle KPI’s komen hieruit voort**

---

### Stap 4 — Vermogensprojectie

Functie:

* `projectNetWorth`

Wat gebeurt hier:

* Iteratieve opbouw van vermogen
* Jaarlijks rendement
* Jaarlijkse besparing toegevoegd
* 50‑jaars tijdlijn

---

### Stap 5 — FIRE‑doel en KPI’s

Functies:

* `findFireYear`
* `monthlySavingsFromCashflow`
* `calculateFireTargetFromExpenses`

Logica:

* FIRE‑doel o.b.v. uitgaven en SWR
* FIRE‑jaar bepalen
* Maandelijks saldo

---

## 📊 Visualisatie & UX

### Stap 6–10 — Vermogensgrafiek & KPI‑presentatie

Component:

* `NetWorthChart`

Kenmerken:

* SVG‑grafiek
* Projectie vs FIRE‑doel
* Volledig client‑side

---

## 👨‍👩‍👧 Huishouden & persoonlijke situatie

### Stap 11 — Huishoudenstype

State:

* `householdType`

Opties:

* `single`
* `fiscal-partner`

Wordt gebruikt in:

* Belasting
* Toeslagen
* Verzamelinkomen

---

### Stap 12 — Verzamelinkomen

Ingebouwd in:

* `calculateIncomeTaxNL`
* `calculateToeslagen`

Bij fiscaal partner:

* inkomens worden samengenomen

---

### Stap 13 — FIRE via SWR

Functie:

* `calculateFireTargetFromExpenses`

Berekening:

```
FIRE-doel = jaarlijkse uitgaven / SWR
```

---

### Stap 14 — Kinderen

State:

* `childrenCount`

Gebruik:

* Toeslagenberekening
* Scenario‑impact

---

### Stap 15 — Toeslagen in cashflow

Geïntegreerd in:

* `calculateAnnualCashflow`

Effect:

* Verhoogt netto inkomen
* Beïnvloedt spaargeld en FIRE‑jaar

---

## 🇳🇱 Nederlandse details

### Stap 16a–c — Belastingdetails

In `calculateIncomeTaxNL`:

* Schijven
* Algemene heffingskorting
* Arbeidskorting

---

### Stap 17 — Toeslagenmodel

Functie:

* `calculateToeslagen`

---

### Stap 18 — Kinderen UI

State + input in `App`

---

### Stap 19 — Huishouden UI

Selectie in `App`

---

### Stap 20 — Verzamelinkomen logica

Automatisch toegepast bij:

* belasting
* toeslagen

---

### Stap 21 — Netto → cashflow → vermogen

De volledige keten:

```
Inkomen → belasting → toeslagen → cashflow → vermogen → FIRE
```

Geïmplementeerd via:

* `calculateAnnualCashflow`
* `projectNetWorth`

---

## Bewuste ontwerpkeuzes

* ❌ Geen backend
* ❌ Geen opslag (nog)
* ❌ Geen ES modules
* ✅ Alles transparant en aanpasbaar
* ✅ GitHub Pages‑proof

---

## Volgende uitbreidingen (suggesties)

1. Meerdere inkomens & uitgaven bewerkbaar maken
2. Hypotheek (annuïtair / lineair)
3. CSV‑export
4. Scenariovergelijking
5. Gedetailleerdere NL fiscaliteit

---

## Disclaimer

Dit is **geen financieel advies**. Alle berekeningen zijn indicatief en bedoeld voor inzicht en educatie.

---

💙 Gemaakt als leerbaar fundament voor FIRE & financiële planning in NL.
