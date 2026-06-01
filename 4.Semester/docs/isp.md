# ISP — Image & Signal Processing

**SW01–SW14:** Signale · Fourier · Filter · Bildverarbeitung · Segmentierung · Kompression

---

## Teil I: Signalverarbeitung

### Signaltypen & Eigenschaften

#### Signaltypen

| Typ | Zeit | Amplitude | Beispiel |
|-----|------|-----------|---------|
| Analog (kontinuierlich) | Kontinuierlich | Kontinuierlich | Sprachsignal, Temperatur |
| Zeitdiskret | Diskret | Kontinuierlich | Abgetastetes Signal |
| Digital | Diskret | Diskret (quantisiert) | Computer-Audio, Bilddatei |

#### Signaleigenschaften

- **Periodizität:** x(t) = x(t + T) – Signal wiederholt sich mit Periode T
- **Symmetrie gerade:** x(−t) = x(t) → nur Kosinus-Terme in Fourier-Reihe
- **Symmetrie ungerade:** x(−t) = −x(t) → nur Sinus-Terme in Fourier-Reihe
- **Asymptotisches Verhalten:** Konvergiert das Signal gegen einen Grenzwert?
- **Mehrkanalig:** z. B. Stereo-Audio (2 Kanäle), RGB-Bild (3 Kanäle)

#### Sinusoide

```
x(t) = A · cos(2πft + φ) = A · cos(ωt + φ)
ω = 2πf,   T = 1/f,   A = Amplitude,   φ = Phase
```

- cos(t) = sin(t + π/2) – Sinus und Kosinus sind phasenverschobene Versionen desselben Signals
- **Schwebung (Beat):** Überlagerung zweier nahe Frequenzen f₁, f₂ → Amplitudenmodulation mit Frequenz |f₁ − f₂|

#### Einheitssignale

| Signal | Definition | Fourier-Transform |
|--------|-----------|------------------|
| Unit Step u(t) | 0 für t<0 ; 1 für t≥0 | 1/(j2πf) + ½·δ(f) |
| Impuls δ(t) | ∞ bei t=0, ∫δ dt=1 | 1 (alle Frequenzen gleich) |
| rect(t) | 1 für |t|≤½ ; sonst 0 | sinc(f) |

---

### Abtastung & Interpolation

#### Nyquist-Shannon-Abtasttheorem

```
f_s ≥ 2 · f_max
```

- f_s = Abtastfrequenz (Samples/s), f_max = höchste im Signal vorhandene Frequenz
- Abtastperiode: T_s = 1 / f_s
- **Überabtastung (Oversampling):** f_s >> 2·f_max → sicherer, aber mehr Daten
- **Unterabtastung (Undersampling):** f_s < 2·f_max → Aliasing entsteht

!!! warning "Aliasing"
    Hohe Frequenzen falten sich auf niedrige zurück → Anti-Aliasing-Tiefpassfilter *vor* dem Abtasten anwenden!

#### Diskretisierung vs. Quantisierung

| Begriff | Was wird gemacht? |
|---------|------------------|
| Diskretisierung | Zeitachse wird diskret: Abtasten im Zeitbereich |
| Quantisierung | Amplitudenachse wird diskret: Runden auf endliche Bit-Stufen |

#### Interpolation

| Methode | Eigenschaften |
|---------|--------------|
| Nearest-Neighbor | Nächster bekannter Wert; schnell, stufig |
| Linear (1. Ordnung) | Lineare Verbindung; glatt, einfach |
| Kubisch / Spline | Glatter Übergang; bessere Qualität |
| Sinc (ideal) | Theoretisch perfekt; praktisch nicht realisierbar |

!!! tip "Python"
    `scipy.interpolate.interp1d()`, `pd.Series.resample()`

---

### Fourier-Reihen

#### Superpositionsprinzip

Jedes periodische Signal lässt sich als Summe von Sinusoiden darstellen (konstruktive / destruktive Interferenz).

#### Fourier-Reihen-Darstellungen (alle äquivalent)

| Form | Formel | Koeffizienten |
|------|--------|--------------|
| Exponential | x(t) = Σ c_k · e^{j2πkt/T} | c_k = (1/T)∫ x(t)·e^{−j2πkt/T} dt |
| Sinus-Kosinus | x(t) = a₀ + Σ [aₖ cos(2πkt/T) + bₖ sin(2πkt/T)] | a_k, b_k aus Integral |
| Amplituden-Phase | x(t) = A₀ + Σ Aₖ · cos(2πkt/T + φₖ) | Aₖ = 2\|c_k\|, φₖ = ∠c_k |

