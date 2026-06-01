# DSV — Digital Storytelling & Visualisation

**Storytelling, Visuelle Variablen, Datenskalen, Data-Ink, Visualisierungs-Verzeichnis**

---

## Data Storytelling — Grundlagen

### Definition (Dykes 2016)

!!! tip ""
    Data Storytelling = **Daten** + **Visuals** + **Narrative**

| Kombination | Resultat |
|------------|---------|
| Daten allein | Rohes Material, nicht kommunikationsfähig |
| Daten + Visuals | Exploration, kein roter Faden |
| Daten + Narrative | Erklärung, kein visueller Anker |
| Alle drei | **Wirkungsvolle Kommunikation** |

### Narrative Konstituenten

| Konstituente | Frage |
|-------------|-------|
| Erzählerposition | Wer erzählt? (1. / 3. Person, omniszient) |
| Spatio-temporale Dimension | Wo und wann? |
| Charaktere / Ereignisse | Wer und was? |
| Sequenzialität | In welcher Reihenfolge? |
| Erzählwürdigkeit (Tellability) | Warum erzählenswert? |

---

## Author-Driven vs. Reader-Driven & Martini-Glass

### Spektrum (Segel & Heer 2010)

| Dimension | Author-Driven | Reader-Driven |
|-----------|--------------|--------------|
| Interaktivität | Gering | Hoch |
| Kontrolle | Autor gibt Pfad vor | Nutzer wählt |
| Botschaft | Eine, klar | Offen |
| Medium | Video, Slides | Interaktives Dashboard |
| Risiko | Langweilig | Verwirrend |

### Martini-Glass-Struktur

```
   |   Enge Einleitung (Author-driven)
   |   Geführte Narration, ein Pfad
  ___
 /   \  Weites Ende (Reader-driven)
/     \ Freie Exploration, eigene Fragen
```

!!! tip ""
    Martini-Glass = beste Strategie für Datenjournalismus: Erst die Botschaft einführen, dann den Nutzer erkunden lassen.

### Typen nach Funktion

| Typ | Funktion | Interaktivität |
|-----|---------|---------------|
| Exploratorisch | Nutzer findet Erkenntnisse | Hoch |
| Explanatory (erklärend) | Hebt Schlüsselerkenntnisse hervor | Mittel |
| Exhibitorisch | Daten zeigen, kein Narrativ | Gering |

---

## Datenskalen (NOIR) & Variablentypen

### NOIR-Skalenniveau

| Skala | Operationen | Lage | Variabilität |
|-------|------------|------|------------|
| **Nominal** | =, ≠ | Modus | Qual. Variation |
| **Ordinal** | >, < | Median | Range, IQR |
| **Intervall** | +, − | Arithm. Mittel | Standardabw. |
| **Ratio** | ×, ÷ (echter Nullpunkt) | Geom. Mittel | Variationskoeff. |

### Datentypen

- **Kategorisch (qualitativ)**: diskret + nominal/ordinal
- **Numerisch (quantitativ)**: intervall oder ratio
- **Strukturiert**: Tabellen, CSV; **Unstrukturiert**: Text, Bilder; **Semi-strukturiert**: XML, JSON

### Beispiel

| Variable | Typ | Skala |
|----------|-----|-------|
| Monat | Kategorisch | Ordinal |
| Standort | Kategorisch | Nominal |
| Temperatur (°C) | Numerisch | Intervall (kein absoluter Nullpunkt) |
| Gewicht (kg) | Numerisch | Ratio |

---

## Visuelle Variablen (Bertin)

### Die 7 visuellen Variablen

| Variable | Deutsch | Beispiel | Geeignet für |
|----------|---------|---------|-------------|
| Form (Shape) | Gestalt | Kreis, Quadrat, Dreieck, Stern, Ellipse | Nominal |
| Position | Lage x/y | Koordinaten auf Achsen | Ordinal/Ratio |
| Orientation | Ausrichtung | 0°, 45°, 90° Rotation | Nominal/Ordinal |
| Size | Grösse | Kleiner vs. grösser Punkt | Ordinal/Ratio |
| Color (Hue) | Farbton | Rot, Blau, Grün | Nominal |
| Value | Helligkeit | Hell- bis Dunkelgrau | Ordinal |
| Texture | Textur | Liniert, gepunktet, kariert | Nominal |

!!! warning "Häufiger Fehler"
    Farbtöne (Hue) für ordinale/metrische Daten — Farben haben keine inhärente Reihenfolge. Für Rangfolgen → Helligkeit (Value) oder Grösse.

