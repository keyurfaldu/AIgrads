## Low-Dimensional Hyperbolic Knowledge Graph Embeddings
### Ines Chami, Adva Wolf, Da-Cheng Juan, Frederic Sala, Sujith Ravi and Christopher Re´
### ACL 2020 [[arXiv](aclweb.org/anthology/2020.acl-main.617.pdf)]

**Whats New**
* This paper present a method that combine hyperbolic reflections and rotations with attention mechanism to model complex KG relational patterns. 

**Main contribution**
* Train hyperbolic embeddings with relation specific curvatures to preseve multiple hierarchies in KGs
* parameterise hyperbolic isometries and leverage their geometric properties to capture relation's logical pattern such as symmetry or anti symmetry
* hyperbolic attention to combine geometric operators and capture multiple logical patterns.

**How it works**
* An illustration of a hyperbolic space and correponding tangential ecludian space is in below figure,
    <p align="center">
        <img width=600 src="images/hyperbolic_space.png">
        <em>Source: Author</em>
        </p>

* As can be seen in the figure, 
    * Tangent space maps to hyperbolic space with exponential map
    * Hyperbolic space maps to tangent space using logorithmic maps
    * x is presnet in both spaces, v is vector in ecludian/tangent space. Lets map it to hyperbolic space using exponential map, and vice versa.

        <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Cexp%20_%7B%5Cmathbf%7B0%7D%7D%5E%7Bc%7D(%5Cmathbf%7Bv%7D)%20%26%3D%5Ctanh%20(%5Csqrt%7Bc%7D%5C%7C%5Cmathbf%7Bv%7D%5C%7C)%20%5Cfrac%7B%5Cmathbf%7Bv%7D%7D%7B%5Csqrt%7Bc%7D%5C%7C%5Cmathbf%7Bv%7D%5C%7C%7D%20%5C%5C%0A%5Clog%20_%7B%5Cmathbf%7B0%7D%7D%5E%7Bc%7D(%5Cmathbf%7By%7D)%20%26%3D%5Coperatorname%7Barctanh%7D(%5Csqrt%7Bc%7D%5C%7C%5Cmathbf%7By%7D%5C%7C)%20%5Cfrac%7B%5Cmathbf%7By%7D%7D%7B%5Csqrt%7Bc%7D%5C%7C%5Cmathbf%7By%7D%5C%7C%7D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
\exp _{\mathbf{0}}^{c}(\mathbf{v}) &amp;=\tanh (\sqrt{c}\|\mathbf{v}\|) \frac{\mathbf{v}}{\sqrt{c}\|\mathbf{v}\|} \\
\log _{\mathbf{0}}^{c}(\mathbf{y}) &amp;=\operatorname{arctanh}(\sqrt{c}\|\mathbf{y}\|) \frac{\mathbf{y}}{\sqrt{c}\|\mathbf{y}\|}
\end{aligned}" /> 

    * Hyperbolic distance has following formula

        <img src="https://i.upmath.me/svg/d%5E%7Bc%7D(%5Cmathbf%7Bx%7D%2C%20%5Cmathbf%7By%7D)%3D%5Cfrac%7B2%7D%7B%5Csqrt%7Bc%7D%7D%20%5Coperatorname%7Barctanh%7D%5Cleft(%5Csqrt%7Bc%7D%7C%7C-%5Cmathbf%7Bx%7D%20%5Coplus%5E%7Bc%7D%20%5Cmathbf%7By%7D%20%5C%7C%5Cright)" alt="d^{c}(\mathbf{x}, \mathbf{y})=\frac{2}{\sqrt{c}} \operatorname{arctanh}\left(\sqrt{c}||-\mathbf{x} \oplus^{c} \mathbf{y} \|\right)" />

    * It is similar to transforming it in ecludian space and measuring distance.


