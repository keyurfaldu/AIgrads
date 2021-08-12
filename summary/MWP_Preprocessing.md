## Solving Arithmetic Word Problems with Transformers and Preprocessing of Problem Text.
### Griffith, Kaden, and Jugal Kalita.
### arXiv preprint [[arXiv:2106.00893](https://arxiv.org/pdf/2106.00893.pdf)] (2021).

**Whats Unique**
This paper selects four datasets (smaller !!) and apply transformers over it, and check which notation is giving a higher performance, and found post-fix is a better one. It also applied pre-processing trechniques and found "lemmetization" and "removing irrelevant numbers" are effective to improve the accuracy.

**Key Takeaway**
* It found following two techniques are helping:
    * Lemetization
    * Selective tagging, which tags the number only if it is relevant for the label generation.
* It replaced all the words by its POS TAG, but obviously as expected, it drastically reduced the performance. Also, sentence reordering had a similar adverse impact.