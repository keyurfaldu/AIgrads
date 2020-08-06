## To Tune or Not to Tune? Adapting Pretrained Representations to Diverse Tasks
### Matthew Peters, Sebastian Ruder, and Noah A. Smith
### Allen Institute of Artifical Intelligence
### ACL 2019

**Whats New** Leveraging pretrained model is a common practice to boost performance on downstream tasks. Pretrained models can be leveraged as feature extraction or with finetuning. This paper compares performance impact of both these techniques.

**Key Insight** It makes following points
* Relative performance depends on traget tasks similarity with pre-training tasks. 
* Guidelines for NLP practitioners 
    * Optimal performance on Feature Extraction can be achieved by adding many task parameters.
    * Fine tuning needs minimal task parameters, it would rather leverage techniques like gradual unfreezing etc.
    * Fine tuning works much better when tasks are aligned with pre-training objectives, for distant tasks, feature extraction with task specific extensive parameters can be better.
    <p align="center">
    <img width=600 src="images/adapting_pretrained_repr_guidelines.png">
    <em>Source: Author</em>
    </p>

**Experiment Setup:**
* Feature extraction: exposed internal layers hidden represenations, depending on task, task specific architecture was designed i.e. NER: BiLSTM with a CRF layer, SA: Bi-attention layer classification network, Sentence pair tasks: ESIM model. 
* Fine tuning: 
    * ELMO: 
        * Text classification: max-pool over LM states, and a softmax layer. 
        * Sentence pair: cross sentence, bi-attention between LM states, pooling, softmax
        * NER: CRF layer on top of LSTM states
    * BERT:
        * Text classification / sentence pairs: Sentence represenation to softmax layer. 
        * NER: extract representaion of the first word piece for each token, and add softmax layer.

**Results**
* BERT pertraining, i.e. sentence paris, and objective, next sentence prediction, has very similarity with "semantic textual simiarity" tasks.  Hence, BERT finetuning performs significantely better for these tasks.
* Impact of target domain:
    * Jensen-Shannon divergence based on terms distribution was computed for each tasks with pre-training data. And, it was checked that if relative performance of fine tuning in comparision to feature extraction is correlated with divergence of target domain. However, no such evidence was found.
* Layer's importance was analysed using diagnostic classifier, and mutual information at each layer.

**Reflection**
* It is important topic, and this paper establishes intuitive hypothesis. However topic of intermediate training, with more similar pretraining objective, target domain data, and its effectiveness can be explored further. 