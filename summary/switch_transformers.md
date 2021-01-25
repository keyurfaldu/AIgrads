## Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity.
### Fedus, William, Barret Zoph, and Noam Shazeer.
### arXiv preprint arXiv:2101.03961 (2021) [[arXiv](https://arxiv.org/pdf/2101.03961.pdf)].

**Whats Unique**
In Deep Leanring, models typically reuse the same parameters for all inputs. The Mixture of Experts (MoE) models defy this and instead select different parameters for each incoming example, which results in sparsely-activared model. It has outrageous numbers of parameters but a constant computational cost. 

It suffers from complexity, communication costs and training instability. Switch Transformers address these challanges and obtain upto 7x increases in pre-training speed.

**Architecture**
* The Fully Connected Dense Feed Forward Network layer is replaced by sparse Switch FFN layer. Where, router independently route the input sample.
* Following figure demonstrate the same.

<p align="center">
    <img width=600 src="images/switch_arch.png">
    <em>Source: Author</em>
    </p>

* More the numbers of experts, more would be sparse model parameters, but it scales well interms of model performance, i.e. perplexity. Which can be seen in the figure below.

<p align="center">
    <img width=600 src="images/switch_scaling.png">
    <em>Source: Author</em>
    </p>

**Sparse Routing**
* Mixture of Expert Routing (Shazeer et al. 2017)

    <img src="https://i.upmath.me/svg/h(x)%3DW_%7Br%7D%20%5Ccdot%20x%5C%5C%0Ap_%7Bi%7D(x)%3D%5Cfrac%7Be%5E%7Bh(x)_%7Bi%7D%7D%7D%7B%5Csum_%7Bj%7D%5E%7BN%7D%20e%5E%7Bh(x)_%7Bj%7D%7D%7D%5C%5C%0Ay%3D%5Csum_%7Bi%20%5Cin%20%5Cmathcal%7BT%7D%7D%20p_%7Bi%7D(x)%20E_%7Bi%7D(x)" alt="h(x)=W_{r} \cdot x\\
    p_{i}(x)=\frac{e^{h(x)_{i}}}{\sum_{j}^{N} e^{h(x)_{j}}}\\
    y=\sum_{i \in \mathcal{T}} p_{i}(x) E_{i}(x)" />

* Switch Routing: Author uses K=1 in Mixture of Expert Routing setup. It has following benefits
    * Router computation is reduced, as now input token is routed to only single expert.
    * The batch size of each expert would be small, as it only needs to consider the tokens being routed to a single expert.
    * Each expert has the fixed batch size, i.e. (total_tokens / num_experts ) * capacity_factor. If an expert recieve extra tokens, these tokens would be forwarded as they are. Capacity factor would enable more expert capacity, but it would add extra blank tokens to other experts.
    * Differentiable Loss:
        <img src="https://i.upmath.me/svg/%0A%5Coperatorname%7Bloss%7D%3D%5Calpha%20N%20%5Ccdot%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20f_%7Bi%7D%20%5Ccdot%20P_%7Bi%7D%5C%5C%0Af_%7Bi%7D%3D%5Cfrac%7B1%7D%7BT%7D%20%5Csum_%7Bx%20%5Cin%20%5Cmathcal%7BB%7D%7D%20%5Cmathbb%7B1%7D%5C%7B%5Coperatorname%7Bargmax%7D%20p(x)%2C%20i%5C%7D%5C%5C%0AP_%7Bi%7D%3D%5Cfrac%7B1%7D%7BT%7D%20%5Csum_%7Bx%20%5Cin%20%5Cmathcal%7BB%7D%7D%20p_%7Bi%7D(x)%0A" alt="
\operatorname{loss}=\alpha N \cdot \sum_{i=1}^{N} f_{i} \cdot P_{i}\\
f_{i}=\frac{1}{T} \sum_{x \in \mathcal{B}} \mathbb{1}\{\operatorname{argmax} p(x), i\}\\
P_{i}=\frac{1}{T} \sum_{x \in \mathcal{B}} p_{i}(x)
" />
    * Note, f_i is not differentiable, but P_i is differentiable. 

**Key Decisions**
* Selective Precision: floating16 precision can exacerbate the instability. So, only in the local part of the model floating32 precision was used, and rest were reduced to fp16.
* Smaller parameters initialisation further improves the stability. Where, paraters to initialise models are scaled by 0.1. This improves the std dev of quality.
* A smaller dataset, with large parameter sized model would cause the problem of over-fitting. Expert dropout is increased to handle this, upto 40%.







