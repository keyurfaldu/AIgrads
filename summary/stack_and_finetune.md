## To Tune or not to Tune? How about the best of both worlds?
### Wang et al
### 2019

**Whats New** This paper present an analysis on stacking a layers on top of pretrained BERT models, train it using frozen BERT, and then fine tune whole model. And, achieves higher performance on tasks like QQP, NER, text classification etc.

**Key Insights**
* Stack task specific layers on top of BERT, train those stacked layers keeping BERT frozen for few epochs, till training accuracy and validation accuracy are similar. 
* Afterwards, fine tune whole BERT. 
* When tasks specific additional layers are stacked, a higher learning rate duing fine tuning can potentially distrub BERT parameters, and lower learning rate may be too slow for those tasks specific layers to learn, hence stack and finetune might balance both.

**Caveat**
* Authors have selected tasks with large datasets, so it has not presented hypothesis on how it will behave with tasks having smaller dataset etc.
* Conveying improvement with Ensemble models could have been avoided, as thats always expected.

**Results**
* NER on CoNLL03 dataset, F1 score is improved by almost 7% using BERT+BiLSTM.
* Text classification has very marginal improvement, where they leverage ensemble model.
* QQP brings about 5% improvement, where a transformer layer is added on top of BERT.
