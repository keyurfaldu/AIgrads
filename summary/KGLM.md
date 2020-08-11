## Barack’s Wife Hillary: Using Knowledge Graphs for Fact-Aware Language Modeling
### Robert L. Logan IV, Nelson F. Liu, Matthew E. Peters, Matt Gardner, Sameer Singh
### ACL 2019

**Whats new** This paper presents a novel KGLM Knowledeg Graph Langauge Model which has capability to select and copy facts from Knowledge Graph while generating language.

**Key Insights**
* Generally, language model learns the probability of popular patterns and it mimicks them. 
* Typically, facts presents in knowledge graph might not be redered by language models because of data scarcity problem
* That creates the opportunity to assist langauge model to select info from KG while generating the text.

**How it works**
* RNN Langauge models parameterise the distribution as follow
<img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0Ap%5Cleft(x_%7Bt%7D%20%5Cmid%20x_%7B%3Ct%7D%5Cright)%20%26%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7BW%7D_%7Bh%7D%20%5Cmathbf%7Bh%7D_%7Bt%7D%2B%5Cmathbf%7Bb%7D%5Cright)%20%5C%5C%0A%5Cmathbf%7Bh%7D_%7Bt%7D%20%26%3D%5Cmathbf%7BR%7D%20%5Cmathbf%7BN%7D%20%5Cmathbf%7BN%7D%5Cleft(%5Cmathbf%7Bh%7D_%7Bt-1%7D%2C%20%5Cmathbf%7Bx%7D_%7Bt-1%7D%5Cright)%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
p\left(x_{t} \mid x_{&lt;t}\right) &amp;=\operatorname{softmax}\left(\mathbf{W}_{h} \mathbf{h}_{t}+\mathbf{b}\right) \\
\mathbf{h}_{t} &amp;=\mathbf{R} \mathbf{N} \mathbf{N}\left(\mathbf{h}_{t-1}, \mathbf{x}_{t-1}\right)
\end{aligned}" /> 

* A knowledge graph (KG) is a directed, labeled graph consisting of entities E as nodes, with edges defined over a set of relations R.
<img src="https://i.upmath.me/svg/%5Cmathcal%7BK%7D%20%5Cmathcal%7BG%7D%3D%20%5Cleft%5C%7B(p%2C%20r%2C%20e)%20%5Cmid%20p%20%5Cin%20%5Cmathcal%7BE%7D_%7B%3Ct%7D%2C%20r%20%5Cin%20%5Cmathcal%7BR%7D%2C%20e%20%5Cin%20%5Cmathcal%7BE%7D%5Cright%5C%7D" alt="\mathcal{K} \mathcal{G}= \left\{(p, r, e) \mid p \in \mathcal{E}_{&lt;t}, r \in \mathcal{R}, e \in \mathcal{E}\right\}" />

* Local graph till token t is also defined as 
<img src="https://i.upmath.me/svg/%5Cmathcal%7BK%7D%20%5Cmathcal%7BG%7D_%7B%3Ct%7D%3D%20%5Cleft%5C%7B(p%2C%20r%2C%20e)%20%5Cmid%20p%20%5Cin%20%5Cmathcal%7BE%7D_%7B%3Ct%7D%2C%20r%20%5Cin%20%5Cmathcal%7BR%7D%2C%20e%20%5Cin%20%5Cmathcal%7BE%7D%5Cright%5C%7D" alt="\mathcal{K} \mathcal{G}_{&lt;t}= \left\{(p, r, e) \mid p \in \mathcal{E}_{&lt;t}, r \in \mathcal{R}, e \in \mathcal{E}\right\}" />

* Formally, KGLM computes p(x_t, E_t | x<t, E<t). Following diagram illustrates it really well.
    <p align="center">
    <img width=600 src="images/KGLM_illustration.png">
    <em>Source: Author</em>
    </p>

    * Decide the type of x_t, denoted by t_t, it can be "new", "related", or "phi" (not an entity mention)
    * If t_t is "new": choose the upcoming entity e_t from all KG entities
    * If t_t is "related": choose the parent entity p_t, relation r_t , and an entity e_t based on p_t and r_t.
    * If t_t is "phi", then e_t = "phi"
    * If e_t does not belong to E<t, then add e_t into E<t, and make it E<t+1

