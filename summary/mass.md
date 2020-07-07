## MASS: Masked Sequence to Sequence Pre-training for Language Generation
### Kaitao Song, Xu Tan, Tao Qin, Jianfeng Lu, Tie-Yan Liu
### ICML 2019, Mircosoft,

* MASS is sequence to sequence, encoder decoder architecture. Where, encoder takes masked sequnece as input, and decoder predicts masked tokens.

* MASS makes following design choices:
    * By predicting masked tokens, forces encoder to learn contexual representation for masked tokens
    * By masking input tokens in decoder, it ensure decoder leverage encoder information for prediction
    * Ablation study proves effectiveness of both these decisions, i.e. 
        * masking a sequence vs discrete masking
        * maksing input unmasked tokens in decoder vs not masking them
    * Also, author performed compartive analysis to find optimal value of k, fraction of tokens to be masked, and it found out that
        * k between 50% to 70% brings best peplexity
        * k about 50% brings optimal downstream task performance
        * Author also gives a possible explanation, that 50% creates a better balance between encoder and decoder
    * MASS has produced better results for downstream tasks like unsupervised NMT (leveraging back translation), summarisation,  and conversational response generation.

* Author also makes a point that under specific parameter selections, BERT and GPT are both special cases of MASS.
    * Softmax in BERT just leveraging encoder representation, is similar to MASS using encoder representation only, and masking out all input tokens in decoder, when k = 1 (where k is number of tokens to be masked out)
    * when k = m, all the tokens are masked out, and it becomes a standard language model like GPT. Where it majorly rely on decoder state.

* Following figures captures illutration of MASS and its special cases leading to BERT and GPT

    <p align="center">
        <img width=600 src="images/mass1.png">
        <em>Source: Author</em>
        </p>

     <p align="center">
        <img width=600 src="images/mass2.png">
        <em>Source: Author</em>
        </p>
