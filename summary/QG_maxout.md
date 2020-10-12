## Paragraph-level Neural Question Generation with Maxout Pointer and Gated Self-attention Networks
###  Yao Zhao, Xiaochuan Ni, Yuanyuan Ding, Qifa Ke
### ACL 2018 [[arXiv](https://www.aclweb.org/anthology/D18-1424.pdf)]

**Whats Unique**
This paper presents new techniques - maxout pointer and self attention encoder - to use longer sequence as context while generating text using copy/pointer networks. It focuses on answer-aware approach using sentences or paragraphs as inputs.

**How It Works**
* Problem Definition: Given paragraph and answer we need to generate a question. 

    <img src="https://i.upmath.me/svg/%5Cbar%7BQ%7D%3D%5Cunderset%7BQ%7D%7B%5Coperatorname%7Bargmax%7D%7D%20%5Coperatorname%7BProb%7D(Q%20%5Cmid%20P%2C%20A)" alt="\bar{Q}=\underset{Q}{\operatorname{argmax}} \operatorname{Prob}(Q \mid P, A)" />

    * Word generated in Q are either from input passage, or from a vocabulary V.

* Following figure illustrate the architecture really well:
    <p align="center">
        <img width=600 src="images/QG_maxout_architecture.png">
        <em>Source: Author</em>
        </p> 

* The attention encoder output is generated as follow:
    * **Gated self attention** has two steps:
        1.  self matching represenation (f_t) by taking encoded passage-answer represenation (u) and conducting matching with itself (U).
        2. combining input (u) with self matching represenation (f_t) using a feature fusion gate.

    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bu%7D_%7Bt%7D%3DR%20N%20N%5E%7BE%7D%5Cleft(%5Cmathbf%7Bu%7D_%7Bt-1%7D%2C%5Cleft%5B%5Cmathbf%7Be%7D_%7Bt%7D%2C%20%5Cmathbf%7Bm%7D_%7Bt%7D%5Cright%5D%5Cright)%5C%5C%0A%5Cmathbf%7Ba%7D_%7Bt%7D%5E%7B%5Cmathbf%7Bs%7D%7D%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BU%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7BW%7D%5E%7Bs%7D%20%5Cmathbf%7Bu%7D_%7Bt%7D%5Cright)%5C%5C%0A%5Cmathbf%7Bs%7D_%7Bt%7D%3D%5Cmathbf%7BU%7D%20%5Ccdot%20%5Cmathbf%7Ba%7D_%7Bt%7D%5E%7B%5Cmathbf%7Bs%7D%7D%5C%5C%0A%5Cmathbf%7Bf%7D_%7Bt%7D%3D%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D%5E%7Bf%7D%5Cleft%5B%5Cmathbf%7Bu%7D_%7Bt%7D%2C%20%5Cmathbf%7Bs%7D_%7Bt%7D%5Cright%5D%5Cright)%5C%5C%0A%5Cmathbf%7Bg%7D_%7Bt%7D%3D%5Coperatorname%7Bsigmoid%7D%5Cleft(%5Cmathbf%7BW%7D%5E%7Bg%7D%5Cleft%5B%5Cmathbf%7Bu%7D_%7Bt%7D%2C%20%5Cmathbf%7Bs%7D_%7Bt%7D%5Cright%5D%5Cright)%5C%5C%0A%5Chat%7B%5Cmathbf%7Bu%7D%7D_%7Bt%7D%3D%5Cmathbf%7Bg%7D_%7Bt%7D%20%5Codot%20%5Cmathbf%7Bf%7D_%7Bt%7D%2B%5Cleft(1-%5Cmathbf%7Bg%7D_%7Bt%7D%5Cright)%20%5Codot%20%5Cmathbf%7Bu%7D_%7Bt%7D" alt="\mathbf{u}_{t}=R N N^{E}\left(\mathbf{u}_{t-1},\left[\mathbf{e}_{t}, \mathbf{m}_{t}\right]\right)\\
\mathbf{a}_{t}^{\mathbf{s}}=\operatorname{softmax}\left(\mathbf{U}^{\top} \mathbf{W}^{s} \mathbf{u}_{t}\right)\\
\mathbf{s}_{t}=\mathbf{U} \cdot \mathbf{a}_{t}^{\mathbf{s}}\\
\mathbf{f}_{t}=\tanh \left(\mathbf{W}^{f}\left[\mathbf{u}_{t}, \mathbf{s}_{t}\right]\right)\\
\mathbf{g}_{t}=\operatorname{sigmoid}\left(\mathbf{W}^{g}\left[\mathbf{u}_{t}, \mathbf{s}_{t}\right]\right)\\
\hat{\mathbf{u}}_{t}=\mathbf{g}_{t} \odot \mathbf{f}_{t}+\left(1-\mathbf{g}_{t}\right) \odot \mathbf{u}_{t}" />

