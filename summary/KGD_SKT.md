## SEQUENTIAL LATENT KNOWLEDGE SELECTION FOR KNOWLEDGE-GROUNDED DIALOGUE
### Byeongchang Kim, Jaewoo Ahn, Gunhee Kim
### Seoul National University
### ICLR 2020

**Whats New** This paper focus on "knowledge selection" to improve multi turn knowledge grounded dialogue. It presents the model named "Sequential Knowledge Transformer" can keep track of prior and posterior distribution over knowledge. 

**Underlying Task** Knowledge grounded task of Wizard of Wikipedia can be seen in below figure.

<p align="center">
    <img width=600 src="images/KGD_SKT_wizard.png">
    <em>Source: Author</em>
    </p>

Wizard is expected to be both knowledgable and engaging in conversation.

**How It Works**

* Graphical representation of Sequential Knowledge Transformer can be seen as below:

<p align="center">
    <img width=600 src="images/KGD_SKT_illustration.png">
    <em>Source: Author</em>
    </p>

* Notations:
    * 1 ≤ t ≤ T to iterate over dialogue turns
    * 1 ≤ m ≤ M and 1 ≤ n ≤ N to respectively for utternance of apperantice and wizard
    * 1 ≤ l ≤ L to denote knowledge sentences in the pool
    * Hence, 
    * x1, ..., xt: utterances from apprentice x
    * y1, ..., yt: utterances from wizard y
    * k1, ..., kt: the knowledge pool, where kt = { k_t,l } for l = 1,..,L

