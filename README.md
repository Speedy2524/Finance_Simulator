# 🏦 3-Töpfe Ruhestands- & Entnahme-Simulator

> **Interaktiver, browserbasierter Ruhestands- und Entnahme-Simulator nach der bewährten 3-Töpfe-Strategie (Tagesgeld, Festgeld-Treppe, Aktien-ETF) mit Monte-Carlo-Simulation, Guyton-Klinger-Leitplanken und historischen Makro-Stresstests.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![HTML5 / Single File](https://img.shields.io/badge/Architecture-Single--File%20Standalone-orange.svg)](index.html)
[![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-v3%20CDN-38bdf8.svg)](https://tailwindcss.com/)
[![Chart.js](https://img.shields.io/badge/Chart.js-v4-ff6384.svg)](https://www.chartjs.org/)
[![GitHub Pages Ready](https://img.shields.io/badge/GitHub%20Pages-Ready-brightgreen.svg)]()

---

## 📖 Inhaltsverzeichnis
- [Überblick & Philosophie](#-überblick--philosophie)
- [Die 3-Töpfe-Strategie im Detail](#-die-3-töpfe-strategie-im-detail)
- [Hauptfunktionen](#-hauptfunktionen)
  - [1. Basis-Planung & Ansparphase](#1-basis-planung--ansparphase)
  - [2. Flexible Festgeld-Treppe](#2-flexible-festgeld-treppe)
  - [3. Monte-Carlo-Simulation & Fat Tails](#3-monte-carlo-simulation--fat-tails)
  - [4. Historische Makro-Stresstests](#4-historische-makro-stresstests)
  - [5. Dynamische Entnahmeregeln (Guyton-Klinger & %-Entnahme)](#5-dynamische-entnahmeregeln-guyton-klinger---entnahme)
  - [6. Konfigurierbare Rebalancing-Strategien](#6-konfigurierbare-rebalancing-strategien)
  - [7. URL-Hash State Serialization & CSV-Export](#7-url-hash-state-serialization--csv-export)
- [Schnellstart & Verwendung](#-schnellstart--verwendung)
- [Mathematische & Modelltheoretische Grundlagen](#-mathematische--modelltheoretische-grundlagen)
- [Technologie-Stack & Architektur](#-technologie-stack--architektur)
- [Rechtlicher Hinweis (Disclaimer)](#-rechtlicher-hinweis-disclaimer)
- [Lizenz](#-lizenz)

---

## 🎯 Überblick & Philosophie

Das größte finanzielle Risiko im Ruhestand ist das sogenannte **Sequence-of-Returns-Risk (Reihenfolgerisiko)**: Wer zu Beginn der Entnahmephase einen schweren Börsencrash erlebt und gezwungen ist, Aktienfonds mit hohem Verlust zur Deckung des Lebensunterhalts zu verkaufen, reduziert den Zinseszins-Bestand irreversibel und riskiert eine vorzeitige Pleite.

Der **3-Töpfe Ruhestands-Simulator** demonstriert visuell und mathematisch fundiert, wie eine strukturierte Vermögensaufteilung den Ruhestand absichert:
1. **Pufferwirkung:** Tagesgeld und eine rollierende Festgeld-Treppe sichern den Konsumbedarf für 3 bis 7 Jahre ab.
2. **Keine Panikverkäufe:** Während eines Bärenmarkts werden Entnahmen rein aus den risikoarmen Töpfen gedeckt – der Aktien-ETF erhält die Zeit, sich vollkommen ohne Notverkäufe zu erholen.
3. **Didaktische Klarheit:** Entwickelt, um komplexe Finanzkonzepte für das Gespräch mit Angehörigen oder Mandanten verständlich, interaktiv und transparent aufzubereiten.

---

## 🏺 Die 3-Töpfe-Strategie im Detail

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        GESAMTVERMÖGEN (Portfolio)                      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
       ┌────────────────────────────┼────────────────────────────┐
       ▼                            ▼                            ▼
┌───────────────┐            ┌───────────────┐            ┌───────────────┐
│    TOPF 1     │            │    TOPF 2     │            │    TOPF 3     │
│   Tagesgeld   │            │Festgeld-Treppe│            │  Aktien-ETF   │
├───────────────┤            ├───────────────┤            ├───────────────┤
│ • 12–36 Mon.  │            │ • 3–7 Tranchen│            │ • Welt-Aktien │
│ • (Oder Fix-€)│ ◄───────── │ • Fälligkeit  │ ◄───────── │ • Renditemotor│
│ • Sofortabruf │            │   rollierend  │            │ • "ETF-Ernte" │
└───────┬───────┘            └───────────────┘            └───────────────┘
        │
        ▼  (Monatliche Entnahme / Konsum)
   [Lebensunterhalt]
```

* **🟦 Topf 1: Tagesgeld (Sofortliquidität & Puffer):** Hält die Lebenshaltungskosten für 6 bis 36 Monate flüssig (alternativ als fester Mindest-Euro-Betrag konfigurierbar). Von hier aus fließen die monatlichen Konsumentnahmen.
* **🟩 Topf 2: Festgeld-Treppe (Laufzeitenpuffer):** Besteht aus mehreren gestaffelten Festgeldkonten (z. B. 1, 2, 3 Jahre Laufzeit). Jährlich wird ein Konto fällig, refinanziert Topf 1 und rolliert für die volle Laufzeit weiter.
* **🟪 Topf 3: Aktien-ETF (Rendite & Zinseszins-Motor):** Investiert in breit diversifizierte Welt-ETFs (z. B. MSCI World / FTSE All-World). Nur bei positiver Marktentwicklung werden hier Gewinne realisiert ("ETF-Ernte"), um die vorderen Töpfe wieder aufzufüllen.

---

## 🚀 Hauptfunktionen

### 1. Basis-Planung & Ansparphase
- **Individuelle Parameter:** Startkapital, monatliche Wunsch-Entnahme, Inflationsrate, Einstiegsalter und Zeithorizont (bis 50 Jahre).
- **Flexible Ansparphase (0–25 Jahre):** Ermöglicht die Simulation einer vorgeschalteten Vermögensaufbauphase.
- **Topf-Aufteilung direkt ab Tag 1:** Das Startkapital wird auf Wunsch sofort auf Tagesgeld, Festgeld und ETF aufgeteilt – die Puffer- und Rollier-Logik greift so risikominimierend bereits während einer vorgeschalteten Ansparphase.
- **Fester Mindest-Puffer in Euro:** Topf 1 kann neben dem Faktor "Monatsausgaben" alternativ auch durch einen harten Euro-Boden fixiert werden.
- **Monatlicher ETF-Sparplan (0–3.000 €/Monat):** Zusätzliche Sparraten fließen während der Ansparphase direkt in Topf 3.
- **Automatische Inflations-Projektion:** Die Entnahmehöhe zum Rentenbeginn wird exakt auf Basis der kumulierten Inflation vorausberechnet.

### 2. Flexible Festgeld-Treppe
- **Gewichtung statt %-Zwang:** Der gesamte Topf 2 sowie einzelne Festgeld-Tranchen können wahlweise über Prozente oder durch direkte Eingabe exakter Euro-Werte gegeneinander gewichtet werden.
- **Beliebige Kontenanzahl:** Dynamisches Hinzufügen und Entfernen von Festgeldkonten.
- **Individuelle Laufzeiten & Zinssätze:** Jede Tranche kann mit einer eigenen Laufzeit (1–10 Jahre) und individuellem Zinssatz (0–10 % p.a.) hinterlegt werden.
- **1-Klick Gleichverteilung:** Schaltfläche zum sofortigen, exakten Aufteilen der Anteile auf alle Konten.
- **Strafzins-Simulation:** Sollte in Extremkrisen ein Festgeld vorzeitig gebrochen werden müssen, berechnet der Simulator realitätsnah 50 % Zinsabzug für das laufende Jahr.

### 3. Monte-Carlo-Simulation & Fat Tails
- **Bis zu 25.000 Pfade:** Hochoptimierte stochastische Pfadsimulation über TypedArrays (`Float64Array`) – 1.000 Pfade über 30 Jahre in unter 15 ms!
- **Leptokurtische Fat-Tails (Student-t mit $\nu=5$):** Realistische Modellierung extremer Marktereignisse (Kurtosis 9, normiert auf Einheitsvarianz 1) als überlegene Alternative zur klassischen Gauß-/Lognormal-Verteilung.
- **Konfidenzbänder (P10 & P90):** Grafische Darstellung des optimistischen (90. Perzentil) und pessimistischen Verlaufs (10. Perzentil) mit transparent schattiertem Konfidenzband.
- **Erfolgswahrscheinlichkeit:** Exakte Solvenzquote des Portfolios über den gesamten Ruhestandshorizont.
- **Deterministischer Mulberry32 PRNG:** Einstellbarer Seed (z. B. Seed 42 für wiederholbare Beratungsgespräche) oder echter Zufall.

### 4. Historische Makro-Stresstests
Auf Knopfdruck simulierbare Marktkrisen zum Härtetest der Strategie:
- 💥 **Finanzkrise 2008:** -38 % in Jahr 1, gefolgt von stufenweiser Erholung (+26 %, +15 %, +12 %).
- 📉 **Dot-Com-Blase 2000–2002:** 3-jährige Baisse (-15 %, -20 %, -25 % in Folge).
- ⚡ **Früher Marktschock:** -30 % in Jahr 1, -15 % in Jahr 2.
- 🗾 **Japan-Szenario (Verlorene Dekade):** 15 Jahre Stagnation & Deflation (0,5 % Inflation) – testet, was passiert, wenn der ETF-Rebound ausbleibt.
- ⛽ **Stagflation der 1970er:** Zweistellige Inflation (bis 11 %) bei gleichzeitig fallenden Aktienkursen.
- 🏛️ **Systemische Krise mit Zinssturz:** -45 % Börseneinbruch gekoppelt an ein 6-jähriges Nullzinsumfeld (Tagesgeld auf 0,25 %, Festgeld-Neuabschlüsse auf 0,5 %).
- ⚙️ **Benutzerdefinierter Schock:** Beliebiges Crash-Jahr (1–20) und Verlust (-10 % bis -70 %).

### 5. Dynamische Entnahmeregeln (Guyton-Klinger & %-Entnahme)
- **Feste Entnahme + Inflation (Standard):** Der klassische Entnahmeplan (Bengen / 4%-Regel).
- **Guyton-Klinger Guardrails:**
  - *Kapitalerhalt-Regel:* Steigt die Entnahmerate krisenbedingt um > 20 % über das Ausgangsniveau, wird die jährliche Inflationsanpassung eingefroren. Bei > 35 % Übersteigung greift eine Entnahmekürzung um 10 %.
  - *Wohlstands-Regel:* Sinkt die Entnahmerate in Boom-Phasen um > 20 % unter den Startwert, wird die Entnahme um 10 % für Konsum/Reisen erhöht.
  - *Sicherheits-Leitplanken:* Fester Floor (min. 80 %) und Cap (max. 150 % der Startentnahme).
- **Prozentuale Entnahme (% des Restdepots):** Jährliche Entnahme von z. B. 4 % des jeweiligen Gesamtwertes mit monatlicher Untergrenze (Floor) und Obergrenze (Cap).

### 6. Konfigurierbare Rebalancing-Strategien
- **Jährliche Kaskade (Standard):** Auffüllen von Topf 1 aus Festgeld; Defizite werden durch ETF-Gewinne ausgeglichen.
- **Schwellenwert-Baisse-Schutz (Verkaufsstopp Topf 3):** Bei negativer ETF-Jahresrendite ($r_3 < 0$) wird der Verkauf von ETF-Anteilen strikt verboten. Der Lebensunterhalt wird voll von Topf 1 und Topf 2 getragen.
- **Risiko-Gleitpfad (Glidepath):** Ab Alter 70 sinkt die ETF-Zielquote automatisch um 0,5 % p.a. zugunsten sicherer Festgelder, um das Langlebigkeitsrisiko zu reduzieren.

### 7. URL-Hash State Serialization & CSV-Export
- **Teilbare Links (v3 URL Hash):** Sämtliche Eingaben, Festgeldkonten und Experten-Optionen werden vollautomatisch im URL-Hash kodiert. Der Link kann kopiert, als Lesezeichen gespeichert oder versendet werden.
- **1-Klick-CSV-Export:** Exportiert die vollständige Jahrestabelle inklusive aller 3 Töpfe, Entnahmen, Altersangaben und Ereignis-Tags für Microsoft Excel, Apple Numbers oder Python/Pandas.

---

## 💻 Schnellstart & Verwendung

Der Simulator benötigt **weder Installation noch Build-Schritte, Node.js oder Webserver**.

### Lokale Nutzung:
1. Repository klonen oder als ZIP herunterladen:
   ```bash
   git clone https://github.com/DEIN_BENUTZERNAME/3-toepfe-ruhestands-simulator.git
   ```
2. Datei `index.html` per Doppelklick in einem beliebigen modernen Webbrowser (Chrome, Firefox, Safari, Edge) öffnen.

### GitHub Pages oder Coolify (Auto-Deployment):
1. Repository zu GitHub pushen (Achte darauf, dass die Datei **`index.html`** heißt).
2. **Über GitHub Pages:** In den Repository-Einstellungen auf **Settings ➔ Pages** gehen, Branch `main` auswählen und auf **Save** klicken.
3. **Über Coolify:** Neues Git-Repository anlegen, Build-Pack `Static` auswählen, Build-Commands leeren, auf *Deploy* klicken und den Webhook aktivieren.

---

## 📐 Mathematische & Modelltheoretische Grundlagen

### 1. Zinseszins & monatliche Entnahmekaskade
Für jedes Simulationsjahr $y$ wird das Portfolio zeitdiszipliniert berechnet:
$$W_y = \text{Topf 1}_y + \sum \text{Topf 2}_{i,y} + \text{Topf 3}_y$$

Die Zinsberechnung auf das Tagesgeld (Topf 1) berücksichtigt unterjährige Entnahmen über den durchschnittlichen Kassenbestand:
$$\text{Topf 1}_{\text{avg}} = \max\left(0, \, \text{Topf 1}_{\text{start}} - \frac{1}{2} W_1\right)$$

### 2. Monte-Carlo Fat Tails (Student-t)
Aktienrenditen weisen in der Realität signifikant stärkere Extremereignisse (Leptokurtosis) auf als eine Normalverteilung. Der Simulator transformiert Chi-Quadrat-gewichtete Normalzufallsvariablen in eine Student-t-Verteilung mit $\nu = 5$ Freiheitsgraden (Kurtosis = 9):

$$Z_{\text{raw}} = \frac{Z_0}{\sqrt{\frac{1}{5} \sum_{i=1}^5 Z_i^2}}$$

Standardisiert auf Einheitsvarianz ($\text{Var} = 1$):
$$Z_{\text{fat}} = Z_{\text{raw}} \cdot \sqrt{\frac{3}{5}}$$

Jahresrendite via Lognormal-Transformation mit Fat-Tail-Schock:
$$R_{\text{ETF}} = \exp\left( \left(\ln(1+\mu) - \frac{1}{2}\sigma^2\right) + \sigma \cdot Z_{\text{fat}} \right) - 1$$

### 3. Guyton-Klinger Entnahmeregeln
Initialisiert mit der Startentnahmerate $r_0 = \frac{E_0}{W_0}$. In jedem Folgejahr:
$$r_y = \frac{E_{y-1} \cdot (1 + i_y)}{W_y}$$
- Wenn $r_y > 1{,}35 \cdot r_0$: $E_y = E_{y-1} \cdot 0{,}90$ (10 % Kürzung)
- Wenn $r_y > 1{,}20 \cdot r_0$: $E_y = E_{y-1}$ (Inflationsstopp)
- Wenn $r_y < 0{,}80 \cdot r_0$: $E_y = E_{y-1} \cdot 1{,}10$ (10 % Wohlstandserhöhung)

---

## 🛠️ Technologie-Stack & Architektur

* **Single-File Architecture:** Vollständig eigenständige HTML5-Datei (`index.html`) ohne externe Build-Pipelines.
* **Tailwind CSS (CDN):** Modernes, responsives Design mit professioneller Farbcodierung der 3 Töpfe.
* **Chart.js (v4):** Gestapeltes Flächendiagramm für das Vermögen mit synchronisierten Sekundärachsen für Konfidenzbänder und kumulierte Entnahmen.
* **Lucide Icons:** Schlanke, moderne Vektorsymbole für alle Steuerelemente.
* **Performance:**
  - `requestAnimationFrame` (rAF) Debouncing für alle Schieberegler (butterweiche 60 FPS).
  - Keine blockierenden DOM-Operationen während der Simulation.
  - Native TypedArrays für Stochastik-Iterationen.

---

## ⚖️ Rechtlicher Hinweis (Disclaimer)

Dieses Software-Tool dient ausschließlich **didaktischen, illustrativen und wissenschaftlich-planerischen Zwecken**. Die Berechnungen, Simulationen und historischen Szenarien stellen **keine Anlageberatung, Steuerberatung oder Finanzberatung** im Sinne des Wertpapierhandelsgesetzes (WpHG) dar.

Historische Renditen und Volatilitäten sind kein verlässlicher Indikator für zukünftige Wertentwicklungen von Kapitalanlagen. Vor jeder finanziellen Entscheidung sollte eine qualifizierte Fachberatung hinzugezogen werden.

---

## 📄 Lizenz

Dieses Projekt ist unter der **MIT-Lizenz** lizenziert – freie Verwendung, Modifikation und Weitergabe für private und gewerbliche Zwecke gestattet. Siehe [LICENSE](LICENSE) für Details.
