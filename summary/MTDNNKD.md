## Improving Multi-Task Deep Neural Networks via Knowledge Distillation for Natural Language Understanding
### Xiaodong Liu, Pengcheng He, Weizhu Chen, Jianfeng Gao1
### 2019

**Whats new** It applies knowledge distillation over ensemble of task specific fine tuned models using multi task DDNs. And, it generates SOTA performance for almost all GLUE tasks.

**Key Insights**
* In the prior paper, authors have demonstrated how Multi Tasks Leanring (i.e. pretraining), and then tasks specific fine tuning delivers better peformance over NLI tasks.
* Independently, it is also known that ensemble of models, always give better performance, but it is difficult to productionise that because of its higher compute and infra requirement.
* Moreover, knowledge distillation is able to shrink model's complexity, as it also learns proabilities of labels, which can be called dark knowledge.
* This paper combines all the three points above to generate MTDNN using Knowledge Distillation, which as expected have outperformed SOTA GLUE metrics.

**Approach**
* It trains 6 MTDNNs using multi task pretraining by varying dropout rates etc parameters. It keeps top 3 of these.
* It trains tasks specific finetuned variantes of these 3 MTDNNs. Ensemble of these task specific models serve as Teacher.
* Mutli task student is trained based on hybrid loss function, 
    * Classic loss funciton:

        <img src="https://i.upmath.me/svg/-%5Csum_%7Bc%7D%20%5Cmath%7B1%7D(X%2C%20c)%20%5Clog%20%5Cleft(P_%7Br%7D(c%20%5Cmid%20X)%5Cright)" alt="-\sum_{c} \math{1}(X, c) \log \left(P_{r}(c \mid X)\right)" />

    * Q is average proabaility function for a class, based on ensemble model:

        <img src="https://i.upmath.me/svg/Q%3D%5Coperatorname%7Bavg%7D%5Cleft(%5Cleft%5BQ%5E%7B1%7D%2C%20Q%5E%7B2%7D%2C%20%5Cldots%2C%20Q%5E%7BK%7D%5Cright%5D%5Cright)" alt="Q=\operatorname{avg}\left(\left[Q^{1}, Q^{2}, \ldots, Q^{K}\right]\right)" />

    * Knowledge Distillation based loss function:
    
        <img src="https://i.upmath.me/svg/-%5Csum_%7Bc%7D%20Q(c%20%5Cmid%20X)%20%5Clog%20%5Cleft(P_%7Br%7D(c%20%5Cmid%20X)%5Cright)" alt="-\sum_{c} Q(c \mid X) \log \left(P_{r}(c \mid X)\right)" />

    * MTDNN_KD uses sum of classic loss function and knowledge distillation based loss function. 

* Its process diagram is illustrated in the figure below:

    <p align="center">
        <img width=600 src="images/mtdnn_kd_process_diagram.png">
        <em>Source: Author</em>
        </p>


**Results**
* It has outperformed on almost all GLUE tasks
* It has also done better on the tasks where it was not MTL pretrained
* It was able to learn performance of ensemble model effectively.

**Critic Reflection**
* It has thoughtfully mixed three techniques together. 
* In general, it can be further investigated what are different ways of generating ensemble models. 
    * i.e. drop out was used by authors, but other strategies can be explored.
    * MTL pretraining and task specific fine tuning is covered here, but beyond that it can be thought further.
* How can we encorportae orhter loss functions like "RTD" in Electra, 

