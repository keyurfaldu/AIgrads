## Improving Neural Question Generation using Answer Separation
### Yanghoon Kim, Hwanhee Lee, Joongbo Shin and Kyomin Jung
### AAAI 2018 [[arXiv](https://arxiv.org/pdf/1809.02393.pdf)]

**Whats Unique**
This paper claims and validate that masking answer in a passage, and having a seperate encoder of seperated answer, would enable decoder to generate better questions, which would be more relevant as they would not contain answer information in them.

**Contribution**
1. Masking out answer in passage encoder
2. Keyword-net model, to encode key features to feed to decoder
3. decoder infromed by passage encoding, key features enconding of keyword net, and retrieval based mechanism to generate question
4. It generate words by querying word embedding.


**Architecture Diagram**
Following diagram illustrate the process.
<p align="center">
    <img width=600 src="images/NQG_answer_sep_arch.png">
    <em>Source: Author</em>
    </p>

* Problem Statement

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cbar%7BY%7D%20%26%3D%5Cunderset%7BY%7D%7B%5Coperatorname%7Bargmax%7D%7D%20P%5Cleft(Y%20%5Cmid%20X%5E%7Bp%7D%2C%20X%5E%7Ba%7D%5Cright)%20%5C%5C%0A%26%3D%5Cunderset%7BY%7D%7B%5Coperatorname%7Bargmax%7D%7D%20%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20P%5Cleft(y_%7Bt%7D%20%5Cmid%20X%5E%7Bp%7D%2C%20X%5E%7Ba%7D%2C%20y_%7B%3Ct%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\bar{Y} &amp;=\underset{Y}{\operatorname{argmax}} P\left(Y \mid X^{p}, X^{a}\right) \\
&amp;=\underset{Y}{\operatorname{argmax}} \sum_{t=1}^{T} P\left(y_{t} \mid X^{p}, X^{a}, y_{&lt;t}\right)
\end{aligned}" />

* Encoder 

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Coverrightarrow%7Bh_%7Bi%7D%5E%7Bp%7D%7D%3D%26%20%5Coverline%7BL%20S%20T%20M%7D%5Cleft(x_%7Bi%7D%5E%7Bp%7D%2C%20%5Coverrightarrow%7Bh%5E%7Bp%7D%7D_%7Bi-1%7D%5Cright)%20%5C%5C%0A%5Cstackrel%7B%5Cleftarrow%7D%7Bh_%7Bi%7D%5E%7Bp%7D%7D%3D%26%20%5Coverleftarrow%7BL%20S%20T%20M%7D%5Cleft(x_%7Bi%7D%5E%7Bp%7D%2C%20%5Cstackrel%7B%5Cleftarrow%7D%7Bh%5E%7Bp%7D%7D_%7Bi%2B1%7D%5Cright)%20%5C%5C%0A%26%20h_%7Bi%7D%5E%7Bp%7D%3D%5Cleft%5B%5Coverrightarrow%7Bh_%7Bi%7D%5E%7Bp%7D%7D%20%3B%20%5Cstackrel%7B%5Cleftarrow%7D%7Bh_%7Bi%7D%5E%7Bp%7D%7D%5Cright%5D%5C%5C%0Ae_%7Bt%20i%7D%3D%26v%5E%7B%5Ctop%7D%20%5Ctanh%20%5Cleft(W_%7Bc%7D%20s_%7Bt-1%7D%2BU_%7Bc%7D%20h_%7Bi%7D%5E%7Bp%7D%5Cright)%20%5C%5C%0A%5Calpha_%7Bt%20i%7D%3D%26%5Cfrac%7B%5Cexp%20%5Cleft(e_%7Bt%20i%7D%5Cright)%7D%7B%5Csum_%7Bk%3D1%7D%5E%7Bn%7D%20%5Cexp%20%5Cleft(e_%7Bt%20k%7D%5Cright)%7D%20%5C%5C%0Ac_%7Bt%7D%3D%26%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bt%20i%7D%20h_%7Bi%7D%5E%7Bp%7D%0A%5Cend%7Barray%7D" alt="\begin{aligned}
\overrightarrow{h_{i}^{p}}=&amp; \overline{L S T M}\left(x_{i}^{p}, \overrightarrow{h^{p}}_{i-1}\right) \\
\stackrel{\leftarrow}{h_{i}^{p}}=&amp; \overleftarrow{L S T M}\left(x_{i}^{p}, \stackrel{\leftarrow}{h^{p}}_{i+1}\right) \\
&amp; h_{i}^{p}=\left[\overrightarrow{h_{i}^{p}} ; \stackrel{\leftarrow}{h_{i}^{p}}\right]\\
e_{t i}=&amp;v^{\top} \tanh \left(W_{c} s_{t-1}+U_{c} h_{i}^{p}\right) \\
\alpha_{t i}=&amp;\frac{\exp \left(e_{t i}\right)}{\sum_{k=1}^{n} \exp \left(e_{t k}\right)} \\
c_{t}=&amp;\sum_{i=1}^{n} \alpha_{t i} h_{i}^{p}
\end{array}" />

* Answer Encoder

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Coverrightarrow%7Bh_%7Bj%7D%5E%7Ba%7D%7D%20%26%3D%5Coverline%7BL%20S%20T%20M%7D%5Cleft(x_%7Bj%7D%5E%7Ba%7D%2C%20%5Coverrightarrow%7Bh%5E%7Ba%7D%7D_%7Bj-1%7D%5Cright)%20%5C%5C%0A%5Cstackrel%7B%5Cleftarrow%7D%7Bh_%7Bj%7D%5E%7Ba%7D%7D%20%26%3D%5Coverleftarrow%7BL%20S%20T%20M%7D%5Cleft(x_%7Bj%7D%5E%7Ba%7D%2C%20%5Cstackrel%7B%5Cleftarrow%7D%7Bh%5E%7Ba%7D%7D_%7Bj%2B1%7D%5Cright)%20%5C%5C%0As_%7B0%7D%20%26%3Dh_%7B%5Ctext%20%7Bfinal%7D%7D%5E%7Ba%7D%3D%5Cleft%5B%5Coverrightarrow%7Bh_%7Bm%7D%5E%7Ba%7D%7D%20%3B%20%5Cstackrel%7B%5Cleftarrow%7D%7Bh_%7Bm%7D%5E%7Ba%7D%7D%5Cright%5D%0Ao_%7Bt%7D%5E%7B0%7D%26%3Dc_%7Bt%7D%20%5C%5C%0Ap_%7Bt%20j%7D%5E%7Bl%7D%26%3D%5Coperatorname%7BSoftmax%7D%5Cleft(%5Cleft(o_%7Bt%7D%5E%7Bl-1%7D%5Cright)%5E%7B%5Ctop%7D%20h_%7Bj%7D%5E%7Ba%7D%5Cright)%20%5C%5C%0Ao_%7Bt%7D%5E%7Bl%7D%26%3D%5Csum_%7Bj%7D%20p_%7Bt%20j%7D%5E%7Bl%7D%20h_%7Bj%7D%5E%7Ba%7D%0A%5Cend%7Barray%7D" alt="\begin{aligned}
\overrightarrow{h_{j}^{a}} &amp;=\overline{L S T M}\left(x_{j}^{a}, \overrightarrow{h^{a}}_{j-1}\right) \\
\stackrel{\leftarrow}{h_{j}^{a}} &amp;=\overleftarrow{L S T M}\left(x_{j}^{a}, \stackrel{\leftarrow}{h^{a}}_{j+1}\right) \\
s_{0} &amp;=h_{\text {final}}^{a}=\left[\overrightarrow{h_{m}^{a}} ; \stackrel{\leftarrow}{h_{m}^{a}}\right]
o_{t}^{0}&amp;=c_{t} \\
p_{t j}^{l}&amp;=\operatorname{Softmax}\left(\left(o_{t}^{l-1}\right)^{\top} h_{j}^{a}\right) \\
o_{t}^{l}&amp;=\sum_{j} p_{t j}^{l} h_{j}^{a}
\end{array}" />

* Retrieval Based Decoder

    <img src="https://i.upmath.me/svg/%0A%5Cbegin%7Baligned%7D%0As_%7Bt%7D%20%26%3D%20L%20S%20T%20M%5Cleft(y_%7Bt-1%7D%2C%20s_%7Bt-1%7D%2C%20c_%7Bt%7D%2C%20o_%7Bt%7D%5E%7BL%7D%5Cright)%20%5C%5C%0Aq_%7Bt%7D%20%26%3D%5Ctanh%20%5Cleft(W_%7Bq%7D%5Cleft%5Bs_%7Bt%7D%20%3B%20c_%7Bt%7D%5Cright%5D%5Cright)%20%5C%5C%0A%5Coperatorname%7Bscore%7D%5Cleft(q_%7Bt%7D%2C%20e_%7Bk%7D%5Cright)%20%26%3Dq_%7Bi%7D%5E%7B%5Ctop%7D%20W_%7Ba%7D%20e_%7Bk%7D%20%5C%5C%0Ap%5Cleft(y_%7Bt%7D%5Cright)%26%3D%5Coperatorname%7BSoftmax%7D%5Cleft(%5Coperatorname%7Bscore%7D%5Cleft(q_%7Bt%7D%2C%20e_%7Bk%7D%5Cright)%5Cright)%0A%5Cend%7Baligned%7D" alt="
\begin{aligned}
s_{t} &amp;= L S T M\left(y_{t-1}, s_{t-1}, c_{t}, o_{t}^{L}\right) \\
q_{t} &amp;=\tanh \left(W_{q}\left[s_{t} ; c_{t}\right]\right) \\
\operatorname{score}\left(q_{t}, e_{k}\right) &amp;=q_{i}^{\top} W_{a} e_{k} \\
p\left(y_{t}\right)&amp;=\operatorname{Softmax}\left(\operatorname{score}\left(q_{t}, e_{k}\right)\right)
\end{aligned}" />

**Note**
* It has compared the baseline performance which was answer-unaware.