# Plots

| **Onafhankelijke** | **Afhankelijke** | **Graf**                           |
| :----------------- | :--------------- | :--------------------------------- |
| Kwalitatief        | Kwalitatief      | Clustered staaf, mozaïek           |
| Kwalitatief        | Kwantitatief     | Boxplot, staaf met errorbars       |
| Kwantitatief       | Kwantitatief     | Spreidingsdiagram, regressierechte |

| **Graf**           | **Code**                                                       |
| :----------------- | :------------------------------------------------------------- |
| Gewone graf        | `df.plot(x= , y= )`                                            |
| Barchart           | `sns.catplot(data= , kind=x, y=)`                              |
| Barchart + error   | `sns.barplot(data=df, x=, y=, errorbar='sd')`                  |
| Clustered barchart | `sns.catplot(data=df, x=, hue=, kind=y)` hue komt uit crosstab |
| Boxplot            | `sns.boxplot(data= , x=)`                                      |
| Histogram          | `sns.displot(x=df['column'])`                                  |
| Kernel density     | `sns.kdeplot(x=df['column'])`                                  |
| His + Kernel       | `sns.displot(x=df['column'], kde=True)`                        |
| Violinplot         | `sns.violinplot(data=df, x=)`                                  |
| Pie chart          | `df['kolom'].value_counts().plot.pie(autopct='%1.1f%%')`       |
| Heatmap            | `sns.heatmap(df.corr(), annot=True)`                           |

## Voorbeelden

```python
# Gewone lijn- of scatterplot
df.plot(x='kolom1', y='kolom2', kind='line')  # of kind='scatter'
plt.show()

# Barchart (categorisch)
sns.catplot(data=df, x='categorie', y='waarde', kind='bar')
plt.show()

# Barchart met errorbars
sns.barplot(data=df, x='categorie', y='waarde', errorbar='sd')
plt.show()

# Clustered barchart
sns.catplot(data=df, x='categorie', hue='groep', y='waarde', kind='bar')
plt.show()

# Boxplot
sns.boxplot(data=df, x='categorie', y='waarde')
plt.show()

# Histogram
sns.displot(x=df['waarde'])
plt.show()

# Kernel density plot
sns.kdeplot(x=df['waarde'])
plt.show()

# Histogram + Kernel density
sns.displot(x=df['waarde'], kde=True)
plt.show()

# Violinplot
sns.violinplot(data=df, x='categorie', y='waarde')
plt.show()

# Pie chart
df['kolom'].value_counts().plot.pie(autopct='%1.1f%%')
plt.show()

# Heatmap van correlatiematrix
sns.heatmap(df.corr(), annot=True)
plt.show()

# Mozaïekdiagram (voor 2 categorische variabelen)
from statsmodels.graphics.mosaicplot import mosaic
mosaic(df, ['kolom1', 'kolom2'])
plt.show()

# Spreidingsdiagram met regressielijn
sns.lmplot(data=df, x='x', y='y')
plt.show()
```

## Combineren van meerdere plots (H7)

```python
# Meerdere plots naast elkaar
fig, axs = plt.subplots(1, 2, figsize=(10, 4))
sns.boxplot(data=df, x='categorie', y='waarde', ax=axs[0])
sns.violinplot(data=df, x='categorie', y='waarde', ax=axs[1])
plt.tight_layout()
plt.show()
```
