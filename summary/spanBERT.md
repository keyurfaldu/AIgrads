## SpanBERT: Improving Pre-training by Representing and Predicting Spans ##

Mandar Joshi, Danqi Chen, Yinhan Liu, Daniel S. Weld,  Luke Zettlemoyer, Omer Levy

Transactions of the Association for Computational Linguistics, vol. 8, pp. 64–77, 2020

Major Contributions:
* **Masking Random Contienous Spans**:
    * Continue till 15% tokens are maksed, 
        * sample a span length from geometric distribution
        * randomly select starting point of the span to be masked
    
* **Span Boundary Objective (SBO)**:
    * To predict entire masked span from observed tokens at its boundary
    * Encourage model to store span level information at its boundary, which is easily accessible during fine tuning.
    * It replaces NSP objective
    * Given masked tokens <img src="https://render.githubusercontent.com/render/math?math=\Large(x_s,%20...,%20x_e)%20\in%20Y">, it represent each token x_i in the span using the output encodings of external boundary tokens x_s-1, x_e+1, and positional encoding. So, 

   <p align="center"> <img align="center" src="https://render.githubusercontent.com/render/math?math=\Large%20y_i%20=%20f(x_{s-1},%20x_{e%2B1},%20P_{i%20-%20s%2B1})"> </p>

 

   * SBO function is implemented as 2-layer feedforward network with GELU activations and layer normalization.

   * Cross entropy loss is computed for predicted token in span, exactly like MLM.

* **Single Sequence BERT**:
    * Pre training on single segments, instead of two half-length segments with NSP.
    * Do not use NSP objective

* **Objective Function**:
    * SpanBERT sums the loss from both SBO and MLM. 
   <p align="center"> <img align="center" src="https://render.githubusercontent.com/render/math?math=\Large%20\mathcal{L}(x_i)%20=%20\mathcal{L}_{MLM}(x_i)%2B\mathcal{L}_{SBO}(x_i)"> </p>
