## KnowBERT: Knowledge Enhanced Contextual Word Representations
### Peters et al
### ACL 2019

**Whats New** It proposes a general method to embed multiple knowledge bases into large scale models, and thereby, enhance their representations with structured human knowledge. For embedding each KB, (1) first use an integrated entity linker to retrieve relevant entity embeddings, and then (2) update contextual word representation using word to entity attention.

**How It Works**
* Following diagram illustrate the complete picture in detail.

<p align="center">
    <img width=600 src="images/knowbert_architecture.png">
    <em>Source: Author</em>
    </p>

* Mention-span representations
    * Project H_i to entity dimension using a linear projection

        <img src="https://i.upmath.me/svg/%5Cmathbf%7BH%7D_%7Bi%7D%5E%7B%5Cmathrm%7Bproj%7D%7D%3D%5Cmathbf%7BH%7D_%7Bi%7D%20%5Cmathbf%7BW%7D_%7B%5Cmathbf%7B1%7D%7D%5E%7B%5Cmathrm%7Bproj%7D%7D%2B%5Cmathbf%7Bb%7D_%7B1%7D%5E%7B%5Cmathrm%7Bproj%7D%7D" alt="\mathbf{H}_{i}^{\mathrm{proj}}=\mathbf{H}_{i} \mathbf{W}_{\mathbf{1}}^{\mathrm{proj}}+\mathbf{b}_{1}^{\mathrm{proj}}" />

    * Pool all wordpieces in mention span using self attentive span pooling, to derive S.

* Entity Linker
    * Mention-span self attention

        <img src="https://i.upmath.me/svg/%24%5Cmathbf%7BS%7D%5E%7Be%7D%3D%24%20TransformerBlock%20%24(%5Cmathbf%7BS%7D)" alt="$\mathbf{S}^{e}=$ TransformerBlock $(\mathbf{S})" />

    * Candidates entities are chosen from KB, each candidate span m has 
        - an associated mention span representation s_m^e
        - M_m candidate entities with word embeddings e_mk and prior probabilities p_mk

            <img src="https://i.upmath.me/svg/%24%5Cpsi_%7Bm%20k%7D%3D%5Coperatorname%7BMLP%7D%5Cleft(p_%7Bm%20k%7D%2C%20%5Cmathbf%7Bs%7D_%7Bm%7D%5E%7Be%7D%20%5Ccdot%20%5Cmathbf%7Be%7D_%7Bm%20k%7D%5Cright)" alt="$\psi_{m k}=\operatorname{MLP}\left(p_{m k}, \mathbf{s}_{m}^{e} \cdot \mathbf{e}_{m k}\right)" />

        - At this stage if gold labels are available, i.e. for a given mention-span, if we know gold entitiy, then a loss function (log liklihood and max margin)

            <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BEL%7D%7D%3D-%5Csum_%7Bm%7D%20%5Clog%20%5Cleft(%5Cfrac%7B%5Cexp%20%5Cleft(%5Cpsi_%7Bm%20g%7D%5Cright)%7D%7B%5Csum_%7Bk%7D%20%5Cexp%20%5Cleft(%5Cpsi_%7Bm%20k%7D%5Cright)%7D%5Cright)%5C%5C%20And%2C%20%5C%5C%20%5Cbegin%7Baligned%7D%20%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BEL%7D%7D%3D%26%20%5Cmax%20%5Cleft(0%2C%20%5Cgamma-%5Cpsi_%7Bm%20g%7D%5Cright)%2B%5C%5C%20%26%20%5Csum_%7Be_%7Bm%20k%7D%20%5Cneq%20e_%7Bm%20g%7D%7D%20%5Cmax%20%5Cleft(0%2C%20%5Cgamma%2B%5Cpsi_%7Bm%20k%7D%5Cright)%20%5Cend%7Baligned%7D" alt="\mathcal{L}_{\mathrm{EL}}=-\sum_{m} \log \left(\frac{\exp \left(\psi_{m g}\right)}{\sum_{k} \exp \left(\psi_{m k}\right)}\right)\\ And, \\ \begin{aligned} \mathcal{L}_{\mathrm{EL}}=&amp; \max \left(0, \gamma-\psi_{m g}\right)+\\ &amp; \sum_{e_{m k} \neq e_{m g}} \max \left(0, \gamma+\psi_{m k}\right) \end{aligned}" />

