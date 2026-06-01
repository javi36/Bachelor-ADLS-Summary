# DaS — Data and Society

**SW01–SW13:** Macht der Daten, Leviathan, Turing, Algorithmen, KI-Geschichte, Kognitive Biases

---

## SW01 — Die Macht der Daten

- Lebenserwartung USA: 47.3 (1900) → 78 Jahre (2006) — Faktor 1.65 in 106 Jahren
- Starke Korrelation: BIP pro Kopf ↑ → Lebenserwartung ↑
- 1918: H1N1-Pandemie ~50 Millionen Tote weltweit
- John Snow 1854: Cholera-Karte London → erste epidemiologische Datenanalyse
- Daten ermöglichen: Vorhersage, Kontrolle, Optimierung von gesellschaftlichen Problemen

---

## SW02 — Narrow Corridor (Acemoglu & Robinson 2019)

### Kernthese

Freiheit entsteht nur im **"Schmalen Korridor"**, wo BEIDE — Staat UND Gesellschaft — stark sind.

### Hobbes: Naturzustand

- "Homo homini lupus est" — Der Mensch ist dem Menschen ein Wolf
- Naturzustand = "warre": "nasty, brutish and short"
- Lösung: Sozialer Vertrag → Leviathan (Staat)
- Leviathan ohne Kontrolle = Despotismus

### Locke: Freiheit

!!! quote "John Locke"
    "Perfect freedom... without asking leave of any other man"

### Vier Quadranten

| Staat | Gesellschaft | Ergebnis |
|-------|-------------|---------|
| Schwach | Schwach | Anarchie / Failed State |
| Stark | Schwach | Despotismus |
| Schwach | Stark | Stammesgesellschaft |
| Stark | Stark | **Schmaler Korridor = Freiheit** |

### Datenmissbrauch: Historische Beispiele

- **Nazi-Deutschland**: Volkszählungen 1933/1939 via Hollerith-Tabelliermaschinen (IBM) zur Verfolgung jüdischer Bürger
- **China / Uiguren**: ~1 Mio. seit 2014 in Umerziehungslagern; KI-gestützte Massenüberwachung
- Jäger-Sammler: ~500 Gewalttote/100 000/Jahr; Lebensrisiko ~25% durch Gewalt

---

## SW03/04 — Entscheidungsproblem & Turing-Maschinen

### Hilbert-Programm (SW03)

- Ziel: Mathematik auf endlichen Axiomen aufbauen, widerspruchsfrei, vollständig, entscheidbar
- Russells Paradox (1903): Grundlagenkrise der Mathematik
- **Kurt Gödel (1931)**: Formale Systeme mit Arithmetik sind notwendig unvollständig

### Turing-Maschine (SW04)

Alan Turing (1930, Cambridge): "Können die Denkprozesse des Geistes von einer Maschine imitiert werden?"

Turing-Maschine = mathematisches Objekt, kann in Realität nur approximiert werden.

### Komponenten der Turing-Maschine

- **Unendliches Band**: sequentiell geordnete Felder; je ein Symbol aus Alphabet; leere Felder erlaubt
- **Lese-/Schreibkopf**: bewegt sich 1 Feld links oder rechts; liest und überschreibt Symbole
- **Programm**: interne Zustände (Z1, Z2, ..., STOP); Übergänge "X → (Y, Q)"

### Programm-Notation

`"X → (Y, Q)"` bedeutet: Falls Symbol X gelesen, schreibe Y und bewege in Richtung Q (L/R)

### Universal Turing Machine

- Kann Berechnungen aller anderen Turing-Maschinen ausführen
- Programm der zu imitierenden Maschine wird auf dem Band als Input übergeben
- Moderne Computer = **Turing-vollständig**

### Church-Turing-These

!!! quote ""
    "The class of functions computable by a universal Turing machine corresponds to the class of intuitively computable functions."

### Halteproblem (Halting Problem)

Hilbert: "Gibt es ein mechanisches Verfahren, das entscheidet ob ein Programm T_n bei Input m hält?"

```
H(n;m) = 0, falls T_n(m) nicht hält
H(n;m) = 1, falls T_n(m) stoppt
```

**Turings Beweis (1936, Widerspruchsbeweis)**: Eine solche Maschine H kann nicht existieren.

Original-Publikation: *"On computable numbers, with an application to the Entscheidungsproblem"* (1936)

Folge: Das Entscheidungsproblem hat **keine Lösung** — nicht alle mathematischen Aussagen sind maschinell entscheidbar.

---

## SW05/06 — Algorithmen & Explore/Exploit

### Multi-Armed Bandit Problem

Wie viel **Exploration** (Neues ausprobieren) vs. **Exploitation** (Bestes nutzen)?

| Strategie | Beschreibung |
|-----------|-------------|
| ε-greedy | Mit Prob. ε erkunden, sonst besten Arm wählen |
| UCB (Upper Confidence Bound) | Unsicherheit explizit berücksichtigen |
| Gittins Index | Optimale Strategie für diskontierte Belohnungen |
| Thompson Sampling | Bayesianisch: Wahrscheinlichkeitsverteilung samplen |

