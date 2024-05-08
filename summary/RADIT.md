## Ra-dit: Retrieval-augmented dual instruction tuning.
* Lin, X. V., Chen, X., Chen, M., Shi, W., Lomeli, M., James, R., ... & Yih, S. (2023). 
* arXiv preprint arXiv:2310.01352 [[PDF](https://arxiv.org/pdf/2310.01352)]

# Key Points
* Retrieval augmented langauge models (RALMs) improve performance by accessing long-tail and up-to-date knowledge. 
* Existing approach to RALMs is (i) Retriever specific modifications to LM pre-training. (ii) post-hoc integration of data-store.
* RADIT mainly has
    * fine tunining pre-trained LM to better use retrieved information. 
    * fine tuninig retreiver to return more relevant results
* RALM improves 0-zhot performance by around 8.9% and 1.4% in 5-shot settings.
* Retriever uses DRAGON+ - a state of the art dense encoder model trained with contrastive learning objective. 
* Chained Objective: Retreival and Generation.
* <p align="center"><img align="center" src="https://i.upmath.me/svg/pLM(y%7Cx%2C%20C)%20%3D%20X_%7Bc%20%5Cin%20C%7D%20pLM(y%7Cc%2C%20x)%20%C2%B7%20pR(c%7Cx)" alt="pLM(y|x, C) = X_{c \in C} pLM(y|c, x) · pR(c|x)" /></p>
# Language model fine tuning: 
* for each (x,y) record, it fetches top 5 contexts, and for each context, it generate a training pair (y, (c, x)). 
* <p align="center"><img align="center" src="https://i.upmath.me/svg/L(D_L)%20%3D%20%E2%88%92%5Csum_i%5Csum_jlogp_%7BLM%7D(y_i%7Cc_%7Bij%7D%20.%20x_i)" alt="L(D_L) = −\sum_i\sum_jlogp_{LM}(y_i|c_{ij} . x_i)" /></p>
# Retriever fine tuning:
* learn KL divergence function for each context c:  <p align="center"><img align="center" src="https://i.upmath.me/svg/L(D_R)%20%3D%20E_%7B(x%2Cy)%E2%88%88D_R%7D%20KL(p_R(c%7Cx)%2C%20p_%7BLSR%7D(c%7Cx%2C%20y))" alt="L(D_R) = E_{(x,y)∈D_R} KL(p_R(c|x), p_{LSR}(c|x, y))" /></p>
* where, $p_{LSR}$ is generalized version of LM-Supervised Retrieval, Shi et al., 2023b.
* <p align="center"><img align="center" src="https://i.upmath.me/svg/p_%7BLSR%7D(c%7Cx%2C%20y)%20%3D%20%5Cfrac%7Bexp%20(p_%7BLM%7D(y%7Cc%20%E2%97%A6%20x)%2F%5Ctau%20)%7D%7B%5Csum_%7Bc'%5CinC%7D%0Aexp%20(p_%7BLM%7D(y%7Cc%E2%80%B2%20%E2%97%A6%20x)%2F%5Ctau%20)%7D" alt="p_{LSR}(c|x, y) = \frac{exp (p_{LM}(y|c ◦ x)/\tau )}{\sum_{c'\inC}
# Results
* Following figure cites the results
<p align="center">
<img width=600 src="images/RADIT_results.png">
<em>Source: Author</em>
</p>
 




