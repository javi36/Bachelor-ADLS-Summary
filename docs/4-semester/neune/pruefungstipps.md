# Prüfungstipps NeuNe

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
