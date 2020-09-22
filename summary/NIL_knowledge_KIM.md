## Neural Natural Language Inference Models Enhanced with External Knowledge
### Qian Chen et al
### ACL 2018

**Whats New**

This paper investigates the impact of integrating external knowledge from WordNet about the pairs of the words at co-attention level, local infernce collection, and knowledge-enhanced composition.

**How It Works**
Following figure illustrates the approach
    <p align="center">
    <img width=600 src="images/NIL_knowledge_KIM_illustration.png">
    <em>Source: Author</em>
    </p>

As shown in the figure, it integrates external knowledge at different constructs

* External lexical knowledge relation:
    * r \in R^d_r, d_r = 5, Synonymy, Antonymy, Hypernymy, Hyponymy, Co-hyponyms. Statistics about these features are as follow:
    <p align="center">
    <img width=600 src="images/NIL_knowledge_KIM_lexical_stats.png">
    <em>Source: Author</em>
    </p>


* Knowledge enriched Co-attention:

    <img src="https://i.upmath.me/svg/e_%7Bi%20j%7D%3D%5Cleft(%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bs%7D%5Cright)%5E%7B%5Cmathrm%7BT%7D%7D%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bs%7D%2BF%5Cleft(%5Cboldsymbol%7Br%7D_%7Bi%20j%7D%5Cright)" alt="e_{i j}=\left(\boldsymbol{a}_{i}^{s}\right)^{\mathrm{T}} \boldsymbol{b}_{j}^{s}+F\left(\boldsymbol{r}_{i j}\right)" />

    * Attention weighted alignment vector for hypothesis and premise are as follow:

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Calpha_%7Bi%20j%7D%20%26%3D%5Cfrac%7B%5Cexp%20%5Cleft(e_%7Bi%20j%7D%5Cright)%7D%7B%5Csum_%7Bk%3D1%7D%5E%7Bn%7D%20%5Cexp%20%5Cleft(e_%7Bi%20k%7D%5Cright)%7D%2C%20%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bc%7D%3D%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bi%20j%7D%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bs%7D%20%5C%5C%20%5Cbeta_%7Bi%20j%7D%20%26%3D%5Cfrac%7B%5Cexp%20%5Cleft(e_%7Bi%20j%7D%5Cright)%7D%7B%5Csum_%7Bk%3D1%7D%5E%7Bm%7D%20%5Cexp%20%5Cleft(e_%7Bk%20j%7D%5Cright)%7D%2C%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bc%7D%3D%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%20%5Cbeta_%7Bi%20j%7D%20%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bs%7D%20%5Cend%7Baligned%7D" alt="\begin{aligned} \alpha_{i j} &amp;=\frac{\exp \left(e_{i j}\right)}{\sum_{k=1}^{n} \exp \left(e_{i k}\right)}, \boldsymbol{a}_{i}^{c}=\sum_{j=1}^{n} \alpha_{i j} \boldsymbol{b}_{j}^{s} \\ \beta_{i j} &amp;=\frac{\exp \left(e_{i j}\right)}{\sum_{k=1}^{m} \exp \left(e_{k j}\right)}, \boldsymbol{b}_{j}^{c}=\sum_{i=1}^{m} \beta_{i j} \boldsymbol{a}_{i}^{s} \end{aligned}" />

* Local Inference Collection with External Knowledge

    <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bm%7D%3DG%5Cleft(%5Cleft%5B%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bs%7D%20%3B%20%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bc%7D%20%3B%20%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bs%7D-%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bc%7D%20%3B%20%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bs%7D%20%5Ccirc%20%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bc%7D%20%3B%20%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bi%20j%7D%20%5Cboldsymbol%7Br%7D_%7Bi%20j%7D%5Cright%5D%5Cright)" alt="\boldsymbol{a}_{i}^{m}=G\left(\left[\boldsymbol{a}_{i}^{s} ; \boldsymbol{a}_{i}^{c} ; \boldsymbol{a}_{i}^{s}-\boldsymbol{a}_{i}^{c} ; \boldsymbol{a}_{i}^{s} \circ \boldsymbol{a}_{i}^{c} ; \sum_{j=1}^{n} \alpha_{i j} \boldsymbol{r}_{i j}\right]\right)" />
    <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bm%7D%3DG%5Cleft(%5Cleft%5B%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bs%7D%2C%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bc%7D%20%3B%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bs%7D-%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bc%7D%20%3B%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bs%7D%20%5Ccirc%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bc%7D%20%3B%20%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%20%5Cbeta_%7Bi%20j%7D%20%5Cboldsymbol%7Br%7D_%7Bj%20i%7D%5Cright%5D%5Cright)" alt="\boldsymbol{b}_{j}^{m}=G\left(\left[\boldsymbol{b}_{j}^{s}, \boldsymbol{b}_{j}^{c} ; \boldsymbol{b}_{j}^{s}-\boldsymbol{b}_{j}^{c} ; \boldsymbol{b}_{j}^{s} \circ \boldsymbol{b}_{j}^{c} ; \sum_{i=1}^{m} \beta_{i j} \boldsymbol{r}_{j i}\right]\right)" />

