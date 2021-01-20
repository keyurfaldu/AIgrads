## Generation-augmented retrieval for open-domain question answering. 
### Mao, Yuning, Pengcheng He, Xiaodong Liu, Yelong Shen, Jianfeng Gao, Jiawei Han, and Weizhu Chen. 
### arXiv preprint arXiv:2009.08553 (2020) [[arXiv](https://arxiv.org/pdf/2009.08553.pdf)]

**Whats Unique**
Open Domain QA follows the approach of retriever + reader. The performance of reader is upper bounded by the performance of retriever. This paper presents ideas on how to improve the retrieval performance by augementing the query using generative language model techniques.

**How It Works**
* In a Retriever-Reader setup, GAR generate query context using pre-trained LM, and those context are used to retrieve documents. Following additional context are considerd:
* The default target (answer): pre-trained LMs are able to answer certain question solely by taking the questions as input and generating answers.
* Sentence containing the default target
* Title of the passage containing the default target

* In open-domain question answering, the final score is computed as: 
<img src="https://i.upmath.me/svg/p%5Cleft(S_%7Bi%7D%5Bj%5D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D(%5Cmathbf%7BD%7D)%5Bi%5D%20%5Ctimes%20%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BS%7D_%7B%5Cmathbf%7Bi%7D%7D%5Cright)%5Bj%5D" alt="p\left(S_{i}[j]\right)=\operatorname{softmax}(\mathbf{D})[i] \times \operatorname{softmax}\left(\mathbf{S}_{\mathbf{i}}\right)[j]" />
    * Where, D[i] is i-th retrieved document
    * Si[j] is jth span in docuemnt i

* These generated additional context are helpful in both sparse retrieval as well as DPR (dense passage retrieval), results are as below:
<p align="center">
    <img width=600 src="images/GAR_results.png">
    <em>Source: Author</em>
    </p>


