## What Does BERT Look At? An Analysis of BERT's Attention
### Kevin Clark, Urvashi Khandelwal, Omer Levy, Christopher D. Manning

Setup:
* Extract attention maps from over 1000 random wikipedia segments
* Attending to \<SEP> token:
    * It is NOT because \<SEP> token aggregate segment level information, as \<SEP> token itself should have attended broadly, but interestingly, \<SEP> token attend to itself with more than 90% of weight.
    * Diving deep, paper proves that heads with specific function attend to \<SEP> when the function is not called for on those tokens.
    <p align="center">
    <img width=600 src="images/sep_to_sep_attention.png">
    <em>Source: Author</em>
    </p>
    * Further "Gradient-based-feature-importance" etablishes that changing attention over \<SEP> token does not impact loss function much.
    <p align="center">
    <img width=600 src="images/gradient_importance_sep.png">
    <em>Source: Author</em>
    </p>
* Probing Individual Attention Heads
    * "from" split word - average attention
    * "to" split word - sum of attention
    * Dependency Syntax:
        * Certain heads specializes in specific dependency relations. And, do achieve higher accuracy then fixed offset heuristics.
        <p align="center">
        <img width=600 src="images/attention_heads_dependency_specialisation.png">
        <em>Source: Author</em>
        </p>
    * Coreference Resolution:
        * Author proves how a specific head is doing reasonably well at coref resolution, and outperforming rule based systems. 
        <p align="center">
        <img width=600 src="images/attention_head_for_coref.png">
        <em>Source: Author</em>
        </p>
    *  Probing classifiers for graph based dependency parsers
        * How building classifer by just using attention weights, and using attention weights + glove embeddings gives reasonable prediction of dependency parsing, and almost matching structural probe which also have used internal contextual representations. 
        * Attention only probe: w_k and u_k are learned.
            <p align="center">
            <img width=600 src="images/dependency_tree_attention_only_probe.png">
            <em>Source: Author</em>
            </p>
        * Attention + Glove weights probe: W and K are learned.
            <p align="center">
            <img width=600 src="images/dependency_tree_attention_weights_probe.png">
            <em>Source: Author</em>
            </p>
        * Structural probe gives 80 UUAS score, while Attn only has given 61, and Attn + Gloves has given 71 score. 
    * Clustering Attention Heads:
        * Attention heads distance is computed based on Jensen-Shannon Divergence on attention distributions.
        * Attention heads in a layer are co-located, so their is a similarity among them. 

* Most recent work on model analysis depends on probing vector representations, or model outputs, and this paper shows intriguing results on attention maps. It should be part of toolkits for researchers to understand what nerual network learns about languages. 