[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

>> SOLUTION

```python
def SimulateSample(lam=2, n=10, iters=1000):
    def VertLine(x, y=1):
        thinkplot.Plot([x, x], [0, y], color='0.8', linewidth=3)

    estimates = []
    for _ in range(iters):
        xs = np.random.exponential(1.0/lam, n)
        lamhat = 1.0 / np.mean(xs)
        estimates.append(lamhat)
        
    # Compute standard error
    stderr = RMSE(estimates, lam)
    print('standard error', stderr)
    
    # Compute confidence interval
    cdf = thinkstats2.Cdf(estimates)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    print('confidence interval', ci)
    VertLine(ci[0])
    VertLine(ci[1])

    # Plot the CDF
    thinkplot.Cdf(cdf)
    thinkplot.Config(xlabel='estimate',
                     ylabel='CDF',
                     title='Sampling distribution')

    return stderr

SimulateSample()
```
### Output for n=10: 
standard error 0.7676696795418035

confidence interval (1.2646255784620983, 3.4798778245314357)

![CDF plot](sampling.png)

### Output for n=100
standard error 0.20132206293593627

confidence interval (1.7210814165411101, 2.3768987615891124)

### Output for n=1000
standard error 0.060329991133675584

confidence interval (1.9003507493175904, 2.101635785128087)

## Conclusion
As the sample size increases, the standard error and the width of the confidence interval decreases. 
