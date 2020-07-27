## ERNIE: Enhanced Language Representation with Informative Entities
### Zhengyan Zhang, Xu Han, Zhiyuan Liu, Xin Jiang, Maosong Sun, Qun Liu
### ACL 2019

**Whats new** informative entities in KGs can enhance language representation with external knowledge

**How it works** 
* Architecture: ERNIE has two encoders, 
    * T-Encoder: Where, contexualised embeddings are first learnt independent of mixing KG augmentatiom 
    * K-Encoder: Information fusion happens with KG entity embeddings, which are pretrained with TransE.
    * Architecture diagram can be seen as below:

    <p align="center">
        <img width=600 src="images/ernie_architecture.png">
        <em>Source: Author</em>
        </p>

    * Token sequence {w_1, . . . , w_n}, and entity sequence {e_1, . . . , e_m}
    * Token entity alignment f(w) = e
    
        <img src="https://i.upmath.me/svg/%5Cleft%5C%7B%5Cboldsymbol%7Bw%7D_%7B1%7D%2C%20%5Cldots%2C%20%5Cboldsymbol%7Bw%7D_%7Bn%7D%5Cright%5C%7D%3D%5Coperatorname%7BT-Encoder%7D%5Cleft(%5Cleft%5C%7Bw_%7B1%7D%2C%20%5Cldots%2C%20w_%7Bn%7D%5Cright%5C%7D%5Cright)" alt="\left\{\boldsymbol{w}_{1}, \ldots, \boldsymbol{w}_{n}\right\}=\operatorname{T-Encoder}\left(\left\{w_{1}, \ldots, w_{n}\right\}\right)" />

        <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bc%7D%0A%5Cleft%5C%7B%5Cboldsymbol%7Bw%7D_%7B1%7D%5E%7Bo%7D%2C%20%5Cldots%2C%20%5Cboldsymbol%7Bw%7D_%7Bn%7D%5E%7Bo%7D%5Cright%5C%7D%2C%5Cleft%5C%7B%5Cboldsymbol%7Be%7D_%7B1%7D%5E%7Bo%7D%2C%20%5Cldots%2C%20%5Cboldsymbol%7Be%7D_%7Bn%7D%5E%7Bo%7D%5Cright%5C%7D%3D%5Ctext%7BK-Encoder%7D(%5Cleft%5Cleft%5C%7B%5Cboldsymbol%7Bw%7D_%7B1%7D%2C%20%5Cldots%2C%20%5Cboldsymbol%7Bw%7D_%7Bn%7D%5Cright%5C%7D%2C%5Cleft%5C%7B%5Cboldsymbol%7Be%7D_%7B1%7D%2C%20%5Cldots%2C%20%5Cboldsymbol%7Be%7D_%7Bm%7D%5Cright%5C%7D%5Cright)%0A%5Cend%7Barray%7D" alt="\begin{array}{c}
