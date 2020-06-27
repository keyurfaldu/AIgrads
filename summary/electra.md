## ELECTRA: Pre-Training Text Encoders As Discriminator Rather Than Generators

### Kevin Clark, Minh-Thang Luong, Quoc V. Le, Christopher D. Manning
### Stanford, Google Brain, 2020

* Opportunities in BERT 
    * BERT's MLM is effective but require more compute.
    * BERT's objective is exposed to only 15% of tokens which are masked
* ELECTRA's take
    * Instead of masking out token, it would be replaced by a small generator
    * Electra's objective would be to detect if its generated or real. 
    * Objective function is computationally effective at learning
    * Objective function exposed learning to all the tokens, makes it effeciant.

* Architecture
    * It consists of a generator and a discriminator. Generator replaces masked tokens, and discriminator detects it. 

    <p align="center">
    <img align="centre" src="images/electra_architecture.png">
    </p>


    * Generator:
        * It is not adversial generator, which try to fool discriminator, as sampling makes it complicated, so it is simpler MLE based generator which replaces randomly masked tokens with predicted tokens.
        * Generator can be lean and small. As, if it does a great job, Discriminator's scope would be affected.
        
        <img width=600 src="https://i.upmath.me/svg/p_%7BG%7D%5Cleft(x_%7Bt%7D%20%5Cmid%20%5Cboldsymbol%7Bx%7D%5Cright)%3D%5Cexp%20%5Cleft(e%5Cleft(x_%7Bt%7D%5Cright)%5E%7BT%7D%20h_%7BG%7D(%5Cboldsymbol%7Bx%7D)_%7Bt%7D%5Cright)%20%2F%20%5Csum_%7Bx%5E%7B%5Cprime%7D%7D%20%5Cexp%20%5Cleft(e%5Cleft(x%5E%7B%5Cprime%7D%5Cright)%5E%7BT%7D%20h_%7BG%7D(%5Cboldsymbol%7Bx%7D)_%7Bt%7D%5Cright)" alt="p_{G}\left(x_{t} \mid \boldsymbol{x}\right)=\exp \left(e\left(x_{t}\right)^{T} h_{G}(\boldsymbol{x})_{t}\right) / \sum_{x^{\prime}} \exp \left(e\left(x^{\prime}\right)^{T} h_{G}(\boldsymbol{x})_{t}\right)" />


        <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BMLM%7D%7D%5Cleft(%5Cboldsymbol%7Bx%7D%2C%20%5Ctheta_%7BG%7D%5Cright)%3D%5Cmathbb%7BE%7D%5Cleft(%5Csum_%7Bi%20%5Cin%20%5Cboldsymbol%7Bm%7D%7D-%5Clog%20p_%7BG%7D%5Cleft(x_%7Bi%7D%20%5Cmid%20%5Cboldsymbol%7Bx%7D%5E%7B%5Cmathrm%7Bmasked%7D%7D%5Cright)%5Cright)" alt="\mathcal{L}_{\mathrm{MLM}}\left(\boldsymbol{x}, \theta_{G}\right)=\mathbb{E}\left(\sum_{i \in \boldsymbol{m}}-\log p_{G}\left(x_{i} \mid \boldsymbol{x}^{\mathrm{masked}}\right)\right)" />

    * Discriminator
        * It's a binary classification to predict on each token, as either it come from real data or is it genereated.


        <img src="https://i.upmath.me/svg/D(%5Cboldsymbol%7Bx%7D%2C%20t)%3D%5Coperatorname%7Bsigmoid%7D%5Cleft(w%5E%7BT%7D%20h_%7BD%7D(%5Cboldsymbol%7Bx%7D)_%7Bt%7D%5Cright)" alt="D(\boldsymbol{x}, t)=\operatorname{sigmoid}\left(w^{T} h_{D}(\boldsymbol{x})_{t}\right)" />

        <img width=600 src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D_%7B%5Cmathrm%7BDisc%7D%7D%5Cleft(%5Cboldsymbol%7Bx%7D%2C%20%5Ctheta_%7BD%7D%5Cright)%3D%5Cmathbb%7BE%7D%5Cleft(%5Csum_%7Bt%3D1%7D%5E%7Bn%7D-%5Cmathbb%7B1%7D%5Cleft(x_%7Bt%7D%5E%7B%5Cmathrm%7Bcorrupt%7D%7D%3Dx_%7Bt%7D%5Cright)%20%5Clog%20D%5Cleft(%5Cboldsymbol%7Bx%7D%5E%7B%5Cmathrm%7Bcorrupt%7D%7D%2C%20t%5Cright)-%5Cmathbb%7B1%7D%5Cleft(x_%7Bt%7D%5E%7B%5Cmathrm%7Bcorrupt%7D%7D%20%5Cneq%20x_%7Bt%7D%5Cright)%20%5Clog%20%5Cleft(1-D%5Cleft(%5Cboldsymbol%7Bx%7D%5E%7B%5Cmathrm%7Bcorrupt%7D%7D%2C%20t%5Cright)%5Cright)%5Cright)" alt="\mathcal{L}_{\mathrm{Disc}}\left(\boldsymbol{x}, \theta_{D}\right)=\mathbb{E}\left(\sum_{t=1}^{n}-\mathbb{1}\left(x_{t}^{\mathrm{corrupt}}=x_{t}\right) \log D\left(\boldsymbol{x}^{\mathrm{corrupt}}, t\right)-\mathbb{1}\left(x_{t}^{\mathrm{corrupt}} \neq x_{t}\right) \log \left(1-D\left(\boldsymbol{x}^{\mathrm{corrupt}}, t\right)\right)\right)" />

* Experiments shows generator of size 1/4 does better 

* Electra small takes just 4 days on 1 GPU V100 to get trained from scratch, and gives 79.9 performance on GLUE Benchmark.

* Electra can be thought of massively scaled up version of CBOW with negative sampling.

* It would be interesting to make Electra's generator auto regressive and add a replaced span detection task.



