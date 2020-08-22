## STRUCTBERT: INCORPORATING LANGUAGE STRUCTURES INTO PRETRAINING FOR DEEP LANGUAGE UNDERSTANDING
### Wang et al, Alibaba Group
### ICLR 2020

**Whats New** This paper proposes two new pre training objectives, word ordering, and sentence order detection. And, ablation study suggest that major improvement for single sentence tasks come from word ordering objective, and for multi sentence tasks comes from sentence order detection.

**How It Works?**
* Following figure illutrate both these objectives.
    <p align="center">
        <img width=600 src="images/structbert_objectives.png">
        <em>Source: Author</em>
        </p>

* As shown in the figure above, 
    * Around 5% of time, it shuffles 3 tokens, and objective is to detect the right ordering.
    * Around 33% of time, either it is next sentence, or previous, or a random.

* Ablation study results are as follow
    <p align="center">
        <img width=600 src="images/structbert_ablation.png">
        <em>Source: Author</em>
        </p>

* Overall, it has outperformed most to the bert variants on GLUE, SQUAD etc. And, StructBert on Robberta setup has given even better results.


