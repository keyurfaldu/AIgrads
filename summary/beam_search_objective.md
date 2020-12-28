## If Beam Search is the Answer, What was the Question
### Clara Meister, Tim Vieira, Ryan Cotterell
### Oct 2020, EMNLP [[arXiv](https://arxiv.org/pdf/2010.02650.pdf)]

**Whats Unique**
In practice, beam-search works very effectively which gives an opportunity to make sub-optimal decisions at each step, however the objective function tries to minimise the global probability, which sometime can cause meaningless or empty string generation.

**How It Works**
* It is the concept of congintive science and information theory that human tries to spread information uniformly in the sentence. Which avoids surprises. 

* Information is defined as the negative log-probability in the information theory.

* UID (uniform information density) - this can be a good regulariser to modify the text decoding objective.

* Normally, decorder use following function to learn text generation.

    <img src="https://i.upmath.me/svg/p_%7B%5Cboldsymbol%7B%5Ctheta%7D%7D(%5Cmathbf%7By%7D%20%5Cmid%20%5Cmathbf%7Bx%7D)%3D%5Cprod_%7Bt%3D1%7D%5E%7B%7C%5Cmathbf%7By%7D%7C%7D%20p_%7B%5Cboldsymbol%7B%5Ctheta%7D%7D%5Cleft(y_%7Bt%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%2C%20%5Cmathbf%7By%7D_%7B%3Ct%7D%5Cright)%5C%5C%0A%5Cmathbf%7By%7D%5E%7B%5Cstar%7D%3D%5Cunderset%7B%5Cmathbf%7By%7D%20%5Cin%20%5Cmathcal%7BY%7D%7D%7B%5Coperatorname%7Bargmax%7D%7D%20%5Clog%20p_%7B%5Ctheta%7D(%5Cmathbf%7By%7D%20%5Cmid%20%5Cmathbf%7Bx%7D)" alt="p_{\boldsymbol{\theta}}(\mathbf{y} \mid \mathbf{x})=\prod_{t=1}^{|\mathbf{y}|} p_{\boldsymbol{\theta}}\left(y_{t} \mid \mathbf{x}, \mathbf{y}_{&lt;t}\right)\\
\mathbf{y}^{\star}=\underset{\mathbf{y} \in \mathcal{Y}}{\operatorname{argmax}} \log p_{\theta}(\mathbf{y} \mid \mathbf{x})" />

* This is commonly known as Maximise a posteriori (MAP) decoding. And solving this problem with RNN is NP Hard. Therefore decoding is generally performed with heuristic method such as greedy exact search, or beam search.

