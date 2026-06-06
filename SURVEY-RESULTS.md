# Real-world coverage survey — results (Gitea-only)

> Privátní záznam běhu. Nepatří na public GitHub (obsahuje konkrétní výsledky
> proti scrapnutému seznamu cizích domén). Kód harnessu je veřejný
> (`tools/survey-coverage.js` na `main`), tahle data a report ne.

**Datum:** 2026-06-06
**Harness:** `tools/survey-coverage.js` (read-only, deterministický, jen GET homepage)
**Seznam:** `tools/data/elementor-sites.txt` — 142 reálných živých Elementor webů
z veřejných „best Elementor sites" showcase seznamů.

## Příkaz
```bash
node tools/survey-coverage.js --sites tools/data/elementor-sites.txt --csv /tmp/elementor_survey.csv
```

## Výsledek

```
Surveyed 142 sites; 87 vrátilo Elementor widgety
(55 bot-blocked / JS-only / not-Elementor k plain fetchi)

  ✅ fully auto-convertible                  4   5%
  ⚠️  mostly (<25% manual + guided TODOs)    68  78%
  ❌ manual-heavy (≥25%)                     15  17%
  ──
  convert-plus utáhne hlavní obsah          72/87  83%
```

Rozpad stavů: 87 responded · 34 not-elementor · 16 unreachable · 5 no-widgets

Dominantní widgety: heading 1865×, image 1050×, text-editor 892×, button 626×,
icon 291×, spacer 190×, icon-list 186×, divider 164×, nav-menu 112×,
theme-post-title 112×, html 110×, theme-post-featured-image 83×.

## Interpretace (honest)

- **83 %** je z **showcase** vzorku (čistší/jednodušší buildy) → horní část pásma.
- Dokumentovaných **60 %** (README badge) je z **náhodného** veřejného vzorku 203 webů
  (97 odpovědělo) — poctivá **spodní hranice**.
- Reálné pásmo: **60–83 %**, 60 % = floor. Badge se nenafukuje na 83 %.

## Pozn. k reprodukovatelnosti

Původní survey 203 webů (v této session, badge commit `6b2bfc1`) byl jednorázový
běh přes paralelní subagenty a **neuložil se** — harness ani list. Tenhle běh tu
mezeru zavírá: harness je commitnutý veřejně, list + report jsou v Gitea na větvi
`test-sites`. publicwww free je za loginem, takže původní list už nešel obnovit.
