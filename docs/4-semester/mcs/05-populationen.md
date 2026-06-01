# 5. 2-Populationen-Modell (Konkurrenz)

```
dN₁/dt = r₁·N₁·(1 − N₁/K₁ − λ₁·N₂/K₁)
dN₂/dt = r₂·N₂·(1 − N₂/K₂ − λ₂·N₁/K₂)
```

- λ₁: Konkurrenzstärke von N₂ auf N₁
- λ₂: Konkurrenzstärke von N₁ auf N₂

## Nullklinen (Isoklinien)

Linie wo dN₁/dt = 0: N₁ = K₁ − λ₁·N₂

## Koexistenz-Bedingungen

| Bedingung | Ergebnis |
|-----------|---------|
| K₁ > K₂/λ₂ && K₂ > K₁/λ₁ | Stabile Koexistenz |
| Beide K kleiner | Instabiles GGW (winner takes all) |
| Nur K₁ > K₂/λ₂ | N₁ gewinnt immer |
