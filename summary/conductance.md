## How Important Is a Neuron?
### Kedar Dhamdhere, Mukund Sundararajan, Qiqi Yan
### Google AI
### NIPS 2018

**Whats New** It agreegates the importance of inputs/features for prediction at neuron level, filter level or layer level, which is called conductance of a neuron or a filter for feature importance driving prediction.

**Survey of related technqiues**
* Importance of hidden unit is speculated based on activation value or product of gradient with activation. However this has undesirable behavior, for example, RELU activation would always be positive.
* Other techniques are based on tweaking input (i.e. images) to optimize activations of a neuron or a group of neuron. But there is no gurantee that all hidden units important for predictions are investigated based on tweaking inputs.

**How it Works**
* Authors have taken "Integrated Gradients" technique as a basd.
* Integrated Gradients rely on integrating gradients over a series of carefully chosen varints inputs, i.e. from baseline to given inputs. 
* Condutance is flow of Integrated Gradients attribution via the hidden unit, which is computed using decomposition of integrated gradients using chain rule.

    <img src="https://i.upmath.me/svg/%5Cmid%20IG_%7Bi%7D(x)%3A%3A%3D%5Cleft(x_%7Bi%7D-x_%7Bi%7D%5E%7B%5Cprime%7D%5Cright)%20%5Ccdot%20%5Cint_%7B%5Calpha%3D0%7D%5E%7B1%7D%20%5Cfrac%7B%5Cpartial%20F%5Cleft(x%5E%7B%5Cprime%7D%2B%5Calpha%5Cleft(x-x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D%7B%5Cpartial%20x_%7Bi%7D%7D%20d%20%5Calpha" alt="\mid IG_{i}(x)::=\left(x_{i}-x_{i}^{\prime}\right) \cdot \int_{\alpha=0}^{1} \frac{\partial F\left(x^{\prime}+\alpha\left(x-x^{\prime}\right)\right)}{\partial x_{i}} d \alpha" />

* We can define conductance of neuron y for the attribution to an input variable i as, 

    <img src="https://i.upmath.me/svg/%5Ctext%20%7B%20Cond%20%7D_%7Bi%7D%5E%7By%7D(x)%3A%3A%3D%5Cleft(x_%7Bi%7D-x_%7Bi%7D%5E%7B%5Cprime%7D%5Cright)%20%5Ccdot%20%5Cint_%7B%5Calpha%3D0%7D%5E%7B1%7D%20%5Cfrac%7B%5Cpartial%20F%5Cleft(x%5E%7B%5Cprime%7D%2B%5Calpha%5Cleft(x-x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D%7B%5Cpartial%20y%7D%20%5Ccdot%20%5Cfrac%7B%5Cpartial%20y%7D%7B%5Cpartial%20x_%7Bi%7D%7D%20d%20%5Calpha" alt="\text { Cond }_{i}^{y}(x)::=\left(x_{i}-x_{i}^{\prime}\right) \cdot \int_{\alpha=0}^{1} \frac{\partial F\left(x^{\prime}+\alpha\left(x-x^{\prime}\right)\right)}{\partial y} \cdot \frac{\partial y}{\partial x_{i}} d \alpha" />

* Total conductance of neuron y would be sum over all inputs. 

    <img src="https://i.upmath.me/svg/%5Ctext%20%7B%20Cond%20%7D%5E%7By%7D(x)%3A%3A%3D%5Csum_%7Bi%7D%5Cleft(x_%7Bi%7D-x_%7Bi%7D%5E%7B%5Cprime%7D%5Cright)%20%5Ccdot%20%5Cint_%7B%5Calpha%3D0%7D%5E%7B1%7D%20%5Cfrac%7B%5Cpartial%20F%5Cleft(x%5E%7B%5Cprime%7D%2B%5Calpha%5Cleft(x-x%5E%7B%5Cprime%7D%5Cright)%5Cright)%7D%7B%5Cpartial%20y%7D%20%5Ccdot%20%5Cfrac%7B%5Cpartial%20y%7D%7B%5Cpartial%20x_%7Bi%7D%7D%20d%20%5Calpha" alt="\text { Cond }^{y}(x)::=\sum_{i}\left(x_{i}-x_{i}^{\prime}\right) \cdot \int_{\alpha=0}^{1} \frac{\partial F\left(x^{\prime}+\alpha\left(x-x^{\prime}\right)\right)}{\partial y} \cdot \frac{\partial y}{\partial x_{i}} d \alpha" />

**Evaluation**
* Conductance was compared against three other models
    * Activation of a neuron
    * Gradient * Activation
    * Internal Influence - which is measure of feature importance, i.e. sort of integration gradient for an hidden unit contribution.
* It was shown that conductance was much better then rest methods
    * Selecting top k-filters and compute feature importance, and using those top features linear classifier performance was computed. If top k-filters are better at computing feature importance then the performance would be higher.
    * Pearson correlation coefficient between conductance and ablation score was computed, where ablation score of a filter is the drop it cause in pre-softmax score when that filter is removed. Conductance using integrated gradients has much higher pearson coefficient.

