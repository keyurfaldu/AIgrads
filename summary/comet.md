## COMET : Commonsense Transformers for Automatic Knowledge Graph Construction
### Bosselut et al
### ACL 2019

**Whats new**
This paper studies if commonsense knowledge in KG canonical form of (subject, releation, object) can be generated? Specifically, given subject and relation, can plausible objects be generated? Authors applies transformers on two commensense database, and analyse results to demonstrate the possibility.

**How it works?**
* Two datasets were considered, ATOMIC and ConceptNet
* Loss function was, given subject and relation, can objects be generated?
<img src="https://i.upmath.me/svg/%5Cmathcal%7BL%7D%3D-%5Csum_%7Bt%3D%7Cs%7C%2B%7Cr%7C%7D%5E%7B%7Cs%7C%2B%7Cr%7C%2B%7Co%7C%7D%20%5Clog%20P%5Cleft(x_%7Bt%7D%20%5Cmid%20x_%7B%3Ct%7D%5Cright)" alt="\mathcal{L}=-\sum_{t=|s|+|r|}^{|s|+|r|+|o|} \log P\left(x_{t} \mid x_{&lt;t}\right)" />

* ATOMIC Experiments:
    * Evaluation criteria were preplexity, BLUE-2, Novality score, and Human evaluated plasibility.
    * For each relation, 100 random events were chosen, nad 10 candidates were selected based on beam search, and 5 works gave a plausibility ratings. COMET scored aroud 56%, and when it was a greedy decoding, it scores as high as 77%, which is close to human atomic baseline of 86.18%.
    * Ablation study was performed to discretise the gains of learning due to pre-training, i.e. 14% relative weight. Greedy decoding has given 10% relative gain, and, even after using just 10% of training data, model is able to generate plausible objects.

* ConceptNet Experiments:
    * pre-trained Bilinear AVG model (Li et al. 2016) was used to test whether a tuple is correct or not. This model was trained on plausible tubles vs random tuples to predict if its correct or not.
    * BiLSTM model was implemented as a baseline model to compare it with transformers based Comet. 
    * Human evaulation was also reported. 
    * To check how creative/generative model was, edit distance of generated objects, with training tuples were computed, and accuracy with edit distance was measured to check, how performance is impacted when edit distance gets larger.
    * Pretraing impact, and represeting relations in natural lanauge - ablation study was performed.
    * Comet has done much better on above setup, i.e. human evaluation suggest 91.7% performance, compared to around 54% by Bi-LSTM baseline.

**Reflection**
* Its very early stage for the problem of "commonsense knowledge base construction" problem. I.e. it would be great if some test data / benchmark is created to put discipline around testing and reporting performance. Currently it is like language model, but just tweaked to operated in subject, relation, object manner. And, human evaluation was used to report if object generated is plausible or not. It would be better if common sense is based on some input text, i.e. not just he plausibility but also if its factual or not.