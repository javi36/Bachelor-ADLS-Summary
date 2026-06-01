# Perceptron — Grundlagen & Lernregel

## Perceptron (Rosenblatt 1957)

Binaerer Klassifikator fuer linear trennbare Daten.

```
y = 1, falls w·x + b ≥ 0   |   y = 0, sonst
```

## Lernregel (Gradientenabstieg)

```
w ← w + η · (y_target − y_pred) · x
b ← b + η · (y_target − y_pred)
```

η = Lernrate (typisch 0.01–0.1). Konvergiert **nur** bei linear trennbaren Daten.

## Lineare Trennbarkeit

| Problem | Linear trennbar? | Perceptron loesbar? |
|---------|-----------------|---------------------|
| AND | Ja | Ja |
| OR | Ja | Ja |
| XOR | Nein | Nein — braucht MLP |
