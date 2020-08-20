## Towards Transparent and Explainable Attention Models
### Mohankumar, Nema, Narasimhan, Mitesh Khapra, Balaji Vasan Srinivasan, Balaraman Ravindran 
### IIT Madras
### ACL 2020


**Whats New** This paper brings out reason behind why attentions mechanism are not faithful and plausible, and address this issue by introducing diversity in hidden representation

**Key Concepts**
* Attention distribution is considered to be "faithful" if higher attention weights implies a greater impact on model's predition.

* It is considered "plausible" if it provides human understandable justification for model's prediction.

* Conicity: As model takes sum of attention weighted hidden representations. Where attention weights are positive.  It suffers from conicity, where in it gets struct in a particular conical regition. Where there is higher concity, attention weights would cease to mean.

* Key Idea: Make each subsequent hidden representation as diverse as it can be. by subtracting a vector component projected on mean of all previous hidden vectors. 

**How it works** 
* Four different tasks (Binary Text Classification, NLI, Paraphrase detection, Question Answering) and several different datasets are considered. Few tasks require to operate on two sentences.

* LSTM model works with attention as follow:

    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0A%5Cmathbf%7Bh%7D_%7Bt%7D%5E%7Bp%7D%3D%5Coperatorname%7BLSTM%7D_%7BP%7D%5Cleft(e%5Cleft(w_%7Bt%7D%5E%7Bp%7D%5Cright)%2C%20%5Cmathbf%7Bh%7D_%7Bt-1%7D%5E%7Bp%7D%5Cright)%20%5Cquad%20%5Cforall%20t%20%5Cin%5B1%2C%20m%5D%20%5C%5C%0A%5Cmathbf%7Bh%7D_%7Bt%7D%5E%7Bq%7D%3D%5Coperatorname%7BLSTM%7D_%7BQ%7D%5Cleft(e%5Cleft(w_%7Bt%7D%5E%7Bq%7D%5Cright)%2C%20%5Cmathbf%7Bh%7D_%7Bt-1%7D%5E%7Bq%7D%5Cright)%20%5Cquad%20%5Cforall%20t%20%5Cin%5B1%2C%20n%5D%5C%5C%0A%5Ctilde%7B%5Calpha%7D_%7Bt%7D%3D%5Cmathbf%7Bv%7D%5E%7BT%7D%20%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7B1%7D%20%5Cmathbf%7Bh%7D_%7Bt%7D%5E%7Bp%7D%2B%5Cmathbf%7BW%7D_%7B2%7D%20%5Cmathbf%7Bh%7D_%7Bn%7D%5E%7Bq%7D%2B%5Cmathbf%7Bb%7D%5Cright)%20%5Cquad%20%5Cforall%20t%20%5Cin%5B1%2C%20m%5D%20%5C%5C%0A%5Calpha_%7Bt%7D%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Ctilde%7B%5Calpha%7D_%7Bt%7D%5Cright)%20%5C%5C%0A%5Cmathbf%7Bc%7D_%7B%5Calpha%7D%3D%5Csum_%7Bt%3D1%7D%5E%7Bm%7D%20%5Calpha_%7Bt%7D%20%5Cmathbf%7Bh%7D%5E%7Bp%7D_t%20%5C%5C%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
\mathbf{h}_{t}^{p}=\operatorname{LSTM}_{P}\left(e\left(w_{t}^{p}\right), \mathbf{h}_{t-1}^{p}\right) \quad \forall t \in[1, m] \\
\mathbf{h}_{t}^{q}=\operatorname{LSTM}_{Q}\left(e\left(w_{t}^{q}\right), \mathbf{h}_{t-1}^{q}\right) \quad \forall t \in[1, n]\\
\tilde{\alpha}_{t}=\mathbf{v}^{T} \tanh \left(\mathbf{W}_{1} \mathbf{h}_{t}^{p}+\mathbf{W}_{2} \mathbf{h}_{n}^{q}+\mathbf{b}\right) \quad \forall t \in[1, m] \\
\alpha_{t}=\operatorname{softmax}\left(\tilde{\alpha}_{t}\right) \\
\mathbf{c}_{\alpha}=\sum_{t=1}^{m} \alpha_{t} \mathbf{h}^{p}_t \\
\end{array}" />

* Conicity is the average consine similarity of each vector from its mean. 

    <img src="https://i.upmath.me/svg/%5Coperatorname%7BATM%7D%5Cleft(%5Cmathbf%7Bv%7D_%7Bi%7D%2C%20%5Cmathbf%7BV%7D%5Cright)%3D%5Coperatorname%7Bcosine%7D%5Cleft(%5Cmathbf%7Bv%7D_%7Bi%7D%2C%20%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_%7Bj%3D1%7D%5E%7Bm%7D%20%5Cmathbf%7Bv%7D_%7Bj%7D%5Cright)%5C%5C%0A%5Coperatorname%7Bconicity%7D(%5Cmathbf%7BV%7D)%3D%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%20%5Coperatorname%7BATM%7D%5Cleft(%5Cmathbf%7Bv%7D_%7Bi%7D%2C%20%5Cmathbf%7BV%7D%5Cright)" alt="\operatorname{ATM}\left(\mathbf{v}_{i}, \mathbf{V}\right)=\operatorname{cosine}\left(\mathbf{v}_{i}, \frac{1}{m} \sum_{j=1}^{m} \mathbf{v}_{j}\right)\\