#### Effekt von Signalsymmetrien auf Koeffizienten

| Symmetrie | Effekt auf Koeffizienten |
|-----------|------------------------|
| Gerade: x(−t)=x(t) | Nur reelle Koeffizienten (nur Kosinus-Terme) |
| Ungerade: x(−t)=−x(t) | Nur imaginäre Koeffizienten (nur Sinus-Terme) |
| Real-wertig | Konjugiert-symmetrisch: c_k = c*_{−k} |

#### Magnitude- & Phasenspektrum

- **Amplitudenspektrum:** |c_k| als Funktion der Frequenz k/T
- **Phasenspektrum:** ∠c_k als Funktion der Frequenz
- DC-Komponente = c₀ = Mittelwert des Signals

---

### Fourier-Transformation

#### Kontinuierliche FT (CTFT)

```
X(f) = ∫ x(t) · e^{−j2πft} dt   (Analyse / Vorwärts)
x(t) = ∫ X(f) · e^{+j2πft} df   (Synthese / Rückwärts)
```

#### Wichtige Eigenschaften

| Eigenschaft | Formel |
|------------|--------|
| Linearität | αx(t) + βy(t) ↔ αX(f) + βY(f) |
| Zeitverschiebung | x(t − t₀) ↔ X(f) · e^{−j2πft₀}  (nur Phase ändert sich!) |
| Skalierung | x(at) ↔ (1/\|a\|)·X(f/a)  (breit im Zeit = schmal in Freq.) |
| Faltungstheorem | (h * x)(t) ↔ H(f) · X(f) |
| Parseval | ∫\|x(t)\|² dt = ∫\|X(f)\|² df  (Energie erhalten) |

#### Wichtige Transformationspaare

| Zeitbereich x(t) | Frequenzbereich X(f) |
|-----------------|---------------------|
| δ(t) | 1 (alle Frequenzen gleich stark) |
| 1 (DC-Signal) | δ(f) |
| cos(2πf₀t) | ½[δ(f−f₀) + δ(f+f₀)] |
| sin(2πf₀t) | j·½[δ(f+f₀) − δ(f−f₀)] |
| rect(t) | sinc(f) |
| Gauss e^{−πt²} | Gauss e^{−πf²} |

#### Fourier-Landschaft (Überblick)

| | Aperiodisch | Periodisch |
|-|------------|-----------|
| **Kontinuierlich** | CTFT | Fourier-Reihe (FS) |
| **Diskret** | DTFT | DFT (endlich, berechenbar) |

!!! tip "Schlüsselprinzip"
    Faltung im Zeitbereich = Multiplikation im Frequenzbereich (und umgekehrt).

---

### DFT, FFT & STFT

#### Diskrete Fourier-Transformation (DFT)

```
X[k] = Σ_{n=0}^{N−1} x[n] · e^{−j2πkn/N}   für k = 0, 1, ..., N−1
```

- N = Anzahl Samples, k = Frequenzindex
- **Frequenzauflösung:** Δf = f_s / N
- Komplexität: O(N²) – bei großem N sehr langsam

#### Fast Fourier Transform (FFT)

- Algorithmische Implementierung der DFT mittels Divide-and-Conquer
- Komplexität: **O(N log N)** statt O(N²) → bei N=1024: ~100× schneller
- FFT ≠ DFT: FFT ist ein *Algorithmus*, DFT ist die *mathematische Transformation*

```python
# Python
scipy.fft.fft(x)
scipy.fft.fftfreq(N, d=1/f_s)
```

#### Short-Time Fourier Transform (STFT)

- FFT auf gleitenden Fenstern → Zeit-Frequenz-Darstellung (Spektrogramm)
- Trade-off: Schmales Fenster = gute Zeitauflösung, schlechte Frequenzauflösung
- Anwendung: Sprachanalyse, Musikerkennung

---

### Faltung & Korrelation

#### Faltung (Convolution)

```
Kontinuierlich:  y(t) = (h * x)(t) = ∫ h(τ) · x(t−τ) dτ
Diskret:         y[n] = Σ_k h[k] · x[n−k]
```

