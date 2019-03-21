[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

>> SOLUTION

```python
# interpolate sample to model data by taking upper bound assuming that hte largest income is one million dollars or 10^6
def InterpolateSample(df, log_upper=6.0):
    """Makes a sample of log10 household income.

    Assumes that log10 income is uniform in each range.

    df: DataFrame with columns income and freq
    log_upper: log10 of the assumed upper bound for the highest range

    returns: NumPy array of log10 household income
    """
    # compute the log10 of the upper bound for each range
    df['log_upper'] = np.log10(df.income)

    # get the lower bounds by shifting the upper bound and filling in
    # the first element
    df['log_lower'] = df.log_upper.shift(1)
    df.loc[0, 'log_lower'] = 3.0

    # plug in a value for the unknown upper bound of the highest range
    df.loc[41, 'log_upper'] = log_upper
    
    # use the freq column to generate the right number of values in
    # each range
    arrays = []
    for _, row in df.iterrows():
        vals = np.linspace(row.log_lower, row.log_upper, row.freq)
        arrays.append(vals)

    # collect the arrays into a single sample
    log_sample = np.concatenate(arrays)
    return log_sample

# Log sample to generate sample
log_sample = InterpolateSample(income_df, log_upper=6.0)

# generate sample
sample = np.power(10, log_sample)

# Mean and median of sample
Mean(sample), Median(sample)
```
>> output: (74278.70753118733, 51226.45447894046)

The mean (74,278.71) is greater than the median (51,226.45) confirming the assumption that the sample will be right skewed. 

```python
# Skewness and Pearson's skewness
Skewness(sample), PearsonMedianSkewness(sample)
```
>> output: (4.949920244429583, 0.7361258019141782)

Both skewness and Pearson's skewness are positive, indicating that hte distribution is skewed to the right. 

```python
# Fraction of households report a taxable income below the mean
cdf.Prob(Mean(sample))
```
>> output: 0.660005879566872

66% of households report a taxable income below the mean. 

The mean and skewness of the sample data is dependent on the assumed upper bound. If we increase the assumed upper bound to 10 million, the mean and skewness increase with the increased upper bound, meaning that they are both dependent on any changes and outliers in the sample data and therefore, not robust statstics. On the otherhand, the median stayed the same and Pearson's Median Coefficient decreased with the increase. 
