# 1. Signalverarbeitung

## 1. Signaltypen & Eigenschaften

<div class="pdf-embed">
  <embed src="pdfs/SW01_SignalsAndSampling.pdf" type="application/pdf" width="100%" height="720px">
  <p class="pdf-fallback">PDF nicht ladbar — <a href="pdfs/SW01_SignalsAndSampling.pdf">herunterladen</a></p>
</div>

### Signaltypen

| Typ | Zeit | Amplitude | Beispiel |
|-----|------|-----------|---------|
| Analog (kontinuierlich) | Kontinuierlich | Kontinuierlich | Sprachsignal, Temperatur |
| Zeitdiskret | Diskret | Kontinuierlich | Abgetastetes Signal |
| Digital | Diskret | Diskret (quantisiert) | Computer-Audio, Bilddatei |

### Signaleigenschaften

- **Periodizität:** x(t) = x(t + T) – Signal wiederholt sich mit Periode T
- **Symmetrie gerade:** x(−t) = x(t) → nur Kosinus-Terme in Fourier-Reihe
- **Symmetrie ungerade:** x(−t) = −x(t) → nur Sinus-Terme in Fourier-Reihe
- **Asymptotisches Verhalten:** Konvergiert das Signal gegen einen Grenzwert?
- **Mehrkanalig:** z. B. Stereo-Audio (2 Kanäle), RGB-Bild (3 Kanäle)

### Sinusoide

```
x(t) = A · cos(2πft + φ) = A · cos(ωt + φ)
ω = 2πf,   T = 1/f,   A = Amplitude,   φ = Phase
```

- cos(t) = sin(t + π/2) – Sinus und Kosinus sind phasenverschobene Versionen desselben Signals
- **Schwebung (Beat):** Überlagerung zweier nahe Frequenzen f₁, f₂ → Amplitudenmodulation mit Frequenz |f₁ − f₂|

### Einheitssignale

| Signal | Definition | Fourier-Transform |
|--------|-----------|------------------|
| Unit Step u(t) | 0 für t<0 ; 1 für t≥0 | 1/(j2πf) + ½·δ(f) |
| Impuls δ(t) | ∞ bei t=0, ∫δ dt=1 | 1 (alle Frequenzen gleich) |
| rect(t) | 1 für |t|≤½ ; sonst 0 | sinc(f) |

---

## 2. Abtastung & Interpolation

### Nyquist-Shannon-Abtasttheorem

```
f_s ≥ 2 · f_max
```

- f_s = Abtastfrequenz (Samples/s), f_max = höchste im Signal vorhandene Frequenz
- Abtastperiode: T_s = 1 / f_s
- **Überabtastung (Oversampling):** f_s >> 2·f_max → sicherer, aber mehr Daten
- **Unterabtastung (Undersampling):** f_s < 2·f_max → Aliasing entsteht

!!! warning "Aliasing"
    Hohe Frequenzen falten sich auf niedrige zurück → Anti-Aliasing-Tiefpassfilter *vor* dem Abtasten anwenden!

### Diskretisierung vs. Quantisierung

| Begriff | Was wird gemacht? |
|---------|------------------|
| Diskretisierung | Zeitachse wird diskret: Abtasten im Zeitbereich |
| Quantisierung | Amplitudenachse wird diskret: Runden auf endliche Bit-Stufen |

### Interpolation

| Methode | Eigenschaften |
|---------|--------------|
| Nearest-Neighbor | Nächster bekannter Wert; schnell, stufig |
| Linear (1. Ordnung) | Lineare Verbindung; glatt, einfach |
| Kubisch / Spline | Glatter Übergang; bessere Qualität |
| Sinc (ideal) | Theoretisch perfekt; praktisch nicht realisierbar |

!!! tip "Python"
    `scipy.interpolate.interp1d()`, `pd.Series.resample()`

---

## 3. Fourier-Reihen

<div class="pdf-embed">
  <embed src="pdfs/SW02_FourierSeries.pdf" type="application/pdf" width="100%" height="720px">
  <p class="pdf-fallback">PDF nicht ladbar — <a href="pdfs/SW02_FourierSeries.pdf">herunterladen</a></p>
</div>

### Superpositionsprinzip

Jedes periodische Signal lässt sich als Summe von Sinusoiden darstellen (konstruktive / destruktive Interferenz).

### Fourier-Reihen-Darstellungen (alle äquivalent)

| Form | Formel | Koeffizienten |
|------|--------|--------------|
| Exponential | x(t) = Σ c_k · e^{j2πkt/T} | c_k = (1/T)∫ x(t)·e^{−j2πkt/T} dt |
| Sinus-Kosinus | x(t) = a₀ + Σ [aₖ cos(2πkt/T) + bₖ sin(2πkt/T)] | a_k, b_k aus Integral |
| Amplituden-Phase | x(t) = A₀ + Σ Aₖ · cos(2πkt/T + φₖ) | Aₖ = 2\|c_k\|, φₖ = ∠c_k |

