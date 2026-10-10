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

Rozkład klas w zbiorze danych:  center: 117, left: 607, right: 168, lean left: 172,
lean right: 78** — zbiór jest wyraźnie niezbalansowany, co bezpośrednio
tłumaczy wyniki poniżej.

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
| Accuracy | 60 % |
| Precision (macro) | 78 % |
| Recall (macro) |  33 % |
| F1-score (macro) |  36 % |

### Dlaczego recall (macro) jest tak niski mimo 60% accuracy?

To klasyczny objaw **niezbalansowania klas (class imbalance)**. Klasa
"left" dominuje w zbiorze danych, więc model osiąga wysoki accuracy,
przewidując głównie tę klasę — ale praktycznie ignoruje klasy
mniejszościowe (np. "lean right", "lean left", "right"). Ponieważ recall macro
liczy średnią z recall **każdej klasy z osobna, z jednakową wagą**,
słabe wyniki na klasach mniejszościowych mocno ciągną metrykę w dół,
nawet jeśli tych klas jest niewiele w danych.

**Wyniki klasyfikacji na zbiorze testowym:**
             | precision  |   recall | f1-score  | support |

      center       1.00      0.37      0.54       117
   lean left       0.82      0.13      0.23 |      172
  lean right       1.00      0.04      0.07        78
        left       0.58      0.97      0.72       607
       right       0.51      0.15      0.23       168

    accuracy                           0.60      1142
   macro avg       0.78      0.33      0.36      1142
weighted avg       0.68      0.60      0.51      1142

---

## Wnioski i możliwe usprawnienia

- Model w obecnej formie nie nadaje się do produkcyjnego użycia przy
  klasach mniejszościowych — wymaga adresowania niezbalansowania.
- Możliwe kierunki poprawy:
  - `class_weight='balanced'` w Decision Tree / innym klasyfikatorze
  - Oversampling klas mniejszościowych (np. SMOTE) lub undersampling
    klasy "lean right"
  - Rozważenie uproszczenia do 3 klas (left / center / right) zamiast 5,
    jeśli rozróżnienie "lean left" od "left" nie jest kluczowe biznesowo
  - Test innych klasyfikatorów (Random Forest, Logistic Regression z
    class_weight) — Decision Tree bez ograniczeń głębokości może się
    przeuczać na klasie dominującej

---

## Technologie

- Python 3.x
- pandas, NumPy — przetwarzanie danych
- NLTK / spaCy — przetwarzanie tekstu (tokenizacja, stopwords, stemming)
- scikit-learn — wektoryzacja (TF-IDF, CountVectorizer), klasyfikacja, metryki
- matplotlib — wizualizacja


