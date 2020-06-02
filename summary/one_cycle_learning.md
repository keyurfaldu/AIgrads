## A DISCIPLINED APPROACH TO NEURAL NETWORK HYPER-PARAMETERS
### Leslie N. Smith, April 2018

It shows how to examine the training validation/test loss function for subtle clues of underfitting and overfitting and suggests guidelines for moving toward the optimal balance point.
* Then it discusses how to increase/decrease the learning rate/momentum to speed up training.
* Weight decay is used as a sample regularizer to show how its optimal value is tightly coupled with the learning rates and momentum
* close attention to these clues while using cyclical learning rates and cyclical momentum.


Useful remarks:
* Remark 1. The test/validation loss is a good indicator of the network’s convergence
* Remark 2. The takeaway is that achieving the horizontal part of the test loss is the goal of hyperparameter tuning
* Remark 3: the amount of regularization must be balanced for each dataset and architecture. Smaller learning rates leads to overfitting, and higher weight decay leads to regularise. So, possible combinations: small LR with high WD, or high LR with small WD.