- Interpretation: Spiegeln des Kernels, verschieben und aufsummieren
- h(t) = Impulsantwort → charakterisiert das System vollständig
- Faltungstheorem: h*x ↔ H(ω)·X(ω)

#### Kreuzkorrelation (Cross-Correlation)

```
R_fg(τ) = ∫ f*(t) · g(t+τ) dt   (kein Spiegeln!)
```

- Misst die **Ähnlichkeit** zweier Signale bei Verschiebung τ
- Peak bei τ → beste Ausrichtung; Zeitverzögerungsschätzung

#### Autokorrelation

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

### Filterung

#### Spektrale Filtertypen

| Filter | Passiert | Sperrt | Anwendung |
|--------|---------|--------|----------|
| Tiefpass (LP) | f < f_c | Hohe Freq. | Glätten, Rauschreduktion |
| Hochpass (HP) | f > f_c | Tiefe Freq. | Kantendetektion, Schärfen |
| Bandpass (BP) | f₁ < f < f₂ | Rest | Kommunikation, EEG-Bänder |
| Bandstopp (BS) | alles außer f₁–f₂ | f₁–f₂ | 50-Hz-Netzbrumm entfernen |

!!! warning "Idealer Tiefpass"
    rect im Frequenzbereich → sinc im Zeitbereich → unendlich lang, daher physikalisch *nicht* realisierbar.

#### Fensterfunktionen

| Fenster | Übergangsband | Nebenkeule |
|---------|--------------|-----------|
| Rechteck (Boxcar) | Schmal | Hoch (−13 dB) |
| Hann | Mittel | Niedrig (−31 dB) |
| Hamming | Mittel | Niedrig (−41 dB) |
| Gaussian | Breit | Sehr niedrig |

#### FIR vs. IIR Filter

| | FIR | IIR |
|-|-----|-----|
| Impulsantwort | Endlich lang | Unendlich (Rückkopplung) |
| Phasengang | Linear möglich | Nichtlinear |
| Stabilität | Immer stabil | Kann instabil werden |
| Beispiel | Box-Filter, Gaussian | Butterworth-Filter |

!!! tip "Butterworth"
    IIR-Filter mit maximal flachem Durchlassbereich (kein Ripple). Ordnung bestimmt Steilheit der Flanke.

---

### sinc, Rauschen, Dezibel, Kompression

#### sinc-Funktion

```
sinc(t) = sin(πt) / (πt)    sinc(0) = 1, Nullstellen bei t = ±1, ±2, ...
```

- FT(rect) = sinc → idealer Tiefpass im Zeitbereich ist eine sinc-Funktion
- FT(sinc) = rect → idealer Tiefpass im Frequenzbereich

#### Rauschen

| Modell | Beschreibung |
|--------|-------------|
| Additiv (AWGN) | y(t) = x(t) + n(t); Gauss-Rauschen mit Mittelwert 0 |
| Multiplikativ | y(t) = x(t) · n(t); z. B. Speckle in Ultraschallbildern |
| Salt & Pepper | Zufällige weiße/schwarze Pixel; Median-Filter wirksam |

#### Dezibel-Skala

```
Leistung [dB]:  L = 10 · log₁₀(P / P_ref)
Amplitude [dB]: L = 20 · log₁₀(A / A_ref)
Schalldruck: A_ref = 20 µPa (Hörschwelle)
```

- +3 dB ≈ Leistungsverdopplung; +6 dB ≈ Amplitudenverdopplung
- −3 dB = halbe Leistung = Grenzfrequenz-Definition bei Filtern

#### Kompression (Grundlagen)

| Typ | Methode | Beispiel |
|-----|---------|---------|
| Verlustlos | RLE (Run-Length Encoding) | "WWWWWBBB" → "5W3B"; BMP |
| Verlustlos | Huffman-Coding | Häufige Symbole = kurze Codes; PNG |
| Verlustbehaftet | Diskardierung von Information | JPEG, MP3 |

---

## Teil II: Bildverarbeitung

### Bildrepräsentation & Farbräume

#### Digitale Bilder als Arrays

- Graustufenbild: 2D-Array [Höhe × Breite], Werte 0–255 (uint8)
- Farbbild: 3D-Array [Höhe × Breite × Kanäle]
- Datentypen: uint8 (0–255), uint16, float32 (0.0–1.0)

#### Speicherverbrauch

```
Größe [Bytes] = Breite × Höhe × Kanäle × (Bits_pro_Kanal / 8)
Beispiel: 1920×1080 RGB uint8 = 1920 × 1080 × 3 ≈ 6 MB
```

