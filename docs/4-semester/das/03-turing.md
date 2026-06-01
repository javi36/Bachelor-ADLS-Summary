# SW03/04 — Entscheidungsproblem & Turing-Maschinen

## Hilbert-Programm (SW03)

- Ziel: Mathematik auf endlichen Axiomen aufbauen, widerspruchsfrei, vollständig, entscheidbar
- Russells Paradox (1903): Grundlagenkrise der Mathematik
- **Kurt Gödel (1931)**: Formale Systeme mit Arithmetik sind notwendig unvollständig

## Turing-Maschine (SW04)

Alan Turing (1930, Cambridge): "Können die Denkprozesse des Geistes von einer Maschine imitiert werden?"

Turing-Maschine = mathematisches Objekt, kann in Realität nur approximiert werden.

## Komponenten der Turing-Maschine

- **Unendliches Band**: sequentiell geordnete Felder; je ein Symbol aus Alphabet; leere Felder erlaubt
- **Lese-/Schreibkopf**: bewegt sich 1 Feld links oder rechts; liest und überschreibt Symbole
- **Programm**: interne Zustände (Z1, Z2, ..., STOP); Übergänge "X → (Y, Q)"

## Programm-Notation

`"X → (Y, Q)"` bedeutet: Falls Symbol X gelesen, schreibe Y und bewege in Richtung Q (L/R)

## Universal Turing Machine

- Kann Berechnungen aller anderen Turing-Maschinen ausführen
- Programm der zu imitierenden Maschine wird auf dem Band als Input übergeben
- Moderne Computer = **Turing-vollständig**

## Church-Turing-These

!!! quote ""
    "The class of functions computable by a universal Turing machine corresponds to the class of intuitively computable functions."

## Halteproblem (Halting Problem)

Hilbert: "Gibt es ein mechanisches Verfahren, das entscheidet ob ein Programm T_n bei Input m hält?"

```
H(n;m) = 0, falls T_n(m) nicht hält
H(n;m) = 1, falls T_n(m) stoppt
```

**Turings Beweis (1936, Widerspruchsbeweis)**: Eine solche Maschine H kann nicht existieren.

Original-Publikation: *"On computable numbers, with an application to the Entscheidungsproblem"* (1936)

Folge: Das Entscheidungsproblem hat **keine Lösung** — nicht alle mathematischen Aussagen sind maschinell entscheidbar.
