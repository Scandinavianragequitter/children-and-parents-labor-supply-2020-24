# Replikation & Erweiterung: Angrist & Evans (1998)

**"Children and Their Parents' Labor Supply: Evidence from Exogenous Variation
in Family Size"**, *American Economic Review* 88(3), Juni 1998, S. 450–477.

Replikation der **Tabellen 3 und 7** mit IPUMS-USA-Mikrodaten und Erweiterung auf
die Gegenwart. Die Tabellen unten folgen der **Struktur des Papers** und sind um
eine Spalte/Block **2021–24** ergänzt. Identische Pipeline auf allen Epochen →
Unterschiede bilden die *Zeit* ab, nicht die Methode.

## Daten

| Extrakt | Sample | Rolle |
|---|---|---|
| `usa_00001` | ACS 2021–24 (1-Jahr) | Erweiterung "heute" |
| `usa_00002` | Census **1980 & 1990 5% state** | Replikation der A&E-Originale |

Stichprobe (A&E-Restriktionen): Frauen 21–35 mit ≥ 2 Kindern, ältestes Kind ≤ 17
im Haushalt, Alter bei Erstgeburt ≥ 15, **ohne** Frauen, deren zweites Kind < 1 Jahr
alt ist, nur Privathaushalte. Gewichtung durchgehend mit `PERWT`. Einkommen in
konstanten **1995-Dollar** (Paper-Basis). Standardfehler in Klammern.

## Ausführen

```bash
conda activate econometrics
# Notebook von oben nach unten ausführen. Erster Lauf liest 4,2 GB und legt
# panel_full.pkl an (Cache); danach laufen alle Tabellen in Sekunden.
# Nach Änderungen an build_panel(): panel_full.pkl löschen erzwingt Neuaufbau.
```

---

# TABELLE 3 — Anteil der Familien, die ein weiteres Kind bekamen, nach Parität und Geschlecht der Kinder

Struktur wie A&E Tabelle 3 (S. 457): zwei Panels, je "Anteil an der Stichprobe"
und "Anteil mit weiterem Kind", getrennt nach allen / verheirateten Frauen.
*frac* = Anteil an der Stichprobe (über Epochen ≈ konstant).

### Panel A — Familien mit *einem oder mehr* Kindern: Anteil mit *zweitem* Kind, nach Geschlecht des ersten Kindes

| Geschlecht 1. Kind | frac | All 1980 | All 1990 | All 2021–24 | Married 1980 | Married 1990 | Married 2021–24 |
|---|---|---|---|---|---|---|---|
| (1) one girl | 0,489 | 0,619 | 0,605 | 0,552 | 0,645 | 0,629 | 0,580 |
| (2) one boy | 0,511 | 0,621 | 0,608 | 0,556 | 0,646 | 0,631 | 0,583 |
| **difference (2)−(1)** | | **0,002** | **0,003** | **0,004** | **0,001** | **0,002** | **0,003** |

→ Wie im Paper hat das Geschlecht des *ersten* Kindes praktisch keinen Effekt auf
weitere Fertilität (Differenz ≈ 0, A&E S. 456 "very small").

### Panel B — Familien mit *zwei oder mehr* Kindern: Anteil mit *drittem* Kind, nach Geschlecht der ersten zwei Kinder

| Geschlecht 1.+2. Kind | frac | All 1980 | All 1990 | All 2021–24 | Married 1980 | Married 1990 | Married 2021–24 |
|---|---|---|---|---|---|---|---|
| one boy, one girl | 0,495 | 0,378 | 0,370 | 0,416 | 0,375 | 0,363 | 0,415 |
| two girls | 0,242 | 0,443 | 0,431 | 0,464 | 0,445 | 0,431 | 0,471 |
| two boys | 0,264 | 0,427 | 0,422 | 0,459 | 0,427 | 0,420 | 0,467 |
| (1) one boy, one girl | 0,495 | 0,378 | 0,370 | 0,416 | 0,375 | 0,363 | 0,415 |
| (2) both same sex | 0,505 | 0,434 | 0,426 | 0,461 | 0,435 | 0,425 | 0,469 |
| **difference (2)−(1)** | | **0,056** | **0,056** | **0,045** | **0,061** | **0,062** | **0,053** |

s.e. der Anteile ≈ 0,001–0,003; s.e. der Differenz: All 0,001 / 0,002 / 0,003,
Married 0,002 / 0,002 / 0,003.

**Validierung 1980 (all women) vs. Paper (S. 457):** one boy/one girl 0,378
(Paper 0,372), two girls 0,443 (0,441), two boys 0,427 (0,423), both same sex
0,434 (0,432), Differenz 0,056 (0,060).

---

# TABELLE 7 — OLS- und 2SLS-Schätzungen des Effekts von "mehr als 2 Kindern" auf das Arbeitsangebot

Struktur wie A&E Tabelle 7 (1980, S. 464) und Tabelle 8 (1990): zwei Spaltengruppen
**All women | Married women**, je **OLS / 2SLS (same sex)
/ 2SLS (two boys, two girls)**. `labor_income` in 1995-Dollar. Jede abhängige Variable
auf ihrer eigenen Stichprobe geschätzt. Koeffizient (Standardfehler).

## 1980 (≙ A&E Tabelle 7)

**All women** (N = 478.469)

