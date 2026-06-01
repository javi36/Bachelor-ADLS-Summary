# NLP — Natural Language Processing

## NLP-Aufgaben

| Aufgabe | Beschreibung |
|---------|-------------|
| Dokumentenklassifikation | Text → Kategorie (Spam, Sentiment) |
| Semantische Suche | Ähnlichkeit von Texten |
| Maschinelle Übersetzung | seq2seq: Seq → andere Sprache |
| Sentiment Analysis | positiv / negativ / neutral |
| Named Entity Recognition | Personen, Orte, Organisationen |
| POS-Tagging | Part-of-speech (Nomen, Verb, ...) |
| Textzusammenfassung | Langer Text → kurze Zusammenfassung |
| Textgenerierung | Nächstes Wort vorhersagen |

## Text-Preprocessing Pipeline

1. **Text laden**: Rohdaten als Strings
2. **Tokenisierung**: Text → Liste von Tokens (Wörter/Zeichen)
3. **Vokabular aufbauen**: Tokens → numerische Indizes
4. **Vektorisierung**: Sequenzen numerischer Indizes → Modell-Input

## Python Text-Preprocessing

```python
# Bereinigung: Grossbuchstaben-Header entfernen
sub_lines = [re.sub(r"[A-Z]{2,}", "", line) for line in lines]
# Kleinbuchstaben + Satzzeichen entfernen
sub_lines = [re.sub(r'[^A-Za-z]+', ' ', line).strip().lower()
             for line in sub_lines]
# Leerzeilen entfernen
sub_lines = [line for line in sub_lines if line.strip()]
main_text_lines = sub_lines[16:-287]  # Metadaten abschneiden
```

## TensorFlow tf.data

```python
tf_dataset = tf.data.Dataset.from_tensor_slices(main_text_lines)
for line in tf_dataset.take(4):
    print(line.numpy())
```

`tf.data`: optimierte Datenpipeline für TensorFlow (grosser Datensatz + streaming)
