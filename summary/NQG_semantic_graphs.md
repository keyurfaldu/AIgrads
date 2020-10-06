## Semantic Graphs for Generating Deep Questions
### Liangming Pan, Yuxi Xie, Yansong Feng, Tat-Seng Chua, Min-Yen Kan
### ACL 2020 [[arXiv](https://arxiv.org/abs/2004.12704)] 

**Whats Unique**
This paper presents a technique for Deep Question Generation. It fuses document level and semantic graph level representations, and generate questions using attention mechanism. It has dual objective of content selection and question construction.

**How It Works**
    <p align="center">
    <img width=600 src="images/DQG_examples.png">
    <em>Source: Author</em>
    </p>

The architecture diagram for the DQG can be seen as below:
    <p align="center">
    <img width=600 src="images/DQG_architecture.png">
    <em>Source: Author</em>
    </p>

* Problem statement
Given the document D and the answer A, the objective is to generate a question Q, that satisfies:

    <img src="https://i.upmath.me/svg/%5Coverline%7B%5Cmathcal%7BQ%7D%7D%3D%5Carg%20%5Cmax%20_%7B%5Cmathcal%7BQ%7D%7D%20P(%5Cmathcal%7BQ%7D%20%5Cmid%20%5Cmathcal%7BD%7D%2C%20%5Cmathcal%7BA%7D)" alt="\overline{\mathcal{Q}}=\arg \max _{\mathcal{Q}} P(\mathcal{Q} \mid \mathcal{D}, \mathcal{A})" />

* Semantic Graph Construction
    * SRL based graph
    * Dependency parse tree graph

* Semantic Enriched Document Representations
    * Document Encoding
        * D = [w1, · · · , wl]
        * X_D = [x1, · · · , xl]
        * x_i = [x_i->; x_i<-]

    * Node Initialisation
        * G = (V, E)
        * V = {v_i}_i=1:Nv
        * E = {e_k}_k=1:Ne
        * Each node of the graph is a text span in document involving neighbour words. 
        * Initial representation of node is obtained by computing word to node attention. 
        * Document encoding: d_D in both direction
        * <img src="https://i.upmath.me/svg/%5Cleft%5C%7Bw_%7Bm_%7Bv%7D%7D%2C%20%5Ccdots%2C%20w_%7Bj%7D%2C%20%5Ccdots%2C%20w_%7Bn_%7Bv%7D%7D%5Cright%5C%7D%24%20in%20%24v%24%20as%20follows%5C%5C" alt="\left\{w_{m_{v}}, \cdots, w_{j}, \cdots, w_{n_{v}}\right\}$ in $v$ as follows\\" />
        * <img src="https://i.upmath.me/svg/%0A%5Cbeta_%7Bj%7D%5E%7Bv%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(%5Coperatorname%7BAttn%7D%5Cleft(%5Cmathbf%7Bd%7D_%7B%5Cmathcal%7BD%7D%7D%2C%20%5Cmathbf%7Bx%7D_%7Bj%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bk%3Dm_%7Bn%7D%7D%5E%7Bn_%7Bv%7D%7D%20%5Cexp%20%5Cleft(%5Cmathbf%7BA%7D%20%5Coperatorname%7Bttn%7D%5Cleft(%5Cmathbf%7Bd%7D_%7B%5Cmathcal%7BD%7D%7D%2C%20%5Cmathbf%7Bx%7D_%7Bk%7D%5Cright)%5Cright)%7D%0A" alt="
