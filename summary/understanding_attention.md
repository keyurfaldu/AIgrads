## Understanding Attention for Text Classification
### Xiaobing Sun and Wei Lu
### ACL 2020


**Whats New**
This paper present an analysis to understand attention mechanism, it splits attention mechanism into attention score, weights and polarity score, where attention score is absolute importance of word for a context, attention weight is relative one for the sequence, and polarity score for token's polarity towards a label. 

**Key Insights**
* Polarity would get aligned to label as part of training, so sooner positive tokens would have positive score and negative tokens would have negative score.
* Attention scores of positve tokens would be positive, and with hence higher attention weights, which will drive to positive polarity score, and label score, which would minimize loss.
* Higher lambda would bring down variance in attention scores and hence attention mechanism would reduce to pooling. 

**How it is done**
* A simplified architecture of attention mechanism is done, can be seen in the figure below.

    <p align="center">
    <img width=600 src="images/simplified_attention_architecture.png">
    <em>Source: Author</em>
    </p>

* For a context vector V, attention score is 

    <img src="https://i.upmath.me/svg/a_%7Bj%7D%3D%5Cfrac%7B%5Cboldsymbol%7Bh%7D_%7Bj%7D%5E%7B%5Ctop%7D%20%5Cboldsymbol%7BV%7D%7D%7B%5Clambda%7D" alt="a_{j}=\frac{\boldsymbol{h}_{j}^{\top} \boldsymbol{V}}{\lambda}" />

* Which is then converted to attention weights using softmax, 
    <img src="https://i.upmath.me/svg/%5Calpha_%7Bj%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(a_%7Bj%7D%5Cright)%7D%7B%5Csum_%7Bj%5E%7B%5Cprime%7D%7D%20%5Cexp%20%5Cleft(a_%7Bj%5E%7B%5Cprime%7D%7D%5Cright)%7D" alt="\alpha_{j}=\frac{\exp \left(a_{j}\right)}{\sum_{j^{\prime}} \exp \left(a_{j^{\prime}}\right)}" />

* Note, let say for task of binar classification, context would be learnt as represenation of positive class, and any positive tokens similar to tokens would have positive attention score, and hence relative higher weight.

* Attention weights would mix input sequence based on its relative importance, 

    <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Bh%7D%3D%5Csum_%7Bi%7D%20%5Calpha_%7Bj%7D%20%5Cboldsymbol%7Bh%7D_%7Bj%7D" alt="\boldsymbol{h}=\sum_{i} \alpha_{j} \boldsymbol{h}_{j}" />

* And, output of linear layer would be

    <img src="https://i.upmath.me/svg/s%3D%5Cboldsymbol%7Bh%7D%5E%7B%5Ctop%7D%20%5Cboldsymbol%7BW%7D" alt="s=\boldsymbol{h}^{\top} \boldsymbol{W}" />

* And, overall loss would be computed as follow:

    <img src="https://i.upmath.me/svg/%5Cell%3D%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_%7Bt%3D1%7D%5E%7Bm%7D%20%5Cell%5E%7B(t)%7D%3D-%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_%7Bt%3D1%7D%5E%7Bm%7D%20%5Clog%20%5Cleft(%5Csigma%5Cleft(y%5E%7B(t)%7D%20s%5E%7B(t)%7D%5Cright)%5Cright)" alt="\ell=\frac{1}{m} \sum_{t=1}^{m} \ell^{(t)}=-\frac{1}{m} \sum_{t=1}^{m} \log \left(\sigma\left(y^{(t)} s^{(t)}\right)\right)" />

    * where, if label is positive, expected polarity score woould be positive, and naturally, those positive contribution would come from positive tokens, which can be seen as below:

        <img src="https://i.upmath.me/svg/s%3D%5Csum_%7Bj%7D%20%5Calpha_%7Bj%7D%20%5Cboldsymbol%7Bh%7D_%7Bj%7D%5E%7B%5Ctop%7D%20%5Cboldsymbol%7BW%7D%3D%5Csum_%7Bj%7D%20%5Calpha_%7Bj%7D%20s_%7Bj%7D" alt="s=\sum_{j} \alpha_{j} \boldsymbol{h}_{j}^{\top} \boldsymbol{W}=\sum_{j} \alpha_{j} s_{j}" />

    * where, we can define token level polarity as 

        <img src="https://i.upmath.me/svg/s_%7Bj%7D%3D%5Cboldsymbol%7Bh%7D_%7Bj%7D%5E%7B%5Ctop%7D%20%5Cboldsymbol%7BW%7D" alt="s_{j}=\boldsymbol{h}_{j}^{\top} \boldsymbol{W}" />

**Experimental Insights**

<p align="center">
    <img width=600 src="images/attention_score_polarity.png">
    <em>Source: Author</em>
    </p>

* We can see in the above figure how polarity score is differentiated between positive, negative and neutral tokens.
* We can also obsever, those positive and negative tokens gets higher attention score, hence they would also have higher attention weights, which would lead to correct label classification, and minimizing loss.









