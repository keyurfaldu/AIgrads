## Why do tree-based models still outperform deep learning on typical tabular data?
### Grinsztajn, L., Oyallon, E., & Varoquaux, G. (2022)
### Advances in neural information processing systems, 35, 507-520.


** Key Points **
* The major contribution from this paper is as follow
    * Prepare a tabular data for the benchmarking
    * Compare tree based and neural models, publish the raw results
    * Data transformations to discover the inductive bias in tree vs neural models


* Major findings regarding the inducative bias are

    * Neural Networks are biased towards smooth target functions. i.e. More smoothened targets helped NN in comparision to tree models. 

     <p align="center">
    <img width=600 src="images/tree_models_on_tabular_smoothend_target.png">
    <em>Source: Author</em>
    </p>


    * Uninformative features affect NNs more than the tree based models. The study was done by understanding the performance gap when the uninfromative features were removed.
    
    <p align="center">
    <img width=600 src="images/tree_models_on_tabular_uninformative_features.png">
    <em>Source: Author</em>
    </p>

    * NN models are invariant to rotational transformation of data
   <p align="center">
    <img width=600 src="images/tree_models_on_tabular_roatational_transform.png">
    <em>Source: Author</em>
    </p>

    