## Accurate short-term analysis of the fundamental frequency and the harmonics-to-noise ratio of a sampled sound
### Boersma, Paul.
### In Proceedings of the institute of phonetic sciences, vol. 17, no. 1193, pp. 97-110. 1993. [PDF](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.218.4956&rep=rep1&type=pdf)

**Whats Unique**
This paper layous out mathematical technique to extract the fundamental frequency and harmonics to noise ratio for any given window of the signal.

**How It Works**
* Autocorrelation and Periodicity: Autocorrelation would be maximum at the time lag of 0, so normalized auto-correlation can be computed by dividing it.

    <img src="https://i.upmath.me/svg/r_%7Bx%7D(%5Ctau)%20%5Cequiv%20%5Cint%20x(t)%20x(t%2B%5Ctau)%20d%20t%20%5C%5C%0Ar_%7Bx%7D%5E%7B%5Cprime%7D(%5Ctau)%20%5Cequiv%20%5Cfrac%7Br_%7Bx%7D(%5Ctau)%7D%7Br_%7Bx%7D(0)%7D" alt="r_{x}(\tau) \equiv \int x(t) x(t+\tau) d t \\
r_{x}^{\prime}(\tau) \equiv \frac{r_{x}(\tau)}{r_{x}(0)}" />

* Noise: Generally, signal would have noise into it. And, if noise is cancelling out each other, then we would find the maximum autocorrelation at the T0 which is the fundamental fequence of the signal. r'_x(T0) would be equal to the share of autocorrelation due to the signal.

    <img src="https://i.upmath.me/svg/r_%7Bx%7D(0)%3Dr_%7BH%7D(0)%2Br_%7BN%7D(0)%5C%5C%0Ar_%7Bx%7D%5Cleft(%5Ctau_%7B%5Cmax%20%7D%5Cright)%3Dr_%7BH%7D%5Cleft(T_%7B0%7D%5Cright)%3Dr_%7BH%7D(0)%5C%5C%0Ar_%7Bx%7D%5E%7B%5Cprime%7D%5Cleft(%5Ctau_%7B%5Cmax%20%7D%5Cright)%3D%5Cfrac%7Br_%7BH%7D(0)%7D%7Br_%7Bx%7D(0)%7D%20%5Cquad%20%3B%20%5Cquad%201-r_%7Bx%7D%5E%7B%5Cprime%7D%5Cleft(%5Ctau_%7B%5Cmax%20%7D%5Cright)%3D%5Cfrac%7Br_%7BN%7D(0)%7D%7Br_%7Bx%7D(0)%7D" alt="r_{x}(0)=r_{H}(0)+r_{N}(0)\\
r_{x}\left(\tau_{\max }\right)=r_{H}\left(T_{0}\right)=r_{H}(0)\\
r_{x}^{\prime}\left(\tau_{\max }\right)=\frac{r_{H}(0)}{r_{x}(0)} \quad ; \quad 1-r_{x}^{\prime}\left(\tau_{\max }\right)=\frac{r_{N}(0)}{r_{x}(0)}" />

* Harmonics ratio can be derived as, 
    <img src="https://i.upmath.me/svg/H%20N%20R(%5Ctext%20%7B%20in%20%7D%20%5Cmathrm%7BdB%7D)%3D10%20%5Ccdot%7B%20%7D%5E%7B10%7D%20%5Clog%20%5Cfrac%7Br_%7Bx%7D%5E%7B%5Cprime%7D%5Cleft(%5Ctau_%7B%5Cmax%20%7D%5Cright)%7D%7B1-r_%7Bx%7D%5E%7B%5Cprime%7D%5Cleft(%5Ctau_%7B%5Cmax%20%7D%5Cright)%7D" alt="H N R(\text { in } \mathrm{dB})=10 \cdot{ }^{10} \log \frac{r_{x}^{\prime}\left(\tau_{\max }\right)}{1-r_{x}^{\prime}\left(\tau_{\max }\right)}" />

* Window function w(t) (hanning window or sine-squared window) is applied to get windowed signal

    <img src="https://i.upmath.me/svg/a(t)%3D%5Cleft(x%5Cleft(t_%7Bm%20i%20d%7D-%5Cfrac%7B1%7D%7B2%7D%20T%2Bt%5Cright)-%5Cmu_%7Bx%7D%5Cright)%20w(t)%5C%5C%0Aw(t)%3D%5Cfrac%7B1%7D%7B2%7D-%5Cfrac%7B1%7D%7B2%7D%20%5Ccos%20%5Cfrac%7B2%20%5Cpi%20t%7D%7BT%7D" alt="a(t)=\left(x\left(t_{m i d}-\frac{1}{2} T+t\right)-\mu_{x}\right) w(t)\\
w(t)=\frac{1}{2}-\frac{1}{2} \cos \frac{2 \pi t}{T}" />

* Normalized auto-correlation on the windowed signal is computed

<img src="https://i.upmath.me/svg/r_%7Ba%7D(%5Ctau)%3Dr_%7Ba%7D(-%5Ctau)%3D%5Cfrac%7B%5Cint_%7B0%7D%5E%7BT-%5Ctau%7D%20a(t)%20a(t%2B%5Ctau)%20d%20t%7D%7B%5Cint_%7B0%7D%5E%7BT%7D%20a%5E%7B2%7D(t)%20d%20t%7D" alt="r_{a}(\tau)=r_{a}(-\tau)=\frac{\int_{0}^{T-\tau} a(t) a(t+\tau) d t}{\int_{0}^{T} a^{2}(t) d t}" />

* Nomralized auto-correlation of the window function w(t) is also computed, and, it is divided to nullify the effect of window in the auto-corrlation

    <img src="https://i.upmath.me/svg/r_%7Bw%7D(%5Ctau)%3D%5Cleft(1-%5Cfrac%7B%7C%5Ctau%7C%7D%7BT%7D%5Cright)%5Cleft(%5Cfrac%7B2%7D%7B3%7D%2B%5Cfrac%7B1%7D%7B3%7D%20%5Ccos%20%5Cfrac%7B2%20%5Cpi%20%5Ctau%7D%7BT%7D%5Cright)%2B%5Cfrac%7B1%7D%7B2%20%5Cpi%7D%20%5Csin%20%5Cfrac%7B2%20%5Cpi%7C%5Ctau%7C%7D%7BT%7D%5C%5C%0Ar_%7Bx%7D(%5Ctau)%20%5Capprox%20%5Cfrac%7Br_%7Ba%7D(%5Ctau)%7D%7Br_%7Bw%7D(%5Ctau)%7D" alt="r_{w}(\tau)=\left(1-\frac{|\tau|}{T}\right)\left(\frac{2}{3}+\frac{1}{3} \cos \frac{2 \pi \tau}{T}\right)+\frac{1}{2 \pi} \sin \frac{2 \pi|\tau|}{T}\\
r_{x}(\tau) \approx \frac{r_{a}(\tau)}{r_{w}(\tau)}" />

* Fundamental freq is derived where r_x(t) is maximum apart from zero.

* Following figure gives detailed illustration.

    <p align="center">
    <img width=600 src="images/fundamental_freq_illutration.png">
    <em>Source: Author</em>
    </p>