* Knowledge Enhanced Entity-Span Representation
    * \psi_mk represent similarity between mention span and entity embedding. Disregard all the entities where \psi_mk is less than threshold.

        <img src="https://i.upmath.me/svg/%5Ctilde%7B%5Cpsi%7D_%7Bm%20k%7D%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Bll%7D%5Cfrac%7B%5Cexp%20%5Cleft(%5Cpsi_%7Bm%20k%7D%5Cright)%7D%7B%5Csum_%7B%5Cpsi_%7Bm%20k%7D%20%5Cgeq%20%5Cdelta%7D%20%5Cexp%20%5Cleft(%5Cpsi_%7Bm%20k%7D%5Cright)%7D%2C%20%26%20%5Cpsi_%7Bm%20k%7D%20%5Cgeq%20%5Cdelta%20%5C%5C%200%2C%20%26%20%5Cpsi_%7Bm%20k%7D%3C%5Cdelta%5Cend%7Barray%7D%5Cright." alt="\tilde{\psi}_{m k}=\left\{\begin{array}{ll}\frac{\exp \left(\psi_{m k}\right)}{\sum_{\psi_{m k} \geq \delta} \exp \left(\psi_{m k}\right)}, &amp; \psi_{m k} \geq \delta \\ 0, &amp; \psi_{m k}&lt;\delta\end{array}\right." />

    * Weighted entity embeddings are computed as follow:

        <img src="https://i.upmath.me/svg/%5Ctilde%7B%5Cmathbf%7Be%7D%7D_%7Bm%7D%3D%5Csum_%7Bk%7D%20%5Ctilde%7B%5Cpsi%7D_%7Bm%20k%7D%20%5Cmathbf%7Be%7D_%7Bm%20k%7D" alt="\tilde{\mathbf{e}}_{m}=\sum_{k} \tilde{\psi}_{m k} \mathbf{e}_{m k}" />

    * Finally, entity span representations are updated using weighted entity embeddings.

        <img src="https://i.upmath.me/svg/%5Cmathbf%7Bs%7D_%7Bm%7D%5E%7B%5Cprime%20e%7D%3D%5Cmathbf%7Bs%7D_%7Bm%7D%5E%7Be%7D%2B%5Ctilde%7B%5Cmathbf%7Be%7D%7D_%7Bm%7D" alt="\mathbf{s}_{m}^{\prime e}=\mathbf{s}_{m}^{e}+\tilde{\mathbf{e}}_{m}" />

* Recontextualization
    * Using attention mechanism, where projected mention span represnetations are taken as query, and entitiy span representations are taken as key and value, and KB contexulised mention span are computed as below:

        <img src="https://i.upmath.me/svg/%5Cmathbf%7BH%7D_%7Bi%7D%5E%7B%5Ctext%20%7B'proj%20%7D%7D%3D%5Coperatorname%7BMLP%7D%5Cleft(%5Cright.%24%20MultiHead%20%24%5Cleft.%5Coperatorname%7BAttn%7D%5Cleft(%5Cmathbf%7BH%7D_%7Bi%7D%5E%7B%5Ctext%20%7Bproj%20%7D%7D%2C%20%5Cmathbf%7Bs%7D%5E%7B%5Cprime%20e%7D%2C%20%5Cmathbf%7Bs%7D%5E%7B%5Cprime%20e%7D%5Cright)%5Cright)" alt="\mathbf{H}_{i}^{\text {'proj }}=\operatorname{MLP}\left(\right.$ MultiHead $\left.\operatorname{Attn}\left(\mathbf{H}_{i}^{\text {proj }}, \mathbf{s}^{\prime e}, \mathbf{s}^{\prime e}\right)\right)" />

* Projected back to BERT dimensions
    * Inverse of weight matrix which projected BERT embeddings to entity dimensions are used here.

        <img src="https://i.upmath.me/svg/%5Cmathbf%7BH%7D_%7Bi%7D%5E%7B%5Cprime%7D%3D%5Cmathbf%7BH%7D_%7Bi%7D%5E%7B%5Cprime%20%5Cmathrm%7Bproj%7D%7D%20%5Cmathbf%7BW%7D_%7B2%7D%5E%7B%5Cmathrm%7Bproj%7D%7D%2B%5Cmathbf%7Bb%7D_%7B2%7D%5E%7B%5Cmathrm%7Bproj%7D%7D%2B%5Cmathbf%7BH%7D_%7Bi%7D" alt="\mathbf{H}_{i}^{\prime}=\mathbf{H}_{i}^{\prime \mathrm{proj}} \mathbf{W}_{2}^{\mathrm{proj}}+\mathbf{b}_{2}^{\mathrm{proj}}+\mathbf{H}_{i}" />

* Loss function of KnowBERT is 

    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BKnowBert%7D%7D%3D%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BBERT%7D%7D%2B%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BEL%7D%7D" alt="\mathcal{L}_{\mathrm{KnowBert}}=\mathcal{L}_{\mathrm{BERT}}+\mathcal{L}_{\mathrm{EL}}" />

* Multiple KBs can be added to BERT starting from lower layers to higher layers. 

* Results, KnowBERT has shown better results in both intrinsic and extrinsic evaluation, i.e. better than ERNIE and Soares 2019 knowledge based LMs. 

**Reflection**
Techniques to infuse knowledge base embeddings to BERT kind of language model is growing traction. It can really make Langauge Models knowledge aware, which can impact downstream tasks.










    





