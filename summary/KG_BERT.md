## KG-BERT: BERT for Knowledge Graph Completion
### Liang Yao, Chengsheng Mao, Yuan Luo
### AAAI 2020 [[arXiv](https://arxiv.org/pdf/1909.03193.pdf)]

**Whats New**
This paper applies BERT on KG tasks, like triplet classification, link prediction, and relation prediction, and it achieves state of the art or comparable results.

**How It Works**
Three KG tasks are as follow:
* Triplet classifcation: (h, r, t) => 0 or 1
* Link prediction: (h, r, ?) => t, (?, r, t) => h
* Relation prediction: (h, ?, t) => r

* Triplet classification and link prediction are solved using following architecture

    <p align="center">
        <img width=600 src="images/kg_bert_a.png">
        <em>Source: Author</em>
        </p>

* Relation prediction is solved using following variant architecture.
    <p align="center">
        <img width=600 src="images/kg_bert_b.png">
        <em>Source: Author</em>
        </p>

* Binary corss entropy loss for Triplet classifcation and link prediction.

    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D%3D-%5Csum_%7B%5Ctau%20%5Cin%20%5Cmathbb%7BD%7D%5E%7B%2B%7D%20%5Ccup%20%5Cmathbb%7BD%7D%5E%7B-%7D%7D%5Cleft(y_%7B%5Ctau%7D%20%5Clog%20%5Cleft(s_%7B%5Ctau%200%7D%5Cright)%2B%5Cleft(1-y_%7B%5Ctau%7D%5Cright)%20%5Clog%20%5Cleft(s_%7B%5Ctau%201%7D%5Cright)%5Cright)" alt="\mathcal{L}=-\sum_{\tau \in \mathbb{D}^{+} \cup \mathbb{D}^{-}}\left(y_{\tau} \log \left(s_{\tau 0}\right)+\left(1-y_{\tau}\right) \log \left(s_{\tau 1}\right)\right)" /> 

    * Where, CLS token is projected to s_t_0 and s_t_1 using W \in R^{2 x H}

* Cross entropy loss is used for relation prediction

    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D%5E%7B%5Cprime%7D%3D-%5Csum_%7B%5Ctau%20%5Cin%20%5Cmathbb%7BD%7D%5E%7B%2B%7D%7D%20%5Csum_%7Bi%3D1%7D%5E%7BR%7D%20y_%7B%5Ctau%20i%7D%5E%7B%5Cprime%7D%20%5Clog%20%5Cleft(s_%7B%5Ctau%20i%7D%5E%7B%5Cprime%7D%5Cright)" alt="\mathcal{L}^{\prime}=-\sum_{\tau \in \mathbb{D}^{+}} \sum_{i=1}^{R} y_{\tau i}^{\prime} \log \left(s_{\tau i}^{\prime}\right)" />

    * CLS token is projected to s'_t_i where i \in R relations.

* Link prediction is very very slow, because for (h, r, ?), score would be computed for each entitiy considered as tail entity, similarily for (?, r, t)

**Results**
* It has used following databases:
    * WN11: WordNet 11, and FB13: Freebase 13 contains positive and negative triplets, so it is used for triplet classification.
    * WN18RR, FB15K, FB15K-237 only contain correct triplets, so it is used for link and relation prediction.
    * Summary of these datasets are as below:
    <p align="center">
        <img width=600 src="images/kg_bert_datasets.png">
        <em>Source: Author</em>
        </p>

* It achieves state of the art results for triplet classification.
* For link preditcion, it achieves SOTA results for mean rank metric, but less than the best results for MRR
* It acheives state of the art results for relation predictions


