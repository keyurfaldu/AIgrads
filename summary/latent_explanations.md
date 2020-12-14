## Towards Interpretable Natural Language Understanding with Explanations as Latent Variables
### Zhou, Hu, Zhang, Liang, Sun, Xiong, Tang et al. 
### [[arXiv](https://arxiv.org/pdf/2011.05268.pdf)]

**Whats Unique**
A new framework where explnations considered as latent variables for underlying reasoning process of a neural model. That way, it can work with small dataset of human annotated explanations. Variational EM framework for optimisation enable an explanation generation module and explanation augmented prediction module. It also extend the framework where pesudo labels and explnations are iteratively generated and improves each other. 


**How It Works**
* ELV (Explanation as Latent Variable) Framework
    * Natural langauge explanations are treated as latent variable
    * Jointly trains explanation generation and explanation augmented prediction
    * ELV framework is being leveraged in semi-supervised learning, where for pseudo lables, explnations are generated iteratively. 
    * Emperical validation on tasks of relation extraction and sentiment analysis.

* Architecture Diagram
    <p align="center">
    <img width=600 src="images/latent_explanations_architecture.png">
    <em>Source: Author</em>
    </p>

* Formulation: We can formulate problem as the variational EM problem, 

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Clog%20p(y%20%5Cmid%20x)%20%26%3D%5Clog%20%5Cint%20p(e%2C%20y%20%5Cmid%20x)%20d%20e%3D%5Clog%20%5Cint%20q_%7B%5Ctheta%7D(e%20%5Cmid%20x%2C%20y)%20%5Cfrac%7Bp(e%2C%20y%20%5Cmid%20x)%7D%7Bq_%7B%5Ctheta%7D(e%20%5Cmid%20x%2C%20y)%7D%20d%20e%20%5C%5C%0A%26%20%5Cgeq%20%5Cmathcal%7BL%7D(%5Ctheta%2C%20%5Cphi)%3DE_%7Bq_%7B%5Ctheta%7D(e%20%5Cmid%20x%2C%20y)%7D%20%5Clog%20%5Cfrac%7Bp(e%2C%20y%20%5Cmid%20x)%7D%7Bq_%7B%5Ctheta%7D(e%20%5Cmid%20x%2C%20y)%7D%3DE_%7Bq_%7B%5Ctheta%7D(e%20%5Cmid%20x%2C%20y)%7D%20%5Clog%20%5Cfrac%7Bp_%7B%5Cphi%7D(y%20%5Cmid%20e%2C%20x)%20p(e%20%5Cmid%20x)%7D%7Bq_%7B%5Ctheta%7D(e%20%5Cmid%20x%2C%20y)%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\log p(y \mid x) &amp;=\log \int p(e, y \mid x) d e=\log \int q_{\theta}(e \mid x, y) \frac{p(e, y \mid x)}{q_{\theta}(e \mid x, y)} d e \\
&amp; \geq \mathcal{L}(\theta, \phi)=E_{q_{\theta}(e \mid x, y)} \log \frac{p(e, y \mid x)}{q_{\theta}(e \mid x, y)}=E_{q_{\theta}(e \mid x, y)} \log \frac{p_{\phi}(y \mid e, x) p(e \mid x)}{q_{\theta}(e \mid x, y)}
\end{aligned}" />

* As we can notice, qθ(e|x, y), where θ is optimised in E-step. UniLM is used for generating explanations given x, and y.

* Whereas, φ in pφ(y|e, x) is optimised in M step. MLP over BERT contextual representation is used to predict the probability of the label. 

**Results**
* For both supervised, and semi-supervised settings, for both the tasks of relation extraction and sentiment analysis, this approach have given better results.


