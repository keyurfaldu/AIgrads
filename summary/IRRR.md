## Retrieve, Rerank, Read, then Iterate: Answering Open-Domain Questions of Arbitrary Complexity from Text

### Peng Qi, Christopher Manning et al. 
### 2020 [[arXiv](https://arxiv.org/pdf/2010.12527.pdf)]

**Whats Unique**
This paper present a single transformer based DNN model which can act as retriever, re-ranker, and reader to solve open domain question answering end to end. And, it is robust to generalise over 3-hop questions, even though it is not trained on for the same, thanks to its inherent architecture.

**Major Contribution**
* A unified DNN model that perfrom all essential sub tasks for open domain QA purely from the text.(retrieval, re-ranking, and reading comprehension)
* A new open domain QA benchmark that features different levels of complexity on an unified, uptodate version of wikipedia with newly annotated 3-hop questions.

**Illustration and Architecture**
<p align="center">
    <img width=600 src="images/IRRR_flow.png">
    <em>Source: Author</em>
    </p>

* Above figure illustrate the flow, query is formed from a question, answer is predicted from the current question and retrieved paras, documents are ranked and selected as the contexual paras for further steps.

* Following figure show multi-taks leanring setup of IRRR system
<p align="center">
    <img width=600 src="images/IRRR_architecture.png">
    <em>Source: Author</em>
    </p>

**Supervised Training**
* Retriever
    * Overlapping spans between target paragraph and question and retrieved paragraphs are taken. 
    * Importance of each overalapped span is computed as follow: (t is target span)

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Ctext%20%7B%20Importance%20%7D%5Cleft(s_%7Bi%7D%5E%7Bo%7D%5Cright)%20%26%3D%5Coperatorname%7BRank%7D%5Cleft(t%2C%5Cleft%5C%7Bs_%7Bj%7D%5E%7Bo%7D%5Cright%5C%7D_%7Bj%3D1%2C%20j%20%5Cneq%20i%7D%5E%7BN%7D%5Cright)%20%5C%5C%0A%26-%5Coperatorname%7BRank%7D%5Cleft(t%2C%5Cleft%5C%7Bs_%7Bi%7D%5E%7Bo%7D%5Cright%5C%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\text { Importance }\left(s_{i}^{o}\right) &amp;=\operatorname{Rank}\left(t,\left\{s_{j}^{o}\right\}_{j=1, j \neq i}^{N}\right) \\
&amp;-\operatorname{Rank}\left(t,\left\{s_{i}^{o}\right\}\right)
\end{aligned}" />
    * Spans are sorted based on its importance and length, and highest one is considered as the oracle query.

* Reader
    * Four way classifer, NOANSWER, Span Yes, and No is trained.
    * And, a sperated span predictor for start token and end token is trained.
    * Answerability is log likelihood ratio between most positive predicted span and the NOANSWER prediction. 

* Reranker
    * Reranker select one of the retrieved paragraphs to expand the search query. 
    * CLS token with linear transformation is used for the same. 

**Results**
* It achieves state of the art performance, and also able to generalise well.





