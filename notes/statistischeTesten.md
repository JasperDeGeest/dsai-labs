# 📊 Overzicht van Statistische Tests (Data Science)

Een overzicht van veelgebruikte statistische toetsen in Python voor Data Science, met uitleg wanneer je welke test gebruikt, welke variabelen nodig zijn, en bijpassende functies.

---

## 🤪 1. Eén variabele vs. Referentiewaarde (Gemiddelden)

### ✅ Z-toets (grote steekproef, σ bekend)

* **Situatie**: Je kent de populatiestandaardafwijking (σ) en n > 30.
* **Variabelen**: 1 kwantitatieve variabele.
* **Python**:

  ```python
  z = (x̄ - μ0) / (σ / √n)
  p = stats.norm.cdf(z)  # of sf() voor rechterstaart
  ```

### ✅ T-toets voor één steekproef

* **Situatie**: σ onbekend of kleine steekproef (n ≤ 30)
* **Variabelen**: 1 kwantitatieve variabele.
* **Python**:

  ```python
  stats.ttest_1samp(data, popmean=μ0)
  ```

---

## ⚖️ 2. Twee Groepen Vergelijken (Gemiddelden)

### ✅ Onafhankelijke t-toets (2 groepen)

* **Situatie**: 2 onafhankelijke groepen (bv. man/vrouw)
* **Variabelen**: 1 categorisch (2 waarden), 1 kwantitatief
* **Python**:

  ```python
  stats.ttest_ind(group1, group2, equal_var=False)  # Welch’s t-test
  ```

### ✅ Gepaarde t-toets

* **Situatie**: Pre-post metingen van dezelfde personen
* **Variabelen**: 1 kwantitatieve variabele met 2 metingen
* **Python**:

  ```python
  stats.ttest_rel(before, after)
  ```

### ✅ Effectgrootte (Cohen’s d)

* **Python**:

  ```python
  d = (mean1 - mean2) / pooled_std
  ```
* **Interpretatie**:

  * 0.2: klein
  * 0.5: gemiddeld
  * 0.8: groot

---

## 📉 3. Verband tussen twee numerieke variabelen

### ✅ Pearson correlatie

* **Situatie**: Verband tussen 2 kwantitatieve variabelen
* **Python**:

  ```python
  stats.pearsonr(x, y)
  ```

### ✅ Lineaire regressie

* **Situatie**: Voorspellen van y met x
* **Python**:

  ```python
  model = LinearRegression().fit(X.reshape(-1,1), y)
  ```

---

## 🥮 4. Kwalitatieve vs. Kwalitatieve variabelen

### ✅ Chi-kwadraat onafhankelijkheidstest

* **Situatie**: Verband tussen 2 categorische variabelen
* **Python**:

  ```python
  chi2, p, dof, expected = stats.chi2_contingency(table)
  ```

### ✅ Chi-square goodness-of-fit

* **Situatie**: Vergelijking van verdeling met verwachte verdeling
* **Python**:

  ```python
  stats.chisquare(f_obs, f_exp)
  ```

### ✅ Cramér’s V (effectgrootte)

* **Python**:

  ```python
  V = np.sqrt(chi2 / (n * (min(k, r) - 1)))
  ```
* **Interpretatie**:

  * 0.1: zwak
  * 0.3: matig
  * 0.5: sterk

---

## 🕒 5. Tijdreeksanalyse

### ✅ Simpele exponentiële afvlakking (niveau)

```python
from statsmodels.tsa.holtwinters import SimpleExpSmoothing
model = SimpleExpSmoothing(data).fit(smoothing_level=α)
```

### ✅ Dubbele exponentiële afvlakking (Holt: niveau + trend)

```python
from statsmodels.tsa.holtwinters import Holt
model = Holt(data).fit(smoothing_level=α, smoothing_trend=β)
```

### ✅ Holt-Winters (niveau + trend + seizoen)

```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing
model = ExponentialSmoothing(
    data,
    trend='add',            # of 'mul'
    seasonal='add',         # of 'mul'
    seasonal_periods=12     # bv. maanden in jaar
).fit()
```

### ✅ Decompositie van tijdreeks

```python
from statsmodels.tsa.seasonal import seasonal_decompose
result = seasonal_decompose(data, model='additive', period=12)
```

---

## 📈 6. Visualisaties

* `sns.histplot(data)` – histogram
* `sns.boxplot(x='groep', y='waarde', data=df)` – boxplot per groep
* `sns.scatterplot(x='x', y='y', data=df)` – spreidingsplot
* `sns.regplot(x='x', y='y', data=df)` – met regressielijn
* `mosaic(df, ['cat1', 'cat2'])` – mozaïekplot

---

## 🔑 Samenvatting: Welke test gebruik je wanneer?

| Situatie                                 | Test                        | Python-functie                     |
| ---------------------------------------- | --------------------------- | ---------------------------------- |
| Gemiddelde vs. waarde (σ bekend)         | Z-toets                     | `stats.norm.cdf`, handmatig        |
| Gemiddelde vs. waarde (σ onbekend)       | T-toets (één steekproef)    | `stats.ttest_1samp`                |
| 2 onafh. groepen                         | T-toets onafhankelijk       | `stats.ttest_ind`                  |
| 2 metingen (voor/na)                     | T-toets gepaard             | `stats.ttest_rel`                  |
| 2 categorische variabelen                | Chi² test onafhankelijkheid | `stats.chi2_contingency`           |
| 1 categorische variabele vs. verw. verd. | Chi² goodness-of-fit        | `stats.chisquare`                  |
| Numeriek vs. numeriek                    | Pearson correlatie          | `stats.pearsonr`                   |
| Voorspellen y uit x                      | Lineaire regressie          | `LinearRegression().fit()`         |
| Tijdreeks voorspelling                   | Exponentiële afvlakking     | `SimpleExpSmoothing`, `Holt`, `HW` |

Laat me weten als je er ook ANOVA, Mann-Whitney, of logistische regressie bij wilt!