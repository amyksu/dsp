[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

>> SOLUTION

```python
# Import scipy.stats
import scipy.stats

# Create normal distribution based on information given 
mu = 178
sigma = 7.7
dist - scipy.stats.norm(loc=mu, scale=sigma)
type(dist)

# How many people are betweene 5'10" and 6'1"?

## 5'10" is 177.8 cm
low = dist.cdf(177.8)
## output is 0.48963902786483265

## 6'1" is 185.42 cm
high = dist.cdf(185.42)
## output is 0.8323858654963063

# Subtract to get the percentage of people within that range
high - low
```
Output it 0.3427468376314737, meaning that about 34% of people are between 5'10" and 6'1". 
