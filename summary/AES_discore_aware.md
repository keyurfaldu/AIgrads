## Automated Essay Scoring with Discourse-Aware Neural Models
### Farah Nadeem, Huy Nguyen, Yang Liu, and Mari Ostendorf
### ACL 2019 [[arXiv](https://www.aclweb.org/anthology/W19-4450.pdf)]


**Whats Unique**
It proposes technique that discourse aware (word level => sentence level => document with attention scheme) models brings better scoring along with pre-traning techniques. 

**How Does It Work**
It uses two architectures which are discorse aware,
  * HAN (Hierarchical Attention Network)
  * BCA (Bidirectional context with attention)

It uses following pre-training objectives which makes sense to extract sementic meaning
* Natural language inference (NLI) task
* Discourse marker prediction (DM) task

It also uses BERT embeddings as contexualised embeddings. It uses second-to-last representations.

**Architecture**
* Word level LSTM, and Bidirectional context (in caser of BCA) is common to all pre-training methods and AES task. Rest components of model are task specific.

<p align="center">
    <img width=600 src="images/AES_discourse_aware_architecture.png">
    <em>Source: Author</em>
    </p>

**Experiments**
It has used following datasets:
* The ETS Corpus of Non-Native Written English from the Linguistic Data Consortium (LDC) of 12000 TOEFL essays
* The Automated Student Assessment Prize (ASAP) Competition dataset. Two sets, each has around 1700 essays.

* Results are captured in Quadratic Weighted Kappa score. 
* It achieves QWK of 0.729 on ETS corpus, and 0.84 on ASAP set 1.





