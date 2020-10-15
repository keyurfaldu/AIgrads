## Question Generation for Question Answering
### Nan Duan, Duyu Tang, Peng Chen, Ming Zhou
### EMNLP 2017 [[arXiv](https://www.aclweb.org/anthology/D17-1090.pdf)]

**Whats Unique**
This paper present a pipeline for question generation using techniques from classical datamining, machine learning, attention, and deep learning. 

**How It Works**
It generates questions using pipeline of the following modules.
1. Question Pattern Mining
    * It mined questions from various datasets, to generate question patterns, i.e. “who founded # ?”, where one word/phrase from question is made replaced by special word. And, the masked phrase becomes question topic.
    <p align="center">
    <img width=600 src="images/QGforQA_question_patterns.png">
    <em>Source: Author</em>
    </p>
2. Question Pattern Prediction
    * Retrieval based approach: Question pattern is predicted with an attention based neural network with the following loss function, where S is paragraph and Q_p is question pattern. It minimise the distance of positive question pattern and maximise the distance of negative question pattern from the paragraph. 
    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Br%7D%0A%5Cmathcal%7BL%7D%3D%5Cmax%20%5Cleft%5C%7B0%2C%20M-%5Coperatorname%7Bcosine%7D%5Cleft(y(%5Cmathcal%7BS%7D)%2C%20y%5Cleft(%5Cmathcal%7BQ%7D_%7Bp%7D%5Cright)%5Cright)%5Cright.%20%5C%5C%0A%5Cleft.%5Cquad%2B%5Coperatorname%7Bcosine%7D%5Cleft(y(%5Cmathcal%7BS%7D)%2C%20y%5Cleft(%5Cmathcal%7BQ%7D_%7Bp%7D%5E%7B-%7D%5Cright)%5Cright)%5Cright%5C%7D%0A%5Cend%7Barray%7D" alt="\begin{array}{r}
\mathcal{L}=\max \left\{0, M-\operatorname{cosine}\left(y(\mathcal{S}), y\left(\mathcal{Q}_{p}\right)\right)\right. \\
\left.\quad+\operatorname{cosine}\left(y(\mathcal{S}), y\left(\mathcal{Q}_{p}^{-}\right)\right)\right\}
\end{array}" />
    * Generative approach: Question pattern is generated based on the passage S with the generative loss function as follow:
    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D%3D-%5Cfrac%7B1%7D%7BM%7D%20%5Csum_%7B%3C%5Cmathcal%7BS%7D%2C%20%5Cmathcal%7BQ%7D_%7Bp%7D%3E%7D%20%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20%5Clog%20%5Cleft(p%5Cleft(y_%7Bt%7D%20%5Cmid%20y_%7B%3Ct%7D%2C%20%5Cmathcal%7BS%7D%5Cright)%5Cright)" alt="\mathcal{L}=-\frac{1}{M} \sum_{&lt;\mathcal{S}, \mathcal{Q}_{p}&gt;} \sum_{t=1}^{T} \log \left(p\left(y_{t} \mid y_{&lt;t}, \mathcal{S}\right)\right)" />
3. Question Topic Selection:
    * Retrieval based appraoch: Confidence of Q_t extracted for Q_p from passage S is given as below. Where, Q_p^tk are historical question topics. and N = Sum(#Q_p^tk for all k)

        <img src="https://i.upmath.me/svg/s%5Cleft(%5Cmathcal%7BQ%7D_%7Bt%7D%2C%20%5Cmathcal%7BQ%7D_%7Bp%7D%5Cright)%3D%5Cfrac%7B1%7D%7BN%7D%20%5Ccdot%20%5Csum_%7Bk%7D%20%5C%23%5Cleft(%5Cmathcal%7BQ%7D_%7Bp%7D%5E%7Bt_%7Bk%7D%7D%5Cright)%20%5Ccdot%20%5Coperatorname%7Bdist%7D%5Cleft(v_%7B%5Cmathcal%7BQ%7D_%7Bt%7D%7D%2C%20v_%7B%5Cmathcal%7BQ%7D_%7Bp%7D%5E%7Bt_%7Bk%7D%7D%7D%5Cright)" alt="s\left(\mathcal{Q}_{t}, \mathcal{Q}_{p}\right)=\frac{1}{N} \cdot \sum_{k} \#\left(\mathcal{Q}_{p}^{t_{k}}\right) \cdot \operatorname{dist}\left(v_{\mathcal{Q}_{t}}, v_{\mathcal{Q}_{p}^{t_{k}}}\right)" />

    * Generative approach: Neural approach use the question topic with maximum attention which was computed to generate question pattern

        <img src="https://i.upmath.me/svg/w_%7Bj%7D%3D%5Carg%20%5Cmax%20_%7Bw_%7Bj%5E%7B%5Cprime%7D%7D%20%5Cin%20%5Cmathcal%7BS%7D%7D%20%5Calpha_%7Bi%20j%5E%7B%5Cprime%7D%7D%3D%5Carg%20%5Cmax%20_%7Bw_%7Bj%5E%7B%5Cprime%7D%7D%20%5Cin%20%5Cmathcal%7BS%7D%7D%20%5Cfrac%7B%5Cexp%20%5Cleft(e_%7Bi%20j%5E%7B%5Cprime%7D%7D%5Cright)%7D%7B%5Csum_%7Bk%3D1%7D%5E%7B%7C%5Cmathcal%7BS%7D%7C%7D%20%5Cexp%20%5Cleft(e_%7Bi%20k%7D%5Cright)%7D" alt="w_{j}=\arg \max _{w_{j^{\prime}} \in \mathcal{S}} \alpha_{i j^{\prime}}=\arg \max _{w_{j^{\prime}} \in \mathcal{S}} \frac{\exp \left(e_{i j^{\prime}}\right)}{\sum_{k=1}^{|\mathcal{S}|} \exp \left(e_{i k}\right)}" />

4. Question Ranking
    * Using labelled data, a linear model is trained to predict the rank of the question genrated, i.e. question pattern + question topic. It uses features like question pattern prediction score, question topic selection score, QA matching score, word overlap between question Q and passage S, question pattern frequency etc.

5. Question generation for QA
    * It select the best question for the best answer which maximise the probability of "generating a question given that answer, multiplied by probability of answer given that question".

        <img src="https://i.upmath.me/svg/%5Cwidehat%7B%5Cmathcal%7BA%7D%7D%3D%5Carg%20%5Cmax%20_%7B%5Cmathcal%7BA%7D%7D%5Cleft%5C%7BP(%5Cmathcal%7BA%7D%20%5Cmid%20%5Cmathcal%7BQ%7D)%2B%5Clambda%20%5Ccdot%20Q%20Q%5Cleft(%5Cmathcal%7BQ%7D%2C%20%5Cmathcal%7BQ%7D_%7B%5Cmax%20%7D%5E%7Bg%20e%20n%7D%5Cright)%5Cright%5C%7D" alt="\widehat{\mathcal{A}}=\arg \max _{\mathcal{A}}\left\{P(\mathcal{A} \mid \mathcal{Q})+\lambda \cdot Q Q\left(\mathcal{Q}, \mathcal{Q}_{\max }^{g e n}\right)\right\}" />

* Results:
    * It has computed BLEU score for both retrieval based method and generative mehthod for SQUAD, MSMarco, and WikiQA. And, for retrieval methods, BLUE scores are around 8-10%, and for generative methods they are around 11-13%.
