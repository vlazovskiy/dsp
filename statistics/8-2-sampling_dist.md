[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

First import the libraries
```python
import thinkstats2
import thinkplot
```
Now use the author's code to define a simulator function 
```python
def SimulateSample(n, lam=2, m=1000):
    
    estimates = []
    for i in range(m):
        xs = np.random.exponential(1.0/lam, n)
        l = 1 / np.mean(xs)
        estimates.append(l)
        
    stderr = RMSE(estimates, lam)
    print('standard error:', stderr)    

    cdf = thinkstats2.Cdf(estimates)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    print('confidence interval:', ci)
    
    thinkplot.Cdf(cdf)
    thinkplot.Config(xlabel='estimate',
                     ylabel='CDF')
```
And plot the sampling distribution of the estimate, compute the standard error of the estimate, and the 90% confidence interval for n=10
```python
SimulateSample(10)
standard error: 0.801273176312
confidence interval: (1.2710805622721233, 3.7508641276186747)
```
<img width="397" alt="fig 9" src="https://user-images.githubusercontent.com/32041665/34924847-b5c353a0-f95a-11e7-9ade-8bca85b9cce6.png">

Now I am going to define a different function to play with the values of n
```python
def SimulateSampleVsSampleSize(n, lam=2, m=1000):
    
    estimates = []
    for i in range(m):
        xs = np.random.exponential(1.0/lam, n)
        l = 1 / np.mean(xs)
        estimates.append(l)
        
    stderr = RMSE(estimates, lam)
    
    return stderr
```
Then I define a range for sample sizes and calculate the standard errors for every sample size in this range to plot a graph
```python
sample_sizes = range(10, 1000, 25)
standard_errors = []

for n in sample_sizes:
    standard_errors.append(SimulateSampleVsSampleSize(n))
    
thinkplot.Scatter(sample_sizes, standard_errors)
thinkplot.Show(xlabel="sample size",
               ylabel="standard error")
```
<img width="396" alt="fig 10" src="https://user-images.githubusercontent.com/32041665/34925068-d895f9d6-f95b-11e7-917e-f931d6b9e98f.png">

Expectedly, the standard error decreases as the sample size increases. 
With n=1000 the CDF is a perfect sigmoid.
```python
SimulateSample(1000)
standard error: 0.0641515610198
confidence interval: (1.9010066585341892, 2.1134819176104545)
```
<img width="393" alt="fig 11" src="https://user-images.githubusercontent.com/32041665/34925183-9343b502-f95c-11e7-8599-70bdbfb91611.png">
