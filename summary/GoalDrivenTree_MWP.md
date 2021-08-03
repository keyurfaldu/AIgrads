## A Goal-Driven Tree-Structured Neural Model for Math Word Problems
### Xie, Zhipeng, and Shichao Sun.
### In IJCAI, pp. 5299-5305. 2019. [PDF](https://www.ijcai.org/proceedings/2019/0736.pdf)

**Whats Unique**
It has a goal driven decomposition of the mathematical expression and decoder generates next token based on the parent and embeddings of sub-tree of its left sibling (if its the right sibling to a node). It limits its decoding vocaboloary and expression decomposition to make sure always syntactically correct output would be produced.

**How Does It Work**
* It has a Bi-directional GRU based decoder. 
* It limits its decoding vocabolury to numeric tokens n_p where p is positions, operators, and constants.
* It has the query vector, and it attend over encoded tokens to generate a context vector. 
* The probability of next token would be generated based on query, context, and the next token representation.

    <img src="https://i.upmath.me/svg/%5Cmathrm%7Bs%7D(y%20%5Cmid%20%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20P)%3D%5Cmathbf%7Bw%7D_%7Bn%7D%5E%7B%5Ctop%7D%20%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Bs%7D%5B%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20%5Cmathbf%7Be%7D(y%20%5Cmid%20P)%5D%5Cright)%5C%5C%0A%5Coperatorname%7Bprob%7D(y%20%5Cmid%20%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20P)%3D%5Cfrac%7B%5Cexp%20(%5Cmathrm%7Bs%7D(y%20%5Cmid%20%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20P))%7D%7B%5Csum_%7Bi%7D%20%5Cexp%20%5Cleft(%5Cmathrm%7Bs%7D%5Cleft(y_%7Bi%7D%20%5Cmid%20%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20P%5Cright)%5Cright)%7D" alt="\mathrm{s}(y \mid \mathbf{q}, \mathbf{c}, P)=\mathbf{w}_{n}^{\top} \tanh \left(\mathbf{W}_{s}[\mathbf{q}, \mathbf{c}, \mathbf{e}(y \mid P)]\right)\\
\operatorname{prob}(y \mid \mathbf{q}, \mathbf{c}, P)=\frac{\exp (\mathrm{s}(y \mid \mathbf{q}, \mathbf{c}, P))}{\sum_{i} \exp \left(\mathrm{s}\left(y_{i} \mid \mathbf{q}, \mathbf{c}, P\right)\right)}" />

    * Where, q is the query vector or the current state. * if current token generated is an operator, then it would generated left tree. q_l would be derived using GRU in this case.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ao_%7Bl%7D%20%26%3D%5Csigma%5Cleft(%5Cmathbf%7BW%7D_%7Bo%20l%7D%5B%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20%5Cmathbf%7Be%7D(%5Chat%7By%7D%20%5Cmid%20P)%5D%5Cright)%20%5C%5C%0AC_%7Bl%7D%20%26%3D%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Bc%20l%7D%5B%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20%5Cmathbf%7Be%7D(%5Chat%7By%7D%20%5Cmid%20P)%5D%5Cright)%20%5C%5C%0A%5Cmathbf%7Bh%7D_%7Bl%7D%20%26%3Do_%7Bl%7D%20%5Codot%20C_%7Bl%7D%20%5C%5C%0Ag_%7Bl%7D%20%26%3D%5Csigma%5Cleft(%5Cmathbf%7BW%7D_%7Bg%20l%7D%20%5Cmathbf%7Bh%7D_%7Bl%7D%5Cright)%20%5C%5C%0AQ_%7Bl%20e%7D%20%26%3D%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Bl%20e%7D%20%5Cmathbf%7Bh%7D_%7Bl%7D%5Cright)%20%5C%5C%0A%5Cmathbf%7Bq%7D_%7Bl%7D%20%26%3Dg_%7Bl%7D%20%5Codot%20Q_%7Bl%20e%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
