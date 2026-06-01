# Teil II: Bildverarbeitung

## Bildrepräsentation & Farbräume

### Digitale Bilder als Arrays

- Graustufenbild: 2D-Array [Höhe × Breite], Werte 0–255 (uint8)
- Farbbild: 3D-Array [Höhe × Breite × Kanäle]
- Datentypen: uint8 (0–255), uint16, float32 (0.0–1.0)

### Speicherverbrauch

```
Größe [Bytes] = Breite × Höhe × Kanäle × (Bits_pro_Kanal / 8)
Beispiel: 1920×1080 RGB uint8 = 1920 × 1080 × 3 ≈ 6 MB
```

### Farbräume

| Farbraum | Kanäle | Anwendung |
|----------|--------|----------|
| RGB | Rot, Grün, Blau | Standard-Anzeige |
| HSV | Hue (Farbton), Saturation, Value | Farbbasierte Segmentierung |
| Lab (CIELAB) | L (Helligkeit), a, b | Farbdistanzmessung, wahrnehmungsgleichmäßig |
| Graustufen | 1 Kanal (Intensität) | Effizienz, viele Algorithmen |

!!! warning "OpenCV = BGR"
    OpenCV liest Bilder als **BGR** (nicht RGB!) → `cv2.cvtColor(img, cv2.COLOR_BGR2RGB)`

### Bayer-Filter

- Sensor-Muster in Digitalkameras: Jedes Pixel misst nur eine Farbe (R, G oder B)
- Muster RGGB: 50% Grün, je 25% Rot/Blau – entspricht menschlicher Wahrnehmung
- Demosaicing rekonstruiert alle 3 Farbkanäle pro Pixel

---

## Bildqualitäts-Attribute

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

### Qualitätsmetriken

```
SNR = 20 · log₁₀(μ_signal / σ_noise)  [dB]
CNR = (μ_ROI − μ_background) / σ_background
```

---

## Punktoperationen & Histogramme

### Punktoperationen (pixelweise)

| Operation | Formel | Effekt |
|-----------|--------|--------|
| Invertierung | y = 255 − x | Negativ-Bild |
| Gamma-Korrektur | y = x^γ (normiert); γ<1 hellt auf, γ>1 verdunkelt | Helligkeitsanpassung |
| Kontraststreckung | Lineares Mapping auf [min, max] | Mehr Kontrast |
| Thresholding | y = 255 wenn x>T, sonst 0 | Binarisierung |

### Histogramm-Operationen

- **Histogram Equalization:** Gleichmäßige Verteilung der Intensitäten → maximaler Kontrast
- **Histogram Matching:** Histogramm an Referenz-Bild anpassen

!!! tip "Python"
    `np.histogram()`, `cv2.equalizeHist()`

---

## Geometrische Transformationen & Affine Matrizen

### Affine Transformationen

y = A·x + t — Homogene Form (3×3 Matrix, ermöglicht Translation):

```
⎡y₀⎤   ⎡a₀₀  a₀₁  t₀⎤   ⎡x₀⎤
⎢y₁⎥ = ⎢a₁₀  a₁₁  t₁⎥ · ⎢x₁⎥
⎣ 1⎦   ⎣ 0    0    1 ⎦   ⎣ 1⎦
```

### Wichtige Transformationsmatrizen

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

### Interpolation bei geometrischen Transformationen

| Methode | Qualität | Geschwindigkeit |
|---------|---------|----------------|
| Nearest-Neighbor | Niedrig (stufig) | Sehr schnell |
| Bilinear | Mittel | Schnell |
| Bikubisch | Hoch | Langsamer |

!!! tip "Python"
    `cv2.warpAffine()`, `cv2.getRotationMatrix2D()`, `cv2.warpPerspective()`, `cv2.getPerspectiveTransform()`

---

## 2D-Fourier & Spektralfilterung

### 2D-Fourier-Transformation

```
F(u,v) = ΣΣ f(x,y) · e^{−j2π(ux/M + vy/N)}
```

- Tiefe Frequenzen (Bildmitte nach fftshift) = grobe Strukturen
- Hohe Frequenzen (Bildrand) = Kanten, Details, Rauschen
- Sinus-Gittermuster → punktförmiges Spektrum; Bilder ≈ Superposition solcher Gitter

### Spektralfilterung im 2D

