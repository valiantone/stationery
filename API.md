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

    + **alpha** : Floating point value in set [0.01, 0.05, 0.10]  
Desired statistical significance (calculated as 1- `alpha`)
    
    + **beta** : Floating point value in set [0.05, 0.20]  
Desired statistical significance (calculated as 1- `beta`)

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

    + **alpha** : Floating point value in set [0.01, 0.05, 0.10]  
Desired statistical significance (calculated as 1- `alpha`)
    
    + **beta** : Floating point value in set [0.05, 0.20]  
Desired statistical significance (calculated as 1- `beta`)

    + **bayesian** : boolean  
Bayesian or Frequentist framework. Defaults to `False`. Additional parameter `prior` required for Bayesian testing.
 
    + **prior** : integer tuple  
Tuple representing conversion rate, (succesful conversions, unsuccesful conversion), for prior known distribution. This field is only required when `bayesian=True`.

+ **Returns**:
    + **result**: object  
Analysis with winner, loser, z-index and p-values.
