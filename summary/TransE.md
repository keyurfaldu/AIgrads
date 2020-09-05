## Translating Embeddings for Modeling Multi-relational Data
### Antoine Bordes, Nicolas Usunier, Alberto Garcia-Duran
### NIPS 2013 [[arXiv](https://papers.nips.cc/paper/5071-translating-embeddings-for-modeling-multi-relational-data.pdf)]

**Whats New** It proposes a simple and effective way for modeling relations as translation of head to tail using low dimensional embeddings.

**How It Works**
* It minimize following margin baed loss:
    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D%3D%5Csum_%7B(h%2C%20%5Cell%2C%20t)%20%5Cin%20S%7D%20%5Csum_%7B%5Cleft(h%5E%7B%5Cprime%7D%2C%20%5Cell%2C%20t%5E%7B%5Cprime%7D%5Cright)%20%5Cin%20S_%7B(h%2C%20%5Cell%2C%20t)%7D%5E%7B%5Cprime%7D%7D%5Cleft%5B%5Cgamma%2Bd(%5Cboldsymbol%7Bh%7D%2B%5Cboldsymbol%7B%5Cell%7D%2C%20%5Cboldsymbol%7Bt%7D)-d%5Cleft(%5Cboldsymbol%7Bh%7D%5E%7B%5Cprime%7D%2B%5Cboldsymbol%7B%5Cell%7D%2C%20%5Cboldsymbol%7Bt%7D%5E%7B%5Cprime%7D%5Cright)%5Cright%5D_%7B%2B%7D" alt="\mathcal{L}=\sum_{(h, \ell, t) \in S} \sum_{\left(h^{\prime}, \ell, t^{\prime}\right) \in S_{(h, \ell, t)}^{\prime}}\left[\gamma+d(\boldsymbol{h}+\boldsymbol{\ell}, \boldsymbol{t})-d\left(\boldsymbol{h}^{\prime}+\boldsymbol{\ell}, \boldsymbol{t}^{\prime}\right)\right]_{+}" />
    * d is disimilarity measure, and h', t' are corrupt triplets. corrupt entries are created as below: 

    <img src="https://i.upmath.me/svg/S_%7B(h%2C%20%5Cell%2C%20t)%7D%5E%7B%5Cprime%7D%3D%5Cleft%5C%7B%5Cleft(h%5E%7B%5Cprime%7D%2C%20%5Cell%2C%20t%5Cright)%20%5Cmid%20h%5E%7B%5Cprime%7D%20%5Cin%20E%5Cright%5C%7D%20%5Ccup%5Cleft%5C%7B%5Cleft(h%2C%20%5Cell%2C%20t%5E%7B%5Cprime%7D%5Cright)%20%5Cmid%20t%5E%7B%5Cprime%7D%20%5Cin%20E%5Cright%5C%7D" alt="S_{(h, \ell, t)}^{\prime}=\left\{\left(h^{\prime}, \ell, t\right) \mid h^{\prime} \in E\right\} \cup\left\{\left(h, \ell, t^{\prime}\right) \mid t^{\prime} \in E\right\}" />

* It experimented on two databases, Freebase and Wordnet.
    * Evaluation criteria:
        * It removes head, and instead evaluate disimilarity between h'+l, and t for all entities as h'. 
        * Arrange all entities h' as per score
        * It measures the rank of correct entitiy h = h'
        * It also tracks hits @ top-10

    * Results shows that TransE has outperformed current SOTA techniques.
        <p align="center">
        <img width=600 src="images/transe_link_prediction.png">
        <em>Source: Author</em>
        </p>

    * Also, perforamnce across 1-1, 1-Many, Many-1, and Many-Many was also encouraging.
    * Few examples of the tail entities predicted are, 
        <p align="center">
        <img width=600 src="images/transe_examples_tail_prediction.png">
        <em>Source: Author</em>
        </p>
    * It also demonstrated capability of transfer learning, by splitting the data into two parts (keeping entities covered, but relationships are partinitoned). TransE was better among the candidates.
    <p align="center">
        <img width=600 src="images/transe_transfer_learnig.png">
        <em>Source: Author</em>
        </p>


