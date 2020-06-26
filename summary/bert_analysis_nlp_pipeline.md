## BERT Rediscovers the Classical NLP Pipeline
### Ian Tenney, Dipanjan Das, Ellie Pavlick

Major Contributions:
* Edge Probing:
    * Probing Classifiers recieves spans s_1 = [i1, j1) and (optionally) s2 = [i2, j2), and must predict a label such as a constituent or relation type.
    * Probing classifers has access to only per token encodings with in the spans.
* Metrics:
    * Sclar Mixing Weights
        * Basically, token representation at each hiddgen layer is mixed using probability distribution derived for each task using softmax.

        <p align="center">
        <img align="centre" src="https://render.githubusercontent.com/render/math?math=\Large%20h_{i,\tau}_%20=%20\gamma\sum_{l=0}^{L} s_\tau^{(l)} * h_i^{(l)}">
        </p>

        * Where, s_τ = softmax(a_τ), and scalar parameters γτ and aτ are parameters learned while training probing classifer.
    * Center of gravity
        * For each task, center of gravity is basically expectation over layer number with its probabilities coming from softmax output.
         <p align="center">
        <img src="https://i.upmath.me/svg/%5Cmathbb%7BE%7D_s%5E%7B(l)%7D%20%3D%20%5CSigma_%7Bl%3D0%7D%5E%7BL%7Dl*s_%5Ctau%5E%7B(l)%7D" alt="\mathbb{E}_s^{(l)} = \Sigma_{l=0}^{L}l*s_\tau^{(l)}" />
        </p>
    * Cumulative scoring: 
        * Series of classifiers are trained, <img src="https://i.upmath.me/svg/%7BP_%5Ctau%5E%7B(l)%7D" alt="{P_\tau^{(l)}" />, which use scalar mixing to layer l as well as all previous layers for task τ.
        * Differential score is computed that how much each layer adds value
        <img src="https://i.upmath.me/svg/%5CDelta_%5Ctau%5E%7B(l)%7D%20%3D%20Score(P_%5Ctau%5E%7B(l)%7D)%20-%20Score(P_%5Ctau%5E%7B(l-1)%7D)" alt="\Delta_\tau^{(l)} = Score(P_\tau^{(l)}) - Score(P_\tau^{(l-1)})" />
    * Expected layer:
        * (pseudo) Expectation by taking how much relative contribution made by layer l. 
        <img src="https://i.upmath.me/svg/%5Cmathbb%7BE%7D_%5CDelta(l)%20%3D%20%5Cfrac%7B%5CSigma_%7Bl%3D1%7D%5E%7Bl%7Dl*%5CDelta_%5Ctau%5E%7B(l)%7D%7D%7B%5CSigma_%7Bl%3D1%7D%5E%7Bl%7D%5CDelta_%5Ctau%5E%7B(l)%7D%7D" alt="\mathbb{E}_\Delta(l) = \frac{\Sigma_{l=1}^{l}l*\Delta_\tau^{(l)}}{\Sigma_{l=1}^{l}\Delta_\tau^{(l)}}" />
* Insights:
    * As we can see in the figure below, syntatics taks are solved in earlier layers of BERT, while deep semantic tasks have expected layer higher. 
    <p align="center">
    <img src="images/bert_analysis_nlp_center_of_gravity_expected_layer.png"></p>
    * Distribution scaling weights (softmax) and differntial weights further reinforces the value addition of each layer for various tasks.
    <p align="center"><img src="images/bert_analysis_nlp_scaling_weights_differential_scores.png"></p>


                
        


    