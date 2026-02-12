# Community Matching App

<a href="https://communitymatching.streamlit.app/" class="md-button md-button--primary">Otwórz aplikację na Streamlit Cloud</a>

Aplikacja webowa stworzona w **Streamlit**, wykorzystująca model **unsupervised learning (clustering)** zbudowany w **PyCaret** do grupowania użytkowników na podstawie ich cech demograficznych i preferencji.

Projekt prezentuje pełny pipeline:

- przygotowanie danych  
- trenowanie modelu klasteryzacji  
- zapis modelu  
- inferencję w aplikacji webowej  
- interpretację klastrów  
- wizualizację wyników  

---

## Cel projektu

Celem aplikacji jest pogrupowanie użytkowników oraz przypisanie nowej osoby do najbardziej podobnej grupy na podstawie jej cech.

Użytkownik podaje dane:

- wiek
- poziomu wykształcenia  
- ulubione zwierzę
- preferowane miejsce spędzania czasu  
- płeć

Na podstawie tych danych model przypisuje użytkownika do określonego klastra, a aplikacja prezentuje charakterystykę tej grupy.

---

## **Technologie**

| Narzędzie | Zastosowanie |
| :--- | :--- |
| **Python 3.11** | Język programowania |
| **Streamlit** | Interfejs aplikacji webowej |
| **PyCaret (Clustering)** | Budowa i zapis pipeline ML |
| **Pandas** | Przetwarzanie danych |
| **Plotly Express** | Wizualizacje |
| **JSON** | Przechowywanie nazw i opisów klastrów |
| **CSV** | Dane wejściowe |  

---

## Architektura aplikacji

### 1. Ładowanie modelu

Model klasteryzacji zapisany jako pipeline jest ładowany przy starcie aplikacji:

- `load_model(MODEL_NAME)`  
- wykorzystanie `@st.cache_data` pozwala ograniczyć wielokrotne ładowanie modelu oraz danych, poprawia wydajność aplikacji
---

### 2. Wczytanie danych historycznych

Dane wszystkich uczestników są wczytywane z pliku CSV, a następnie przypisywane do klastrów przy użyciu wytrenowanego modelu:

- `pd.read_csv(DATA, sep=';')`  
- `predict_model(model, data=all_df)`  

Pozwala to analizować strukturę całej populacji w podziale na segmenty.

---

### 3. Predykcja dla nowego użytkownika

Dane z formularza w panelu bocznym są konwertowane do `DataFrame` i przekazywane do modelu:

- `predict_model(model, data=person_df)`  

Model zwraca identyfikator klastra, do którego użytkownik jest najbardziej podobny.

---

### 4. Interpretacja klastra

Każdy klaster posiada:

- nazwę  
- opis semantyczny  

Informacje te są przechowywane w pliku JSON i oddzielone od warstwy modelu, co zwiększa czytelność oraz umożliwia łatwą modyfikację opisów bez zmiany kodu aplikacji.

---

## Wizualizacja wyników

Dla osób należących do tego samego klastra generowane są histogramy przedstawiające:

- rozkład wieku  
- rozkład wykształcenia  
- preferencje dotyczące zwierząt  
- preferencje dotyczące miejsca spędzania czasu  
- rozkład płci  

Wizualizacje tworzone są przy użyciu `Plotly Express`, co umożliwia interaktywną eksplorację danych.

---

## Możliwe rozszerzenia

Projekt można rozbudować o:

- redukcję wymiarowości (PCA) w celu wizualizacji klastrów w 2D  
- porównanie użytkownika z centroidem klastra  
- zapis nowych użytkowników do bazy danych  
- dynamiczne przetrenowanie modelu  
- panel administracyjny z analizą segmentów  
- system rekomendacji oparty na klastrach  

---

## Wartość biznesowa

Rozwiązanie tego typu może być wykorzystane w:

- segmentacji klientów  
- marketingu personalizowanym  
- dopasowywaniu ofert  
- aplikacjach społecznościowych  
- systemach HR  

---

## Podsumowanie

Projekt łączy:

- analizę danych  
- machine learning  
- aplikację webową  
- wizualizację  
- interpretację segmentów  

Stanowi kompletny przykład wdrożenia modelu klasteryzacji w środowisku aplikacji webowej (MVP), demonstrując integrację warstwy analitycznej z warstwą prezentacyjną.