### Effekt von Signalsymmetrien auf Koeffizienten

| Symmetrie | Effekt auf Koeffizienten |
|-----------|------------------------|
| Gerade: x(−t)=x(t) | Nur reelle Koeffizienten (nur Kosinus-Terme) |
| Ungerade: x(−t)=−x(t) | Nur imaginäre Koeffizienten (nur Sinus-Terme) |
| Real-wertig | Konjugiert-symmetrisch: c_k = c*_{−k} |

### Magnitude- & Phasenspektrum

- **Amplitudenspektrum:** |c_k| als Funktion der Frequenz k/T
- **Phasenspektrum:** ∠c_k als Funktion der Frequenz
- DC-Komponente = c₀ = Mittelwert des Signals

---

## 4. Fourier-Transformation

<div class="pdf-embed">
  <embed src="pdfs/SW03_FourierTransformtion.pdf" type="application/pdf" width="100%" height="720px">
  <p class="pdf-fallback">PDF nicht ladbar — <a href="pdfs/SW03_FourierTransformtion.pdf">herunterladen</a></p>
</div>

### Kontinuierliche FT (CTFT)

```
X(f) = ∫ x(t) · e^{−j2πft} dt   (Analyse / Vorwärts)
x(t) = ∫ X(f) · e^{+j2πft} df   (Synthese / Rückwärts)
```

### Wichtige Eigenschaften

| Eigenschaft | Formel |
|------------|--------|
| Linearität | αx(t) + βy(t) ↔ αX(f) + βY(f) |
| Zeitverschiebung | x(t − t₀) ↔ X(f) · e^{−j2πft₀}  (nur Phase ändert sich!) |
| Skalierung | x(at) ↔ (1/\|a\|)·X(f/a)  (breit im Zeit = schmal in Freq.) |
| Faltungstheorem | (h * x)(t) ↔ H(f) · X(f) |
| Parseval | ∫\|x(t)\|² dt = ∫\|X(f)\|² df  (Energie erhalten) |

### Wichtige Transformationspaare

| Zeitbereich x(t) | Frequenzbereich X(f) |
|-----------------|---------------------|
| δ(t) | 1 (alle Frequenzen gleich stark) |
| 1 (DC-Signal) | δ(f) |
| cos(2πf₀t) | ½[δ(f−f₀) + δ(f+f₀)] |
| sin(2πf₀t) | j·½[δ(f+f₀) − δ(f−f₀)] |
| rect(t) | sinc(f) |
| Gauss e^{−πt²} | Gauss e^{−πf²} |

### Fourier-Landschaft (Überblick)

| | Aperiodisch | Periodisch |
|-|------------|-----------|
| **Kontinuierlich** | CTFT | Fourier-Reihe (FS) |
| **Diskret** | DTFT | DFT (endlich, berechenbar) |

!!! tip "Schlüsselprinzip"
    Faltung im Zeitbereich = Multiplikation im Frequenzbereich (und umgekehrt).

---

## 5. DFT, FFT & STFT

### Diskrete Fourier-Transformation (DFT)

```
X[k] = Σ_{n=0}^{N−1} x[n] · e^{−j2πkn/N}   für k = 0, 1, ..., N−1
```

- N = Anzahl Samples, k = Frequenzindex
- **Frequenzauflösung:** Δf = f_s / N
- Komplexität: O(N²) – bei großem N sehr langsam

### Fast Fourier Transform (FFT)

- Algorithmische Implementierung der DFT mittels Divide-and-Conquer
- Komplexität: **O(N log N)** statt O(N²) → bei N=1024: ~100× schneller
- FFT ≠ DFT: FFT ist ein *Algorithmus*, DFT ist die *mathematische Transformation*

```python
# Python
scipy.fft.fft(x)
scipy.fft.fftfreq(N, d=1/f_s)
```

### Short-Time Fourier Transform (STFT)

- FFT auf gleitenden Fenstern → Zeit-Frequenz-Darstellung (Spektrogramm)
- Trade-off: Schmales Fenster = gute Zeitauflösung, schlechte Frequenzauflösung
- Anwendung: Sprachanalyse, Musikerkennung

---

## 6. Faltung & Korrelation

<div class="pdf-embed">
  <embed src="pdfs/SW04_05_Filtering.pdf" type="application/pdf" width="100%" height="720px">
  <p class="pdf-fallback">PDF nicht ladbar — <a href="pdfs/SW04_05_Filtering.pdf">herunterladen</a></p>
</div>