| Filter | Im Frequenzbereich | Effekt im Bild |
|--------|------------------|----------------|
| Tiefpass (LP) | Kreisförmige Maske, behält Mitte | Weichzeichnen |
| Hochpass (HP) | Maske sperrt Mitte | Kanten betonen |
| Gauss | Gauss-Maske | Glätten ohne Ringing |
| Bandpass / Notch | Ring / einzelne Punkte | Periodische Artefakte entfernen |

!!! tip "Python"
    `scipy.fft.fft2()`, `np.fft.fftshift()`, Maske anlegen, dann `ifft2()`

---

## 2D-Faltung & räumliche Filter

### 2D-Faltung

```
(f * h)[x,y] = ΣΣ f[x−s, y−t] · h[s,t]
```

- Output-Größe (Valid-Padding): (M − k + 1) × (N − k + 1)
- Faltungstheorem gilt auch in 2D: f * h ↔ F(u,v) · H(u,v)

### Wichtige 2D-Kernel

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

## Kantendetektion

### Methoden im Überblick

| Methode | Basis | Eigenschaften |
|---------|-------|--------------|
| Sobel | 1. Ableitung (Gradient) | Einfach, rauschempfindlich |
| Prewitt | 1. Ableitung | Ähnlich Sobel, gleichgewichtet |
| Laplacian | 2. Ableitung | Isotropisch, rauschempfindlich |
| LoG (Marr-Hildreth) | Gauss + Laplacian | Rauschrobuster, Zero-Crossings = Kanten |
| Canny | Mehrstufig | State-of-the-art, robusteste Methode |

### Canny-Algorithmus (4 Schritte)

1. **Gauss-Glättung:** Rauschen reduzieren
2. **Gradient-Berechnung:** Sobel in x und y → Magnitude + Richtung
3. **Non-Maximum Suppression:** Kanten auf 1 Pixel Breite ausdünnen
4. **Hysteresis-Thresholding:** Starke Kanten (T_high) + schwache (T_low) wenn mit starken verbunden

!!! tip "Python"
    `cv2.Sobel()`, `cv2.Canny(img, threshold1, threshold2)`

---

## Feature-Erkennung & SIFT

### Lokale Features

- Keypoint (Interesse-Punkt) + Deskriptor (lokale Beschreibung)
- Sollen robust sein gegenüber: Skalierung, Rotation, Translation, Beleuchtung
- Anwendungen: Image Registration, Stitching, Objekterkennung

### SIFT — Scale-Invariant Feature Transform

1. **Scale-Space Extrema Detection:** DoG (Difference of Gaussians) über mehrere Skalen
2. **Keypoint Localization:** Subpixel-Genauigkeit, schwache Punkte verwerfen
3. **Orientation Assignment:** Dominante Gradientenrichtung → Rotationsinvarianz
4. **Feature Descriptor:** 128-dim Vektor aus Gradienten-Histogrammen im 16×16-Patch

### Feature Matching & Image Registration

1. Features in beiden Bildern erkennen (SIFT / ORB / Harris)
2. Matching: Nearest-Neighbor im Deskriptorenraum + Ratio-Test
3. Geometrisches Modell schätzen (Homographie via RANSAC)
4. Bild transformieren und blenden (Image Stitching)

!!! tip ""
    Weitere Detektoren: Harris Corner Detector, SURF, ORB, HOG

---

## Morphologische Operationen

### Grundoperationen (auf Binärbildern)

Strukturierendes Element (SE) = kleine Maske, die über das Bild gleitet.

| Operation | Beschreibung | Wirkung |
|-----------|-------------|---------|
| Dilation | Pixel = Vordergrund wenn SE überlappt | Objekte wachsen, Lücken schließen |
| Erosion | Pixel = Vordergrund wenn SE vollständig passt | Objekte schrumpfen, kleine Objekte weg |
| Opening = Erosion + Dilation | Erosion dann Dilation | Rauschen entfernen, Objekte trennen |
| Closing = Dilation + Erosion | Dilation dann Erosion | Löcher füllen, Objekte verbinden |

### Connected Components

- Zusammenhängende Pixel gleichen Labels
- Attribute: Fläche, Zentroid, Bounding Box, Kontur
- 4-Konnektivität (oben/unten/links/rechts) oder 8-Konnektivität (+Diagonalen)

### Distance Transform

