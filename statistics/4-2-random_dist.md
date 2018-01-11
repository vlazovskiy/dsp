[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

First, I import the libraries I will need:
```python
import numpy as np
import thinkstats2
import thinkplot
```
Then, I will generate an array of random numbers between 0 and 1:
```python
random_numbers = np.random.random(1000)
```
Now, I am going to plot the PMF for this array:
```python
pmf = thinkstats2.Pmf(random_numbers)
thinkplot.Pmf(pmf)
thinkplot.Show(xlabel='random number', ylabel='PMF')
```
<img width="416" alt="fig 3" src="https://user-images.githubusercontent.com/32041665/34853296-d1300f4a-f6e7-11e7-84ba-43a1ff95885e.png">

And also look at the CDF:
```python
cdf = thinkstats2.Cdf(random_numbers)
thinkplot.Cdf(cdf)
thinkplot.Show(xlabel='random number', ylabel='CDF')
```
<img width="401" alt="fig 4" src="https://user-images.githubusercontent.com/32041665/34853299-d570d116-f6e7-11e7-8c29-ef5079fc225a.png">

The ditrsibution usrely looks uniform from both of these graphs!
