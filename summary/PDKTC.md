## Prerequisite-Driven Deep Knowledge Tracing
### Penghe Chen, Yu Lu, Vincent W. Zheng, Yang Pian 
### ICDM 2018 [[arXiv](https://aic-fe.bnu.edu.cn/docs/20190108101850881476.pdf)]


**Whats Unique**
This paper presents a new loss function to accomodate concepts pre-requisite constraints in deep knowledge tracing model.

**How It Works**
* Following figure illustrates the system diagram

<p align="center">
    <img width=600 src="images/PDKTC_illustration.png">
    <em>Source: Author</em>
    </p>

* Following figure presents the architecture
<p align="center">
    <img width=600 src="images/PDKTC_architecture.png">
    <em>Source: Author</em>
    </p>

* Concept mastery are computed by applying sigmoid on dot product of hidden state and concept embedding

    <img src="https://i.upmath.me/svg/%20P%5Cleft(m_%7Bi%2C%20k%2C%20t%7D%3D1%20%5Cmid%20%5Cmathbf%7Bs%7D_%7Bi%7D%2C%20%5CTheta_%7BG%20R%20U%7D%2C%20%5Cmathbf%7Bc%7D_%7Bk%7D%5Cright)%3D%5Csigma%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%2C%20t-1%7D%5E%7BT%7D%20%5Cmathbf%7Bc%7D_%7Bk%7D%2Bb_%7Bm%7D%5Cright)" alt=" P\left(m_{i, k, t}=1 \mid \mathbf{s}_{i}, \Theta_{G R U}, \mathbf{c}_{k}\right)=\sigma\left(\mathbf{h}_{i, t-1}^{T} \mathbf{c}_{k}+b_{m}\right)" />

* Correctness is predicted by taking product of concept mastery

    <img src="https://i.upmath.me/svg/%5CDelta_%7Bi%2C%20j%2C%20t%7D%3D%5Cprod_%7Bk%3A%20O_%7Bj%2C%20k%7D%3D1%7D%20P%5Cleft(m_%7Bi%2C%20k%2C%20t%7D%3D1%20%5Cmid%20%5Cmathbf%7Bs%7D_%7Bi%7D%2C%20%5CTheta_%7BG%20R%20U%7D%2C%20%5Cmathbf%7Bc%7D_%7Bk%7D%5Cright)" alt="\Delta_{i, j, t}=\prod_{k: O_{j, k}=1} P\left(m_{i, k, t}=1 \mid \mathbf{s}_{i}, \Theta_{G R U}, \mathbf{c}_{k}\right)" />

    <img src="https://i.upmath.me/svg/P%5Cleft(y_%7Bi%2C%20j%2C%20t%7D%3D1%20%5Cmid%20%5Cmathbf%7Bs%7D_%7Bi%7D%2C%20%5CTheta%5Cright)%3D%5CDelta_%7Bi%2C%20j%2C%20t%7D" alt="P\left(y_{i, j, t}=1 \mid \mathbf{s}_{i}, \Theta\right)=\Delta_{i, j, t}" />

* Updated loss function with the constraint of pre-requisite concepts are as below

    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0A%5Cmax%20_%7B%5CTheta%7D%20%5Clog%20%5Cprod_%7Bi%7D%20%5Cprod_%7Bt%7D%20P%5Cleft(y_%7Bi%2C%20%5Cpi(i%2C%20t)%2C%20t%7D%20%5Cmid%20%5Cmathbf%7Bs%7D_%7Bi%7D%2C%20%5CTheta%5Cright)%20%5C%5C%0A%5Ctext%20%7B%20s.t.%2C%20%7D%20P%5Cleft(m_%7Bi%2C%20k_%7B2%7D%2C%20t_%7B2%7D%7D%3D1%5Cright)%20%5Cleq%20P%5Cleft(m_%7Bi%2C%20k_%7B1%7D%2C%20t_%7B1%7D%7D%3D1%5Cright)%20%5C%5C%0A%5Cquad%20%5Cforall%5Cleft(k_%7B1%7D%2C%20k_%7B2%7D%5Cright)%20%5Cin%20E%20%5Cquad%20%5C%26%20%5Cquad%20y_%7Bi%2C%20%5Cpi%5Cleft(i%2C%20t_%7B1%7D%5Cright)%2C%20t_%7B1%7D%7D%3Dy_%7Bi%2C%20%5Cpi%5Cleft(i%2C%20t_%7B2%7D%5Cright)%2C%20t_%7B2%7D%7D%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
\max _{\Theta} \log \prod_{i} \prod_{t} P\left(y_{i, \pi(i, t), t} \mid \mathbf{s}_{i}, \Theta\right) \\
\text { s.t., } P\left(m_{i, k_{2}, t_{2}}=1\right) \leq P\left(m_{i, k_{1}, t_{1}}=1\right) \\
\quad \forall\left(k_{1}, k_{2}\right) \in E \quad \&amp; \quad y_{i, \pi\left(i, t_{1}\right), t_{1}}=y_{i, \pi\left(i, t_{2}\right), t_{2}}
\end{array}" />

**Results**
* PDKTC has been applied on various open datasets and it has outperformed SOTA results

<p align="center">
    <img width=600 src="images/PDKTC_results.png">
    <em>Source: Author</em>
    </p>

