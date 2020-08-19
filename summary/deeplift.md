## Learning Important Features Through Propagating Activation Differences
### Avanti Shrikumar, Peyton Greenside, Anshul Kundaje
### Stanford University
### ICML 2019



**Whats New** DeepLift is a method for decomposing the output prediction of neural network on a specific inputs by back propagating the contributions through all intermediate neurons. 

**Major Contribution**
It has two unique contributions:
* "difference-from-reference" method allows DeepLift to handle zero gradients as well as discontineous gradients unlike others.
* Seperate positive and negative contributions would reveal dependencies missed by other approaches. 

**How It Works**
* Formally, let  **t**  represent target output.
* let **x1,x2,..,xn** represent some neurons/set of layers or inputs which are necessary and sufficient to compute **t**.
* **\delta t = t - t_0** is change in output with respect to reference output
* **\delta x_i = x_i - x_i_0** is change in i_th x component. 
* DeepLIFT assigns contribution scores **C_delta_x_delta_t** to **delta_x** as follow "**summation-to-delta**" property

    <img src="https://i.upmath.me/svg/%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%20C_%7B%5CDelta%20x_%7Bi%7D%20%5CDelta%20t%7D%3D%5CDelta%20t" alt="\sum_{i=1}^{n} C_{\Delta x_{i} \Delta t}=\Delta t" />

    * **C_delta_x_delta_t** can be positive even if partial derivative of dt/dx is zero, so it solves the problem of saturation.

* Definition of multipliers: This is analogus to partial derivative.

    <img src="https://i.upmath.me/svg/m_%7B%5CDelta%20x%20%5CDelta%20t%7D%3D%5Cfrac%7BC_%7B%5CDelta%20x%20%5CDelta%20t%7D%7D%7B%5CDelta%20x%7D" alt="m_{\Delta x \Delta t}=\frac{C_{\Delta x \Delta t}}{\Delta x}" />

* **The chain rule of multipliers** is analogus to chain rule of partial derivatives.

    <img src="https://i.upmath.me/svg/m_%7B%5CDelta%20x_%7Bi%7D%20%5CDelta%20t%7D%3D%5Csum_%7Bj%7D%20m_%7B%5CDelta%20x_%7Bi%7D%20%5CDelta%20y_%7Bj%7D%7D%20m_%7B%5CDelta%20y_%7Bj%7D%20%5CDelta%20t%7D" alt="m_{\Delta x_{i} \Delta t}=\sum_{j} m_{\Delta x_{i} \Delta y_{j}} m_{\Delta y_{j} \Delta t}" />

* **Seperating Positive and Negative Contirbutions**
    * Another consistency can be achieved if positive and negative contributions are seperated. i.e. shapely approximations can be applied.

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5CDelta%20y%20%26%3D%5CDelta%20y%5E%7B%2B%7D%2B%5CDelta%20y%5E%7B-%7D%20%5C%5C%0AC_%7B%5CDelta%20y%20%5CDelta%20t%7D%20%26%3DC_%7B%5CDelta%20y%5E%7B%2B%7D%20%5CDelta%20t%7D%2BC_%7B%5CDelta%20y%5E%7B-%7D%20%5CDelta%20t%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\Delta y &amp;=\Delta y^{+}+\Delta y^{-} \\
C_{\Delta y \Delta t} &amp;=C_{\Delta y^{+} \Delta t}+C_{\Delta y^{-} \Delta t}
\end{aligned}" />

