[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

>> Solution

```python

# Define Cohen function
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d


# Distinguish first borns and others

firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

# Cohen's D effect size to quantify the difference between groups based on totalwgt_lb

CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
```

Based on the calculation above, the Cohen's D for first borns bersus others, is -0.088672927072602. 

When comparing first babies' total weight and pregnancy length, Cohen's effect size for pregnancy length is positive while the Cohen's D for total weight between first babies and others is neagtive. When Cohen's D is negative, the direction of the effect is negative meaning, the effect decreases the mean. On the other hand, a positive Cohen's D means that the effect increases the mean. 
