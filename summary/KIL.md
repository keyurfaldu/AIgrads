## Knowledge Infused Learning (K-IL): Towards Deep Incorporation of Knowledge in Deep Learning
### Ugur Kursuncu, Manas Gaur, Amit Sheth 
### AAAI 2020

**Whats new**
This paper is a poisiton or a framework paper which demonstrate the need of two extremes to merge, conceptual and probabilistic representations. Which can be thought as bottomup deep learning with top-down symbolic computing. 

**Underlying concepts**
* ML systems are probablistic in nature, and it poses fundamental challange because of its relaince on underlying training data, statistical significance of the patterns present in it. Because of which it can end up generating false alarm, or it can missout on obvious settings. These challanges are broadly classified as follow:
    * dependency on large datasets 
    * bias in dataset
    * sparsity of the data
    * lack of explainability
    * convergence information
    * complexity of architecture
    * false alarms

* This poistion paper answers mainly following:
    * How do we decide whether to infuse knowledge or not
    * How to merge latent representations between layers
    * How to propagate the knowledge through the learned latent representation?

**How it works**
* KG embeddings can be thought as representation concepts enriched by relationships.
* Knowlege infusion:
    * After each epoc, KG knowledge would be infused
    * It has mainly two constituent:
        * Knowledge-Aware Loss Function: It is to minimise D_KL of h_T vs K_e, such that difference between D_KL of h_T and h_T-1 should be with in threshold (or minimised too). Where, D_KL is KL divergence of hidden representation vs knowlege graph embedding.

        <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Br%7D%0A%5Cmathrm%7BK%7D-%5Cmathrm%7BLF%7D%3D%5Cmin%20%5Cmathbf%7BD%7D_%7BK%20L%7D%5Cleft(%5Coverrightarrow%7Bh_%7BT%7D%7D%20%5C%7C%20%5Cvec%7BK%7D_%7Be%7D%5Cright)%20%5C%5C%0A%5Ctext%20%7Bs.t.D%20%7D_%7BK%20L%7D%5Cleft(%5Coverrightarrow%7Bh_%7BT%7D%7D%20%5C%7C%20%5Cvec%7BK%7D_%7Be%7D%5Cright)%3C%5Cmathbf%7BD%7D_%7BK%20L%7D%5Cleft(h_%7BT-1%7D%5E%7B%5Crightarrow%7D%20%5C%7C%20%5Cvec%7BK%7D_%7Be%7D%5Cright)%0A%5Cend%7Barray%7D" alt="\begin{array}{r}
\mathrm{K}-\mathrm{LF}=\min \mathbf{D}_{K L}\left(\overrightarrow{h_{T}} \| \vec{K}_{e}\right) \\
\text {s.t.D }_{K L}\left(\overrightarrow{h_{T}} \| \vec{K}_{e}\right)&lt;\mathbf{D}_{K L}\left(h_{T-1}^{\rightarrow} \| \vec{K}_{e}\right)
\end{array}" />

        * Knowledge Modulation Function:  It merges differntial knowledge representation with the partially learned representation. It need vector space transformation, and its weights have to be learnt as function of differential knowledge.

* Following architecture diagram illustrate the process along with algorithm

    <p align="center">
        <img width=600 src="images/KIL_arch.png">
        <em>Source: Author</em>
        </p>

    <p align="center">
        <img width=600 src="images/KIL_network.png">
        <em>Source: Author</em>
        </p>

    <p align="center">
        <img width=600 src="images/KIL_algo.png">
        <em>Source: Author</em>
        </p>

**Reflection**
It presents good insights, specifically how KG embedding can be mixed at hidden layer, and how loss function can have convergence critera, and back propogation of hidden representation weights as well as how updated KG embedding loop back in the system, to arrive at an equilibrium.
Although, it would have been great to have implementation, experiments and results along with. 


