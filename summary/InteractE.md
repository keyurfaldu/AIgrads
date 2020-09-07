## InteractE: Improving Convolution-based Knowledge Graph Embeddings by Increasing Feature Interactions
### Shikhar Vashishth, Soumya Sanyal, Vikram Nitin, Nilesh Agrawal, Partha Talukdar
### AAAI 2020 [[arXiv](https://arxiv.org/pdf/1911.00219.pdf)]

**Whats New** Existing KG suffers from incompleteness, this paper propose a technique for link prediction task using three key contributions, feature permutation, feature reshaping and circular convolution. It gives SOTA performance.

**Key Contribution**
1. InteractE, a method to extend the expressive power of ConvE through feature permutations, "checkered" feature reshaing and circular convolution.
2. How interactions are increased in InteractE, and correlation between hetrogenous interactions and link prediction performance.

**How It Works**
* Context: ConvE
<img src="https://i.upmath.me/svg/%5Cpsi(s%2C%20r%2C%20o)%3Df%5Cleft(%5Coperatorname%7Bvec%7D%5Cleft(f%5Cleft(%5Cleft%5B%5Coverline%7Be_%7Bs%7D%7D%20%3B%20%5Coverline%7Be_%7Br%7D%7D%20%5Cstar%20w%5Cright%5D%5Cright)%5Cright)%20%5Cboldsymbol%7BW%7D%5Cright)%20e_%7B%5Cboldsymbol%7Bo%7D%7D" alt="\psi(s, r, o)=f\left(\operatorname{vec}\left(f\left(\left[\overline{e_{s}} ; \overline{e_{r}} \star w\right]\right)\right) \boldsymbol{W}\right) e_{\boldsymbol{o}}" />
    * e_s dash, and e_r dash  are 2D reshaping of e_s and e_r
    * star denotes the conv operations

* Reshaping: As we can see, e_s and e_r can be reshaped into 2D metrics, with following three thechniques.

    <p align="center">
        <img width=600 src="images/InteractE_reshaping.png">
        <em>Source: Author</em>
        </p>

* Interaction: It the number of possible triples, (x, y, M_k), where M_k is subset of reshaped 2D metric depending upon the kernel size, and x and y are elements of reshaped 2D metric. 
    * Interaction is hetrogeneous if x \in e_s, and y \in e_r.
    * Interaction is homogenous if both belongs to either e_s or e_r.
    * Note, in chequered reshaping there are maximum numbers of hetrogeneous interactions.

* Circular Convolution
    * With modulo operation it finds the elements to be convoluted. 
    <p align="center">
        <img width=600 src="images/InteractE_circular.png">
        <em>Source: Author</em>
        </p>

* Results:
    * Ablation study has shown that chequered reshaping and cicular convolution has given better accuracy.
    * On three datasets, it has produced better results then ConvE and RotatE, and other latest techniques.
    * MRR: mean reciprocal length, MR is the mean rank, H@10 is hit at 10, and H@1 is hit at 1.

    <p align="center">
        <img width=600 src="images/InteractE_results.png">
        <em>Source: Author</em>
        </p>





