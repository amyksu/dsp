[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)
>> QUESTION: Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

Use the NSFG respondent variable numkdhh to construct the actual distribution for the number of children under 18 in the respondents' households.

Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

Plot the actual and biased distributions, and compute their means.

>> SOLUTION

```python
# Find actual pmf
actual_pmf = thinkstats2.Pmf(resp.numkdhh, label='numkdhh')

# Plot actual pmf
thinkplt.Pmf(actual_pmf)
thinkplot.Config(xlabel='Number of children', ylabel='PMF')
```
![Actual PMF](actual_pmf_plot.png)

```python
# Bias PMF function
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf

# Calculate biased pmf
biased_pmf = BiasPmf(actual_pmf, label='biased')

# Plot both actual and biased PMF's 
thinkplot.PrePlot(2)
thinkplot.Pmfs([actual_pmf, biased_pmf])
thinkplot.Show(xlabel='Number of Children', ylabel='PMF')
```
![Actual versus Biased PMF](actual_v_bias_pmf.png)

```python
# Find mean
actual_pmf.Mean()
```
1.024205155043831

```python
# Find mean
actual_pmf.Mean()
```
2.403679100664282
