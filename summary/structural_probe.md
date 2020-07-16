## A Structural Probe for Finding Syntax in Word Representations
### John Hewitt, Christopher D. Manning
### 2019, NAACL 2019, Standford

**Whats new** This paper proves that linear transformartion of vector space of BERT and ELMO embeddings does embed liguistic structure, i.e. dependency tree.

**How is it done**
* Linear transformation is learnt which would capture the linguist structure

* Model 1: distance between words in dependency trees is  as distance between two vector representation which are linear transformation of embeddings

    * <img src="https://i.upmath.me/svg/d_%7BB%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B%5Cell%7D%2C%20%5Cmathbf%7Bh%7D_%7Bj%7D%5E%7B%5Cell%7D%5Cright)%5E%7B2%7D%3D%5Cleft(B%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B%5Cell%7D-%5Cmathbf%7Bh%7D_%7Bj%7D%5E%7B%5Cell%7D%5Cright)%5Cright)%5E%7BT%7D%5Cleft(B%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B%5Cell%7D-%5Cmathbf%7Bh%7D_%7Bj%7D%5E%7B%5Cell%7D%5Cright)%5Cright)" alt="d_{B}\left(\mathbf{h}_{i}^{\ell}, \mathbf{h}_{j}^{\ell}\right)^{2}=\left(B\left(\mathbf{h}_{i}^{\ell}-\mathbf{h}_{j}^{\ell}\right)\right)^{T}\left(B\left(\mathbf{h}_{i}^{\ell}-\mathbf{h}_{j}^{\ell}\right)\right)" />
    * <img src="https://i.upmath.me/svg/%5Cmin%20_%7BB%7D%20%5Csum_%7B%5Cell%7D%20%5Cfrac%7B1%7D%7B%5Cleft%7Cs%5E%7B%5Cell%7D%5Cright%7C%5E%7B2%7D%7D%20%5Csum_%7Bi%2C%20j%7D%5Cleft%7Cd_%7BT%5E%7B%5Cell%7D%7D%5Cleft(w_%7Bi%7D%5E%7B%5Cell%7D%2C%20w_%7Bj%7D%5E%7B%5Cell%7D%5Cright)-d_%7BB%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%5E%7B%5Cell%7D%2C%20%5Cmathbf%7Bh%7D_%7Bj%7D%5E%7B%5Cell%7D%5Cright)%5E%7B2%7D%5Cright%7C" alt="\min _{B} \sum_{\ell} \frac{1}{\left|s^{\ell}\right|^{2}} \sum_{i, j}\left|d_{T^{\ell}}\left(w_{i}^{\ell}, w_{j}^{\ell}\right)-d_{B}\left(\mathbf{h}_{i}^{\ell}, \mathbf{h}_{j}^{\ell}\right)^{2}\right|" />

* Model 2: level of depth in dependence tree is learnt as squared norm of linear transformation of embeddings
    * <img src="https://i.upmath.me/svg/%5Cmin%20_%7BB%7D%20%5Csum_%7B%5Cell%7D%20%5Cfrac%7B1%7D%7B%5Cleft%7Cs_%7B%5Cell%7D%5Cright%7C%7D%20%5Csum_%7Bi%7D%5Cleft(%5Cleft%5C%7Cw_%7Bi%7D%5Cright%5C%7C-%5Cleft%5C%7CB%20h_%7Bi%7D%5Cright%5C%7C%5E%7B2%7D%5Cright)" alt="\min _{B} \sum_{\ell} \frac{1}{\left|s_{\ell}\right|} \sum_{i}\left(\left\|w_{i}\right\|-\left\|B h_{i}\right\|^{2}\right)" />

**What are major insights**
    * Following figure illustarte that UAAS score of aroun d 80 is observed and it is observed at hidden layer index of about 8 in 12 layer BERT, and aroubt 18 in 24 layer BERT.
      <p align="center">
        <img width=600 src="images/structure_probe_distance_layerwise.png">
        <em>Source: Author</em>
        </p>
    * As shown below, dependency tree depth is highly correlated highly with gold labels. 
    <p align="center">
        <img width=600 src="images/structure_probe_depth.png">
        <em>Source: Author</em>
        </p>
    * It can be seen that linear transformation would project BERT and ELMo vectors in to space of lignuist strcture, how dimensions of these projections impact performance... beyond 64 dimensions, it does not help much to increase dimensionality.
     <p align="center">
        <img width=600 src="images/structure_probe_transformation_dim.png">
        <em>Source: Author</em>
        </p>