## Towards Generalizable Neuro-Symbolic Systems for Commonsense Question Answering
### Kaixin Ma et al. 
### COIN workshop, ACL 2019 [[arXiv](https://www.aclweb.org/anthology/D19-6003.pdf)]

**Whats New**
This paper present the knowledge ingection experiements on Option Comparison Network for commonsense question answering.

**Important Points**
* Different kinds of Knowledge Graphs would be needed based on underlying nature of data and task.
    * **Declarative commonsense** encompasses factual knowledge, e.g., ‘the sky isblue’, ‘Paris is in France’; 
    * **Taxonomic knowledge** ,e.g., ‘football players are athletes’, ‘cats are mammals’; relational knowledge, e.g., ‘the nose is partof the skull’, ‘handwriting requires a hand anda writing instrument’; 
    * **Procedural commonsense** ,which includes prescriptive knowledge, e.g., ‘oneneeds an oven before baking cakes’, ‘the electricity should be off while the switch is being repaired’
    * **Sentiment knowledge** ,e.g., ‘rushing to the hospital makes people worried’, ‘being in vacation makes people relaxed’;Metaphorical knowledge (e.g., ‘time flies’,‘raining cats and dogs’). 

**How It Works**
* It demonstrate impact of following:
    * Knowledge Injection 
    * Pretrainig on Knowledge base
* It selects two datasets for its experiments:
    * DREAM
    * CommonsenseQA
* It selects two knowledge bases for injecting different kinds of knowledge
    * ConceptNet: 21 millions edges, and 8 million nodes. It is most common semantic network for common sense
    * ATOMIC: new knowledge base focuses on procedural knowlege
* Following figure illsutrates the architecture
    <p align="center">
    <img width=600 src="images/OCNKI_illustration.png">
    <em>Source: Author</em>
    </p>
    
* Knowledge Ingection:
    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cwidetilde%7BH%7D_%7BM%7D%20%26%3DH_%7BM%7D%20%5Ccdot%20W_%7Bp%20r%20o%20j%7D%20%5C%5C%20%5Cmathcal%7BS%7D%20%26%3D%5Coperatorname%7BAtt%7D%5Cleft(H_%7BM%7D%2C%20T_%7Be%20n%20c%7D%5Cright)%20%5C%5C%20A_%7Bm%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D(%5Cmathcal%7BS%7D)%20%5Ccdot%20%5Cwidetilde%7BH%7D_%7BM%7D%20%5C%5C%20A_%7Bt%7D%3D%5Coperatorname%7Bsoftmax%7D(%5Cmathcal%7BS%7D)%20%26%20%5Ccdot%20%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathcal%7BS%7D%5E%7BT%7D%5Cright)%20%5Ccdot%20T_%7Be%20n%20c%7D%20%5C%5C%20T_%7BC%7D%3D%5Cleft%5BT_%7Be%20n%20c%7D%20%3B%20A_%7Bm%7D%5Cright.%26%5Cleft.%3B%20T_%7Be%20n%20c%7D%20%5Ccirc%20A_%7Bm%7D%20%3B%20T_%7Be%20n%20c%7D%20%5Ccirc%20A_%7Bt%7D%5Cright%5D%20%5C%5C%20T_%7Bo%20u%20t%7D%20%26%3D%5Coperatorname%7BReLU%7D%5Cleft(T_%7BC%7D%20%5Ccdot%20W_%7Ba%7D%5Cright)%20%5Cend%7Baligned%7D" alt="\begin{aligned} \widetilde{H}_{M} &amp;=H_{M} \cdot W_{p r o j} \\ \mathcal{S} &amp;=\operatorname{Att}\left(H_{M}, T_{e n c}\right) \\ A_{m} &amp;=\operatorname{softmax}(\mathcal{S}) \cdot \widetilde{H}_{M} \\ A_{t}=\operatorname{softmax}(\mathcal{S}) &amp; \cdot \operatorname{softmax}\left(\mathcal{S}^{T}\right) \cdot T_{e n c} \\ T_{C}=\left[T_{e n c} ; A_{m}\right.&amp;\left.; T_{e n c} \circ A_{m} ; T_{e n c} \circ A_{t}\right] \\ T_{o u t} &amp;=\operatorname{ReLU}\left(T_{C} \cdot W_{a}\right) \end{aligned}" />
    * As shown above, T_enc is the enocoding of dialogue, question and answer option.
    * H_M is the encoding of relevant knolwedge from knowledge base
    * H_M is projected to T_enc space
    * S similarity matrix is computed using trilinear attention between H_M and T_enc
    * Text-to-knowledge attention is computed using similarity matrix, A_m
    * Knowledge-to-text attention is computed, A_t
    * Knowledge aware T_enc is produced as T_out

* Knowledge Pre-training
    * OMCS (dataset behind ConceptNet) was used for BERT pretraining
    * COMET was used to convert ATOMIC to senstences, and used to pre-train BERT.
    
* Results are as follow:
    <p align="center">
    <img width=600 src="images/OCNKI_results.png">
    <em>Source: Author</em>
    </p>

 
