# Cheat Sheet DSAI

## Basisimports
```python
import numpy as np
import pandas as pd
import scipy.stats as stats
import matplotlib.pyplot as plt
import seaborn as sns
from statsmodels.graphics.mosaicplot import mosaic
from sklearn.linear_model import LinearRegression
from statsmodels.tsa.holtwinters import SimpleExpSmoothing, Holt, ExponentialSmoothing
from statsmodels.tsa.seasonal import seasonal_decompose
```

## Datamanipulatie
```python
df = pd.read_csv('data.csv')                        # Laad data
df['categorie'] = df['categorie'].astype('category')  # Converteer naar categorie
df['datum'] = pd.to_datetime(df['datum'])            # Converteer naar datum

# Data selectie
df.query('leeftijd > 30')                           # Filteren
df.groupby('groep').mean()                          # Groeperen
pd.crosstab(df['kolom1'], df['kolom2'])             # Kruistabel
```

## Univariate 
```python
# Centrummaten
np.mean(data)                                       # Gemiddelde
np.median(data)                                     # Mediaan
stats.mode(data)                                    # Modus

# Spreidingsmaten
np.var(data, ddof=1)                                # Steekproefvariantie (n-1)
np.std(data, ddof=1)                                # Steekproefstandaardafwijking
stats.iqr(data)                                     # Interkwartielafstand
np.ptp(data)                                        # Bereik (max-min)
```

## Toetsen & statistische analyses
### Hypothese-toetsing (H3)
```python
# Z-toets (grote steekproef, σ bekend)
stats.norm.cdf(z_score)                             # P-waarde linkerstaart
stats.norm.sf(z_score)                              # P-waarde rechterstaart
stats.norm.isf(0.95)                                # Kritieke waarde α=0.05

# T-toets (kleine steekproef, σ onbekend)
stats.ttest_1samp(data, popmean=μ0)                 # Eén steekproef t-toets
stats.t.cdf(t_score, df=n-1)                        # P-waarde linkerstaart
stats.t.isf(0.975, df=n-1)                          # Kritieke waarde α=0.05 (tweezijdig)
```

### Kwalitatief vs kwalitatief (H4)
```python
# Chi-kwadraat toets voor onafhankelijkheid
chi2, p, dof, expected = stats.chi2_contingency(observed_table)

# Goodness-of-fit toets
chi2, p = stats.chisquare(f_obs=observed, f_exp=expected)

# Cramér's V berekening
n = observed_table.sum().sum()
k = min(observed_table.shape) - 1
V = np.sqrt(chi2 / (n * k))
```

### Kwalitatief vs kwantitatief (H5)
```python
# Onafhankelijke steekproeven t-toets
stats.ttest_ind(groep1, groep2, equal_var=False)    # Welch's t-toets

# Gepaarde steekproeven t-toets
stats.ttest_rel(voor, na)

# Cohen's d effectgrootte
pooled_std = np.sqrt(((n1-1)*std1**2 + (n2-1)*std2**2) / (n1+n2-2))
cohen_d = (mean1 - mean2) / pooled_std
```

### Kwantitatief vs kwantitatief (H6)
```python
# Lineaire regressie
model = LinearRegression().fit(X.reshape(-1,1), y)
slope = model.coef_[0]
intercept = model.intercept_

# Correlatiecoëfficiënt
r, p_value = stats.pearsonr(x, y)                  # Pearson's r

# Determiantiecoëfficiënt
r_squared = r**2
```

### Tijdreeksanalyse (H7)
```python
# Eenvoudige exponentiële afvlakking
model = SimpleExpSmoothing(data).fit(smoothing_level=α)
forecast = model.forecast(steps)

# Dubbele exponentiële afvlakking (Holt)
model = Holt(data).fit(smoothing_level=α, smoothing_trend=β)

# Drievoudige exponentiële afvlakking (Holt-Winters)
model = ExponentialSmoothing(data, trend='add', seasonal='add', 
                            seasonal_periods=12).fit()

# Seizoensdecompositie
result = seasonal_decompose(data, model='additive', period=12)

# Nauwkeurigheidsmetingen
mae = mean_absolute_error(actual, forecast)
rmse = np.sqrt(mean_squared_error(actual, forecast))
```

## Visualisaties
### Univariate visualisaties
```python
sns.histplot(data, kde=True)                       # Histogram + KDE
sns.boxplot(data)                                   # Boxplot
sns.violinplot(data)                                # Violin plot
```

### Bivariate visualisaties
```python
# Kwalitatief vs kwalitatief
sns.countplot(data=df, x='categorie', hue='groep')  # Gegroepeerd staafdiagram
mosaic(df, ['kolom1', 'kolom2'])                    # Mozaïekplot

# Kwalitatief vs kwantitatief
sns.boxplot(data=df, x='categorie', y='waarde')     # Gegroepeerde boxplot
sns.violinplot(data=df, x='categorie', y='waarde')  # Gegroepeerde violin plot

# Kwantitatief vs kwantitatief
sns.scatterplot(data=df, x='var1', y='var2')        # Spreidingsdiagram
sns.regplot(data=df, x='var1', y='var2')            # Spreidingsdiagram met regressielijn
```

### Tijdreeksvisualisaties
```python
data.plot(title='Tijdreeks')                         # Lijnplot
result.plot()                                        # Decompositieplot
```

## Belangrijkste interpretaties
### Cramér's V (H4)
- 0.0-0.1: Geen associatie
- 0.1-0.25: Zwakke associatie
- 0.25-0.5: Matige associatie
- 0.5: Sterke associatie

### Cohen's d (H5)
- 0.0-0.2: Verwaarloosbaar effect
- 0.2-0.5: Klein effect
- 0.5-0.8: Gemiddeld effect
- 0.8: Groot effect

### Pearson's r (H6)
- ±0.0-0.3: Zeer zwakke correlatie
- ±0.3-0.5: Zwakke correlatie
- ±0.5-0.7: Matige correlatie
- ±0.7-0.9: Sterke correlatie
- ±0.9-1.0: Zeer sterke correlatie