* Decoding with without attention and without max-out pointer:

    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bd%7D_%7Bt%7D%3DR%20N%20N%5E%7BD%7D%5Cleft(%5Cmathbf%7Bd%7D_%7Bt-1%7D%2C%20%5Cmathbf%7By%7D_%7Bt-1%7D%5Cright)%5C%5C%0Ap%5Cleft(y_%7Bt%7D%20%5Cmid%5Cleft%5C%7By_%7B%3Ct%7D%5Cright%5C%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BW%7D%5E%7BV%7D%20%5Cmathbf%7Bd%7D_%7Bt%7D%5Cright)" alt="\mathbf{d}_{t}=R N N^{D}\left(\mathbf{d}_{t-1}, \mathbf{y}_{t-1}\right)\\
p\left(y_{t} \mid\left\{y_{&lt;t}\right\}\right)=\operatorname{softmax}\left(\mathbf{W}^{V} \mathbf{d}_{t}\right)" />

* Decoding with attention and without max-out pointer

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cmathbf%7Br%7D_%7Bt%7D%20%26%3D%5Chat%7B%5Cmathbf%7BU%7D%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7BW%7D%5E%7Ba%7D%20%5Cmathbf%7Bd%7D_%7B%5Cmathbf%7Bt%7D%7D%20%5C%5C%20%5Cmathbf%7Ba%7D_%7Bt%7D%5E%7B%5Cmathbf%7Bd%7D%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7Br%7D_%7Bt%7D%5Cright)%20%5C%5C%20%5Cmathbf%7Bc%7D_%7Bt%7D%20%26%3D%5Chat%7B%5Cmathbf%7BU%7D%7D%20%5Ccdot%20%5Cmathbf%7Ba%7D%5E%7B%5Cmathbf%7Bd%7D%7D%20t%20%5C%5C%20%5Chat%7B%5Cmathbf%7Bd%7D%7D_%7Bt%7D%20%26%3D%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D%5E%7Bb%7D%5Cleft%5B%5Cmathbf%7Bd%7D_%7Bt%7D%2C%20%5Cmathbf%7Bc%7D_%7Bt%7D%5Cright%5D%5Cright)%20%5Cend%7Baligned%7D" alt="\begin{aligned} \mathbf{r}_{t} &amp;=\hat{\mathbf{U}}^{\top} \mathbf{W}^{a} \mathbf{d}_{\mathbf{t}} \\ \mathbf{a}_{t}^{\mathbf{d}} &amp;=\operatorname{softmax}\left(\mathbf{r}_{t}\right) \\ \mathbf{c}_{t} &amp;=\hat{\mathbf{U}} \cdot \mathbf{a}^{\mathbf{d}} t \\ \hat{\mathbf{d}}_{t} &amp;=\tanh \left(\mathbf{W}^{b}\left[\mathbf{d}_{t}, \mathbf{c}_{t}\right]\right) \end{aligned}" />

* Decoding with Copy/Pointer

    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bs%20c%7D%5E%7Bc%20o%20p%20y%7D%5Cleft(y_%7Bt%7D%5Cright)%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Blr%7D%5Csum_%7Bk%2C%20w%20h%20e%20r%20e%20~%20x_%7Bk%7D%3Dy_%7Bt%7D%7D%20r_%7Bt%2Ck%7D%20%26%20y_%7Bt%7D%20%5Cin%20%5Cchi%20%5C%5C%20-i%20n%20f%2C%20%26%20%5Ctext%20%7B%20otherwise%20%7D%5Cend%7Barray%7D%5Cright." alt="\mathbf{s c}^{c o p y}\left(y_{t}\right)=\left\{\begin{array}{lr}\sum_{k, w h e r e ~ x_{k}=y_{t}} r_{t,k} &amp; y_{t} \in \chi \\ -i n f, &amp; \text { otherwise }\end{array}\right." />

* Decoding with max/out pointer

    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bs%20c%7D%5E%7Bc%20o%20p%20y%7D%5Cleft(y_%7Bt%7D%5Cright)%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Blr%7D%5Cmax%20_%7Bk%2C%20w%20h%20e%20r%20e%20x_%7Bk%7D%3Dy_%7Bt%7D%7D%20r_%7Bt%2Ck%7D%20%26%20y_%7Bt%7D%20%5Cin%20%5Cchi%20%5C%5C%20-i%20n%20f%2C%20%26%20%5Ctext%20%7B%20otherwise%20%7D%5Cend%7Barray%7D%5Cright." alt="\mathbf{s c}^{c o p y}\left(y_{t}\right)=\left\{\begin{array}{lr}\max _{k, w h e r e x_{k}=y_{t}} r_{t,k} &amp; y_{t} \in \chi \\ -i n f, &amp; \text { otherwise }\end{array}\right." />

* scores of SC_copy can be appeneded to generative score d_t, which then can be fed together to softmax to generate the output. Independently, SC_copy and d_t can independently passed to softmax, and output is picked from one of them using another dynamic weight learned.

* Results: In the following ablation study, it demonstrate how each architectural design has impacted performance positively.

<p align="center">
    <img width=600 src="images/QG_maxout_ablation.png">
    <em>Source: Author</em>
    </p>









