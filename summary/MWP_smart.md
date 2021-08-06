## SMART: A Situation Model for Algebra Story Problems via Attributed Grammar.
### Hong, Yining, Qing Li, Ran Gong, Daniel Ciao, Siyuan Huang, and Song-Chun Zhu. 
### In Proceedings of the AAAI Conference on Artificial Intelligence, vol. 35, no. 14, pp. 13009-13017. 2021. [[PDF](https://arxiv.org/pdf/2012.14011.pdf)]

**Whats Unique**
This paper adopts attributed grammer to build situation representation for the algebra story problems. First, extract information for nodes, attributes, events and relations and then build a parse graph. And it learns this process in an iterative way.

**How Does It Work**
* The basic motivation of this paper comes from human's intuitive way of thinking. Which first build a situation model in the mind to answer a math story question. It could be understood with the figure below:
    <p align="center">
    <img width=600 src="images/MWP_smart_motivation.png">
    <em>Source: Author</em>
    </p>
* It adopts attributed grammer, which represents World, Agent, Events, and Relations.
* In the context of MWP, using NER it extacts following entities: 
    * Nodes : World, Agent, Events (V_pg)
    * Attributes: values of nodes etc (A_pg)
    * Relations; (E_pg)
* Parse graph is created by joining these nodes based on their distances in the problem text, and distance between dependency tree. 
* Given Nodes, Attributes, and Relations as text, it uses seq2seq model to generate equation.
* So it formulate the problem to get the parse_graph as follow:

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ap%20g%5E%7B*%7D%26%3D%5Carg%20%5Cmax%20_%7Bp%20g%20%5Cin%20%5Cmathcal%7BL%7D(G)%7D%20p(p%20g%20%5Cmid%20x)%5C%5C%0Ap(p%20g%20%5Cmid%20x)%20%26%3Dp%5Cleft(V_%7Bp%20g%7D%2C%20A_%7Bp%20g%7D%2C%20E_%7Bp%20g%7D%20%5Cmid%20x%5Cright)%20%5C%5C%0A%26%3Dp%5Cleft(V_%7Bp%20g%7D%20%5Cmid%20x%5Cright)%20%5Ccdot%20p%5Cleft(A_%7Bp%20g%7D%20%5Cmid%20x%5Cright)%20%5Ccdot%20p%5Cleft(E_%7Bp%20g%7D%20%5Cmid%20x%5Cright)%5C%5C%0Ap%5Cleft(E_%7Bp%20g%7D%20%5Cmid%20x%5Cright)%26%3D%5Csum_%7Be%20%5Cin%20E_%7Bp%20g%7D%7D%20p_%7B%5Ctext%20%7Bseq%20%7D%202%20s%20e%20q%7D%5Cleft(e%20%5Cmid%20%5Cmathrm%7BREL%7D%2C%20V_%7Bp%20g%7D%2C%20A_%7Bp%20g%7D%5Cright)%5C%5C%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
p g^{*}&amp;=\arg \max _{p g \in \mathcal{L}(G)} p(p g \mid x)\\
p(p g \mid x) &amp;=p\left(V_{p g}, A_{p g}, E_{p g} \mid x\right) \\
&amp;=p\left(V_{p g} \mid x\right) \cdot p\left(A_{p g} \mid x\right) \cdot p\left(E_{p g} \mid x\right)\\
p\left(E_{p g} \mid x\right)&amp;=\sum_{e \in E_{p g}} p_{\text {seq } 2 s e q}\left(e \mid \mathrm{REL}, V_{p g}, A_{p g}\right)\\
\end{aligned}" />

* Iterative Learning: It builds parge graph using naive methods, and if it evaluates to true answer it becomes the labelled data, and on wich the parge-graph generator model would get trained. The process repeats till it converge.

* Following figure gives the overview of the system:
    <p align="center">
    <img width=600 src="images/MWP_smart_overview.png">
    <em>Source: Author</em>
    </p>

* It extracted story types problems, where there are entities/characters etc. It found around 6.6K problems to form the dataset ASP6.6K from Math23K dataset. These 6.6K problems are distributed over four categories, Motion, Task, Relation, and Price.



