## Semantically-aligned universal tree-structured solver for math word problems.
### Jinghui Qin, Lihui Lin, Xiaodan Liang, Rumin Zhang, and Liang Lin. 2020.
### In Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing ([EMNLP](https://aclanthology.org/2020.emnlp-main.309.pdf)), pages 3780–3789.

**Whats Unique**
This paper brings three novelties, 1) Universal Expression Tree to handle multiple equations, 2) New challanging Hybrid Math Word Problems dataset, 3) Semantically algined new tree-structure decoder.

**How Does It Work**
* Universal Expression Tree: As can be seen in the figure below, different equations are concatenated in the tree with the special symbol ";". It also introduces multiple unknowns like x, y etc.

<p align="center">
<img width=600 src="images/SAU_equation_tree.png">
<em>Source: Author</em>
</p>

* Semantically aligend Tree-structued decoder: SAU Solver
As shown in the figure below, a new token is generated by attending its parent, or subtree from the sibling and attention weighted encoder represnetation on the problem. 

<p align="center">
<img width=600 src="images/SAU_architecture.png">
<em>Source: Author</em>
</p>

* Semantically aligned regularization: It generates attention weighed encoder representation for a subtree representation. It transforms both into a vector space, where they should be semantically aligned.

    <img src="https://i.upmath.me/svg/%5Cmathbf%7Be%7D_%7Bs%20a%7D%3D%5Cmathbf%7BW%7D_%7Be%202%7D%20%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Be%201%7D%20%5Cmathbf%7Ba%7D%5Cright)%5C%5C%0A%5Cmathbf%7Bd%7D_%7Bs%20a%7D%3D%5Cmathbf%7BW%7D_%7Bd%202%7D%20%5Ctanh%20%5Cleft(%5Cmathbf%7BW%7D_%7Bd%201%7D%20%5Cmathbf%7Bt%7D%5Cright)%5C%5C%0A%5Cmathcal%7BL%7D_%7Bs%20a%7D(T%20%5Cmid%20P)%3D%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_%7Bi%3D1%7D%5E%7Bm%7D%5Cleft%5C%7C%5Cmathbf%7Bd%7D_%7Bs%20a%7D-%5Cmathbf%7Be%7D_%7Bs%20a%7D%5Cright%5C%7C_%7B2%7D" alt="\mathbf{e}_{s a}=\mathbf{W}_{e 2} \tanh \left(\mathbf{W}_{e 1} \mathbf{a}\right)\\
\mathbf{d}_{s a}=\mathbf{W}_{d 2} \tanh \left(\mathbf{W}_{d 1} \mathbf{t}\right)\\
\mathcal{L}_{s a}(T \mid P)=\frac{1}{m} \sum_{i=1}^{m}\left\|\mathbf{d}_{s a}-\mathbf{e}_{s a}\right\|_{2}" />

* It demonstrates the improvement across different datasets like HMWP, ALG514, Math23K, Dolphin18K etc.