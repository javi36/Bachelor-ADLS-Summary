# 3. Logistisches Wachstum & Fixpunkte

## Logistisches Wachstumsmodell

```
dN/dt = r · N · (1 − N/K)
```

- **r**: intrinsische Wachstumsrate
- **K**: Tragfähigkeit (carrying capacity)

## Analytische Lösung

```
N(t) = K · N₀ · e^{rt} / (K − N₀(1 − e^{rt}))
```

## Fixpunkte & Stabilität

| Fixpunkt | Stabilitätsbedingung |
|---------|---------------------|
| N* = 0 | f'(0) = r > 0 → **instabil** |
| N* = K | f'(K) = −r < 0 → **stabil** |

Stabilitätsanalyse: Linearisierung f'(N*) — negatives Vorzeichen = stabil.
