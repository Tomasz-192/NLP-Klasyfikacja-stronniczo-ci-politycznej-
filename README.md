# NLP-Klasyfikacja-stronniczości-politycznej-


Projekt klasyfikacji tekstów prasowych do 5 klas stronniczości 
politycznej z wykorzystaniem technik NLP i uczenia maszynowego.  
Zrealizowany w ramach studiów podyplomowych **Uczenie Maszynowe 
i Data Science** — Uniwersytet Ekonomiczny w Katowicach (2025).

---

## Problem

Automatyczna klasyfikacja artykułów prasowych do jednej 
z 5 klas stronniczości politycznej:

| Klasa | Opis |
|---|---|
| left | Lewica |
| lean left | Centrum-lewica |
| center | Centrum |
| lean right | Centrum-prawica |
| right | Prawica |

---

## Pipeline NLP

1. **Czyszczenie tekstu** — lowercase, usunięcie cyfr, 
   tagów HTML, znaków interpunkcyjnych, emoji
2. **Tokenizacja** — podział na pojedyncze słowa
3. **Stemming** — PorterStemmer (sprowadzenie do rdzenia)
4. **Usunięcie stopwords** — lista spaCy (en)
5. **Wektoryzacja** — TF-IDF (TfidfVectorizer) 
   oraz CountVectorizer (porównanie metod)
6. **Klasyfikacja** — Decision Tree Classifier
7. **Wizualizacja** — top-15 najważniejszych tokenów 
   per klasa (matplotlib)

---

## Wyniki

| Metryka | Wartość |
|---|---|
| Accuracy | ~% |
| Precision (macro) | ~% |
| Recall (macro) | ~% |

