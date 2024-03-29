## The curious case of neural text degeneration.
### Holtzman, Ari, Jan Buys, Li Du, Maxwell Forbes, and Yejin Choi
### arXiv preprint [[arXiv:1904.09751](https://arxiv.org/pdf/1904.09751.pdf)] (2019).

**Whats Unique**
This paper demonstrate an effective method, Nucleus Sampling, to generate text, which is more close to humans in terms of probability, perplexity, diversitiy and quality. It compares Nucleus sampling with other methods like Beam Search, Pure Sampling, Top-k sampling with different temperatures. 


**How It Works**
* Beam Search: It alyways consider top k paths, and generate one with the highest probability.
* Pure Sampling: Next token is always sampled using the probability distribution.
* Top-K sampling: Next token is sampled from fixed k tokens based on their probabilitiy distrubution, Note that probabilities of all other tokens (not in top-K) is truncated, and probabilities for top-k tokens are re-adjusted.
* Top-K sampling with temperature: Temperature is divided from the logit value, on which softmax is applied. Lower temperature gives very steep probability distribution.
    <img src="https://i.upmath.me/svg/p%5Cleft(x%3DV_%7Bl%7D%20%5Cmid%20x_%7B1%3A%20i-1%7D%5Cright)%3D%5Cfrac%7B%5Cexp%20%5Cleft(u_%7Bl%7D%20%2F%20t%5Cright)%7D%7B%5Csum_%7Bl%5E%7B%5Cprime%7D%7D%20%5Cexp%20%5Cleft(u_%7Bl%7D%5E%7B%5Cprime%7D%20%2F%20t%5Cright)%7D" alt="p\left(x=V_{l} \mid x_{1: i-1}\right)=\frac{\exp \left(u_{l} / t\right)}{\sum_{l^{\prime}} \exp \left(u_{l}^{\prime} / t\right)}" />

* Nucleus Sampling: A minimal subset of tokens having cumulative probability greater than p is considered as nucleus. And, tokens are sampled based on its normalised probability distribution.

    <img src="https://i.upmath.me/svg/%5Csum_%7Bx%20%5Cin%20V%5E%7B(p)%7D%7D%20P%5Cleft(x%20%5Cmid%20x_%7B1%3A%20i-1%7D%5Cright)%20%5Cgeq%20p" alt="\sum_{x \in V^{(p)}} P\left(x \mid x_{1: i-1}\right) \geq p" />

**Analysis**
* This paper brings lots of analysis and insights.
* Example of text generated by different sampling methods:
<p align="center">
    <img width=600 src="images/nucleus_examples.png">
    <em>Source: Author</em>
    </p>
* The conditional probability of the next token for human generated text and beam search generated text is as below:
<p align="center">
    <img width=600 src="images/nucleus_beam_search.png">
    <em>Source: Author</em>
    </p>
* Why Top-K sampling is problematic. If next token candidates have "flat probability distribution", a small value of k would carry the risk of generating bland or generic texts. On the other hand, if next token candidates have "peaked distribution", choosing high value for k would lead to incoherant and unnatural text generation. 

<p align="center">
    <img width=600 src="images/nucleus_topk_next_token_pdf.png">
    <em>Source: Author</em>
    </p>

* Self-BLEU was used to evaluate how diverse are generated texts. 
* HUSE: Human Unified Statistical Evaluation: Where a classifer is trained to classify if text is human generated or model generated using two features, probability and human judgement of "typicality". 