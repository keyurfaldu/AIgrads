## CopyBERT: A Unified Approach to Question Generation with Self-Attention
### Stalin Varanasi, Saadullah Amin, Gunter Neumann
### ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.nlp4convai-1.3.pdf)]

**Whats Unique**
This paper presents a copy mechnism, and how it can be effectively leveraged for the use case of question answering.

**How It Works**
* It finds a copy probability metrix for y_i th locaction over paragraph, answer and question generated till y-i-1th location.
    <img src="https://i.upmath.me/svg/p_%7Bc%7D%5Cleft(y_%7Bi%7D%20%5Cmid%20%5Ccdot%5Cright)%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Bll%7D%5Csum_%7Bk%3D1%3A%20y_%7Bi%7D%3Dt_%7Bk%7D%7D%5E%7BP%2Bi-1%7D%20p_%7Ba%7D%5Cleft(k%20%5Cmid%20y_%7Bi%7D%5Cright)%2C%20%26%20t_%7Bk%7D%20%5Cin%20Y%20%5C%5C%200%2C%20%26%20%5Ctext%20%7B%20else%20%7D%5Cend%7Barray%7D%5Cright." alt="p_{c}\left(y_{i} \mid \cdot\right)=\left\{\begin{array}{ll}\sum_{k=1: y_{i}=t_{k}}^{P+i-1} p_{a}\left(k \mid y_{i}\right), &amp; t_{k} \in Y \\ 0, &amp; \text { else }\end{array}\right." />

    * probability that y_i is t_k token, its n x n matrix, but its valid only for valid target token, i.e. paragraph tokens and tokens generated till i-1.

    * P_a matrix is n x n matrix and it is generated with few strategies:
        * Normal Copy: Just depending on hidden representations of last layer, with weight parameters

            <img src="https://i.upmath.me/svg/%24%5Cmathbf%7BP%7D_%7Ba%7D%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BH%7D%20%5Cmathbf%7BW%7D_%7Bn%7D%20%5Cmathbf%7BH%7D%5E%7BT%7D%5Cright)%20%5Cin%20%5Cmathbb%7BR%7D%5E%7Bn%20%5Ctimes%20n%7D" alt="$\mathbf{P}_{a}=\operatorname{softmax}\left(\mathbf{H} \mathbf{W}_{n} \mathbf{H}^{T}\right) \in \mathbb{R}^{n \times n}" />
            
            * W is hxh parameters matrix

        * Self-Copy: 
            * Cmompute weight of each attention head from hidden represenations of last layer, for each token. S is n x M matrix
            * For each token, get the weighted average of attention of that token with other tokens, consider that as the probabilities.

            <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cmathbf%7BS%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BH%7D%20%5Cmathbf%7BW%7D_%7Ba%7D%5Cright)%20%5Cin%20%5Cmathbb%7BR%7D%5E%7Bn%20%5Ctimes%20M%7D%20%5C%5C%20%5Cwidetilde%7B%5Cmathbf%7BP%7D%7D_%7Ba%7D%20%26%3D%5Cleft%5B%5Cmathcal%7BS%7D_%7B1%7D%20%5Cmathcal%7BA%7D_%7B1%7D%5E%7BT%7D%20%3B%20%5Cldots%20%3B%20%5Cmathcal%7BS%7D_%7Bn%7D%20%5Cmathcal%7BA%7D_%7Bn%7D%5E%7BT%7D%5Cright%5D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7Bn%20%5Ctimes%201%20%5Ctimes%20n%7D%20%5Cend%7Baligned%7D" alt="\begin{aligned} \mathbf{S} &amp;=\operatorname{softmax}\left(\mathbf{H} \mathbf{W}_{a}\right) \in \mathbb{R}^{n \times M} \\ \widetilde{\mathbf{P}}_{a} &amp;=\left[\mathcal{S}_{1} \mathcal{A}_{1}^{T} ; \ldots ; \mathcal{S}_{n} \mathcal{A}_{n}^{T}\right] \in \mathbb{R}^{n \times 1 \times n} \end{aligned}" />

            * P_a matrix can be achieved by dropping middle dimension.

        * Two-hop:
            * Get another matrix of P_a, with different sets of parameters. Take square of it to get 2-hop probability. And consider original P_a as 1-hop probability, and get final probability as follow:

            <img src="https://i.upmath.me/svg/%24%0A%5Cmathbf%7BP%7D_%7Ba%7D%5Cleft(q_%7Bi%7D%5Cright)%3Dh_%7Bi%7D%20%5Cmathbf%7BP%7D_%7B1-%5Ctext%20%7B%20hop%20%7D%7D%5Cleft(q_%7Bi%7D%5Cright)%2B%5Cleft(1-h_%7Bi%7D%5Cright)%20%5Cmathbf%7BP%7D_%7B2-%5Ctext%20%7B%20hop%20%7D%7D%5Cleft(q_%7Bi%7D%5Cright)%5C%5C%0A%5C%5Ch_%7Bi%7D%3D%5Csigma%5Cleft(%5Cmathbf%7Bh%7D_%7Bq_%7Bi%7D%7D%5E%7BT%7D%20%5Cmathbf%7BW%7D_%7B%5Cmathrm%7Bh%7D%7D%5Cright)%24%20and%20%24%5Cmathbf%7BW%7D_%7B%5Cmathrm%7Bh%7D%7D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7Bh%7D" alt="$
