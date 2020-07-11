## ALBERT: A lite BERT for self-supervised learning of language representations, Zenzhong Lan, Mingada Chen, 2020


* Is having better NLP model is as easy as having large models? 
* Memory limitation of hardware and training time is bottleneck trainig large models. 
* Albert proposes three innovations, which includes, two parameters reduction techniques, and a modification to loss function:
    * ### N-gram masking 
        * with probablity decayes with larger n.

    * ### Factorized Embedding Parameterization
        * Generally Langauge Models have large vocabolary, and hence its parameters are V x H, where H is also first hidden layer size and as well embedding size. Embeddings are supposed to be context independent and hidden layers are supposed to add context dependent part to it. Embeddings are factorised, so parameters reduces from O(V x H) is factorized into O((V x E) + (E x H)), where H >> E. 
        
            E of 128 size gave a better results compared to others under "all shared parameters" settings.

    * ### Cross-layer Parameters Sharing

        * Ablation study with four cases, i.e. no-sharing, shared-FFN, shared-attn, and all-shared have been evaluated. All-shared experiment reduces parameters significantly, but also hurts performance.
        * All-shared is less hurt for embedding size of 128 compared to 768. 


    * ### Sentence Order Prediction
        * Three experiemtal condations have been studied for inter-sentence loss: None, NSP, and SOP. It is interesting to note that NSP does not give any discriminative power to SOP, however SOP does perform well on NSP too.

    * ### Dropuout removal
        * Since there are parameters sharing, model did not get overfit even after 1M steps, so study was carried out to remove dropout. That gave improvement on MLM loss as well as downstream tasks.

    * ### Ensembles
        * Ensembles models based on candidate models which are finetuned for task specific from checkpoints from different training points. 


* ALBERT model has carried out experiments on GLUE, SQUAD and RACE.


* Important References:
    * Gradient checkpointing to reduce memory requirements to be sublinear at the cost of extra forward pass, Chen et al, 2016
    * Reproduction of each layer's activation from next layer without storing intermediate activations. Gomez et al, 2017.