* Beam Search - it is a pruned breath first search, where at every step maximum k hypothesis are expanded.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0AY_%7B0%7D%3D%5C%7B%5Ctext%20%7B%20BOS%20%7D%5C%7D%20%5C%5C%0AY_%7Bt%7D%3D%5Cunderset%7BY%5E%7B%5Cprime%7D%20%5Csubseteq%20%5Cmathcal%7BB%7D_%7Bt%7D%2C%20%7CY%5E%7B%5Cprime%7D%7C%3Dk%20%7D%7B%5Coperatorname%7Bargmax%7D%7D%20%5Clog%20p_%7B%5Ctheta%7D%5Cleft(Y%5E%7B%5Cprime%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5Cright)%20%5C%5C%0A%5Cend%7Barray%7D%5C%5C%0A%5Cmathcal%7BB%7D_%7Bt%7D%3D%5Cleft%5C%7B%5Cmathbf%7By%7D_%7Bt-1%7D%20%5Ccirc%20y%20%5Cmid%20y%20%5Cin%20%5Coverline%7B%5Cmathcal%7BV%7D%7D%20%5Ctext%20%7B%20and%20%7D%20%5Cmathbf%7By%7D_%7Bt-1%7D%20%5Cin%20Y_%7Bt-1%7D%5Cright%5C%7D%0A" alt="\begin{array}{l}
Y_{0}=\{\text { BOS }\} \\
Y_{t}=\underset{Y^{\prime} \subseteq \mathcal{B}_{t}, |Y^{\prime}|=k }{\operatorname{argmax}} \log p_{\theta}\left(Y^{\prime} \mid \mathbf{x}\right) \\
\end{array}\\
\mathcal{B}_{t}=\left\{\mathbf{y}_{t-1} \circ y \mid y \in \overline{\mathcal{V}} \text { and } \mathbf{y}_{t-1} \in Y_{t-1}\right\}
" />
    * Where operator P_theta (Y'|x) is overloaded, as Y' is the set of hypothesis.
    * It is defined as the product of probability for each hypothesis. P_theta (y1 | x) * P_theta (y2 | x) * ..

* Decoding can be regularised with additional regulariser
    <img src="https://i.upmath.me/svg/%5Cmathbf%7By%7D%5E%7B%5Cstar%7D%3D%5Cunderset%7B%5Cmathbf%7By%7D%20%5Cin%20%5Cmathcal%7BY%7D%7D%7B%5Coperatorname%7Bargmax%7D%7D%5Cleft(%5Clog%20p_%7B%5Ctheta%7D(%5Cmathbf%7By%7D%20%5Cmid%20%5Cmathbf%7Bx%7D)-%5Clambda%20%5Ccdot%20%5Cmathcal%7BR%7D(%5Cmathbf%7By%7D)%5Cright)" alt="\mathbf{y}^{\star}=\underset{\mathbf{y} \in \mathcal{Y}}{\operatorname{argmax}}\left(\log p_{\theta}(\mathbf{y} \mid \mathbf{x})-\lambda \cdot \mathcal{R}(\mathbf{y})\right)" /> 

* Basic idea is to keep reducing the new information which gets added at each step, we can derive it as follow
    * New information expressed at time t, 

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Au_%7B0%7D(%5Cmathrm%7BBOS%7D)%20%26%3D0%20%5C%5C%0Au_%7Bt%7D(y)%20%26%3D-%5Clog%20p_%7B%5Ctheta%7D%5Cleft(y%20%5Cmid%20%5Cmathbf%7Bx%7D%2C%20%5Cmathbf%7By%7D_%7B%3Ct%7D%5Cright)%2C%20%5Ctext%20%7B%20for%20%7D%20t%20%5Cgeq%201%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
u_{0}(\mathrm{BOS}) &amp;=0 \\
u_{t}(y) &amp;=-\log p_{\theta}\left(y \mid \mathbf{x}, \mathbf{y}_{&lt;t}\right), \text { for } t \geq 1
\end{aligned}" />

    * Now we can derive greedy decoding with the following objective.

    <img src="https://i.upmath.me/svg/%5Cmathcal%7BR%7D_%7B%5Ctext%20%7Bgreedy%20%7D%7D(%5Cmathbf%7By%7D)%3D%5Csum_%7Bt%3D1%7D%5E%7B%7C%5Cmathbf%7By%7D%7C%7D%5Cleft(u_%7Bt%7D%5Cleft(y_%7Bt%7D%5Cright)-%5Cmin%20_%7By%5E%7B%5Cprime%7D%20%5Cin%20%5Cmathcal%7BV%7D%7D%20u_%7Bt%7D%5Cleft(y%5E%7B%5Cprime%7D%5Cright)%5Cright)%5E%7B2%7D" alt="\mathcal{R}_{\text {greedy }}(\mathbf{y})=\sum_{t=1}^{|\mathbf{y}|}\left(u_{t}\left(y_{t}\right)-\min _{y^{\prime} \in \mathcal{V}} u_{t}\left(y^{\prime}\right)\right)^{2}" /> 

    where, the idea is to minimize the new information (or maximize the probability) at each step.

    * We can write decoding objective for beam search as follow: 

    <img src="https://i.upmath.me/svg/Y%5E%7B%5Cstar%7D%3D%5Cunderset%7BY%20%5Csubseteq%20%5Cmathcal%7BY%7D%20%5Catop%7CY%7C%3Dk%7D%7B%5Coperatorname%7Bargmax%7D%7D%5Cleft(%5Clog%20p_%7B%5Ctheta%7D(Y%20%5Cmid%20%5Cmathbf%7Bx%7D)-%5Clambda%20%5Ccdot%20%5Cmathcal%7BR%7D(Y)%5Cright)" alt="Y^{\star}=\underset{Y \subseteq \mathcal{Y} \atop|Y|=k}{\operatorname{argmax}}\left(\log p_{\theta}(Y \mid \mathbf{x})-\lambda \cdot \mathcal{R}(Y)\right)" />

    * where, we can formulate regularizer as follow:

    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0A%5Cmathcal%7BR%7D_%7B%5Ctext%20%7Bbeam%20%7D%7D(Y)%3D%20%5Csum_%7Bt%3D1%7D%5E%7Bn_%7B%5Cmax%20%7D%7D%5Cleft(u_%7Bt%7D%5Cleft(Y_%7Bt%7D%5Cright)-%5Cmin%20_%7BY%5E%7B%5Cprime%7D%20%5Csubseteq%20%5Cmathcal%7BB%7D_%7Bt%7D%2C%7D%20u_%7Bt%7D%5Cleft(Y%5E%7B%5Cprime%7D%5Cright)%5Cright)%5E%7B2%7D%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
\mathcal{R}_{\text {beam }}(Y)= \sum_{t=1}^{n_{\max }}\left(u_{t}\left(Y_{t}\right)-\min _{Y^{\prime} \subseteq \mathcal{B}_{t},} u_{t}\left(Y^{\prime}\right)\right)^{2}
\end{array}" />

    * Operator u_t which was defined for unique hypotheis, have been overloaded for the set of hypothesis as following: 
    
    <img src="https://i.upmath.me/svg/u_%7Bt%7D(Y)%3D%5Csum_%7By%20%5Cin%20Y%7D%20u_%7Bt%7D(y)" alt="u_{t}(Y)=\sum_{y \in Y} u_{t}(y)" />

* Following figure illustrate, how a with varying lambda values, how an objective can generate a greey decoding, and how greedier decoding will have lesser surprisals. 

<p align="center">
    <img width=600 src="images/beam_search_objective_illustration.png">
    <em>Source: Author</em>
    </p>


