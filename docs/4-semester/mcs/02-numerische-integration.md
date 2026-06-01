# 2. Numerische Integration (Euler, RK2, RK4)

## 1. Euler-Methode

```
y_{n+1} = y_n + h · f(t_n, y_n)
```

h = Schrittweite. Einfach, aber ungenau — instabil bei grossem h.

## 2. Runge-Kutta 2. Ordnung (Heun)

```
k₁ = f(t_n, y_n)
k₂ = f(t_n + h, y_n + h·k₁)
y_{n+1} = y_n + h/2 · (k₁ + k₂)
```

## 3. Runge-Kutta 4. Ordnung (RK4)

```
k₁ = f(t_n, y_n)
k₂ = f(t_n + h/2, y_n + h/2·k₁)
k₃ = f(t_n + h/2, y_n + h/2·k₂)
k₄ = f(t_n + h, y_n + h·k₃)
y_{n+1} = y_n + h/6 · (k₁ + 2k₂ + 2k₃ + k₄)
```

## 4. Vergleich

| Methode | Lokaler Fehler | Evaluierungen/Schritt |
|---------|---------------|----------------------|
| Euler | O(h²) | 1 |
| RK2 | O(h³) | 2 |
| RK4 | O(h⁵) | 4 — Standard |
