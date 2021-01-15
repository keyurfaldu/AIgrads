## Technical report on conversational question answering
### Ju, Ying, Fubang Zhao, Shijie Chen, Bowen Zheng, Xuefeng Yang, and Yunfeng Liu.
### 2019 [[arXiv](https://arxiv.org/pdf/1909.10772.pdf)]

**Whats Unique**
This paper solves the question answering dataset CoQA with state of the art performance, with adversarial trainig, knowledge distillation, and ensemble. 

**How Does It Work**
* As its conversational QA, all the previous questions, with its answers are also given as the input. 

    <img src="https://i.upmath.me/svg/Q_%7Bk%7D%5E%7B*%7D%3D%5Cleft%5C%7BQ_%7B1%7D%2C%20A_%7B1%7D%2C%20%5Cldots%2C%20Q_%7Bk-1%7D%2C%20A_%7Bk-1%7D%2C%20Q_%7Bk%7D%5Cright%5C%7D" alt="Q_{k}^{*}=\left\{Q_{1}, A_{1}, \ldots, Q_{k-1}, A_{k-1}, Q_{k}\right\}" />

* There are four possible outcome, a free form text, Yes, No or Unknown. In case of all the answers except Unknown, a rationale is also generated.

* The base loss is computed by computing logitd for all these four options, and putting a softmax on top of it.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ap%5E%7Bs%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cleft%5Bl%5E%7Bs%7D%2C%20l%5E%7By%7D%2C%20l%5E%7Bn%7D%2C%20l%5E%7Bu%7D%5Cright%5D%5Cright)%20%5C%5C%0Ap%5E%7Be%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cleft%5Bl%5E%7Be%7D%2C%20l%5E%7By%7D%2C%20l%5E%7Bn%7D%2C%20l%5E%7Bu%7D%5Cright%5D%5Cright)%20%5C%5C%0A%5Cmathcal%7BL%7D_%7B%5Ctext%20%7BBase%20%7D%7D%20%26%3D-%5Cfrac%7B1%7D%7B2%20N%7D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%5Cleft(%5Clog%20p_%7By_%7Bi%7D%5E%7Bs%7D%7D%5E%7Bs%7D%2B%5Clog%20p_%7By_%7Bi%7D%5E%7Be%7D%7D%5E%7Be%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
p^{s} &amp;=\operatorname{softmax}\left(\left[l^{s}, l^{y}, l^{n}, l^{u}\right]\right) \\
p^{e} &amp;=\operatorname{softmax}\left(\left[l^{e}, l^{y}, l^{n}, l^{u}\right]\right) \\
\mathcal{L}_{\text {Base }} &amp;=-\frac{1}{2 N} \sum_{i=1}^{N}\left(\log p_{y_{i}^{s}}^{s}+\log p_{y_{i}^{e}}^{e}\right)
\end{aligned}" />

* Rationale Tagging Loss: Each token is evaluated if it is a part of rationale or not, and accordingly cross entropy loss is evaluated.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0Ap_%7Bt%7D%5E%7Br%7D%3D%5Coperatorname%7Bsigmoid%7D%5Cleft(w_%7B2%7D%20%5Coperatorname%7BRelu%7D%5Cleft(W_%7B1%7D%20h_%7Bt%7D%5Cright)%5Cright)%5C%5C%0A%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BRTi%7D%7D%3D-%5Cfrac%7B1%7D%7BT%7D%20%5Csum_%7Bt%3D1%7D%5E%7BT%7D%5Cleft(y_%7Bi%20t%7D%5E%7Br%7D%20%5Clog%20p_%7Bi%20t%7D%5E%7Br%7D%2B%5Cleft(1-y_%7Bi%20t%7D%5Cright)%20%5Clog%20%5Cleft(1-p_%7Bi%20t%7D%5E%7Br%7D%5Cright)%5Cright)%20%5C%5C%0A%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BRT%7D%7D%3D%5Cfrac%7B1%7D%7BN%7D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BRTi%7D%7D%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
p_{t}^{r}=\operatorname{sigmoid}\left(w_{2} \operatorname{Relu}\left(W_{1} h_{t}\right)\right)\\
\mathcal{L}_{\mathrm{RTi}}=-\frac{1}{T} \sum_{t=1}^{T}\left(y_{i t}^{r} \log p_{i t}^{r}+\left(1-y_{i t}\right) \log \left(1-p_{i t}^{r}\right)\right) \\
\mathcal{L}_{\mathrm{RT}}=\frac{1}{N} \sum_{i=1}^{N} \mathcal{L}_{\mathrm{RTi}}
\end{array}" />

    * Rationale probability, P_t^r is used to compute the attention for the internal representation of each token, which is then used to computed yes/no/unknown logits.

* Adversarial Training Loss: Computed gradient with repsect to input embeddings, and based on that create input purturbations:
    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0Ag_%7Bw%7D%3D-%5Cnabla%20v_%7Bw%7D%20%5Cmathcal%7BL%7D%5Cleft(y_%7Bi%7D%20%5Cmid%20v_%7Bw%7D%20%3B%20%5Chat%7B%5Ctheta%7D%5Cright)%20%5C%5C%0Av_%7Bw%7D%5E%7B*%7D%3Dv_%7Bw%7D%2B%5Cepsilon%20g_%7Bw%7D%20%2F%5Cleft%5C%7Cg_%7Bw%7D%5Cright%5C%7C_%7B2%7D%5C%5C%0A%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BAT%7D%7D(%5Ctheta)%3D-%5Cfrac%7B1%7D%7BN%7D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20C%20r%20o%20s%20s%20E%20n%20t%20%5Coperatorname%7Brop%7D%20y%5Cleft(%5Ccdot%20%5Cmid%20V%5E%7B*%7D%20%3B%20%5Ctheta%5Cright)%5C%5C%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
g_{w}=-\nabla v_{w} \mathcal{L}\left(y_{i} \mid v_{w} ; \hat{\theta}\right) \\
v_{w}^{*}=v_{w}+\epsilon g_{w} /\left\|g_{w}\right\|_{2}\\
\mathcal{L}_{\mathrm{AT}}(\theta)=-\frac{1}{N} \sum_{i=1}^{N} C r o s s E n t \operatorname{rop} y\left(\cdot \mid V^{*} ; \theta\right)\\
\end{array}" /> 
* Virtual Adversarial Training (VAT): it uses un-supervised adversarial perturbations. First, it adds random noise to the input, compute KL divergence on posterior probabilities between acutal input embedding and purturbated input embeddings, and create the perturbations with estimated gradients based on that KL divergence.

    <img src="https://i.upmath.me/svg/v_%7Bw%7D%5E%7B%5Cprime%7D%3Dv_%7Bw%7D%2B%5Cxi%20d_%7Bw%7D%5C%5C%0Ag_%7Bw%7D%3D%5Cnabla_%7Bv%5E%7B%5Cprime%7D%7D%20D_%7B%5Cmathrm%7BKL%7D%7D%5Cleft(p%5Cleft(%5Ccdot%20%5Cmid%20v_%7Bw%7D%20%3B%20%5Chat%7B%5Ctheta%7D%5Cright)%20%5C%7C%20p%5Cleft(%5Ccdot%20%5Cmid%20v_%7Bw%7D%5E%7B%5Cprime%7D%20%3B%20%5Chat%7B%5Ctheta%7D%5Cright)%5Cright)%5C%5C%0Av_%7Bw%7D%5E%7B*%7D%3Dv_%7Bw%7D%2B%5Cepsilon%20g_%7Bw%7D%20%2F%5Cleft%5C%7Cg_%7Bw%7D%5Cright%5C%7C_%7B2%7D%5C%5C%0A%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BVAT%7D%7D(%5Ctheta)%3D%5Cfrac%7B1%7D%7BN%7D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20D_%7B%5Cmathrm%7BKL%7D%7D%5Cleft(p(%5Ccdot%20%5Cmid%20V%20%3B%20%5Ctheta)%20%5C%7C%20p%5Cleft(%5Ccdot%20%5Cmid%20V%5E%7B*%7D%20%3B%20%5Ctheta%5Cright)%5Cright)%0A" alt="v_{w}^{\prime}=v_{w}+\xi d_{w}\\
g_{w}=\nabla_{v^{\prime}} D_{\mathrm{KL}}\left(p\left(\cdot \mid v_{w} ; \hat{\theta}\right) \| p\left(\cdot \mid v_{w}^{\prime} ; \hat{\theta}\right)\right)\\
v_{w}^{*}=v_{w}+\epsilon g_{w} /\left\|g_{w}\right\|_{2}\\
\mathcal{L}_{\mathrm{VAT}}(\theta)=\frac{1}{N} \sum_{i=1}^{N} D_{\mathrm{KL}}\left(p(\cdot \mid V ; \theta) \| p\left(\cdot \mid V^{*} ; \theta\right)\right)
" />
* Distillation Loss over N teacher models trained with different hyper parameters:

    <img src="https://i.upmath.me/svg/p_%7Bi%7D%5E%7Bk%20d%7D%3D%5Cfrac%7B1%7D%7B%5Cmathcal%7BT%7D%7D%20%5Csum_%7B%5Ctau%3D1%7D%5E%7B%5Cmathcal%7BT%7D%7D%20f%5Cleft(x%5E%7Bi%7D%2C%20%5Ctheta%5E%7B%5Ctau%7D%5Cright)%5C%5C%0A%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BKD%7D%7D%5Cleft(%5Ctheta%5E%7Bs%7D%5Cright)%3D-%5Cfrac%7B1%7D%7BN%20T%7D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20p_%7Bi%20t%7D%5E%7Bk%20d%7D%20%5Clog%20f%5Cleft(x_%7Bi%20t%7D%2C%20%5Ctheta%5E%7Bs%7D%5Cright)" alt="p_{i}^{k d}=\frac{1}{\mathcal{T}} \sum_{\tau=1}^{\mathcal{T}} f\left(x^{i}, \theta^{\tau}\right)\\
\mathcal{L}_{\mathrm{KD}}\left(\theta^{s}\right)=-\frac{1}{N T} \sum_{i=1}^{N} \sum_{t=1}^{T} p_{i t}^{k d} \log f\left(x_{i t}, \theta^{s}\right)" />

* Final Loss is computed as below:
<img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BS%7D%7D%3D%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BBD%7D%7D%2B%5Cbeta_%7B1%7D%20%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BRA%7D%7D%2B%5Cbeta_%7B2%7D%20%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BAT%7D%7D%2B%5Cbeta_%7B3%7D%20%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BVAT%7D%7D%2B%5Cbeta_%7B4%7D%20%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BKD%7D%7D" alt="\mathcal{L}_{\mathrm{S}}=\mathcal{L}_{\mathrm{BD}}+\beta_{1} \mathcal{L}_{\mathrm{RA}}+\beta_{2} \mathcal{L}_{\mathrm{AT}}+\beta_{3} \mathcal{L}_{\mathrm{VAT}}+\beta_{4} \mathcal{L}_{\mathrm{KD}}" />

* Ensembles: Further it takes ensembles of such models, around 68 different models were trained, and in one setting, top 5 models were selected based on Genetic Algorithm, to produce state of the art performance on CoQA task.