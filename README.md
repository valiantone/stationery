# stationery
_Lightweight Offline A/B Testing Framework_


### Guidelines for A/B Testing with Optimizely
+ Since Optimizely offers limited control of experiments (power, significance etc) we design our experiments with care using appropriate tooling. Currently, the focus of our test designs is to determine evaluation criteria (one-tailed vs two-tailed) and test horizon.
+ We use the `determine_sample_size` tool to compute minimum sample size required to achieve desired level of significance and measure the minimum desired effect. More description on input parameters for this tool are described below in the Toolbox section.
+ A good rule of thumb as of now, is to use one-tailed tests for determining winners in A/B split tests and two-tailed tests for relative determination of best variant in multi-variant testing. Both test results are available via the `split_test_results`.
+ With efficient use of `determine_sample_size`, Optimizely should be able to report results on our tests. In several cases however an alternative test may be appropriate and hence in these situations `split_test_results` may be better suited.
+ `split_test_results` offers functionality for both frequentist and bayesian testing.