\beta_{j}^{v}=\frac{\exp \left(\operatorname{Attn}\left(\mathbf{d}_{\mathcal{D}}, \mathbf{x}_{j}\right)\right)}{\sum_{k=m_{n}}^{n_{v}} \exp \left(\mathbf{A} \operatorname{ttn}\left(\mathbf{d}_{\mathcal{D}}, \mathbf{x}_{k}\right)\right)}
" />
        * <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bv%7D%5E%7B0%7D%3D%5Csum_%7Bj%3Dm_%7Bv%7D%7D%5E%7Bn_%7Bv%7D%7D%20%5Cbeta_%7Bj%7D%5E%7Bv%7D%20%5Cmathbf%7Bx%7D_%7Bj%7D" alt="\mathbf{h}_{v}^{0}=\sum_{j=m_{v}}^{n_{v}} \beta_{j}^{v} \mathbf{x}_{j}" />
    
        * In esscence, each node of the graph would have multiple words, attention for each of those word would be computed in context of whole document embeddings. And, node represenation would be the weighted embedding of those words.

    * Graph Encoding (Att-GGNN) - Attention based gated graph neural network
        * Represeantions based on incoming edges, and outgoing edges, weighted by attentions between nodes, and also weighted by the type of the edge between nodes is computed as follow:

        * <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cvdash(i)%7D%7D%5E%7B(k)%7D%3D%5Csum_%7Bv_%7Bj%7D%20%5Cin%20%5Cmathcal%7BN%7D_%7B%5Cvdash(i)%7D%7D%20%5Calpha_%7Bi%20j%7D%5E%7B(k)%7D%20%5Cmathbf%7BW%7D%5E%7Bt_%7Be_%7Bi%20j%7D%7D%7D%20%5Cmathbf%7Bh%7D_%7Bj%7D%5E%7B(k)%7D%5C%5C%0A%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cdashv(i)%7D%7D%5E%7B(k)%7D%3D%5Csum_%7Bv_%7Bj%7D%20%5Cin%20%5Cmathcal%7BN%7D_%7B%5Cdashv(i)%7D%7D%20%5Calpha_%7Bi%20j%7D%5E%7B(k)%7D%20%5Cmathbf%7BW%7D%5E%7Bt_%7Be%20j%20i%7D%7D%20%5Cmathbf%7Bh%7D_%7Bj%7D%5E%7B(k)%7D" alt="\mathbf{h}_{\mathcal{N}_{\vdash(i)}}^{(k)}=\sum_{v_{j} \in \mathcal{N}_{\vdash(i)}} \alpha_{i j}^{(k)} \mathbf{W}^{t_{e_{i j}}} \mathbf{h}_{j}^{(k)}\\
\mathbf{h}_{\mathcal{N}_{\dashv(i)}}^{(k)}=\sum_{v_{j} \in \mathcal{N}_{\dashv(i)}} \alpha_{i j}^{(k)} \mathbf{W}^{t_{e j i}} \mathbf{h}_{j}^{(k)}" />

        * Where, attention between two nodes are computed as below:
    
        <img src="https://i.upmath.me/svg/%5Calpha_%7Bi%20j%7D%5E%7B(k)%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(%5Coperatorname%7BAttn%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B(k)%7D%2C%20%5Cmathbf%7Bh%7D_%7Bj%7D%5E%7B(k)%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bt%20%5Cin%20%5Cmathcal%7BN%7D_%7B(i)%7D%7D%20%5Cexp%20%5Cleft(%5Coperatorname%7BAttn%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B(k)%7D%2C%20%5Cmathbf%7Bh%7D_%7Bt%7D%5E%7B(k)%7D%5Cright)%5Cright)%7D" alt="\alpha_{i j}^{(k)}=\frac{\exp \left(\operatorname{Attn}\left(\mathbf{h}_{i}^{(k)}, \mathbf{h}_{j}^{(k)}\right)\right)}{\sum_{t \in \mathcal{N}_{(i)}} \exp \left(\operatorname{Attn}\left(\mathbf{h}_{i}^{(k)}, \mathbf{h}_{t}^{(k)}\right)\right)}" />

        * Hiddent state after k-th transition is as follow:

        <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B(k%2B1)%7D%3D%5Coperatorname%7BGRU%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B(k)%7D%2C%5Cleft%5B%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cvdash%7D(i)%7D%5E%7B(k)%7D%20%3B%20%5Cmathbf%7Bh%7D_%7B%5Cmathcal%7BN%7D_%7B%5Cdashv(i)%7D%7D%5E%7B(k)%7D%5Cright%5D%5Cright)" alt="\mathbf{h}_{i}^{(k+1)}=\operatorname{GRU}\left(\mathbf{h}_{i}^{(k)},\left[\mathbf{h}_{\mathcal{N}_{\vdash}(i)}^{(k)} ; \mathbf{h}_{\mathcal{N}_{\dashv(i)}}^{(k)}\right]\right)" />

    * Fusing graph and document represeantions. It uses a matching strategy where a finest granular node in graph which comaintains the document word is selected.
* Joint Task Question Generation

    * Sementic enriched encoded representations as the attention memomry to generate the output sequence. 
    * Decoder hidden state is initialised with answer embeddings
    * At each step model learns to generate
        * Context vector c_t from semantic enriched encoded representations
        * Decoding state s_t
        * Copying probability is computed based on c_t, s_t, and y_t-1
        * Copyting probability to generate word from vocabolory or from document inputs
        * Coverage vector - to penalise attending over same locations of input documents.
    * Content selection task specific layer as multi task training.

* Evaluation
    * BLEU, ROUGE, METEOR scores
    * Human evaluations with three dimensions, fluency, relevance, and complexity.

    <p align="center">
    <img width=600 src="images/DQG_results.png">
    <em>Source: Author</em>
    </p>

    * Also, Ablation study for design decisions.



