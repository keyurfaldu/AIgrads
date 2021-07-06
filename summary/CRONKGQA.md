## Question Answering Over Temporal Knowledge Graphs.
### Saxena, Apoorv, Soumen Chakrabarti, and Partha Talukdar
### [[arXiv](https://arxiv.org/pdf/2106.01515.pdf)].


**Whats Unique**
This paper present question answering task over temporal knowledge graph. It has also created the temporal KG heuristically.

**How It Works**
* ComplEx is popular KG embedding method, which represents each entity e as a complex vector u_e \in C^D. Given subject entity s, object entity o and relation in between r, it has the score \phi for the fact as below:
<img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cphi(s%2C%20r%2C%20o)%20%26%3D%5CRe%5Cleft(%5Cleft%5Clangle%5Cboldsymbol%7Bu%7D_%7Bs%7D%2C%20%5Cboldsymbol%7Bv%7D_%7Br%7D%2C%20%5Cboldsymbol%7Bu%7D_%7Bo%7D%5E%7B%5Cstar%7D%5Cright%5Crangle%5Cright)%20%5C%5C%0A%26%3D%5CRe%5Cleft(%5Csum_%7Bd%3D1%7D%5E%7BD%7D%20%5Cboldsymbol%7Bu%7D_%7Bs%7D%5Bd%5D%20%5Cboldsymbol%7Bv%7D_%7Br%7D%5Bd%5D%20%5Cboldsymbol%7Bu%7D_%7Bo%7D%5Bd%5D%5E%7B%5Cstar%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\phi(s, r, o) &amp;=\Re\left(\left\langle\boldsymbol{u}_{s}, \boldsymbol{v}_{r}, \boldsymbol{u}_{o}^{\star}\right\rangle\right) \\
&amp;=\Re\left(\sum_{d=1}^{D} \boldsymbol{u}_{s}[d] \boldsymbol{v}_{r}[d] \boldsymbol{u}_{o}[d]^{\star}\right)
\end{aligned}" />

*  TComplEx, TNTComplE: It is an extension of ComplEx, where each timestamp t is also represented as vector w_t. So, the score of the claimed fact (s, o, r, t). 
<img src="https://i.upmath.me/svg/%20%5Cphi(s%2C%20r%2C%20o%2C%20t)%3D%5CRe%5Cleft(%5Cleft%5Clangle%5Cboldsymbol%7Bu%7D_%7Bs%7D%2C%20%5Cboldsymbol%7Bv%7D_%7Br%7D%2C%20%5Cboldsymbol%7Bu%7D_%7Bo%7D%5E%7B%5Cstar%7D%2C%20%5Cboldsymbol%7Bw%7D_%7Bt%7D%5Cright%5Crangle%5Cright)" alt=" \phi(s, r, o, t)=\Re\left(\left\langle\boldsymbol{u}_{s}, \boldsymbol{v}_{r}, \boldsymbol{u}_{o}^{\star}, \boldsymbol{w}_{t}\right\rangle\right)" />

* Core Idea: 

    * Architecture diagram can be seen as below:
    <p align="center">
        <img width=600 src="images/cronkgqa_arch.png">
        <em>Source: Author</em>
        </p>


    * Using TComplEx, temporal KG embeddings are learned. 
    * Fact sentence embeddings are derived using pretrained language model, like BERT. Afterwards, it is projected to the vector space of TComplEx, and treated as relation embeddings.
    * Entity Scoring Function: Temporal KG embeddings of subject entity and timestamp, and relation embeddings derived above, are used, and score is derived over all possible entities.


        <img src="https://i.upmath.me/svg/%20%0A%5Ctext%20%7B%20For%20each%20%7D%20e%20%5Cin%20%5Cmathbf%7BE%7D%20%5Ctext%20%7B%20as%20%7D%20%5C%5C%0A%5Cqquad%20%5Cboldsymbol%7B%5Cphi%7D_%7B%5Ctext%20%7Bent%20%7D%7D(e)%3D%5CRe%5Cleft(%5Cleft%5Clangle%5Cboldsymbol%7Bu%7D_%7Bs%7D%2C%20%5Cboldsymbol%7Bq%7D%20%5Cboldsymbol%7Be%7D_%7Be%20n%20t%7D%2C%20%5Cboldsymbol%7Bu%7D_%7Be%7D%5E%7B%5Cstar%7D%2C%20%5Cboldsymbol%7Bw%7D_%7Bt%7D%5Cright%5Crangle%5Cright)%0A" alt=" 
\text { For each } e \in \mathbf{E} \text { as } \\
\qquad \boldsymbol{\phi}_{\text {ent }}(e)=\Re\left(\left\langle\boldsymbol{u}_{s}, \boldsymbol{q} \boldsymbol{e}_{e n t}, \boldsymbol{u}_{e}^{\star}, \boldsymbol{w}_{t}\right\rangle\right)
" />

    * Time Scoring Function: Temporal KG embeddings of subject and object entities, and relation embeddings derived above are used, and score is derived over all possible times. 

        <img src="https://i.upmath.me/svg/%0A%5Ctext%7BFor%20each%20timestamp%20%7D%20t%20%5Cin%20%5Cmathbf%7BT%7D%20%5Ctext%20%7B%20as%20%7D%20%5C%5C%0A%26%5Cboldsymbol%7B%5Cphi%7D_%7B%5Cboldsymbol%7Bt%20i%20m%20e%7D%7D(t)%3D%5CRe%5Cleft(%5Cleft%5Clangle%5Cboldsymbol%7Bu%7D_%7Bs%7D%2C%20%5Cboldsymbol%7Bq%7D%20%5Cboldsymbol%7Be%7D_%7Bt%20i%20m%20e%7D%2C%20%5Cboldsymbol%7Bu%7D_%7Bo%7D%5E%7B%5Cstar%7D%2C%20%5Cboldsymbol%7Bw%7D_%7Bt%7D%5Cright%5Crangle%5Cright)%0A" alt="
\text{For each timestamp } t \in \mathbf{T} \text { as } \\
&amp;\boldsymbol{\phi}_{\boldsymbol{t i m e}}(t)=\Re\left(\left\langle\boldsymbol{u}_{s}, \boldsymbol{q} \boldsymbol{e}_{t i m e}, \boldsymbol{u}_{o}^{\star}, \boldsymbol{w}_{t}\right\rangle\right)
" />

    * It outperfoms other baseline methods which are not using temporal KG embeddings significantly.