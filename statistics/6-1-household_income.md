[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

First, import all the required libraries
```python
import pandas as pd
import numpy as np
import thinkstats2
import thinkplot
import hinc
```
Then define all the functions I will be using. All of them are provided by the author with some slight changes by me.
```python
def InterpolateSample(df, log_upper=6.0):
    """Makes a sample of log10 household income.

    Assumes that log10 income is uniform in each range.

    df: DataFrame with columns income and freq
    log_upper: log10 of the assumed upper bound for the highest range

    returns: NumPy array of log10 household income
    """
    # compute the log10 of the upper bound for each range
    df['log_upper'] = np.log10(df.income)

    # get the lower bounds by shifting the upper bound and filling in
    # the first element
    df['log_lower'] = df.log_upper.shift(1)
    df.loc[0, 'log_lower'] = 3.0

    # plug in a value for the unknown upper bound of the highest range
    df.loc[41, 'log_upper'] = log_upper
    
    # use the freq column to generate the right number of values in
    # each range
    arrays = []
    for _, row in df.iterrows():
        vals = np.linspace(row.log_lower, row.log_upper, row.freq)
        arrays.append(vals)

    # collect the arrays into a single sample
    log_sample = np.concatenate(arrays)
    return log_sample

def Median(xs):
    cdf = thinkstats2.Cdf(xs)
    return cdf.Value(0.5)

def PearsonMedianSkewness(xs):
    median = Median(xs)
    mean = RawMoment(xs, 1)
    var = CentralMoment(xs, 2)
    std = math.sqrt(var)
    gp = 3 * (mean - median) / std
    return gp

def CentralMoment(xs, k):
    mean = RawMoment(xs, 1)
    return sum((x - mean)**k for x in xs) / len(xs)

def StandardizedMoment(xs, k):
    var = CentralMoment(xs, 2)
    std = math.sqrt(var)
    return CentralMoment(xs, k) / std**k

def Skewness(xs):
    return StandardizedMoment(xs, 3)

def RawMoment(xs, k):
    return sum(x**k for x in xs) / len(xs)

def Mean(xs):
    return RawMoment(xs, 1)
```
Now read the data
```python
income_df = hinc.ReadData()
```
1. I will look at data with incomes whose upper bound is defined by one million
```python
log_sample = InterpolateSample(income_df, log_upper=6.0)
log_cdf = thinkstats2.Cdf(log_sample)
thinkplot.Cdf(log_cdf)
thinkplot.Config(xlabel='Household income (log $)',
               ylabel='CDF')
```
<img width="401" alt="fig 12" src="https://user-images.githubusercontent.com/32041665/34930090-949f2376-f97c-11e7-9799-bcc7073e6216.png">
```python
sample = np.power(10, log_sample)
cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Household income ($)',
               ylabel='CDF')
```
<img width="404" alt="fig 13" src="https://user-images.githubusercontent.com/32041665/34930097-a3016c30-f97c-11e7-8493-f39f5967d756.png">
Now I will look at the required statistics
```python
Median(sample)
51226.454478940461

Mean(sample)
74278.707531187334

Skewness(sample)
4.9499202444295829

PearsonMedianSkewness(sample)
0.7361258019141782

cdf.Prob(Mean(sample))
0.66000587956687196
```
So 66% of the housholds make less than the mean.

2. Now repeat the same with incomes whose upper bound is defined by one billion
```python
log_sample = InterpolateSample(income_df, log_upper=7.0)
log_cdf = thinkstats2.Cdf(log_sample)
thinkplot.Cdf(log_cdf)
thinkplot.Config(xlabel='Household income (log $)',
               ylabel='CDF')
```
<img width="400" alt="fig 14" src="https://user-images.githubusercontent.com/32041665/34930317-d12c4b10-f97d-11e7-8e02-b6eb3f619ac9.png">
```python
sample = np.power(10, log_sample)
cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Household income ($)',
               ylabel='CDF')
```
<img width="399" alt="fig 15" src="https://user-images.githubusercontent.com/32041665/34930328-dd9104ea-f97d-11e7-965c-7f9be9e80ed9.png">
```python
Median(sample)
51226.454478940461

Mean(sample)
124267.39722164685

Skewness(sample)
11.603690267537793

PearsonMedianSkewness(sample)
0.39156450927742087

cdf.Prob(Mean(sample))
0.8565630665207663
```
So this time 86% of the households make less than the mean.
