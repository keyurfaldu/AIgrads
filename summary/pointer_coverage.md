## Get To The Point: Summarization with Pointer-Generator Networks
### Abigail See, Peter J. Liu, Christopher D. Manning, 2017 
### 2017, [[arXiv](https://arxiv.org/pdf/1704.04368.pdf)] 

**Whats Unique**
This paper presents the technique for copy mechanism via pointing based on attention distribution, and avoid repetations by maintaining coverage state which penalise repeated higher attentions for the words.

**Major Contribution**
* Explicit probability to generate vs copy
* Copy mechanism by pointing.
* Coverage by avoiding repeated attention, and accomodating that in loss function.

**How It Works**

**Baseline Model (Seq2Seq with Attention)**
* Attention over hidden states in encoder, 
    * h_i is hidden state of word_i in encoder. 
    * s_t is decoder state at time t

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ae_%7Bi%7D%5E%7Bt%7D%20%26%3Dv%5E%7BT%7D%20%5Ctanh%20%5Cleft(W_%7Bh%7D%20h_%7Bi%7D%2BW_%7Bs%7D%20s_%7Bt%7D%2Bb_%7B%5Cmathrm%7Battn%7D%7D%5Cright)%20%5C%5C%0Aa%5E%7Bt%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(e%5E%7Bt%7D%5Cright)%20%5C%5C%0Ah_%7Bt%7D%5E%7B*%7D%20%26%3D%5Csum_%7Bi%7D%20a_%7Bi%7D%5E%7Bt%7D%20h_%7Bi%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
e_{i}^{t} &amp;=v^{T} \tanh \left(W_{h} h_{i}+W_{s} s_{t}+b_{\mathrm{attn}}\right) \\
a^{t} &amp;=\operatorname{softmax}\left(e^{t}\right) \\
h_{t}^{*} &amp;=\sum_{i} a_{i}^{t} h_{i}
\end{aligned}" />

*   Using context vector and decoder hidden state, the probability of vocabolary can be estiamted.

    <img src="https://i.upmath.me/svg/P_%7B%5Ctext%20%7Bvocab%20%7D%7D%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(V%5E%7B%5Cprime%7D%5Cleft(V%5Cleft%5Bs_%7Bt%7D%2C%20h_%7Bt%7D%5E%7B*%7D%5Cright%5D%2Bb%5Cright)%2Bb%5E%7B%5Cprime%7D%5Cright)%5C%5C%0AP(w)%3DP_%7B%5Cmathrm%7Bvocab%7D%7D(w)" alt="P_{\text {vocab }}=\operatorname{softmax}\left(V^{\prime}\left(V\left[s_{t}, h_{t}^{*}\right]+b\right)+b^{\prime}\right)\\
P(w)=P_{\mathrm{vocab}}(w)" />

* **Loss function** can be designed as follow:

    <img src="https://i.upmath.me/svg/%5Coperatorname%7Bloss%7D_%7Bt%7D%3D-%5Clog%20P%5Cleft(w_%7Bt%7D%5E%7B*%7D%5Cright)%5C%5C%0A%5Ctext%20%7B%20loss%20%7D%3D%5Cfrac%7B1%7D%7BT%7D%20%5Csum_%7Bt%3D0%7D%5E%7BT%7D%20%5Coperatorname%7Bloss%7D_%7Bt%7D" alt="\operatorname{loss}_{t}=-\log P\left(w_{t}^{*}\right)\\
\text { loss }=\frac{1}{T} \sum_{t=0}^{T} \operatorname{loss}_{t}" />

**Pointer Network**
* Probability of generating new word can be estimated using context vector, hidden state, and input word

    <img src="https://i.upmath.me/svg/p_%7B%5Cmathrm%7Bgen%7D%7D%3D%5Csigma%5Cleft(w_%7Bh%5E%7B*%7D%7D%5E%7BT%7D%20h_%7Bt%7D%5E%7B*%7D%2Bw_%7Bs%7D%5E%7BT%7D%20s_%7Bt%7D%2Bw_%7Bx%7D%5E%7BT%7D%20x_%7Bt%7D%2Bb_%7B%5Cmathrm%7Bptr%7D%7D%5Cright)%5C%5C%0AP(w)%3Dp_%7B%5Cmathrm%7Bgen%7D%7D%20P_%7B%5Cmathrm%7Bvocab%7D%7D(w)%2B%5Cleft(1-p_%7B%5Cmathrm%7Bgen%7D%7D%5Cright)%20%5Csum_%7Bi%3A%20w_%7Bi%7D%3Dw%7D%20a_%7Bi%7D%5E%7Bt%7D" alt="p_{\mathrm{gen}}=\sigma\left(w_{h^{*}}^{T} h_{t}^{*}+w_{s}^{T} s_{t}+w_{x}^{T} x_{t}+b_{\mathrm{ptr}}\right)\\
P(w)=p_{\mathrm{gen}} P_{\mathrm{vocab}}(w)+\left(1-p_{\mathrm{gen}}\right) \sum_{i: w_{i}=w} a_{i}^{t}" />

**Coverage Mechanism**
* Coverage score is the sum of attentions till time step t
* Deriving new attention distribution, give access to coverage information as well
* Coverage loss will penalise the attention to give repeated higher value.

 <img src="https://i.upmath.me/svg/c%5E%7Bt%7D%3D%5Csum_%7Bt%5E%7B%5Cprime%7D%3D0%7D%5E%7Bt-1%7D%20a%5E%7Bt%5E%7B%5Cprime%7D%7D%5C%5C%0Ae_%7Bi%7D%5E%7Bt%7D%3Dv%5E%7BT%7D%20%5Ctanh%20%5Cleft(W_%7Bh%7D%20h_%7Bi%7D%2BW_%7Bs%7D%20s_%7Bt%7D%2Bw_%7Bc%7D%20c_%7Bi%7D%5E%7Bt%7D%2Bb_%7B%5Cmathrm%7Battn%7D%7D%5Cright)%5C%5C%0A%5Ctext%20%7B%20covloss%20%7D_%7Bt%7D%3D%5Csum_%7Bi%7D%20%5Cmin%20%5Cleft(a_%7Bi%7D%5E%7Bt%7D%2C%20c_%7Bi%7D%5E%7Bt%7D%5Cright)" alt="c^{t}=\sum_{t^{\prime}=0}^{t-1} a^{t^{\prime}}\\
e_{i}^{t}=v^{T} \tanh \left(W_{h} h_{i}+W_{s} s_{t}+w_{c} c_{i}^{t}+b_{\mathrm{attn}}\right)\\
\text { covloss }_{t}=\sum_{i} \min \left(a_{i}^{t}, c_{i}^{t}\right)" />

**Architecture Diagram**
<p align="center">
<img width=600 src="images/pointer_coverage_architecture.png">
<em>Source: Author</em>
</p>



