# 4. Ernte-Modell & Bifurkation

## Logistisches Wachstum mit Ernte

```
dN/dt = r·N·(1 − N/K) − h·N
```

## Fixpunkte

- N* = 0
- N* = K · (1 − h/r)   [nur real für h < r]

## Stabilitätstabelle

| Bedingung | N*=0 | N*=K(1−h/r) |
|-----------|------|-------------|
| r > h | Instabil | Stabil (Population überlebt) |
| r < h | Stabil | Inexistent (Population kollabiert) |
| r = h | Semi-stabil | Bifurkationspunkt |

!!! tip "Bifurkation"
    **Bifurkation** bei h = r: qualitative Änderung der Systemdynamik (Populationsaussterben bei Überernten).
