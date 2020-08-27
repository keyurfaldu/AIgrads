## CTRL: A CONDITIONAL TRANSFORMER LANGUAGE MODEL FOR CONTROLLABLE GENERATION
### Nitish Shirish Keskar, Bryan McCann, Lav R. Varshney, Caiming Xiong, Richard Socher
### 2020

**Whats New**
This paper is about creating conditional transformer language model, which is trained to condition on control codes that govern style, content and task specific behavior.  Control codes were derived from structure that naturally co-occurs with raw texts. 

**How it works**
* In computer vision, the advent of generative adversarial networks improved image generation.
* Language models are generally trained for a specific task. But less is understood about the generation which is not constrained to any specific task.
* For example, large resources like Wikipedia, Project Gutenberg, and Amazon Reviews can each be assigned a domain-related control code
* On other URLs also represents certain linguist patterns pertaining to the community which is interacting with that sets of URLs. So, that can also serve as code.
* Language models are trained with following loss functions:

    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D(D)%3D-%5Csum_%7Bk%3D1%7D%5E%7B%7CD%7C%7D%20%5Clog%20p_%7B%5Ctheta%7D%5Cleft(x_%7Bi%7D%5E%7Bk%7D%20%5Cmid%20x_%7B%3Ci%7D%5E%7Bk%7D%5Cright)" alt="\mathcal{L}(D)=-\sum_{k=1}^{|D|} \log p_{\theta}\left(x_{i}^{k} \mid x_{&lt;i}^{k}\right)" />

* CTRL, has additional control code, so loss function would become:

    <img src="https://i.upmath.me/svg/p(x%20%5Cmid%20c)%3D%5Cprod_%7Bi%3D1%7D%5E%7Bn%7D%20p%5Cleft(x_%7Bi%7D%20%5Cmid%20x_%7B%3Ci%7D%2C%20c%5Cright)%20%5Cquad%20%5Cmathcal%7BL%7D(D)%3D-%5Csum_%7Bk%3D1%7D%5E%7B%7CD%7C%7D%20%5Clog%20p_%7B%5Ctheta%7D%5Cleft(x_%7Bi%7D%5E%7Bk%7D%20%5Cmid%20x_%7B%3Ci%7D%5E%7Bk%7D%2C%20c%5E%7Bk%7D%5Cright)" alt="p(x \mid c)=\prod_{i=1}^{n} p\left(x_{i} \mid x_{&lt;i}, c\right) \quad \mathcal{L}(D)=-\sum_{k=1}^{|D|} \log p_{\theta}\left(x_{i}^{k} \mid x_{&lt;i}^{k}, c^{k}\right)" />

* Around 140 GB data was used as training data which was drawn from different domains like wikipedia etc

* Data was tokenized using fastBPE with vocabolary size of 250K tokens. 

* CTRL is really a big model with dimension of 1048, with inner dimension of 8192, 48 layers, 16 heads.

* It was trained on 256 cores of a Cloud TPU v3 Pod, and got trained for 2 weeks.

* Controllable Generation:
    * Given temperature T, and scores x_i, the probability of predicting that token i is 

        <img src="https://i.upmath.me/svg/p_%7Bi%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(x_%7Bi%7D%20%2F%20T%5Cright)%7D%7B%5Csum_%7Bj%7D%20%5Cexp%20%5Cleft(x_%7Bj%7D%20%2F%20T%5Cright)%7D" alt="p_{i}=\frac{\exp \left(x_{i} / T\right)}{\sum_{j} \exp \left(x_{j} / T\right)}" />

    * Generally, top-K tokens are chosen using the probability score. T=0, it would become greedy. T=infinite will flatten distribution to uniform
    * Common practice, the nucleus sampling approach chooses probability p_t and sets k to be the lowest value such that sigma of top k elements are greater then the probability threshold. 
        * So, if model is confident, automatically k would be lower.
        * Some factual information requires only unique token to be generated. Relaxing that would choose wrong information, but on other hand it would also suffer from repetations. In order to balance both, **"Penaliaing Sampling"** works by discounting the score of already generated samples.

        <img src="https://i.upmath.me/svg/p_%7Bi%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(x_%7Bi%7D%20%2F(T%20%5Ccdot%20I(i%20%5Cin%20g))%5Cright.%7D%7B%5Csum_%7Bj%7D%20%5Cexp%20%5Cleft(x_%7Bj%7D%20%2F(T%20%5Ccdot%20I(j%20%5Cin%20g))%5Cright.%7D" alt="p_{i}=\frac{\exp \left(x_{i} /(T \cdot I(i \in g))\right.}{\sum_{j} \exp \left(x_{j} /(T \cdot I(j \in g))\right.}" />
* Control codes and examples
    * Style by domain: Few examples are, Wikipedia, books, horror, legal, relationships etc
    * More complex control codes: like URLs
    * Triggering specific tasks: specific tasks can be triggered by using control codes




