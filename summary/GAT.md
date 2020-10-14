## GRAPH ATTENTION NETWORKS
### Petar Velickovi, Yoshua Bengio et. al
### ICLR 2018 [[arXiv](https://arxiv.org/pdf/1710.10903.pdf)]

**Whats Unique**
This paper presnet a novel neural network architecture, graph attention network, which can operate on graph structured data, leveraging masked self attention layers.

**How It Works**
* Graph Attention Layer
    * Input to layer is h, where each node in 1..N has F features, where as output would have each layer F' features.

        <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D%3D%5Cleft%5C%7B%5Cvec%7Bh%7D_%7B1%7D%2C%20%5Cvec%7Bh%7D_%7B2%7D%2C%20%5Cldots%2C%20%5Cvec%7Bh%7D_%7BN%7D%5Cright%5C%7D%2C%20%5Cvec%7Bh%7D_%7Bi%7D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7BF%7D%5C%5C%0A%5Cmathbf%7Bh%7D%5E%7B%5Cprime%7D%3D%5Cleft%5C%7B%5Cvec%7Bh%7D_%7B1%7D%5E%7B%5Cprime%7D%2C%20%5Cvec%7Bh%7D_%7B2%7D%5E%7B%5Cprime%7D%2C%20%5Cldots%2C%20%5Cvec%7Bh%7D_%7BN%7D%5E%7B%5Cprime%7D%5Cright%5C%7D%2C%20%5Cvec%7Bh%7D_%7Bi%7D%5E%7B%5Cprime%7D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7BF%5E%7B%5Cprime%7D%7D" alt="\mathbf{h}=\left\{\vec{h}_{1}, \vec{h}_{2}, \ldots, \vec{h}_{N}\right\}, \vec{h}_{i} \in \mathbb{R}^{F}\\
\mathbf{h}^{\prime}=\left\{\vec{h}_{1}^{\prime}, \vec{h}_{2}^{\prime}, \ldots, \vec{h}_{N}^{\prime}\right\}, \vec{h}_{i}^{\prime} \in \mathbb{R}^{F^{\prime}}" />

    * For each edge a, an attention fucntion 'a' is applied (i.e.. dot product in Transformers). Attention weights are computed by normalising it.

        <img src="https://i.upmath.me/svg/e_%7Bi%20j%7D%3Da%5Cleft(%5Cmathbf%7BW%7D%20%5Cvec%7Bh%7D_%7Bi%7D%2C%20%5Cmathbf%7BW%7D%20%5Cvec%7Bh%7D_%7Bj%7D%5Cright)%5C%5C%0A%5Calpha_%7Bi%20j%7D%3D%5Coperatorname%7Bsoftmax%7D_%7Bj%7D%5Cleft(e_%7Bi%20j%7D%5Cright)%3D%5Cfrac%7B%5Cexp%20%5Cleft(e_%7Bi%20j%7D%5Cright)%7D%7B%5Csum_%7Bk%20%5Cin%20%5Cmathcal%7BN%7D_%7Bi%7D%7D%20%5Cexp%20%5Cleft(e_%7Bi%20k%7D%5Cright)%7D" alt="e_{i j}=a\left(\mathbf{W} \vec{h}_{i}, \mathbf{W} \vec{h}_{j}\right)\\
\alpha_{i j}=\operatorname{softmax}_{j}\left(e_{i j}\right)=\frac{\exp \left(e_{i j}\right)}{\sum_{k \in \mathcal{N}_{i}} \exp \left(e_{i k}\right)}" />

    * This paper presents a new attention function, with parameterised vector and LeakyRelu activation function. 

        <img src="https://i.upmath.me/svg/%5Calpha_%7Bi%20j%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(%5Ctext%20%7B%20LeakyReLU%20%7D%5Cleft(%5Coverrightarrow%7B%5Cmathbf%7Ba%7D%7D%5E%7BT%7D%5Cleft%5B%5Cmathbf%7BW%7D%20%5Cvec%7Bh%7D_%7Bi%7D%20%5C%7C%20%5Cmathbf%7BW%7D%20%5Cvec%7Bh%7D_%7Bj%7D%5Cright%5D%5Cright)%5Cright)%7D%7B%5Csum_%7Bk%20%5Cin%20%5Cmathcal%7BN%7D_%7Bi%7D%7D%20%5Cexp%20%5Cleft(%5Ctext%20%7B%20LeakyReLU%20%7D%5Cleft(%5Coverrightarrow%7B%5Cmathbf%7Ba%7D%7D%5E%7BT%7D%5Cleft%5B%5Cmathbf%7BW%7D%20%5Cvec%7Bh%7D_%7Bi%7D%20%5C%7C%20%5Cmathbf%7BW%7D%20%5Cvec%7Bh%7D_%7Bk%7D%5Cright%5D%5Cright)%5Cright)%7D%5C%5C%0Awhere%2C%20%5Coverrightarrow%7B%5Cmathbf%7Ba%7D%7D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7B2%20F%5E%7B%5Cprime%7D%7D" alt="\alpha_{i j}=\frac{\exp \left(\text { LeakyReLU }\left(\overrightarrow{\mathbf{a}}^{T}\left[\mathbf{W} \vec{h}_{i} \| \mathbf{W} \vec{h}_{j}\right]\right)\right)}{\sum_{k \in \mathcal{N}_{i}} \exp \left(\text { LeakyReLU }\left(\overrightarrow{\mathbf{a}}^{T}\left[\mathbf{W} \vec{h}_{i} \| \mathbf{W} \vec{h}_{k}\right]\right)\right)}\\
where, \overrightarrow{\mathbf{a}} \in \mathbb{R}^{2 F^{\prime}}" />

    * Take attention weighted representation from neighbours and apply non-linearity. And, we can also formalise it as multihead attention, i.e. K.

    <img src="https://i.upmath.me/svg/%5Cvec%7Bh%7D_%7Bi%7D%5E%7B%5Cprime%7D%3D%5Csigma%5Cleft(%5Csum_%7Bj%20%5Cin%20%5Cmathcal%7BN%7D_%7Bi%7D%7D%20%5Calpha_%7Bi%20j%7D%20%5Cmathbf%7BW%7D%20%5Cvec%7Bh%7D_%7Bj%7D%5Cright)%5C%5C%0A%5Cvec%7Bh%7D_%7Bi%7D%5E%7B%5Cprime%7D%3D%5C%7C_%7Bk%3D1%7D%5E%7BK%7D%20%5Csigma%5Cleft(%5Csum_%7Bj%20%5Cin%20%5Cmathcal%7BN%7D_%7Bi%7D%7D%20%5Calpha_%7Bi%20j%7D%5E%7Bk%7D%20%5Cmathbf%7BW%7D%5E%7Bk%7D%20%5Cvec%7Bh%7D_%7Bj%7D%5Cright)" alt="\vec{h}_{i}^{\prime}=\sigma\left(\sum_{j \in \mathcal{N}_{i}} \alpha_{i j} \mathbf{W} \vec{h}_{j}\right)\\
\vec{h}_{i}^{\prime}=\|_{k=1}^{K} \sigma\left(\sum_{j \in \mathcal{N}_{i}} \alpha_{i j}^{k} \mathbf{W}^{k} \vec{h}_{j}\right)" />

* This GAT model was applied for text classification problem, and it has given SOTA results or matched it.




