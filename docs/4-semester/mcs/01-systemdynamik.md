# 1. Systemdynamik — Grundelemente

## Grundelemente (Stella / Vensim)

| Element | Symbol | Bedeutung |
|---------|--------|----------|
| Stock (Bestand) | Rechteck | Zustandsgrösse — akkumuliert über Zeit |
| Flow (Fluss) | Doppelpfeil + Ventil | Rate der Änderung des Stocks |
| Converter | Kreis | Hilfsvariable |
| Connector | Pfeil | Informationsfluss |

```
Stock(t + Δt) = Stock(t) + (Inflows − Outflows) · Δt
```

## Rückkopplungsschleifen

- **Positiv (R-Loop / reinforcing)**: Verstärkend → exponentielles Wachstum/Zerfall
- **Negativ (B-Loop / balancing)**: Ausgleichend → strebt zu Gleichgewicht
