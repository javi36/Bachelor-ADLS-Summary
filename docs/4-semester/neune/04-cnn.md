# 4. CNN — Convolutional Neural Networks

## Motivation

- **Lokale Rezeptivfelder**: Neuron sieht nur Teil des Bildes
- **Geteilte Gewichte**: Gleicher Kernel über gesamtes Bild
- **Translation-Invarianz**: Position-unabhängige Erkennung

## Faltungsoperationen

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

## Parameter einer Conv2D-Schicht

| Parameter | Bedeutung | Keras-Default |
|-----------|-----------|---------------|
| filters | Anzahl Output-Kanäle | — |
| kernel_size | Filtergrösse (z.B. 3×3) | — |
| strides | Schrittweite | 1 |
| padding | 'valid' oder 'same' | 'valid' |

## Output-Grösse (ohne Padding)

```
output = floor((input − kernel) / stride) + 1
```

## Anzahl Parameter (Conv-Schicht)

```
(kernel_h × kernel_w × in_channels + 1) × filters
```

## Pooling

| Typ | Operation |
|-----|-----------|
| Max Pooling | Maximum im Fenster — häufigste Wahl |
| Average Pooling | Mittelwert im Fenster |

## LeNet-5 Architektur

```
Input (32×32×1)
→ Conv2D(6, 5×5, ReLU)    → 28×28×6
→ AvgPool2D(2×2)           → 14×14×6
→ Conv2D(16, 5×5, ReLU)   → 10×10×16
→ AvgPool2D(2×2)           → 5×5×16
→ Flatten → Dense(120) → Dense(84) → Dense(10, Softmax)
```

## Keras-Beispiel

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
