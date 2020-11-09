## SenseBERT: Driving Some Sense into BERT
### Yoav Levine et al. AI21 Labs, 
### May 2020 [[arXiv](https://arxiv.org/pdf/1908.05646.pdf)]

**Whats Unique**
This paper present a technique to predict super-sense of the masked word, with the help of weak supervision by infusing supersense of the words during pretraining. And, it surpasses state of the art results for WiC task of SuperGLUE.

**How It Works**
* It has selected set of 45 supersenses as the candidates for infusion in weak supervision as well as for prediction.
* Following figure layout the diagram for architecture
    <p align="center">
        <img width=600 src="images/sensebert_architecture.png">
        <em>Source: Author</em>
        </p>

* Following example illustrate the concept of **weak supervion**
    <p align="center">
        <img width=600 src="images/sensebert_supersense_infusion.png">
        <em>Source: Author</em>
        </p>

* Sense-language-modelling: Allowed senses prediction

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BSLM%7D%7D%5E%7B%5Ctext%20%7Ballowed%20%7D%7D%20%26%3D-%5Clog%20p(s%20%5Cin%20A(w)%20%5Cmid%20%5Ctext%20%7B%20context%20%7D)%20%5C%5C%0A%26%3D-%5Clog%20%5Csum_%7Bs%20%5Cin%20A(w)%7D%20p(s%20%5Cmid%20%5Ctext%20%7B%20context%20%7D)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\mathcal{L}_{\mathrm{SLM}}^{\text {allowed }} &amp;=-\log p(s \in A(w) \mid \text { context }) \\
&amp;=-\log \sum_{s \in A(w)} p(s \mid \text { context })
\end{aligned}" />

* Sense-language-modelling Regularisation

    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BSLM%7D%7D%5E%7B%5Cmathrm%7Breg%7D%7D%3D-%5Csum_%7Bs%20%5Cin%20A(w)%7D%20%5Cfrac%7B1%7D%7B%7CA(w)%7C%7D%20%5Clog%20p(s%20%5Cmid%20%5Ctext%20%7B%20context%20%7D)" alt="\mathcal{L}_{\mathrm{SLM}}^{\mathrm{reg}}=-\sum_{s \in A(w)} \frac{1}{|A(w)|} \log p(s \mid \text { context })" />

* SLM Loss function
    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BSLM%7D%7D%3D%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BSLM%7D%7D%5E%7B%5Ctext%20%7Ballowed%20%7D%7D%2B%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BSLM%7D%7D%5E%7B%5Cmathrm%7Breg%7D%7D" alt="\mathcal{L}_{\mathrm{SLM}}=\mathcal{L}_{\mathrm{SLM}}^{\text {allowed }}+\mathcal{L}_{\mathrm{SLM}}^{\mathrm{reg}}" />

* Following figure shows an example of how it predicts supersenses for masked words as well as for unmasked sentence.
    <p align="center">
        <img width=600 src="images/sensebert_supersense_prediction_example.png">
        <em>Source: Author</em>
        </p>

**Results**
* It has shown 2.5% improvement for WiC task.