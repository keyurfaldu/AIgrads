## Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks
### Piktus et al, Facebook AI Research, NYU
### NIPS 2020 [[arXiv](https://arxiv.org/pdf/2005.11401.pdf)]


**Whats Unique**
This paper proposes and validate that pre-trained models with a differentiable access mechanism to explicit nonparametric memory can perform better on knwoledge intensive tasks with a general purpose fine tuning recipe (RAG). 

**Whats RAG**
RAG: Retrieval Augmented Generation is a general purpose fine tuning recipe to combine pre-trained parametric and non-parametric memory for language generation. 

**How It Works**
Architecture diagram for RAG is shown below.

<p align="center">
    <img width=600 src="images/RAG_architecture.png">
    <em>Source: Author</em>
    </p>

RAG model use the input sequence x to retrieve text passages z and use these passages as additional context when generating the target sequence y.

It has following main components:
* Retriever:
    * Given a query x, it retrieve top-K passages z.
* Generator:
    * Given a query x, passages z, it generates a token sequence.

Two different RAG architectures are hypothesised and validated.
* RAG-sequence model: It fix a document and generate the token sequence.

    <img src="https://i.upmath.me/svg/p_%7B%5Ctext%20%7BRAG-Sequence%20%7D%7D(y%20%5Cmid%20x)%3D%5Csum_%7Bz%20%5Cin%20%5Coperatorname%7Btop%7D-k(p(%5Ccdot%20%5Cmid%20x))%7D%20p_%7B%5Ceta%7D(z%20%5Cmid%20x)%20%5Cprod_%7Bi%7D%5E%7BN%7D%20p_%7B%5Ctheta%7D%5Cleft(y_%7Bi%7D%20%5Cmid%20x%2C%20z%2C%20y_%7B1%3A%20i-1%7D%5Cright)" alt="p_{\text {RAG-Sequence }}(y \mid x)=\sum_{z \in \operatorname{top}-k(p(\cdot \mid x))} p_{\eta}(z \mid x) \prod_{i}^{N} p_{\theta}\left(y_{i} \mid x, z, y_{1: i-1}\right)" />
    * It uses "Thorough Decocoding" (for any sequence using a passage, it would also compute proabilities over other passages), and "Fast Decoding" (for any sequene from a passage, if that sequence is not among beam search outputs from other passages, it would be assumed 0). 


* RAG-token model: It runs in auto-regressive mode, where at each token it attend over all the documents.

    <img src="https://i.upmath.me/svg/p_%7B%5Ctext%20%7BRAG-Token%20%7D%7D(y%20%5Cmid%20x)%3D%5Cprod_%7Bi%7D%5E%7BN%7D%20%5Csum_%7Bz%20%5Cin%20%5Coperatorname%7Btop%7D-k(p(%5Ccdot%20%5Cmid%20x))%7D%20p_%7B%5Ceta%7D%5Cleft(z_%7Bi%7D%20%5Cmid%20x%5Cright)%20p_%7B%5Ctheta%7D%5Cleft(y_%7Bi%7D%20%5Cmid%20x%2C%20z_%7Bi%7D%2C%20y_%7B1%3A%20i-1%7D%5Cright)" alt="p_{\text {RAG-Token }}(y \mid x)=\prod_{i}^{N} \sum_{z \in \operatorname{top}-k(p(\cdot \mid x))} p_{\eta}\left(z_{i} \mid x\right) p_{\theta}\left(y_{i} \mid x, z_{i}, y_{1: i-1}\right)" />

* DPR (Dense Passage Retrieval) is used for retrieval, and BART is used as a generator.

**Results**
- Over closed book, open book, extractive and abstractive question answering, and other NLP tasks it does produce good results.

