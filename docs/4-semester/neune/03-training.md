# 3. Training Pipeline, Lernbegriff & Performance

!!! quote "Mitchell 1997"
    "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

## 1. Pipeline

1. Task definieren
2. Daten sammeln & aufteilen
3. Architektur / Loss / Optimizer wählen
4. Trainieren
5. Evaluieren auf Validierungsdaten
6. Hyperparameter-Tuning
7. Regularisierung (Dropout, L2, Augmentation)

## 2. Aufgabentypen

| Typ | Funktion | Loss |
|-----|----------|------|
| Klassifikation | f: R^n → {1,...,k} | Cross-Entropy |
| Regression | f: R^n → R | MSE |

## 3. Performance-Metriken

| Metrik | Formel |
|--------|--------|
| Accuracy | (TP+TN) / N_total |
| Precision | TP / (TP+FP) |
| Recall | TP / (TP+FN) |
| F1-Score | 2·P·R / (P+R) |

## 4. Dataset-Aufteilung

- **Training ~80%**: Modell lernt
- **Validation ~20% des Trainings**: Hyperparameter-Tuning
- **Test (held-out)**: Nur 1× zur finalen Evaluation

## 5. MNIST

- 60 000 Trainings- / 10 000 Testbilder; 28×28 Graustufen
- Shape: `(60000, 28, 28)`; Labels {0,...,9}
- Normalisierung: Pixelwerte ÷ 255 → [0,1]

!!! warning "Loss ≠ Metrik!"
    Loss muss differenzierbar sein (für Backprop). Accuracy ist es nicht — wird nur zur Anzeige verwendet.
