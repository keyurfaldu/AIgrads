## DeepXML: A Deep Extreme Multi-Label Learning Framework Applied to Short Text Documents. 
### Dahiya, Kunal, Deepak Saini, Anshul Mittal, Ankush Shaw, Kushal Dave, Akshay Soni, Himanshu Jain, Sumeet Agarwal, and Manik Varma. 
 In Proceedings of the 14th ACM International Conference on Web Search and Data Mining, pp. 31-39. 2021.[[arXiv](http://manikvarma.org/pubs/dahiya21-main.pdf)]

**Whats Unique**

This paper presents an architecture or modular system to solve extreme classification problem, which is a multi-label classification problem having millions of labels. 

**How It Works**

We need to learn Z and W, where Z is for the feature learning and W is to learn the final task. The complexity of learning the following task is O(NLD), 

<img src="https://i.upmath.me/svg/%0A%5Cmathcal%7BL%7D(%5Cmathcal%7BZ%7D%2C%20%5Cmathbf%7BW%7D)%3D%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%5Csum_%7Bl%3D1%7D%5E%7BL%7D%20%5Cell%5Cleft(%5Cmathbf%7Bx%7D_%7Bi%7D%2C%20y_%7Bi%20l%7D%20%3B%20%5Cmathcal%7BZ%7D%2C%20%5Cmathbf%7BW%7D%5Cright)%0A" alt="
\mathcal{L}(\mathcal{Z}, \mathbf{W})=\sum_{i=1}^{N} \sum_{l=1}^{L} \ell\left(\mathbf{x}_{i}, y_{i l} ; \mathcal{Z}, \mathbf{W}\right)
" />

so DeepXML idea lies in reducing labels to log(labels), for which the complexity would become O(NDlogL)

<img src="https://i.upmath.me/svg/%0A%5Chat%7B%5Cmathcal%7BL%7D%7D(%5Cmathcal%7BZ%7D%2C%20%5Cmathbf%7BW%7D)%3D%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%5Csum_%7Bl%20%5Cin%20%5Chat%7B%5Cmathcal%7BN%7D%7D_%7Bi%7D%20%5Ccup%20%5Cmathcal%7BP%7D_%7Bi%7D%7D%20%5Cell%5Cleft(%5Cmathbf%7Bx%7D_%7Bi%7D%2C%20y_%7Bi%20l%7D%20%3B%20%5Cmathcal%7BZ%7D%2C%20%5Cmathbf%7BW%7D%5Cright)%0A" alt="
\hat{\mathcal{L}}(\mathcal{Z}, \mathbf{W})=\sum_{i=1}^{N} \sum_{l \in \hat{\mathcal{N}}_{i} \cup \mathcal{P}_{i}} \ell\left(\mathbf{x}_{i}, y_{i l} ; \mathcal{Z}, \mathbf{W}\right)
" />

Where, the negative labels are derived as follow:

<img src="https://i.upmath.me/svg/%5Csum_%7Bl%3A%20y_%7Bi%20l%7D%3D-1%7D%20%5Cell%5Cleft(%5Cmathbf%7Bx%7D_%7Bi%7D%2C%20y_%7Bi%20l%7D%20%3B%20%5Cmathcal%7BZ%7D%2C%20%5Cmathbf%7BW%7D%5Cright)%20%5Capprox%20%5Csum_%7Bl%20%5Cin%20%5Chat%7BN%7D_%7Bi%7D%7D%20%5Cell%5Cleft(%5Cmathbf%7Bx%7D_%7Bi%7D%2C%20y_%7Bi%20l%7D%20%3B%20%5Cmathcal%7BZ%7D%2C%20%5Cmathbf%7BW%7D%5Cright)" alt="\sum_{l: y_{i l}=-1} \ell\left(\mathbf{x}_{i}, y_{i l} ; \mathcal{Z}, \mathbf{W}\right) \approx \sum_{l \in \hat{N}_{i}} \ell\left(\mathbf{x}_{i}, y_{i l} ; \mathcal{Z}, \mathbf{W}\right)" />



It breaks down problem into the four parts:
* **Surrogate problem** for feature learning: Surrogate problem is derived, i.e. predicting the meta-label (which is derived from the clustering of the current label). Lets call this as Z0.
* **Hard Negative Selection**: Using the features learned in step 1, hard negative labels are selected, i.e. in optimal margin classifer hard negatives would be one breaching the margin, or where there is non-zero loss.
* **Transfer Learning** of features from surrogate task, if needed apply re-parameterisation from Z0 to Z. Lets call this as Z.
* **Classifier Learning** Final network W, and including Z are both tuned together over the hard negative labels. 

It achives micro-second performance on the query time because of the decreased complexity. Which makes it suitable for many applications as Ad-selection, Maching queries to bid phrases, Personalised ads etc

Metrics to measure performance is Precision@K, and NDCG@K. 