## FNet: Mixing Tokens with Fourier Transforms.
### Lee-Thorp, James, Joshua Ainslie, Ilya Eckstein, and Santiago Ontanon.  
### [arXiv preprint arXiv:2105.03824](https://arxiv.org/pdf/2105.03824.pdf).


**Whats New**
This paper has demonstrated that huge performance gain of attention based language models are due to its intermixing of tokens. Even if simple non-parameterized intermixing is done, it achives 92% accuracy, with lower memory footprint and 7 times the training speed over GPUs.

**Key Contributions**
* Attention mechanism works best because it does task dependent and token dependent intermixinig

* Intermixing tokens in sequence and hidden dimensions even in non-parameterised way would retain majority performance gain, and make model extremely fast.

* **FNet encoder** replaces self attention layer with a fourier sublayer, defined as follow: (1) a weight of token is sum over all the tokens of previous layer with weights derived from fourier transform. (2) fourier sublayer is applied over hidden dimension and then over sequence length.   

    <img src="https://i.upmath.me/svg/%0AX_%7Bk%7D%3D%5Csum_%7Bn%3D0%7D%5E%7BN-1%7D%20x_%7Bn%7D%20e%5E%7B-%5Cfrac%7B2%20%5Cpi%20i%7D%7BN%7D%20n%20k%7D%2C%20%5Cquad%200%20%5Cleq%20k%20%5Cleq%20N-1%5C%5C%0Ay%3D%5CRe%5Cleft(%5Cmathcal%7BF%7D_%7B%5Ctext%20%7Bseq%20%7D%7D%5Cleft(%5Cmathcal%7BF%7D_%7B%5Ctext%20%7Bhidden%20%7D%7D(x)%5Cright)%5Cright)%20" alt="
X_{k}=\sum_{n=0}^{N-1} x_{n} e^{-\frac{2 \pi i}{N} n k}, \quad 0 \leq k \leq N-1\\
y=\Re\left(\mathcal{F}_{\text {seq }}\left(\mathcal{F}_{\text {hidden }}(x)\right)\right) " />

<p align="center">
        <img width=600 src="images/FNet.png">
        <em>Source: Author</em>
        </p>

* They have trained another model, **Linear encoder**, where self-attention layer is replaced with two learnable, dense and linear layer and it performs better than FNet, but ofcourse it has more parameters than FNet but lesser than vanilla BERT.

* Parameters, Loss, Accuracy over GLUE benchmark and GPU/TPU time per step has been published as results.

* For Long-Range Arena benchmark, its performance reaches almost on-par with BERT, which makes its suitable to apply at much lower memory footprint and higher speed.