* Sentences are encoded using BERT average pooling
    * uttenrence y^t-1 is encoded as h_y^t-1
    * apprentice-wizard utternence pair h_xy^t = [h_x^t, h_y^t], and GRU layer represents that as d_xy^t = GRU_dialog(d_xy^t-1, h_xy^t)

        <img src="https://i.upmath.me/svg/p%5Cleft(%5Cmathbf%7By%7D%5E%7Bt%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5E%7B%5Cleq%20t%7D%2C%20%5Cmathbf%7By%7D%5E%7B%3Ct%7D%5Cright)%20%5Capprox%20%5Cprod_%7Bi%3D1%7D%5E%7Bt-1%7D%20%5Csum_%7B%5Cmathbf%7Bk%7D%5E%7Bi%7D%7D%20q_%7B%5Cphi%7D%5Cleft(%5Cmathbf%7Bk%7D%5E%7Bi%7D%5Cright)%5Cleft(%5Csum_%7B%5Cmathbf%7Bk%7D%5E%7Bt%7D%7D%20p_%7B%5Ctheta%7D%5Cleft(%5Cmathbf%7By%7D%5E%7Bt%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5E%7B%5Cleq%20t%7D%2C%20%5Cmathbf%7By%7D%5E%7B%3Ct%7D%2C%20%5Cmathbf%7Bk%7D%5E%7Bt%7D%5Cright)%20%5Cpi_%7B%5Ctheta%7D%5Cleft(%5Cmathbf%7Bk%7D%5E%7Bt%7D%5Cright)%5Cright)" alt="p\left(\mathbf{y}^{t} \mid \mathbf{x}^{\leq t}, \mathbf{y}^{&lt;t}\right) \approx \prod_{i=1}^{t-1} \sum_{\mathbf{k}^{i}} q_{\phi}\left(\mathbf{k}^{i}\right)\left(\sum_{\mathbf{k}^{t}} p_{\theta}\left(\mathbf{y}^{t} \mid \mathbf{x}^{\leq t}, \mathbf{y}^{&lt;t}, \mathbf{k}^{t}\right) \pi_{\theta}\left(\mathbf{k}^{t}\right)\right)" /> 

    * Where, 
    * q_phi is posterior knowledge from turn 1 to t-1
    * pi_theta is prior knowledge at turn t, estimated based on x_<=t, and y_<t

        <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0A%5Cpi_%7B%5Ctheta%7D%5Cleft(%5Cmathbf%7Bk%7D%5E%7Bt%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5E%7B%5Cleq%20t%7D%2C%20%5Cmathbf%7By%7D%5E%7B%3Ct%7D%2C%20%5Cmathbf%7Bk%7D_%7Bs%7D%5E%7B%5Cleq%20t-1%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7Bq%7D_%7Bp%20r%20i%20o%20r%7D%5E%7Bt%7D%5Cleft%5B%5Cmathbf%7Bh%7D_%7Bk%7D%5E%7Bt%2C%201%7D%2C%20%5Cldots%2C%20%5Cmathbf%7Bh%7D_%7Bk%7D%5E%7Bt%2C%20L%7D%5Cright%5D%5E%7B%5Ctop%7D%5Cright)%20%5Cin%20%5Cmathbb%7BR%7D%5E%7BL%7D%20%5C%5C%0Aq_%7B%5Cphi%7D%5Cleft(%5Cmathbf%7Bk%7D%5E%7Bt%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5E%7B%5Cleq%20t%7D%2C%20%5Cmathbf%7By%7D%5E%7B%5Cleq%20t%7D%2C%20%5Cmathbf%7Bk%7D_%7Bs%7D%5E%7B%5Cleq%20t-1%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7Bq%7D_%7Bp%20o%20s%20t%7D%5E%7Bt%7D%5Cleft%5B%5Cmathbf%7Bh%7D_%7Bk%7D%5E%7Bt%2C%201%7D%2C%20%5Cldots%2C%20%5Cmathbf%7Bh%7D_%7Bk%7D%5E%7Bt%2C%20L%7D%5Cright%5D%5E%7B%5Ctop%7D%5Cright)%20%5Cin%20%5Cmathbb%7BR%7D%5E%7BL%7D%20%5C%5C%0A%5Cmathbf%7Bq%7D_%7Bp%20r%20i%20o%20r%7D%5E%7Bt%7D%3D%5Cmathbf%7BW%7D_%7Bp%20r%20i%20o%20r%7D%5Cleft(%5Cleft%5B%5Cmathbf%7Bd%7D_%7Bx%20y%7D%5E%7Bt-1%7D%20%3B%20%5Cmathbf%7Bh%7D_%7Bx%7D%5E%7Bt%7D%20%3B%20%5Coperatorname%7BGRU%7D_%7Bh%20i%20s%20t%7D%5Cleft(%5Cmathbf%7Bd%7D_%7Bk%7D%5E%7Bt-2%7D%2C%20%5Cmathbf%7Bh%7D_%7Bk%7D%5E%7Bt-1%2C%20s%7D%5Cright)%5Cright%5D%5Cright)%20%5C%5C%0A%5Cmathbf%7Bq%7D_%7Bp%20o%20s%20t%7D%5E%7Bt%7D%3D%5Cmathbf%7BW%7D_%7Bp%20o%20s%20t%7D%5Cleft(%5Cleft%5B%5Cmathbf%7Bd%7D_%7Bx%20y%7D%5E%7Bt%7D%20%3B%20%5Coperatorname%7BGRU%7D_%7Bh%20i%20s%20t%7D%5Cleft(%5Cmathbf%7Bd%7D_%7Bk%7D%5E%7Bt-2%7D%2C%20%5Cmathbf%7Bh%7D_%7Bk%7D%5E%7Bt-1%2C%20s%7D%5Cright)%5Cright%5D%5Cright)%0A%5Cend%7Barray%7D" alt="\begin{array}{l}\pi_{\theta}\left(\mathbf{k}^{t} \mid \mathbf{x}^{\leq t}, \mathbf{y}^{&lt;t}, \mathbf{k}_{s}^{\leq t-1}\right)=\operatorname{softmax}\left(\mathbf{q}_{p r i o r}^{t}\left[\mathbf{h}_{k}^{t, 1}, \ldots, \mathbf{h}_{k}^{t, L}\right]^{\top}\right) \in \mathbb{R}^{L} \\ q_{\phi}\left(\mathbf{k}^{t} \mid \mathbf{x}^{\leq t}, \mathbf{y}^{\leq t}, \mathbf{k}_{s}^{\leq t-1}\right)=\operatorname{softmax}\left(\mathbf{q}_{p o s t}^{t}\left[\mathbf{h}_{k}^{t, 1}, \ldots, \mathbf{h}_{k}^{t, L}\right]^{\top}\right) \in \mathbb{R}^{L} \\ \mathbf{q}_{p r i o r}^{t}=\mathbf{W}_{p r i o r}\left(\left[\mathbf{d}_{x y}^{t-1} ; \mathbf{h}_{x}^{t} ; \operatorname{GRU}_{h i s t}\left(\mathbf{d}_{k}^{t-2}, \mathbf{h}_{k}^{t-1, s}\right)\right]\right) \\ \mathbf{q}_{p o s t}^{t}=\mathbf{W}_{p o s t}\left(\left[\mathbf{d}_{x y}^{t} ; \operatorname{GRU}_{h i s t}\left(\mathbf{d}_{k}^{t-2}, \mathbf{h}_{k}^{t-1, s}\right)\right]\right) \end{array}" />

    * As, we can see, prior probability is just the dot product of W_prior . [d_xy_t-1, h_x_t] . [h_k^t_1, .. h_k^t_L], where d_xy_t-1 is the result of GRU state.
    * Posterior probability is the dot product of W_posterior . [d_xy_t] . [h_k^t_1, .. h_k^t_L], where d_xy_t-1 is the result of GRU state.

    * During decoding, it uses copy mechanism to maximize the effect of selected knowledge for response generation. So, either it copies or it generate the word based on a sigmoid over a hyper parameter.

    * Training loss is combination of perplexity and KL divergence between posteriori and priori.

* Results:
    * It has achieved state of the art results in metrics - unigram F1, bigram F1 and perplexity. 







