## Toward Subgraph Guided Knowledge Graph Question Generation with Graph Neural Networks
### Yu Chen, Lingfei Wu, Mohammed J. Zaki
### [[arXiv](https://arxiv.org/pdf/2004.06015.pdf)] 2020

**Whats Unique**
This paper proposes BiGGNN (Bidirectional Gated Graph Neural Network) based question generation from KG subgraph. It proposes Graph2Seq model for the same. 

**Main Contributions**
1. Propose Graph2Seq model for sub graph guided question generation from KGs.
2. Extended RNN decoder with a novel copy mechanism, that allow node attributes to be borrowed from KG subgraph.
3. Compare initialising node/relation embeddings when applying a GNN to process KG Subgraphs.

**Problem Formulation**
* Given KG subgraph G, and Answer Entity, we need to generate question Q which has the max conditional likelihood.

**Encoding Layer**
* Nodes and edges are intitialised with BiLSTM on GloVE embeddings of words making up the textual attributes. Authors believes that decoder would find it easy to generate questions given these hints.
* Leanrable answer markup vector is associated to each node/edge to indicate whether it is an answer or not.
* Initial vector representation of node/edge would be concatenation of BiLSTM output and the answer markup vector.

**Architecture**
<p align="center">
        <img width=600 src="images/Graph2Seq_QG_architecture.png">
        <em>Source: Author</em>
        </p>
**BiDirectional Graph2Seq Generator with Copying Mechanism**
* BiDirectional Graph Encoder
    * Take average of incoming and outgoing neighbors and fuse it to get the representation of a node for the next hop. n number of hops is an hyperparameter.
    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cdashv(v)%7D%7D%5E%7Bk%7D%3D%5Coperatorname%7BAVG%7D%5Cleft(%5Cleft%5C%7B%5Cmathbf%7Bh%7D_%7Bv%7D%5E%7Bk-1%7D%5Cright%5C%7D%20%5Ccup%5Cleft%5C%7B%5Cmathbf%7Bh%7D_%7Bu%7D%5E%7Bk-1%7D%2C%20%5Cforall%20u%20%5Cin%20%5Cmathcal%7BN%7D_%7B%5Cdashv(v)%7D%5Cright%5C%7D%5Cright)%5C%5C%0A%24%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cvdash(v)%7D%7D%5E%7Bk%7D%3D%5Coperatorname%7BAVG%7D%5Cleft(%5Cleft%5C%7B%5Cmathbf%7Bh%7D_%7Bv%7D%5E%7Bk-1%7D%5Cright%5C%7D%20%5Ccup%5Cleft%5C%7B%5Cmathbf%7Bh%7D_%7Bu%7D%5E%7Bk-1%7D%2C%20%5Cforall%20u%20%5Cin%20%5Cmathcal%7BN%7D_%7B%5Cvdash(v)%7D%5Cright%5C%7D%5Cright)" alt="\mathbf{h}_{\mathcal{N}_{\dashv(v)}}^{k}=\operatorname{AVG}\left(\left\{\mathbf{h}_{v}^{k-1}\right\} \cup\left\{\mathbf{h}_{u}^{k-1}, \forall u \in \mathcal{N}_{\dashv(v)}\right\}\right)\\
$\mathbf{h}_{\mathcal{N}_{\vdash(v)}}^{k}=\operatorname{AVG}\left(\left\{\mathbf{h}_{v}^{k-1}\right\} \cup\left\{\mathbf{h}_{u}^{k-1}, \forall u \in \mathcal{N}_{\vdash(v)}\right\}\right)" />
    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B(v)%7D%7D%5E%7Bk%7D%3D%5Coperatorname%7BFuse%7D%5Cleft(%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cdashv(v)%7D%7D%5E%7Bk%7D%2C%20%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cvdash(v)%7D%7D%5E%7Bk%7D%5Cright)" alt="\mathbf{h}_{\mathcal{N}_{(v)}}^{k}=\operatorname{Fuse}\left(\mathbf{h}_{\mathcal{N}_{\dashv(v)}}^{k}, \mathbf{h}_{\mathcal{N}_{\vdash(v)}}^{k}\right)" />
    <img src="https://i.upmath.me/svg/Fuse%20%24(%5Cmathbf%7Ba%7D%2C%20%5Cmathbf%7Bb%7D)%3D%5Cmathbf%7Bz%7D%20%5Codot%20%5Cmathbf%7Ba%7D%2B(1-%5Cmathbf%7Bz%7D)%20%5Codot%20%5Cmathbf%7Bb%7D%24%5C%5C%0A%24%5Cmathbf%7Bz%7D%3D%5Csigma%5Cleft(%5Cmathbf%7BW%7D_%7Bz%7D%5B%5Cmathbf%7Ba%7D%20%3B%20%5Cmathbf%7Bb%7D%20%3B%20%5Cmathbf%7Ba%7D%20%5Codot%20%5Cmathbf%7Bb%7D%20%3B%20%5Cmathbf%7Ba%7D-%5Cmathbf%7Bb%7D%5D%2B%5Cmathbf%7Bb%7D_%7Bz%7D%5Cright)" alt="Fuse $(\mathbf{a}, \mathbf{b})=\mathbf{z} \odot \mathbf{a}+(1-\mathbf{z}) \odot \mathbf{b}$\\
