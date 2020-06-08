Internal Covariate Shift: Change in distribution of network activations due to change in network parameters during traing.
This paper aims to reduce Internal Covariate Shift, by taking following actions:
* Instead of whitelisting features inputs and outputs jointly, it normalise each scalar feature independently, by making its mean zero and variance 1.
* Each dimension of d-dimensional features would be normalised as follow 
<img align="centre" src="https://render.githubusercontent.com/render/math?math=\Large \hat%20x^{(k)}%20=%20\frac{x^{k}-E[x^{k}]}{\sqrt{Var[x^{k}]}}">
