# H5 -> 1 kalitatieve variabele en 1 kwantitatieve variabelen - bivariate-qual-quant

## The t-test for independent samples (two-sample t-test)

- vergelijken van het gemiddelde van 2 groepen (niet perse even groot)
- gemiddelde van 2 verschillende groepen
- Groep met placebo en groep met medicijn

```py
# alternative = 'less' -> one-tailed test
#  `alternative='less'` indicates that we want to test for the alternative hypothesis that the mean of the control group is less than the mean of the treatment group.
# alternative = 'two-sided' -> two-tailed test
# alternative = 'greater' -> one-tailed test
control = np.array([91, 87, 99, 77, 88, 91])
treatment = np.array([101, 110, 103, 93, 99, 104])

stats.ttest_ind(a=control, b=treatment,
    alternative='less', equal_var=False)

print(f"T-statistic = {result.statistic}, p-value = {result.pvalue}")

if result.pvalue < 0.05:
    print("Since p < 0.05, we reject the null hypothesis: x scores are significantly lower than y.")
else:
    print("Since p ≥ 0.05, we do not reject the null hypothesis: no significant difference between x and y.")

```

## The t-test for paired samples (paired t-test)

- vergelijken van dingen op dezelfde groep bv
- Voorbeelden
- Voorbeeld zelfde auto met verschillende soorten benzine

```md
      Before and after measurements: Paired samples are often used when you want to compare the measurements of the same variable before and after a treatment or intervention. For example, you might measure the blood pressure of individuals before and after they undergo a specific treatment to see if there is a significant change.

      Matched pairs: Paired samples analysis is useful when you have a natural pairing or matching between the observations in the two data sets. For instance, in a study comparing the effectiveness of two different drugs, you might pair each participant with another participant who has similar characteristics, such as age, gender, or disease severity. Then, you would measure the outcomes for each pair under the different drug conditions.

      Repeated measures: Paired samples can be used when you have multiple measurements taken on the same subject over time or under different conditions. This could include measuring variables like reaction time, performance scores, or pain levels before and after different treatments within the same individuals.
```

```py
# Measurements:
before =   np.array([16, 20, 21, 22, 23, 22, 27, 25, 27, 28])
after = np.array([19, 22, 24, 24, 25, 25, 26, 26, 28, 32])

# Paired t-test with ttest_rel() -> vergeet niet alternative='less' of 'greater' of 'two-sided'
stats.ttest_rel(before, after, alternative='less')

from scipy import stats

result = stats.ttest_rel(cans.AO, cans.AN, alternative='less')

print(f"T-statistic = {result.statistic}, p-value = {result.pvalue}")

if result.pvalue < 0.05:
    print("Since p < 0.05, we reject the null hypothesis: x scores are significantly lower than y.")
else:
    print("Since p ≥ 0.05, we do not reject the null hypothesis: no significant difference between x and y.")

```

## Cohen's d

_Effect size_ is another metric to express the magnitude of the difference between two groups. Several definitions of effect size exist, but one of the most commonly used is _Cohen's $d$_.

```py
def cohen_d(a, b):
    na = len(a)
    nb = len(b)
    pooled_sd = np.sqrt( ((na-1) * a.std(ddof=1)**2 +
                          (nb-1) * b.std(ddof=1)**2) / (na + nb - 2) )
    return (b.mean() - a.mean()) / pooled_sd

cohend = cohen_d(before, after)

print("Cohen's d: ",cohend)

# Interpretation thresholds
if cohend < 0.01:
    interpretation = "Negligible"
elif cohend < 0.2:
    interpretation = "Very small"
elif cohend < 0.5:
    interpretation = "Small"
elif cohend < 0.8:
    interpretation = "Average"
elif cohend < 1.2:
    interpretation = "Large"
elif cohend < 2.0:
    interpretation = "Very large"
else:
    interpretation = "Huge"

print(f"-> {interpretation} effect size")
```
