## A diverse corpus for evaluating and developing english math word problem solvers.
### Miao, Shen-Yun, Chao-Chun Liang, and Keh-Yih Su. ["
### arXiv preprint [arXiv:2106.15772](https://arxiv.org/pdf/2106.15772.pdf) (2021).


**Whats Unique**
This paper presents a dataset, which is lexically diverse, and it is annotated with the problem types. It also present a lexicon usage diversity metric. It reports the baseline performance of SOTA models on this dataset.

**Problem Types**
* Currently 24 different Problem Types (PTs) are provided and they are classified into three categories. 
    * Basic arithmatic operations
    * Aggregative operations
    * Additional domain knowledge required
* Few examples are as below:

<p align="center">
<img width=600 src="images/Asdiv_problem_types_eg.png">
<em>Source: Author</em>
</p>

* Lexicon Diversity Metric:
For a given problem type, BLEU score is computed with all other problems under that problem type, and max BLEU score is substracted from 1, to get the lexicon diversity score.

    <img src="https://i.upmath.me/svg/L%20D_%7Bi%7D%3D1-%5Cmax%20_%7Bj%2C%20j%20%5Cneq%20i%7D%20%5Cfrac%7BB%20L%20E%20U%5Cleft(P_%7Bi%7D%2C%20P_%7Bj%7D%5Cright)%2BB%20L%20E%20U%5Cleft(P_%7Bj%7D%2C%20P_%7Bi%7D%5Cright)%7D%7B2%7D" alt="L D_{i}=1-\max _{j, j \neq i} \frac{B L E U\left(P_{i}, P_{j}\right)+B L E U\left(P_{j}, P_{i}\right)}{2}" />

* Problems in MathQA: It has very low lexicon diversity score of 0.05. Other such MWP datasets also have low lexicon diversity score. It can be seen as below:

<p align="center">
<img width=600 src="images/Asdiv_MWDDatasets_LDS.png">
<em>Source: Author</em>
</p>

* It has evaluated SOTA models on MathQA-C (which is subset of MathQA by making it more consistent and error-free) and Asdiv. Results are as below:

<p align="center">
<img width=600 src="images/Asdiv_results.png">
<em>Source: Author</em>
</p>