\operatorname{conicity}(\mathbf{V})=\frac{1}{m} \sum_{i=1}^{m} \operatorname{ATM}\left(\mathbf{v}_{i}, \mathbf{V}\right)" />

* Diversity in hidden representation is introduced in following way after each sequential step in LSTM.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Coverline%7B%5Cmathbf%7Bh%7D%7D_%7Bt%7D%20%26%3D%5Csum_%7Bi%3D1%7D%5E%7Bt-1%7D%20%5Cmathbf%7Bh%7D_%7Bi%7D%20%5C%5C%0A%5Cmathbf%7Bh%7D_%7B%5Cmathbf%7Bt%7D%7D%20%26%3D%5Chat%7B%5Cmathbf%7Bh%7D%7D_%7Bt%7D-%5Cfrac%7B%5Chat%7B%5Cmathbf%7Bh%7D%7D_%7Bt%7D%5E%7BT%7D%20%5Coverline%7B%5Cmathbf%7Bh%7D%7D_%7Bt%7D%7D%7B%5Coverline%7B%5Cmathbf%7Bh%7D%7D_%7Bt%7D%5E%7BT%7D%20%5Coverline%7B%5Cmathbf%7Bh%7D%7D_%7Bt%7D%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\overline{\mathbf{h}}_{t} &amp;=\sum_{i=1}^{t-1} \mathbf{h}_{i} \\
\mathbf{h}_{\mathbf{t}} &amp;=\hat{\mathbf{h}}_{t}-\frac{\hat{\mathbf{h}}_{t}^{T} \overline{\mathbf{h}}_{t}}{\overline{\mathbf{h}}_{t}^{T} \overline{\mathbf{h}}_{t}}
\end{aligned}" />

    * Which is illustrated in the following figure

    <p align="center">
        <img width=600 src="images/diversity_attention_1.png">
        <em>Source: Author</em>
        </p>

**Experiments and Results**
* Hypothesis 1: Tokens are removed based on their attention weights, and check when does the decision flips.

    <p align="center">
        <img width=600 src="images/diversity_attention_experiments_flip.png">
        <em>Source: Author</em>
        </p>

    * As can be seen, diversity models are doing much better to identity important tokens, so decision gets flipped as early as possible.

* Hypothesis 2: How conicity is reduced, and not at the cost of impact on accuracy.

     <p align="center">
        <img width=600 src="images/diversity_attention_experiments_conicity.png">
        <em>Source: Author</em>
        </p>
    * As can be seen, Conicity goes down multiple times, and there is not much impact on accuracy. 

* Hypothesis 3: How results would be impacted if attention weights are permutated randomly. 

    <p align="center">
        <img width=600 src="images/diversity_attention_experiments_permutations.png">
        <em>Source: Author</em>
        </p>    

* Hypotheis 4: Comparision with rationales, where rational means minimum set of words which required to make decisions. So, how rationale length and rational attention weights compares with vanilla LSTM and diverse LSTM

    <p align="center">
        <img width=600 src="images/diversity_attention_experiments_rationale.png">
        <em>Source: Author</em>
        </p> 
    
* Hypotheis 5: Comparison of pearson correlation and Jensen Shannon divergence between gradient based importance and attention weights

    <p align="center">
        <img width=600 src="images/diversity_attention_experiments_gradients_weights.png">
        <em>Source: Author</em>
        </p> 

* Hypotheis 6: How diversity mechanism avoid unnceccesary weights to punctuation etc.
    * It is observed that the attention given to punctuation marks is significantly reduced from 28.6%, 34.0% and 23.0% in the vanilla LSTM to 3.1%, 13.8% and 3.4% in the Diversity LSTM on the Yelp, Amazon and QQP datasets respectively.

* Hypotheis 7: How human compare attentions weights of vanilla and diversity LSTM across overall plausibility and faithfulness, completeness, and correctness. 
    * Around 200 samples taken, each sample was reviewed by 3 humans, and majority vote was taken.
    * Diversity model outperformed vanilla significantly over all these three dimensions.

**Reflection**
* This is a simple but profound technique can helps in interpretability and attribution
* Need to see how it can be extended to transforerms model as well? How much conicity problem lies in transformer architecture, and how diversity can be applied. Just on the last layer, or at each layer etc.

















