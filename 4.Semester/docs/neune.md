# NeuNe — Neural Networks

**SW01–SW06:** Perceptron, MLP, CNN, Training, RNN, NLP

---

## Perceptron — Grundlagen & Lernregel

### Perceptron (Rosenblatt 1957)

Binaerer Klassifikator fuer linear trennbare Daten.

```
y = 1, falls w·x + b ≥ 0   |   y = 0, sonst
```

### Lernregel (Gradientenabstieg)

```
w ← w + η · (y_target − y_pred) · x
b ← b + η · (y_target − y_pred)
```

η = Lernrate (typisch 0.01–0.1). Konvergiert **nur** bei linear trennbaren Daten.

### Lineare Trennbarkeit

| Problem | Linear trennbar? | Perceptron loesbar? |
|---------|-----------------|---------------------|
| AND | Ja | Ja |
| OR | Ja | Ja |
| XOR | Nein | Nein — braucht MLP |

---

## MLP — Multilayer Perceptron & Backpropagation

### Kuenstliches Neuron

```
y_i = σ( Σ_j w_{ij} · x_j + b_i )
```

### Aktivierungsfunktionen

| Funktion | Formel | Einsatz |
|----------|--------|---------|
| Sigmoid | 1 / (1+e^{-x}) | Binaerer Output |
| ReLU | max(0, x) | Hidden Layers (Standard) |
| Tanh | (e^x−e^{-x})/(e^x+e^{-x}) | Hidden Layers |
| Softmax | e^{x_i} / Σ e^{x_j} | Multi-Klassen Output |

### Backpropagation

1. Forward Pass: Vorhersage berechnen
2. Loss berechnen: L(y_pred, y_true)
3. Gradienten via Kettenregel: ∂L/∂w
4. Gewichte: w ← w − η · ∂L/∂w

---

## Training Pipeline, Lernbegriff & Performance

!!! quote "Mitchell 1997"
    "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

### Pipeline

1. Task definieren
2. Daten sammeln & aufteilen
3. Architektur / Loss / Optimizer wählen
4. Trainieren
5. Evaluieren auf Validierungsdaten
6. Hyperparameter-Tuning
7. Regularisierung (Dropout, L2, Augmentation)

### Aufgabentypen

| Typ | Funktion | Loss |
|-----|----------|------|
| Klassifikation | f: R^n → {1,...,k} | Cross-Entropy |
| Regression | f: R^n → R | MSE |

### Performance-Metriken

| Metrik | Formel |
|--------|--------|
| Accuracy | (TP+TN) / N_total |
| Precision | TP / (TP+FP) |
| Recall | TP / (TP+FN) |
| F1-Score | 2·P·R / (P+R) |

### Dataset-Aufteilung

- **Training ~80%**: Modell lernt
- **Validation ~20% des Trainings**: Hyperparameter-Tuning
- **Test (held-out)**: Nur 1× zur finalen Evaluation

### MNIST

- 60 000 Trainings- / 10 000 Testbilder; 28×28 Graustufen
- Shape: `(60000, 28, 28)`; Labels {0,...,9}
- Normalisierung: Pixelwerte ÷ 255 → [0,1]

!!! warning "Loss ≠ Metrik!"
    Loss muss differenzierbar sein (für Backprop). Accuracy ist es nicht — wird nur zur Anzeige verwendet.

---

## CNN — Convolutional Neural Networks

### Motivation

- **Lokale Rezeptivfelder**: Neuron sieht nur Teil des Bildes
- **Geteilte Gewichte**: Gleicher Kernel über gesamtes Bild
- **Translation-Invarianz**: Position-unabhängige Erkennung

### Faltungsoperationen

**1D:**
```
(x * w)[i] = Σ_n x[i−n] · w[n]
```

**2D (Bild):**
```
(X * W)[i,j] = Σ_n Σ_k X[i−n, j−k] · W[n,k]
```

**Faltungsschicht (mit Tiefe/Kanälen):**
```
z_{i,j,d} = Σ_n Σ_k Σ_m X[i+n, j+k, m] · W[n,k,m,d] + b_d
```

### Parameter einer Conv2D-Schicht

| Parameter | Bedeutung | Keras-Default |
|-----------|-----------|---------------|
| filters | Anzahl Output-Kanäle | — |
| kernel_size | Filtergrösse (z.B. 3×3) | — |
| strides | Schrittweite | 1 |
| padding | 'valid' oder 'same' | 'valid' |

### Output-Grösse (ohne Padding)

```
output = floor((input − kernel) / stride) + 1
```

### Anzahl Parameter (Conv-Schicht)

```
(kernel_h × kernel_w × in_channels + 1) × filters
```

### Pooling

| Typ | Operation |
|-----|-----------|
| Max Pooling | Maximum im Fenster — häufigste Wahl |
| Average Pooling | Mittelwert im Fenster |

### LeNet-5 Architektur

```
Input (32×32×1)
→ Conv2D(6, 5×5, ReLU)    → 28×28×6
→ AvgPool2D(2×2)           → 14×14×6
→ Conv2D(16, 5×5, ReLU)   → 10×10×16
→ AvgPool2D(2×2)           → 5×5×16
→ Flatten → Dense(120) → Dense(84) → Dense(10, Softmax)
```

