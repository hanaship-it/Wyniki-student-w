# Analiza wpływu czynników edukacyjnych i pozaedukacyjnych na wyniki studentów

Głównym celem projektu jest analiza danych i implementacja modeli uczenia maszynowego do przewidywania wyników studentów (regresja).

## 1. Źródło i Opis Danych
Wykorzystany zbiór danych pochodzi z platformy Kaggle: [Student Performance Multiple Linear Regression](https://www.kaggle.com/datasets/nikhil7280/student-performance-multiple-linear-regression). Zbiór początkowo zawierał 10 000 wpisów, a po etapie czyszczenia z duplikatów do modelowania wykorzystano **9873 unikalne wiersze**.

**Cel analizy (Zmienna objaśniana):**
* `Performance Index` - Ostateczny wskaźnik wydajności ucznia (wartość od 10.0 do 100.0).

**Wykorzystane cechy (Zmienne objaśniające):**
1. `Hours Studied` - Liczba godzin nauki.
2. `Previous Scores` - Wyniki z poprzednich testów.
3. `Extracurricular Activities` - Udział w zajęciach pozalekcyjnych (Przekształcono: Yes=1, No=0).
4. `Sleep Hours` - Ilość snu.
5. `Sample Question Papers Practiced` - Liczba wykonanych testów próbnych.

## 2. Etapy Projektu
1. **Pobranie i wczytanie danych** - z użyciem biblioteki `kagglehub` oraz `pandas`.
2. **Czyszczenie danych** - sprawdzenie wartości pustych (`df.info()`) oraz usunięcie ponad 100 zduplikowanych wierszy (`drop_duplicates()`). Przekształcenie danych tekstowych na numeryczne za pomocą metody `.map()`.
3. **Eksploracyjna Analiza Danych (EDA)** - wykorzystanie histogramów do zbadania rozkładów zmiennych oraz mapy cieplnej (Heatmap) do analizy korelacji.
4. **Przygotowanie modeli (Pipeline)** - wykorzystanie `StandardScaler` do ujednolicenia skal zmiennych. Podział danych na zbiór treningowy (80%) i testowy (20%).
5. **Walidacja krzyżowa (Cross-Validation)** - wstępna ocena 3 różnych algorytmów tylko na danych treningowych.
6. **Strojenie Hiperparametrów** - użycie `GridSearchCV` w celu poszukiwania optymalnych parametrów dla Lasu Losowego.
7. **Ostateczna Ewaluacja** - test najlepszego modelu na wyizolowanym zbiorze testowym.

## 3. Zastosowane Modele i Wyniki
W trakcie eksperymentów przetestowano:
* **Linear Regression** (Regresja Liniowa)
* **Decision Tree Regressor** (Drzewo Decyzyjne)
* **Random Forest Regressor** (Las Losowy)

### Który model wygrał?
**Zwycięzcą okazała się Regresja Liniowa.** W trakcie walidacji krzyżowej i testowania, skomplikowane algorytmy (jak optymalizowany przez Grid Search Las Losowy, który osiągnął błąd RMSE = 2.25) nie były w stanie pokonać prostego modelu matematycznego. 

Ostateczne wyniki Regresji Liniowej na zbiorze testowym:
* **Błąd modelu (RMSE):** 2.08 punktów (model myli się średnio tylko o ~2 punkty na 100 możliwych).
* **Dokładność (R2):** 0.988 (98.8% zmienności wyników zostało wyjaśnione przez model).

## 4. Główne Wnioski
Największy wpływ na wynik końcowy mają **wcześniejsze oceny** (korelacja 0.92) oraz **czas poświęcony na naukę** (korelacja 0.37). Pozostałe czynniki, takie jak sen czy zajęcia pozalekcyjne, w analizowanym zbiorze danych nie miały istotnego wpływu statystycznego. Ze względu na wybitnie liniową zależność najważniejszych cech, model Regresji Liniowej okazał się optymalnym, najszybszym i najdokładniejszym wyborem.
