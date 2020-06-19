## LAMB: Large Batch Optimization for Deep Learning: Training BERT in 76 minutes, Yang You, Jing Li 

* LAMB: layerwise adaptive large batch optimization technique
* Enables training of very large batches, i.e. batch size of 32868
* Prior work conclusion (Goyal et al. (2017))
    * large batch size enables linear scaling of learning rates ~ size of mini batch, altough it can be harmful in intial phase. So, hand tuned warmup strategy of slowly increasing learning rate.
    * linear scaling of learning rate can be detrimental beyond a certain batch size.
* Major contrinutions:
    * Intuition on general adaptive strategy catered to large batch learning
    * LAMB: new algo to achieve adaptivity in learning rates, and convergence in non-convex settings
    * Emperical performance on BERT, reducing training time from 3 days to 76 minutes
    * RESNET - where adpative solvers like ADAM fails to match SGD, LAMB outperform.
    * Authors achieved 49.1 times speedup by 64 times computational resources (76.7% efficiency)


* Experimental Nuances
    * Sequence length of 128 for 9/10 th of all epochs, and 512 for remaining last 1/10 th of all epochs.
    * In second stage, when batch size beccomes smaller, decreasing batchsize can bring divergence, so re-warmup of learnign rate from zero becomed more effective.

* Algorithms
    * General Strategy: <p align="center">
    <img align="centre" src="https://render.githubusercontent.com/render/math?math=x_{t%2B1}%20=%20x_{t}%20%2B%20\eta_{t}%20u_{t}"></p>
        * Where, u_{t} is update by any algorithm, and \eta_{t} is learning rate. 
    * Author proposes following two changes:
        * Normalise updates to u_{t}/||u_{t}||
        * Learning rate scaled by <img src="https://render.githubusercontent.com/render/math?math=\phi(||x_t||)">
    * So, SGD would become instance of this general strategy where, <p align="center">
    <img align="centre" src="https://render.githubusercontent.com/render/math?math=x_{t%2B1}^{(i)} %20=%20x_{t}^{(i)}%20-%20\eta_{t}%20\frac{\phi(||x_t^{(i)}||)}{||{g_t^{(i)}}||}g_{t}^{(i)}"></p>
        * Where, <img src="https://render.githubusercontent.com/render/math?math=g_t"> is gradient.
    * <p align="center"> <img width=600 src="images/lamb_algo.png"></p>
    * LARS, would become instance of this general strategy by taking momentum into an account (i.e. adam)
    * LAMB, would extend it further by taking updates with momentum normalized by square root of second order momentum. 
    * Naturally, there is layer wise learnign of LR adaptivity as well.



