## DistilBERT, a distilled version of BERT: smaller, faster, cheaper and lighter

### Victor Sanh, Lysandre Debut, Julien Chaumond, Thomas Wolf, 2020

* Major Contribution
    * Using knowledge distilation, it was possible to reduce BERT parameters by 40%, and still retaining 97% of its language understanding capabilities, and being 60% faster.
    * To leverage inductive bias of large models, it uses triple loss:
        * language modelling
        * distillation
        * cosine distance loss

* **Knowledge Distillation**: compression technique in which student model is trained to reproduce behavior of a larger mode - i.e. teacher model.
* Models's generalization capabilities lies with the distribution of near-zero probabilities, where they are larger for some classes than others. 
* Training Loss: 
    * **Distillation loss**: <img align="center" src="https://render.githubusercontent.com/render/math?math=\Large{\mathcal{L}}_{ce}%20=%20\Large{\Sigma}_i%20{t_i%20*%20log(s_i)}">,
        *  where t_i is probability learned by teacher model for class s_i in student model.
    * **Mask Language Modelling Loss**: <img align="center" src="https://render.githubusercontent.com/render/math?math=\Large{\mathcal{L}}_{mlm}">
    * **Cosine Embedding Loss**: <img align="center" src="https://render.githubusercontent.com/render/math?math=\Large{\mathcal{L}}_{cos}"> which will tend to align directions of the student and teacher hidden state vectors.

* Student Architecture:
    * Token-type embedding layers and pooler layers are removed.
    * It is emperically shown that variation on hidden size dimension has lesser impact then number of layers on computational complexity with the availability of optimized linear algebra techniques. So, focus in student models is to have lesser layers.
    * Student model is initialized from teacher model by taking one layer out of two.

* Distilbert was trained with very large batch of around 4K examples per batch.

* Ablation study shows that <img align="center" src="https://render.githubusercontent.com/render/math?math=\Large{\mathcal{L}}_{ce}"> has highest impact, also weight initialization from teacher model.



    
