[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

>> SOLUTION

```python
class DiffMeansResample(DiffMeansPermute):
    
    def RunModel(self):
        group1 = np.random.choice(self.pool, self.n, replace=True)
        group2 = np.random.choice(self.pool, self.m, replace=True)
        return group1, group2
 
def RunResampleTest(firsts, others):
    data = firsts.prglngth.values, others.prglngth.values
    ht = DiffMeansResample(data)
    p_value = ht.PValue(iters=10000)
    print('\ndiff means resample pregnancy length')
    print('p-value =', p_value)
    print('actual =', ht.actual)
    print('ts max =', ht.MaxTestStat())
    
    data2 = (firsts.totalwgt_lb.dropna().values, 
             others.totalwgt_lb.dropna().values)
    ht = DiffMeansPermute(data2)
    p_value = ht.PValue(iters=10000)
    print('\ndiff means resample birthweight')
    print('p-value =', p_value)
    print('actual =', ht.actual)
    print('ts max =', ht.MaxTestStat())

# Run function
RunResampleTest(firsts, others)
```

### Output
diff means resample pregnancy length

p-value = 0.1628

actual = 0.07803726677754952

ts max = 0.2744886651730454

diff means resample birthweight

p-value = 0.0

actual = 0.12476118453549034

ts max = 0.11238244915618889

## Conclusion
Using resampling instead of permutation does not have a great effect on the results of our testing. There is a slight different but not anything significant enough to choose one or the other.
