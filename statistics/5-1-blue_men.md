[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

For this problem, I am going to import scipy.stats
```python
import scipy.stats
```
And use the function provided by the author
```python
def EvalNormalCdf(x, mu, sigma):
    return scipy.stats.norm.cdf(x, loc=mu, scale=sigma)
```
Now I can define my parameters
```python
mu = 178
sigma = 7.7
min_height = 177.8 # 5'10"
max_height = 185.4 # 6'1"
```
And calculate the answer
```python
EvalNormalCdf(max_height, mu, sigma) - EvalNormalCdf(min_height, mu, sigma)
0.34209468294595308
```
Therefore, 34% of the US male population can join the Blue Man Group.

