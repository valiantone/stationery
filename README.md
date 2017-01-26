# statnery
_Statistical Testing Tools and Playbook_


Statistical significance testing is paramount in the field of experimentation as it establishes higher degree of confidence in our results being better than a random effect of chance. The following guide is an attempt to institutionalize a common shared framework for testing. At Bellhops our A/B Testing vendor of choice is Optimizely and hence a lot of the definitions and practices are tailored to conform with their knowledge base. The idea for this playbook was inspired by Julien Le Nestour's [blog](https://julienlenestour.com/maths-behind-minimum-sample-size-ab-testing/) post of a similar nature.

### Statistical Significance
> Statistical significance deals with the risk of false positives—in the situation when there is no difference between your original and your variation, it predicts how often your test results will accurately say that there is no difference, and how often your test results will incorrectly tell you there is a difference (a false positive). Usually tests are run at 95% statistical significance. This means that when there is no difference between your original and your variation, you will accurately measure no difference 95% of the time (19 out of 20 tests), and you will measure a false positive 5% of the time (1 out of 20 tests).

> Bottom line: the higher your level of statistical significance, the less likely you are to conclude that your variation is a winner when it is not.

Source: [Optimizely](https://help.optimizely.com/Analyze_Results/How_long_to_run_a_test)

#### Common Pitfalls with Statistical Significance
1. Terminating a test when significance is acieved - significance should not be the termination criteria. Most fruitful tests involve deteriming a test horizon on the basis of minimum sample size required for desired level of significance. The horizon is pre-determined and testing is carried out over this period.
2. Interpret a statistically insignificant result as support for lack of difference/lack of effect. Fortunately, this can be corrected for by the notion of **statistical power**.

### Statistical Power
> Statistical power deals with the risk of false negatives—in the situation where there is a difference between your original and your variation, it predicts how often your test results will accurately say that there is a difference, and how often your test results will incorrectly tell you there is no difference (a false negative). Usually people run tests at 80% statistical power. This means that 80% of the time (8 out of 10 tests), a winning variation will be identified as a winning variation. In other words, 20% of the time (2 out of 10 tests), you will not detect a winning variation even though you have one.

> Bottom line: the higher your level of statistical power, the less likely you are to miss out on identifying a winning variation.

Source: [Optimizely](https://help.optimizely.com/Analyze_Results/How_long_to_run_a_test)

#### Common Pitfalls with Statistical Power
Most tools like Optimizely set default power to 0.80, which is considered a good standard heuristic. Varying strength can lead to underpowering/overpowering tests whic have thier own repercussions.
+ Underpowered tests increase the chance to detect a statistically significant (and often practically significant) result where there is none.
+ Overpowering a study leads to most likely wasting money and other resources when we’ve already proven our point beyond the reasonable doubt we are willing to apply.

####  Power, Effect Size, Sample Size and Alpha
When discussing statistical power, we have four inter-related concepts:  power, effect size, sample size and alpha.  These four things are related such that each is a function of the other three.  In other words, if three of these values are fixed, the fourth is completely determined (Cohen, 1988, page 14).  We mention this because, by increasing one, you can decrease (or increase) another.  For example, if you can increase your effect size, you will need fewer subjects, given the same power and alpha level.  Specifically, increasing the effect size, the sample size and/or alpha will increase your power.
![Power Analysis](http://www.ats.ucla.edu/stat/seminars/Intro_power/ips1.gif)

### Testing
At Bellhops our toolbox currently supports the following tests:
+ One-tailed Tests
+ Two-tailed Tests

When you conduct a test of statistical significance, whether it is from a correlation, an ANOVA, a regression or some other kind of test, you are given a p-value somewhere in the output.  If your test statistic is symmetrically distributed, you can select one of three alternative hypotheses. Two of these correspond to one-tailed tests and one corresponds to a two-tailed test.

#### Two-tailed Tests
If you are using a significance level of 0.05, a two-tailed test allots half of your alpha to testing the statistical significance in one direction and half of your alpha to testing statistical significance in the other direction.  This means that .025 is in each tail of the distribution of your test statistic. When using a two-tailed test, regardless of the direction of the relationship you hypothesize, you are testing for the possibility of the relationship in both directions.  For example, we may wish to compare the mean of a sample to a given value x using a t-test.  Our null hypothesis is that the mean is equal to x. A two-tailed test will test both if the mean is significantly greater than x and if the mean significantly less than x. The mean is considered significantly different from x if the test statistic is in the top 2.5% or bottom 2.5% of its probability distribution, resulting in a p-value less than 0.05.

![Two-tailed P-value](http://www.ats.ucla.edu/stat/mult_pkg/faq/pvalue1.gif)

#### One-tailed Tests
If you are using a significance level of .05, a one-tailed test allots all of your alpha to testing the statistical significance in the one direction of interest.  This means that .05 is in one tail of the distribution of your test statistic. When using a one-tailed test, you are testing for the possibility of the relationship in one direction and completely disregarding the possibility of a relationship in the other direction.  Let's return to our example comparing the mean of a sample to a given value x using a t-test.  Our null hypothesis is that the mean is equal to x. A one-tailed test will test either if the mean is significantly greater than x or if the mean is significantly less than x, but not both. Then, depending on the chosen tail, the mean is significantly greater than or less than x if the test statistic is in the top 5% of its probability distribution or bottom 5% of its probability distribution, resulting in a p-value less than 0.05.  
<table border="0"><tr><td><img src='http://www.ats.ucla.edu/stat/mult_pkg/faq/pvalue2.gif'></td><td><img src='http://www.ats.ucla.edu/stat/mult_pkg/faq/pvalue3.gif'></td></tr></table>

### Determining Appropriate Test
The one-tailed test provides more power to detect an effect in one direction by not testing the effect in the other direction.The one-tailed test provides more power to detect an effect in one direction by not testing the effect in the other direction.

So when is a one-tailed test appropriate? If you consider the consequences of missing an effect in the untested direction and conclude that they are negligible and in no way irresponsible or unethical, then you can proceed with a one-tailed test. Choosing a one-tailed test for the sole purpose of attaining significance is not appropriate.  Choosing a one-tailed test after running a two-tailed test that failed to reject the null hypothesis is not appropriate, no matter how "close" to significant the two-tailed test was.  Using statistical tests inappropriately can lead to invalid results that are not replicable and highly questionable--a steep price to pay for a significance star in your results table.

#### A Note about tests in Optimizely
> When you run a test, you can run a 1-tailed or 2-tailed test. 2-tailed tests are designed to detect differences between your original and your variation in both directions—it will tell you if your variation is a winner and it will also tell you if your variation is a loser. 1-tailed tests are designed to detect differences between your original and your variation in only one direction.

> At Optimizely, we use 1-tailed tests. We do this because we believe that 1) the ability to identify a “winner” is more valuable than the ability to identify a “loser” when choosing between an original and a variation and 2) this enables faster decision-making. The fastest way to help you identify your winners is to run a 1-tailed test. Because of this, the sample size calculator is set to 1-tailed tests by default.

> However, you may want to run your experiment as a 2-tailed test, which will double the acceptable false positive rate. In our example, that means doubling 5% to 10%. Simply select the 2-tailed option in the calculator.

_Optimizely is an A/B Testing vendor and all test functionality may be subject to change in the future._


### Guidelines for A/B Testing with Optimizely
+ Since Optimizely offers limited control of experiments (power, significance etc) we design our experiments with care using appropriate tooling. Currently, the focus of our test designs is to determine evaluation criteria (one-tailed vs two-tailed) and test horizon.
+ We use the `determine_sample_size` tool to compute minimum sample size required to achieve desired level of significance and measure the minimum desired effect. More description on input parameters for this tool are described below in the Toolbox section.
+ A good rule of thumb as of now, is to use one-tailed tests for determining winners in A/B split tests and two-tailed tests for relative determination of best variant in multi-variant testing. Both test results are available via the `split_test_results`.
+ With efficient use of `determine_sample_size`, Optimizely should be able to report results on our tests. In several cases however an alternative test may be appropriate and hence in these situations `split_test_results` may be better suited.
+ `split_test_results` offers functionality for both frequentist and bayesian testing.


### Standard Testing Toolkit API

`determine_sample_size(baserate, effect, alpha=0.05, beta=0.2, alternative='one-sided', relative=False)`
Determine minimum sample size for significance
+ **Parameters**:
    + **alternative** : string  
Describes test type, defaults to one-sided. Functionality for one-sided and two-sided tests.

    + **baserate** : Floating point value in range [0, 1]  
Estimated current conversion rate.

    + **effect** : Floating point value in range [0, 1]  
Minimum detectable effect over baseline that can be measured within confidence interval.

    + **alpha** : Floating point value in range [0, 1]  
Desired statistical significance (calculated as 1- ![equation](http://www.sciweavers.org/tex2img.php?eq=%5Calpha&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0))
    
    + **beta** : Floating point value in range [0, 1]  
Desired statistical significance (calculated as 1- ![equation](http://www.sciweavers.org/tex2img.php?eq=%5Cbeta&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0))

    + **relative** : boolean  
Absolute or Relative effect desired, defaults to `False` indicating absolute.

+ **Returns**:
    + **N**: integer

**Formulation**
Mimimum sample size calculated as:

![equation](http://www.sciweavers.org/tex2img.php?eq=N%20%3D%20%20%5Cfrac%7B%28%20Z_%7B%5Calpha%7D%20%2B%20Z_%7B1-%5Cbeta%7D%29%5E%7B2%7D%7D%7Bd%5E%7B2%7D%7D%20%5Bp_%7B1%7D%281%20-%20p_%7B1%7D%29%20%2B%20p_%7B2%7D%281%20-%20p_%7B2%7D%29%5D%0A&bc=White&fc=Black&im=png&fs=12&ff=arev&edit=0)

-------

`split_test_results(visitors, conversions, alpha=0.05, beta=0.2, alternative='one-sided', bayesian=False)`
Function to perform desired split test and return a summary of results.
+ **Parameters**:
    + **alternative** : string  
Describes test type, defaults to one-sided. Functionality for one-sided and two-sided tests.

    + **visitors** : integer tuple  
Visitors for control A and variant B - (A, B) 

    + **conversions** : integer tuple  
Conversions for control A and variant B - (A, B)

    + **alpha** : Floating point value in range [0, 1]  
Desired statistical significance (calculated as 1- ![equation](http://www.sciweavers.org/tex2img.php?eq=%5Calpha&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0))
    
    + **beta** : Floating point value in range [0, 1]  
Desired statistical significance (calculated as 1- ![equation](http://www.sciweavers.org/tex2img.php?eq=%5Cbeta&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0))

    + **bayesian** : boolean  
Bayesian or Frequentist framework. Defaults to `False`. Additional parameter `prior` required for Bayesian testing.
 
    + **prior** : integer tuple  
Tuple representing conversion rate, (succesful conversions, unsuccesful conversion), for prior known distribution. This field is only required when `bayesian=True`.

+ **Returns**:
    + **result**: object  
Analysis with winner, loser, z-index and p-values.
