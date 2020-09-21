## KEPLER: A Unified Model for Knowledge Embedding and  Pre-trained Language Representation
### Wang et al, 
### Preprint, Feb 2020 [[arXiv](https://arxiv.org/pdf/1911.06136.pdf)]

**Whats New**
This paper proposes "Knowledge Embedding and Pre-trainined Language Representation" method to jointly learn KG and pre-trained LM representations, and it shows its impact on downstream tasks.

**Major Contribution**
Major contribution of this paper is three fold
* Author proposes KEPLER, knolwedge enhanced PLR with jointly optimizing the KE and MLM objectives which brings great improvements on wide range of NLP tasks. 
* By encoding text descriptions as entity embeddings, KEPLER shows its effectiveness as a KE model, especially in an inductive setting
* Authors introduced a dataset Wikidata5M, a new large-scale KG dataset, which shall promote the research on large scale KG, inductive KG, and the interactions between KG and NLP.

AS a PLM, it achieves following:
* Integrate knowledge into language understanding
* Inherits strong ability of langauge understanding from PLMs by the MLM objective
* KE objective enhances the ability to extract knowledge from the text
* Can be directly adopted to a wide range of NLP tasks without additional infernece overhead

AS a KE model
* Can better utilises the abundant information from entity descriptions
* Inductive in nature, can generate entity embeddings in inductive fashion from entity descriptions

**How it works**
* Following figure illustrates the process really well
    <p align="center">
        <img width=600 src="images/kepler_illustration.png">
        <em>Source: Author</em>
        </p>
* KF loss is inspired from RotateE/tansE, 

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BKE%7D%7D%20%26%3D-%5Clog%20%5Csigma%5Cleft(%5Cgamma-d_%7Br%7D(%5Cmathbf%7Bh%7D%2C%20%5Cmathbf%7Bt%7D)%5Cright)%20%5C%5C-%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%20%26%20%5Cfrac%7B1%7D%7Bn%7D%20%5Clog%20%5Csigma%5Cleft(d_%7Br%7D%5Cleft(%5Cmathbf%7Bh%7D_%7B%5Cmathbf%7Bi%7D%7D%5E%7B%5Cprime%7D%2C%20%5Cmathbf%7Bt%7D_%7B%5Cmathbf%7Bi%7D%7D%5E%7B%5Cprime%7D%5Cright)-%5Cgamma%5Cright)%20%5Cend%7Baligned%7D" alt="\begin{aligned} \mathcal{L}_{\mathrm{KE}} &amp;=-\log \sigma\left(\gamma-d_{r}(\mathbf{h}, \mathbf{t})\right) \\-\sum_{i=1}^{n} &amp; \frac{1}{n} \log \sigma\left(d_{r}\left(\mathbf{h}_{\mathbf{i}}^{\prime}, \mathbf{t}_{\mathbf{i}}^{\prime}\right)-\gamma\right) \end{aligned}" />
    * Where, h is head entity, t is tail entity and dr is a score function given head, tail and relation r. lambda is a margin.

    * Following score function is used.

    <img src="https://i.upmath.me/svg/d_%7Br%7D(%5Cmathbf%7Bh%7D%2C%20%5Cmathbf%7Bt%7D)%3D%5C%7C%5Cmathbf%7Bh%7D%2B%5Cmathbf%7Br%7D-%5Cmathbf%7Bt%7D%5C%7C_%7Bp%7D" alt="d_{r}(\mathbf{h}, \mathbf{t})=\|\mathbf{h}+\mathbf{r}-\mathbf{t}\|_{p}" />

    * Head and Tail embeddings are embeddings of CLS token of their description.

Wikidata5M dataset comparision with other datasets are as below:
    <p align="center">
        <img width=600 src="images/kepler_wikidata5M.png">
        <em>Source: Author</em>
        </p>

Experiments:
* It has used following different models
    * Kepler-Wiki
    * Kepler-WordNet
    * Kepler-Wiki+WordNet

* And it has proven its value addtion on following kinds of NLP tasks
    * Relationship classification: classify the relationship type between two given entities
        * TACRED
        * FewRel

    * Entity Typing: Classify given entity mentions into pre-defined types
    * GLUE
    * Link Prediction in transductive setting and inductive settings

