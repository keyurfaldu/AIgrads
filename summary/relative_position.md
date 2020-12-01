## Self-Attention with Relative Position Representations
### Peter Shaw, Jakob Uszkoreit, Ashish Vaswani
### 2018, Google Brain [[arXiv](https://arxiv.org/pdf/1803.02155.pdf)]

**Whats Unique**
Instead of relying on an unique positional embeddings, it incorporate relative positional distance based embeddings while computing contexulised representation and attention weights. It brings improvement of 1.3 BLEU score on WMT problem.

**How It Work**
* Attention works the following way
    * Contexulised representation:
    <img src="https://i.upmath.me/svg/%20z_%7Bi%7D%3D%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bi%20j%7D%5Cleft(x_%7Bj%7D%20W%5E%7BV%7D%5Cright)%20" alt=" z_{i}=\sum_{j=1}^{n} \alpha_{i j}\left(x_{j} W^{V}\right) " />

    * Attention weights

        <img src="https://i.upmath.me/svg/%20%5Calpha_%7Bi%20j%7D%3D%5Cfrac%7B%5Cexp%20e_%7Bi%20j%7D%7D%7B%5Csum_%7Bk%3D1%7D%5E%7Bn%7D%20%5Cexp%20e_%7Bi%20k%7D%7D" alt=" \alpha_{i j}=\frac{\exp e_{i j}}{\sum_{k=1}^{n} \exp e_{i k}}" /> 

    * Compatibility function for attention weights

        <img src="https://i.upmath.me/svg/%20e_%7Bi%20j%7D%3D%5Cfrac%7B%5Cleft(x_%7Bi%7D%20W%5E%7BQ%7D%5Cright)%5Cleft(x_%7Bj%7D%20W%5E%7BK%7D%5Cright)%5E%7BT%7D%7D%7B%5Csqrt%7Bd_%7Bz%7D%7D%7D" alt=" e_{i j}=\frac{\left(x_{i} W^{Q}\right)\left(x_{j} W^{K}\right)^{T}}{\sqrt{d_{z}}}" /> 

* Innovation: edge between the input elements x_i and x_j is represented by vectors a_ij^V, and a_ij^K. 
    * a_ij_V => edge information is added while coxtexual representations are being derived.

        <img src="https://i.upmath.me/svg/%20z_%7Bi%7D%3D%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bi%20j%7D%5Cleft(x_%7Bj%7D%20W%5E%7BV%7D%2Ba_%7Bi%20j%7D%5E%7BV%7D%5Cright)" alt=" z_{i}=\sum_{j=1}^{n} \alpha_{i j}\left(x_{j} W^{V}+a_{i j}^{V}\right)" /> 

    * a_ij_K is used in the compatibility function used to further compute attention weights

        <img src="https://i.upmath.me/svg/%20e_%7Bi%20j%7D%3D%5Cfrac%7Bx_%7Bi%7D%20W%5E%7BQ%7D%5Cleft(x_%7Bj%7D%20W%5E%7BK%7D%2Ba_%7Bi%20j%7D%5E%7BK%7D%5Cright)%5E%7BT%7D%7D%7B%5Csqrt%7Bd_%7Bz%7D%7D%7D" alt=" e_{i j}=\frac{x_{i} W^{Q}\left(x_{j} W^{K}+a_{i j}^{K}\right)^{T}}{\sqrt{d_{z}}}" /> 

    * Common weights are used accorss all different attention heads. And, clip function is used to clip relative positional distance to a threshold

        <img src="https://i.upmath.me/svg/%20%5Cbegin%7Baligned%7D%0Aa_%7Bi%20j%7D%5E%7BK%7D%20%26%3Dw_%7B%5Cmathrm%7Bclip%7D(j-i%2C%20k)%7D%5E%7BK%7D%20%5C%5C%0Aa_%7Bi%20j%7D%5E%7BV%7D%20%26%3Dw_%7B%5Cmathrm%7Bclip%7D(j-i%2C%20k)%7D%5E%7BV%7D%20%5C%5C%0A%5Coperatorname%7Bclip%7D(x%2C%20k)%20%26%3D%5Cmax%20(-k%2C%20%5Cmin%20(k%2C%20x))%0A%5Cend%7Baligned%7D" alt=" \begin{aligned}
a_{i j}^{K} &amp;=w_{\mathrm{clip}(j-i, k)}^{K} \\
a_{i j}^{V} &amp;=w_{\mathrm{clip}(j-i, k)}^{V} \\
\operatorname{clip}(x, k) &amp;=\max (-k, \min (k, x))
\end{aligned}" /> 

**Results**
* BLEU score for WMT is improved by 1.3 when this mechanism was used instead of absolute poitional embeddings. 




