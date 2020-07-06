## XLNet: Generalized Autoregressive Pretraining for Language Understanding
### Zhilin Yang, Zihang Dai, Yiming Yang, Jaime Carbonell, Ruslan Salakhutdinov, Quoc V. Le
### Google AI Brain, 2019

* BERT is AE (autoencoding) language modeling with the objective of denoising the corrupted input. 
* BERT leverage bidirectional context but neglects dependency between masked positions, and hence there is a pre-train and fine tune discrepancy. 
* Autoregressive models does not have such limitations, but typically they are unidirectional.
* XLNet merges pros of AE language modelling (i.e. bidirectional context) at the same time in an AR (auto-regressive) fashion, so it does not suffer from neglecting dependencies between masked tokens.
* Inorder to have AR nature and simulataneously leverage bidirectional context, XLNet proposes permutation language modelling objecitve, where it maximizes expected likelihood of language model over all permutations.
* Mathematically, formulations are as below:
    * Autoregressive Language Models:
    
        <img src="https://i.upmath.me/svg/%5Cmax%20_%7B%5Ctheta%7D%20%5Clog%20p_%7B%5Ctheta%7D(%5Cmathbf%7Bx%7D)%3D%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20%5Clog%20p_%7B%5Ctheta%7D%5Cleft(x_%7Bt%7D%20%5Cmid%20%5Cmathbf%7Bx%7D_%7B%3Ct%7D%5Cright)%3D%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20%5Clog%20%5Cfrac%7B%5Cexp%20%5Cleft(h_%7B%5Ctheta%7D%5Cleft(%5Cmathbf%7Bx%7D_%7B1%3A%20t-1%7D%5Cright)%5E%7B%5Ctop%7D%20e%5Cleft(x_%7Bt%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bx%5E%7B%5Cprime%7D%7D%20%5Cexp%20%5Cleft(h_%7B%5Ctheta%7D%5Cleft(%5Cmathbf%7Bx%7D_%7B1%3A%20t-1%7D%5Cright)%5E%7B%5Ctop%7D%20e%5Cleft(x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D" alt="\max _{\theta} \log p_{\theta}(\mathbf{x})=\sum_{t=1}^{T} \log p_{\theta}\left(x_{t} \mid \mathbf{x}_{&lt;t}\right)=\sum_{t=1}^{T} \log \frac{\exp \left(h_{\theta}\left(\mathbf{x}_{1: t-1}\right)^{\top} e\left(x_{t}\right)\right)}{\sum_{x^{\prime}} \exp \left(h_{\theta}\left(\mathbf{x}_{1: t-1}\right)^{\top} e\left(x^{\prime}\right)\right)}" />


        * x_t depends on context learnt from x_1:t-1

    * BERT: AutoEncoder Denoising Language Models:

        <img src="https://i.upmath.me/svg/%5Cmax%20_%7B%5Ctheta%7D%20%5Clog%20p_%7B%5Ctheta%7D(%5Coverline%7B%5Cmathbf%7Bx%7D%7D%20%5Cmid%20%5Chat%7B%5Cmathbf%7Bx%7D%7D)%20%5Capprox%20%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20m_%7Bt%7D%20%5Clog%20p_%7B%5Ctheta%7D%5Cleft(x_%7Bt%7D%20%5Cmid%20%5Chat%7B%5Cmathbf%7Bx%7D%7D%5Cright)%3D%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20m_%7Bt%7D%20%5Clog%20%5Cfrac%7B%5Cexp%20%5Cleft(H_%7B%5Ctheta%7D(%5Chat%7B%5Cmathbf%7Bx%7D%7D)_%7Bt%7D%5E%7B%5Ctop%7D%20e%5Cleft(x_%7Bt%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bx%5E%7B%5Cprime%7D%7D%20%5Cexp%20%5Cleft(H_%7B%5Ctheta%7D(%5Chat%7B%5Cmathbf%7Bx%7D%7D)_%7Bt%7D%5E%7B%5Ctop%7D%20e%5Cleft(x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D" alt="\max _{\theta} \log p_{\theta}(\overline{\mathbf{x}} \mid \hat{\mathbf{x}}) \approx \sum_{t=1}^{T} m_{t} \log p_{\theta}\left(x_{t} \mid \hat{\mathbf{x}}\right)=\sum_{t=1}^{T} m_{t} \log \frac{\exp \left(H_{\theta}(\hat{\mathbf{x}})_{t}^{\top} e\left(x_{t}\right)\right)}{\sum_{x^{\prime}} \exp \left(H_{\theta}(\hat{\mathbf{x}})_{t}^{\top} e\left(x^{\prime}\right)\right)}" />

        * x_hat is corrupted sentence by maksing tokens
        * x_bar are masked tokens, only those tokens are to be predicted.
        * m_t is boolean flag if its a masked token

    * XLNET:
        * XLNET objective is to maximize expected likelihood over all permutations of input text

            <img src="https://i.upmath.me/svg/%5Cmax%20_%7B%5Ctheta%7D%20%5Cquad%20%5Cmathbb%7BE%7D_%7B%5Cmathbf%7Bz%7D%20%5Csim%20%5Cmathcal%7BZ%7D_%7BT%7D%7D%5Cleft%5B%5Csum_%7Bt%3D1%7D%5E%7BT%7D%20%5Clog%20p_%7B%5Ctheta%7D%5Cleft(x_%7Bz_%7Bt%7D%7D%20%5Cmid%20%5Cmathbf%7Bx%7D_%7B%5Cmathbf%7Bz%7D_%7B%3Ct%7D%7D%5Cright)%5Cright%5D" alt="\max _{\theta} \quad \mathbb{E}_{\mathbf{z} \sim \mathcal{Z}_{T}}\left[\sum_{t=1}^{T} \log p_{\theta}\left(x_{z_{t}} \mid \mathbf{x}_{\mathbf{z}_{&lt;t}}\right)\right]" />

            * Over different permutation z, it predicts t-th word given all prior words in that permutation. And, ofcourse, since positional information is jumbled up in permuation, prediction and context both should be position aware:

            <img src="https://i.upmath.me/svg/p_%7B%5Ctheta%7D%5Cleft(X_%7Bz_%7Bt%7D%7D%3Dx%20%5Cmid%20%5Cmathbf%7Bx%7D_%7Bz_%7B%3Ct%7D%7D%5Cright)%3D%5Cfrac%7B%5Cexp%20%5Cleft(e(x)%5E%7B%5Ctop%7D%20g_%7B%5Ctheta%7D%5Cleft(%5Cmathbf%7Bx%7D_%7B%5Cmathbf%7Bz%7D_%7B%3Ct%7D%7D%2C%20z_%7Bt%7D%5Cright)%5Cright)%7D%7B%5Csum_%7Bx%5E%7B%5Cprime%7D%7D%20%5Cexp%20%5Cleft(e%5Cleft(x%5E%7B%5Cprime%7D%5Cright)%5E%7B%5Ctop%7D%20g_%7B%5Ctheta%7D%5Cleft(%5Cmathbf%7Bx%7D_%7B%5Cmathbf%7Bz%7D_%7B%3Ct%7D%7D%2C%20z_%7Bt%7D%5Cright)%5Cright)%7D" alt="p_{\theta}\left(X_{z_{t}}=x \mid \mathbf{x}_{z_{&lt;t}}\right)=\frac{\exp \left(e(x)^{\top} g_{\theta}\left(\mathbf{x}_{\mathbf{z}_{&lt;t}}, z_{t}\right)\right)}{\sum_{x^{\prime}} \exp \left(e\left(x^{\prime}\right)^{\top} g_{\theta}\left(\mathbf{x}_{\mathbf{z}_{&lt;t}}, z_{t}\right)\right)}" />

            * where g is context representation, where:
                * it should have access to positions and content for all prior tokens
                * it should have access to target position without accessing content of target postion

            * Two stream attention:
                * Content representation: h_z_t - it is similar to transformer.
                * Query representation: g_z_t - contextual information of x_z<t, and positon z_t.

                *  For each self attention layer, m = 1,...,M, the two streams of attentions is computed as follow:

                    <img src="https://i.upmath.me/svg/%5Cbegin%7Barray%7D%7Bl%7D%0Ag_%7Bz_%7Bt%7D%7D%5E%7B(m)%7D%20%5Cleftarrow%20%5Ctext%20%7B%20Attention%20%7D%5Cleft(%5Cmathrm%7BQ%7D%3Dg_%7Bz_%7Bt%7D%7D%5E%7B(m-1)%7D%2C%20%5Cmathrm%7BKV%7D%3D%5Cmathbf%7Bh%7D_%7B%5Cmathrm%7Bz%7D%3Ct%7D%5E%7B(m-1)%7D%20%3B%20%5Ctheta%5Cright)%20%5C%5C%0Ah_%7Bz_%7Bt%7D%7D%5E%7B(m)%7D%20%5Cleftarrow%20%5Ctext%20%7B%20Attention%20%7D%5Cleft(%5Cmathrm%7BQ%7D%3Dh_%7Bz_%7Bt%7D%7D%5E%7B(m-1)%7D%2C%20%5Cmathrm%7BKV%7D%3D%5Cmathbf%7Bh%7D_%7B%5Cmathrm%7Bz%7D%3Ct%7D%5E%7B(m-1)%7D%20%3B%20%5Ctheta%5Cright)%0A%5Cend%7Barray%7D" alt="\begin{array}{l}
                g_{z_{t}}^{(m)} \leftarrow \text { Attention }\left(\mathrm{Q}=g_{z_{t}}^{(m-1)}, \mathrm{KV}=\mathbf{h}_{\mathrm{z}&lt;t}^{(m-1)} ; \theta\right) \\
                h_{z_{t}}^{(m)} \leftarrow \text { Attention }\left(\mathrm{Q}=h_{z_{t}}^{(m-1)}, \mathrm{KV}=\mathbf{h}_{\mathrm{z}&lt;t}^{(m-1)} ; \theta\right)
                \end{array}" />

                * In successive transformers layer, g_z_t can only see target position, but content as well as postions for prior context, because g_i^(0) is initiatlized as w, where as h_i^(0) is initialized as e(x_i).

            * Partial prediction, since its convergence is very slow, it only does prediction of last few tokens in a factorization order.   

            * Following plot explains two stream self attentio for target aware representation

                <img src="images/xlnet_two_stream.png">

    * Overall, XLNet performs much better than BERT and Roberta. But its training time and cost is huge. It takes around 5 times more computational complexity than BERT. Training cost of XLNet is estimated between $200K to $500K. 


        