* **Linear Rule** 
    * This applies to dense and convolution layers. When y is a lienar function of x_i. 

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5CDelta%20y%5E%7B%2B%7D%20%26%3D%5Csum_%7Bi%7D%201%5Cleft%5C%7Bw_%7Bi%7D%20%5CDelta%20x_%7Bi%7D%3E0%5Cright%5C%7D%20w_%7Bi%7D%20%5CDelta%20x_%7Bi%7D%20%5C%5C%0A%26%3D%5Csum%201%5Cleft%5C%7Bw_%7Bi%7D%20%5CDelta%20x_%7Bi%7D%3E0%5Cright%5C%7D%20w_%7Bi%7D%5Cleft(%5CDelta%20x_%7Bi%7D%5E%7B%2B%7D%2B%5CDelta%20x_%7Bi%7D%5E%7B-%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\Delta y^{+} &amp;=\sum_{i} 1\left\{w_{i} \Delta x_{i}&gt;0\right\} w_{i} \Delta x_{i} \\
&amp;=\sum 1\left\{w_{i} \Delta x_{i}&gt;0\right\} w_{i}\left(\Delta x_{i}^{+}+\Delta x_{i}^{-}\right)
\end{aligned}" /> 

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5CDelta%20y%5E%7B-%7D%20%26%3D%5Csum_%7Bi%7D%201%5Cleft%5C%7Bw_%7Bi%7D%20%5CDelta%20x_%7Bi%7D%3C0%5Cright%5C%7D%20w_%7Bi%7D%20%5CDelta%20x_%7Bi%7D%20%5C%5C%0A%26%3D%5Csum_%7Bi%7D%201%5Cleft%5C%7Bw_%7Bi%7D%20%5CDelta%20x_%7Bi%7D%3C0%5Cright%5C%7D%20w_%7Bi%7D%5Cleft(%5CDelta%20x_%7Bi%7D%5E%7B%2B%7D%2B%5CDelta%20x_%7Bi%7D%5E%7B-%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\Delta y^{-} &amp;=\sum_{i} 1\left\{w_{i} \Delta x_{i}&lt;0\right\} w_{i} \Delta x_{i} \\
&amp;=\sum_{i} 1\left\{w_{i} \Delta x_{i}&lt;0\right\} w_{i}\left(\Delta x_{i}^{+}+\Delta x_{i}^{-}\right)
\end{aligned}" />

* **Rescale Rule**
    * This rule applies to nonlinear transformations that take single input, such as Relu or Sigmoid.

        <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0A%5CDelta%20y%5E%7B%2B%7D%3D%5Cfrac%7B%5CDelta%20y%7D%7B%5CDelta%20x%7D%20%5CDelta%20x%5E%7B%2B%7D%3DC_%7B%5CDelta%20x%5E%7B%2B%7D%20%5CDelta%20y%5E%7B%2B%7D%7D%20%5C%5C%0A%5CDelta%20y%5E%7B-%7D%3D%5Cfrac%7B%5CDelta%20y%7D%7B%5CDelta%20x%7D%20%5CDelta%20x%5E%7B-%7D%3DC_%7B%5CDelta%20x%5E%7B-%7D%20%5CDelta%20y%5E%7B-%7D%7D%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
\Delta y^{+}=\frac{\Delta y}{\Delta x} \Delta x^{+}=C_{\Delta x^{+} \Delta y^{+}} \\
\Delta y^{-}=\frac{\Delta y}{\Delta x} \Delta x^{-}=C_{\Delta x^{-} \Delta y^{-}}
\end{array}" />

* **RevealCancel Rule: Shapely Approximation**
    * Positive outcomes are computed from adding positive contributions in reference inputs, and reference inputs with negative contributions. Similerly for Negative outcomes.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5CDelta%20y%5E%7B%2B%7D%20%26%3D%5Cfrac%7B1%7D%7B2%7D%5Cleft(f%5Cleft(x%5E%7B0%7D%2B%5CDelta%20x%5E%7B%2B%7D%5Cright)-f%5Cleft(x%5E%7B0%7D%5Cright)%5Cright)%20%5C%5C%0A%26%2B%5Cfrac%7B1%7D%7B2%7D%5Cleft(f%5Cleft(x%5E%7B0%7D%2B%5CDelta%20x%5E%7B-%7D%2B%5CDelta%20x%5E%7B%2B%7D%5Cright)-f%5Cleft(x%5E%7B0%7D%2B%5CDelta%20x%5E%7B-%7D%5Cright)%5Cright)%20%5C%5C%0A%5CDelta%20y%5E%7B-%7D%20%26%3D%5Cfrac%7B1%7D%7B2%7D%5Cleft(f%5Cleft(x%5E%7B0%7D%2B%5CDelta%20x%5E%7B-%7D%5Cright)-f%5Cleft(x%5E%7B0%7D%5Cright)%5Cright)%20%5C%5C%0A%26%2B%5Cfrac%7B1%7D%7B2%7D%5Cleft(f%5Cleft(x%5E%7B0%7D%2B%5CDelta%20x%5E%7B%2B%7D%2B%5CDelta%20x%5E%7B-%7D%5Cright)-f%5Cleft(x%5E%7B0%7D%2B%5CDelta%20x%5E%7B%2B%7D%5Cright)%5Cright)%20%5C%5C%0Am_%7B%5CDelta%20x%5E%7B%2B%7D%20%5CDelta%20y%5E%7B%2B%7D%7D%20%26%3D%5Cfrac%7BC_%7B%5CDelta%20x%5E%7B%2B%7D%20y%5E%7B%2B%7D%7D%7D%7B%5CDelta%20x%5E%7B%2B%7D%7D%3D%5Cfrac%7B%5CDelta%20y%5E%7B%2B%7D%7D%7B%5CDelta%20x%5E%7B%2B%7D%7D%20%3B%20m_%7B%5CDelta%20x%5E%7B-%7D%20%5CDelta%20y%5E%7B-%7D%7D%3D%5Cfrac%7B%5CDelta%20y%5E%7B-%7D%7D%7B%5CDelta%20x%5E%7B-%7D%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\Delta y^{+} &amp;=\frac{1}{2}\left(f\left(x^{0}+\Delta x^{+}\right)-f\left(x^{0}\right)\right) \\
&amp;+\frac{1}{2}\left(f\left(x^{0}+\Delta x^{-}+\Delta x^{+}\right)-f\left(x^{0}+\Delta x^{-}\right)\right) \\
\Delta y^{-} &amp;=\frac{1}{2}\left(f\left(x^{0}+\Delta x^{-}\right)-f\left(x^{0}\right)\right) \\
&amp;+\frac{1}{2}\left(f\left(x^{0}+\Delta x^{+}+\Delta x^{-}\right)-f\left(x^{0}+\Delta x^{+}\right)\right) \\
m_{\Delta x^{+} \Delta y^{+}} &amp;=\frac{C_{\Delta x^{+} y^{+}}}{\Delta x^{+}}=\frac{\Delta y^{+}}{\Delta x^{+}} ; m_{\Delta x^{-} \Delta y^{-}}=\frac{\Delta y^{-}}{\Delta x^{-}}
\end{aligned}" />   

    * This rule helps alleviating issue which arise from positive terms cancelling negative terms and vice versa.

* Target layer
    * Pre-softmax layer is taken as a target layer. Where, contributions are normalised.

**Results**
* MNIST: to change original class to target class, pixel importance are computed, and pixels are ranked in the order of their importance, and top 20% pixels are masked. The change in log odds of original vs target class is computed. It is found that DeepLift does much better than gradients, gradients*input, integrated gradient.

    <p align="center">
        <img width=600 src="images/deeplift_results.png">
        <em>Source: Author</em>
        </p>







    