| Dependent | OLS | 2SLS (same sex) | 2SLS (2 boys/2 girls) |
|---|---|---|---|
| Worked for pay | −0,171 (0,001) | −0,120 (0,025) | −0,114 (0,024) |
| Weeks worked | −8,695 (0,065) | −5,382 (1,092) | −5,108 (1,086) |
| Hours/week | −6,523 (0,056) | −4,250 (0,939) | −4,020 (0,934) |
| Labor income | −3.596 (31) | −1.707 (522) | −1.653 (519) |

**Married women** (N = 396.068)

| Dependent | OLS | 2SLS (same sex) | 2SLS (2 boys/2 girls) |
|---|---|---|---|
| Worked for pay | −0,162 (0,002) | −0,128 (0,025) | −0,124 (0,025) |
| Weeks worked | −8,065 (0,071) | −5,648 (1,095) | −5,482 (1,088) |
| Hours/week | −5,984 (0,061) | −4,744 (0,936) | −4,591 (0,930) |
| Labor income | −3.216 (33) | −1.640 (512) | −1.644 (509) |

## 1990 (≙ A&E Tabelle 8)

**All women** (N = 485.503)

| Dependent | OLS | 2SLS (same sex) | 2SLS (2 boys/2 girls) |
|---|---|---|---|
| Worked for pay | −0,147 (0,002) | −0,092 (0,027) | −0,092 (0,027) |
| Weeks worked | −8,316 (0,075) | −6,223 (1,277) | −6,189 (1,277) |
| Hours/week | −6,429 (0,064) | −3,648 (1,087) | −3,646 (1,086) |
| Labor income | −3.726 (41) | −2.522 (711) | −2.507 (711) |

**Married women** (N = 398.582)

| Dependent | OLS | 2SLS (same sex) | 2SLS (2 boys/2 girls) |
|---|---|---|---|
| Worked for pay | −0,142 (0,002) | −0,105 (0,026) | −0,105 (0,026) |
| Weeks worked | −8,047 (0,083) | −6,409 (1,249) | −6,402 (1,249) |
| Hours/week | −6,154 (0,070) | −3,804 (1,049) | −3,802 (1,049) |
| Labor income | −3.594 (45) | −2.896 (704) | −2.891 (704) |


## 2021–24 (Erweiterung, gleiche Struktur)

**All women** (N = 209.574)

| Dependent | OLS | 2SLS (same sex) | 2SLS (2 boys/2 girls) |
|---|---|---|---|
| Worked for pay | −0,119 (0,003) | −0,179 (0,056) | −0,179 (0,056) |
| Weeks worked | −6,774 (0,145) | −9,910 (2,925) | −9,904 (2,925) |
| Hours/week | −5,299 (0,115) | −6,859 (2,333) | −6,854 (2,333) |
| Labor income | −3.331 (109) | −3.817 (2.217) | −3.772 (2.217) |

**Married women** (N = 165.687)

| Dependent | OLS | 2SLS (same sex) | 2SLS (2 boys/2 girls) |
|---|---|---|---|
| Worked for pay | −0,129 (0,003) | −0,135 (0,055) | −0,135 (0,055) |
| Weeks worked | −7,325 (0,165) | −8,801 (2,818) | −8,791 (2,818) |
| Hours/week | −5,792 (0,131) | −5,541 (2,249) | −5,527 (2,249) |
| Labor income | −3.688 (132) | −2.665 (2.277) | −2.631 (2.278) |

---


# Diskrepanzen zum Paper — Gründe & Belegstellen

Übereinstimmend: Geschlechtszusammensetzung, alle Arbeitsangebots-Mittelwerte,
OLS-Schätzer, 2SLS-Beteiligung, Ehemänner-Wochen. Restliche Abweichungen:

| Diskrepanz | Grund | Stelle im Paper |
|---|---|---|
| Frühere Fertilität ~0,03 zu niedrig (behoben) | Ausschluss "zweites Kind < 1 Jahr" fehlte; nach Einbau 0,407 vs. 0,402 | Tabelle 2 **Notes, S. 455** ("…except for women whose second child is less than a year old") |
| Stichprobe N ~21 % höher; Panel-A-Niveau (0,62 vs. 0,69) | A&E bauten 1980 einen **eigenen** Mutter-Kind-Haushaltsmatch; IPUMS `MOMLOC` ist ein anderer Algorithmus. Betrifft nur das *Niveau*, nicht Differenzen/Koeffizienten | **S. 456** ("the 1990 match is probably not as good as the 1980 match … data problems related to the match") |
| Verheiratete 1980-Stichprobe weicht ab (Diff. 0,061 vs. 0,068) | A&E-Definition = "einmal verheiratet, bei Erstgeburt verheiratet"; wir nutzen `SPLOC>0`. Braucht `MARRNO`/`AGEMARR` — **nicht im Extrakt** | **S. 454** und Tabelle 2 **Notes, S. 455** |
| labor_income nicht exakt | A&E in 1995-Dollar mit eigenem Topcoding ($75.000 in 1980); Topcoding-Regeln unterscheiden sich | Tabelle 2 **S. 455** ("in 1995 dollars"); **Fußnote S. 456** (Topcoding) |

Frühere große Abweichungen waren **Methodenfehler** (ungewichtet, `EMPSTAT`
statt "worked last year", fehlender Infant-Ausschluss) und sind behoben. Die Reste
sind **Daten-Grenzen** (A&E-eigener Match; Heirats-Variablen nicht im Extrakt).

