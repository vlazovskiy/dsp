[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

Import the library
```python
import random
```
Define functions
```python
def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
    
def GoalEstimate(lam, m):
    
    estimates = []
    
    for i in range(m):
        estimates.append(SimulateGame(lam))

    print('rmse:', RMSE(estimates, lam))
    print('mean error:', MeanError(estimates, lam))
    
    cdf = thinkstats2.Cdf(estimates)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    print('confidence interval:', ci)
    
    pmf = thinkstats2.Pmf(estimates)
    thinkplot.Hist(pmf)
    thinkplot.Config(xlabel='Goals scored', ylabel='PMF')
```
1. Run tests with different *lam* but fixed *m*

```python
GoalEstimate(2, 1000000)
rmse: 1.41291861054
mean error: -0.000797
confidence interval: (0, 5)
```
<img width="398" alt="fig 16" src="https://user-images.githubusercontent.com/32041665/34930862-8c401646-f980-11e7-880f-15951633f809.png">

```python
GoalEstimate(3, 1000000)
rmse: 1.73152302901
mean error: 0.000154
confidence interval: (1, 6)
```
<img width="405" alt="fig 17" src="https://user-images.githubusercontent.com/32041665/34930881-a4905f94-f980-11e7-8689-c0a9be513cf2.png">

```python
GoalEstimate(4, 1000000)
rmse: 1.99789614345
mean error: 0.000275
confidence interval: (1, 8)
```
<img width="402" alt="fig 18" src="https://user-images.githubusercontent.com/32041665/34930902-b4f35904-f980-11e7-9e3c-89ae4b7e59b6.png">

```python
GoalEstimate(5, 1000000)
rmse: 2.23383481932
mean error: 0.001414
confidence interval: (2, 9)
```
<img width="419" alt="fig 19" src="https://user-images.githubusercontent.com/32041665/34930908-c04a03b6-f980-11e7-933c-496ead89ba6e.png">

The RMSE is increasing with increase in *lam*, and the mean error seems to increase, as well. This makes sense because if the time between goals is exponential and there are too many goals, the fixed match time is simply not enough to accomodate all of the projected goals, which increases the error.

2. Now, I will run the tests with the same *lam* but varying *m*

```python
GoalEstimate(2, 100)
rmse: 1.22065556157
mean error: -0.09
confidence interval: (0, 4)
```
<img width="403" alt="fig 20" src="https://user-images.githubusercontent.com/32041665/34931145-f7f5f260-f981-11e7-87e6-296c5bd17f7d.png">

```python
GoalEstimate(2, 1000)
rmse: 1.45430395722
mean error: 0.017
confidence interval: (0, 5)
```
<img width="411" alt="fig 21" src="https://user-images.githubusercontent.com/32041665/34931149-003921ae-f982-11e7-958d-bc73884c26c6.png">

```python
GoalEstimate(2, 10000)
rmse: 1.42576295365
mean error: -0.0046
confidence interval: (0, 5)
```
<img width="410" alt="fig 22" src="https://user-images.githubusercontent.com/32041665/34931155-0c02ebb4-f982-11e7-89d4-92b5479204b2.png">

```python
GoalEstimate(2, 100)
rmse: 1.4128234143
mean error: 0.00159
confidence interval: (0, 5)
```
<img width="409" alt="fig 23" src="https://user-images.githubusercontent.com/32041665/34931164-144cc24a-f982-11e7-8610-c74846773de6.png">

The mean error is small to begin with and decreases significantly as *m* increases, so this estimator is fairly unbiased.
