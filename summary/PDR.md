## Posterior Differential Regularization with f-divergence for Improving Model Robustness.
### Cheng, Hao, Xiaodong Liu, Lis Pereira, Yaoliang Yu, and Jianfeng Gao. 
### arXiv preprint arXiv:2010.12638 (2020) [[arXiv](https://arxiv.org/pdf/2010.12638.pdf)].

**Whats Unique**
This paper focus on the impact of methods regularising the model posterior difference between clean and noisy inputs. Theoretically, it provides connection of two methods, Jacobian Regularisation, and Virtual Adversarial Training. 

**Motivation**
* Following figure shows the downfall on the performance when a model is applied to out of domain or adversarial in-domain attack.

<p align="center">
<img align="centre" src="images/PDR_motivation.png">
</p>

**Adversarial Learning**
* It focus on minimizing the following objective:

    <img src="https://i.upmath.me/svg/%5Cmin%20_%7B%5CTheta%7D%20%5Cmax%20_%7B%5C%7C%5Cepsilon%5C%7C%20%5Cleq%20c%7D%20L%5Cleft(f_%7B%5CTheta%7D(%5Cmathbf%7Bx%7D%2B%5Cepsilon)%2C%20y%5Cright)" alt="\min _{\Theta} \max _{\|\epsilon\| \leq c} L\left(f_{\Theta}(\mathbf{x}+\epsilon), y\right)" />

**Posterior Differnce Regularisation**
* It focus on regularising the difference in the posterior.
    
    <img src="https://i.upmath.me/svg/%5Cmin%20_%7B%5CTheta%7D%20L%5Cleft(f_%7B%5CTheta%7D(%5Cmathbf%7Bx%7D)%2C%20%5Cmathbf%7By%7D%5Cright)%2B%5Calpha%20R%5Cleft(f_%7B%5CTheta%7D(%5Cmathbf%7Bx%7D)%2C%20f_%7B%5CTheta%7D(%5Chat%7B%5Cmathbf%7Bx%7D%7D)%5Cright)" alt="\min _{\Theta} L\left(f_{\Theta}(\mathbf{x}), \mathbf{y}\right)+\alpha R\left(f_{\Theta}(\mathbf{x}), f_{\Theta}(\hat{\mathbf{x}})\right)" />

* Where PDR funciton R can be either Jacobian Regularisation, or it can be Virtual Adversarial Training.

* Jacobian Regularisation:
    * First order taylor approximation would give following input-out jacobian matrix:

    <img src="https://i.upmath.me/svg/f(%5Cmathbf%7Bx%7D%2B%5Cepsilon)%3Df(%5Cmathbf%7Bx%7D)%2BJ_%7Bf%7D(%5Cmathbf%7Bx%7D)%20%5Cepsilon" alt="f(\mathbf{x}+\epsilon)=f(\mathbf{x})+J_{f}(\mathbf{x}) \epsilon" />

    * It can be shown theoretically, that to reduce overall sensitivity of model to input perturbations, directly Frobonius Norm of Jacobian matrix can be mininised (considered as R). Which is:
        * <img src="https://i.upmath.me/svg/%5C%7CJ%5C%7C_%7BF%7D%5E%7B2%7D%3D%5Coperatorname%7Btr%7D%5Cleft(J%5E%7BT%7D%20J%5Cright)" alt="\|J\|_{F}^{2}=\operatorname{tr}\left(J^{T} J\right)" />

* Virtual Adversarial Training
    * The objective to minimize the impact of input perturbations is, 

    <img src="https://i.upmath.me/svg/%5Cmin%20%5BL(%5Cmathbf%7By%7D%2C%20%5Chat%7B%5Cmathbf%7By%7D%7D)%2B%5Calpha%20%5Cunderbrace%7B%5Cmax%20_%7B%5C%7C%5Cepsilon%5C%7C%20%5Cleq%20c%7D%20%5Coperatorname%7BKL%7D(%5Chat%7B%5Cmathbf%7By%7D%7D%2C%20f(%5Cmathbf%7Bx%7D%2B%5Cepsilon))%7D_%7BR%7D%5D" alt="\min [L(\mathbf{y}, \hat{\mathbf{y}})+\alpha \underbrace{\max _{\|\epsilon\| \leq c} \operatorname{KL}(\hat{\mathbf{y}}, f(\mathbf{x}+\epsilon))}_{R}]" />

    * Where, KL is the kullback divergence

* Author shows that f-divergence is a family of various posterior difference regularisation functions like KL, or Jacobian regularisation. 

* On the tasks, of NLI, and QA, papers shows the improvement by these regularisation methods in out-of-domain and adversarial attack settings.

**Results**

<p align="center">
<img align="centre" src="images/PDR_results.png">
</p>




