## GATE: Graph Attention Transformer Encoder for Cross-lingual Relation and Event Extraction
### Wasi Uddin Ahmad, Nanyun Peng, Kai-Wei Chang
### Oct 2020, [[arXiv](https://arxiv.org/pdf/2010.03009.pdf)]

**Whats Unique**
This present an approach to fuse structural information to learn the dependencies between words at different syntactic distances through self-attention mechanism, which improves cross lingual transferability on tasks like relation extraction and event extractions. 

ACE05 dataset was used, which is multilingual dataset for english, chinese and arabic. 

**Tasks**
* Relation extraction
- Task to idenify the relation type of an ordered pair of entity mentions, e_s: subject entity, e_o: object entity, and sentence s. 
- Extract relation r for tripple (e_s, e_o, s)
* Event Extraction
    * Event detection
        * Task of identifying event triggers, e_t
    * Event argument role labelling
        * Words or phrases that expresses event occurances
        * Whether word or phrase participate in events and their roles. 
        * Given event trigger e_t, and a entity mention, e_a from a sentence s, what is the argument role labelling to predict mention's role.

**Approach**
* Invoke UDPipe to convert input sentence to language-universal dependency tree
* Embed words into shared multilingual embedding space. Word representatios is enriched by POS tag, dependency relation, and entity type embedding. => language universal features
* Encode inputsentence using GATE encoder, which leverage syntactic information with self attention mechnism
* Downstream classifer to predict target relation and argument role label based on encoded representation produced by GATE.

**Fusing Syntactic Information**
* Distance matrics is computed as follow:
<p align="center">
    <img width=600 src="images/GATE_distance_matrix.png">
    <em>Source: Author</em>
    </p>

* Attention score is computed based on following updated mechanism
    <img src="https://i.upmath.me/svg/%20A_%7Bl%7D%3DF%5Cleft(%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cfrac%7BQ%20K%5E%7BT%7D%7D%7B%5Csqrt%7Bd_%7Bk%7D%7D%7D%2BM%5Cright)%5Cright)%20V_%7Bl%7D" alt=" A_{l}=F\left(\operatorname{softmax}\left(\frac{Q K^{T}}{\sqrt{d_{k}}}+M\right)\right) V_{l}" />

* Where attention mask M is computed as follow: Where, delta is a configurable parameter.
    <img src="https://i.upmath.me/svg/%20M_%7Bi%20j%7D%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Bll%7D%0A0%2C%20%26%20D_%7Bi%20j%7D%20%5Cleq%20%5Cdelta%20%5C%5C%0A-%5Cinfty%2C%20%26%20%5Ctext%20%7B%20otherwise%20%7D%0A%5Cend%7Barray%7D%5Cright." alt=" M_{i j}=\left\{\begin{array}{ll} 0, &amp; D_{i j} \leq \delta \\ -\infty, &amp; \text { otherwise } \end{array}\right." />

    <img src="https://i.upmath.me/svg/F(P)_%7Bi%20j%7D%3D%5Cfrac%7BP_%7Bi%20j%7D%7D%7BZ_%7Bi%7D%20D_%7Bi%20j%7D%7D%20%5C%5C%0AZ_%7Bi%7D%3D%5Csum_%7Bj%7D%20%5Cfrac%7BP_%7Bi%20j%7D%7D%7BD_%7Bi%20j%7D%7D" alt="F(P)_{i j}=\frac{P_{i j}}{Z_{i} D_{i j}} \\
Z_{i}=\sum_{j} \frac{P_{i j}}{D_{i j}}" />

* Loss functions
    * Relation Extraction
    <img src="https://i.upmath.me/svg/%20%5Cmathcal%7BL%7D_%7Br%7D%3D-%5Csum_%7Bs%3D1%7D%5E%7BN%7D%20%5Csum_%7Bo%3D1%7D%5E%7BN%7D%20%5Csum_%7Br%20%5Cin%20R%7D%20y_%7Bs%20o%7D%5E%7Br%7D%20%5Clog%20%5Cleft(%5Csigma%5Cleft(%5Cboldsymbol%7BU%7D%5E%7Br%7D%20%5Ccdot%5Cleft%5B%5Chat%7Be_%7Bs%7D%7D%20%3B%20%5Chat%7Be%7D_%7Bo%7D%20%3B%20%5Chat%7Bs%7D%5Cright%5D%5Cright)%5Cright)" alt=" \mathcal{L}_{r}=-\sum_{s=1}^{N} \sum_{o=1}^{N} \sum_{r \in R} y_{s o}^{r} \log \left(\sigma\left(\boldsymbol{U}^{r} \cdot\left[\hat{e_{s}} ; \hat{e}_{o} ; \hat{s}\right]\right)\right)" />

    * Event Argument Role Labeler
    <img src="https://i.upmath.me/svg/%20%5Cmathcal%7BL%7D_%7Ba%7D%3D%5Csum_%7Bt%3D1%7D%5E%7BN%7D%20%5Csum_%7Ba%3D1%7D%5E%7BC_%7Bt%7D%7D%20%5Csum_%7Br%20%5Cin%20R%7D%20y_%7Bt%20a%7D%5E%7Br%7D%20%5Clog%20%5Cleft(%5Csigma%5Cleft(%5Cboldsymbol%7BU%7D%5E%7Ba%7D%20%5Ccdot%5Cleft%5B%5Chat%7Be_%7Bt%7D%7D%20%3B%20%5Chat%7Be_%7Ba%7D%7D%20%3B%20%5Chat%7Bs%7D%5Cright%5D%5Cright)%5Cright)" alt=" \mathcal{L}_{a}=\sum_{t=1}^{N} \sum_{a=1}^{C_{t}} \sum_{r \in R} y_{t a}^{r} \log \left(\sigma\left(\boldsymbol{U}^{a} \cdot\left[\hat{e_{t}} ; \hat{e_{a}} ; \hat{s}\right]\right)\right)" />

* Results
    * GATE has shown improvement over other SOTA methods.


    