* Rotations and Reflections can be modeled as following:

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%0A%5Coperatorname%7BRot%7D%5Cleft(%5CTheta_%7Br%7D%5Cright)%3D%5Coperatorname%7Bdiag%7D%5Cleft(G%5E%7B%2B%7D%5Cleft(%5Ctheta_%7Br%2C%201%7D%5Cright)%2C%20%5Cldots%2C%20G%5E%7B%2B%7D%5Cleft(%5Ctheta_%7Br%2C%20%5Cfrac%7Bd%7D%7B2%7D%7D%5Cright)%5Cright)%20%5C%5C%0A%5Coperatorname%7BRef%7D%5Cleft(%5CPhi_%7Br%7D%5Cright)%3D%5Coperatorname%7Bdiag%7D%5Cleft(G%5E%7B-%7D%5Cleft(%5Cphi_%7Br%2C%201%7D%5Cright)%2C%20%5Cldots%2C%20G%5E%7B-%7D%5Cleft(%5Cphi_%7Br%2C%20%5Cfrac%7Bn%7D%7B2%7D%7D%5Cright)%5Cright)%20%5C%5C%0A%5Ctext%20%7B%20where%20%7D%20G%5E%7B%5Cpm%7D(%5Ctheta)%3A%3D%5Cleft%5B%5Cbegin%7Barray%7D%7Bcc%7D%0A%5Ccos%20(%5Ctheta)%20%26%20%5Cmp%20%5Csin%20(%5Ctheta)%20%5C%5C%0A%5Csin%20(%5Ctheta)%20%26%20%5Cpm%20%5Ccos%20(%5Ctheta)%0A%5Cend%7Barray%7D%5Cright%5D%0A%5Cend%7Baligned%7D" alt="\begin{aligned}
    \operatorname{Rot}\left(\Theta_{r}\right)=\operatorname{diag}\left(G^{+}\left(\theta_{r, 1}\right), \ldots, G^{+}\left(\theta_{r, \frac{d}{2}}\right)\right) \\
    \operatorname{Ref}\left(\Phi_{r}\right)=\operatorname{diag}\left(G^{-}\left(\phi_{r, 1}\right), \ldots, G^{-}\left(\phi_{r, \frac{n}{2}}\right)\right) \\
    \text { where } G^{\pm}(\theta):=\left[\begin{array}{cc}
    \cos (\theta) &amp; \mp \sin (\theta) \\
    \sin (\theta) &amp; \pm \cos (\theta)
    \end{array}\right]
    \end{aligned}" />

    * Note these are diagnoal metrics
    * They are specific to relations r
    * Theta and Phi are learnable parameters.

* Hyperbolic attention:
    * Map x, and y in ecludian space. And compute attention scores. And compute weightage average using tangent space, which is mapped back to hyperbolic space using exponential map.

        <img src="https://i.upmath.me/svg/%5Cmathbf%7Bx%7D%5E%7BE%7D%3D%5Clog%20_%7B%5Cmathbf%7B0%7D%7D%5E%7Bc%7D%5Cleft(%5Cmathbf%7Bx%7D%5E%7BH%7D%5Cright)%20%5Ctext%20%7B%20and%20%7D%20%5Cmathbf%7By%7D%5E%7BE%7D%3D%5Clog%20_%7B%5Cmathbf%7B0%7D%7D%5E%7Bc%7D%5Cleft(%5Cmathbf%7By%7D%5E%7BH%7D%5Cright)" alt="\mathbf{x}^{E}=\log _{\mathbf{0}}^{c}\left(\mathbf{x}^{H}\right) \text { and } \mathbf{y}^{E}=\log _{\mathbf{0}}^{c}\left(\mathbf{y}^{H}\right)" />

        <img src="https://i.upmath.me/svg/%0A%5Cleft(%5Calpha_%7B%5Cmathbf%7Bx%7D%7D%2C%20%5Calpha_%7B%5Cmathbf%7By%7D%7D%5Cright)%3D%5Coperatorname%7BSoftmax%7D%5Cleft(%5Cmathbf%7Ba%7D%5E%7BT%7D%20%5Cmathbf%7Bx%7D%5E%7BE%7D%2C%20%5Cmathbf%7Ba%7D%5E%7BT%7D%20%5Cmathbf%7By%7D%5E%7BE%7D%5Cright)%5C%5C%0A%5Coperatorname%7BAtt%7D%5Cleft(%5Cmathbf%7Bx%7D%5E%7BH%7D%2C%20%5Cmathbf%7By%7D%5E%7BH%7D%20%3B%20%5Cmathbf%7Ba%7D%5Cright)%3A%3D%5Cexp%20_%7B%5Cmathbf%7B0%7D%7D%5E%7Bc%7D%5Cleft(%5Calpha_%7B%5Cmathbf%7Bx%7D%7D%20%5Cmathbf%7Bx%7D%5E%7BE%7D%2B%5Calpha_%7B%5Cmathbf%7By%7D%7D%20%5Cmathbf%7By%7D%5E%7BE%7D%5Cright)%0A" alt="
\left(\alpha_{\mathbf{x}}, \alpha_{\mathbf{y}}\right)=\operatorname{Softmax}\left(\mathbf{a}^{T} \mathbf{x}^{E}, \mathbf{a}^{T} \mathbf{y}^{E}\right)\\
\operatorname{Att}\left(\mathbf{x}^{H}, \mathbf{y}^{H} ; \mathbf{a}\right):=\exp _{\mathbf{0}}^{c}\left(\alpha_{\mathbf{x}} \mathbf{x}^{E}+\alpha_{\mathbf{y}} \mathbf{y}^{E}\right)
" />

