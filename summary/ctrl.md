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

* Data was tokenized using fastBPE with vocabolary size of 2

