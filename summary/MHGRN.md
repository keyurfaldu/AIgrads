## Scalable multi-hop relational reasoning for knowledge-aware question answering
### Feng, Yanlin, Xinyue Chen, Bill Yuchen Lin, Peifeng Wang, Jun Yan, and Xiang Ren. 
### arXiv preprint [[arXiv:2005.00646](https://arxiv.org/pdf/2005.00646.pdf)] (2020).

**Whats Unique**
This paper presnet's knowledge aware commonsense answering technique, where it combines infusing knowledge over multi-hop paths with GNN approch. It uses ConceptNet to get the subgraph and infuse it on MultiHop datasets like CommonsenseQA and O    penBookQA.

**Motivation**
Following example shows the motivation for the problem, where how ConceptNet can be used to solve a multi-hop problem.

<p align="center">
    <img width=600 src="images/MHGRN_motivation.png">
    <em>Source: Author</em>
    </p>

**Overview** of current knowledge aware QA systems is as follow:
<p align="center">
    <img width=600 src="images/MHGRN_overview.png">
    <em>Source: Author</em>
    </p>
There are mainly two types of models, GNN and Pathbased. This paper aims at leveraging both these techniques.

**Architecture**
Architecture of MHGRN is shown below in the figure. 

<p align="center">
    <img width=600 src="images/MHGRN_architecture.png">
    <em>Source: Author</em>
    </p>

First, subgraph is obtained from the ConceptNet by looking up all the nodes and preserving their relationships.

As can be seen, the representation for the nodes are transformed using the relationships of path (max k). And, final represenation of node is weighted sum of transformed representation as results of multiple paths. 

<img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cboldsymbol%7Bz%7D_%7Bi%7D%5E%7Bk%7D%20%26%3D%5Csum_%7B%5Cleft(j%2C%20r_%7B1%7D%2C%20%5Cldots%2C%20r_%7Bk%7D%2C%20i%5Cright)%20%5Cin%20%5CPhi_%7Bk%7D%7D%20%5Calpha%5Cleft(j%2C%20r_%7B1%7D%2C%20%5Cldots%2C%20r_%7Bk%7D%2C%20i%5Cright)%20%2F%20d_%7Bi%7D%5E%7Bk%7D%20%5Ccdot%20%5Cboldsymbol%7BW%7D_%7B0%7D%5E%7BK%7D%20%5Ccdots%20%5Cboldsymbol%7BW%7D_%7B0%7D%5E%7Bk%2B1%7D%20%5Cboldsymbol%7BW%7D_%7Br_%7Bk%7D%7D%5E%7Bk%7D%20%5Ccdots%20%5Cboldsymbol%7BW%7D_%7Br_%7B1%7D%7D%5E%7B1%7D%20%5Cboldsymbol%7Bx%7D_%7Bj%7D%20%5Cquad(1%20%5Cleq%20k%20%5Cleq%20K)%20%5Cend%7Baligned%7D" alt="\begin{aligned} \boldsymbol{z}_{i}^{k} &amp;=\sum_{\left(j, r_{1}, \ldots, r_{k}, i\right) \in \Phi_{k}} \alpha\left(j, r_{1}, \ldots, r_{k}, i\right) / d_{i}^{k} \cdot \boldsymbol{W}_{0}^{K} \cdots \boldsymbol{W}_{0}^{k+1} \boldsymbol{W}_{r_{k}}^{k} \cdots \boldsymbol{W}_{r_{1}}^{1} \boldsymbol{x}_{j} \quad(1 \leq k \leq K) \end{aligned}" />

* Note, W_0^K padding matrix are added, just to make sure the scale of final representation remains similar.

Final representation is, weighted sub from all differnt path,

<img src="https://i.upmath.me/svg/z_%7Bi%7D%3D%5Csum_%7Bk%3D1%7D%5E%7BK%7D%20%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cright.%24%20bilinear%20%24%5Cleft.%5Cleft(s%2C%20z_%7Bi%7D%5E%7Bk%7D%5Cright)%5Cright)%20%5Ccdot%20z_%7Bi%7D%5E%7Bk%7D" alt="z_{i}=\sum_{k=1}^{K} \operatorname{softmax}\left(\right.$ bilinear $\left.\left(s, z_{i}^{k}\right)\right) \cdot z_{i}^{k}" />

MHGRN methods have given perforamnce gain on CommonsenseQA, and OpenBookQA tasks.


