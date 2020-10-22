## Taming Pretrained Transformers for Extreme Multi-label Text Classification
### Wei-Cheng Chang, Hsiang-Fu Yu, Kai Zhong, Yiming Yang, Inderjit S. Dhillon, 2020
### [[arXiv](https://assets.amazon.science/32/d7/bb602e97419ead030dde419b9191/taming-pretrained-transformers-for-extreme-multi-label-text-classification.pdf)]

**Whats Unique**
This paper presents a technique for extreme multi label classification using transformers. It first clusters the labels, then cluster classification using transformer, and ranking using one-vs-all binary classifers.

**How does it work**

<p align="center">
    <img width=600 src="images/XMC_XTransformer_architecture.png">
    <em>Source: Author</em>
    </p>

* It learns a score function between an instance x, and label l as follow:

    <img src="https://i.upmath.me/svg/f(%5Cmathbf%7Bx%7D%2C%20l)%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Bll%7D%0A%5Csigma%5Cleft(g%5Cleft(%5Cmathbf%7Bx%7D%2C%20c_%7Bl%7D%5Cright)%2C%20h(%5Cmathbf%7Bx%7D%2C%20l)%5Cright)%2C%20%26%20%5Ctext%20%7B%20if%20%7D%20c_%7Bl%7D%20%5Cin%20g_%7Bb%7D(%5Cmathbf%7Bx%7D)%20%5C%5C%0A-%5Cinfty%2C%20%26%20%5Ctext%20%7B%20otherwise%20%7D%0A%5Cend%7Barray%7D%5Cright" alt="f(\mathbf{x}, l)=\left\{\begin{array}{ll}
\sigma\left(g\left(\mathbf{x}, c_{l}\right), h(\mathbf{x}, l)\right), &amp; \text { if } c_{l} \in g_{b}(\mathbf{x}) \\
-\infty, &amp; \text { otherwise }
\end{array}\right" />

    * g(x, c_l) is transformer fine tuned to map instance x to a cluster l [Nerual Matcher]
    * h(x, l) is one vs all classifier trained for positive instances x and l, and negative instances of x in cluster where l belongs. [Ranking]

**Semantic Label Indexing**
* label representation is derived either from a label or the instances belonging to the label.
*  They are clustered using hierarchical classification of tree with K leaf nodes.

**Deep Transformer as Neural Matcher**
* Square hinge loss is used to train nerual matcher. 

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cmin%20_%7B%5Cmathbf%7BW%7D%2C%20%5Ctheta%7D%20%26%20%5Cfrac%7B1%7D%7BN%20K%7D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%5Csum_%7Bk%3D1%7D%5E%7BK%7D%20%5Cmax%20%5Cleft(0%2C1-%5Ctilde%7BM%7D_%7Bi%20k%7D%20g(%5Cmathbf%7Bx%7D%2C%20k%20%3B%20%5Cmathbf%7BW%7D%2C%20%5Ctheta)%5Cright)%5E%7B2%7D%20%5C%5C%0A%5Ctext%20%7B%20s.t.%20%7D%20%26%20g(%5Cmathbf%7Bx%7D%2C%20k%20%3B%20%5Cmathbf%7BW%7D%2C%20%5Ctheta)%3D%5Cmathbf%7Bw%7D_%7Bk%7D%5E%7BT%7D%20%5Cphi_%7B%5Ctext%20%7Btransformer%20%7D%7D(%5Cmathbf%7Bx%7D)%5C%5C%0A%5Ctext%20%7B%20where%20%7D%20%5Ctilde%7B%5Cmathbf%7BM%7D%7D_%7Bi%20k%7D%26%3D2%20%5Cmathbf%7BM%7D_%7Bi%20k%7D-1%20%5Cin%5C%7B-1%2C1%5C%7D%2C%20%5Cmathbf%7BW%7D%3D%5Cleft%5B%5Cmathbf%7Bw%7D_%7B1%7D%2C%20%5Cldots%2C%20%5Cmathbf%7Bw%7D_%7BK%7D%5Cright%5D%5E%7BT%7D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7BK%20%5Ctimes%20d%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\min _{\mathbf{W}, \theta} &amp; \frac{1}{N K} \sum_{i=1}^{N} \sum_{k=1}^{K} \max \left(0,1-\tilde{M}_{i k} g(\mathbf{x}, k ; \mathbf{W}, \theta)\right)^{2} \\
\text { s.t. } &amp; g(\mathbf{x}, k ; \mathbf{W}, \theta)=\mathbf{w}_{k}^{T} \phi_{\text {transformer }}(\mathbf{x})\\
\text { where } \tilde{\mathbf{M}}_{i k}&amp;=2 \mathbf{M}_{i k}-1 \in\{-1,1\}, \mathbf{W}=\left[\mathbf{w}_{1}, \ldots, \mathbf{w}_{K}\right]^{T} \in \mathbb{R}^{K \times d}
\end{aligned}" />

**Ranking**
* Teacher Forcing Negatives (TFN): only those instances which belong to same cluster.
* Matcher aware negatives:  instances from top-b predicted clusters.
* OVA (one-vs-all) classifer with binary loss is used.

**Results**
* It produces state of the art results.