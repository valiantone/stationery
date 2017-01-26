# stationery
Statistical Testing Tools and Playbook

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

#### Common Pitfalls with Statistical Significance
Most tools like Optimizely set default power to 0.80, which is considered a good standard heuristic. Varying strength can lead to underpowering/overpowering tests whic have thier own repercussions.
+ Underpowered tests increase the chance to detect a statistically significant (and often practically significant) result where there is none.
+ Overpowering a study leads to most likely wasting money and other resources when we’ve already proven our point beyond the reasonable doubt we are willing to apply.

### Testing
At Bellhops our toolbox currently supports the following tests:
+ One-tailed
+ Two-tailed 

