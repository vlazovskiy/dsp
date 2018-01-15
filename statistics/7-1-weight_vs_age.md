[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

First, I will import the  libraries
```python
import numpy as np
import pandas as pd
import brfss
import thinkstats2
import thinkplot
import first
```
Then import the database
```python
live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])
```
Now I can do some plotting
```python
thinkplot.Scatter(live.agepreg, live.totalwgt_lb)
thinkplot.Show(xlabel="mother's age",
               ylabel="child's birth weight",
               legend=False)
```
<img width="393" alt="fig 5" src="https://user-images.githubusercontent.com/32041665/34922970-92f987c2-f94b-11e7-8757-a221e362c894.png">

The image is a little too crowded, so I am going to reduce the saturation
```python
thinkplot.Scatter(live.agepreg, live.totalwgt_lb, alpha=0.02)
thinkplot.Show(xlabel="mother's age",
               ylabel="child's birth weight",
               legend=False)
```
<img width="399" alt="fig 6" src="https://user-images.githubusercontent.com/32041665/34922980-dcf39b10-f94b-11e7-904b-2834e80635dd.png">

It is still a bit too crowded, so I will look at another graph
```python
thinkplot.HexBin(live.agepreg, live.totalwgt_lb)
thinkplot.Show(xlabel="mother's age",
               ylabel="child's birth weight",
               legend=False)
```
<img width="397" alt="fig 7" src="https://user-images.githubusercontent.com/32041665/34922991-12594cc8-f94c-11e7-9cc7-2088ea079e5c.png">

Now, I am going to plot the percentiles with the code the author provided in his text
```python
bins = np.arange(10, 45, 5)
indices = np.digitize(live.agepreg, bins)
groups = live.groupby(indices)

ages = [group.agepreg.mean() for i, group in groups]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups]

for percent in [75, 50, 25]:
    weights = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(ages, weights, label=label)
    
thinkplot.Show(xlabel='age',
               ylabel='birth weight',
               legend=True)  
```
<img width="403" alt="fig 8" src="https://user-images.githubusercontent.com/32041665/34923011-60530c66-f94c-11e7-8925-45e5e0fed866.png">

Now I will use the author's function definitions
```python
def Cov(xs, ys, meanx=None, meany=None):
    xs = np.asarray(xs)
    ys = np.asarray(ys)

    if meanx is None:
        meanx = np.mean(xs)
    if meany is None:
        meany = np.mean(ys)

    cov = np.dot(xs-meanx, ys-meany) / len(xs)
    return cov
    
def Corr(xs, ys):
    xs = np.asarray(xs)
    ys = np.asarray(ys)

    meanx, varx = thinkstats2.MeanVar(xs)
    meany, vary = thinkstats2.MeanVar(ys)

    corr = Cov(xs, ys, meanx, meany) / np.sqrt(varx * vary)
    return corr
    
def SpearmanCorr(xs, ys):
    xranks = pd.Series(xs).rank()
    yranks = pd.Series(ys).rank()
    return Corr(xranks, yranks)
```
And calculate Pearson's and Spearman's rank correlation
```python
Pearson = Corr(live.agepreg, live.totalwgt_lb)
Pearson
0.068833970354109097
```
```python
Spearman = SpearmanCorr(live.agepreg, live.totalwgt_lb)
Spearman
0.094610041096582262
```
Both the scatterplots and the correlation coefficient show a very weak relationship between these two variable, almost non-existent. That makes sense because medically speaking the weight of the child should not depend on the mother's age.
