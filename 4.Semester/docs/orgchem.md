# OrgChem — Organische Chemie

**Bindungen, Nomenklatur, Stereochemie, Reaktionen, Gleichgewicht**

---

## Kohlenstoff-Bindungen, Hybridisierung & Allotrope

### Hybridisierung

| Hybr. | Bindungswinkel | Bindungstyp | Beispiel |
|-------|---------------|-------------|---------|
| sp³ | 109.5° | 4 Einfachbindungen, tetraedrisch | Methan CH₄, Alkane |
| sp² | 120° | 1 Doppelb. + 2 Einfachb., planar | Ethylen, Benzol |
| sp | 180° | 1 Dreifachb. + 1 Einfachb., linear | Ethin HC≡CH |

### Allotrope des Kohlenstoffs

| Allotrop | Hybr. | Struktur | Eigenschaft |
|----------|-------|---------|------------|
| Diamant | sp³ | 3D-Gitter, tetraedrisch | Härtestes natürliches Material, Nichtleiter |
| Graphit | sp² | Sechsring-Schichten, π-System | Elektrisch leitend, weich |
| Graphen | sp² | Einzelne Graphitschicht | Sehr hohe Leitfähigkeit, flexibel |
| Fulleren C₆₀ | sp² | 60 C-Atome, kugelförmig | 12 Fünf- + 20 Sechsringe |
| CNT Nanoröhren | sp² | Gerolltes Graphen | Sehr zugfest, leitend/halbleitend |

### Bindungsenthalpien (kJ/mol)

| Bindung | kJ/mol | Bindung | kJ/mol |
|---------|--------|---------|--------|
| H–H | 432 | C=C | 614 |
| C–H | 411 | C≡C | 835 |
| C–C | 362 | Cl–Cl | 243 |

---

## Klassifikation & IUPAC-Nomenklatur

### Systematik organischer Verbindungen

- **Aliphatisch**: Ketten ohne Ringe
    - Alkane: CₙH₂ₙ₊₂ (gesättigt)
    - Alkene: CₙH₂ₙ (eine Doppelbindung)
    - Alkine: CₙH₂ₙ₋₂ (eine Dreifachbindung)
- **Zyklisch**: karbozyklisch (nur C) oder heterozyklisch (N, O, S im Ring)
- **Aromatisch**: delokalisierte π-Elektronen, Hückel-Regel: 4n+2

### IUPAC-Nomenklatur — 4 Schritte

1. **Hauptkette**: Längste ununterbrochene C-Kette bestimmen
2. **Seitenketten**: Alphabetisch benennen (Ethyl vor Methyl)
3. **Vielfachheit**: di-, tri-, tetra- (werden nicht alphabetisch gezählt)
4. **Nummerierung**: Substituenten sollen kleinstmögliche Positionsnummern erhalten

### Stammname nach C-Zahl

| C | Präfix | C | Präfix |
|---|--------|---|--------|
| 1 | Meth- | 5 | Pent- |
| 2 | Eth- | 6 | Hex- |
| 3 | Prop- | 7 | Hept- |
| 4 | But- | 8 | Oct- |

---

## Isomerie

```
Isomerie
├── Konstitutionsisomerie (gleiche Formel, andere Verknüpfung)
└── Stereoisomerie (gleiche Verknüpfung, andere Raumanordnung)
    ├── Konfigurationsisomerie (Bindungsbruch nötig)
    │   ├── Enantiomerie (Spiegelbilder, chirales C)
    │   └── Diastereomerie (cis/trans, kein Spiegelbild)
    └── Konformationsisomerie (Rotation, kein Bindungsbruch)
```

### Chiralitätszentrum (R/S)

- sp³-C mit 4 verschiedenen Substituenten
- **R** (rectus): Prioritäten 1→2→3 im Uhrzeigersinn
- **S** (sinister): Prioritäten 1→2→3 gegen Uhrzeigersinn
- CIP-Priorität: höhere Ordnungszahl = höhere Priorität

### E/Z-Isomerie (Doppelbindungen)

- **Z** (zusammen): höhere Prioritäten auf gleicher Seite
- **E** (entgegen): höhere Prioritäten auf gegenüberliegenden Seiten

---

## Funktionelle Gruppen

| Klasse | Gruppe | Strukturformel | Suffix |
|--------|--------|---------------|--------|
| Alkohol | Hydroxyl | R–OH | -ol |
| Ether | Ether | R–O–R' | -ether |
| Aldehyd | Carbonyl | R–CHO | -al |
| Keton | Carbonyl | R–CO–R' | -on |
| Carbonsäure | Carboxyl | R–COOH | -säure |
| Ester | Ester | R–COO–R' | -at / -ester |
| Amid | Amidgruppe | R–CO–NH₂ | -amid |
| Amin | Amingruppe | R–NH₂ | -amin |
| Thiol | Sulfanyl | R–SH | -thiol |
| Halogenid | Halogen | R–X | halo- |
| Nitril | Cyano | R–C≡N | -nitril |

