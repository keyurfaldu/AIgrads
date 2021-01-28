## ISAAQ--Mastering Textbook Questions with Pre-trained Transformers and Bottom-Up and Top-Down Attention.
### Gomez-Perez, Jose Manuel, and Raul Ortega. 
### [[arXiv:2010.00562](https://arxiv.org/pdf/2010.00562.pdf)] (2020).

**Whats Unique**
This paper presents the use of top-down and bottom-up attention by concatanating diagram and text representations in an ensemble setup to answer text book questions. 

TQA dataset consists of 1076 lessons, 78K sentences, 3.4K diagrams and 5400 boolq, 8293 text MC, and 12567 diagram MC Questions

It achieves SOTA results with accuracies of 81.36%, 71.11%, and 55.12% for boolq, text MC, and diagram MC questions.

**Approach**
Following figure illustrate the approach laid in the paper.

<p align="center">
    <img width=600 src="images/ISAAQ_architecture.png">
    <em>Source: Author</em>
    </p>

As shown in the figure, there are three different retrievals are used to get the back ground knowledge to answer a question.

<img src="https://i.upmath.me/svg/%5Coperatorname%7Bseq%7D%5Cleft(K%2C%20Q%20A_%7Bi%7D%5Cright)%3D%5BC%20L%20S%5D%20K%5BS%20E%20P%5D%20Q%20A_%7Bi%7D%5BS%20E%20P%5D%5C%5C%0A%5Coperatorname%7Bseq%7D(q%2C%20l%20s)%3D%5BC%20L%20S%5D%20q%5BS%20E%20P%5D%20l%20s%5BS%20E%20P%5D" alt="\operatorname{seq}\left(K, Q A_{i}\right)=[C L S] K[S E P] Q A_{i}[S E P]\\
\operatorname{seq}(q, l s)=[C L S] q[S E P] l s[S E P]" />


Using YOLO, regions and positions are derived, and they are intermixed using learnable transformations. Afterwhich, its top down attention is computed using the CLS representations of questions, answer option and background knowledge sequence. Attention weighted representations of diagram is computed.

<img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Chat%7Bf%7D_%7Bj%7D%20%26%3D%5Ctext%20%7B%20LayerNorm%20%7D%5Cleft(W_%7BF%7D%2C%20f_%7Bj%7D%2Bb_%7Bf%7D%5Cright)%20%5C%5C%0A%5Chat%7Bp%7D_%7Bj%7D%20%26%3D%5Ctext%20%7B%20Layer%20%7D%20%5Coperatorname%7BNorm%7D%5Cleft(W_%7BP%7D%2C%20p_%7Bj%7D%2Bb_%7BP%7D%5Cright)%20%5C%5C%0Av_%7Bj%7D%20%26%3D%5Cleft(%5Chat%7Bf%7D_%7Bj%7D%2B%5Chat%7Bp%7D_%7Bj%7D%5Cright)%20%2F%202%5C%5C%0Aa_%7Bi%20j%7D%26%3Dw_%7Ba%7D%5E%7BT%7D%20g_%7Ba%7D%5Cleft(%5Cleft%5Bv_%7Bj%7D%2C%20C_%7Bi%7D%5Cright%5D%5Cright)%5C%5C%0A%5Calpha_%7Bi%20j%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(a_%7Bi%20j%7D%5Cright)%20%5C%5C%0A%5Chat%7Bv%7D_%7Bi%7D%20%26%3D%5Csum_%7Bj%3D1%7D%5E%7Bm%7D%20%5Calpha_%7Bi%20j%7D%20v_%7Bj%7D%20%5C%5C%0A%5Chat%7By%7D%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(U%20W_%7Bu%7D%5Cright)%2C%5Ctext%7Bwhere%20%7D%20u_%7Bi%7D%3DC_%7Bi%7D%20%5Ccirc%20%5Chat%7Bv%7D_%7Bi%7D%20%5C%5C%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\hat{f}_{j} &amp;=\text { LayerNorm }\left(W_{F}, f_{j}+b_{f}\right) \\
\hat{p}_{j} &amp;=\text { Layer } \operatorname{Norm}\left(W_{P}, p_{j}+b_{P}\right) \\
v_{j} &amp;=\left(\hat{f}_{j}+\hat{p}_{j}\right) / 2\\
a_{i j}&amp;=w_{a}^{T} g_{a}\left(\left[v_{j}, C_{i}\right]\right)\\
\alpha_{i j} &amp;=\operatorname{softmax}\left(a_{i j}\right) \\
\hat{v}_{i} &amp;=\sum_{j=1}^{m} \alpha_{i j} v_{j} \\
\hat{y}&amp;=\operatorname{softmax}\left(U W_{u}\right),\text{where } u_{i}=C_{i} \circ \hat{v}_{i} \\
\end{aligned}" />


Textual sequence representation, and attention weighed diagram representations are concatenated, and prediction is made using softmax layer. 

Following figure illustrate the complete approach.


<p align="center">
    <img width=600 src="images/ISAAQ_system.png">
    <em>Source: Author</em>
    </p>
    