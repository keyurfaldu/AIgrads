## Neural Models for Key Phrase Extraction and Question Generation
### Sandeep Subramanian, Yoshuwa Benjio 
### Machine Reading for Question Answering workshop at ACL 2018 [[arXiv](https://arxiv.org/pdf/1706.04560.pdf)]


**Whats New**
This paper leverage SQUAD data to extract key-phrases for answers, and generate question based on that using generative decoder with pointer copy mechanism.

**How It Works**

Pointer Network for Key Phrase Extraction
* Pointer network is an extension of sequence to sequence models where the target sequence consists of poistions in the source sequence.

    <img src="https://i.upmath.me/svg/P%5Cleft(w_%7Bi%7D%5E%7Bd%7D%20%5Cmid%20%5Cboldsymbol%7Bh%7D_%7B1%7D%5E%7Bp%7D%20%5Cldots%20%5Cboldsymbol%7Bh%7D_%7Bj%7D%5E%7Bp%7D%2C%20%5Cboldsymbol%7Bh%7D_%7B.%7D%5E%7Bd%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(W_%7B1%7D%20%5Cboldsymbol%7Bh%7D_%7Bj%7D%5E%7Bp%7D%20%5Ccdot%20%5Cboldsymbol%7Bh%7D%5E%7Bd%7D%5Cright)" alt="P\left(w_{i}^{d} \mid \boldsymbol{h}_{1}^{p} \ldots \boldsymbol{h}_{j}^{p}, \boldsymbol{h}_{.}^{d}\right)=\operatorname{softmax}\left(W_{1} \boldsymbol{h}_{j}^{p} \cdot \boldsymbol{h}^{d}\right)" />

* Where, h_d is the encoder state of document, and h_p are the decoder state for phrase generated, and w^d_i is parameterised for start or end. 

Question Generation:
* Decoder either copy from encoder, or it generates
    <img src="https://i.upmath.me/svg/P%5Cleft(%5Chat%7Bw%7D_%7Bt%7D%5Cright)%20%5Csim%20s%5E%7B(t)%7D%20%5Cboldsymbol%7B%5Calpha%7D%5E%7B(t)%7D%2B%5Cleft(1-s%5E%7B(t)%7D%5Cright)%20%5Cboldsymbol%7Bo%7D%5E%7B(t)%7D" alt="P\left(\hat{w}_{t}\right) \sim s^{(t)} \boldsymbol{\alpha}^{(t)}+\left(1-s^{(t)}\right) \boldsymbol{o}^{(t)}" />

    <img src="https://i.upmath.me/svg/s%5E%7B(t)%7D%3Dh%5Cleft(%5Cboldsymbol%7Bs%7D_%7B2%7D%5E%7B(t)%7D%2C%20%5Cboldsymbol%7Bv%7D%5E%7B(t)%7D%2C%20%5Cboldsymbol%7B%5Calpha%7D%5E%7B(t)%7D%2C%20%5Cboldsymbol%7Bo%7D%5E%7B(t)%7D%5Cright)" alt="s^{(t)}=h\left(\boldsymbol{s}_{2}^{(t)}, \boldsymbol{v}^{(t)}, \boldsymbol{\alpha}^{(t)}, \boldsymbol{o}^{(t)}\right)" />

* Where, o(t) is generative decodeder, and alpha_t is attention pointer 

* Pointing decoder has two cascading LSTM cells, c1, and c2
    <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Bs%7D_%7B1%7D%5E%7B(t)%7D%3Dc_%7B1%7D%5Cleft(%5Cboldsymbol%7By%7D%5E%7B(t-1)%7D%2C%20%5Cboldsymbol%7Bs%7D_%7B2%7D%5E%7B(t-1)%7D%5Cright)%5C%5C%0A%24%5Cboldsymbol%7Bs%7D_%7B2%7D%5E%7B(t)%7D%3Dc_%7B2%7D%5Cleft(%5Cboldsymbol%7Bv%7D%5E%7B(t)%7D%2C%20%5Cboldsymbol%7Bs%7D_%7B1%7D%5E%7B(t)%7D%5Cright)" alt="\boldsymbol{s}_{1}^{(t)}=c_{1}\left(\boldsymbol{y}^{(t-1)}, \boldsymbol{s}_{2}^{(t-1)}\right)\\ \boldsymbol{s}_{2}^{(t)}=c_{2}\left(\boldsymbol{v}^{(t)}, \boldsymbol{s}_{1}^{(t)}\right)" />

* v(t) is attention weighted encoder state over document, and y(t-1) is the last generated output

    <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Bv%7D%5E%7B(t)%7D%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bi%7D%5E%7B(t)%7D%20%5Cboldsymbol%7Bh%7D_%7Bi%7D%5E%7Bd%7D" alt="\boldsymbol{v}^{(t)}=\sum_{i=1}^{n} \alpha_{i}^{(t)} \boldsymbol{h}_{i}^{d}" />

* Where, attention is computed as function of decoder LSTM cell, document and answer encoding.

    <img src="https://i.upmath.me/svg/%5Calpha_%7Bi%7D%5E%7B(t)%7D%3Df%5Cleft(%5Cboldsymbol%7Bh%7D_%7Bi%7D%5E%7Bd%7D%2C%20%5Cboldsymbol%7Bh%7D%5E%7Ba%7D%2C%20%5Cboldsymbol%7Bs%7D_%7B1%7D%5E%7B(t-1)%7D%5Cright)" alt="\alpha_{i}^{(t)}=f\left(\boldsymbol{h}_{i}^{d}, \boldsymbol{h}^{a}, \boldsymbol{s}_{1}^{(t-1)}\right)" />

Quantitative Evaluation of Key Phrase Extraction
* Multi-Span F1
    * p_i is computed as the token wise f1 score of predicted phrase i, and any gold phrase j.
    * r_j is computed as the token wise f1 score of any predicted phrase i, with a fixed gold phrase j.
    * Precision = average(p_i)
    * Recall = average(r_j)

Quantitative Evaluation of QA Pairs
* BLUE score
* Pre-trained QA model
    * For document d and answer a => q_hat is generated question (and q was a gold question)
    * If pre-trained QA model is able to answer a given (d, q), and answer a_hat given (d, q_hat)
    * n-gram overlab between a, and a_hat is considered the overlap between q and q_hat for the computation of BLUE score.
* Human evaluation was also done.