### Reaktivitätsreihenfolge

```
Carbonsäure > Ester ≈ Amid > Keton ≈ Aldehyd > Alkohol
```

---

## Reaktionen & Mechanismen

### Radikalische Halogenierung (Alkane)

Bedingungen: hν (UV-Licht) oder T > 300°C

1. **Initiation**: Cl₂ → 2 Cl• (homolytische Spaltung)
2. **Propagation**: CH₄ + Cl• → CH₃• + HCl; CH₃• + Cl₂ → CH₃Cl + Cl•
3. **Termination**: Zwei Radikale rekombinieren

Stufenweise Chlorierung: CH₄ → CH₃Cl → CH₂Cl₂ → CHCl₃ → CCl₄

### Reaktivität & Selektivität der Halogene

| Halogen | Reaktivität | Selektivität |
|---------|------------|-------------|
| F₂ | Sehr hoch | Sehr gering |
| Cl₂ | Hoch | Gering |
| Br₂ | Mittel | Hoch (tertiäre C bevorzugt) |
| I₂ | Gering (endotherm) | Sehr hoch |

### Wichtige Reaktionstypen

| Typ | Kürzel | Beispiel |
|-----|--------|---------|
| Substitution radikalisch | SR | Halogenierung von Alkanen |
| Substitution elektrophil | SE | Nitrierung von Benzol |
| Addition elektrophil | AE | HBr an Alkene (Markownikov) |
| Elimination | E1/E2 | Dehydratisierung von Alkoholen |
| Substitution nukleophil | SN1/SN2 | R–X + OH⁻ → R–OH |

---

## Chemisches Gleichgewicht & Massenwirkungsgesetz

### Dynamisches Gleichgewicht

Die meisten chemischen Reaktionen laufen **nicht vollständig** ab. Edukte und Produkte liegen nebeneinander vor.

Gleichgewichtszustand: v_hin = v_rück — Konzentrationen bleiben konstant, Reaktion läuft weiter.

Beispiel: N₂O₄ ⇌ 2 NO₂ (Gleichgewicht bei 25°C, K_c = 0.0047)

### Massenwirkungsgesetz (MWG)

Gilt für jede reversible Reaktion im Gleichgewicht:

```
aA + bB ⇌ cC + dD

K_c(T) = [C]^c · [D]^d / ([A]^a · [B]^b)
```

- K_c = Gleichgewichtskonstante (nur T-abhängig)
- Zähler: Produkte (stöchiometrische Koeffizienten als Exponenten)
- Nenner: Edukte (stöchiometrische Koeffizienten als Exponenten)
- Reaktionsrichtung angeben! K_hin = 1/K_rück

### Reaktionsquotient Q

Wie K_c, aber mit beliebigen (nicht Gleichgewichts-)Konzentrationen:

- Q < K_c: Reaktion läuft vorwärts
- Q > K_c: Reaktion läuft rückwärts
- Q = K_c: Gleichgewicht erreicht

### Prinzip von Le Chatelier

Ein System im Gleichgewicht reagiert auf äussere Störungen so, dass es der Störung entgegenwirkt:

| Störung | Systemreaktion |
|---------|---------------|
| Konzentration Edukte ↑ | Reaktion vorwärts (mehr Produkte) |
| Konzentration Produkte ↑ | Reaktion rückwärts |
| Temperatur ↑ | Endotherme Richtung bevorzugt |
| Druck ↑ (Gase) | Seite mit weniger Gasmolekülen bevorzugt |
| Katalysator | Kein Einfluss auf Gleichgewichtslage, nur auf Geschwindigkeit |

### Bedeutung von K_c

| K_c | Bedeutung |
|-----|-----------|
| K_c >> 1 | Produkte stark bevorzugt (Reaktion läuft fast vollständig ab) |
| K_c << 1 | Edukte stark bevorzugt (kaum Produkte) |
| K_c ≈ 1 | Edukte und Produkte ungefähr gleich |

---

## Prüfungstipps OrgChem

!!! tip "Häufige Aufgaben"
    1. IUPAC-Name: 4-Schritte-Regel anwenden (längste Kette!)
    2. Bindungswinkel und Hybridisierung zuordnen
    3. Stereozentren erkennen, R/S bestimmen (CIP-Regeln)
    4. Funktionelle Gruppe aus Strukturformel erkennen
    5. Massenwirkungsgesetz aufstellen (K_c für Reaktion)
    6. Le Chatelier: Welche Richtung bevorzugt bei Störung?
    7. Q berechnen und mit K_c vergleichen → Reaktionsrichtung

!!! warning "Häufige Fehler"
    - Nicht die längste Kette gewählt
    - Alphabetische Reihenfolge (Ethyl vor Dimethyl — di/tri zählen nicht)
    - Reaktionsrichtung bei K_c nicht angegeben → K_hin ≠ K_rück
    - Katalysator verändert Gleichgewichtslage (falsch — nur Geschwindigkeit)
