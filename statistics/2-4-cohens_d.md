[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

>> First, I am going to copy the code the author provided in his text.
>> ```python
import numpy as np
import math
import nsfg

preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

def CohenEffectSize(group1, group2):
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / math.sqrt(pooled_var)
    return d
```
>> Now, I am going to do my investigation.
>> ```python
print(firsts.totalwgt_lb.mean())
7.201094430437772
print(others.totalwgt_lb.mean())
7.325855614973262
```
>> I can see that first babies are generally lighter.
>> Now, I am going to calculate Cohen's d for firsts abd others:
>> ```python
CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
-0.088672927072602
```
>> The value is negative because, as I have noted, first babies are lighter than others on average.
>> The absolute value of Cohen's d in this case is 0.09, which is one order bigger than the 0.029 Cohen's d for pregnancy length between first and other babies. 
