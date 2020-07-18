## ON IDENTIFIABILITY IN TRANSFORMERS

### Gino Brunner, Yang Liu, Damian Pascual, Oliver Richter, Massimiliano Ciaramita, Roger Wattenhofer

### Google Research, ICLR, 2020

**Whats New** This paper further deepen understanding of attention weights, and contextual embeddings. It comes up with more reliable attention weights for better interpretibility. Further, it demonstrate tokens are better identifiable with cosine similarity, and dive into what contributes to contextual embeddings and what is lost as part of it.

**Key Concepts**
* Effective Attention:
    * Mathematical proof on how left null space of T, LN(T)can be added into Attention matrix and it would still produce same outcomes.

    * <img src="https://i.upmath.me/svg/%5Ctext%20%7B%20Attention%20%7D(%5Cboldsymbol%7BQ%7D%2C%20%5Cboldsymbol%7BK%7D%2C%20%5Cboldsymbol%7BV%7D)%20%5Cboldsymbol%7BH%7D%3D%5Cboldsymbol%7BA%7D%20%5Cboldsymbol%7BE%7D%20%5Cboldsymbol%7BW%7D%5E%7BV%7D%20%5Cboldsymbol%7BH%7D%3D%5Cboldsymbol%7BA%7D%20%5Cboldsymbol%7BT%7D" alt="\text { Attention }(\boldsymbol{Q}, \boldsymbol{K}, \boldsymbol{V}) \boldsymbol{H}=\boldsymbol{A} \boldsymbol{E} \boldsymbol{W}^{V} \boldsymbol{H}=\boldsymbol{A} \boldsymbol{T}" />


    * <img src="https://i.upmath.me/svg/%5Cboldsymbol%7BW%7D%5E%7BV%7D%20%5Cin%20%5Cmathbb%7BR%7D%5E%7Bd%20%5Ctimes%20d_%7Bv%7D%7D%2C%20%5Cboldsymbol%7BV%7D%3D%5Cboldsymbol%7BE%7D%20%5Cboldsymbol%7BW%7D%5E%7BV%7D%2C%20%5Cboldsymbol%7BT%7D%3D%5Cboldsymbol%7BE%7D%20%5Cboldsymbol%7BW%7D%5E%7BV%7D%20%5Cboldsymbol%7BH%7D" alt="\boldsymbol{W}^{V} \in \mathbb{R}^{d \times d_{v}}, \boldsymbol{V}=\boldsymbol{E} \boldsymbol{W}^{V}, \boldsymbol{T}=\boldsymbol{E} \boldsymbol{W}^{V} \boldsymbol{H}" />

    * LN(T) would be non empty if rank of matrix T is lesser than sequence_legth, and that would be the case when sequence_length is greater than dimensions of attention heads. Which is 64 in BERT.

    * Author propose to remove part of A, which is because of LN(T), to produce effective attention
    <img src="https://i.upmath.me/svg/%5Cboldsymbol%7BA%7D%5E%7B%5Cperp%7D%3D%5Cboldsymbol%7BA%7D-%5Ctext%20%7B%20Projection%20%7D_%7B%5Cmathrm%7BLN%7D(T)%7D%20%5Cboldsymbol%7BA%7D" alt="\boldsymbol{A}^{\perp}=\boldsymbol{A}-\text { Projection }_{\mathrm{LN}(T)} \boldsymbol{A}" />


    * They demonstrate that,
        * Pearson coefficient of attention weights vs effective attention goes down when sequence length increases beyond 64.
        * spike in attention weights of "SEP" (in paper what Bert Looks At?) tokens can be reduced to a normal level because of this notion. 

    <p align="center">
        <img width=600 src="images/effective_attention.png">
        <em>Source: Author</em>
        </p>

* Token Identifiability
    * Can we retrive original token using token's contextual weight after layer l by applying lienar transform and nearest neighbour operation?

    <p align="center">
        <img width=600 src="images/identifiability.png">
        <em>Source: Author</em>
        </p>

    * Above figure demonstrates that "cosine similarity" is better embedded in contextual embeddings, and as layer deepens, identifiability drops because of more mixture of contextual information.

* Token Mixing
    * Contribution of the same input token drops in subsequent layers, and how 30% of tokens becomes no more main contributors of their corresponding contextual embeddings. Figure below:

     <p align="center">
        <img width=600 src="images/token_mixing.png">
        <em>Source: Author</em>
        </p>

    * Relative contribution of farther neighbours increases deeper layers, and total contibution of neighbours follows normal distributions with mean at local. Self explanatory figure below:

    
     <p align="center">
        <img width=600 src="images/neighbours_contribution.png">
        <em>Source: Author</em>
        </p>


* Overall, this paper would contribute to
    * Actually measure contribution of each word to other word
    * Also, ignited, by collapsing left and right transformation matrix can inference be reduced to just two matrix product?