\left\{\boldsymbol{w}_{1}^{o}, \ldots, \boldsymbol{w}_{n}^{o}\right\},\left\{\boldsymbol{e}_{1}^{o}, \ldots, \boldsymbol{e}_{n}^{o}\right\}=\text{K-Encoder}(\left\left\{\boldsymbol{w}_{1}, \ldots, \boldsymbol{w}_{n}\right\},\left\{\boldsymbol{e}_{1}, \ldots, \boldsymbol{e}_{m}\right\}\right)
\end{array}" />

    * For token with aligned entities, information is fused as follow

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cboldsymbol%7Bh%7D_%7Bj%7D%20%26%3D%5Csigma%5Cleft(%5Ctilde%7B%5Cboldsymbol%7BW%7D%7D_%7Bt%7D%5E%7B(i)%7D%20%5Ctilde%7B%5Cboldsymbol%7Bw%7D%7D_%7Bj%7D%5E%7B(i)%7D%2B%5Ctilde%7B%5Cboldsymbol%7BW%7D%7D_%7Be%7D%5E%7B(i)%7D%20%5Ctilde%7B%5Cboldsymbol%7Be%7D%7D_%7Bk%7D%5E%7B(i)%7D%2B%5Ctilde%7B%5Cboldsymbol%7Bb%7D%7D%5E%7B(i)%7D%5Cright)%20%5C%5C%0A%5Cboldsymbol%7Bw%7D_%7Bj%7D%5E%7B(i)%7D%20%26%3D%5Csigma%5Cleft(%5Cboldsymbol%7BW%7D_%7Bt%7D%5E%7B(i)%7D%20%5Cboldsymbol%7Bh%7D_%7Bj%7D%2B%5Cboldsymbol%7Bb%7D_%7Bt%7D%5E%7B(i)%7D%5Cright)%20%5C%5C%0A%5Cboldsymbol%7Be%7D_%7Bk%7D%5E%7B(i)%7D%20%26%3D%5Csigma%5Cleft(%5Cboldsymbol%7BW%7D_%7Be%7D%5E%7B(i)%7D%20%5Cboldsymbol%7Bh%7D_%7Bj%7D%2B%5Cboldsymbol%7Bb%7D_%7Be%7D%5E%7B(i)%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\boldsymbol{h}_{j} &amp;=\sigma\left(\tilde{\boldsymbol{W}}_{t}^{(i)} \tilde{\boldsymbol{w}}_{j}^{(i)}+\tilde{\boldsymbol{W}}_{e}^{(i)} \tilde{\boldsymbol{e}}_{k}^{(i)}+\tilde{\boldsymbol{b}}^{(i)}\right) \\
\boldsymbol{w}_{j}^{(i)} &amp;=\sigma\left(\boldsymbol{W}_{t}^{(i)} \boldsymbol{h}_{j}+\boldsymbol{b}_{t}^{(i)}\right) \\
\boldsymbol{e}_{k}^{(i)} &amp;=\sigma\left(\boldsymbol{W}_{e}^{(i)} \boldsymbol{h}_{j}+\boldsymbol{b}_{e}^{(i)}\right)
\end{aligned}" />

    * For token without aligned entities, fusion happens as follow

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cboldsymbol%7Bh%7D_%7Bj%7D%20%26%3D%5Csigma%5Cleft(%5Cboldsymbol%7B%5Ctilde%20%7B%20W%20%7D%7D_%7Bt%7D%5E%7B(i)%7D%20%5Ctilde%7B%5Cboldsymbol%7Bw%7D%7D_%7Bj%7D%5E%7B(i)%7D%2B%5Ctilde%7B%5Cboldsymbol%7Bb%7D%7D%5E%7B(i)%7D%5Cright)%20%5C%5C%0A%5Cboldsymbol%7Bw%7D_%7Bj%7D%5E%7B(i)%7D%20%26%3D%5Csigma%5Cleft(%5Cboldsymbol%7BW%7D_%7Bt%7D%5E%7B(i)%7D%20%5Cboldsymbol%7Bh%7D_%7Bj%7D%2B%5Cboldsymbol%7Bb%7D_%7Bt%7D%5E%7B(i)%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
        \boldsymbol{h}_{j} &amp;=\sigma\left(\boldsymbol{\tilde { W }}_{t}^{(i)} \tilde{\boldsymbol{w}}_{j}^{(i)}+\tilde{\boldsymbol{b}}^{(i)}\right) \\
        \boldsymbol{w}_{j}^{(i)} &amp;=\sigma\left(\boldsymbol{W}_{t}^{(i)} \boldsymbol{h}_{j}+\boldsymbol{b}_{t}^{(i)}\right)
        \end{aligned}" />

* Pre-training Objective (dEA):
    * dEA:
        * Given token sequence, and entity sequence, it needs to predict aligned entity. Its distribution is predicted by softmax.
        * 5% of time, token entity alignement is corrupted
        * 15% token-entity alignment is masked
        * 80% time, it is kept intact.
    * and, also MLM and NSP


* Fine-tuning tasks:
    * On NLP task, it follows normal BERT approach with CLS token in the begining.
    * For Relation classification, it introduce HD, and TL tokens as boundary markers, and take pooling on those, which then gets concatenated and given to classifier.
    * For Entity Typining, it just introduce ENT tokens as positional markers, and rest is similar.
    * Its illustration can be seen in following figure.

     <p align="center">
        <img width=600 src="images/ernie_finetuning.png">
        <em>Source: Author</em>
        </p>

* **Results**, ERNIE achieves better results on KG relationship classification, and entity typing tasks, where as it stays comparable for GLUE tasks. 
