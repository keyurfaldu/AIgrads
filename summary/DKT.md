## Deep Knowledge Tracing
### Piech et al
### 2015,  [NILPS](https://proceedings.neurips.cc/paper/2015/file/bac9162b47c56fc8a4d2a519803d51b3-Paper.pdf)

**Whats Unique**
This paper formulate and implement the problem of knowledge tracing using LSTM, and demonstrate the new SOTA benchmark.

**How does it work**
* Problem Illustration is shown in the figure below. Where on about 50 excercies, student's correctness was given, and each stage, the knowledge state of studen over all the concepts were computed.

<p align="center">
    <img width=600 src="images/DKT_example.png">
    <em>Source: Author</em>
    </p>

* Inputs: 
    * M unique exercise, input is one hot encoding of {q_t, a_t}
    * If M is too large, random projections of k-sparse data of d dimensions on k*log(d) can be used. 
    * Output vector y_t is length of the number of problems. 
* Simple network can be defined by following equations
    
    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0A%5Cmathbf%7Bh%7D_%7Bt%7D%3D%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Bh%20x%7D%20%5Cmathbf%7Bx%7D_%7Bt%7D%2B%5Cmathbf%7BW%7D_%7Bh%20h%7D%20%5Cmathbf%7Bh%7D_%7Bt-1%7D%2B%5Cmathbf%7Bb%7D_%7Bh%7D%5Cright)%20%5C%5C%0A%5Cmathbf%7By%7D_%7Bt%7D%3D%5Csigma%5Cleft(%5Cmathbf%7BW%7D_%7By%20h%7D%20%5Cmathbf%7Bh%7D_%7Bt%7D%2B%5Cmathbf%7Bb%7D_%7By%7D%5Cright)%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
\mathbf{h}_{t}=\tanh \left(\mathbf{W}_{h x} \mathbf{x}_{t}+\mathbf{W}_{h h} \mathbf{h}_{t-1}+\mathbf{b}_{h}\right) \\
\mathbf{y}_{t}=\sigma\left(\mathbf{W}_{y h} \mathbf{h}_{t}+\mathbf{b}_{y}\right)
\end{array}" /> 

* LSTM can be used as well. 

<p align="center">
    <img width=600 src="images/DKT_architecture.png">
    <em>Source: Author</em>
    </p>

* Objective function for loss can be computed as below:

    <img src="https://i.upmath.me/svg/L%3D%5Csum_%7Bt%7D%20%5Cell%5Cleft(%5Cmathbf%7By%7D%5E%7BT%7D%20%5Cdelta%5Cleft(q_%7Bt%2B1%7D%5Cright)%2C%20a_%7Bt%2B1%7D%5Cright)" alt="L=\sum_{t} \ell\left(\mathbf{y}^{T} \delta\left(q_{t+1}\right), a_{t+1}\right)" />

    * Notice, prediction of answer a_t+1 on question q_t+1 is dervied based on the output at q_t.

* AUC of 0.86 is achieved. 

* Content structure was discovered based on the sensitivity caused by exercise on each other. 1.4 millions of Khan academy exercise was used for about 45K students over 69 different types of exercise (concepts)

<p align="center">
    <img width=600 src="images/DKT_content_structure.png">
    <em>Source: Author</em>
    </p>



