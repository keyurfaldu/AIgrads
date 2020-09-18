## KagNet: Knowledge-Aware Graph Networks for Commonsense Reasoning
### Bill Yuchen Lin, Xinyue Chen, Jamin Chen, Xiang Ren
### EMNLP-IJCNLP 19 [[arXiv](https://arxiv.org/pdf/1909.02151.pdf)]

**Whats New**
Using ConceptNet as the external knwoledge source, this paper achieves state of the art results on CommonsenseQA dataset, and proposes framework to transform question answers into a subgraph of external knowledge, and arriving decision by applying graph convolutional networks and LSTMs.

**How It Works**
* Commonsense required natural language question q and set of answers N, task is to choose the right answer.
* This involves two modules, 
1) Schema Graph Grounding
2) Graph Modelling Infernce
* Following figure illustrates it neatly
    <p align="center">
    <img width=600 src="images/kagnet_architecture.png">
    <em>Source: Author</em>
    </p>

* Schema Graph Grounding: It deals with extracting the graph from external knowledge ConceptNet, which requires to determine the plausible answer. The graphs are named "Schema Graphs" inspired by schema theory. It has three substes
    * Concept Recognition: Mentions maching concepts in  Extrenal grpahs are extracted by n-gram comparison, with some rules like soft-matching, lemmatization etc.
    * Schema Graph Construction: One way to find is minimal spanning tree covering the requried concepts identifed in step 1. This is NP-Complete problem to find "Steiner tree problem". Authors proposed a straightforward algo, to find paths among mentioned concepts (shorter than k).
    * Path pruning: ConceptNet is trained with ConvE, and path are decomposed in to triplets, and each triples is scored by ConvE. Triplets constituting a path are multipled to find the score of a path, and it is pruned if it is less than some threshold.

** Knowledge Aware Graph Network
    
* It applies GCN to tune embeddings for concept nodes in the context of extracted sub graph.
    
* Relation Path Encoding:
    
    * Path k between question concept node i, and answer concept node j is a sequence of triplets, 

        <img src="https://i.upmath.me/svg/P_%7Bi%2C%20j%7D%5Bk%5D%3D%5Cleft%5B%5Cleft(c_%7Bi%7D%5E%7B(q)%7D%2C%20r_%7B0%7D%2C%20t_%7B0%7D%5Cright)%2C%20%5Cldots%2C%5Cleft(t_%7Bn-1%7D%2C%20r_%7Bn%7D%2C%20c_%7Bj%7D%5E%7B(a)%7D%5Cright)%5Cright%5D" alt="P_{i, j}[k]=\left[\left(c_{i}^{(q)}, r_{0}, t_{0}\right), \ldots,\left(t_{n-1}, r_{n}, c_{j}^{(a)}\right)\right]" />

    * Latent representations of all the paths between Question concept i and Answer concept j is, 

        <img src="https://i.upmath.me/svg/%5Cmathbf%7BR%7D_%7Bi%2C%20j%7D%3D%5Cfrac%7B1%7D%7B%5Cleft%7CP_%7Bi%2C%20j%7D%5Cright%7C%7D%20%5Csum_%7Bk%7D%20%5Coperatorname%7BLSTM%7D%5Cleft(P_%7Bi%2C%20j%7D%5Bk%5D%5Cright)" alt="\mathbf{R}_{i, j}=\frac{1}{\left|P_{i, j}\right|} \sum_{k} \operatorname{LSTM}\left(P_{i, j}[k]\right)" />

    * Latent representation of sentence (question + answer), and question concept i, and aswer concept j is 

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cmathbf%7BT%7D_%7Bi%2C%20j%7D%20%26%3D%5Coperatorname%7BMLP%7D%5Cleft(%5Cleft%5B%5Cmathbf%7Bs%7D%20%3B%20%5Cmathbf%7Bc%7D_%7B%5Cmathbf%7Bq%7D%7D%5E%7B(%5Cmathbf%7Bi%7D)%7D%20%3B%20%5Cmathbf%7Bc%7D_%7B%5Cmathbf%7Ba%7D%7D%5E%7B(%5Cmathbf%7Bj%7D)%7D%5Cright%5D%5Cright)%20%5C%5C%20%5Cmathbf%7Bg%7D%20%26%3D%5Cfrac%7B%5Csum_%7Bi%2C%20j%7D%5Cleft%5B%5Cmathbf%7BR%7D_%7Bi%2C%20j%7D%20%3B%20%5Cmathbf%7BT%7D_%7Bi%2C%20j%7D%5Cright%5D%7D%7B%5Cleft%7C%5Cmathcal%7BC%7D_%7Bq%7D%5Cright%7C%20%5Ctimes%5Cleft%7C%5Cmathcal%7BC%7D_%7Ba%7D%5Cright%7C%7D%20%5Cend%7Baligned%7D" alt="\begin{aligned} \mathbf{T}_{i, j} &amp;=\operatorname{MLP}\left(\left[\mathbf{s} ; \mathbf{c}_{\mathbf{q}}^{(\mathbf{i})} ; \mathbf{c}_{\mathbf{a}}^{(\mathbf{j})}\right]\right) \\ \mathbf{g} &amp;=\frac{\sum_{i, j}\left[\mathbf{R}_{i, j} ; \mathbf{T}_{i, j}\right]}{\left|\mathcal{C}_{q}\right| \times\left|\mathcal{C}_{a}\right|} \end{aligned}" />

    * g, graph representation, is the average pooling of all pairs i, j for all-path-representation and direct-representation of question concept i and answer concept j. 

    * We can get the score with 
        * score(q, a) = sigmoid(MLP(g))

