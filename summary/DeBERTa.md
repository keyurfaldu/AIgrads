## DeBERTa: Decoding-enhanced BERT with Disentangled Attention."
### He, Pengcheng, Xiaodong Liu, Jianfeng Gao, and Weizhu Chen. 
### arXiv preprint arXiv:2006.03654 (2020). [[arXiv](https://arxiv.org/pdf/2006.03654.pdf)]

**Whats Unique**
DeBERTa solves the problem of fading impact of positional weights using seperate representations for content and positions and cleverly leveraging attention mechanism

**How It Works**
* It keeps two representation for each token at each layer, content representation and position representation.

* It computes attention between word i and j using content_i . content_j, content_i . position_j, and position_i . content_j interactions.


<img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0AQ_%7Bc%7D%3DH%20W_%7Bq%2C%20c%7D%2C%20K_%7Bc%7D%3D%26%20H%20W_%7Bk%2C%20c%7D%2C%20V_%7Bc%7D%3DH%20W_%7Bv%2C%20c%7D%2C%20Q_%7Br%7D%3DP%20W_%7Bq%2C%20r%7D%2C%20K_%7Br%7D%3DP%20W_%7Bk%2C%20r%7D%20%5C%5C%0A%5Ctilde%7BA%7D_%7Bi%2C%20j%7D%3D%26%20%5Cunderbrace%7BQ_%7Bi%7D%5E%7Bc%7D%20K_%7Bj%7D%5E%7Bc%20%5Ctop%7D%7D_%7B%5Ctext%20%7B(a)%20content-to-content%20%7D%7D%2B%5Cunderbrace%7BQ_%7Bi%7D%5E%7Bc%7D%20K_%7B%5Cdelta(i%2C%20j)%7D%5E%7Br%7D%20T%7D_%7B%5Ctext%20%7B(b)%20content-to-position%20%7D%7D%2B%5Cunderbrace%7BK_%7Bj%7D%5E%7Bc%7D%20Q_%7B%5Cdelta(j%2C%20i)%7D%5E%7Br%7D%7D_%7B%5Ctext%20%7B(c)%20position-to-content%20%7D%7D%20%5C%5C%0AH_%7Bo%7D%3D%26%20%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cfrac%7B%5Ctilde%7BA%7D%7D%7B%5Csqrt%7B3%20d%7D%7D%5Cright)%20V_%7Bc%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
Q_{c}=H W_{q, c}, K_{c}=&amp; H W_{k, c}, V_{c}=H W_{v, c}, Q_{r}=P W_{q, r}, K_{r}=P W_{k, r} \\
\tilde{A}_{i, j}=&amp; \underbrace{Q_{i}^{c} K_{j}^{c \top}}_{\text {(a) content-to-content }}+\underbrace{Q_{i}^{c} K_{\delta(i, j)}^{r} T}_{\text {(b) content-to-position }}+\underbrace{K_{j}^{c} Q_{\delta(j, i)}^{r}}_{\text {(c) position-to-content }} \\
H_{o}=&amp; \operatorname{softmax}\left(\frac{\tilde{A}}{\sqrt{3 d}}\right) V_{c}
\end{aligned}" />

* It has given much improvement on GLUE, SuperGLUE and other NLP downstream tasks.

