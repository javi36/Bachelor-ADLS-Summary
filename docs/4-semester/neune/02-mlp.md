# MLP — Multilayer Perceptron & Backpropagation

## Kuenstliches Neuron

```
y_i = σ( Σ_j w_{ij} · x_j + b_i )
```

## Aktivierungsfunktionen

| Funktion | Formel | Einsatz |
|----------|--------|---------|
| Sigmoid | 1 / (1+e^{-x}) | Binaerer Output |
| ReLU | max(0, x) | Hidden Layers (Standard) |
| Tanh | (e^x−e^{-x})/(e^x+e^{-x}) | Hidden Layers |
| Softmax | e^{x_i} / Σ e^{x_j} | Multi-Klassen Output |

## Backpropagation

1. Forward Pass: Vorhersage berechnen
2. Loss berechnen: L(y_pred, y_true)
3. Gradienten via Kettenregel: ∂L/∂w
4. Gewichte: w ← w − η · ∂L/∂w
