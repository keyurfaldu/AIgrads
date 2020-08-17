## Analysis Methods in Neural Language Processing: A Survey
### Yonatan Belinkov, James Glass
### ACL, 2019

* Two major trends:
    * Some push back against the abandonment of linguistic knowledge and call for incorporating it inside, the networks in different ways.
    * To better understand how NLP models work
* Arguments in favor of interpretability in machine learning usually mention goals like accountability, trust, fairness, safety, and reliability
* Sections:
    * What kind of linguistic information is captured in neural networks?
    * Visualization methods, and emphasizes the difficulty in evaluating visualization work
    * We discuss the compilation of challenge sets, or test suites, for fine-grained evaluation, a methodology that has old roots in NLP.
    * Deals with the generation and use of adversarial examples to probe weaknesses of neural networks
    * Summarizes work on explaining model predictions, an important goal of interpretability research.

* Relevant methods from history:
    * Analysis of english past tense learner model by Rumelhart and McClelland (1986).
    * Evaluating generalization or various linguistic phenomena, and visulizing them. (Elman, 1989)

* What linguistic information is present?
    * auxiliary prediction tasks (Adi et al., 2017b)
    * diagnostic classifiers ’ (Veldhoen et al., 2016)
    * probing tasks (Conneau et al., 2018)
    * Insights:
        * local features are somehow preserved in the lower layer whereas more global, abstract information tends to be stored in the upper layer
        * Artetxe et al. (2018) showed that word embeddings contain divergent linguistic information, which can be uncovered by applying a linear transformation on the learned embeddings.
        * Though information is captured, but have that been used? 
            * Encoder's hidden state - classifer predict tense 90% of time. But, output translation has only 79% correct tense.
            * Correlation vs causation. Giulianelli et al. (2018) intervened and changed internal hidden activation, which improved the performance.

*  Adversarial Examples
    * Adversarial examples can be generated using access to model parameters, also known as white-box attacks, or without such access, with black-box attacks.
    * White-box attacks are difficult to adapt to the text world as they typically require computing gradients with respect to the input, which would be discrete in the text case. Work around is nearest neighbour or synonym. 
    * And, they can also be classified as targeted or non-targed. Targeted are to generate adversarial example to be classified for a particular class. Whereas, non-targeted is just to mis-classify it. Targeted are harder and required to know model internal parameters etc.

* Explaining Predictions
    * a desideratum in intereptability work (Lipton, 2016), argued to increase the accountability of machine learning systems
    * Most popular approach is to use part of inputs as explanation. 
    * Or,  perturbing the input and finding the most relevant associations.

* Limitations:
    * The use of auxiliary classification tasks for identifying which linguistic properties neural networks capture has become standard practice (Section 2), while lacking both a theoretical foundation and a better empirical consideration of the link between the auxiliary tasks and the original task.
    * Relatively little work has been done on explaining predictions of neural network models, apart from providing visualizations
    * More challenge sets for evaluating other tasks besides NLI and MT are needed