* ATTH Model
    * Rotation and reflection of head entity with relation r is taken.
    
    <img src="https://i.upmath.me/svg/%5Cmathbf%7Bq%7D_%7B%5Cmathrm%7BRot%7D%7D%5E%7BH%7D%3D%5Coperatorname%7BRot%7D%5Cleft(%5CTheta_%7Br%7D%5Cright)%20%5Cmathbf%7Be%7D_%7Bh%7D%5E%7BH%7D%2C%20%5Cmathbf%7Bq%7D_%7B%5Cmathrm%7Bref%7D%7D%5E%7BH%7D%3D%5Coperatorname%7BRef%7D%5Cleft(%5CPhi_%7Br%7D%5Cright)%20%5Cmathbf%7Be%7D_%7Bh%7D%5E%7BH%7D" alt="\mathbf{q}_{\mathrm{Rot}}^{H}=\operatorname{Rot}\left(\Theta_{r}\right) \mathbf{e}_{h}^{H}, \mathbf{q}_{\mathrm{ref}}^{H}=\operatorname{Ref}\left(\Phi_{r}\right) \mathbf{e}_{h}^{H}" />

    * Rotations and reflections are combined with attention mechanism

        <img src="https://i.upmath.me/svg/%5Cmathrm%7BQ%7D(h%2C%20r)%3D%5Coperatorname%7BAtt%7D%5Cleft(%5Cmathbf%7Bq%7D_%7B%5Cmathrm%7BRot%7D%7D%5E%7BH%7D%2C%20%5Cmathbf%7Bq%7D_%7B%5Cmathrm%7BRef%7D%7D%5E%7BH%7D%20%3B%20%5Cmathbf%7Ba%7D_%7Br%7D%5Cright)%20%5Coplus%5E%7Bc_%7Br%7D%7D%20%5Cmathbf%7Br%7D_%7Br%7D%5E%7BH%7D" alt="\mathrm{Q}(h, r)=\operatorname{Att}\left(\mathbf{q}_{\mathrm{Rot}}^{H}, \mathbf{q}_{\mathrm{Ref}}^{H} ; \mathbf{a}_{r}\right) \oplus^{c_{r}} \mathbf{r}_{r}^{H}" />

    * Distance between tail entity and transformed head entity is computed.

        <img src="https://i.upmath.me/svg/s(h%2C%20r%2C%20t)%3D-d%5E%7Bc_%7Br%7D%7D%5Cleft(Q(h%2C%20r)%2C%20%5Cmathbf%7Be%7D_%7Bt%7D%5E%7BH%7D%5Cright)%5E%7B2%7D%2Bb_%7Bh%7D%2Bb_%7Bt%7D" alt="s(h, r, t)=-d^{c_{r}}\left(Q(h, r), \mathbf{e}_{t}^{H}\right)^{2}+b_{h}+b_{t}" />

* Loss functipon: minimising full cross entropy loss with uniform negative sampling.

    <img src="https://i.upmath.me/svg/%5Cbegin%7Baligned%7D%20%5Cmathcal%7BL%7D%3D%26%20%5Csum_%7Bt%5E%7B%5Cprime%7D%20%5Csim%20%5Cmathcal%7BU%7D(%5Cmathcal%7BV%7D)%7D%20%5Clog%20%5Cleft(1%2B%5Cexp%20%5Cleft(y_%7Bt%5E%7B%5Cprime%7D%7D%20s%5Cleft(h%2C%20r%2C%20t%5E%7B%5Cprime%7D%5Cright)%5Cright)%5Cright)%20%5C%5C%20%26%20%5Ctext%20%7B%20where%20%7D%20y_%7Bt%5E%7B%5Cprime%7D%7D%3D%5Cleft%5C%7B%5Cbegin%7Barray%7D%7Bll%7D-1%20%26%20%5Ctext%20%7B%20if%20%7D%20t%5E%7B%5Cprime%7D%3Dt%20%5C%5C%201%20%26%20%5Ctext%20%7B%20otherwise%20%7D%5Cend%7Barray%7D%5Cright.%5Cend%7Baligned%7D" alt="\begin{aligned} \mathcal{L}=&amp; \sum_{t^{\prime} \sim \mathcal{U}(\mathcal{V})} \log \left(1+\exp \left(y_{t^{\prime}} s\left(h, r, t^{\prime}\right)\right)\right) \\ &amp; \text { where } y_{t^{\prime}}=\left\{\begin{array}{ll}-1 &amp; \text { if } t^{\prime}=t \\ 1 &amp; \text { otherwise }\end{array}\right.\end{aligned}" />


* Results
    * ATTH has got much better results in the lower dimension.
    * In higher dimension, even ecludian space can potentailly model hierarchies, so it is at par.
    


