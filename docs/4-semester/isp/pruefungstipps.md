# Prüfungstipps ISP

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

## Wichtige Python-Funktionen

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

---

## Abschluss-Zusammenfassung (SW14)

<div class="pdf-embed">
  <embed src="pdfs/SW14_Finale.pdf" type="application/pdf" width="100%" height="720px">
  <p class="pdf-fallback">PDF nicht ladbar — <a href="pdfs/SW14_Finale.pdf">herunterladen</a></p>
</div>