$\mathbf{z}=\sigma\left(\mathbf{W}_{z}[\mathbf{a} ; \mathbf{b} ; \mathbf{a} \odot \mathbf{b} ; \mathbf{a}-\mathbf{b}]+\mathbf{b}_{z}\right)" />
    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bv%7D%5E%7Bk%7D%3D%5Coperatorname%7BGRU%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bv%7D%5E%7Bk-1%7D%2C%20%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B(v)%7D%7D%5E%7Bk%7D%5Cright)" alt="\mathbf{h}_{v}^{k}=\operatorname{GRU}\left(\mathbf{h}_{v}^{k-1}, \mathbf{h}_{\mathcal{N}_{(v)}}^{k}\right)" />

* Handling multi-relational graphs: Following two possible ways
    * Levi graph transformation, where each edge is converted into a node. So, it will result a bipartate graph.
    * Gated message passing with edge information 
    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7B%5Cmathfrak%7BN%7D_%7B%5Cdashv(v)%7D%7D%5E%7Bk%7D%3D%5Coperatorname%7BAVG%7D%5Cleft(%5Cleft%5C%7B%5Cmathbf%7Bh%7D_%7Bv%7D%5E%7Bk-1%7D%5Cright%5C%7D%20%5Ccup%5Cleft%5C%7Bf%5Cleft(%5Cleft%5B%5Cmathbf%7Bh%7D_%7Bu%7D%5E%7Bk-1%7D%20%3B%20%5Cmathbf%7Be%7D_%7Bu%20v%7D%5Cright%5D%5Cright)%2C%20%5Cforall%20u%20%5Cin%20%5Cmathcal%7BN%7D_%7B%5Cdashv(v)%7D%5Cright%5C%7D%5Cright)%5C%5C%0A%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cvdash(v)%7D%7D%5E%7Bk%7D%3D%5Coperatorname%7BAVG%7D%5Cleft(%5Cleft%5C%7B%5Cmathbf%7Bh%7D_%7Bv%7D%5E%7Bk-1%7D%5Cright%5C%7D%20%5Ccup%5Cleft%5C%7Bf%5Cleft(%5Cleft%5B%5Cmathbf%7Bh%7D_%7Bu%7D%5E%7Bk-1%7D%20%3B%20%5Cmathbf%7Be%7D_%7Bu%20v%7D%5Cright%5D%2C%20%5Cforall%20u%20%5Cin%20%5Cmathcal%7BN%7D_%7B%5Cvdash(v)%7D%5Cright%5C%7D%5Cright)%5Cright." alt="\mathbf{h}_{\mathfrak{N}_{\dashv(v)}}^{k}=\operatorname{AVG}\left(\left\{\mathbf{h}_{v}^{k-1}\right\} \cup\left\{f\left(\left[\mathbf{h}_{u}^{k-1} ; \mathbf{e}_{u v}\right]\right), \forall u \in \mathcal{N}_{\dashv(v)}\right\}\right)\\
\mathbf{h}_{\mathcal{N}_{\vdash(v)}}^{k}=\operatorname{AVG}\left(\left\{\mathbf{h}_{v}^{k-1}\right\} \cup\left\{f\left(\left[\mathbf{h}_{u}^{k-1} ; \mathbf{e}_{u v}\right], \forall u \in \mathcal{N}_{\vdash(v)}\right\}\right)\right." />

**Results**
* Ablation study on number of hops for GNN was also carried out.
* It has shown significant boost in BLEU score for question generation from KG on two dataset, WQ (WebQuestions) and PQ (PathQuestions)

