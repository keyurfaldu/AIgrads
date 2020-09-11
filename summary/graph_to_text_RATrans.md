## Structural Information Preserving for Graph-to-Text Generation
### Linfeng Song et al., 
### ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.712.pdf)]

**Whats New**
This paper proposes two kinds of autoencoder losses for local and linear structure of the graph for the problem of graph to text generation.

**Background**
* Many text generation processes takes graph as an input
* Abstract Meaning Representation (AMR) text generation is one such problem.
* Following figure explains the problem statement
    <p align="center">
    <img width=600 src="images/graph_to_text_problem.png">
    <em>Source: Author</em>
    </p>
* Graph and expected statement to be generated in the figure above.

**Base: Structure Aware Transformer**
* structure aware encoder:
    <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Bh%7D_%7Bi%7D%5E%7Bl%7D%3D%5Csum_%7Bj%20%5Cin%5B1%20.%20.%20N%5D%7D%20%5Calpha_%7Bi%20j%7D%5Cleft(%5Cboldsymbol%7Bh%7D_%7Bj%7D%5E%7Bl-1%7D%20%5Cboldsymbol%7BW%7D%5E%7BP%7D%2B%5Cboldsymbol%7B%5Cgamma%7D_%7Bi%20j%7D%20%5Cboldsymbol%7BW%7D%5E%7BR_%7B1%7D%7D%5Cright)" alt="\boldsymbol{h}_{i}^{l}=\sum_{j \in[1 . . N]} \alpha_{i j}\left(\boldsymbol{h}_{j}^{l-1} \boldsymbol{W}^{P}+\boldsymbol{\gamma}_{i j} \boldsymbol{W}^{R_{1}}\right)" />
    * hidden state where its attention weighed sum of hidden states of previous layer and also the vector represenation of relations lambda_i_j between node vi and vj
    * Attention weights are computed using query and key. 
        * Query: based on hidden state of previous layer
        * Key: based on hidden state of previous layer and vector represenation of relations.

    * Relation aware self attention:
    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Calpha_%7Bi%20j%7D%20%26%3D%5Cfrac%7B%5Cexp%20%5Cleft(e_%7Bi%20j%7D%5Cright)%7D%7B%5Csum_%7Bk%20%5Cin%5B1%20.%20.%20N%5D%7D%20%5Cexp%20%5Cleft(e_%7Bi%20k%7D%5Cright)%7D%20%5C%5C%20e_%7Bi%20j%7D%20%26%3D%5Cfrac%7B%5Cleft(%5Cboldsymbol%7Bh%7D_%7Bi%7D%5E%7Bl-1%7D%20%5Cboldsymbol%7BW%7D%5E%7BQ%7D%5Cright)%5Cleft(%5Cboldsymbol%7Bh%7D_%7Bj%7D%5E%7Bl-1%7D%20%5Cboldsymbol%7BW%7D%5E%7BK%7D%2B%5Cboldsymbol%7B%5Cgamma%7D_%7Bi%20j%7D%20%5Cboldsymbol%7BW%7D%5E%7BR_%7B2%7D%7D%5Cright)%5E%7B%5Ctop%7D%7D%7B%5Csqrt%7Bd_%7Bh%7D%7D%7D%20%5Cend%7Baligned%7D" alt="\begin{aligned} \alpha_{i j} &amp;=\frac{\exp \left(e_{i j}\right)}{\sum_{k \in[1 . . N]} \exp \left(e_{i k}\right)} \\ e_{i j} &amp;=\frac{\left(\boldsymbol{h}_{i}^{l-1} \boldsymbol{W}^{Q}\right)\left(\boldsymbol{h}_{j}^{l-1} \boldsymbol{W}^{K}+\boldsymbol{\gamma}_{i j} \boldsymbol{W}^{R_{2}}\right)^{\top}}{\sqrt{d_{h}}} \end{aligned}" />

* Standard decoder:
    * Given hidden state of s i-1, and previously generated vector y_i-1, it generates y i, and s i

        <img src="https://i.upmath.me/svg/y_%7Bi%7D%2C%20%5Cboldsymbol%7Bs%7D_%7Bi%7D%3D%5Coperatorname%7BSADecoder%7D%5Cleft(%5Cleft%5B%5Cboldsymbol%7BH%7D%5E%7BL%7D%20%3B%20%5Cboldsymbol%7Bs%7D_%7B1%7D%20%5Cldots%20%5Cboldsymbol%7Bs%7D_%7Bi-1%7D%5Cright%5D%2C%20y_%7Bi-1%7D%5Cright)" alt="y_{i}, \boldsymbol{s}_{i}=\operatorname{SADecoder}\left(\left[\boldsymbol{H}^{L} ; \boldsymbol{s}_{1} \ldots \boldsymbol{s}_{i-1}\right], y_{i-1}\right)" />