### Sortieralgorithmen

| Algorithmus | Best | Avg | Worst |
|------------|------|-----|-------|
| Bubble Sort | O(n) | O(n²) | O(n²) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) |

Untere Schranke (vergleichsbasiert): O(n·log n)

---

## SW08 — Geschichte der KI (Walter Pitts)

### Walter Pitts — Biografie

- Autodidakt aus Detroit; las mit 12 Jahren Bertrand Russells Principia Mathematica
- Zusammenarbeit mit Warren McCulloch → erstes mathematisches Neuronenmodell (1943)
- Werk legte Grundstein für künstliche neuronale Netze

### Verbindungskette zur KI

```
Principia Mathematica (Russell/Whitehead)
  → Hilbert-Programm
  → Gödels Unvollständigkeit
  → Turing-Maschinen
  → Pitts/McCulloch Neuron
  → Von Neumann (Computerarchitektur)
  → KI
```

Pitts zeigte: Neuronale Netze können logische Operationen berechnen → Gehirn = logische Maschine → Maschinen können "denken"

---

## SW10/12 — Techno-Optimismus & Produktivitäts-Bandwagon

### Produktivitäts-Bandwagon (Acemoglu & Johnson, *Power and Progress* 2023)

- In der Vergangenheit: Techno-Optimismus = neue Technologie führt immer zu geteiltem Wohlstand
- Mechanismus: Neue Technologie → mehr Arbeitsnachfrage → höhere Löhne
- Zwei kausale Verbindungen: (1) Neue Technologie → mehr Nachfrage nach Arbeit; (2) Mehr Nachfrage → höhere Löhne
- Probleme können beide Verbindungen stören
- Funktionierender Bandwagon-Effekt braucht **richtige gesellschaftliche und institutionelle Umgebung**

### Kritik am Techno-Optimismus

- Automatisierung kann Arbeit ersetzen statt ergänzen
- Historische Beispiele: Industrialisierung → zuerst Lohnrückgang, dann langsam Erholung
- KI-Risiko: Konzentration von Gewinn bei wenigen, Verdrängung vieler

---

## SW13 — Kognitive Biases (Kahneman & Tversky)

### Daniel Kahneman — Biografie

Jüdischer Junge in Paris 1941 unter Nazi-Besatzung. Begegnung mit SS-Offizier, der ihn mit Bild seines Sohnes vergleicht — tiefe Erkenntnis über menschliche Komplexität. Später: lebenslange Zusammenarbeit mit Amos Tversky.

### Mathematische Psychologie

Fragen: Wie treffen Menschen Entscheidungen unter Unsicherheit? Welche Algorithmen verwendet das Gehirn? Unter welchen Bedingungen weichen Menschen von rationalem Entscheiden ab?

### Drei kognitive Heuristiken (Tversky & Kahneman 1974, Science)

| Heuristik | Definition | Klassisches Beispiel |
|-----------|-----------|---------------------|
| **Representativeness** | "Grad, zu dem ein Ereignis den wesentlichen Eigenschaften seiner Elternpopulation ähnelt" | HHHTTT vs HTHTTH — beide gleich wahrscheinlich, HTHTTH "sieht zufälliger aus" |
| **Availability** | Wahrscheinlichkeit einer Ereigniskategorie beurteilt durch Leichtigkeit der Erinnerung | Buchstabe K: häufiger in 1. oder 3. Position? → K häufiger in 3., aber 1. leichter abrufbar |
| **Anchoring** | Schätzungen werden durch einen Ausgangswert (Anker) beeinflusst | 8×7×6×5×4×3×2×1 vs 1×2×3×4×5×6×7×8 → Gruppe A schätzt viel höher |

### Prospect Theory

- Verluste werden stärker gewichtet als äquivalente Gewinne (Loss Aversion)
- Subjektive Wahrscheinlichkeiten weichen von objektiven ab (besonders an Extremen)

### Computational Theory of Mind

Das Gehirn als Computer → kognitive Biases sind evolutionäre Algorithmen. Wenn identifiziert, können Entscheidungsumgebungen so gestaltet werden, dass zuverlässigere Entscheidungen entstehen.

---

## Prüfungstipps DaS

!!! tip "Häufige Prüfungsfragen"
    1. Narrow Corridor: Wann entsteht Freiheit? (BEIDE Staat + Gesellschaft stark)
    2. Hobbes vs. Locke: Ausgangspunkte und Schlussfolgerungen
    3. Datenmissbrauch-Beispiele nennen und einordnen
    4. Turing-Maschine: Komponenten, Programm-Notation, Halteproblem
    5. Church-Turing-These formulieren
    6. Drei Kahneman/Tversky-Heuristiken + je ein Beispiel
    7. Explore/Exploit Trade-off: ε-greedy Strategie

!!! warning "Wichtiger Hinweis"
    DaS = normatives Fach. Argumentationsstruktur wichtiger als reine Faktenwiedergabe. Kontext und Implikationen mitdenken.
