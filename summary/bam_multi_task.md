## BAM! Born-Again Multi-Task Networks for Natural Language Understanding

### Kevin Clark, Minh-Thang Luong, Urvashi Khandelwal, Christopher D. Manning, Quoc V. Le

### Standord, Google Brain, 2019

**Whats New** Generally it is challaning for multi task neural network models to outperform single task fine tuned models. Where this paper shows it is possible.

**How it works** This paper gives series of tricks, which makes Mutli Tasks networks can outperform single task tuned networks. Those techniques are:
* Mutli Task Knowledge Distillation

    <img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D(%5Ctheta)%3D%5Csum_%7B%5Ctau%20%5Cin%20%5Cmathcal%7BT%7D%7D%20%5Csum_%7Bx_%7B%5Ctau%7D%5E%7Bi%7D%2C%20y_%7B%5Ctau%7D%5E%7Bi%7D%20%5Cin%20%5Cmathcal%7BD%7D_%7B%5Ctau%7D%7D%20%5Cell%5Cleft(f_%7B%5Ctau%7D%5Cleft(x_%7B%5Ctau%7D%5E%7Bi%7D%2C%20%5Ctheta_%7B%5Ctau%7D%5Cright)%2C%20f_%7B%5Ctau%7D%5Cleft(x_%7B%5Ctau%7D%5E%7Bi%7D%2C%20%5Ctheta%5Cright)%5Cright)" alt="\mathcal{L}(\theta)=\sum_{\tau \in \mathcal{T}} \sum_{x_{\tau}^{i}, y_{\tau}^{i} \in \mathcal{D}_{\tau}} \ell\left(f_{\tau}\left(x_{\tau}^{i}, \theta_{\tau}\right), f_{\tau}\left(x_{\tau}^{i}, \theta\right)\right)" />

    * Loss function aggregate loss over each task T, where labels comes from teacher model with parameters \theta_t

* Teacher Annealing

    <img src="https://i.upmath.me/svg/%5Cell%5Cleft(%5Clambda%20y_%7B%5Ctau%7D%5E%7Bi%7D%2B(1-%5Clambda)%20f_%7B%5Ctau%7D%5Cleft(x_%7B%5Ctau%7D%5E%7Bi%7D%2C%20%5Ctheta_%7B%5Ctau%7D%5Cright)%2C%20f_%7B%5Ctau%7D%5Cleft(x_%7B%5Ctau%7D%5E%7Bi%7D%2C%20%5Ctheta%5Cright)%5Cright)" alt="\ell\left(\lambda y_{\tau}^{i}+(1-\lambda) f_{\tau}\left(x_{\tau}^{i}, \theta_{\tau}\right), f_{\tau}\left(x_{\tau}^{i}, \theta\right)\right)" />

    * As can seen \lambda parameters control wightage between teacher model outcome, and gold label

* Layer wise learning rate

    * This technique is from Howard (2018), where lower layer (close to input) has lower learning rates. the learning rate for a particular layer d is set to BASE_LR · α^d

* Task Sampling
    
    * the probability of training on an example for a particular task τ is proportional to |Dτ |^0.75


* Ablation studies
    * It shows how each of above techniques are helping out.

        <p align="center">
        <img width=600 src="images/bam_multitask_table_4.png">
        <em>Source: Author</em>
        </p>

    * It also shows, relative improvement of a model trained on multi tasks and followed by single task fine tuning vs model BAM multi task model followed by single task fine tuning, where it establish the point that most of the gain related to single task fine tuning are already captured by BAM-multi task model.

        <p align="center">
        <img width=600 src="images/bam_multitask_table_5.png">
        <em>Source: Author</em>
        </p>

    * Similar tasks help out each other, and they also regularise each other. Let say, RTE has very less numbers of samples, but when it is fined tuned with MNLI it has huge gain, and marginal gains are also obsevered with other tasks. BAM-multi-tasks leverage all tasks. 
        <p align="center">
        <img width=600 src="images/bam_multitask_table_6.png">
        <em>Source: Author</em>
        </p>

    * It does Mann-Whitney U tests for ablation study.
