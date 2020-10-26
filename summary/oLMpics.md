## oLMpics - On what Language Model Pre-training Captures
### Alon Talmor, Yoav Goldberg et al. 
### The Allen Institute for AI, 
### 2020 [[arXiv](https://arxiv.org/pdf/1912.13283.pdf)]


**Whats Unique**
This paper has designed knowledge probes for 8 different knowledge tasks and comparative study framework to undederstand pre-trained LM capabilities, and learning curve with fine tuning and control tasks with no language setting. 

**Tasks Considered for Knowledge Probes**
<p align="center">
    <img width=600 src="images/oLMpics_examples.png">
    <em>Source: Author</em>
    </p>

**Methods**
* It uses MC-MLM and MC-QA method to probe models.
* MC-MLM: 
    * feed contextual representation of masked word in MC-MLM layer to predict the token l from vocaboarly
    * Take dot product of l over candidate words and take softmax to learn probability distribution.

        <img src="https://i.upmath.me/svg/l%3DF%20F_%7B%5Cmathrm%7BMLM%7D%7D%5Cleft(%5Cboldsymbol%7Bh%7D_%7Bi%7D%5Cright)%20%5Cin%20%5Cmathbb%7BR%7D%5E%7B%7C%5Cmathcal%7BV%7D%7C%7D%2C%20p%3D%5Coperatorname%7Bsoftmax%7D(m%20%5Codot%20l)" alt="l=F F_{\mathrm{MLM}}\left(\boldsymbol{h}_{i}\right) \in \mathbb{R}^{|\mathcal{V}|}, p=\operatorname{softmax}(m \odot l)" />

* MC-QA: representation by passing contextual repre
    * Given a question q and candidate answers a1, . . . , aK, we compute for each candidate answer ak representations h(k) from the input tokens “[CLS] q [SEP] ak [SEP]”.

        <img src="https://i.upmath.me/svg/l%5E%7B(k)%7D%3DF%20F_%7B%5Cmathrm%7BQA%7D%7D%5Cleft(%5Cboldsymbol%7Bh%7D_%7B1%7D%5E%7B(k)%7D%5Cright)%2C%20p%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(l%5E%7B(1)%7D%2C%20%5Cldots%2C%20l%5E%7B(K)%7D%5Cright)" alt="l^{(k)}=F F_{\mathrm{QA}}\left(\boldsymbol{h}_{1}^{(k)}\right), p=\operatorname{softmax}\left(l^{(1)}, \ldots, l^{(K)}\right)" />

**Results**
Final findings are as below for Roberta and BERT models on 8 different knowledge tasks
<p align="center">
    <img width=600 src="images/oLMpics_results.png">
    <em>Source: Author</em>
    </p>

