## How to Fine-Tune BERT for Text Classification?
### Chi Sun, Xipeng Qiu, Yige Xu, Xuanjing Huang
### 2019

**Whats new** This paper analyse different startegies around finetuning BERT for text classication.

**Key Insights**
* Diminishing learning rate is used. Decay factor of 0.95 or 0.9 gave better results.
* Head+Tail truncation methods give better results
* Lower learning rate (2e-5) is kept to avoid catestrophic forgetting
* With in task and In domain pretraining helps a lot.
* Multi task trainig helps, but cross domain pre-training subsumes the benefit.
* In-task pretraining is also helpful even if there is marginal training data for the task is available.

**Reflection**
* This paper studied mostly intuitive points. It could have gone deeper into higher order analysis like data augmentation, fine tuning architectural choices, etc.