* Knowledge-Enhanced Inference Composition
    * Compositions can be thought as hidden representation of biLSTM layer

        <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bv%7D%3D%5Coperatorname%7BComposition%7D%5Cleft(%5Cboldsymbol%7Ba%7D%5E%7Bm%7D%2C%20i%5Cright)" alt="\boldsymbol{a}_{i}^{v}=\operatorname{Composition}\left(\boldsymbol{a}^{m}, i\right)" />
        <img src="https://i.upmath.me/svg/%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bv%7D%3D%5Coperatorname%7BComposition%7D%5Cleft(%5Cboldsymbol%7Bb%7D%5E%7Bm%7D%2C%20j%5Cright)" alt="\boldsymbol{b}_{j}^{v}=\operatorname{Composition}\left(\boldsymbol{b}^{m}, j\right)" />

    * Attention-and-lexical-knwoledge weighted pooling is computed as below:

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cboldsymbol%7Ba%7D%5E%7B%5Cmathrm%7Bw%7D%7D%20%26%3D%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%20%5Cfrac%7B%5Cexp%20%5Cleft(H%5Cleft(%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bi%20j%7D%20%5Cboldsymbol%7Br%7D_%7Bi%20j%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%20%5Cexp%20%5Cleft(H%5Cleft(%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Calpha_%7Bi%20j%7D%20%5Cboldsymbol%7Br%7D_%7Bi%20j%7D%5Cright)%5Cright)%7D%20%5Cboldsymbol%7Ba%7D_%7Bi%7D%5E%7Bv%7D%20%5C%5C%20%5Cboldsymbol%7Bb%7D%5E%7B%5Cmathrm%7Bw%7D%7D%20%26%3D%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Cfrac%7B%5Cexp%20%5Cleft(H%5Cleft(%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%20%5Cbeta_%7Bi%20j%7D%20%5Cboldsymbol%7Br%7D_%7Bj%20i%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20%5Cexp%20%5Cleft(H%5Cleft(%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%20%5Cbeta_%7Bi%20j%7D%20%5Cboldsymbol%7Br%7D_%7Bj%20i%7D%5Cright)%5Cright)%7D%20%5Cboldsymbol%7Bb%7D_%7Bj%7D%5E%7Bv%7D%20%5Cend%7Baligned%7D" alt="\begin{aligned} \boldsymbol{a}^{\mathrm{w}} &amp;=\sum_{i=1}^{m} \frac{\exp \left(H\left(\sum_{j=1}^{n} \alpha_{i j} \boldsymbol{r}_{i j}\right)\right)}{\sum_{i=1}^{m} \exp \left(H\left(\sum_{j=1}^{n} \alpha_{i j} \boldsymbol{r}_{i j}\right)\right)} \boldsymbol{a}_{i}^{v} \\ \boldsymbol{b}^{\mathrm{w}} &amp;=\sum_{j=1}^{n} \frac{\exp \left(H\left(\sum_{i=1}^{m} \beta_{i j} \boldsymbol{r}_{j i}\right)\right)}{\sum_{j=1}^{n} \exp \left(H\left(\sum_{i=1}^{m} \beta_{i j} \boldsymbol{r}_{j i}\right)\right)} \boldsymbol{b}_{j}^{v} \end{aligned}" />

**Results**
* It shows that it achieved 1-2% higher performance then SOTA technique on NLI tasks, SNLI, MNLI etc
* Ablation study where external knwoledge was integrated in either or of Attention, Infernce, and Composition.
* Ablation study on impact of controlling number of samples to be enhanced with external knowledge.
* It has shown samples where previous SOTA fails, but current method excels, and attributed that to external knowledge.