Für jeden Vordergrundpixel: Distanz zum nächsten Hintergrundpixel → nützlich für Watershed-Segmentierung.

### Binäre Maskenoperationen

| Operation | Anwendung |
|-----------|----------|
| AND | ROI ausschneiden |
| OR | Masken kombinieren |
| XOR | Unterschiede finden |
| NOT | Maske invertieren |

!!! tip "Python"
    `cv2.erode()`, `cv2.dilate()`, `cv2.morphologyEx()`, `cv2.connectedComponents()`, `cv2.distanceTransform()`

---

## Segmentierung

| Methode | Prinzip | Stärke / Schwäche |
|---------|---------|------------------|
| Globales Thresholding | Fester Schwellwert T | Einfach; versagt bei ungleichmäßiger Beleuchtung |
| Adaptives Thresholding | Lokaler Schwellwert pro Region | Robuster bei variabler Helligkeit |
| Color Clustering (k-Means) | Cluster im Farbraum | Flexibel; Anzahl Cluster muss bekannt sein |
| Watershed | Gradient als Topographie; Fluten von Minima | Gut für berührende Objekte; marker-basiert empfohlen |

!!! tip "Python"
    `cv2.threshold()`, `cv2.adaptiveThreshold()`, `cv2.watershed()`

---

## Dateiformate & JPEG-Kompression

### Raster- vs. Vektorgrafiken

| Typ | Formate | Eigenschaften |
|-----|---------|--------------|
| Raster | PNG, JPEG, BMP, TIFF, GIF | Pixelbasiert; Qualitätsverlust beim Skalieren |
| Vektor | SVG, PDF, EPS | Kurvenbasiert; beliebig skalierbar ohne Verlust |

### Bézier-Kurven

- Kurven durch Kontrollpunkte P₀, P₁, ..., Pₙ
- Grad 1: Linie; Grad 2: quadratisch; Grad 3: kubisch (häufigste)
- Kurve berührt nur Start- und Endpunkt; Zwischenpunkte ziehen die Kurve an

### JPEG-Kompression (5 Schritte)

1. **Farbraumkonversion:** RGB → YCbCr + Chroma-Subsampling (4:2:0)
2. **Aufteilung:** Bild in 8×8-Blöcke
3. **DCT:** Diskrete Kosinus-Transformation → Frequenzkoeffizienten
4. **Quantisierung:** Koeffizienten / Quantisierungsmatrix (verlustbehafteter Schritt!)
5. **Entropy-Coding:** Zigzag-Scan + RLE + Huffman → komprimierter Bitstrom

!!! warning ""
    JPEG ist verlustbehaftet – jedes erneute Speichern verschlechtert Qualität. Für Verarbeitung PNG oder TIFF verwenden!

### Lossless Kompression

| Methode | Idee | Verwendet in |
|---------|------|------------|
| RLE | Wiederholungen als (Wert, Anzahl) | BMP, unkomprimierte Formate |
| Huffman | Häufige Symbole = kurze Codes | PNG, JPEG-Entropie |
| LZW / Deflate | Wörterbuch-basiert | GIF, ZIP, PNG |

---

## QR-Code

### Grundlagen

- 2D-Barcode, erfunden 1994 (Toyota/Denso Wave); inspiriert vom japanischen Brettspiel Go
- Kodiert bis ~3000 Zeichen; Versionen 1–40 (Version 1 = 21×21 Pixel)
- ISO-Standard: ISO/IEC 18004

### Struktur eines QR-Codes

| Komponente | Funktion |
|-----------|---------|
| Positionsmuster (3 Ecken) | Erkennung und Lokalisierung |
| Timing-Markierungen | Definition des Pixelrasters |
| Format-Information | Fehlerkorrekturlevel und Masken-Muster |
| Ausrichtungsmuster | Korrektur von Perspektivverzerrung (ab Version 2) |
| Ruhezone (Quiet Zone) | Weißer Rand für Erkennbarkeit |
| Datenbereiche | Nutzdaten + Fehlerkorrektur-Daten |

### Fehlerkorrektur

- Reed-Solomon-Codes ermöglichen Rekonstruktion beschädigter Daten
- Level L: 7%, M: 15%, Q: 25%, H: 30% Wiederherstellung möglich
- QR-Codes mit Logo oder leichter Beschädigung können noch gelesen werden

!!! tip "Python"
    `import qrcode; qr.make(data)`
