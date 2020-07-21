## Human Attention Maps for Text Classification: Do Humans and Neural Networks Focus on the Same Words?

### Cansu Sen, Thomas Hartvigsen, Biao Yin, Xiangnan Kong, Elke Rundensteiner

### ACL, 2020

**Whats New** A new dataset containing human attention labels for about 15000 Yelp reviews, and a method demonstrating BI-RNN has better similarity with human attention maps. 

**How is it done**
* A large-scale collection of 15,000 human attention maps as a companion to the publicly-available Yelp Review dataset.
* New metrics to give better insights
    * behavioral similarity

    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bc%7D%0A%5Ctext%20%7B%20Pairwise%20%7D%20%5Coperatorname%7BSim%7D_%7Bi%7D%3DA%20U%20C%5Cleft(%5Cmathrm%7BHAM%7D_%7Bi%7D%2C%20%5Cmathrm%7BMAM%7D_%7Bi%7D%5Cright)%20%5C%5C%0A%5Ctext%20%7B%20Behavioralsim%20%7D(M%2C%20H)%3D%5Cfrac%7B1%7D%7B%7C%5Cmathcal%7BD%7D%7C%7D%20%5Csum_%7Bi%7D%5Cleft(%5Ctext%20%7B%20Pairwise%20%7D%20%5Coperatorname%7Bsim%7D_%7Bi%7D%5Cright)%0A%5Cend%7Barray%7D" alt="\begin{array}{c}
    \text { Pairwise } \operatorname{Sim}_{i}=A U C\left(\mathrm{HAM}_{i}, \mathrm{MAM}_{i}\right) \\
    \text { Behavioralsim }(M, H)=\frac{1}{|\mathcal{D}|} \sum_{i}\left(\text { Pairwise } \operatorname{sim}_{i}\right)
    \end{array}" />

    * Lexical similarity

        <img src="https://i.upmath.me/svg/%5Coperatorname%7BLS%7D(M%2C%20H)%3D%5Coperatorname%7Bcorr%7D%5Cleft(%5Coperatorname%7Bdist%7D%5Cleft(%5Coperatorname%7Bwords%7D_%7BH%7D%5Cright)%2C%20%5Coperatorname%7Bdist%7D%5Cleft(%5Coperatorname%7Bwords%7D_%7BM%7D%5Cright)%5Cright)" alt="\operatorname{LS}(M, H)=\operatorname{corr}\left(\operatorname{dist}\left(\operatorname{words}_{H}\right), \operatorname{dist}\left(\operatorname{words}_{M}\right)\right)" />

        <img src="https://i.upmath.me/svg/%5Ctext%20%7B%20AdjustedLS%20%7D%3D%5Cfrac%7B%5Cmathrm%7BLS%7D(M%2C%20H)-%5Cmathrm%7BLS%7D(R%2C%20H)%7D%7B1-%5Cmathrm%7BLS%7D(R%2C%20H)%7D" alt="\text { AdjustedLS }=\frac{\mathrm{LS}(M, H)-\mathrm{LS}(R, H)}{1-\mathrm{LS}(R, H)}" />

        * Where, LS(R, H) is random selection of tokens. Note, if human has selected k tokens, then top-K tokens were chosen by model.

    * context-dependency

        * Note, ratio of poisitve words vs negative words selected. For HAM, it can be computed as below.

        <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0Ap_%7B-%7D%20%5Ctext%20%7Bwords%7D%3D%5Coperatorname%7Bget%7D_%7B-%7D%20%5Ctext%20%7Bwords%7D%5Cleft(%5Ctext%20%7BHAM%7D_%7B%5Cmathcal%7BD%7D%7D%2C%20Y%3D1%5Cright)%20%5C%5C%0A%5Ctext%20%7Bn.words%7D%3D%5Coperatorname%7Bget%7D_%7B-%7D%20%5Coperatorname%7Bwords%7D%5Cleft(%5Ctext%20%7BHAM%7D_%7B%5Cmathcal%7BD%7D%7D%2C%20Y%3D0%5Cright)%20%5C%5C%0A%5Cqquad%20%5Cbegin%7Baligned%7D%0AC%20S%20S%20R_%7Bp%7D%20%26%3D%5Cfrac%7B%5Cmid%20p_%7B-%7D%20%5Ctext%20%7Bwords%7D%20%5Ccap%20%5Cmathcal%7BN%7D%20%5Cmid%7D%7B%5Cmid%20p_%7B-%7D%20%5Ctext%20%7Bwords%7D%20%5Ccap%20%5Cmathcal%7BP%7D%20%5Cmid%7D%20%5C%5C%0A%5Coperatorname%7BCSSR%7D_%7Bn%7D%3D%26%20%5Cfrac%7B%5Cmid%20n_%7B-%7D%20%5Ctext%20%7Bwords%20%7D%20%5Ccap%20%5Cmathcal%7BP%7D%20%5Cmid%7D%7B%5Cmid%20n_%7B-%7D%20%5Ctext%20%7Bwords%7D%20%5Ccap%20%5Cmathcal%7BN%7D%20%5Cmid%7D%0A%5Cend%7Baligned%7D%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
        p_{-} \text {words}=\operatorname{get}_{-} \text {words}\left(\text {HAM}_{\mathcal{D}}, Y=1\right) \\
        \text {n.words}=\operatorname{get}_{-} \operatorname{words}\left(\text {HAM}_{\mathcal{D}}, Y=0\right) \\
        \qquad \begin{aligned}
        C S S R_{p} &amp;=\frac{\mid p_{-} \text {words} \cap \mathcal{N} \mid}{\mid p_{-} \text {words} \cap \mathcal{P} \mid} \\
        \operatorname{CSSR}_{n}=&amp; \frac{\mid n_{-} \text {words } \cap \mathcal{P} \mid}{\mid n_{-} \text {words} \cap \mathcal{N} \mid}
        \end{aligned}
        \end{array}" />

* Findings:
    * Behavioural similairty of Bi-RNN was higher among all models choices. And, it was much higher for CAM (i.e. consensus attention map)
    * As, the review length increases, the behavioral similarity score decreases for all model choices. 
    * Both lexical similarity and cross sentiment score also observed similar findings, where Bi-LSTM outperfomed other models.

