## Fastpitch: Parallel text-to-speech with pitch prediction.
### Łańcucki, Adrian
### In ICASSP 2021-2021 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP), pp. 6588-6592. IEEE, 2021 [[Arxiv](https://arxiv.org/pdf/2006.06873.pdf)].

**Whats Unique**
Fastpitch is a fully parallel approach for text-to-speech model, it is based on fastspeech and conditioning the fundamental freuqency contours. 

**How it works**
* It is inspired from fastspeech, where it has two Feed Forward transformer blocks, one in the dimensionality of input, and another in the dimensionality of the output. 
* It uses duration predictor, similar to fastspeech, where it uses a trained Tacotran2 model for the same.
* It does not require knowledge distillation approach for mel-spectrogram prediction, which is there in the fastspeech.
* Instead, it has pitch prediction module, which is trained alogn with, where ground truth pitch is derived for each input value.
* It is similar to fastspeech2 model, where pitch was predicted not for each value, but for each spectogram frame, which makes it bit costly.
* Architecture diagram is as follow:

<p align="center">
    <img width=600 src="images/fastpitch_arch.png">
    <em>Source: Author</em>
    </p>

* Ground truth for the pitch prediciton per input value:
<p align="center">
    <img width=600 src="images/fastpitch_pitch.png">
    <em>Source: Author</em>
    </p>

* Predicted pitch is added to the hidden representation from the first FFT block, and after which it is upsampled by the duration predicted for each input value.

<img src="https://i.upmath.me/svg/%5Chat%7B%5Cboldsymbol%7Bd%7D%7D%3D%5Ctext%20%7B%20DurationPredictor%20%7D(%5Cboldsymbol%7Bh%7D)%2C%20%5Cquad%20%5Chat%7B%5Cboldsymbol%7Bp%7D%7D%3D%5Coperatorname%7BPitchPredictor%7D(%5Cboldsymbol%7Bh%7D)%5C%5C%0A%5Cbegin%7Baligned%7D%0A%5Cboldsymbol%7Bg%7D%20%26%3D%5Cboldsymbol%7Bh%7D%2B%5Ctext%20%7B%20PitchEmbedding%20%7D(%5Cboldsymbol%7Bp%7D)%20%5C%5C%0A%5Chat%7B%5Cboldsymbol%7By%7D%7D%20%26%3D%5Coperatorname%7BFFTr%7D%5Cleft(%5B%5Cunderbrace%7Bg_%7B1%7D%2C%20%5Cldots%2C%20g_%7B1%7D%7D_%7Bd_%7B1%7D%7D%2C%20%5Cldots%20%5Cunderbrace%7Bg_%7Bn%7D%2C%20%5Cldots%2C%20g_%7Bn%7D%7D_%7Bd_%7Bn%7D%7D%5D%5Cright)%20.%0A%5Cend%7Baligned%7D" alt="\hat{\boldsymbol{d}}=\text { DurationPredictor }(\boldsymbol{h}), \quad \hat{\boldsymbol{p}}=\operatorname{PitchPredictor}(\boldsymbol{h})\\
\begin{aligned}
\boldsymbol{g} &amp;=\boldsymbol{h}+\text { PitchEmbedding }(\boldsymbol{p}) \\
\hat{\boldsymbol{y}} &amp;=\operatorname{FFTr}\left([\underbrace{g_{1}, \ldots, g_{1}}_{d_{1}}, \ldots \underbrace{g_{n}, \ldots, g_{n}}_{d_{n}}]\right) .
\end{aligned}" />

* Its inference is 900 times faster than Tacotron2.