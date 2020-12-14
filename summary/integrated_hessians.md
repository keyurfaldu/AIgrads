## Explaining Explanations: Axiomatic Feature Interactions for Deep Networks
### Janizek, Sturmfels, Lee, 
### 2020 [[arXiv](https://arxiv.org/pdf/2002.04138.pdf)]

**Whats Unique**
Recently, feature attributions methods explain how much a feature is an important for the model prediction. However, interactions between the features helps us to understand model behavior. Author presents a new technique Integrated Hessians - which is an extension to Integrated Gradients to capture feature interactions for their role in model prediction.

**How It Works**

* Integrated Gradients take the derivate of model output over a feature taking values along a path from baseline to current.

<img src="https://i.upmath.me/svg/%5Cphi_%7Bi%7D(x)%3D%5Cleft(x_%7Bi%7D-x_%7Bi%7D%5E%7B%5Cprime%7D%5Cright)%20%5Ctimes%20%5Cint_%7B%5Calpha%3D0%7D%5E%7B1%7D%20%5Cfrac%7B%5Cpartial%20f%5Cleft(x%5E%7B%5Cprime%7D%2B%5Calpha%5Cleft(x-x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D%7B%5Cpartial%20x_%7Bi%7D%7D%20d%20%5Calpha" alt="\phi_{i}(x)=\left(x_{i}-x_{i}^{\prime}\right) \times \int_{\alpha=0}^{1} \frac{\partial f\left(x^{\prime}+\alpha\left(x-x^{\prime}\right)\right)}{\partial x_{i}} d \alpha" />


* Integrated hessians is the Integratred Gradients of Integrated Gradients.

<img src="https://i.upmath.me/svg/%5CGamma_%7Bi%2C%20j%7D(x)%3D%5Cphi_%7Bj%7D%5Cleft(%5Cphi_%7Bi%7D(x)%5Cright)" alt="\Gamma_{i, j}(x)=\phi_{j}\left(\phi_{i}(x)\right)" />

<img src="https://i.upmath.me/svg/%5CGamma_%7Bi%2C%20j%7D(x)%3D%5Cleft(x_%7Bi%7D-x_%7Bi%7D%5E%7B%5Cprime%7D%5Cright)%5Cleft(x_%7Bj%7D-x_%7Bj%7D%5E%7B%5Cprime%7D%5Cright)%20%5Ctimes%20%5Cint_%7B%5Cbeta%3D0%7D%5E%7B1%7D%20%5Cint_%7B%5Calpha%3D0%7D%5E%7B1%7D%20%5Calpha%20%5Cbeta%20%5Cfrac%7B%5Cpartial%5E%7B2%7D%20f%5Cleft(x%5E%7B%5Cprime%7D%2B%5Calpha%20%5Cbeta%5Cleft(x-x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D%7B%5Cpartial%20x_%7Bi%7D%20%5Cpartial%20x_%7Bj%7D%7D%20d%20%5Calpha%20d%20%5Cbeta" alt="\Gamma_{i, j}(x)=\left(x_{i}-x_{i}^{\prime}\right)\left(x_{j}-x_{j}^{\prime}\right) \times \int_{\beta=0}^{1} \int_{\alpha=0}^{1} \alpha \beta \frac{\partial^{2} f\left(x^{\prime}+\alpha \beta\left(x-x^{\prime}\right)\right)}{\partial x_{i} \partial x_{j}} d \alpha d \beta" />

And, Integrated hessians satisfies fundamental axioms.
1. Interaction Completeness axiom

<img src="https://i.upmath.me/svg/%5Csum_%7Bi%7D%20%5Csum_%7Bj%7D%20%5CGamma_%7Bi%2C%20j%7D(x)%3Df(x)-f%5Cleft(x%5E%7B%5Cprime%7D%5Cright)" alt="\sum_{i} \sum_{j} \Gamma_{i, j}(x)=f(x)-f\left(x^{\prime}\right)" />


2. Self Completeness axiom
<img src="https://i.upmath.me/svg/%5CGamma_%7Bi%2C%20i%7D(x)%3D%5Cphi_%7Bi%7D(x)-%5Csum_%7Bj%20%5Cneq%20i%7D%20%5CGamma_%7Bi%2C%20j%7D(x)" alt="\Gamma_{i, i}(x)=\phi_{i}(x)-\sum_{j \neq i} \Gamma_{i, j}(x)" />
- when cross interactions terms are zero, integrated hessians are just the integrated gradients.

* Making RELU work
- Relu has second order derivative all zero. So, inorder to make Integrared Hessians work for RELU, an approximation of RELU, which is SoftPlus can be used.

    <img src="https://i.upmath.me/svg/%5Coperatorname%7BSoftPlus%7D_%7B%5Cbeta%7D(x)%3D%5Cfrac%7B1%7D%7B%5Cbeta%7D%20%5Clog%20%5Cleft(1%2Be%5E%7B-%5Cbeta%20x%7D%5Cright)" alt="\operatorname{SoftPlus}_{\beta}(x)=\frac{1}{\beta} \log \left(1+e^{-\beta x}\right)" />

* XOR was explained in the paper by demonstraing how feature interactions are capture by Integrated hessians which could not get captured by Integrated Gradients.

* Examples in NLP domain, where feature interactions are explaining model. 

    <p align="center">
    <img width=600 src="images/Integrated_Gradients_NLP_examples_0.png">
    <em>Source: Author</em>
    </p>


    * how adjectives interacts with each other or with noun, and give meaningful attribution
    * when multiple adjectives are modifying nouns it impacts noun's attribution significantly, whereas individual adjectives attribution becomes smaller.

    <p align="center">
    <img width=600 src="images/Integrated_Gradients_NLP_examples.png">
    <em>Source: Author</em>
    </p>










