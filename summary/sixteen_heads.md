## Are Sixteen Heads Really Better than One?
### Paul Michel, Omer Levy, Graham Neubig
### NIPS, 2019

* Two major observations:
    * Large percentage of attention heads can be removed without impacting performance
    * Some layers can be even reduced to a single head.

* Approach note
    * One-head-masking: Individual each head was masked and its impact on accuacy was monitored. As in the figure below, majority of the heads can be removed individually without impacting performance.

    <p align="center">
    <img width=600 src="images/one_head_masking_histogram.png">
    <em>Source: Author</em>
    </p>

    * Ablating all heads but one: Experiment was done for each layer, where only one best head was kept. And, most of the layers can be reduced to single layer without impacting the performance much. Note each experiment was limited to one layer at a time.

    * Scatter plot shows that when individual heads are removed, its performance impact on one dataset has a high positive correlation with other dataset.

    * Iterative pruning of attention heads
        * Importance of each head was derived by taking derivative of loss over weighing parameter sai for that head.
        
        <img src="https://i.upmath.me/svg/%5Coperatorname%7BMHAtt%7D(%5Cmathbf%7Bx%7D%2C%20q)%3D%5Csum_%7Bh%3D1%7D%5E%7BN_%7Bh%7D%7D%20%5Cxi_%7Bh%7D%20%5Coperatorname%7BAtt%7D_%7BW_%7Bk%7D%5E%7Bh%7D%2C%20W_%7Bq%7D%5E%7Bh%7D%2C%20W_%7Bv%7D%5E%7Bh%7D%2C%20W_%7Bo%7D%5E%7Bh%7D%7D(%5Cmathbf%7Bx%7D%2C%20q)" alt="\operatorname{MHAtt}(\mathbf{x}, q)=\sum_{h=1}^{N_{h}} \xi_{h} \operatorname{Att}_{W_{k}^{h}, W_{q}^{h}, W_{v}^{h}, W_{o}^{h}}(\mathbf{x}, q)" />


        <img src="https://i.upmath.me/svg/I_%7Bh%7D%3D%5Cmathbb%7BE%7D_%7Bx%20%5Csim%20X%7D%5Cleft%7C%5Cfrac%7B%5Cpartial%20%5Cmathcal%7BL%7D(x)%7D%7B%5Cpartial%20%5Cxi_%7Bh%7D%7D%5Cright%7C" alt="I_{h}=\mathbb{E}_{x \sim X}\left|\frac{\partial \mathcal{L}(x)}{\partial \xi_{h}}\right|" />


        <img src="https://i.upmath.me/svg/I_%7Bh%7D%3D%5Cmathbb%7BE%7D_%7Bx%20%5Csim%20X%7D%5Cleft%7C%5Coperatorname%7BAtt%7D_%7Bh%7D(x)%5E%7BT%7D%20%5Cfrac%7B%5Cpartial%20%5Cmathcal%7BL%7D(x)%7D%7B%5Cpartial%20%5Coperatorname%7BAtt%7D_%7Bh%7D(x)%7D%5Cright%7C" alt="I_{h}=\mathbb{E}_{x \sim X}\left|\operatorname{Att}_{h}(x)^{T} \frac{\partial \mathcal{L}(x)}{\partial \operatorname{Att}_{h}(x)}\right|" />

        * Based on importance, iterative pruning of each head was done, and its impact can be seen as below:

        <p align="center">
        <img width=600 src="images/iterative_head_masking.png">
        <em>Source: Author</em>
        </p>

        * As shown above, around 20-30% heads can be pruned. 

        * Also, it not only reduces numbers of paramters but also inference speed.

    * Effect of pruning head during training time was also measured, and it was inferred heads can be pruned early in training (not in very begining though) without impacting performance much.