* Parameters are chosen as below to achieve the same
    * Hidden state is chosen as 
    
        <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bt%7D%3D%5Cleft%5B%5Cmathbf%7Bh%7D_%7Bt%2C%20x%7D%20%3B%20%5Cmathbf%7Bh%7D_%7Bt%2C%20p%7D%20%3B%20%5Cmathbf%7Bh%7D_%7Bt%2C%20r%7D%5Cright%5D" alt="\mathbf{h}_{t}=\left[\mathbf{h}_{t, x} ; \mathbf{h}_{t, p} ; \mathbf{h}_{t, r}\right]" />
    * t_t = softmax(h_t,x, {new, related, phi})
    * New entity is chosen as: 

        <img src="https://i.upmath.me/svg/p%5Cleft(e_%7Bt%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7Bv%7D_%7Be%7D%20%5Ccdot%5Cleft(%5Cmathbf%7Bh%7D_%7Bt%2C%20p%7D%2B%5Cmathbf%7Bh%7D_%7Bt%2C%20r%7D%5Cright)%5Cright)" alt="p\left(e_{t}\right)=\operatorname{softmax}\left(\mathbf{v}_{e} \cdot\left(\mathbf{h}_{t, p}+\mathbf{h}_{t, r}\right)\right)" />

    * Parent entity, and relation is chosen as:

        <img src="https://i.upmath.me/svg/p%5Cleft(p_%7Bt%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7Bv%7D_%7Bp%7D%20%5Ccdot%20%5Cmathbf%7Bh%7D_%7Bt%2C%20p%7D%5Cright)" alt="p\left(p_{t}\right)=\operatorname{softmax}\left(\mathbf{v}_{p} \cdot \mathbf{h}_{t, p}\right)" />

        * and, 
        
        <img src="https://i.upmath.me/svg/p%5Cleft(r_%7Bt%7D%5Cright)%3D%5Coperatorname%7Bsoftmax%7D%5Cleft(%5Cmathbf%7Bv%7D_%7Br%7D%20%5Ccdot%20%5Cmathbf%7Bh%7D_%7Bt%2C%20r%7D%5Cright)" alt="p\left(r_{t}\right)=\operatorname{softmax}\left(\mathbf{v}_{r} \cdot \mathbf{h}_{t, r}\right)" />

    * Whenever, and entity is selected, it influence the distribution over vocabolary to generate new token, i.e. 
    
        <img src="https://i.upmath.me/svg/%5Cmathbf%7Bh%7D_%7Bt%2C%20x%7D%5E%7B%5Cprime%7D%3D%5Cmathbf%7BW%7D_%7B%5Cmathrm%7Bproj%7D%7D%5Cleft%5B%5Cmathbf%7Bh%7D_%7Bt%2C%20x%7D%20%3B%20%5Cmathbf%7Bv%7D_%7Be_%7Bt%7D%7D%5Cright%5D" alt="\mathbf{h}_{t, x}^{\prime}=\mathbf{W}_{\mathrm{proj}}\left[\mathbf{h}_{t, x} ; \mathbf{v}_{e_{t}}\right]" />

    * Training KG Embeddings, i.e. v_et, These are pretrained using TransE. 

        * <img src="https://i.upmath.me/svg/%5Cdelta%5Cleft(%5Cmathbf%7Bv%7D_%7Bp%7D%2C%20%5Cmathbf%7Bv%7D_%7Br%7D%2C%20%5Cmathbf%7Bv%7D_%7Be%7D%5Cright)%3D%5Cleft%5C%7C%5Cmathbf%7Bv%7D_%7Bp%7D%2B%5Cmathbf%7Bv%7D_%7Br%7D-%5Cmathbf%7Bv%7D_%7Be%7D%5Cright%5C%7C%5E%7B2%7D" alt="\delta\left(\mathbf{v}_{p}, \mathbf{v}_{r}, \mathbf{v}_{e}\right)=\left\|\mathbf{v}_{p}+\mathbf{v}_{r}-\mathbf{v}_{e}\right\|^{2}" />

    * And, objective function of negative loglikelihood is minimized, 

        <img src="https://i.upmath.me/svg/%5Cell(%5CTheta)%3D%5Csum_%7Bt%7D%20%5Clog%20p%5Cleft(x_%7Bt%7D%2C%20%5Cmathcal%7BE%7D_%7Bt%7D%20%5Cmid%20x_%7B%3Ct%7D%2C%20%5Cmathcal%7BE%7D_%7B%3Ct%7D%20%3B%20%5CTheta%5Cright)" alt="\ell(\Theta)=\sum_{t} \log p\left(x_{t}, \mathcal{E}_{t} \mid x_{&lt;t}, \mathcal{E}_{&lt;t} ; \Theta\right)" />

* Annotations in the dataset can be understood as follow:
 <p align="center">
    <img width=600 src="images/KGLM_annotations.png">
    <em>Source: Author</em>
    </p>

* Results: This clearly shown much improvement to generate factual information in comparison to GPT2 etc. Test dataset aiming to generate factual information like national capital, birthloc, birthdate, spouse, city-state, book-author was compared using baseline, GPT2, and KGLM, and following results were achieved.

 <p align="center">
    <img width=600 src="images/KGLM_results.png">
    <em>Source: Author</em>
    </p>

**Reflection** Indeed, one of the good paper aiming to integrate KG with LM really well. How it fairs to transformer, it would be really good to observe. Learning both language model, and KG from same text, integrating them while generating or question answering etc would be interesting to know.






