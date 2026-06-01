# MCS — Modellierung komplexer Systeme

**Systemdynamik, ODEs, Logistisches Wachstum, Stabilität, Chaos**

---

## Systemdynamik — Grundelemente

### Grundelemente (Stella / Vensim)

| Element | Symbol | Bedeutung |
|---------|--------|----------|
| Stock (Bestand) | Rechteck | Zustandsgrösse — akkumuliert über Zeit |
| Flow (Fluss) | Doppelpfeil + Ventil | Rate der Änderung des Stocks |
| Converter | Kreis | Hilfsvariable |
| Connector | Pfeil | Informationsfluss |

```
Stock(t + Δt) = Stock(t) + (Inflows − Outflows) · Δt
```

### Rückkopplungsschleifen

- **Positiv (R-Loop / reinforcing)**: Verstärkend → exponentielles Wachstum/Zerfall
- **Negativ (B-Loop / balancing)**: Ausgleichend → strebt zu Gleichgewicht

---

## Numerische Integration (Euler, RK2, RK4)

### Euler-Methode

```
y_{n+1} = y_n + h · f(t_n, y_n)
```

h = Schrittweite. Einfach, aber ungenau — instabil bei grossem h.

### Runge-Kutta 2. Ordnung (Heun)

```
k₁ = f(t_n, y_n)
k₂ = f(t_n + h, y_n + h·k₁)
y_{n+1} = y_n + h/2 · (k₁ + k₂)
```

### Runge-Kutta 4. Ordnung (RK4)

```
k₁ = f(t_n, y_n)
k₂ = f(t_n + h/2, y_n + h/2·k₁)
k₃ = f(t_n + h/2, y_n + h/2·k₂)
k₄ = f(t_n + h, y_n + h·k₃)
y_{n+1} = y_n + h/6 · (k₁ + 2k₂ + 2k₃ + k₄)
```

### Vergleich

| Methode | Lokaler Fehler | Evaluierungen/Schritt |
|---------|---------------|----------------------|
| Euler | O(h²) | 1 |
| RK2 | O(h³) | 2 |
| RK4 | O(h⁵) | 4 — Standard |

---

## Logistisches Wachstum & Fixpunkte

### Logistisches Wachstumsmodell

```
dN/dt = r · N · (1 − N/K)
```

- **r**: intrinsische Wachstumsrate
- **K**: Tragfähigkeit (carrying capacity)

### Analytische Lösung

```
N(t) = K · N₀ · e^{rt} / (K − N₀(1 − e^{rt}))
```

### Fixpunkte & Stabilität

| Fixpunkt | Stabilitätsbedingung |
|---------|---------------------|
| N* = 0 | f'(0) = r > 0 → **instabil** |
| N* = K | f'(K) = −r < 0 → **stabil** |

Stabilitätsanalyse: Linearisierung f'(N*) — negatives Vorzeichen = stabil.

---

## Ernte-Modell & Bifurkation

### Logistisches Wachstum mit Ernte

```
dN/dt = r·N·(1 − N/K) − h·N
```

### Fixpunkte

- N* = 0
- N* = K · (1 − h/r)   [nur real für h < r]

### Stabilitätstabelle

| Bedingung | N*=0 | N*=K(1−h/r) |
|-----------|------|-------------|
| r > h | Instabil | Stabil (Population überlebt) |
| r < h | Stabil | Inexistent (Population kollabiert) |
| r = h | Semi-stabil | Bifurkationspunkt |

!!! tip "Bifurkation"
    **Bifurkation** bei h = r: qualitative Änderung der Systemdynamik (Populationsaussterben bei Überernten).

---

## 2-Populationen-Modell (Konkurrenz)

```
dN₁/dt = r₁·N₁·(1 − N₁/K₁ − λ₁·N₂/K₁)
dN₂/dt = r₂·N₂·(1 − N₂/K₂ − λ₂·N₁/K₂)
```

- λ₁: Konkurrenzstärke von N₂ auf N₁
- λ₂: Konkurrenzstärke von N₁ auf N₂

### Nullklinen (Isoklinien)

Linie wo dN₁/dt = 0: N₁ = K₁ − λ₁·N₂

### Koexistenz-Bedingungen

| Bedingung | Ergebnis |
|-----------|---------|
| K₁ > K₂/λ₂ && K₂ > K₁/λ₁ | Stabile Koexistenz |
| Beide K kleiner | Instabiles GGW (winner takes all) |
| Nur K₁ > K₂/λ₂ | N₁ gewinnt immer |

---

## Chaos & Nichtlineare Systeme

### Duffing-Gleichung (erzwungener Oszillator)

```
ẍ + δẋ + αx + βx³ = γ·cos(ωt)
```

- δ: Dämpfung, α: lineare Federkonstante, β: Nichtlinearität, γ: Antrieb, ω: Antriebsfrequenz

### Chaos-Eigenschaften

- **Sensitivität**: Kleine Unterschiede → grosse Abweichungen
- **Deterministisch aber unvorhersehbar** auf langer Skala
- **Strange Attractor**: Fraktale Struktur im Phasenraum
- **Lyapunov-Exponent > 0**: Exponentielles Auseinanderwachsen

### Bifurkationsdiagramm

Zeigt qualitative Änderungen von Fixpunkten/Zyklen mit Parametern. Klassisch: Periode-Verdopplungs-Route zum Chaos.

---

## Prüfungstipps MCS

!!! tip "Häufige Prüfungsaufgaben"
    1. Fixpunkte berechnen: dN/dt = 0 setzen und lösen
    2. Stabilität: f'(N*) berechnen — negativ = stabil
    3. RK4-Schritt von Hand ausführen (k₁ bis k₄ berechnen)
    4. Bifurkationspunkt identifizieren (Parameter = kritischer Wert)
    5. Stocks, Flows, Feedbackschleifen im Diagramm benennen

!!! warning "Häufige Fehler"
    - Euler instabil bei grossem h — nicht als genau annehmen
    - Fixpunkt-Stabilität aus Wert schliessen (falsch) — aus f' ableiten
    - N* = K(1-h/r) für h>r als real betrachten (→ negativ = nicht existent)