### Formvariablen im Detail

| Form | Implikation |
|------|------------|
| Kreis | Symmetrisch, allgemein, kein Trend |
| Quadrat | Geordnet, kategorial, vier Seiten gleich |
| Dreieck | Richtungsanzeige (Pfeilspitze) |
| Stern | Aufmerksamkeit, Auszeichnung |
| Ellipse | Richtungsangabe durch Achsenverhältnis |

---

## Data-Ink Ratio & Chartjunk (Tufte)

*Edward Tufte — The Visual Display of Quantitative Information, 1983*

### Graphical Excellence

!!! quote "Tufte"
    "The well-designed presentation of interesting data — a matter of substance, of statistics, and of design."

!!! quote "Tufte"
    "Gives to the viewer the greatest number of ideas in the shortest time with the least ink in the smallest space."

- Clarity, precision, efficiency

### Data-Ink Ratio

```
Data-Ink Ratio = ink used to describe data / total ink used to print the graphic
```

!!! quote "Tufte"
    "The proportion of a graphic's ink devoted to the non-redundant display of data information."

!!! tip "Regel"
    Maximize the data-ink ratio, within reason.

### Chartjunk (Non-Data-Ink)

!!! quote "Tufte"
    "The interior decoration of graphics generates a lot of ink that does not tell the viewer anything new."

Drei Elemente von Chartjunk:

1. **Vibrations**: Texturen die Moiré-Effekte erzeugen (schraffierte Balken etc.)
2. **The self-promoting graphical duck**: Form dominiert über Funktion (z.B. Gebäude als Balken)
3. **The dreaded grid**: Unnötige Gitterlinien im Hintergrund

---

## Verzeichnis der Visualisierungen

### Numerische Einzelwerte

| Charttyp | Variante | Verwendung |
|---------|---------|-----------|
| Balkendiagramm | Vertikal, horizontal, Dot | Mengen vergleichen |
| Histogram | Histogram, Density, CDF | Verteilung kontinuierlicher Variablen |
| Boxplot / Violin Plot | — | Verteilung + Ausreisser |

### Beziehungen zwischen Variablen

| Fragestellung | Charttyp |
|--------------|---------|
| 2 Variablen (ordinal+) | Scatterplot, Bubble Chart (3. Var = Grösse) |
| 2 kontinuierliche Var. | 2D-Density, Contour, 2D-Histogram, Hex Bins |
| Zeit + Wert | Liniendiagramm, Connected Scatterplot |
| Kontinuierlich–diskret | Slope Graph |
| Mehrere numerische Var. | Correlogram |

### Anteile & Proportionen

| Fragestellung | Charttyp |
|--------------|---------|
| Teile eines Ganzen | Stacked Bar, Pie Chart |
| Verschachtelte Anteile | Mosaic Plot, Treemap, Parallel Sets |
| Mengenüberschneidungen | Venn-Diagramm |

### Wahl des richtigen Charttyps

| Frage | Empfehlung |
|-------|----------|
| Vergleich zwischen Gruppen | Balkendiagramm (horizontal bei vielen Kategorien) |
| Verlauf über Zeit | Liniendiagramm |
| Korrelation zweier Variablen | Scatterplot |
| Anteil am Ganzen | Stacked Bar (Pie nur max. 5 Segmente) |
| Verteilung + Ausreisser | Box Plot oder Violin Plot |
| Muster in Matrix | Heatmap |

---

## Prüfungstipps DSV

!!! tip "Häufige Prüfungsfragen"
    1. Data Storytelling = Daten + Visuals + Narrative (alle drei nötig)
    2. Martini-Glass skizzieren und erklären
    3. Welche visuelle Variable für welchen Datentyp?
    4. Author-driven vs. Reader-driven: Vor-/Nachteile
    5. NOIR-Skalen: Welche Statistiken sind erlaubt?
    6. Data-Ink Ratio: Definition + Maxime
    7. Chartjunk: 3 Typen nennen und erklären
    8. Richtigen Charttyp für Fragestellung begründen

!!! warning "Häufige Fehler"
    - Hue für ordinal/metrisch → Fehler: keine inhärente Reihenfolge
    - Exploratorisch mit Explanatory verwechseln
    - Pie Chart mit mehr als 5 Segmenten → schwer lesbar
    - Chartjunk erhöht Datenmenge visuell, informiert aber nicht
