## Dense Passage Retrieval for Open-Domain Question Answering
### Karpukhin, Vladimir, Barlas Oğuz, Sewon Min, Ledell Wu, Sergey Edunov, Danqi Chen, and Wen-tau Yih.
### [[arXiv](https://arxiv.org/pdf/2004.04906.pdf)]

**Whats Unique**
This paper presents that dense vector retrieval can effectively outperform sparse vector (i.e. BM25, TFIDF etc) retrival in open domain question answering, where in key techniques to train DPR are "in-batch negatives", and "top BM25 retrieved candidate". It also present QA on retrieved paragraph using span selection and paragraph selection approach, that outperforms current benchmarks.

**How It Works**
* Datasets considered: Following table captures what all datasets are considered.

<p align="center">
<img align="centre" src="images/DPR_datasets.png">
</p>

* Key Concepts in fine tuning retriver:
    * In Batch Negatives: For a batch of size B, each question i has a relevant passage i as the positive instance, and all other passages B-1 are as the negative instances.
    * One hard negative, i.e. top results from BM25 system can also be added.
    * BERT was fine tuned using the loss function to train DPR and CLS token was used as its embedding.
        <img src="https://i.upmath.me/svg/%5Coperatorname%7Bsim%7D(q%2C%20p)%3DE_%7BQ%7D(q)%5E%7B%5Ctop%7D%20E_%7BP%7D(p)" alt="\operatorname{sim}(q, p)=E_{Q}(q)^{\top} E_{P}(p)" />
    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%26%20L%5Cleft(q_%7Bi%7D%2C%20p_%7Bi%7D%5E%7B%2B%7D%2C%20p_%7Bi%2C%201%7D%5E%7B-%7D%2C%20%5Ccdots%2C%20p_%7Bi%2C%20n%7D%5E%7B-%7D%5Cright)%20%3D%26-%5Clog%20%5Cfrac%7Be%5E%7B%5Coperatorname%7Bsim%7D%5Cleft(q_%7Bi%7D%2C%20p_%7Bi%7D%5E%7B%2B%7D%5Cright)%7D%7D%7Be%5E%7B%5Coperatorname%7Bsim%7D%5Cleft(q_%7Bi%7D%2C%20p_%7Bi%7D%5E%7B%2B%7D%5Cright)%7D%2B%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20e%5E%7B%5Coperatorname%7Bsim%7D%5Cleft(q_%7Bi%7D%2C%20p_%7Bi%2C%20j%7D%5E%7B-%7D%5Cright)%7D%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
&amp; L\left(q_{i}, p_{i}^{+}, p_{i, 1}^{-}, \cdots, p_{i, n}^{-}\right) =&amp;-\log \frac{e^{\operatorname{sim}\left(q_{i}, p_{i}^{+}\right)}}{e^{\operatorname{sim}\left(q_{i}, p_{i}^{+}\right)}+\sum_{j=1}^{n} e^{\operatorname{sim}\left(q_{i}, p_{i, j}^{-}\right)}}
\end{aligned}" />
    * FAISS system was used to retrieve the passages using their embeddings.
   
* Results and Ablation Study
    * Retrieval systems result can be seen as below:
    <p align="center">
    <img align="centre" src="images/DPR_retrieval_results.png">
    </p>
    * Comparative study of different training schemes are as follow: As we can see, in-batch negatives, with one hard negative using BM25 gives the best result
    <p align="center">
    <img align="centre" src="images/DPR_training_schemes.png">
    </p>

* End-to-end Question Answering:
    * Probability of span, and probability of passage selection are computed as below:
    * P_i is i-th passage, where it has LxH size, where L is number of tokens and H is embedding dimensions
    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20P_%7B%5Ctext%20%7Bstart%20%7D%2C%20i%7D(s)%3D%26%20%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BP%7D_%7Bi%7D%20%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7Bstart%20%7D%7D%5Cright)_%7Bs%7D%20%5C%5C%20P_%7B%5Ctext%20%7Bend%20%7D%2C%20i%7D(t)%3D%26%20%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BP%7D_%7Bi%7D%20%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7Bend%20%7D%7D%5Cright)_%7Bt%7D%20%5C%5C%20P_%7B%5Ctext%20%7Bselected%20%7D%7D(i)%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Chat%7B%5Cmathbf%7BP%7D%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7Bselected%20%7D%7D%5Cright)_%7Bi%7D%2C%20%5C%5C%20%5Ctext%20%7B%20where%20%7D%20%5Chat%7B%5Cmathbf%7BP%7D%7D%3D%26%5Cleft%5B%5Cmathbf%7BP%7D_%7B1%7D%5E%7B%5B%5Cmathrm%7BCLS%7D%5D%7D%2C%20%5Cldots%2C%20%5Cmathbf%7BP%7D_%7Bk%7D%5E%7B%5B%5Cmathrm%7BCLS%7D%5D%7D%5Cright%5D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7Bh%20%5Ctimes%20k%7D%20%5Ctext%20%7B%20and%20%7D%20%5Cend%7Baligned%7D%5C%5C%0A%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7Bstart%20%7D%7D%2C%20%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7Bend%20%7D%7D%2C%20%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7Bselected%20%7D%7D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7Bh%7D%24%20are%20learnable%20vectors." alt="\begin{aligned} P_{\text {start }, i}(s)=&amp; \operatorname{softmax}\left(\mathbf{P}_{i} \mathbf{w}_{\text {start }}\right)_{s} \\ P_{\text {end }, i}(t)=&amp; \operatorname{softmax}\left(\mathbf{P}_{i} \mathbf{w}_{\text {end }}\right)_{t} \\ P_{\text {selected }}(i) &amp;=\operatorname{softmax}\left(\hat{\mathbf{P}}^{\top} \mathbf{w}_{\text {selected }}\right)_{i}, \\ \text { where } \hat{\mathbf{P}}=&amp;\left[\mathbf{P}_{1}^{[\mathrm{CLS}]}, \ldots, \mathbf{P}_{k}^{[\mathrm{CLS}]}\right] \in \mathbb{R}^{h \times k} \text { and } \end{aligned}\\
\mathbf{w}_{\text {start }}, \mathbf{w}_{\text {end }}, \mathbf{w}_{\text {selected }} \in \mathbb{R}^{h}$ are learnable vectors." />
    * End-to-end QA has also outperformed other systems, and gives accuracy of about 40-50% on different datasets.