o_{l} &amp;=\sigma\left(\mathbf{W}_{o l}[\mathbf{q}, \mathbf{c}, \mathbf{e}(\hat{y} \mid P)]\right) \\
C_{l} &amp;=\tanh \left(\mathbf{W}_{c l}[\mathbf{q}, \mathbf{c}, \mathbf{e}(\hat{y} \mid P)]\right) \\
\mathbf{h}_{l} &amp;=o_{l} \odot C_{l} \\
g_{l} &amp;=\sigma\left(\mathbf{W}_{g l} \mathbf{h}_{l}\right) \\
Q_{l e} &amp;=\tanh \left(\mathbf{W}_{l e} \mathbf{h}_{l}\right) \\
\mathbf{q}_{l} &amp;=g_{l} \odot Q_{l e}
\end{aligned}" />

    * If current token is a numeber, then it falls back recursively, and right subtree would be generated. While generating right subtree, it would also consider the representation of left subtree generated so far, ie. t_l

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ao_%7Br%7D%20%26%3D%5Csigma%5Cleft(%5Cmathbf%7BW%7D_%7Bo%20r%7D%5B%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20%5Cmathbf%7Be%7D(%5Chat%7By%7D%20%5Cmid%20P)%5D%5Cright)%20%5C%5C%0AC_%7Br%7D%20%26%3D%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Bc%20r%7D%5B%5Cmathbf%7Bq%7D%2C%20%5Cmathbf%7Bc%7D%2C%20%5Cmathbf%7Be%7D(%5Chat%7By%7D%20%5Cmid%20P)%5D%5Cright)%20%5C%5C%0A%5Cmathbf%7Bh%7D_%7Br%7D%20%26%3Do_%7Br%7D%20%5Codot%20C_%7Br%7D%20%5C%5C%0Ag_%7Br%7D%20%26%3D%5Csigma%5Cleft(%5Cmathbf%7BW%7D_%7Bg%20r%7D%5Cleft%5B%5Cmathbf%7Bh%7D_%7Br%7D%2C%20%5Cmathbf%7Bt%7D_%7Bl%7D%5Cright%5D%5Cright)%20%5C%5C%0AQ_%7Br%20e%7D%20%26%3D%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Br%20e%7D%5Cleft%5B%5Cmathbf%7Bh%7D_%7Br%7D%2C%20%5Cmathbf%7Bt%7D_%7Bl%7D%5Cright%5D%5Cright)%20%5C%5C%0A%5Cmathbf%7Bq%7D_%7Br%7D%20%26%3Dg_%7Br%7D%20%5Codot%20Q_%7Br%20e%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
o_{r} &amp;=\sigma\left(\mathbf{W}_{o r}[\mathbf{q}, \mathbf{c}, \mathbf{e}(\hat{y} \mid P)]\right) \\
C_{r} &amp;=\tanh \left(\mathbf{W}_{c r}[\mathbf{q}, \mathbf{c}, \mathbf{e}(\hat{y} \mid P)]\right) \\
\mathbf{h}_{r} &amp;=o_{r} \odot C_{r} \\
g_{r} &amp;=\sigma\left(\mathbf{W}_{g r}\left[\mathbf{h}_{r}, \mathbf{t}_{l}\right]\right) \\
Q_{r e} &amp;=\tanh \left(\mathbf{W}_{r e}\left[\mathbf{h}_{r}, \mathbf{t}_{l}\right]\right) \\
\mathbf{q}_{r} &amp;=g_{r} \odot Q_{r e}
\end{aligned}" />

* Following figure gives example of how decoding is done:
<p align="center">
    <img width=600 src="images/GoalDrivenTree_decoder.png">
    <em>Source: Author</em>
    </p>

* Over a simple linear decoder, goal driven decomposition has achieved a substantial improvement.
<p align="center">
    <img width=600 src="images/GoalDrivenTree_results.png">
    <em>Source: Author</em>
    </p>

