## Huggingface's Transformers: State-of-the-art Natural Language Processing
### Wolf et al, 2020

* Its a revolutionary open-source framework for NLP community. 

* It addresses following key challanges:
    * Sharing pretrained models - Pretraining language model is computationally very expensive, it gives a platform where one can share their pretrained models, which can be leveraged for downstream supervised tasks.
    * Easy access and high performance - Model, library with standard APIs and behcmark datasets with demo scripts and documentation 
    * Interpretibility and diversity - by making hidden weights avaible, and Bertology etc
    * Pushing best practices forward, object oriented designs, and unified API layer.
    * Research to production by implementing optimzed and performant source code. Torchscript is also one intiative in this regard.

* Library design: Core components are as follow:
    * Configuration
    * Tokenizers
    * Model
    * Auto classes
    * Optimizer
    * Schedular 

* Ease of experimenting
    * Language understanding benchmarks and datasets
    * Ability to fine tune language models 