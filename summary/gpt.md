## Improving Language Understanding by Generative Pre-Training
### Alec Radford, Karthik Narasimhan, Tim Salimans, Ilya Sutskever @ OpenAI, 2018

* GPT was one of the first paper to leverage transformer-decoder architecture to train left-to-right language model and further reinforce concept of generative pre-training and discriminative fine-tuning.

* Generative pre-trarining:
    * It is trained with language model objective which is supervised pre-learning which can be applied on raw data.
    
    
        <img src="https://i.upmath.me/svg/L_%7B1%7D(%5Cmathcal%7BU%7D)%3D%5Csum%20%5Clog%20P%5Cleft(u_%7Bi%7D%20%5Cmid%20u_%7Bi-k%7D%2C%20%5Cldots%2C%20u_%7Bi-1%7D%20%3B%20%5CTheta%5Cright)" alt="L_{1}(\mathcal{U})=\sum \log P\left(u_{i} \mid u_{i-k}, \ldots, u_{i-1} ; \Theta\right)" />

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ah_%7B0%7D%20%26%3DU%20W_%7Be%7D%2BW_%7Bp%7D%20%5C%5C%0Ah_%7Bl%7D%20%26%3D%5Coperatorname%7Btransformer%7D_%7B-%7D%20%5Ctext%20%7Bblock%20%7D%5Cleft(h_%7Bl-1%7D%5Cright)%20%5Cforall%20i%20%5Cin%5B1%2C%20n%5D%20%5C%5C%0AP(u)%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(h_%7Bn%7D%20W_%7Be%7D%5E%7BT%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
        h_{0} &amp;=U W_{e}+W_{p} \\
        h_{l} &amp;=\operatorname{transformer}_{-} \text {block }\left(h_{l-1}\right) \forall i \in[1, n] \\
        P(u) &amp;=\operatorname{softmax}\left(h_{n} W_{e}^{T}\right)
        \end{aligned}" />

    * As shown above, W_e is word embedding matrix, and W_p is positional embeddings. Token u is predicted given prior tokens.

* Supervised fine-tuning
    * Labels y is available for input sequence x_1, .. x_n. Inputs are transformed using transformer block activations, and are passed to linear output layer with parameters W_y to predict y.

        <img src="https://i.upmath.me/svg/P%5Cleft(y%20%5Cmid%20x%5E%7B1%7D%2C%20%5Cldots%2C%20x%5E%7Bm%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(h_%7Bl%7D%5E%7Bm%7D%20W_%7By%7D%5Cright)" alt="P\left(y \mid x^{1}, \ldots, x^{m}\right)=\operatorname{softmax}\left(h_{l}^{m} W_{y}\right)" />

    * Objective is to maximize log-liklihood of the probabilities of these labels.

        <img src="https://i.upmath.me/svg/L_%7B2%7D(%5Cmathcal%7BC%7D)%3D%5Csum_%7B(x%2C%20y)%7D%20%5Clog%20P%5Cleft(y%20%5Cmid%20x%5E%7B1%7D%2C%20%5Cldots%2C%20x%5E%7Bm%7D%5Cright)" alt="L_{2}(\mathcal{C})=\sum_{(x, y)} \log P\left(y \mid x^{1}, \ldots, x^{m}\right)" />

    * **Auxiliary Objective** in fine tuning phase improves results by (a) improving regularization, (b) accelerating convergence. 

        <img src="https://i.upmath.me/svg/L_%7B3%7D(%5Cmathcal%7BC%7D)%3DL_%7B2%7D(%5Cmathcal%7BC%7D)%2B%5Clambda%20*%20L_%7B1%7D(%5Cmathcal%7BC%7D)" alt="L_{3}(\mathcal{C})=L_{2}(\mathcal{C})+\lambda * L_{1}(\mathcal{C})" />

        * Where, L2 is task specific objective and L1 is language model objective serving as auxiliary objective in fine tuning mode.

    * Architecture of GPT is seen in image below: 
    <img src="images/gpt_arch.png">
        * Question similarity task is fed into transformer as two independent sequences, and which are then fed to a linear block to classify into similar or disimilar.
        * Multiple choices questions are passed as independent sequences for each answer option to linear blocks, which further given to softmax layer to get probability distribution.

* Analysis: 
    * It shows number of layers in transformer blocks positively impact output.
    * Also, pretraining updates also helps task performance. and, transformer block is more effective then LSTM block.
    * Alation study was carried out to establish following:
        * Transformers without pre-tranining (-14%)
        * Transformer without auxiliary language modelling objective (~%)
        * replacing LSTM with aux LM. (-6%)

* GLUE SOTA was taken from 68.9 to 72.8% performance