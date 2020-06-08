**Internal Covariate Shift**: Change in distribution of network activations due to change in network parameters during traing.
This paper aims to reduce Internal Covariate Shift, by taking following actions:
* Instead of whitelisting features inputs and outputs jointly, it normalise each scalar feature independently, by making its mean zero and variance 1.
* Each dimension of d-dimensional features would be normalised as follow 
<p align="center">
<img align="centre" src="https://render.githubusercontent.com/render/math?math=\Large \hat%20x^{(k)}%20=%20\frac{x^{k}-E[x^{k}]}{\sqrt{Var[x^{k}]}}">
</p>

* Simply normalizing the inputs to each layer may change what input represents itself, i.e. normalizing the inputs to sigmoid would always constraint it to be on the linear regime of non-linearity. In order to solve this problem, we have introduced scale and shift parameters as model parameters to be learned as well.
<p align="center">
<img align="centre", src="https://render.githubusercontent.com/render/math?math=\Large%20y^{(k)}%20=%20\gamma^{(k)}\hat%20x^{(k)}%20%2B%20\beta^{(k)}">
</p>


Batch normalization reduces the dependencies on the scale of parameters and their initial values, that has beneficial effect on the gradient flow through network, 
* It allows use of much higher learning rates
* It regularize the model as well
* It makes it possible to use saturating nonlinearities by preventing the network from getting stuck in the saturated mode.
