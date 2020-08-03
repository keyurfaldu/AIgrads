## Axiomatic Attribution for Deep Networks
### Mukund Sundararajan, Ankur Taly, Qiqi Yan
### ICML 2017

**Whats new** This paper presents presents two desired axioms for an attribution method for feature importance. And it surveys existing methods and how they do not satisfy both these axioms together. It proposes a new method "integrated gradients" supporting these axioms, and heuristic and computationally efficienct then Shaply's method.

**How it works**
* Two desired axioms are as follow
    * Sensitivity: If every input and baseline that differens only in one feature, but have different prediction, then, the differing feature should be given non zero attribution.
        * "Gradients" method violate sensitivity. i.e. f(x) = 1 - Relu(1-x), would procude f(x) 0 at x=0, and 1 at x = 2. However gradients would be 0 for x = 2.
        * Other back propogation methods involves back propagating final prediction score through each layer down to individual features, i.e DeepLift, (Layerwise relevance propagation) LRP, DeConvNets, Guided Backpropagation etc
        * DeConvNets and Guided Backpropagation would not pass gradient back through RELU if its not turned on. Hence suffer from not supporting Sensitivity axiom.
        * DeepLift and LRP do tackle sensitivity by taking discrete jumps wrt baseline instead of taking instantaneous gradient.
    * Implementation Invariance
        * Two networks are functionally equivalent, if their outputs are equal for all inputs. Attribution methods should satisfy implementation invariance, i.e. attributions are identical for two functionally equivalent networks.
        * However, DeepLift and LRP breaks this axiom. df/dg = df/dh * dh/dg. Because they rely on modified form of back propagation for discrete gradients which does not hold chain rule, i.e. 
        <img src="https://i.upmath.me/svg/%5Cfrac%7Bf%5Cleft(x_%7B1%7D%5Cright)-f%5Cleft(x_%7B0%7D%5Cright)%7D%7Bg%5Cleft(x_%7B1%7D%5Cright)-g%5Cleft(x_%7B0%7D%5Cright)%7D%20%5Cneq%20%5Cfrac%7Bf%5Cleft(x_%7B1%7D%5Cright)-f%5Cleft(x_%7B0%7D%5Cright)%7D%7Bh%5Cleft(x_%7B1%7D%5Cright)-h%5Cleft(x_%7B0%7D%5Cright)%7D%20.%20%5Cfrac%7Bh%5Cleft(x_%7B1%7D%5Cright)-h%5Cleft(x_%7B0%7D%5Cright)%7D%7Bg%5Cleft(x_%7B1%7D%5Cright)-g%5Cleft(x_%7B0%7D%5Cright)%7D" alt="\frac{f\left(x_{1}\right)-f\left(x_{0}\right)}{g\left(x_{1}\right)-g\left(x_{0}\right)} \neq \frac{f\left(x_{1}\right)-f\left(x_{0}\right)}{h\left(x_{1}\right)-h\left(x_{0}\right)} . \frac{h\left(x_{1}\right)-h\left(x_{0}\right)}{g\left(x_{1}\right)-g\left(x_{0}\right)}" />
* Integrated Gradient: Compute gradients over a straight line path from baseline to input, and compute integrated gradient by cumulating gradients over this straight line for each dimension of the input. 

    <img src="https://i.upmath.me/svg/%5Ctext%20%7B%20IntegratedGrads%20%7D_%7Bi%7D(x)%3A%3A%3D%5Cleft(x_%7Bi%7D-x_%7Bi%7D%5E%7B%5Cprime%7D%5Cright)%20%5Ctimes%20%5Cint_%7B%5Calpha%3D0%7D%5E%7B1%7D%20%5Cfrac%7B%5Cpartial%20F%5Cleft(x%5E%7B%5Cprime%7D%2B%5Calpha%20%5Ctimes%5Cleft(x-x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D%7B%5Cpartial%20x_%7Bi%7D%7D%20d%20%5Calpha" alt="\text { IntegratedGrads }_{i}(x)::=\left(x_{i}-x_{i}^{\prime}\right) \times \int_{\alpha=0}^{1} \frac{\partial F\left(x^{\prime}+\alpha \times\left(x-x^{\prime}\right)\right)}{\partial x_{i}} d \alpha" />

    * Note, there are many other methods which takes integrated gradients along different paths (not just straight line). Integrated gradients corresponding to cost sharing method is called Aumann Shapely.
    * Also, Sahpely-Shubik method is computationally expensive, it also take order of each dimension to traverse to explore different paths, which is n!.  

    * Integrated gradients can be efficiently approximated via summation. By taking m as number of steps in Riemman approximation, 
    <img src="https://i.upmath.me/svg/%5Cleft(x_%7Bi%7D-x_%7Bi%7D%5E%7B%5Cprime%7D%5Cright)%20%5Ctimes%20%5CSigma_%7Bk%3D1%7D%5E%7Bm%7D%20%5Cfrac%7B%5Cleft.%5Cpartial%20F%5Cleft(x%5E%7B%5Cprime%7D%2B%5Cfrac%7Bk%7D%7Bm%7D%20%5Ctimes%5Cleft(x-x%5E%7B%5Cprime%7D%5Cright)%5Cright)%5Cright)%7D%7B%5Cpartial%20x_%7Bi%7D%7D%20%5Ctimes%20%5Cfrac%7B1%7D%7Bm%7D" alt="\left(x_{i}-x_{i}^{\prime}\right) \times \Sigma_{k=1}^{m} \frac{\left.\partial F\left(x^{\prime}+\frac{k}{m} \times\left(x-x^{\prime}\right)\right)\right)}{\partial x_{i}} \times \frac{1}{m}" />

* In order to compute integrated gradient, for images, black image can be taken as a baseline, and for text, an embedding vector of all zeroes can be taken as a baseline.







