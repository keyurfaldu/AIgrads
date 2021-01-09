## BoxE: A Box Embedding Model for Knowledge Base Completion
### Abboud, Ralph, Ismail Ceylan, Thomas Lukasiewicz, and Tommaso Salvatori. 
### Advances in Neural Information Processing Systems 33 (2020).[[NIPS](https://papers.nips.cc/paper/2020/file/6dbbe6abe5f14af882ff977fc3f35501-Paper.pdf)]

**Whats Unique**
This paper presents a novel spatio-transational KG embedding technique, BoxE for knowledge base completion. BoxE can both capture and inject rules from rich classes of rich languages, and naturally applies to higher-arity relationships. 

**How Does It Work**
* Knowledge Base can be viewed as collection of facts of the form r(e1, e2, .. , en)
* KB is known as KG when all the relations are binary (composed of two entities).

* In BoxE, 
    * every entity e_i \in E is represented by two vectors. e_i, b_i \in R_d. 
        * e_i defines the base position and b_i defines its transational bump
        * The final embedding of an entity e_i relative to the fact r(e1, e2, .. e_n) is

        <img src="https://i.upmath.me/svg/e_%7Bi%7D%5E%7Br%5Cleft(e_%7B1%7D%2C%20%5Cldots%2C%20e_%7Bn%7D%5Cright)%7D%3D%5Cleft(e_%7Bi%7D-b_%7Bi%7D%5Cright)%2B%5Csum_%7B1%20%5Cleq%20j%20%5Cleq%20n%7D%20b_%7Bj%7D" alt="e_{i}^{r\left(e_{1}, \ldots, e_{n}\right)}=\left(e_{i}-b_{i}\right)+\sum_{1 \leq j \leq n} b_{j}" />

    * every relation r is represented by n hyper-rectanges. boxes r(1), r(2), ..., r(n) \in R^d
    
* Following figure denotes, entitites base embeddings and bump, and box for each n-arity of relation.

<p align="center">
    <img width=600 src="images/BoxE_illustration.png">
    <em>Source: Author</em>
    </p>


* Distance function: 
    * An entity embedding is adjusted with the translation bump
    * If it e_i is found in r(i) box, its good. With in box it recieves lesser penalty for being away from the center, but high penalty when it is out of the box. Following function capture this.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%26%5Coperatorname%7Bdist%7D%5Cleft(e_%7Bi%7D%5E%7Br%5Cleft(e_%7B1%7D%2C%20%5Cldots%2C%20e_%7Bn%7D%5Cright)%7D%2C%20r%5E%7B(i)%7D%5Cright)%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Bll%7D%0A%5Cleft%7Ce_%7Bi%7D%5E%7Br%5Cleft(e_%7B1%7D%2C%20%5Cldots%2C%20e_%7Bn%7D%5Cright)%7D-c%5E%7B(i)%7D%5Cright%7C%20%5Coslash%20%5Cboldsymbol%7Bw%7D%5E%7B(i)%7D%20%26%20%5Ctext%20%7B%20if%20%7D%20e_%7Bi%7D%20%5Cin%7B%5Cboldsymbol%7Br%7D%7D%5E%7B(i)%7D%20%5C%5C%0A%5Cleft%7Ce_%7B%5Cboldsymbol%7Bi%7D%7D%5E%7B%5Cboldsymbol%7Br%7D%5Cleft(e_%7B1%7D%2C%20%5Cldots%2C%20e_%7Bn%7D%5Cright)%7D-%5Cboldsymbol%7Bc%7D%5E%7B(i)%7D%5Cright%7C%20%5Ccirc%20%5Cboldsymbol%7Bw%7D%5E%7B(i)%7D-%5Ckappa%20%26%20%5Ctext%20%7B%20otherwise%20%7D%0A%5Cend%7Barray%7D%5Cright.%5C%5C%0A%26%5Ctext%20%7B%20where%20%7D%20%5Ckappa%3D0.5%20%5Ccirc%5Cleft(%5Cboldsymbol%7Bw%7D%5E%7B(i)%7D-1%5Cright)%20%5Ccirc%5Cleft(%5Cboldsymbol%7Bw%7D%5E%7B(i)%7D-%5Cboldsymbol%7Bw%7D%5E%7B(i)%5E%7B%5Ccirc-1%7D%7D%5Cright)%2C%20%5Ctext%20%7B%20is%20a%20width-dependent%20factor%20%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned} &amp;\operatorname{dist}\left(e_{i}^{r\left(e_{1}, \ldots, e_{n}\right)}, r^{(i)}\right)=\left\{\begin{array}{ll} \left|e_{i}^{r\left(e_{1}, \ldots, e_{n}\right)}-c^{(i)}\right| \oslash \boldsymbol{w}^{(i)} &amp; \text { if } e_{i} \in{\boldsymbol{r}}^{(i)} \\ \left|e_{\boldsymbol{i}}^{\boldsymbol{r}\left(e_{1}, \ldots, e_{n}\right)}-\boldsymbol{c}^{(i)}\right| \circ \boldsymbol{w}^{(i)}-\kappa &amp; \text { otherwise } \end{array}\right.\\&amp;\text { where } \kappa=0.5 \circ\left(\boldsymbol{w}^{(i)}-1\right) \circ\left(\boldsymbol{w}^{(i)}-\boldsymbol{w}^{(i)^{\circ-1}}\right), \text { is a width-dependent factor } \end{aligned}" />

    * Following figure shows how distance function varies for different scenarios.
    
    <p align="center">
    <img width=600 src="images/BoxE_distance_function.png">
    <em>Source: Author</em>
    </p>

* Objective function to minimise is:

<img src="https://i.upmath.me/svg/%5Coperatorname%7Bscore%7D%5Cleft(r%5Cleft(e_%7B1%7D%2C%20%5Cldots%2C%20e_%7Bn%7D%5Cright)%5Cright)%3D%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%5Cleft%5C%7C%5Coperatorname%7Bdist%7D%5Cleft(e_%7Bi%7D%5E%7Br%5Cleft(e_%7B1%7D%2C%20%5Cldots%2C%20e_%7Bn%7D%5Cright)%7D%2C%20r%5E%7B(i)%7D%5Cright)%5Cright%5C%7C_%7Bx%7D" alt="\operatorname{score}\left(r\left(e_{1}, \ldots, e_{n}\right)\right)=\sum_{i=1}^{n}\left\|\operatorname{dist}\left(e_{i}^{r\left(e_{1}, \ldots, e_{n}\right)}, r^{(i)}\right)\right\|_{x}" />

* It has outperformed other KG embeddings like TransE, RotateE, ComplEx, DistMult etc