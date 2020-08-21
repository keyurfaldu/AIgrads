## Unifying Question Answering, Text Classification, and Regression via Span Extraction
### Nitish Shirish Keskar, Bryan McCann, Caiming Xiong, Richard Socher
### Sep 2019

**Whats New**
This paper transforms regression, and classification tasks also as the span extraction, i.e. similar to question answering. And it demonstrate the impact of intermediate training and better transfer of inductive bias as a result.

**Major Takeaways**
* Span Extraction is an effective approach for unifying question answering, text classification, and regression.
* Span Extraction can also leverage intermediate training effectively, and it pass on benefits to classification and regression tasks.
* Span extractive multi tasks learning yield stronger multi tasks models. 

**How It Works**
* Following figure illustrate the approach of unifying regression, classification and question answering as span extraction problem.

    <p align="center">
        <img width=600 src="images/spanex_unified.png">
        <em>Source: Author</em>
        </p>

* It adds two trainable parameters vectors d_start and d_end, specifically to learn the possible range of start and end, and then detecting span in that range.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ap_%7B%5Ctext%20%7Bstart%7D%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(X_%7Bs%20f%7D%20d_%7B%5Ctext%20%7Bstart%7D%7D%5Cright)%20%5C%5C%0Ap_%7B%5Ctext%20%7Bend%7D%7D%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(X_%7Bs%20f%7D%20d_%7B%5Ctext%20%7Bend%7D%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
p_{\text {start}} &amp;=\operatorname{softmax}\left(X_{s f} d_{\text {start}}\right) \\
p_{\text {end}} &amp;=\operatorname{softmax}\left(X_{s f} d_{\text {end}}\right)
\end{aligned}" />

    * where, X_sf is the output from top layer of transformer.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cmathcal%7BL%7D_%7B%5Ctext%20%7Bstart%7D%7D%20%26%3D-%5Csum_%7Bi%7D%20%5Cmathrm%7BI%7D%5Cleft%5C%7Ba%5E%7B*%7D%3Di%5Cright%5C%7D%20%5Clog%20p_%7B%5Ctext%20%7Bstart%7D%7D(i)%20%5C%5C%0A%5Cmathcal%7BL%7D_%7B%5Ctext%20%7Bend%7D%7D%20%26%3D-%5Csum_%7Bi%7D%20%5Cmathrm%7BI%7D%5Cleft%5C%7Bb%5E%7B*%7D%3Di%5Cright%5C%7D%20%5Clog%20p_%7B%5Ctext%20%7Bend%7D%7D(i)%20%5C%5C%0A%5Cmathcal%7BL%7D%20%26%3D%5Cmathcal%7BL%7D_%7B%5Ctext%20%7Bstart%7D%7D%2B%5Cmathcal%7BL%7D_%7B%5Ctext%20%7Bend%7D%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\mathcal{L}_{\text {start}} &amp;=-\sum_{i} \mathrm{I}\left\{a^{*}=i\right\} \log p_{\text {start}}(i) \\
\mathcal{L}_{\text {end}} &amp;=-\sum_{i} \mathrm{I}\left\{b^{*}=i\right\} \log p_{\text {end}}(i) \\
\mathcal{L} &amp;=\mathcal{L}_{\text {start}}+\mathcal{L}_{\text {end}}
\end{aligned}" />

**Results**
* With intermediate training on Squad and MNLI, it has achieved better results over GLUE tasks as well.
* Similarily, Multi-task model also followed same trend, where best joint single model was intermediate trained on MNLI->Squad, and then to all differnt tasks.