#### Farbräume

| Farbraum | Kanäle | Anwendung |
|----------|--------|----------|
| RGB | Rot, Grün, Blau | Standard-Anzeige |
| HSV | Hue (Farbton), Saturation, Value | Farbbasierte Segmentierung |
| Lab (CIELAB) | L (Helligkeit), a, b | Farbdistanzmessung, wahrnehmungsgleichmäßig |
| Graustufen | 1 Kanal (Intensität) | Effizienz, viele Algorithmen |

!!! warning "OpenCV = BGR"
    OpenCV liest Bilder als **BGR** (nicht RGB!) → `cv2.cvtColor(img, cv2.COLOR_BGR2RGB)`

#### Bayer-Filter

- Sensor-Muster in Digitalkameras: Jedes Pixel misst nur eine Farbe (R, G oder B)
- Muster RGGB: 50% Grün, je 25% Rot/Blau – entspricht menschlicher Wahrnehmung
- Demosaicing rekonstruiert alle 3 Farbkanäle pro Pixel

---

### Bildqualitäts-Attribute

| Attribut | Beschreibung |
|---------|-------------|
| Auflösung | Anzahl Pixel; Nyquist gilt auch im Bild → Moire-Effekte möglich |
| Quantisierung | Bittiefe; 8 bit = 256 Stufen; mehr Bits = weichere Übergänge |
| Kontrast | Unterschied zwischen hellen und dunklen Bereichen |
| Dynamikbereich | Verhältnis von max. zu min. darstellbarem Wert |
| Belichtung | Über-/Unterbelichtung → Informationsverlust in Lichtern/Schatten |
| Rauschen | Zufällige Intensitätsschwankungen |
| Unschärfe (Blur) | Bewegungsunschärfe, Defokus; hohe Frequenzen gehen verloren |
| Artefakte | JPEG-Blockierung, Aliasing, Moire-Muster |
| Farbtreue | Wie gut entsprechen Farben der Realität? |

#### Qualitätsmetriken

```
SNR = 20 · log₁₀(μ_signal / σ_noise)  [dB]
CNR = (μ_ROI − μ_background) / σ_background
```

---

### Punktoperationen & Histogramme

#### Punktoperationen (pixelweise)

| Operation | Formel | Effekt |
|-----------|--------|--------|
| Invertierung | y = 255 − x | Negativ-Bild |
| Gamma-Korrektur | y = x^γ (normiert); γ<1 hellt auf, γ>1 verdunkelt | Helligkeitsanpassung |
| Kontraststreckung | Lineares Mapping auf [min, max] | Mehr Kontrast |
| Thresholding | y = 255 wenn x>T, sonst 0 | Binarisierung |

#### Histogramm-Operationen

- **Histogram Equalization:** Gleichmäßige Verteilung der Intensitäten → maximaler Kontrast
- **Histogram Matching:** Histogramm an Referenz-Bild anpassen

!!! tip "Python"
    `np.histogram()`, `cv2.equalizeHist()`

---

### Geometrische Transformationen & Affine Matrizen

#### Affine Transformationen

y = A·x + t — Homogene Form (3×3 Matrix, ermöglicht Translation):

```
⎡y₀⎤   ⎡a₀₀  a₀₁  t₀⎤   ⎡x₀⎤
⎢y₁⎥ = ⎢a₁₀  a₁₁  t₁⎥ · ⎢x₁⎥
⎣ 1⎦   ⎣ 0    0    1 ⎦   ⎣ 1⎦
```

#### Wichtige Transformationsmatrizen

| Transformation | Matrix A (2×2 Teil) |
|---------------|---------------------|
| Identität | [[1, 0], [0, 1]] |
| Skalierung (isotrop, s) | [[s, 0], [0, s]] |
| Rotation um φ | [[cos φ, −sin φ], [sin φ, cos φ]] |
| Spiegelung (y-Achse) | [[−1, 0], [0, 1]] |
| Scherung (x) | [[1, sh], [0, 1]] |

!!! warning ""
    Translation ist *keine* lineare Transformation → braucht homogene 3×3 Matrix!

**Composite:** Mehrere Transformationen verketten via A_total = Aₙ · ... · A₂ · A₁ (Reihenfolge beachten!)

#### Interpolation bei geometrischen Transformationen

