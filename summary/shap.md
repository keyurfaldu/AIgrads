## A Unified Approach to Interpreting Model Predictions

### Scott M. Lundberg, Su-In Lee
### University of Washington

### NIPS 2017

**Whats new** This paper provides framework and theory for additive attributions based on shapely values, and desired properties, and approximate it with linear local estimations by LIME etc.

**How it works**
* Can any complex function f(x) be estimated by another function g(z'), where z' is simplified inputs, and g(z')=f(h(z'))? And, function g(z') is defined as follow:

    <img src="https://i.upmath.me/svg/g%5Cleft(z%5E%7B%5Cprime%7D%5Cright)%3D%5Cphi_%7B0%7D%2B%5Csum_%7Bi%3D1%7D%5E%7BM%7D%20%5Cphi_%7Bi%7D%20z_%7Bi%7D%5E%7B%5Cprime%7D" alt="g\left(z^{\prime}\right)=\phi_{0}+\sum_{i=1}^{M} \phi_{i} z_{i}^{\prime}" />

    * Where, z' \in {0,1}^M, denotes if a particular feature is present or not. M is number of simplified input features. 


* LIME method tries to estimate that local function g for a given function f:

    <img src="https://i.upmath.me/svg/%5Cxi%3D%5Cunderset%7Bg%20%5Cin%20%5Cmathcal%7BG%7D%7D%7B%5Carg%20%5Cmin%20%7D%20L%5Cleft(f%2C%20g%2C%20%5Cpi_%7Bx%5E%7B%5Cprime%7D%7D%5Cright)%2B%5COmega(g)" alt="\xi=\underset{g \in \mathcal{G}}{\arg \min } L\left(f, g, \pi_{x^{\prime}}\right)+\Omega(g)" />

    * It is an estimation over set of samples using loss function L, which are weighted by local kernel Pi_x'.

* Classic shapely regression value estimation

    <img src="https://i.upmath.me/svg/%5Cphi_%7Bi%7D%3D%5Csum_%7BS%20%5Csubseteq%20F%20%5Cbackslash%5C%7Bi%5C%7D%7D%20%5Cfrac%7B%7CS%7C%20!(%7CF%7C-%7CS%7C-1)%20!%7D%7B%7CF%7C%20!%7D%5Cleft%5Bf_%7BS%20%5Ccup%5C%7Bi%5C%7D%7D%5Cleft(x_%7BS%20%5Ccup%5C%7Bi%5C%7D%7D%5Cright)-f_%7BS%7D%5Cleft(x_%7BS%7D%5Cright)%5Cright%5D" alt="\phi_{i}=\sum_{S \subseteq F \backslash\{i\}} \frac{|S| !(|F|-|S|-1) !}{|F| !}\left[f_{S \cup\{i\}}\left(x_{S \cup\{i\}}\right)-f_{S}\left(x_{S}\right)\right]" />

    * Where, weight component represents numbers of possible permutations prior and post to input feature i, which is |S|! and (|F| - |S| - 1)! respectively.

* Now, to use this classic shapeluy equation in context, g(z') = f(h(z')), where z' is simplified input, denoting if a particular feature is present or not. Now, g(z') can be derived by estimating weights fi_i, where

    <img src="https://i.upmath.me/svg/%5Cphi_%7Bi%7D(f%2C%20x)%3D%5Csum_%7Bz%5E%7B%5Cprime%7D%20%5Csubseteq%20x%5E%7B%5Cprime%7D%7D%20%5Cfrac%7B%5Cleft%7Cz%5E%7B%5Cprime%7D%5Cright%7C%20!%5Cleft(M-%5Cleft%7Cz%5E%7B%5Cprime%7D%5Cright%7C-1%5Cright)%20!%7D%7BM%20!%7D%5Cleft%5Bf_%7Bx%7D%5Cleft(z%5E%7B%5Cprime%7D%5Cright)-f_%7Bx%7D%5Cleft(z%5E%7B%5Cprime%7D%20%5Cbackslash%20i%5Cright)%5Cright%5D" alt="\phi_{i}(f, x)=\sum_{z^{\prime} \subseteq x^{\prime}} \frac{\left|z^{\prime}\right| !\left(M-\left|z^{\prime}\right|-1\right) !}{M !}\left[f_{x}\left(z^{\prime}\right)-f_{x}\left(z^{\prime} \backslash i\right)\right]" />

    * These weights are esimated using local function, f_x, which is linear estimation in the local space based on if feature is present or not.

* Such function, g(z) can directly be esimated by minimizing loss in 2nd equation, which LIME does by sampling inputs near given input, and giving them weights based on kernel similarity.

* It shows, how feature importance are attributed for a particular prediction

    <p align="center">
        <img width=600 src="images/shap_feature_importance.png">
        <em>Source: Author</em>
        </p>


