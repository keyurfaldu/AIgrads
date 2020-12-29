## Group Normalization
### Wu, Yuxin, and Kaiming He.
### European conference on computer vision (ECCV). 2018. [[arXiv](https://arxiv.org/pdf/1803.08494.pdf)]

**Whats Unique**
This paper presents a novel technique - Group normalisation, which normalise features across channels, (or, let say embedding dimesions) instead of normalising it across the batch level. Hence it is batch agnostic and works effectively in comparison to Batch Norm when batch size is small.

**How It Works**
* Following figure illustrates four different types of normalisation.

<p align="center">
    <img width=600 src="images/group_norm_illustration.png">
    <em>Source: Author</em>
    </p>

* Formulation
    * Each sample x_i is normalised as follow: 
    <img src="https://i.upmath.me/svg/%5Chat%7Bx%7D_%7Bi%7D%3D%5Cfrac%7B1%7D%7B%5Csigma_%7Bi%7D%7D%5Cleft(x_%7Bi%7D-%5Cmu_%7Bi%7D%5Cright)%5C%5C%0Ai%3D%5Cleft(i_%7BN%7D%2C%20i_%7BC%7D%2C%20i_%7BH%7D%2C%20i_%7BW%7D%5Cright)%5C%5C%0A%5Cmu_%7Bi%7D%3D%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_%7Bk%20%5Cin%20%5Cmathcal%7BS%7D_%7Bi%7D%7D%20x_%7Bk%7D%2C%20%5Cquad%20%5Csigma_%7Bi%7D%3D%5Csqrt%7B%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_%7Bk%20%5Cin%20%5Cmathcal%7BS%7D_%7Bi%7D%7D%5Cleft(x_%7Bk%7D-%5Cmu_%7Bi%7D%5Cright)%5E%7B2%7D%2B%5Cepsilon%7D%5C%5C%0A%5C%5C%0ABatch%20Norm%3A%20%5C%20%5Cmathcal%7BS%7D_%7Bi%7D%3D%5Cleft%5C%7Bk%20%5Cmid%20k_%7BC%7D%3Di_%7BC%7D%5Cright%5C%7D%20%5C%5C%0ALayer%20Norm%3A%20%5C%20%5Cmathcal%7BS%7D_%7Bi%7D%3D%5Cleft%5C%7Bk%20%5Cmid%20k_%7BN%7D%3Di_%7BN%7D%5Cright%5C%7D%5C%5C%0AInstance%20Norm%3A%20%5Cmathcal%7BS%7D_%7Bi%7D%3D%5Cleft%5C%7Bk%20%5Cmid%20k_%7BN%7D%3Di_%7BN%7D%2C%20k_%7BC%7D%3Di_%7BC%7D%5Cright%5C%7D%5C%5C%0AGroup%20Norm%3A%20%5Cmathcal%7BS%7D_%7Bi%7D%3D%5Cleft%5C%7Bk%20%5Cmid%20k_%7BN%7D%3Di_%7BN%7D%2C%5Cleft%5Clfloor%5Cfrac%7Bk_%7BC%7D%7D%7BC%20%2F%20G%7D%5Cright%5Crfloor%3D%5Cleft%5Clfloor%5Cfrac%7Bi_%7BC%7D%7D%7BC%20%2F%20G%7D%5Cright%5Crfloor%5Cright%5C%7D%5C%5C%0A%5C%5C%0A%5Ctext%7BScaling%20and%20Shift%20after%20normalisation%3A%7D%5C%5C%0Ay_%7Bi%7D%3D%5Cgamma%20%5Chat%7Bx%7D_%7Bi%7D%2B%5Cbeta%0A" alt="\hat{x}_{i}=\frac{1}{\sigma_{i}}\left(x_{i}-\mu_{i}\right)\\
i=\left(i_{N}, i_{C}, i_{H}, i_{W}\right)\\
\mu_{i}=\frac{1}{m} \sum_{k \in \mathcal{S}_{i}} x_{k}, \quad \sigma_{i}=\sqrt{\frac{1}{m} \sum_{k \in \mathcal{S}_{i}}\left(x_{k}-\mu_{i}\right)^{2}+\epsilon}\\
\\
Batch Norm: \ \mathcal{S}_{i}=\left\{k \mid k_{C}=i_{C}\right\} \\
Layer Norm: \ \mathcal{S}_{i}=\left\{k \mid k_{N}=i_{N}\right\}\\
Instance Norm: \mathcal{S}_{i}=\left\{k \mid k_{N}=i_{N}, k_{C}=i_{C}\right\}\\
Group Norm: \mathcal{S}_{i}=\left\{k \mid k_{N}=i_{N},\left\lfloor\frac{k_{C}}{C / G}\right\rfloor=\left\lfloor\frac{i_{C}}{C / G}\right\rfloor\right\}\\
\\
\text{Scaling and Shift after normalisation:}\\
y_{i}=\gamma \hat{x}_{i}+\beta
" />

* Results:
Following figure shows the stability of Group Norm at different batch size (ofcourse, since it is batch-agnostic)
<p align="center">
    <img width=600 src="images/group_norm_batch_sensitivity.png">
    <em>Source: Author</em>
    </p>

In the following figure, we can see how group norm outperform batch norm for smaller batch sizes.
<p align="center">
    <img width=600 src="images/group_norm_vs_batch_norm.png">
    <em>Source: Author</em>
    </p>