| Methode | Qualität | Geschwindigkeit |
|---------|---------|----------------|
| Nearest-Neighbor | Niedrig (stufig) | Sehr schnell |
| Bilinear | Mittel | Schnell |
| Bikubisch | Hoch | Langsamer |

!!! tip "Python"
    `cv2.warpAffine()`, `cv2.getRotationMatrix2D()`, `cv2.warpPerspective()`, `cv2.getPerspectiveTransform()`

---

### 2D-Fourier & Spektralfilterung

#### 2D-Fourier-Transformation

```
F(u,v) = ΣΣ f(x,y) · e^{−j2π(ux/M + vy/N)}
```

- Tiefe Frequenzen (Bildmitte nach fftshift) = grobe Strukturen
- Hohe Frequenzen (Bildrand) = Kanten, Details, Rauschen
- Sinus-Gittermuster → punktförmiges Spektrum; Bilder ≈ Superposition solcher Gitter

#### Spektralfilterung im 2D

| Filter | Im Frequenzbereich | Effekt im Bild |
|--------|------------------|----------------|
| Tiefpass (LP) | Kreisförmige Maske, behält Mitte | Weichzeichnen |
| Hochpass (HP) | Maske sperrt Mitte | Kanten betonen |
| Gauss | Gauss-Maske | Glätten ohne Ringing |
| Bandpass / Notch | Ring / einzelne Punkte | Periodische Artefakte entfernen |

!!! tip "Python"
    `scipy.fft.fft2()`, `np.fft.fftshift()`, Maske anlegen, dann `ifft2()`

---

### 2D-Faltung & räumliche Filter

#### 2D-Faltung

```
(f * h)[x,y] = ΣΣ f[x−s, y−t] · h[s,t]
```

- Output-Größe (Valid-Padding): (M − k + 1) × (N − k + 1)
- Faltungstheorem gilt auch in 2D: f * h ↔ F(u,v) · H(u,v)

#### Wichtige 2D-Kernel

| Kernel | Wirkung | Typ |
|--------|---------|-----|
| Box-Filter | Gleichmäßiges Weichzeichnen | Tiefpass |
| Gaussian | Gewichtetes Weichzeichnen, kein Ringing | Tiefpass |
| Sobel x / y | Gradient horizontal / vertikal | Kantendetektion |
| Laplacian | 2. Ableitung, isotropisch | Hochpass |
| LoG | Gauss dann Laplacian, rauschrobuster | Bandpass |
| Unsharp Mask | Original + Hochpassanteil | Schärfen |

!!! tip "Python"
    `cv2.filter2D()`, `scipy.signal.convolve2d()`

!!! tip "CNN-Verbindung"
    CNN-Faltung = technisch 2D-Kreuzkorrelation (Kernel wird nicht gespiegelt).

---

### Kantendetektion

#### Methoden im Überblick

| Methode | Basis | Eigenschaften |
|---------|-------|--------------|
| Sobel | 1. Ableitung (Gradient) | Einfach, rauschempfindlich |
| Prewitt | 1. Ableitung | Ähnlich Sobel, gleichgewichtet |
| Laplacian | 2. Ableitung | Isotropisch, rauschempfindlich |
| LoG (Marr-Hildreth) | Gauss + Laplacian | Rauschrobuster, Zero-Crossings = Kanten |
| Canny | Mehrstufig | State-of-the-art, robusteste Methode |

#### Canny-Algorithmus (4 Schritte)

1. **Gauss-Glättung:** Rauschen reduzieren
2. **Gradient-Berechnung:** Sobel in x und y → Magnitude + Richtung
3. **Non-Maximum Suppression:** Kanten auf 1 Pixel Breite ausdünnen
4. **Hysteresis-Thresholding:** Starke Kanten (T_high) + schwache (T_low) wenn mit starken verbunden

!!! tip "Python"
    `cv2.Sobel()`, `cv2.Canny(img, threshold1, threshold2)`

---

### Feature-Erkennung & SIFT

#### Lokale Features

- Keypoint (Interesse-Punkt) + Deskriptor (lokale Beschreibung)
- Sollen robust sein gegenüber: Skalierung, Rotation, Translation, Beleuchtung
- Anwendungen: Image Registration, Stitching, Objekterkennung

#### SIFT — Scale-Invariant Feature Transform

