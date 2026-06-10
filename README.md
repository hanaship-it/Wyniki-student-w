# Analiza Wpływu Czynników Edukacyjnych i Pozaedukacyjnych na Wyniki Studentów

## 1. Źródło Danych
Dane wykorzystane w projekcie pochodzą z platformy Kaggle: [Student Performance Dataset](https://www.kaggle.com/datasets/nikhil7280/student-performance-multiple-linear-regression). Zbiór zawiera dane o **10 000 studentów** i opisuje różne czynniki wpływające na ich wskaźnik efektywności naukowej.

## 2. Cel Projektu i Opis Zmiennych
Celem projektu było stworzenie modelu uczenia maszynowego zdolnego do przewidywania **wskaźnika wydajności studenta (Performance Index)** na podstawie cech wejściowych (zmiennych niezależnych).

### Zmienna Wynikowa (Cel):
* **Performance Index**: Wskaźnik wydajności nauki studenta (od 10.0 do 100.0).

### Cechy Wejściowe (Zmienne Niezależne):
1. **Hours Studied**: Liczba godzin spędzonych na nauce.
2. **Previous Scores**: Wyniki z poprzednich egzaminów.
3. **Extracurricular Activities**: Udział w zajęciach pozalekcyjnych (Tak/Nie).
4. **Sleep Hours**: Średnia liczba godzin snu na dobę.
5. **Sample Question Papers Practiced**: Liczba rozwiązanych arkuszy egzaminacyjnych.

---

## 3. Zastosowane Metody i Algorytmy
W projekcie zaimplementowano pełen proces przetwarzania danych i budowy modeli (Pipeline) przy użyciu biblioteki `scikit-learn`:
* **Preprocessing**: Skalowanie cech numerycznych (`StandardScaler`) oraz kodowanie zmiennych kategorycznych (`OneHotEncoder` dla zmiennej *Extracurricular Activities*).
* **Modele**: Porównano dwa podejścia:
  1. **Regresja Liniowa (Linear Regression)** – jako model bazowy dla zależności liniowych.
  2. **Las Losowy (Random Forest Regressor)** – jako model nieliniowy, zoptymalizowany za pomocą automatycznego strojenia hiperparametrów (`GridSearchCV`).

---

## 4. Wyniki i Porównanie Modeli
Modele zostały ocenione na zbiorze testowym (20% danych) za pomocą miar **RMSE (Root Mean Squared Error)** oraz **R² (Współczynnik Determinacji)**.

| Model | RMSE | R² (Dokładność) |
| :--- | :---: | :---: |
| **Linear Regression** | ~2.02 | ~0.99 |
| **Random Forest (Tuned)** | ~2.04 | ~0.99 |

### Który model wygrał?
**Regresja Liniowa (Linear Regression)** okazała się minimalnie lepsza lub równorzędna z modelem Lasu Losowego. Wynika to ze specyfiki zbioru danych – analiza macierzy korelacji wykazała potężną, liniową zależność między zmienną `Previous Scores` a `Performance Index` (korelacja wynosząca **0.92**) oraz `Hours Studied` (**0.37**). W przypadku tak silnie liniowych zbiorów danych syntetycznych, prosty model regresji liniowej osiąga idealne dopasowanie bez ryzyka przeuczenia, przewyższając bardziej złożone modele drzewiaste.

---

## 5. Instrukcja Uruchomienia
1. Otwórz notatnik `programowanie.ipynb` w środowisku Google Colab lub Jupyter Notebook.
2. Uruchom komórki po kolei, aby pobrać dane bezpośrednio z Kaggle (wymagany token API Kaggle) lub wczytaj załączony plik `Student_Performance.csv`.
