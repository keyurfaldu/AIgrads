## Connecting the dots: A knowledgeable path generator for commonsense question answering.
### Wang, Peifeng, Nanyun Peng, Filip Ilievski, Pedro Szekely, and Xiang Ren. 
### arXiv preprint arXiv:2005.00691 (2020).

**Whats Unique**
This paper presents a knowledgeable path generator, and shows its utitlity in lifting the performance of NLP models for QA task. Given two entities from question and answer, it automatically generate a KG path, which may contain novel relations as well. 

To infuse a relevant portion of Knowledge Graph in NLP models, (1) it is important to contextualize and extract sub-graph or paths from the complete KG. (2) Generally, KG suffers from sparsity and incompleteness.

This research try to fill both the above gaps.

**Motivating Example**
Following figure demonstrate how KG can be relevant.
<p align="center">
    <img width=600 src="images/ConnectingDots_example.png">
    <em>Source: Author</em>
    </p>

**How It Works**

**Dynamic KG Path Generator**
* It fine-tune GPT-2 model to generate dynamic KG path as follow: Given "Tail Entity, [SEP], Head Entity", GPT-2 would generate a complete path from head entity till the tail entity.
* It fine-tune GPT-2 model using triples and multi-hop paths sampled from ConceptNet and ATOMIC commonsense KG.
* It extract the hidden representation of the tokens of the generated path, and aggregate it based on the attention of context (i.e. question and answer choice)

**KG Augmented Framework**
Following figure demonstrate how dynamic paths from KG can be augmented.
<p align="center">
    <img width=600 src="images/ConnectingDots_KGAug.png">
    <em>Source: Author</em>
    </p>

Knowledge Encoder derives embedding k using following math. Where it is the weighted average of each paths embeddings using its attention with respect to context of question and answer.

<img src="https://i.upmath.me/svg/%5Cmathbf%7Bk%7D%3Df_%7B%5Cphi%7D%5Cleft(%5Cleft%5C%7Bg_%7B%5Ctheta%7D(p)%20%5Cmid%20p%20%5Cin%20%5Cmathcal%7BP%7D%5Cright%5C%7D%5Cright)%5C%5C%0A%5Cmathbf%7Bk%7D%3D%5Csum_%7Bp%20%5Cin%20%5Cmathcal%7BP%7D%7D%20%5Calpha_%7Bp%7D%20%5Cmathbf%7Bp%7D%5C%5C%0A%5Calpha_%7Bp%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(%5Chat%7B%5Calpha%7D_%7Bp%7D%5Cright)%7D%7B%5Csum_%7Bp%7D%5E%7B%5Cprime%7D%20%5Cexp%20%5Cleft(%5Chat%7B%5Calpha%7D_%7Bp%7D%5E%7B%5Cprime%7D%5Cright)%7D%5C%5C%0A%5Chat%7B%5Calpha%7D_%7Bp%7D%3D%5Cmathbf%7Bc%7D%5E%7B%5Ctop%7D%20%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Ba%20t%20t%7D%20%5Ccdot%20%5Cmathbf%7Bp%7D%2B%5Cmathbf%7Bb%7D_%7Ba%20t%20t%7D%5Cright)" alt="\mathbf{k}=f_{\phi}\left(\left\{g_{\theta}(p) \mid p \in \mathcal{P}\right\}\right)\\
\mathbf{k}=\sum_{p \in \mathcal{P}} \alpha_{p} \mathbf{p}\\
\alpha_{p}=\frac{\exp \left(\hat{\alpha}_{p}\right)}{\sum_{p}^{\prime} \exp \left(\hat{\alpha}_{p}^{\prime}\right)}\\
\hat{\alpha}_{p}=\mathbf{c}^{\top} \tanh \left(\mathbf{W}_{a t t} \cdot \mathbf{p}+\mathbf{b}_{a t t}\right)" />

**Results**
It improves the performance of CommonsenseQA and OpendomainQA using the KG augmentation with the help of dynamic kg path discovery.