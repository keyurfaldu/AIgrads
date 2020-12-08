## Individualized Bayesian Knowledge Tracing
Models](summary/Individualised_BKT.md) 
### Michael V. Yudelson, Kenneth R. Koedinger, and Geoffrey J. Gordon, 
### CMU, [[Springer 2013](https://www.cs.cmu.edu/~ggordon/yudelson-koedinger-gordon-individualized-bayesian-knowledge-tracing.pdf)]

**Whats New**
This paper presents a systematic method for individualised BKT, where two parameters intial learning state and transition probabilities are individualised and compared with vanilla BKT. 

**How Does It Work**

BKT has mainly four parameters
* p(L_0): initial learning state
* P(T): Transition probability from unlearned state to learned state once user is given opportunity to apply
* P(S): probability of incorrect in learned state
* P(G): probability of correct in unlearned state, i.e. guessing

<img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ap%5Cleft(L_%7B1%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%26%3Dp%5Cleft(L_%7B0%7D%5Cright)%5E%7Bk%7D%20%5C%5C%0Ap%5Cleft(L_%7Bt%2B1%7D%20%5Cmid%20o%20b%20s%3D%5Coperatorname%7Bcorrect%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%26%3D%5Cfrac%7Bp%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%5Ccdot%5Cleft(1-p(S)%5E%7Bk%7D%5Cright)%7D%7Bp%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%5Ccdot%5Cleft(1-p(S)%5E%7Bk%7D%5Cright)%2B%5Cleft(1-p%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%5Cright)%20%5Ccdot%20p(G)%5E%7Bk%7D%7D%20%5C%5C%0Ap%5Cleft(L_%7Bt%2B1%7D%20%5Cmid%20o%20b%20s%3Dw%20r%20o%20n%20g%5Cright)_%7Bu%7D%5E%7Bk%7D%20%26%3D%5Cfrac%7Bp%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%20%5Ccdot%20p(S)%5E%7Bk%7D%7D%7Bp%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%5Ccdot%20p(S)%5E%7Bk%7D%2B%5Cleft(1-p%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%5Cright)%20%5Ccdot%5Cleft(1-p(G)%5E%7Bk%7D%5Cright)%7D%20%5C%5C%0Ap%5Cleft(L_%7Bt%2B1%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%26%3Dp%5Cleft(L_%7Bt%2B1%7D%20%5Cmid%20o%20b%20s%5Cright)_%7Bu%7D%5E%7Bk%7D%2B%5Cleft(1-p%5Cleft(L_%7Bt%2B1%7D%20%5Cmid%20o%20b%20s%5Cright)_%7Bu%7D%5E%7Bk%7D%5Cright)%20%5Ccdot%20p(T)%5E%7Bk%7D%20%5C%5C%0Ap%5Cleft(C_%7Bt%2B1%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%26%3Dp%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%20%5Ccdot%5Cleft(1-p(S)%5E%7Bk%7D%5Cright)%2B%5Cleft(1-p%5Cleft(L_%7Bt%7D%5Cright)_%7Bu%7D%5E%7Bk%7D%5Cright)%20%5Ccdot%20p(G)%5E%7Bk%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
p\left(L_{1}\right)_{u}^{k} &amp;=p\left(L_{0}\right)^{k} \\
p\left(L_{t+1} \mid o b s=\operatorname{correct}\right)_{u}^{k} &amp;=\frac{p\left(L_{t}\right)_{u}^{k} \cdot\left(1-p(S)^{k}\right)}{p\left(L_{t}\right)_{u}^{k} \cdot\left(1-p(S)^{k}\right)+\left(1-p\left(L_{t}\right)_{u}^{k}\right) \cdot p(G)^{k}} \\
p\left(L_{t+1} \mid o b s=w r o n g\right)_{u}^{k} &amp;=\frac{p\left(L_{t}\right)_{u} \cdot p(S)^{k}}{p\left(L_{t}\right)_{u}^{k} \cdot p(S)^{k}+\left(1-p\left(L_{t}\right)_{u}^{k}\right) \cdot\left(1-p(G)^{k}\right)} \\
p\left(L_{t+1}\right)_{u}^{k} &amp;=p\left(L_{t+1} \mid o b s\right)_{u}^{k}+\left(1-p\left(L_{t+1} \mid o b s\right)_{u}^{k}\right) \cdot p(T)^{k} \\
p\left(C_{t+1}\right)_{u}^{k} &amp;=p\left(L_{t}\right)_{u}^{k} \cdot\left(1-p(S)^{k}\right)+\left(1-p\left(L_{t}\right)_{u}^{k}\right) \cdot p(G)^{k}
\end{aligned}" />

* Where P(C_t+1) is the predicted probability of a correct attempt at time t+1 on skill k by user u.

* This paper presents efficient way to backpropogate and learn parameters, where parameters are stored in matrix form

<p align="center">
    <img width=600 src="images/BKT_params_tables.png">
    <em>Source: Author</em>
    </p>

* To successfully solve BKT problems, we need to solve two problems
    * Evaluation problem: given BKT parameters lambda = (Pi, A, B), and senquence of observations O = (o_t, t \in 1..T), what is the probability of that observations are generated from the given BKT model.
    * Learning problem: given BKT parameters lambda, and a sequence of observations, O, how should lambda be adjusted to maximise p(O|lambda)

* Results
    * KDD Cup 2010 dataset was used, where it had two datasets
        * Algebra 1: 8,918,054 rows of practive attempts by 3310 students, with more than 550 different skills.
        * The Bridge to Algebra: 20 million attempts for about 6,043 students, over about 900 distinct skills.

    * BKT model with individualised transition probability has given the best improvement.

