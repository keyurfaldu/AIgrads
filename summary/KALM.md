## Knowledge-Augmented Language Model and Its Application to Unsupervised Named-Entity Recognition
### Angli Liu, Jingfei Du, Veselin Stoyanov
### Facebook AI
### NAACL 2019

**Whats New** This paper presents augmentation method in generative langugage model, which learns latent entity types, and leverages external knowledge bases in unsupervised fashion. 

**How it works**
* In RNN setup, to predict the next word,
    * It needs to predict the probability of next word, 
    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0AP%5Cleft(y_%7Bt%2B1%7D%20%5Cmid%20c_%7Bt%7D%5Cright)%3D%26%20%5Csum_%7Bj%3D0%7D%5E%7BK%7D%20P%5Cleft(y_%7Bt%2B1%7D%2C%20%5Ctau_%7Bt%2B1%7D%3Dj%20%5Cmid%20c_%7Bt%7D%5Cright)%20%5C%5C%0A%3D%26%20%5Csum_%7Bj%3D0%7D%5E%7BK%7D%20P%5Cleft(y_%7Bt%2B1%7D%20%5Cmid%20%5Ctau_%7Bt%2B1%7D%3Dj%2C%20c_%7Bt%7D%5Cright)%0A%5Ccdot%20P%5Cleft(%5Ctau_%7Bt%2B1%7D%3Dj%20%5Cmid%20c_%7Bt%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
P\left(y_{t+1} \mid c_{t}\right)=&amp; \sum_{j=0}^{K} P\left(y_{t+1}, \tau_{t+1}=j \mid c_{t}\right) \\
=&amp; \sum_{j=0}^{K} P\left(y_{t+1} \mid \tau_{t+1}=j, c_{t}\right)
\cdot P\left(\tau_{t+1}=j \mid c_{t}\right)
\end{aligned}" />
    * Which is probability of word given type multiplied by probability of type given hidden state. Ofcourse the weighted sum across all the types. 

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%26P%5Cleft(y_%7Bt%2B1%7D%3Di%20%5Cmid%20%5Ctau_%7Bt%2B1%7D%3Dj%2C%20c_%7Bt%7D%5Cright)%3D%5Cfrac%7B%5Cexp%20%5Cleft(%5Cboldsymbol%7BW%7D_%7Bi%2C%3A%7D%5E%7Bp%2C%20j%7D%20%5Ccdot%20%5Cboldsymbol%7Bh%7D_%7Bt%7D%5Cright)%7D%7B%5Csum_%7Bw%3D1%7D%5E%7B%5Cleft%7CV_%7Bj%7D%5Cright%7C%7D%20%5Cexp%20%5Cleft(%5Cboldsymbol%7BW%7D_%7Bw%2C%3A%7D%5E%7Bp%2C%20j%7D%20%5Ccdot%20%5Cboldsymbol%7Bh%7D_%7Bt%7D%5Cright)%7D%5C%5C%0A%26P%5Cleft(%5Ctau_%7Bt%2B1%7D%3Dj%20%5Cmid%20c_%7Bt%7D%5Cright)%3D%5Cfrac%7B%5Cexp%20%5Cleft(%5Cboldsymbol%7BW%7D_%7Bj%2C%3A%7D%5E%7Be%7D%20%5Ccdot%5Cleft(%5Cboldsymbol%7BW%7D%5E%7Bh%7D%20%5Ccdot%20%5Cboldsymbol%7Bh%7D_%7Bt%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bk%3D0%7D%5E%7BK%7D%20%5Cexp%20%5Cleft(%5Cboldsymbol%7BW%7D_%7Bk%2C%3A%7D%5E%7Be%7D%20%5Ccdot%5Cleft(%5Cboldsymbol%7BW%7D%5E%7Bh%7D%20%5Ccdot%20%5Cboldsymbol%7Bh%7D_%7Bt%7D%5Cright)%5Cright)%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
&amp;P\left(y_{t+1}=i \mid \tau_{t+1}=j, c_{t}\right)=\frac{\exp \left(\boldsymbol{W}_{i,:}^{p, j} \cdot \boldsymbol{h}_{t}\right)}{\sum_{w=1}^{\left|V_{j}\right|} \exp \left(\boldsymbol{W}_{w,:}^{p, j} \cdot \boldsymbol{h}_{t}\right)}\\
&amp;P\left(\tau_{t+1}=j \mid c_{t}\right)=\frac{\exp \left(\boldsymbol{W}_{j,:}^{e} \cdot\left(\boldsymbol{W}^{h} \cdot \boldsymbol{h}_{t}\right)\right)}{\sum_{k=0}^{K} \exp \left(\boldsymbol{W}_{k,:}^{e} \cdot\left(\boldsymbol{W}^{h} \cdot \boldsymbol{h}_{t}\right)\right)}
\end{aligned}" />

    * Probability weighted type embedding vector will be concatenated to generated word, as it would carry forward type information in it, which will help to predict type of the next word as well.

        <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bc%7D%0A%5Cboldsymbol%7B%5Cnu%7D_%7Bt%2B1%7D%3D%5Csum_%7Bj%3D0%7D%5E%7BK%7D%20P%5Cleft(%5Ctau_%7Bt%2B1%7D%3Dj%20%5Cmid%20c_%7Bt%7D%5Cright)%20%5Ccdot%20%5Cboldsymbol%7BW%7D_%7Bj%2C%3A%7D%5E%7Be%7D%20%5C%5C%0A%5Ctilde%7B%5Cboldsymbol%7By%7D%7D_%7Bt%2B1%7D%3D%5Cleft%5B%5Cboldsymbol%7By%7D_%7Bt%2B1%7D%20%3B%20%5Cboldsymbol%7B%5Cnu%7D_%7Bt%2B1%7D%5Cright%5D%0A%5Cend%7Barray%7D" alt="\begin{array}{c}
\boldsymbol{\nu}_{t+1}=\sum_{j=0}^{K} P\left(\tau_{t+1}=j \mid c_{t}\right) \cdot \boldsymbol{W}_{j,:}^{e} \\
\tilde{\boldsymbol{y}}_{t+1}=\left[\boldsymbol{y}_{t+1} ; \boldsymbol{\nu}_{t+1}\right]
\end{array}" />


    * Following figure demonstrate it really well
    <p align="center">
        <img width=600 src="images/KALM_architecture.png">
        <em>Source: Author</em>
        </p>

    * After that it adds three more techniques:
        * for NER tasks it leverages bidirectional context.
        * It also leverage type prior for each entity from external source
        * It uses wikitext-2 data alogn with CoNLL dataset.

    * Loss function trained as below:

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0AL%3D%26%20H%5Cleft(P%5Cleft(y_%7Bi%7D%20%5Cmid%20c_%7Bl%7D%2C%20c_%7Br%7D%5Cright)%2C%20P%5Cleft(%5Chat%7By%7D_%7Bi%7D%20%5Cmid%20c_%7Bl%7D%2C%20c_%7Br%7D%5Cright)%5Cright)%20%5C%5C%0A%26%2B%5Clambda%20%5Ccdot%5Cleft%5C%7CK%20L%5Cleft(P%5Cleft(%5Ctau_%7Bi%7D%20%5Cmid%20c_%7Bl%7D%2C%20c_%7Br%7D%5Cright)%2C%20P%5Cleft(%5Ctau_%7Bi%7D%20%5Cmid%20y_%7Bi%7D%5Cright)%5Cright)%5Cright%5C%7C%5E%7B2%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
L=&amp; H\left(P\left(y_{i} \mid c_{l}, c_{r}\right), P\left(\hat{y}_{i} \mid c_{l}, c_{r}\right)\right) \\
&amp;+\lambda \cdot\left\|K L\left(P\left(\tau_{i} \mid c_{l}, c_{r}\right), P\left(\tau_{i} \mid y_{i}\right)\right)\right\|^{2}
\end{aligned}" />

**Results**
    * In unsupervised way, it gives F1 score of 0.86 for entity types LOC, MISC, ORG, PER in CoNLL 
    * As external knowledge base gets corrupt, its NER perfromance get impacted, as can be seen below:
    <p align="center">
        <img width=600 src="images/KALM_results.png">
        <em>Source: Author</em>
        </p>