1. **Scale-Space Extrema Detection:** DoG (Difference of Gaussians) über mehrere Skalen
2. **Keypoint Localization:** Subpixel-Genauigkeit, schwache Punkte verwerfen
3. **Orientation Assignment:** Dominante Gradientenrichtung → Rotationsinvarianz
4. **Feature Descriptor:** 128-dim Vektor aus Gradienten-Histogrammen im 16×16-Patch

#### Feature Matching & Image Registration

1. Features in beiden Bildern erkennen (SIFT / ORB / Harris)
2. Matching: Nearest-Neighbor im Deskriptorenraum + Ratio-Test
3. Geometrisches Modell schätzen (Homographie via RANSAC)
4. Bild transformieren und blenden (Image Stitching)

!!! tip ""
    Weitere Detektoren: Harris Corner Detector, SURF, ORB, HOG

---

### Morphologische Operationen

#### Grundoperationen (auf Binärbildern)

Strukturierendes Element (SE) = kleine Maske, die über das Bild gleitet.

| Operation | Beschreibung | Wirkung |
|-----------|-------------|---------|
| Dilation | Pixel = Vordergrund wenn SE überlappt | Objekte wachsen, Lücken schließen |
| Erosion | Pixel = Vordergrund wenn SE vollständig passt | Objekte schrumpfen, kleine Objekte weg |
| Opening = Erosion + Dilation | Erosion dann Dilation | Rauschen entfernen, Objekte trennen |
| Closing = Dilation + Erosion | Dilation dann Erosion | Löcher füllen, Objekte verbinden |

#### Connected Components

- Zusammenhängende Pixel gleichen Labels
- Attribute: Fläche, Zentroid, Bounding Box, Kontur
- 4-Konnektivität (oben/unten/links/rechts) oder 8-Konnektivität (+Diagonalen)

#### Distance Transform

Für jeden Vordergrundpixel: Distanz zum nächsten Hintergrundpixel → nützlich für Watershed-Segmentierung.

#### Binäre Maskenoperationen

| Operation | Anwendung |
|-----------|----------|
| AND | ROI ausschneiden |
| OR | Masken kombinieren |
| XOR | Unterschiede finden |
| NOT | Maske invertieren |

!!! tip "Python"
    `cv2.erode()`, `cv2.dilate()`, `cv2.morphologyEx()`, `cv2.connectedComponents()`, `cv2.distanceTransform()`

---

### Segmentierung

| Methode | Prinzip | Stärke / Schwäche |
|---------|---------|------------------|
| Globales Thresholding | Fester Schwellwert T | Einfach; versagt bei ungleichmäßiger Beleuchtung |
| Adaptives Thresholding | Lokaler Schwellwert pro Region | Robuster bei variabler Helligkeit |
| Color Clustering (k-Means) | Cluster im Farbraum | Flexibel; Anzahl Cluster muss bekannt sein |
| Watershed | Gradient als Topographie; Fluten von Minima | Gut für berührende Objekte; marker-basiert empfohlen |

!!! tip "Python"
    `cv2.threshold()`, `cv2.adaptiveThreshold()`, `cv2.watershed()`

---

### Dateiformate & JPEG-Kompression

#### Raster- vs. Vektorgrafiken

| Typ | Formate | Eigenschaften |
|-----|---------|--------------|
| Raster | PNG, JPEG, BMP, TIFF, GIF | Pixelbasiert; Qualitätsverlust beim Skalieren |
| Vektor | SVG, PDF, EPS | Kurvenbasiert; beliebig skalierbar ohne Verlust |

#### Bézier-Kurven

- Kurven durch Kontrollpunkte P₀, P₁, ..., Pₙ
- Grad 1: Linie; Grad 2: quadratisch; Grad 3: kubisch (häufigste)
- Kurve berührt nur Start- und Endpunkt; Zwischenpunkte ziehen die Kurve an

#### JPEG-Kompression (5 Schritte)

1. **Farbraumkonversion:** RGB → YCbCr + Chroma-Subsampling (4:2:0)
2. **Aufteilung:** Bild in 8×8-Blöcke
3. **DCT:** Diskrete Kosinus-Transformation → Frequenzkoeffizienten
4. **Quantisierung:** Koeffizienten / Quantisierungsmatrix (verlustbehafteter Schritt!)
5. **Entropy-Coding:** Zigzag-Scan + RLE + Huffman → komprimierter Bitstrom

!!! warning ""
    JPEG ist verlustbehaftet – jedes erneute Speichern verschlechtert Qualität. Für Verarbeitung PNG oder TIFF verwenden!

