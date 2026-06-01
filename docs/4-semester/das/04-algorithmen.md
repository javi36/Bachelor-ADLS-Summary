# SW05/06 — Algorithmen & Explore/Exploit

## Multi-Armed Bandit Problem

Wie viel **Exploration** (Neues ausprobieren) vs. **Exploitation** (Bestes nutzen)?

| Strategie | Beschreibung |
|-----------|-------------|
| ε-greedy | Mit Prob. ε erkunden, sonst besten Arm wählen |
| UCB (Upper Confidence Bound) | Unsicherheit explizit berücksichtigen |
| Gittins Index | Optimale Strategie für diskontierte Belohnungen |
| Thompson Sampling | Bayesianisch: Wahrscheinlichkeitsverteilung samplen |

## Sortieralgorithmen

| Algorithmus | Best | Avg | Worst |
|------------|------|-----|-------|
| Bubble Sort | O(n) | O(n²) | O(n²) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) |

Untere Schranke (vergleichsbasiert): O(n·log n)