* Hierarchical Attention Mechanism
    * Concept-pair-path level attention
        * It is applied to get thre represetnation of all paths for a concept pair.
            <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Calpha_%7B(i%2C%20j%2C%20k)%7D%20%26%3D%5Cmathbf%7BT%7D_%7Bi%2C%20j%7D%20%5Cmathbf%7BW%7D_%7B1%7D%20%5Coperatorname%7BLSTM%7D%5Cleft(P_%7Bi%2C%20j%7D%5Bk%5D%5Cright)%20%5C%5C%20%5Chat%7B%5Calpha%7D_%7B(i%2C%20j%2C%20%5Ccdot)%7D%20%26%3D%5Coperatorname%7BSoftMax%7D%5Cleft(%5Calpha_%7B(i%2C%20j%2C%20%5Ccdot)%7D%5Cright)%20%5C%5C%20%5Chat%7B%5Cmathbf%7BR%7D%7D_%7Bi%2C%20j%7D%20%26%3D%5Csum%20%5Chat%7B%5Calpha%7D_%7B(i%2C%20j%2C%20k)%7D%20%5Ccdot%20%5Coperatorname%7BLSTM%7D%5Cleft(P_%7Bi%2C%20j%7D%5Bk%5D%5Cright)%20%5Cend%7Baligned%7D" alt="\begin{aligned} \alpha_{(i, j, k)} &amp;=\mathbf{T}_{i, j} \mathbf{W}_{1} \operatorname{LSTM}\left(P_{i, j}[k]\right) \\ \hat{\alpha}_{(i, j, \cdot)} &amp;=\operatorname{SoftMax}\left(\alpha_{(i, j, \cdot)}\right) \\ \hat{\mathbf{R}}_{i, j} &amp;=\sum \hat{\alpha}_{(i, j, k)} \cdot \operatorname{LSTM}\left(P_{i, j}[k]\right) \end{aligned}" />

    * Concept-pair level attention
        * It is applied to get the graph represenation.

            <img src="https://i.upmath.me/svg/%24%5Cbegin%7Baligned%7D%20%5Cbeta_%7B(i%2C%20j)%7D%20%26%3D%5Cmathbf%7Bs%7D%20%5Cmathbf%7BW%7D_%7B2%7D%20%5Cmathbf%7BT%7D_%7Bi%2C%20j%7D%20%5C%5C%20%5Chat%7B%5Cbeta%7D_%7B(%5Ccdot%2C%20%5Ccdot)%7D%20%26%3D%5Coperatorname%7BSoftMax%7D%5Cleft(%5Cbeta_%7B(%5Ccdot%2C%20%5Ccdot)%7D%5Cright)%20%5C%5C%20%5Chat%7B%5Cmathbf%7Bg%7D%7D%20%26%3D%5Csum_%7Bi%2C%20j%7D%20%5Chat%7B%5Cbeta%7D_%7B(i%2C%20j)%7D%5Cleft%5B%5Chat%7B%5Cmathbf%7BR%7D%7D_%7Bi%2C%20j%7D%20%3B%20%5Cmathbf%7BT%7D_%7Bi%2C%20j%7D%5Cright%5D%20%5Cend%7Baligned%7D" alt="$\begin{aligned} \beta_{(i, j)} &amp;=\mathbf{s} \mathbf{W}_{2} \mathbf{T}_{i, j} \\ \hat{\beta}_{(\cdot, \cdot)} &amp;=\operatorname{SoftMax}\left(\beta_{(\cdot, \cdot)}\right) \\ \hat{\mathbf{g}} &amp;=\sum_{i, j} \hat{\beta}_{(i, j)}\left[\hat{\mathbf{R}}_{i, j} ; \mathbf{T}_{i, j}\right] \end{aligned}" />
* Following figure illustrate the above steps:
    <p align="center">
    <img width=600 src="images/kagnet_steps.png">
    <em>Source: Author</em>
    </p>

**Results**
* It gives a table to compare performance at 10%, 50% and 100% of training data.
* It gives a marginal improvement of around 1% for BERT-finetuning methods
* It gives ablation study to back up design choices.

 