* Standard langauge modelling loss

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20l_%7B%5Ctext%20%7Bbase%7D%7D%20%26%3D-%5Csum_%7Bi%20%5Cin%5B1%20.%20.%20N%5D%7D%20%5Clog%20p%5Cleft(y_%7Bi%7D%20%5Cmid%20y_%7B1%7D%2C%20%5Cldots%2C%20y_%7Bi-1%7D%20%3B%20%5Cboldsymbol%7BG%7D%5Cright)%20%5C%5C%20%26%3D-%5Csum_%7Bi%20%5Cin%5B1%20.%20.%20N%5D%7D%20p%5Cleft(y_%7Bi%7D%20%5Cmid%20%5Cboldsymbol%7Bs%7D_%7Bi%7D%20%3B%20%5Cboldsymbol%7B%5Ctheta%7D%5Cright)%20%5Cend%7Baligned%7D" alt="\begin{aligned} l_{\text {base}} &amp;=-\sum_{i \in[1 . . N]} \log p\left(y_{i} \mid y_{1}, \ldots, y_{i-1} ; \boldsymbol{G}\right) \\ &amp;=-\sum_{i \in[1 . . N]} p\left(y_{i} \mid \boldsymbol{s}_{i} ; \boldsymbol{\theta}\right) \end{aligned}" />

* Multi view auto-encoding losses:
    <p align="center">
    <img width=600 src="images/graph_to_text_auto_encoding_losses.png">
    <em>Source: Author</em>
    </p>

    * Loss 1: Reconstructing two loss relations
        <img src="https://i.upmath.me/svg/p%5Cleft(y_%7Bj%7D%2C%20l%20%5Cmid%20y_%7Bi%7D%5Cright)%3Dp%5Cleft(l%20%5Cmid%20y_%7Bj%7D%2C%20y_%7Bi%7D%5Cright)%20%5Ccdot%20p%5Cleft(y_%7Bj%7D%20%5Cmid%20y_%7Bi%7D%5Cright)%24%0A%24%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cphi_%7Bi%2C%20j%7D%5E%7B%5Ctext%20%7Blabel%20%7D%7D%5Cright)_%7B%5Bl%5D%7D%20%5Ccdot%20%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cphi_%7Bi%7D%5E%7B%5Ctext%20%7Barc%20%7D%7D%5Cright)_%7B%5Bj%5D%7D" alt="p\left(y_{j}, l \mid y_{i}\right)=p\left(l \mid y_{j}, y_{i}\right) \cdot p\left(y_{j} \mid y_{i}\right)$
$=\operatorname{softmax}\left(\phi_{i, j}^{\text {label }}\right)_{[l]} \cdot \operatorname{softmax}\left(\phi_{i}^{\text {arc }}\right)_{[j]}" />
        * Computes probability of an arch between i and j, and then the label between i and j.

    * Loss 2: Linear graph sequence generation

        <img src="https://i.upmath.me/svg/l_%7B%5Ctext%20%7Bauto%7D%202%7D%3D-%5Csum_%7Bi%20%5Cin%5B1%20.%20.%20M%5D%7D%20%5Clog%20p%5Cleft(x_%7Bi%7D%20%5Cmid%20%5Cboldsymbol%7Bt%7D_%7Bi%7D%20%3B%20%5Cboldsymbol%7B%5Ctheta%7D%5Cright)" alt="l_{\text {auto} 2}=-\sum_{i \in[1 . . M]} \log p\left(x_{i} \mid \boldsymbol{t}_{i} ; \boldsymbol{\theta}\right)" />

        * sequence x_i can be token, bracket or relation. As shwon in the figure with dotted box view 2.

* Final training loss is weighted average of all the three losses

    <img src="https://i.upmath.me/svg/l_%7B%5Ctext%20%7Bfinal%7D%7D%3Dl_%7B%5Ctext%20%7Bbase%7D%7D%2B%5Calpha%20l_%7B%5Ctext%20%7Bauto%7D%201%7D%2B%5Cbeta%20l_%7B%5Ctext%20%7Bauto%7D%202%7D" alt="l_{\text {final}}=l_{\text {base}}+\alpha l_{\text {auto} 1}+\beta l_{\text {auto} 2}" />

* Impact of these additional two losses can be seen in the following figure, where x axis are the weights

    <p align="center">
    <img width=600 src="images/graph_to_text_impact_of_AEloss.png">
    <em>Source: Author</em>
    </p>

* Examples of input graph, reference and output can be seen as below:
    <p align="center">
    <img width=600 src="images/graph_to_text_examples.png">
    <em>Source: Author</em>
    </p>









    
