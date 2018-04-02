# Statistics

# Table of Contents

[1. Introduction](#section-a)  
[2. Why We Are Using Think Stats](#section-b)  
[3. Instructions for Cloning the Repo](#section-c)  
[4. Required Exercises](#section-d)  
[5. Optional Exercises](#section-e)  
[6. Recommended Reading](#section-f)  
[7. Resources](#section-g)

## <a name="section-a"></a>1.  Introduction

[<img src="img/think_stats.jpg" title="Think Stats"/>](http://greenteapress.com/thinkstats2/)

Use Allen Downey's [Think Stats (second edition)](http://greenteapress.com/thinkstats2/) book for getting up to speed with core ideas in statistics and how to approach them programmatically. This book is available online, or you can buy a paper copy if you would like.

Use this book as a reference when answering the 6 required statistics questions below.  The Think Stats book is approximately 200 pages in length.  **It is recommended that you read the entire book, particularly if you are less familiar with introductory statistical concepts.**

Complete the following exercises along with the questions in this file. Some can be solved using code provided with the book. The preface of Think Stats [explains](http://greenteapress.com/thinkstats2/html/thinkstats2001.html#toc2) how to use the code.  

Communicate the problem, how you solved it, and the solution, within each of the following [markdown](https://guides.github.com/features/mastering-markdown/) files. (You can include code blocks and images within markdown.)

## <a name="section-b"></a>2.  Why We Are Using Think Stats 

The stats exercises have been chosen to introduce/solidify some relevant statistical concepts related to data science.  The solutions for these exercises are available in the [ThinkStats repository on GitHub](https://github.com/AllenDowney/ThinkStats2).  You should focus on understanding the statistical concepts, python programming and interpreting the results.  If you are stuck, review the solutions and recode the python in a way that is more understandable to you. 

For example, in the first exercise, the author has already written a function to compute Cohen's D.  **You could import it, or you could write your own code to practice python and develop a deeper understanding of the concept.** 

Think Stats uses a higher degree of python complexity from the python tutorials and introductions to python concepts, and that is intentional to prepare you for the bootcamp.  

**One of the skills to learn here is to understand other people’s code.  And this author is quite experienced, so it’s good to learn how functions and imports work.**

---

## <a name="section-c"></a>3.  Instructions for Cloning the Repo 
Using the [code referenced in the book](https://github.com/AllenDowney/ThinkStats2), follow the step-by-step instructions below.  

**Step 1. Create a directory on your computer where you will do the prework.  Below is an example:**

```
(Mac):      /Users/yourname/ds/metis/metisgh/prework  
(Windows):  C:/ds/metis/metisgh/prework
```

**Step 2. cd into the prework directory.  Use GitHub to pull this repo to your computer.**

```
$ git clone https://github.com/AllenDowney/ThinkStats2.git
```

**Step 3.  Put your ipython notebook or python code files in this directory (that way, it can pull the needed dependencies):**

```
(Mac):     /Users/yourname/ds/metis/metisgh/prework/ThinkStats2/code  
(Windows):  C:/ds/metis/metisgh/prework/ThinkStats2/code
```

---


## <a name="section-d"></a>4.  Required Exercises

*Include your Python code, results and explanation (where applicable).*

### Q1. [Think Stats Chapter 2 Exercise 4](statistics/2-4-cohens_d.md) (effect size of Cohen's d)  
Cohen's D is an example of effect size.  Other examples of effect size are:  correlation between two variables, mean difference, regression coefficients and standardized test statistics such as: t, Z, F, etc. In this example, you will compute Cohen's D to quantify (or measure) the difference between two groups of data.   

You will see effect size again and again in results of algorithms that are run in data science.  For instance, in the bootcamp, when you run a regression analysis, you will recognize the t-statistic as an example of effect size.

```python
import numpy as np

import nsfg
import first

preg = nsfg.ReadFemPreg()

first_b = preg[preg.pregordr==1]
other_b = preg[preg.pregordr!=1]

def Cohens(g1, g2):
    
    var1 = g1.var()
    var2 = g2.var()
    
    mean_diff = g1.mean()-g2.mean()
    
    n1, n2 = len(g1), len(g2)
    var_pool = (n1*var1 +n2*var2)/(n1+n2)
    d = mean_diff/(np.sqrt(var_pool))
    return d

Cohens(first_b.totalwgt_lb, other_b.totalwgt_lb)

```
The effect size is -0.069 deviations.  Compared to pregnency length, the effect is in the opposite direction. Meaning that it is more likely to have heavier babies after the first pregnency.


### Q2. [Think Stats Chapter 3 Exercise 1](statistics/3-1-actual_biased.md) (actual vs. biased)
This problem presents a robust example of actual vs biased data.  As a data scientist, it will be important to examine not only the data that is available, but also the data that may be missing but highly relevant.  You will see how the absence of this relevant data will bias a dataset, its distribution, and ultimately, its statistical interpretation.

The following is the Python code for the exercise.  The mean of the actual distribution is 1.024. The mean for the biased 2.403. The difference in means was created by the absence of respondents in households with 0 kids for the biased mean.
```Python
import nsfg
import matplotlib.pyplot as plt

resp = nsfg.ReadFemResp()
num_kd = resp.numkdhh
act_dist = {}
act_mean = num_kd.mean()
n1 = len(num_kd)
for x in num_kd:
    if x in act_dist:
        act_dist[x] += 1
    else:
        act_dist[x] = 1
print(act_dist)
bias_dist = {}
sum2=0
n2=0
counter =0
x1 = []
s_s = n1 - act_dist[0]
for x in act_dist:
    n2 = act_dist[x]*x
    bias_dist[x] = n2
    sum2+=(n2*x)
    counter += n2
    x1.append(x)
bias_mean= sum2/counter


sum1=0
y1 = []
y2 = []
x1 = sorted(x1)
for x in x1:
    act_dist[x] = act_dist[x]/n1
    bias_dist[x] = bias_dist[x]/counter
    y1.append(act_dist[x])
    y2.append(bias_dist[x])

print('The actual mean is: ', act_mean, 'The biased mean is: ', bias_mean)

plt.step(x1, y1, 'r--', x1, y2, 'g--')
plt.xlim([-1,6])
plt.show()
```

### Q3. [Think Stats Chapter 4 Exercise 2](statistics/4-2-random_dist.md) (random distribution)  
This questions asks you to examine the function that produces random numbers.  Is it really random?  A good way to test that is to examine the pmf and cdf of the list of random numbers and visualize the distribution.  If you're not sure what pmf is, read more about it in Chapter 3.  

The distribution of PMFs based on the random numbers generated turned into a flat line because there were too may different values to show distinctions between the same values.  The CDF shows that there were some repeat values, but for the most part, the distribution is uniform.

```Python
import numpy as np
import random
import matplotlib.pyplot as plt

rand = []
rand = [random.random() for q in range(1000)]
rand.sort()

cdf = []
pmf = {}
def  CDF(val, ser):
    counter = 0
    for x in ser:
        if x <= val:
            counter+=1
    prob = counter / len(ser)
    return prob
def PMF(ser):
    pmf_list = []
    for x in ser:
        if x in pmf:
            pmf[x] +=1
        else:
            pmf[x] = 1
    for q in ser:
        pmf_list.append(pmf[q]/len(ser))
    return pmf_list

for t in rand:
    cdf.append(CDF(t, rand))
pmf1 = []
pmf1 = PMF(rand)

print(cdf)
print(pmf1)
plt.subplot(2,1,1)
plt.step(rand, cdf, 'r--')
plt.ylabel('CDF')

plt.subplot(2,1,2)
plt.step(rand, pmf1, 'g--')
plt.xlabel('Random Value')
plt.ylabel('PMF')
plt.show()
```


### Q4. [Think Stats Chapter 5 Exercise 1](statistics/5-1-blue_men.md) (normal distribution of blue men)
This is a classic example of hypothesis testing using the normal distribution.  The effect size used here is the Z-statistic. 

The amount of men in the respondents that meet the criteria of being between 5'10" and 6'1" is 34.2%.

```Python
import scipy.stats
#Constructing frozen variable
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
type(dist)

#finding percent of respondents between 5'10" and 6'1"
cm1 = 70*2.54
cm2 = 73*2.54 
per = dist.cdf(cm2)-dist.cdf(cm1)
print(per*100)
```

### Q5. Bayesian (Elvis Presley twin) 

Bayes' Theorem is an important tool in understanding what we really know, given evidence of other information we have, in a quantitative way.  It helps incorporate conditional probabilities into our conclusions.

Elvis Presley had a twin brother who died at birth.  What is the probability that Elvis was an identical twin? Assume we observe the following probabilities in the population: fraternal twin is 1/125 and identical twin is 1/300.  

The probability Elvis was an identical twin is 0.294.  This was calculated using the bayesian theorem.  P(A) = 17/1500, P(B) = 1/300, and the P(A|B) = 1 because we know that he had a twin brother.

---

### Q6. Bayesian &amp; Frequentist Comparison  
How do frequentist and Bayesian statistics compare?

Frequentist stats use an experienment theoretically repeated a fixed amount of times.  Depenedent on the result of these experiments.
Bayesian stats provide tools to update the evidence with new data, making it less dependent on the results of repeated experiments.

---

## <a name="section-e"></a>5.  Optional Exercises

The following exercises are optional, but we highly encourage you to complete them if you have the time.

### Q7. [Think Stats Chapter 7 Exercise 1](statistics/7-1-weight_vs_age.md) (correlation of weight vs. age)
In this exercise, you will compute the effect size of correlation.  Correlation measures the relationship of two variables, and data science is about exploring relationships in data.    

### Q8. [Think Stats Chapter 8 Exercise 2](statistics/8-2-sampling_dist.md) (sampling distribution)
In the theoretical world, all data related to an experiment or a scientific problem would be available.  In the real world, some subset of that data is available.  This exercise asks you to take samples from an exponential distribution and examine how the standard error and confidence intervals vary with the sample size.

### Q9. [Think Stats Chapter 6 Exercise 1](statistics/6-1-household_income.md) (skewness of household income)
### Q10. [Think Stats Chapter 8 Exercise 3](statistics/8-3-scoring.md) (scoring)
### Q11. [Think Stats Chapter 9 Exercise 2](statistics/9-2-resampling.md) (resampling)

---

## <a name="section-f"></a>6.  Recommended Reading

Read Allen Downey's [Think Bayes](http://greenteapress.com/thinkbayes/) book.  It is available online for free, or you can buy a paper copy if you would like.

[<img src="img/think_bayes.png" title="Think Bayes"/>](http://greenteapress.com/thinkbayes/) 

---

## <a name="section-g"></a>7.  More Resources

Some people enjoy video content such as Khan Academy's [Probability and Statistics](https://www.khanacademy.org/math/probability) or the much longer and more in-depth Harvard [Statistics 110](https://www.youtube.com/playlist?list=PL2SOU6wwxB0uwwH80KTQ6ht66KWxbzTIo). You might also be interested in the book [Statistics Done Wrong](http://www.statisticsdonewrong.com/) or a very short [overview](http://schoolofdata.org/handbook/courses/the-math-you-need-to-start/) from School of Data.