### Faltung (Convolution)

```
Kontinuierlich:  y(t) = (h * x)(t) = ∫ h(τ) · x(t−τ) dτ
Diskret:         y[n] = Σ_k h[k] · x[n−k]
```

- Interpretation: Spiegeln des Kernels, verschieben und aufsummieren
- h(t) = Impulsantwort → charakterisiert das System vollständig
- Faltungstheorem: h*x ↔ H(ω)·X(ω)

### Kreuzkorrelation (Cross-Correlation)

```
R_fg(τ) = ∫ f*(t) · g(t+τ) dt   (kein Spiegeln!)
```

- Misst die **Ähnlichkeit** zweier Signale bei Verschiebung τ
- Peak bei τ → beste Ausrichtung; Zeitverzögerungsschätzung

### Autokorrelation

```
R_xx(τ) = ∫ x*(t) · x(t+τ) dt
```

- Ähnlichkeit eines Signals mit sich selbst → Periodizitätsdetektion
- R_xx(0) = Signalenergie (Maximum)

| | Faltung | Kreuzkorrelation | Autokorrelation |
|-|---------|-----------------|----------------|
| Spiegeln? | Ja | Nein | Nein |
| Zweck | Filter / Systemantwort | Signalvergleich | Periodizität |

!!! tip "Python"
    `scipy.signal.convolve()`, `scipy.signal.correlate()`

---

## 7. Filterung

### Spektrale Filtertypen

| Filter | Passiert | Sperrt | Anwendung |
|--------|---------|--------|----------|
| Tiefpass (LP) | f < f_c | Hohe Freq. | Glätten, Rauschreduktion |
| Hochpass (HP) | f > f_c | Tiefe Freq. | Kantendetektion, Schärfen |
| Bandpass (BP) | f₁ < f < f₂ | Rest | Kommunikation, EEG-Bänder |
| Bandstopp (BS) | alles außer f₁–f₂ | f₁–f₂ | 50-Hz-Netzbrumm entfernen |

!!! warning "Idealer Tiefpass"
    rect im Frequenzbereich → sinc im Zeitbereich → unendlich lang, daher physikalisch *nicht* realisierbar.

### Fensterfunktionen

| Fenster | Übergangsband | Nebenkeule |
|---------|--------------|-----------|
| Rechteck (Boxcar) | Schmal | Hoch (−13 dB) |
| Hann | Mittel | Niedrig (−31 dB) |
| Hamming | Mittel | Niedrig (−41 dB) |
| Gaussian | Breit | Sehr niedrig |

### FIR vs. IIR Filter

| | FIR | IIR |
|-|-----|-----|
| Impulsantwort | Endlich lang | Unendlich (Rückkopplung) |
| Phasengang | Linear möglich | Nichtlinear |
| Stabilität | Immer stabil | Kann instabil werden |
| Beispiel | Box-Filter, Gaussian | Butterworth-Filter |

!!! tip "Butterworth"
    IIR-Filter mit maximal flachem Durchlassbereich (kein Ripple). Ordnung bestimmt Steilheit der Flanke.

---

## 8. sinc, Rauschen, Dezibel, Kompression

### sinc-Funktion

```
sinc(t) = sin(πt) / (πt)    sinc(0) = 1, Nullstellen bei t = ±1, ±2, ...
```

- FT(rect) = sinc → idealer Tiefpass im Zeitbereich ist eine sinc-Funktion
- FT(sinc) = rect → idealer Tiefpass im Frequenzbereich

### Rauschen

| Modell | Beschreibung |
|--------|-------------|
| Additiv (AWGN) | y(t) = x(t) + n(t); Gauss-Rauschen mit Mittelwert 0 |
| Multiplikativ | y(t) = x(t) · n(t); z. B. Speckle in Ultraschallbildern |
| Salt & Pepper | Zufällige weiße/schwarze Pixel; Median-Filter wirksam |

### Dezibel-Skala

```
Leistung [dB]:  L = 10 · log₁₀(P / P_ref)
Amplitude [dB]: L = 20 · log₁₀(A / A_ref)
Schalldruck: A_ref = 20 µPa (Hörschwelle)
```

- +3 dB ≈ Leistungsverdopplung; +6 dB ≈ Amplitudenverdopplung
- −3 dB = halbe Leistung = Grenzfrequenz-Definition bei Filtern

### Kompression (Grundlagen)

| Typ | Methode | Beispiel |
|-----|---------|---------|
| Verlustlos | RLE (Run-Length Encoding) | "WWWWWBBB" → "5W3B"; BMP |
| Verlustlos | Huffman-Coding | Häufige Symbole = kurze Codes; PNG |
| Verlustbehaftet | Diskardierung von Information | JPEG, MP3 |
