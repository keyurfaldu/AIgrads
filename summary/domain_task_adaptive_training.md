## Don’t Stop Pretraining: Adapt Language Models to Domains and Tasks
### Suchin Gururangan, Ana Marasovic, Swabha Swayamdipta, Kyle Lo, Iz Beltagy, Doug Downey, Noah A. Smith
### Allen Institute of AI
### ACL 2020

**Whats Next**
This paper presents evidence of domain adaptie pretraining, and task adaptive pretraining. Multi phase adaptive training does give better preformance.

**Key Insights**
* Following figure illustrate the intuition behind multi phase adaptive training
    <p align="center">
        <img width=600 src="images/dapt_tapt_illustration.png">
        <em>Source: Author</em>
        </p>

* Domain Adaptive Pre-Training (DAPT)
    * Unlabelled data for the domain of task was taken.
    * Disimilarity of domain data with LM pretraining data was computed based on the top 10K vocabolary overlap
    * Following plot demonstrate it,
    <p align="center">
        <img width=600 src="images/domain_data_similarity.png">
        <em>Source: Author</em>
        </p>

    * Following table shows the impact of DAPT, and also rules out if the impact is just because of additional training. So, last column represent a disimilar-domain pre-training.
    <p align="center">
        <img width=600 src="images/DAPT_performance.png">
        <em>Source: Author</em>
        </p>

* Task Adaptive Pre-Training (TAPT)
    * Second phase of pre-training based on the unlabelled training data of the task, which is masked out as per Roberta's need
    * 100 epochs are trained under TAPT phase
    * TAPT and DAPT together brings additional performance boost
    * Following table highlights performance improvement from TAPT, DAPT and both
    <p align="center">
        <img width=600 src="images/DAPT_TAPT.png">
        <em>Source: Author</em>
        </p>

    * Also, following two more methods have been found effective
        * Unlablled data related to task is proven very effective. Sometime dataset creation involves creating a large pool of data, and selectively filter task specific data, in that case the original larger pool of data turns effective for boosting the performance.
        * Find out subset of in-domain data which is similar to task specific data  using embedding similarity also leads to improved performance. For each record in task, when top-K nearest neighbours were chosen, the gain in perfomance was reported as following.

    <p align="center">
        <img width=600 src="images/TAPT_Similar_Data_Retrieval.png">
        <em>Source: Author</em>
        </p>



    


