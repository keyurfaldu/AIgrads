## Syntax-guided Controlled Generation of Paraphrases
### Ashutosh Kumar, Kabir Ahuja, Raghuram Vadapalli, Partha Talukdar, 
### ACL 2020 [[arXiv](https://arxiv.org/pdf/2005.08417.pdf)]


**Whats New** This paper invent a technique to paraphrase an input sentence in a controlled manned with guided syntax. 

**Major Contribution**
* An end-to-end model to generate syntactically controlled paraphrases at different level of granularity using a syntax parsed exemplar.
* New mechanism to incorporate syntactic information from exemplar sentence's syntactic parse. 
* Dataset formed from Quora Question Pairs for evaluating models. And, set of extensive experiments to prove validity.

**How It Works**
* SGCP has following major modules:
    * Inputs
        * Input sentence X
        * Syntactic Exemplar Y (with leaf node removed)
    * **Semantic Encoder**
        * <img src="https://i.upmath.me/svg/h_%7Bt%7D%5E%7BX%7D%3D%5Coperatorname%7BGRU%7D%5Cleft(h_%7Bt-1%7D%5E%7BX%7D%2C%20e%5Cleft(x_%7Bt%7D%5Cright)%5Cright)" alt="h_{t}^{X}=\operatorname{GRU}\left(h_{t-1}^{X}, e\left(x_{t}\right)\right)" />
        * e(x_t) is embedding of x_t
    * **Syntactic Endoder**
        * Let constituency tree,  <img src="https://i.upmath.me/svg/%5Cmathcal%7BC%7D%5E%7BY%7D%3D%5C%7B%5Cmathcal%7BV%7D%2C%20%5Cmathcal%7BE%7D%2C%20%5Cmathcal%7BY%7D%5C%7D" alt="\mathcal{C}^{Y}=\{\mathcal{V}, \mathcal{E}, \mathcal{Y}\}" />
        * V is set of nodes, E is set of edges, and Y the labels associated with each node.
        * Using technique similar to TreeLSTM, 
        <img src="https://i.upmath.me/svg/h_%7Bv%7D%5E%7BY%7D%3D%5Coperatorname%7BGeLU%7D%5Cleft(W_%7Bp%20a%7D%20h_%7Bp%20a(v)%7D%5E%7BY%7D%2BW_%7Bv%7D%20e%5Cleft(y_%7Bv%7D%5Cright)%2Bb_%7Bv%7D%5Cright)" alt="h_{v}^{Y}=\operatorname{GeLU}\left(W_{p a} h_{p a(v)}^{Y}+W_{v} e\left(y_{v}\right)+b_{v}\right)" />
        * Syntatic tree is randomly pruned at height from {3,.., H_max}
        * Queue of terminal nodes of syntactic tree is maintained. L_H^Y
            <img src="https://i.upmath.me/svg/%5Cmathbb%7BL%7D_%7BH%7D%5E%7BY%7D%3D%5Cleft%5Bh_%7B%5Cmathrm%7BWP%7D%7D%5E%7BY%7D%2C%20h_%7B%5Cmathrm%7BVBZ%7D%7D%5E%7BY%7D%2C%20h_%7B%5Cmathrm%7BNP%7D%7D%5E%7BY%7D%2C%20h_%7B%3C%5Cmathrm%7BDOT%7D%3E%7D%5E%7BY%7D%5Cright%5D" alt="\mathbb{L}_{H}^{Y}=\left[h_{\mathrm{WP}}^{Y}, h_{\mathrm{VBZ}}^{Y}, h_{\mathrm{NP}}^{Y}, h_{&lt;\mathrm{DOT}&gt;}^{Y}\right]" />


    * **Syntactic Paraphrase Decoder**
        * <img src="https://i.upmath.me/svg/Z%5E%7B*%7D%3D%5Cunderset%7Bz%7D%7B%5Coperatorname%7Bargmax%7D%7D%20%5Cprod_%7Bt%3D1%7D%5E%7BT_%7BZ%7D%7D%5Cleft(z_%7Bt%7D%20%5Cmid%20z_%7B1%7D%2C%20%5Cldots%2C%20z_%7Bt-1%7D%2C%20X%2C%20Y%5Cright)" alt="Z^{*}=\underset{z}{\operatorname{argmax}} \prod_{t=1}^{T_{Z}}\left(z_{t} \mid z_{1}, \ldots, z_{t-1}, X, Y\right)" />
        * X is input sentence, and Y is exemplar sentence

            
            
    * **Using Semantic Information**

        <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bc%7D%0Ae_%7Bi%7D%5E%7Bt%7D%3Dv%5E%7B%5Ctop%7D%20%5Ctanh%20%5Cleft(W_%7Bh%7D%20h_%7Bi%7D%5E%7BX%7D%2BW_%7Bs%7D%20s_%7Bt%7D%2Bb_%7B%5Ctext%20%7Battn%20%7D%7D%5Cright)%20%5C%5C%0A%5Calpha%5E%7Bt%7D%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(e%5E%7Bt%7D%5Cright)%5C%5C%0Ac_%7Bt%7D%3D%5Csum_%7Bi%7D%20%5Calpha_%7Bi%7D%5E%7Bt%7D%20h_%7Bi%7D%5E%7BX%7D%0A%5Cend%7Barray%7D" alt="\begin{array}{c}
