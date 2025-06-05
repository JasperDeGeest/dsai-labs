### HOOFDSTUK 1

### 🔹 `pd.read_csv(filepath)`

**Doel:** Leest een CSV-bestand in als een DataFrame.
**Voorbeeld:**

```python
ais = pd.read_csv('../data/ais.csv')
```

**Output:** DataFrame met rijen en kolommen van het CSV-bestand.

---

### 🔹 `df.shape`

**Doel:** Geeft het aantal rijen en kolommen als tuple `(rijen, kolommen)`.
**Voorbeeld:**

```python
print(ais.shape)
```

**Output:**

```
(202, 14)  # bijv. 202 observaties en 14 variabelen
```

---

### 🔹 `df.info()`

**Doel:** Toont algemene info over het DataFrame, zoals kolomnamen, types en ontbrekende waarden.
**Voorbeeld:**

```python
ais.info()
```

**Output:**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 202 entries, 0 to 201
Columns: 14 entries (bv. sex, age, bmi, ...)
Dtypes: float64 (10), object (2), int64 (2)
```

---

### 🔹 `df.dtypes` en `df.dtypes.value_counts()`

**Doel:** Toont het datatype per kolom en het aantal kolommen per datatype.
**Voorbeeld:**

```python
print(ais.dtypes)
print(ais.dtypes.value_counts())
```

**Output:**

```
sex         object
age        float64
...
float64     10
object       2
int64        2
```

---

### 🔹 `df.set_index('kolom')`

**Doel:** Zet een kolom als index. Niet-destructief zonder `inplace=True`.
**Voorbeeld:**

```python
ais.set_index('id')
```

**Output:** DataFrame met 'id' als rij-index (niet opgeslagen zonder `inplace=True`).

---

### 🔹 `df['kolom'].astype('category')`

**Doel:** Zet een kolom om naar het type "categorisch".
**Voorbeeld:**

```python
ais.sex = ais.sex.astype('category')
```

**Output:** Kolom 'sex' is nu van type category.

---

### 🔹 `df['kolom'].describe()`

**Doel:** Geeft beschrijvende statistiek van een kolom. Werkt voor numeriek en categorisch.
**Voorbeeld:**

```python
ais['ferr'].describe()
```

**Output voor numeriek:**

```
count    202.000000
mean      66.301980
std       73.021859
min        7.000000
max      499.000000
```

---

### 🔹 `df['kolom'].value_counts()`

**Doel:** Tel het aantal voorkomens van elke unieke waarde.
**Voorbeeld:**

```python
ais['sport'].value_counts()
```

**Output:**

```
Basketball    28
Rowing        27
...
```

---

### 🔹 `df['kolom'].unique()`

**Doel:** Toont unieke waarden van een kolom.
**Voorbeeld:**

```python
ais['sex'].unique()
```

**Output:**

```
['f', 'm']
```

---

### 🔹 `df.iloc[]`

**Doel:** Selecteert rijen/kolommen op basis van positie (integers).
**Voorbeelden:**

```python
ais.iloc[1]        # tweede rij
ais.iloc[4:7]      # rijen 5 t.e.m. 7
ais.iloc[:, 5:8]   # kolommen 6 t.e.m. 8
```

**Output:** DataFrame-rij(en) of kolommen met opgegeven positie.

---

### 🔹 `df.loc[]`

**Doel:** Selecteert rijen/kolommen op basis van labels.
**Voorbeeld:**

```python
ais.loc[:, 'pcBfat']
```

**Output:** Reeks met de waarden van kolom 'pcBfat'.

---

### 🔹 `df[voorwaarde]`

**Doel:** Filtert rijen die voldoen aan een conditie.
**Voorbeeld:**

```python
ais[ais['sport'] == 'Netball']
```

**Output:** Subset van DataFrame waar sport gelijk is aan 'Netball'.

---

### 🔹 `df[kolom][voorwaarde]`

**Doel:** Filtert rijen en selecteert 1 kolom.
**Voorbeeld:**

```python
ais.wt[ais['sport'] == 'Netball']
```

**Output:** Reeks met gewichten van Netball-atleten.

---

### 🔹 `df[kolom].value_counts()` (na filtering)

**Doel:** Telt frequentie van waarden in een kolom na filtering.
**Voorbeeld:**

```python
ais.loc[ais['bmi'] > 26, 'sport'].value_counts()
```

**Output:**

```
Basketball    10
Field         7
...
```

### 🔹 `pd.read_csv(filepath, sep='...')`

**Wat het doet:** Laadt een CSV-bestand in, met de mogelijkheid om een ander scheidingsteken dan een komma te gebruiken.
**Voorbeeld:**

```python
android_persistence = pd.read_csv('../data/android_persistence_cpu.csv', sep=';')
```

**Output:** DataFrame met ingelezen gegevens, correct gescheiden op basis van `;`.

---

### 🔹 `CategoricalDtype(categories=[...], ordered=True)`

**Wat het doet:** Maakt een ordinale categorische datatype-definitie, zodat de volgorde van categorieën expliciet wordt vastgelegd.
**Voorbeeld:**

```python
from pandas.api.types import CategoricalDtype
DataSize_type = CategoricalDtype(categories=['Small', 'Medium', 'Large'], ordered=True)
```

---

### 🔹 `df['col'] = df['col'].astype(CategoricalDtype(...))`

**Wat het doet:** Zet een kolom om naar een (ordinaal) categorisch datatype met opgelegde volgorde.
**Voorbeeld:**

```python
android_persistence.DataSize = android_persistence.DataSize.astype(DataSize_type)
```

---

### 🔹 `pd.crosstab(row_var, col_var)`

**Wat het doet:** Maakt een kruistabel (contingentietabel) van twee categorische variabelen.
**Voorbeeld:**

```python
pd.crosstab(android_persistence.PersistenceType, android_persistence.DataSize)
```

**Output:**

| DataSize        | Small | Medium | Large |
| --------------- | ----- | ------ | ----- |
| PersistenceType | x     | y      | z     |


### 🔹 `pd.read_excel(filepath)`

**Wat het doet:** Laadt een Excel-bestand in een DataFrame.
**Voorbeeld:**

```python
df = pd.read_excel('belgian_population.xlsx')
```

---

### 🔹 `CategoricalDtype(categories=[...], ordered=True)`

**Wat het doet:** Maakt een ordinale categorische datatype aan.
**Voorbeeld:**

```python
from pandas.api.types import CategoricalDtype
size_type = CategoricalDtype(categories=['Small', 'Medium', 'Large'], ordered=True)
```

---

### 🔹 `df['col'].astype(CategoricalDtype(...))`

**Wat het doet:** Zet een kolom om naar een ordinale categorische variabele.
**Voorbeeld:**

```python
df['DataSize'] = df['DataSize'].astype(size_type)
```

---

### 🔹 `pd.crosstab(row_var, col_var)`

**Wat het doet:** Maakt een kruistabel (contingentietabel) van twee categorische variabelen.
**Voorbeeld:**

```python
pd.crosstab(df['PersistenceType'], df['DataSize'])
```

---

### 🔹 `df.fillna(0)`

**Wat het doet:** Vervangt alle ontbrekende waarden (NaN) door nul.
**Voorbeeld:**

```python
df = df.fillna(0)
```

---

### 🔹 `df['new_col'] = df[col1] + df[col2] + ...`

**Wat het doet:** Voegt meerdere kolommen samen tot een nieuwe kolom door ze op te tellen.
**Voorbeeld:**

```python
df['Number_of_Women'] = df['Women_Unmarried'] + df['Women_Married'] + ...
```

---

### 🔹 `np.sum(df[col] * df['Age']) / df[col].sum()`

**Wat het doet:** Berekening van het gewogen gemiddelde (vb. gemiddelde leeftijd).
**Voorbeeld:**

```python
avg_age = np.sum(df['Number_of_Women'] * df['Age']) / df['Number_of_Women'].sum()
```


### HOOFDSTUK 2

# --- NumPy ---
np.median(a)                     # Mediaan van array 'a'
np.mean(a)                       # Gemiddelde van array 'a'
np.max(a), np.min(a)            # Maximum / minimum waarde in array
np.quantile(a, q)               # Bereken het q-de percentiel van array 'a'
# voorbeeld: q=0.25 (1e kwartiel), q=0.75 (3e kwartiel)

# --- SciPy ---
stats.iqr(a)                    # Interkwartielafstand (alternatief voor np.quantile)

# --- pandas ---
pd.DataFrame.from_dict(dict)   # Creëert DataFrame uit dictionary

# --- Python standaard ---
l.extend([waarde]*frequentie)   # Herhaal "waarde" x keer en voeg toe aan lijst

# --- Visualisatie-opties gebruikt (niet nieuw, maar herhaald voor volledigheid) ---
plt.hist(data)                  # Histogram
sns.boxplot(x=data)             # Boxplot
sns.violinplot(x=data)          # Violinplot
sns.histplot(data, kde=True)    # Histogram met KDE

## Cheatsheet Statistische Functies in Python (Pandas/Numpy/Scipy)

### 1. `sum()`

* **Wat doet het:** Berekening van de som van waarden.
* **Voorbeeld:**

  ```python
  df['kolom'].sum()
  ```

### 2. `mean()`

* **Wat doet het:** Gemiddelde berekenen.
* **Voorbeeld:**

  ```python
  df['kolom'].mean()
  ```

### 3. `median()`

* **Wat doet het:** Mediaan berekenen.
* **Voorbeeld:**

  ```python
  df['kolom'].median()
  ```

### 4. `mode()`

* **Wat doet het:** Modus (meest voorkomende waarde).
* **Voorbeeld:**

  ```python
  df['kolom'].mode().iloc[0]
  ```

### 5. `min()` / `max()`

* **Wat doet het:** Minimum / maximum waarde bepalen.
* **Voorbeeld:**

  ```python
  df['kolom'].min()
  df['kolom'].max()
  ```

### 6. `quantile()`

* **Wat doet het:** Percentielen berekenen (bijv. kwartielen).
* **Voorbeeld:**

  ```python
  df['kolom'].quantile([0.25, 0.5, 0.75])
  ```

### 7. `var()`

* **Wat doet het:** Variantie berekenen.
* **Voorbeeld:**

  ```python
  df['kolom'].var()
  ```

### 8. `std()`

* **Wat doet het:** Standaardafwijking berekenen.
* **Voorbeeld:**

  ```python
  df['kolom'].std()
  ```

### 9. `skew()`

* **Wat doet het:** Scheefheid van de verdeling.
* **Voorbeeld:**

  ```python
  df['kolom'].skew()
  ```

### 10. `kurtosis()`

* **Wat doet het:** Kurtosis (mate van spitsheid).
* **Voorbeeld:**

  ```python
  df['kolom'].kurtosis()
  ```

### 11. `describe()`

* **Wat doet het:** Statistische samenvatting (count, mean, std, min, max, quartiles).
* **Voorbeeld:**

  ```python
  df['kolom'].describe()
  ```

### 12. `value_counts()`

* **Wat doet het:** Tel frequenties van unieke waarden.
* **Voorbeeld:**

  ```python
  df['kolom'].value_counts()
  ```

### 13. `groupby()` + `agg()`

* **Wat doet het:** Statistiek toepassen per groep.
* **Voorbeeld:**

  ```python
  df.groupby('groep')['kolom'].agg(['mean', 'std'])
  ```

### 14. `scipy.stats.iqr()`

* **Wat doet het:** Interkwartielafstand berekenen.
* **Voorbeeld:**

  ```python
  from scipy import stats
  stats.iqr(df['kolom'])
  ```

### 15. `np.sqrt()`

* **Wat doet het:** Vierkantswortel, gebruikt bij standaardafwijking.
* **Voorbeeld:**

  ```python
  import numpy as np
  np.sqrt(variantie)
  ```
