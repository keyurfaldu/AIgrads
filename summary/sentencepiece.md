## SentencePiece: Subword Regularization: Improving Neural Network Translation Models with Multiple Subword Candidates
### Taku Kudo
### Google, 2018

**Whats New** This paper puts probablistic approach (subword sampling) on segmenting sentences into tokens limited to vocabolaries of subwords. It also propose a unigram langugage model to derive vocabolary and associated probabilities. 

**How it works**
* On the fly subword sampling:
    * As an usecase, NML system aims to translate y from x, with following mathematical formulation

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cleft%5C%7B%5Cleft%5Clangle%20X%5E%7B(s)%7D%2C%20Y%5E%7B(s)%7D%5Cright%5Crangle%5Cright%5C%7D_%7Bs%3D1%7D%5E%7B%7CD%7C%7D%20%26%3D%5Cleft%5C%7B%5Cleft%5Clangle%5Cmathbf%7Bx%7D%5E%7B(s)%7D%2C%20%5Cmathbf%7By%7D%5E%7B(s)%7D%5Cright%5Crangle%5Cright%5C%7D_%7Bs%3D1%7D%5E%7B%7CD%7C%7D%20%5C%5C%0A%5Ctheta_%7BM%20L%20E%7D%20%26%3D%5Cunderset%7B%5Ctheta%7D%7B%5Carg%20%5Cmax%20%7D%20%5Cmathcal%7BL%7D(%5Ctheta)%20%5C%5C%0AWhere%2C%20%5Cmathcal%7BL%7D(%5Ctheta)%20%26%3D%5Csum_%7Bs%3D1%7D%5E%7B%7CD%7C%7D%20%5Clog%20P%5Cleft(%5Cmathbf%7By%7D%5E%7B(s)%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5E%7B(s)%7D%20%3B%20%5Ctheta%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\left\{\left\langle X^{(s)}, Y^{(s)}\right\rangle\right\}_{s=1}^{|D|} &amp;=\left\{\left\langle\mathbf{x}^{(s)}, \mathbf{y}^{(s)}\right\rangle\right\}_{s=1}^{|D|} \\
\theta_{M L E} &amp;=\underset{\theta}{\arg \max } \mathcal{L}(\theta) \\
Where, \mathcal{L}(\theta) &amp;=\sum_{s=1}^{|D|} \log P\left(\mathbf{y}^{(s)} \mid \mathbf{x}^{(s)} ; \theta\right)
\end{aligned}" />

    * In subword regularisation, each segmentation x from in input X has its own proabability, so loss is minimised as follow

        <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Ctext%20%7Bmarginal%7D%7D(%5Ctheta)%3D%5Csum_%7Bs%3D1%7D%5E%7B%7CD%7C%7D%20%5Cmathbb%7BE%7D_%7B%5Cmathbf%7Bx%7D%20%5Csim%20P%5Cleft(%5Cmathbf%7Bx%7D%20%5Cmid%20X%5E%7B(s)%7D%5Cright)%7D%5B%5Clog%20P(%5Cmathbf%7By%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%20%3B%20%5Ctheta)%5D" alt="\mathcal{L}_{\text {marginal}}(\theta)=\sum_{s=1}^{|D|} \mathbb{E}_{\mathbf{x} \sim P\left(\mathbf{x} \mid X^{(s)}\right)}[\log P(\mathbf{y} \mid \mathbf{x} ; \theta)]" />
    
    * However, computing above over all posibilities is expensive, so we can approximate it with k possibilities, 

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cmathcal%7BL%7D_%7B%5Ctext%20%7Bmarginal%7D%7D(%5Ctheta)%20%26%20%5Ccong%20%5Cfrac%7B1%7D%7Bk%5E%7B2%7D%7D%20%5Csum_%7Bs%3D1%7D%5E%7B%7CD%7C%7D%20%5Csum_%7Bi%3D1%7D%5E%7Bk%7D%20%5Csum_%7Bj%3D1%7D%5E%7Bk%7D%20%5Clog%20P%5Cleft(%5Cmathbf%7By%7D_%7Bj%7D%20%5Cmid%20%5Cmathbf%7Bx%7D_%7Bi%7D%20%3B%20%5Ctheta%5Cright)%20%5C%5C%0A%5Cmathbf%7Bx%7D_%7Bi%7D%20%26%20%5Csim%20P%5Cleft(%5Cmathbf%7Bx%7D%20%5Cmid%20X%5E%7B(s)%7D%5Cright)%2C%20%5Cquad%20%5Cmathbf%7By%7D_%7Bj%7D%20%5Csim%20P%5Cleft(%5Cmathbf%7By%7D%20%5Cmid%20Y%5E%7B(s)%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
    \mathcal{L}_{\text {marginal}}(\theta) &amp; \cong \frac{1}{k^{2}} \sum_{s=1}^{|D|} \sum_{i=1}^{k} \sum_{j=1}^{k} \log P\left(\mathbf{y}_{j} \mid \mathbf{x}_{i} ; \theta\right) \\
    \mathbf{x}_{i} &amp; \sim P\left(\mathbf{x} \mid X^{(s)}\right), \quad \mathbf{y}_{j} \sim P\left(\mathbf{y} \mid Y^{(s)}\right)
    \end{aligned}" /> 

    * But if we limit k=1, then in online setting, after sufficient mini-batch iterations it would alsop be able to approximate above. 

* Unigram Language Modelling
    * It needs to derive p(x), and all possible x \in S(X), where S(X) are all possible ways of segmenting over some vocabolary. Where as vocabalory is also not fixed, so it becomes an intractable problem.
    * Unigram langauge model estimates probablity of each subword x_i, p(x_i), and with following MLE estimation:
        <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D%3D%5Csum_%7Bs%3D1%7D%5E%7B%7CD%7C%7D%20%5Clog%20%5Cleft(P%5Cleft(X%5E%7B(s)%7D%5Cright)%5Cright)%3D%5Csum_%7Bs%3D1%7D%5E%7B%7CD%7C%7D%20%5Clog%20%5Cleft(%5Csum_%7B%5Cmathbf%7Bx%7D%20%5Cin%20%5Cmathcal%7BS%7D%5Cleft(X%5E%7B(s)%7D%5Cright)%7D%20P(%5Cmathbf%7Bx%7D)%5Cright)" alt="\mathcal{L}=\sum_{s=1}^{|D|} \log \left(P\left(X^{(s)}\right)\right)=\sum_{s=1}^{|D|} \log \left(\sum_{\mathbf{x} \in \mathcal{S}\left(X^{(s)}\right)} P(\mathbf{x})\right)" /> 
    * Vocabloary is chosen as below:
        * Fix a big seed vocab
        * optimize p(x) using EM algorithm
        * compute loss for each subword x_i, i.e. if it is removed from vocab, how the loss would be reduced.
        * keep 80% or such top-x_i, and remove rest from vocabolary.
        * repeat the process till desired vocab length is met.

* Subword sampling:
    * l-best segmentation approach
        * l-best segmentations according to the probability P(x|X)
        * One segmentation x_i is then sampled from the multinomial distribution 
        <img src="https://i.upmath.me/svg/P%5Cleft(%5Cmathbf%7Bx%7D_%7Bi%7D%20%5Cmid%20X%5Cright)%20%5Ccong%20P%5Cleft(%5Cmathbf%7Bx%7D_%7Bi%7D%5Cright)%5E%7B%5Calpha%7D%20%2F%20%5Csum_%7Bi%3D1%7D%5E%7Bl%7D%20P%5Cleft(%5Cmathbf%7Bx%7D_%7Bi%7D%5Cright)%5E%7B%5Calpha%7D" alt="P\left(\mathbf{x}_{i} \mid X\right) \cong P\left(\mathbf{x}_{i}\right)^{\alpha} / \sum_{i=1}^{l} P\left(\mathbf{x}_{i}\right)^{\alpha}" />
        where, alpha is smoothing parameter.

**Performance**
* It gives consistent better performance on NMT task over in-domain and out-domain datasets. 