#### Lossless Kompression

| Methode | Idee | Verwendet in |
|---------|------|------------|
| RLE | Wiederholungen als (Wert, Anzahl) | BMP, unkomprimierte Formate |
| Huffman | Häufige Symbole = kurze Codes | PNG, JPEG-Entropie |
| LZW / Deflate | Wörterbuch-basiert | GIF, ZIP, PNG |

---

### QR-Code

#### Grundlagen

- 2D-Barcode, erfunden 1994 (Toyota/Denso Wave); inspiriert vom japanischen Brettspiel Go
- Kodiert bis ~3000 Zeichen; Versionen 1–40 (Version 1 = 21×21 Pixel)
- ISO-Standard: ISO/IEC 18004

#### Struktur eines QR-Codes

| Komponente | Funktion |
|-----------|---------|
| Positionsmuster (3 Ecken) | Erkennung und Lokalisierung |
| Timing-Markierungen | Definition des Pixelrasters |
| Format-Information | Fehlerkorrekturlevel und Masken-Muster |
| Ausrichtungsmuster | Korrektur von Perspektivverzerrung (ab Version 2) |
| Ruhezone (Quiet Zone) | Weißer Rand für Erkennbarkeit |
| Datenbereiche | Nutzdaten + Fehlerkorrektur-Daten |

#### Fehlerkorrektur

- Reed-Solomon-Codes ermöglichen Rekonstruktion beschädigter Daten
- Level L: 7%, M: 15%, Q: 25%, H: 30% Wiederherstellung möglich
- QR-Codes mit Logo oder leichter Beschädigung können noch gelesen werden

!!! tip "Python"
    `import qrcode; qr.make(data)`

---

## Prüfungstipps ISP

!!! tip "Teil I – Signalverarbeitung"
    1. Nyquist prüfen: f_s ≥ 2·f_max; Aliasing entsteht darunter
    2. Faltungstheorem: Faltung im Zeit = Multiplikation im Frequenzbereich
    3. FFT ≠ DFT: FFT ist O(N log N) Algorithmus; DFT ist die mathematische Operation
    4. Symmetrien: gerades Signal → reelles Spektrum; ungerades → imaginäres
    5. Filtertyp aus Frequenzgang erkennen (LP/HP/BP/BS)
    6. Kreuz- vs. Autokorrelation: Kreuz = Ähnlichkeit zweier Signale; Auto = Periodizität
    7. Dezibel: 20·log₁₀ für Amplitude, 10·log₁₀ für Leistung; −3 dB = Grenzfrequenz

!!! tip "Teil II – Bildverarbeitung"
    1. OpenCV = BGR (nicht RGB!) → `cv2.COLOR_BGR2RGB` nicht vergessen
    2. Speichergröße: B × H × Kanäle × Bytes_pro_Kanal
    3. Output-Größe 2D-Faltung (Valid): (M − k + 1) × (N − k + 1)
    4. Affine 3×3 Matrix in homogenen Koordinaten; Translation = Verschiebungsvektor
    5. Canny = 4 Schritte: Gauss → Gradient → Non-Max-Suppression → Hysteresis
    6. Morphologie: Opening = Rauschen entfernen; Closing = Lücken füllen
    7. JPEG: verlustbehaftet; DCT + Quantisierung → jedes Speichern = Qualitätsverlust
    8. QR-Code: 3 Positionsmuster, Reed-Solomon bis 30% Wiederherstellung

### Wichtige Python-Funktionen

| Funktion | Zweck |
|----------|-------|
| `scipy.fft.fft(x)` | 1D-FFT |
| `scipy.fft.fft2(img)` | 2D-FFT für Bilder |
| `scipy.signal.convolve()` | 1D-Faltung |
| `scipy.signal.correlate()` | 1D-Kreuzkorrelation |
| `scipy.signal.convolve2d()` | 2D-Faltung |
| `cv2.filter2D()` | 2D-Faltung mit Kernel |
| `cv2.Canny()` | Canny Kantendetektion |
| `cv2.watershed()` | Watershed-Segmentierung |
| `cv2.morphologyEx()` | Opening/Closing/Gradient |
| `cv2.connectedComponents()` | Zusammenhängende Komponenten |
| `cv2.warpAffine()` | Affine Transformation |
| `scipy.interpolate.interp1d()` | 1D-Interpolation |