### Keras-Beispiel

```python
model = tf.keras.Sequential([
    tf.keras.layers.Conv2D(32, kernel_size=3, strides=1,
                           padding='valid', activation='relu',
                           input_shape=(28,28,1)),
    tf.keras.layers.MaxPool2D(pool_size=2, strides=2),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')
])
```

---

## RNN — Recurrent Neural Networks

### Motivation: Sequentielle Daten

- FNN: gut für tabellarische Daten (i.i.d. Annahme)
- CNN: gut für Bilder (lokale Muster)
- RNN: designed für **sequentielle/temporale Daten** (Zeitreihen, Text)

Sequentielle Daten **verletzen die i.i.d.-Annahme** — aufeinanderfolgende Punkte sind korreliert.

### Zeitreihenvorhersage

- Aufgabe: Vorhersage x_{t+1} aus (x_0, ..., x_t)
- Naives Benchmark-Modell: x̂_{t+1} = x_t
- Autoregressive Modell: ŷ = ax_t + b
- Fenstergrösse τ: Input x_t = (x_t, x_{t-1}, ..., x_{t-τ})

### Latentes Variablenmodell (Hidden State)

```
h_t = f(x_t, h_{t-1})
```

### Einfaches RNN

```
h^t = σ_h(U·x^t + W·h^{t-1})
y^t = σ_out(V·h^t)
```

- U: Gewichte Input → Hidden
- W: Gewichte Hidden → Hidden (Rekurrenz)
- V: Gewichte Hidden → Output

### FNN vs RNN

| Aspekt | FNN | RNN |
|--------|-----|-----|
| Informationsfluss | Nur vorwärts | Auch rückwärts (Feedback) |
| Sequenz | Keine | Ja — Gedächtnis |
| Dynamisches System | Nein | Ja |

### Modell-Annahmen

- **Stationarität**: Dynamik ändert sich nicht über Zeit
- **Markov-Bedingung**: p(x_{t+1}|x_t) — Zukunft hängt nur von unmittelbarer Vergangenheit ab
- **Kausalität**: Zukunft hängt nicht von Zukunft ab

---

## NLP — Natural Language Processing

### NLP-Aufgaben

| Aufgabe | Beschreibung |
|---------|-------------|
| Dokumentenklassifikation | Text → Kategorie (Spam, Sentiment) |
| Semantische Suche | Ähnlichkeit von Texten |
| Maschinelle Übersetzung | seq2seq: Seq → andere Sprache |
| Sentiment Analysis | positiv / negativ / neutral |
| Named Entity Recognition | Personen, Orte, Organisationen |
| POS-Tagging | Part-of-speech (Nomen, Verb, ...) |
| Textzusammenfassung | Langer Text → kurze Zusammenfassung |
| Textgenerierung | Nächstes Wort vorhersagen |

### Text-Preprocessing Pipeline

1. **Text laden**: Rohdaten als Strings
2. **Tokenisierung**: Text → Liste von Tokens (Wörter/Zeichen)
3. **Vokabular aufbauen**: Tokens → numerische Indizes
4. **Vektorisierung**: Sequenzen numerischer Indizes → Modell-Input

### Python Text-Preprocessing

```python
# Bereinigung: Grossbuchstaben-Header entfernen
sub_lines = [re.sub(r"[A-Z]{2,}", "", line) for line in lines]
# Kleinbuchstaben + Satzzeichen entfernen
sub_lines = [re.sub(r'[^A-Za-z]+', ' ', line).strip().lower()
             for line in sub_lines]
# Leerzeilen entfernen
sub_lines = [line for line in sub_lines if line.strip()]
main_text_lines = sub_lines[16:-287]  # Metadaten abschneiden
```

### TensorFlow tf.data

```python
tf_dataset = tf.data.Dataset.from_tensor_slices(main_text_lines)
for line in tf_dataset.take(4):
    print(line.numpy())
```

`tf.data`: optimierte Datenpipeline für TensorFlow (grosser Datensatz + streaming)

---

## Prüfungstipps NeuNe

!!! tip "Häufige Prüfungsfragen"
    1. Warum kann Perceptron kein XOR lösen? → Nicht linear trennbar
    2. Output-Grösse einer Conv-Schicht berechnen: (input − kernel)/stride + 1
    3. Anzahl Parameter in Conv-Schicht: (k×k×in + 1)×filters
    4. padding='valid' vs 'same' — was ist der Unterschied?
    5. Unterschied Loss vs Metrik
    6. Validation Set vs Test Set — Warum zwei getrennte?
    7. Warum brauchen wir RNNs statt FNNs für Zeitreihen?
    8. Was ist der Hidden State h_t?

!!! warning "Häufige Fehler"
    - Testdaten für Hyperparameter-Tuning verwenden → Data Leakage
    - Accuracy als Loss-Funktion (nicht differenzierbar)
    - padding='valid' → Output kleiner als Input (kein Padding)
    - padding='same' → Output = Input-Grösse (Zero-Padding)
    - Bias bei Parameteranzahl vergessen
