## Learning to Ask: Neural Question Generation for Reading Comprehension
### Xinya Du, Junru Shao, Claire Cardie
### ACL 2017 [[arXiv](https://arxiv.org/pdf/1705.00106.pdf)]

**Whats New**
This paper presents BILSTM, encoder-decoder, and attention driven approach for question generation using SQUAD as the training data.

**How It Works**
* Token is generated based on the last hidden state, and recently computed encoder encoding
<img src="https://i.upmath.me/svg/%24P%5Cleft(y_%7Bt%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%2C%20y_%7B%3Ct%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BW%7D_%7Bs%7D%20%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Bt%7D%5Cleft%5B%5Cmathbf%7Bh%7D_%7Bt%7D%20%3B%20%5Cmathbf%7Bc%7D_%7Bt%7D%5Cright%5D%5Cright)%5Cright)" alt="$P\left(y_{t} \mid \mathbf{x}, y_{&lt;t}\right)=\operatorname{softmax}\left(\mathbf{W}_{s} \tanh \left(\mathbf{W}_{t}\left[\mathbf{h}_{t} ; \mathbf{c}_{t}\right]\right)\right)" />

* Decoder is an LSTM, which takes last generated token, and hidden state as the input, and outputs the new hidden state.
<img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bt%7D%3D%5Coperatorname%7BLSTM%7D_%7B1%7D%5Cleft(y_%7Bt-1%7D%2C%20%5Cmathbf%7Bh%7D_%7Bt-1%7D%5Cright)" alt="\mathbf{h}_{t}=\operatorname{LSTM}_{1}\left(y_{t-1}, \mathbf{h}_{t-1}\right)" />


* Encoder encodings at time t are computed as follow 
    * Bidirectional LSTM generates encoding of each token
<img src="https://i.upmath.me/svg/%5Coverrightarrow%7B%5Cmathbf%7Bb%7D_%7Bt%7D%7D%3D%5Coverline%7B%5Coperatorname%7BLSTM%7D_%7B2%7D%7D%5Cleft(x_%7Bt%7D%2C%20%5Coverrightarrow%7B%5Cmathbf%7Bb%7D_%7Bt-1%7D%7D%5Cright)%0A%24%5Coverleftarrow%7B%5Cmathbf%7Bb%7D_%7Bt%7D%7D%3D%5Coverleftarrow%7B%5Coperatorname%7BLSTM%7D_%7B2%7D%7D%5Cleft(x_%7Bt%7D%2C%20%5Coverleftarrow%7B%5Cmathbf%7Bb%7D_%7Bt%2B1%7D%7D%5Cright)" alt="\overrightarrow{\mathbf{b}_{t}}=\overline{\operatorname{LSTM}_{2}}\left(x_{t}, \overrightarrow{\mathbf{b}_{t-1}}\right)
$\overleftarrow{\mathbf{b}_{t}}=\overleftarrow{\operatorname{LSTM}_{2}}\left(x_{t}, \overleftarrow{\mathbf{b}_{t+1}}\right)" />

    * Attention is comptued based on hidden state of decoder and encoder encoding of each token

        <img src="https://i.upmath.me/svg/a_%7Bi%2C%20t%7D%3D%5Cfrac%7B%5Cexp%20%5Cleft(%5Cmathbf%7Bh%7D_%7Bt%7D%5E%7BT%7D%20%5Cmathbf%7BW%7D_%7Bb%7D%20%5Cmathbf%7Bb%7D_%7Bi%7D%5Cright)%7D%7B%5Csum_%7Bj%7D%20%5Cexp%20%5Cleft(%5Cmathbf%7Bh%7D_%7Bt%7D%5E%7BT%7D%20%5Cmathbf%7BW%7D_%7Bb%7D%20%5Cmathbf%7Bb%7D_%7Bj%7D%5Cright)%7D" alt="a_{i, t}=\frac{\exp \left(\mathbf{h}_{t}^{T} \mathbf{W}_{b} \mathbf{b}_{i}\right)}{\sum_{j} \exp \left(\mathbf{h}_{t}^{T} \mathbf{W}_{b} \mathbf{b}_{j}\right)}" />


    * Encoder encoding is attention weighted average of each token

        <img src="https://i.upmath.me/svg/%5Cmathbf%7Bc%7D_%7Bt%7D%3D%5Csum_%7Bi%3D1%2C%20%5Cldots%2C%7C%5Cmathbf%7Bx%7D%7C%7D%20a_%7Bi%2C%20t%7D%20%5Cmathbf%7Bb%7D_%7Bi%7D" alt="\mathbf{c}_{t}=\sum_{i=1, \ldots,|\mathbf{x}|} a_{i, t} \mathbf{b}_{i}" />
* Training, negative log likelihood of probability of generating token given input sentence as loss

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cmathcal%7BL%7D%20%26%3D-%5Csum_%7Bi%3D1%7D%5E%7BS%7D%20%5Clog%20P%5Cleft(%5Cmathbf%7By%7D%5E%7B(i)%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5E%7B(i)%7D%20%3B%20%5Ctheta%5Cright)%20%5C%5C%20%26%3D-%5Csum_%7Bi%3D1%7D%5E%7BS%7D%20%5Csum_%7Bj%3D1%7D%5E%7B%5Cleft%7C%5Cmathbf%7By%7D%5E%7B(i)%7D%5Cright%7C%7D%20%5Clog%20P%5Cleft(y_%7Bj%7D%5E%7B(i)%7D%20%5Cmid%20%5Cmathbf%7Bx%7D%5E%7B(i)%7D%2C%20y_%7B%3Cj%7D%5E%7B(i)%7D%20%3B%20%5Ctheta%5Cright)%20%5Cend%7Baligned%7D" alt="\begin{aligned} \mathcal{L} &amp;=-\sum_{i=1}^{S} \log P\left(\mathbf{y}^{(i)} \mid \mathbf{x}^{(i)} ; \theta\right) \\ &amp;=-\sum_{i=1}^{S} \sum_{j=1}^{\left|\mathbf{y}^{(i)}\right|} \log P\left(y_{j}^{(i)} \mid \mathbf{x}^{(i)}, y_{&lt;j}^{(i)} ; \theta\right) \end{aligned}" />


* SQUAD Data:
    * 500+ articles
    * 100000+ questions
    * Each sentence has around 1.4 questions

* Evaluation
    * BLUE 1, BLUE 2, BLUE 3, BLUE 4, METEOR, ROUGE scores were used to compare
    * Human evaluation was also done
    * System outperformed other baselines.


