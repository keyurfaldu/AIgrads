## Lora: Low-rank adaptation of large language models.
### Hu, Edward J., et al.
### arXiv preprint arXiv:2106.09685 (2021). [[PDF](https://arxiv.org/pdf/2106.09685.pdf)]

**Key Points**

* LORA - Low Rank Adaptation to fine tune pre-trained model by freezing its weight and injecting trainable rank decomposition metric in transformer architecture. 

* Another fine tuning technique is Adapter layer, which introduce couple of adapter layer with non linearity and only those layers gets trained. But since it adds few more layers, it impacts the inference latency of the model.

* Directly optimizing promot (like prefix tuning) is hard, moreover, it also needs to reserve the part of the sequence length in the model input, which reduces the usable input size. 

* LORA aims to learn two low rank metrics A and B. 

<img src="https://i.upmath.me/svg/h%20%3D%20W_0%20x%20%2B%20%5CDelta%20Wx%20%3D%20%20W_0%20x%20%2B%20BAx%7D." alt="h = W_0 x + \Delta Wx =  W_0 x + BAx}." />

* LORA has a generalisation to full fine-tuning when the number of parameters are increased to the all weights metrics. 

* LORA doesnt cause any additional delay in the latency. The final weight metrics can be computed by summing the weights of low rank and actual pre-trained metric.

* The most significant benefit of the LORA technique is the reduction of memory and storage usage. 

* LORA has a limitations that it is not possible to back inputs from different tasks in a single batch.

* Low rank structures are inutitive in the deep learning because many learning problems have certain intrinsic low rank structure. 

* Interpretability analysis of low rank metrics with different ranks suggests that the most important vector has very high correlation with each other. 

* LORA outperforms other fine tuning methods like prefix-tuning, adapters etc, and gives performance very close to the actual fine tuning of the pretranined model. 