\mathbf{P}_{a}\left(q_{i}\right)=h_{i} \mathbf{P}_{1-\text { hop }}\left(q_{i}\right)+\left(1-h_{i}\right) \mathbf{P}_{2-\text { hop }}\left(q_{i}\right)\\
\\h_{i}=\sigma\left(\mathbf{h}_{q_{i}}^{T} \mathbf{W}_{\mathrm{h}}\right)$ and $\mathbf{W}_{\mathrm{h}} \in \mathbb{R}^{h}" />

            * weight to rely on 1-hop and 2-hop probability is again computed from hidden repr of the current token


* It find a generative probabiliy over vocaboarly by transforming its last layer hidden representation of previous token over vocabolary of size V

    <img src="https://i.upmath.me/svg/p_%7Bg%7D%5Cleft(q_%7Bi%7D%20%5Cmid%20%5Ccdot%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bq_%7Bi-1%7D%7D%5E%7BT%7D%20%5Cmathbf%7BV%7D%5Cright)" alt="p_{g}\left(q_{i} \mid \cdot\right)=\operatorname{softmax}\left(\mathbf{h}_{q_{i-1}}^{T} \mathbf{V}\right)" />

    * Where, V \in R ^ h x |V|
    * h_qi-1 \in R ^ h x 1

* It learns a flag to rely on copy or generated probability, by transforming of last layer hidden representation of previous token 
<img src="https://i.upmath.me/svg/p%5Cleft(q_%7Bi%7D%20%5Cmid%20.%5Cright)%3D%5Cleft(1-c_%7Bi%7D%5Cright)%20p_%7Bg%7D%5Cleft(q_%7Bi%7D%20%5Cmid%20.%5Cright)%2Bc_%7Bi%7D%20p_%7Bc%7D%5Cleft(q_%7Bi%7D%20%5Cmid%20.%5Cright)%5C%5C%0Ac_%7Bi%7D%3D%5Csigma%5Cleft(%5Cmathbf%7Bh%7D_%7Bq_%7Bi-1%7D%7D%5E%7BT%7D%20%5Cmathbf%7Bw%7D%5Cright)" alt="p\left(q_{i} \mid .\right)=\left(1-c_{i}\right) p_{g}\left(q_{i} \mid .\right)+c_{i} p_{c}\left(q_{i} \mid .\right)\\
c_{i}=\sigma\left(\mathbf{h}_{q_{i-1}}^{T} \mathbf{w}\right)" />
    * where w \in R ^ h x 1

**Results** 
* Results are as below, along with the ablation study.
    <p align="center">
        <img width=600 src="images/CopyBERT_QG.png">
        <em>Source: Author</em>
        </p>