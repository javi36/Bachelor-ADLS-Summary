# 5. RNN — Recurrent Neural Networks

## 1. Motivation: Sequentielle Daten

- FNN: gut für tabellarische Daten (i.i.d. Annahme)
- CNN: gut für Bilder (lokale Muster)
- RNN: designed für **sequentielle/temporale Daten** (Zeitreihen, Text)

Sequentielle Daten **verletzen die i.i.d.-Annahme** — aufeinanderfolgende Punkte sind korreliert.

## 2. Zeitreihenvorhersage

- Aufgabe: Vorhersage x_{t+1} aus (x_0, ..., x_t)
- Naives Benchmark-Modell: x̂_{t+1} = x_t
- Autoregressive Modell: ŷ = ax_t + b
- Fenstergrösse τ: Input x_t = (x_t, x_{t-1}, ..., x_{t-τ})

## 3. Latentes Variablenmodell (Hidden State)

```
h_t = f(x_t, h_{t-1})
```

## 4. Einfaches RNN

```
h^t = σ_h(U·x^t + W·h^{t-1})
y^t = σ_out(V·h^t)
```

- U: Gewichte Input → Hidden
- W: Gewichte Hidden → Hidden (Rekurrenz)
- V: Gewichte Hidden → Output

## 5. FNN vs RNN

| Aspekt | FNN | RNN |
|--------|-----|-----|
| Informationsfluss | Nur vorwärts | Auch rückwärts (Feedback) |
| Sequenz | Keine | Ja — Gedächtnis |
| Dynamisches System | Nein | Ja |

## 6. Modell-Annahmen

- **Stationarität**: Dynamik ändert sich nicht über Zeit
- **Markov-Bedingung**: p(x_{t+1}|x_t) — Zukunft hängt nur von unmittelbarer Vergangenheit ab
- **Kausalität**: Zukunft hängt nicht von Zukunft ab
