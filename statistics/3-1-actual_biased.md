[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

First, I am going to import the required libraries and load in the file.

```python
import thinkstats2
import thinkplot

resp = nsfg.ReadFemResp()
```
Now, I am going to count the number of children in families based on the values in NUMKDHH.

```python
d = {}

for num in resp.numkdhh:
    if num not in d:
        d[num] = 1
    else:
        d[num] += 1
```
And create a distribution for them.

```python
pmf = thinkstats2.Pmf(d)
```
Then, I plot the distribution.

```python
thinkplot.Pmf(pmf)
thinkplot.Config(xlabel='children in family', ylabel='PMF')
```
![Fig. 1](https://user-images.githubusercontent.com/32041665/34850333-3dee4cf4-f6da-11e7-99c8-97a649db384e.png) 
<img src="image" width="40%">

Now I am going to use the function provided by the author to calculate the biased distribution:
```python
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
```
And plot the actual and biased distributions together.
```python
pmf = thinkstats2.Pmf(d, label='actual')
biased_pmf = BiasPmf(pmf, label='observed')
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
thinkplot.Show(xlabel='children in family', ylabel='PMF')
```
