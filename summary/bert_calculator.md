## Giving BERT a Calculator: Finding Operations and Arguments with Reading Comprehension
### Daniel Andor, Luheng He, Kenton Lee, Emily Pitler
### ACL 2019

**Whats New**
This paper augment BERT model with light weight executable programs for simple numerical operations, to perform discrete math operations over comprehension tasks. Rather than learning to manipulate numbers directly, the model pick a program to execute it.

**How It Works**
* Model is trained and validated on dataset DROP - Discrete Reasoning Over Passages. Example from DROP can be shown as below.
    <p align="center">
        <img width=600 src="images/bert_calc_drop_example.png">
        <em>Source: Author</em>
        </p>
* Model picks simple programs like Operations(args, ...)
* Where possible operations include span extraction, answering yes or no, or arithmatic.
* This model presents its effectiveness over following dimension:
    * Simple unary and binary operations
    * Compositions
    * Pre-training on CoQA and applying over DROP
    * Few-shot learning on illionis dataset (for multiplication and division)
* Model
    * BERT model is extended with light weight extraction and composition layer.
    * Model predict derivation d (progra) given Passage P and Question Q. 
    * Derivations:
        * Literals: Yes/No/0..9
        * Numerical Operations: Sum / Diff
        * Text Spans: Composition of tokens in to text-spans
        * Composition of compositions: Sum3, Merge 
    * Model Representation and Scoring:
        * Literatls: <img src="https://i.upmath.me/svg/%5Crho(d)%3D%5Cmathbf%7Bw%7D_%7Bd%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7BM%7D%20%5Cmathbf%7BL%7D%20%5Cmathbf%7BP%7D_%7B%5Cmathrm%7Blit%7D%7D%5Cleft(%5Cmathbf%7Bh%7D_%7B%5Cmathrm%7BCLS%7D%7D%5Cright)" alt="\rho(d)=\mathbf{w}_{d}^{\top} \mathbf{M} \mathbf{L} \mathbf{P}_{\mathrm{lit}}\left(\mathbf{h}_{\mathrm{CLS}}\right)" />
        * Numerical Operations: 
            * <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bd%7D%3D%5Cmathbf%7BM%20L%20P%7D_%7B%5Ctext%20%7Bbinary%20%7D%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%2C%20%5Cmathbf%7Bh%7D_%7Bj%7D%2C%20%5Cmathbf%7Bh%7D_%7Bi%7D%20%5Ccirc%20%5Cmathbf%7Bh%7D_%7Bj%7D%5Cright)" alt="\mathbf{h}_{d}=\mathbf{M L P}_{\text {binary }}\left(\mathbf{h}_{i}, \mathbf{h}_{j}, \mathbf{h}_{i} \circ \mathbf{h}_{j}\right)" />
            * <img src="https://i.upmath.me/svg/%5Crho(d)%3D%5Cmathbf%7Bw%7D_%7Bo%20p%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7Bh%7D_%7Bd%7D" alt="\rho(d)=\mathbf{w}_{o p}^{\top} \mathbf{h}_{d}" />
        * Text spans
            * <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bd%7D%3D%5Cmathbf%7BM%20L%20P%7D_%7B%5Ctext%20%7Bspan%20%7D%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bi%7D%2C%20%5Cmathbf%7Bh%7D_%7Bj%7D%5Cright)" alt="\mathbf{h}_{d}=\mathbf{M L P}_{\text {span }}\left(\mathbf{h}_{i}, \mathbf{h}_{j}\right)" />
            * <img src="https://i.upmath.me/svg/%5Crho(d)%3D%5Cmathbf%7Bw%7D_%7B%5Cmathrm%7Bspan%7D%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7Bh%7D_%7Bd%7D" alt="\rho(d)=\mathbf{w}_{\mathrm{span}}^{\top} \mathbf{h}_{d}" />
        * Compositions of composition:
            * <img src="https://i.upmath.me/svg/%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7BSum3%20%7D%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7BM%20L%20P%7D_%7B%5Ctext%20%7BSum3%20%7D%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bd%200%7D%2C%20%5Cmathbf%7Bh%7D_%7Bk%7D%5Cright)" alt="\mathbf{w}_{\text {Sum3 }}^{\top} \mathbf{M L P}_{\text {Sum3 }}\left(\mathbf{h}_{d 0}, \mathbf{h}_{k}\right)" />
            * <img src="https://i.upmath.me/svg/%5Cmathbf%7Bw%7D_%7B%5Ctext%20%7BMerge%20%7D%7D%5E%7B%5Ctop%7D%20%5Cmathbf%7BM%7D%20%5Cmathbf%7BL%7D%20P_%7B%5Ctext%20%7BMerge%20%7D%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bd%200%7D%2C%20%5Cmathbf%7Bh%7D_%7Bd%201%7D%2C%20%5Cmathbf%7Bh%7D_%7Bd%200%7D%20%5Ccirc%20%5Cmathbf%7Bh%7D_%7Bd%201%7D%5Cright)" alt="\mathbf{w}_{\text {Merge }}^{\top} \mathbf{M} \mathbf{L} P_{\text {Merge }}\left(\mathbf{h}_{d 0}, \mathbf{h}_{d 1}, \mathbf{h}_{d 0} \circ \mathbf{h}_{d 1}\right)" />
    * Training: 
        * While training, exhaustive pre-computed oracle derivations D* were used, and marginalised all d* that lead to an answer. 
        * <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cmathcal%7BJ%7D%5Cleft(P%2C%20Q%2C%20%5Cmathcal%7BD%7D%5E%7B*%7D%5Cright)%20%26%3D-%5Clog%20%5Csum_%7Bd%5E%7B*%7D%20%5Cin%20%5Cmathcal%7BD%7D%5E%7B*%7D%7D%20P%5Cleft(d%5E%7B*%7D%20%5Cmid%20P%2C%20Q%5Cright)%20%5C%5C%0AP(d%20%5Cmid%20P%2C%20Q)%20%26%3D%5Cfrac%7B%5Cexp%20%5Crho(d%2C%20P%2C%20Q)%7D%7B%5Csum_%7Bd%5E%7B%5Cprime%7D%7D%20%5Cexp%20%5Crho%5Cleft(d%5E%7B%5Cprime%7D%2C%20P%2C%20Q%5Cright)%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\mathcal{J}\left(P, Q, \mathcal{D}^{*}\right) &amp;=-\log \sum_{d^{*} \in \mathcal{D}^{*}} P\left(d^{*} \mid P, Q\right) \\
P(d \mid P, Q) &amp;=\frac{\exp \rho(d, P, Q)}{\sum_{d^{\prime}} \exp \rho\left(d^{\prime}, P, Q\right)}
\end{aligned}" />
    * During inference, possible space of derivation can grow quadratic with compostions, so, only top 128 span and sum results were used to compute merge and sum3. 
* Results:
    * Following figure demonstrate the impact of model, its ablation study, and over differnt types of questions, and comparision with respect to Oracle.
    <p align="center">
        <img width=600 src="images/bert_calc_results.png">
        <em>Source: Author</em>
        </p>
    * Model was also easily able to learn other operations like multiplication and division on very small data Illionis math word problems dataset.







