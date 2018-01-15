[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

Import the library
```python
import thinkstats2
```
Define classes
```python
class HypothesisTest(object):

    def __init__(self, data):
        self.data = data
        self.MakeModel()
        self.actual = self.TestStatistic(data)

    def PValue(self, iters=1000):
        self.test_stats = [self.TestStatistic(self.RunModel()) 
                           for _ in range(iters)]

        count = sum(1 for x in self.test_stats if x >= self.actual)
        return count / iters

    def TestStatistic(self, data):
        raise UnimplementedMethodException()

    def MakeModel(self):
        pass

    def RunModel(self):
        raise UnimplementedMethodException()
        
class DiffMeansPermute(thinkstats2.HypothesisTest):

    def TestStatistic(self, data):
        group1, group2 = data
        test_stat = abs(group1.mean() - group2.mean())
        return test_stat

    def MakeModel(self):
        group1, group2 = self.data
        self.n, self.m = len(group1), len(group2)
        self.pool = np.hstack((group1, group2))

    def RunModel(self):
        np.random.shuffle(self.pool)
        data = self.pool[:self.n], self.pool[self.n:]
        return data
        
 class DiffMeansResample(DiffMeansPermute):
    
    def RunModel(self):
        resample1 = np.random.choice(self.pool, self.n, replace=True)
        resample2 = np.random.choice(self.pool, self.m, replace=True)
        return resample1, resample2
```
Define parameters and data
```python
iters = 10000
data_prglngth = firsts.prglngth.values, others.prglngth.values
data_totalwgt = firsts.totalwgt_lb, others.totalwgt_lb
```
Do the pregnancy length comparison
```python
ht = DiffMeansResample(data_prglngth)
pvalue = ht.PValue(iters)
print('p-value:', pvalue)
print('actual:', ht.actual)
p-value: 0.1651
actual: 0.0780372667775

ht = DiffMeansPermute(data_prglngth)
pvalue = ht.PValue(iters)
print('p-value:', pvalue)
print('actual:', ht.actual)
p-value: 0.1731
actual: 0.0780372667775
```
And birth weight comparison
```python
ht = DiffMeansResample(data_totalwgt)
pvalue = ht.PValue(iters)
print('p-value:', pvalue)
print('actual:', ht.actual)
p-value: 0.0
actual: 0.12476118453549034

ht = DiffMeansPermute(data_totalwgt)
pvalue = ht.PValue(iters)
print('p-value:', pvalue)
print('actual:', ht.actual)
p-value: 0.0
actual: 0.12476118453549034
```
Turns out in this case the difference between the results of these two models is very insignificant, virtually non-existent.
