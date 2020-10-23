## UNILMv2: Pseudo-Masked Language Models for Unified Language Model Pre-Training
### Hangbo Bao et al. 
### 2020 [[arXiv](https://arxiv.org/pdf/2002.12804.pdf)]

**Whats Unique**
It invents an unified language model for both autoencoding (BERT like) and partially autoregressive language (XLNet for Span) modeling tasks using a novel training procedure referred to as a pseudo masked language modelling. 

**How It Works**
* Conventional masks to learn inter-relation between corrupted tokens and context via auto-encoding. 
* Pseudo masks learn intra-relations between masked spans via partially auto-regressive modeling.

<p align="center">
    <img width=600 src="images/unilmv2_illustration.png">
    <em>Source: Author</em>
    </p>

* Auto encoding objective remains conventional.
* Partially auto regressive objective lets psedo masked span attend to prior predicted tokens, and corresponding masked tokens. 

Following table gives an overview of how Auto Encoding, Auto Regressive objective, and Partially Auto Regressive objective. 

<p align="center">
    <img width=600 src="images/unilmv2_objectives_comparision.png">
    <em>Source: Author</em>
    </p>

Following figure shows pseudo masked language models for Unified model pre-training. It appends input sequence with pseudo masked tokens as well as original tokens for masked ones. And, with attention mechanism it trains model with dual objectives at the same time.

<p align="center">
    <img width=600 src="images/unilmv2_architecture.png">
    <em>Source: Author</em>
    </p>

**Model**

* Auto encoding loss

<img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BAE%7D%7D%3D-%5Csum_%7Bx%20%5Cin%20%5Cmathcal%7BD%7D%7D%20%5Clog%20%5Cprod_%7Bm%20%5Cin%20M%7D%20p%5Cleft(x_%7Bm%7D%20%5Cmid%20x_%7B%5Cbackslash%20M%7D%5Cright)" alt="\mathcal{L}_{\mathrm{AE}}=-\sum_{x \in \mathcal{D}} \log \prod_{m \in M} p\left(x_{m} \mid x_{\backslash M}\right)" />

* Partially Auto-regressive Modelling
    * In each factorization step, a model can predict one or multiple tokens.
    * Let M = < M1, M2, .. M_|M|> is factorization order, where M_i = {m_1, .., m_i}, or set of token span to be masked in factorisation step i
    * <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ap%5Cleft(x_%7BM%7D%20%5Cmid%20x_%7B%5Cbackslash%20M%7D%5Cright)%20%26%3D%5Cprod_%7Bi%3D1%7D%5E%7B%7CM%7C%7D%20p%5Cleft(x_%7BM_%7Bi%7D%7D%20%5Cmid%20x_%7B%5Cbackslash%20M_%7B%5Cgeq%20i%7D%7D%5Cright)%20%5C%5C%0A%26%3D%5Cprod_%7Bi%3D1%7D%5E%7B%7CM%7C%7D%20%5Cprod_%7Bm%20%5Cin%20M_%7Bi%7D%7D%20p%5Cleft(x_%7Bm%7D%20%5Cmid%20x_%7B%5Cbackslash%20M%20%5Cgeq%20i%7D%5Cright.%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
p\left(x_{M} \mid x_{\backslash M}\right) &amp;=\prod_{i=1}^{|M|} p\left(x_{M_{i}} \mid x_{\backslash M_{\geq i}}\right) \\
&amp;=\prod_{i=1}^{|M|} \prod_{m \in M_{i}} p\left(x_{m} \mid x_{\backslash M \geq i}\right.
\end{aligned}" />

    * <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BPAR%7D%7D%3D-%5Csum_%7Bx%20%5Cin%20%5Cmathcal%7BD%7D%7D%20%5Cmathbb%7BE%7D_%7BM%7D%20%5Clog%20p%5Cleft(x_%7BM%7D%20%5Cmid%20x_%7B%5Cbackslash%20M%7D%5Cright)" alt="\mathcal{L}_{\mathrm{PAR}}=-\sum_{x \in \mathcal{D}} \mathbb{E}_{M} \log p\left(x_{M} \mid x_{\backslash M}\right)" />

* Following figure illustrate the implementation details at attention mask level.

<p align="center">
    <img width=600 src="images/unilmv2_implementation.png">
    <em>Source: Author</em>
    </p>
