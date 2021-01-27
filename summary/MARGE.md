## "MARGE: Pre-training via paraphrasing."
### Lewis, Mike, Marjan Ghazvininejad, Gargi Ghosh, Armen Aghajanyan, Sida Wang, and Luke Zettlemoyer.
### 2020, [arXiv](https://arxiv.org/pdf/2006.15020.pdf)

**Whats Unique**
This paper presents a new alternative pre-training procedure which is best suited at task like para phrasing, translation, and summarisation. It has two model relevance and reconstruction. The Attention bias in reconstruction model comes through relevance model, hence back propogation is also able to train relevance model alongside. 

**Motivation: Pretraining via Paraphrasing**
* It has multi-lingual multi-document paraphrasing objective.
* Objective funciton is to reconstruct the target text by retrieving the similar text from multiple documents.
* It is possible to jointly learn reconstruction and retreival through attention mechanism.
* The objective captures the aspect of translation, summarisation, paraphrasing and retrieval. 

<p align="center">
    <img width=600 src="images/MARGE_motivation.png">
    <em>Source: Author</em>
    </p>

**Approach**
* Cosine Similarity score between target text and evidence text:

<img src="https://i.upmath.me/svg/f(x%2C%20z)%3D%5Cfrac%7Bg(x)%20%5Ccdot%20g(z)%7D%7B%5C%7Cg(x)%5C%7C%5C%7Cg(z)%5C%7C%7D" alt="f(x, z)=\frac{g(x) \cdot g(z)}{\|g(x)\|\|g(z)\|}" />

* We would need to minimize the negative log likelihood of the target document, given similarity and evidence documents.
* Its an auto-encoder type of loss where we need to generate target document from evidence and information bottleneck created because of similairy score.

<img src="https://i.upmath.me/svg/L_%7B%5Ctheta%7D%3D-%5Csum_%7Bi%7D%20%5Clog%20p_%7B%5Ctheta%7D%5Cleft(x_%7Bi%7D%20%5Cmid%20z_%7B1%20.%20.%20M%7D%2C%20f%5Cleft(x_%7Bi%7D%2C%20z_%7B1%7D%5Cright)%2C%20%5Cldots%2C%20f%5Cleft(x_%7Bi%7D%2C%20z_%7BM%7D%5Cright)%5Cright)" alt="L_{\theta}=-\sum_{i} \log p_{\theta}\left(x_{i} \mid z_{1 . . M}, f\left(x_{i}, z_{1}\right), \ldots, f\left(x_{i}, z_{M}\right)\right)" />

* Attention mechanism would also have a bias of similairity score, so it would also alter or learn the similarity scoring by tweaking the embeddings.

<img src="https://i.upmath.me/svg/%5Calpha%3D%5Coperatorname%7Bsoftmax%7D_%7Bz_%7B1%20.%20.%20M%7D%7D%3DQ%5E%7Bl%20h%7D%5Cleft(x_%7Bi%7D%5Cright)%20K%5E%7Bl%20h%7D%5Cleft(z_%7B1%20.%20.%20M%7D%5Cright)%2B%5Cbeta%20f%5Cleft(x_%7Bi%7D%2C%20z_%7Bj%7D%5Cright)%20%5Cin%20%5Cmathbb%7BR%7D%5E%7B%5Cleft%7Cx_%7Bi%7D%5Cright%7C%20%5Ctimes%20%5Csum_%7Bj%7D%5Cleft%7Cz_%7Bj%7D%5Cright%7C%7D" alt="\alpha=\operatorname{softmax}_{z_{1 . . M}}=Q^{l h}\left(x_{i}\right) K^{l h}\left(z_{1 . . M}\right)+\beta f\left(x_{i}, z_{j}\right) \in \mathbb{R}^{\left|x_{i}\right| \times \sum_{j}\left|z_{j}\right|}" />

* With around 1B parameters, it took 4700 GPU days to pretrain a model, which would be better suited for translation, summarisation, paraphrasing etc objectives.
