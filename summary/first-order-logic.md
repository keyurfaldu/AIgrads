## Augmenting Neural Networks with First-order Logic
### Tao Li, Vijay Srikumar
### 2019, [[arXiv](https://arxiv.org/pdf/1906.06298.pdf)]

**Whats New**
It gives a framework to augment neuron with a rule from external knowledge, and proves its effectivenss specifically with the lesser training data.

**Illustrative Example**
    <p align="center">
    <img width=600 src="images/first_order_logic_example.png">
    <em>Source: Author</em>
    </p>


**Major Contribution**
* Framework incorporating first-oder logic rules into neural network design
* Experiments on augmenting neural network with first order logic at following three levels:
    * intermediate decisions (i.e. attentions);
    * output decisions constrained by intermediate states
    *output decisions constrained using label dependencies
* Validation of the framework on three use cases

**How It Works**
* Augmenting Attentions
    <p align="center">
    <img width=600 src="images/first_order_logic_attention.png">
    <em>Source: Author</em>
    </p>

    * As can be seen above, attentions are modifed with external knowledge, rules can be specified as follow
        <img src="https://i.upmath.me/svg/R_%7B1%7D%3A%20%5Cquad%20%5Cforall%20i%2C%20j%20%5Cin%20C%2C%20K_%7Bi%2C%20j%7D%20%5Crightarrow%20%5Coverleftarrow%7BA%7D_%7Bi%2C%20j%7D%5E%7B%5Cprime%7D%20%5C%5C%0A%24R_%7B2%7D%3A%20%5Cquad%20%5Cforall%20i%2C%20j%20%5Cin%20C%2C%20K_%7Bi%2C%20j%7D%20%5Cwedge%20%5Coverleftarrow%7BA%7D_%7Bi%2C%20j%7D%20%5Crightarrow%20%5Coverleftarrow%7BA%7D_%7Bi%2C%20j%7D%5E%7B%5Cprime%7D" alt="R_{1}: \quad \forall i, j \in C, K_{i, j} \rightarrow \overleftarrow{A}_{i, j}^{\prime} \\$R_{2}: \quad \forall i, j \in C, K_{i, j} \wedge \overleftarrow{A}_{i, j} \rightarrow \overleftarrow{A}_{i, j}^{\prime}" />

    * Where, K_ij is the external knowledge between tokens i and j, let say word relatedness from conceptnet.

    * Following results wehre achieved.
    <p align="center">
    <img width=600 src="images/first_order_logic_attention_results.png">
    <em>Source: Author</em>
    </p>

* Output decisions at Intermediate States
    <p align="center">
    <img width=600 src="images/first_order_logic_intermediate_output.png">
    <em>Source: Author</em>
    </p>

    * As can be seen, it directly modifies output decision, it can take augemented attention as inputs.





