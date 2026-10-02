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