e_{i}^{t}=v^{\top} \tanh \left(W_{h} h_{i}^{X}+W_{s} s_{t}+b_{\text {attn }}\right) \\
\alpha^{t}=\operatorname{softmax}\left(e^{t}\right)\\
c_{t}=\sum_{i} \alpha_{i}^{t} h_{i}^{X}
\end{array}" />

    * **Using Syntactic Information**

        <img src="https://i.upmath.me/svg/%0A%5Cmathbb%7BP%7D_%7B%5Ctext%20%7Bvocab%20%7D%7D%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(W%5Cleft(%5Cleft%5Bc_%7Bt%7D%20%3B%20h_%7Bt%7D%5E%7BY%7D%20%3B%20s_%7Bt%7D%20%3B%20e%5Cleft(z_%7Bt%7D%5E%7B%5Cprime%7D%5Cright)%5Cright%5D%5Cright)%2Bb%5Cright)%5C%5C%0A%5Cmathbb%7BP%7D(z)%20%26%3Dp_%7B%5Ctext%20%7Bgen%20%7D%7D%20%5Cmathbb%7BP%7D_%7B%5Ctext%20%7Bvocab%20%7D%7D(z)%2B%5Cleft(1-p_%7B%5Ctext%20%7Bgen%20%7D%7D%5Cright)%20%5Csum_%7Bi%3A%20z_%7Bi%7D%3Dz%7D%20%5Calpha_%7Bi%7D%5E%7Bt%7D%20%5C%5C%0Ap_%7B%5Ctext%20%7Bgen%20%7D%7D%20%26%3D%5Csigma%5Cleft(w_%7Bc%7D%5E%7B%5Ctop%7D%20c_%7Bt%7D%2Bw_%7Bs%7D%5E%7B%5Ctop%7D%20s_%7Bt%7D%2Bw_%7Bx%7D%5E%7B%5Ctop%7D%20e%5Cleft(z_%7Bt%7D%5E%7B%5Cprime%7D%5Cright)%2Bb_%7Bg%20e%20n%7D%5Cright)%0A" alt="
\mathbb{P}_{\text {vocab }}=\operatorname{softmax}\left(W\left(\left[c_{t} ; h_{t}^{Y} ; s_{t} ; e\left(z_{t}^{\prime}\right)\right]\right)+b\right)\\
\mathbb{P}(z) &amp;=p_{\text {gen }} \mathbb{P}_{\text {vocab }}(z)+\left(1-p_{\text {gen }}\right) \sum_{i: z_{i}=z} \alpha_{i}^{t} \\
p_{\text {gen }} &amp;=\sigma\left(w_{c}^{\top} c_{t}+w_{s}^{\top} s_{t}+w_{x}^{\top} e\left(z_{t}^{\prime}\right)+b_{g e n}\right)
" />

    * **Objective Function**

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cmathcal%7BL%7D%3D%26-%5Cfrac%7B1%7D%7BT%7D%20%5Csum_%7Bt%3D0%7D%5E%7BT%7D%5Cleft%5B%5Clog%20%5Cmathbb%7BP%7D%5Cleft(z_%7Bt%7D%5E%7B*%7D%5Cright)%5Cright.%5C%5C%0A%26%2Ba_%7Bt%7D%20%5Clog%20%5Cleft(p_%7Bt%7D%5Cright)%20%5C%5C%0A%26%5Cleft.%2B%5Cleft(1-a_%7Bt%7D%5Cright)%20%5Clog%20%5Cleft(1-p_%7Bt%7D%5Cright)%5Cright%5D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\mathcal{L}=&amp;-\frac{1}{T} \sum_{t=0}^{T}\left[\log \mathbb{P}\left(z_{t}^{*}\right)\right.\\
&amp;+a_{t} \log \left(p_{t}\right) \\
&amp;\left.+\left(1-a_{t}\right) \log \left(1-p_{t}\right)\right]
\end{aligned}" />

    * Following figure illustrate it really well. 
        <p align="center">
        <img width=600 src="images/SGCP_architecture.png">
        <em>Source: Author</em>
        </p>

* Results
    * SGCP is well evaluated on two different aspects, paraphrase should retain the meaning, and it should also have syntactic structure.
        <p align="center">
        <img width=600 src="images/SGCP_results.png">
        <em>Source: Author</em>
        </p>
    * BLUE, METEOR, ROUGE-1, ROUGE-2, ROUGE-3 - are evaluaion to measure semantic correctness.
    * Tree-edit distance is used to measure syntatic distance.
    * PDS - is Phraphrase detection score, is the performance of quora paraphrase classifiers. 
    * SGCP examples for different exemplars can be found as below.
        <p align="center">
        <img width=600 src="images/SGCP_examples.png">
        <em>Source: Author</em>
        </p>







