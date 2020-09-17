# grad-AI
This is a niche collection of research papers which are proven to be gradients pushing the field of Natural Language Processing, Deep Learning and Artificial Intelligence

## NLP Pretraining

* [ERNIE 2.0: A Continual Pre-Training Framework for Language Understanding](summary/ERNIE2.md) Sun et al. AAAI 2020 [[arXiv](https://arxiv.org/pdf/1907.12412.pdf)]

* [STRUCTBERT: INCORPORATING LANGUAGE STRUCTURES INTO PRETRAINING FOR DEEP LANGUAGE UNDERSTANDING](summary/structbert.md) Wang et al, ICLR 2020 [[arXiv](https://openreview.net/pdf?id=BJgQ4lSFPH)]

* [PEGASUS: Pre-training with Extracted Gap-sentences for Abstractive Summarization](summary/pegasus.md), Jingqing Zhang, Yao Zhao, Mohammad Saleh, Peter J Liu. Google Research, ICML 2020 [[arXiv](https://arxiv.org/pdf/1912.08777.pdf)]

* [GPT3: Language Models are Few Shot Learners](summary/GPT3.md), Brown et al, Open AI, 2020 [[arXiv](https://arxiv.org/pdf/2005.14165.pdf)]

* [ELECTRA: Pre-Training Text Encoders As Discriminators Rather Than Genererators](summary/electra.md), Clark et al., Stanford and Google, 2020 [[arXiv](https://arxiv.org/pdf/2003.10555.pdf)]

* [XLNet: Generalized Autoregressive Pretraining for Language Understanding](summary/xlnet.md), Yang et al. NIPS 2019, Google AI Brain, 2019 [[arXiv](https://arxiv.org/pdf/1906.08237.pdf)]

* [ALBERT: A Lite BERT for Self-Supervised Learning of Language Representations](summary/albert.md), Zhenzhong Lan1, Mingda Chen, 2020 [[arXiv](https://arxiv.org/pdf/1909.11942.pdf)]

* [T5: Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer](summary/T5.md), Raffel et al, Google, 2019 [[arXiv](https://arxiv.org/pdf/1910.10683.pdf)]


* [RoBERTa: A Robustly Optimized BERT Pretraining Approach](summary/roberta.md), Liu et al. Facebook AI, 2019 [[arXiv](https://arxiv.org/pdf/1907.11692.pdf)]

* [SpanBERT: Improving Pre-training by Representing and Predicting Spans](summary/spanBERT.md), Joshi, Chen, AllenAI, Facebook Research, 2020 [[arXiv](https://www.mitpressjournals.org/doi/pdf/10.1162/tacl_a_00300)]

* [UniLM: Unified Language Model Pre-training for Natural Language Understanding and Generation](summary/unilm.md), Dong et al., Microsoft Research, 2019 [[NIPS](http://papers.nips.cc/paper/9464-unified-language-model-pre-training-for-natural-language-understanding-and-generation.pdf)]

* [DistilBERT, a distilled version of BERT: smaller,faster, cheaper and lighter](summary/distilbert.md), Victor SANH, Lysandre DEBUT, Julien CHAUMOND, Thomas WOLF, 2020 [[arXiv](https://arxiv.org/abs/1910.01108)]

* [BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension](summary/bart.md), Lewis et al. [[arXiv](https://arxiv.org/pdf/1910.13461.pdf)]

* [MASS: Masked Sequence to Sequence Pre-training for Language Generation](summary/mass.md), Song et al. [[arXiv](https://arxiv.org/pdf/1905.02450.pdf)]

* [GPT-2: Language Models are Unsupervised Multitask Learners](summary/gpt2.md) Radford et al. 2018, OpenAI [[OpenAI](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)]

* [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](summary/bert.md) Devlin et al. 2018, Google AI Language [[arXiv](https://arxiv.org/pdf/1810.04805.pdf)]

* [GPT: Improving Language Understanding by Generative Pre-Training](summary/gpt.md) Alec Radford, Karthik Narasimhan, Tim Saliman, Ilya Sutskever @ OpenAI, 2018 [[OpenAI](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)]

* [Attention Is All You Need](summary/transformers.md), Vaswani et al, 2017 [[arXiv](https://arxiv.org/pdf/1706.03762.pdf)]

## Fine Tuning & Down-stream Tasks

* [Syntax-guided Controlled Generation of Paraphrases](summary/SGCP.md), Ashutosh Kumar, Kabir Ahuja, Raghuram Vadapalli, Partha Talukdar, ACL 2020 [[arXiv](https://arxiv.org/pdf/2005.08417.pdf)]

* [Giving BERT a Calculator: Finding Operations and Arguments with Reading Comprehension](summary/bert_calculator.md) Daniel Andor, Luheng He, Kenton Lee, Emily Pitler, ACL 2019 [[arXiv](https://arxiv.org/abs/1909.00109)]

* [CTRL: A CONDITIONAL TRANSFORMER LANGUAGE MODEL FOR CONTROLLABLE GENERATION](summary/ctrl.md) Nitish Shirish Keskar, Richard Socher, 2020 [[arXiv](https://einstein.ai/presentations/ctrl.pdf)]

* [Don’t Stop Pretraining: Adapt Language Models to Domains and Tasks](summary/domain_task_adaptive_training.md), Gururangan et al, ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.740.pdf)]

* [Unifying Question Answering, Text Classification, and Regression via Span Extraction](SpEx-BERT.md) Nitish Keskar, Richard Socher et al [[arXiv](https://arxiv.org/pdf/1904.09286.pdf)]

* [How to Fine-Tune BERT for Text Classification?](summary/finetune_bert_text_classification.md) Sun et al, 2019[[arXiv](https://arxiv.org/abs/1905.05583)]


* [To Tune or Not to Tune? Adapting Pretrained Representations to Diverse Tasks](summary/adapting_pretrained_repr.md) Peters, Ruder, Smith, AI2, ACL 2019 [[arXiv](https://arxiv.org/abs/1903.05987)]

* [To Tune or Not To Tune? How About the Best of Both Worlds?](summary/stack_and_finetune.md), Wang et al, 2019, [[arXiv](https://arxiv.org/abs/1907.05338)]


* [Leveraging Pre-trained Checkpoints for Sequence Generation Tasks](summary/seq_generation_from_pretrained.md) Sascha Rothe, Shashi Narayan, Aliaksei Severyn, ACL 2020 [[arXiv](https://arxiv.org/pdf/1907.12461.pdf)]

* [Fine-Tuning Pretrained Language Models: Weight Initializations, Data Orders, and Early Stopping](summary/finetuning_wi_do.md), Dodge et al. 2020  [[arXiv](https://arxiv.org/pdf/2002.06305.pdf)]

## Multi task learning

* [MT-DNNKD: Improving Multi-Task Deep Neural Networks via Knowledge Distillation for Natural Language Understanding](summary/MTDNNKD.md), Xiaodong Liu et al. [[arXiv](https://arxiv.org/pdf/1904.09482.pdf)]

* [Multi-Task Deep Neural Networks for Natural Language Understanding](summary/MTDNN_GLUE.md), Xiaodong Liu, Pengcheng He, Weizhu Chen, Jianfeng Gao, 2019 [[arXiv](https://arxiv.org/abs/1901.11504)]

* [BAM! Born-Again Multi-Task Networks for Natural Language Understanding](summary/bam_multi_task.md), Kevin Clark, Christopher D. Manning et al. [[arXiv](https://arxiv.org/pdf/1907.04829.pdf)]

## Datasets, Benchmarks & Metrics

* [Word Sense Disambiguation: A Unified Evaluation Framework and Empirical Comparison](summary/WSD.md),Alessandro Raganato, Jose Camacho-Collados and Roberto Navigli, ACL 2017 [[arXiv](https://www.aclweb.org/anthology/E17-1010.pdf)]

* [SuperGLUE: A Stickier Benchmark for General-Purpose Language Understanding Systems](summary/superGLUE.md), Wang et al, NIPS 2019 [[arXiv](https://arxiv.org/pdf/1905.00537.pdf)]

* [CHECKLIST: Beyond Accuracy: Behavioral Testing of NLP Models with CHECKLIST](summary/checklist.md), Ribeiro, Wu, Guestrin, Sameer Singh, 2020 [[ACLWeb](https://www.aclweb.org/anthology/2020.acl-main.442.pdf)]



## Probing and Interpretability

* [Towards Transparent and Explainable Attention Models](summary/diversity_attention.md) Mohankumar, Mitesh Khapra et al. ACL 2020 [[arXiv](https://arxiv.org/abs/2004.14243)]

* [Revealing the Dark Secrets of BERT](summary/dark_secret_BERT.md) Olga Kovaleva, ACL 2019 [[arXiv](https://arxiv.org/abs/1908.08593)]

* [DeepLift: Learning Important Features Through Propagating Activation Differences](summary/deeplift.md) Avanti Shrikumar et al, Stanford University, ICML 2019 [[arXiv](https://arxiv.org/pdf/1704.02685.pdf)]

* [Analysis Methods in Neural Language Processing: A Survey](summary/survey_nlp_analysis.md), Belinkov, Glass 2019 [[arXiv](https://www.mitpressjournals.org/doi/pdfplus/10.1162/tacl_a_00254)]

* [LIME: "Why Should I Trust You?": Explaining the Predictions of Any Classifier](summary/LIME.md) Ribeiro, Sameer Singh, Guestrin, University of Washington, KDD 2016 [[arXiv](https://arxiv.org/pdf/1602.04938.pdf)]

* [Axiomatic Attribution for Deep Networks](summary/integrated_gradients.md), Sundararajan, Taly, Yan, Google, ICML 2017 [[arXiv](https://arxiv.org/pdf/1703.01365.pdf)]

* [How Important Is a Neuron?](summary/conductance.md), Kedar Dhamdhere, Mukund Sundararajan, Qiqi Yan, Google Research [[arXiv](https://arxiv.org/pdf/1805.12233.pdf)]

* [SHAP: A Unified Approach to Interpreting Model Predictions](summary/shap.md), Lundberg, Lee, University of Washington, NIPS 2017 [[arXiv](http://papers.nips.cc/paper/7062-a-unified-approach-to-interpreting-model-predictions.pdf)]

* [Attention is not not explanation](summary/attention_not_not.md) Sarah Wiegreffe, Yuval Pinter,  EMNLP 2019 [[arXiv](https://arxiv.org/abs/1908.04626)]

* [Attention is not Explanation](summary/attention_not_explanation.md), Sarthak Jain, Byron C Wallace, NAACL-2019, [[arXiv](https://arxiv.org/pdf/1902.10186.pdf)]

* [What do you Learn from Context? Probing for Sentence Structure in Contextualized Word Representations](summary/edge_probing.md), ICLR 2019, Tenney at el [[openreview](https://openreview.net/pdf?id=SJzSgnRcKX)]

* [Are Sixteen Heads Really Better than One?](summary/sixteen_heads.md), Paul Michel, Omer Levy, Graham Neubig, 2019 [[arXiv](https://arxiv.org/pdf/1905.10650.pdf)]

* [Fine-Grained Analysis of Sentence Embedding Using Auxiliary Prediction Tasks](summary/aux_pred.md), Yossi Adi, Yoav Goldberg et al, ICLR 2017 [[arXiv](https://arxiv.org/pdf/1608.04207.pdf)]

* [Assessing BERT’s Syntactic Abilities](summary/bert_syntactic.md), Yoav Goldberg, 2019 [[arXiv](https://arxiv.org/pdf/1901.05287.pdf)]

* [Generating Derivational Morphology with BERT](summary/bert_derivational_morphology.md) Valentin Hofmann, Janet B. Pierrehumbert, Hinrich Schutze, 2020 [[arXiv](https://arxiv.org/pdf/2005.00672.pdf)]

* [Investigating BERT’s Knowledge of Language: Five Analysis Methods with NPIs](summary/bert_npi.md) Warstadt et al. [[arXiv](https://arxiv.org/pdf/1909.02597.pdf)]

* [What Does BERT Look At? An Analysis of BERT’s Attention](summary/bert_analysis.md), Kevin Clark, Urvashi Khandelwal, Omer Levy, Christopher D. Manning, 2019 [[arXiv](https://arxiv.org/abs/1906.04341)]

* [BERT Rediscovers the Classical NLP Pipeline](summary/bert_analysis_nlp_pipeline.md), Ian Tenney, Dipanjan Das, Ellie Pavlick, 2019 [[arXiv](https://arxiv.org/pdf/1905.05950.pdf)]

* [Visualizing and Measuring the Geometry of BERT](summary/bert_geometry.md), Andy Coenen, Martin Wattenberg et al, NIPS 2019 [[arXiv](https://arxiv.org/pdf/1906.02715.pdf)]

* [Designing and Interpreting Probes with Control Tasks](summary/designing_probes.md), John Hewitt, Percy Liang, EMNLP-2019 [[arXiv](https://www.aclweb.org/anthology/D19-1275.pdf)]

* [Open Sesame: Getting Inside BERT’s Linguistic Knowledge](summary/sesame.md), Yongjie Lin, Yi Chern Tan, Robert Frank, 2019 [[arXiv](https://arxiv.org/pdf/1906.01698.pdf)]

* [A Structural Probe for Finding Syntax in Word Representations](summary/structural_probe.md), John Hewitt, Christopher D. Manning, 2019, NAACL 2019, Standford [[arXiv](https://nlp.stanford.edu/pubs/hewitt2019structural.pdf)]

* [On Identifiability in Transformers](summary/identifiability.md), Brunner, Liu, Pascual, Richter, Ciaramita, Wattenhofer, Google Research, ICLR 2020 [[arXiv](https://openreview.net/pdf?id=BJg1f6EFDB)]

* [NILE : Natural Language Inference with Faithful Natural Language Explanations](summary/nile.md), Sawan Kumar, Partha Talukdar, 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.771.pdf)]

* [Quantifying Attention Flow in Transformers](summary/attention_flow.md), Samira Abnar, Willem Zuidema, ACL 2020 [[arXiv](https://arxiv.org/pdf/2005.00928.pdf)] 

* [Human Attention Maps for Text Classification: Do Humans and Neural Networks Focus on the Same Words?](summary/human_attention_comparision.md) Sen et al, ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.419.pdf)]
]

* [Understanding Attention for Text Classification](summary/understanding_attention.md), Xiaobing Sun and Wei Lu, Singapore University, ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.312.pdf)]

## Conversational AI

* [Zero-Shot Transfer Learning with Synthesized Data for Multi-Domain Dialogue State Tracking](summary/cai_synthetic_data.md), Giovanni Campagna Agata Foryciarz Mehrad Moradshahi Monica S. Lam, ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.12.pdf)]

## Knowledge Graphs + NLP

* [Improving question answering with external knowledge](summary/qa_external_knowledge.md) Xiaoman Pan et al. MRQA 2019 [[arXiv](https://arxiv.org/pdf/1902.00993.pdf)]

* [Improving Natural Language Inference Using External Knowledge in the Science Questions Domain](summary/ConSeqNet.md) Wang et al, AAAI 2019 [[arXiv](https://www.aaai.org/ojs/index.php/AAAI/article/view/4705)]

* [KG-BERT: BERT for Knowledge Graph Completion](summary/KG_BERT.md), Liang Yao, Chengsheng Mao, Yuan Luo, AAAI 2020 [[arXiv](https://arxiv.org/pdf/1909.03193.pdf)]

* [K-BERT: Enabling Language Representation with Knowledge Graph](summary/k-bert.md), Weijie Liu, Peng Zhou, Zhe Zhao, Zhiruo Wang, Qi Ju, Haotang Deng, Ping Wang, AAAI 2020 [[arXiv](https://arxiv.org/pdf/1909.07606.pdf)]

* [Structural Information Preserving for Graph-to-Text Generation](summary/graph_to_text_RATrans.md), Linfeng Song et al., ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.712.pdf)]

* [Low-Dimensional Hyperbolic Knowledge Graph Embeddings](summary/Hyperbolic_KG_embedding.md) Chami et al, ACL 2020 [[arXiv](aclweb.org/anthology/2020.acl-main.617.pdf)]

* [Convolutional 2D Knowledge Graph Embeddings](summary/ConvE.md), Dettmers et al, AAAI 2018 [[arXiv](https://arxiv.org/abs/1707.01476)]

* [InteractE: Improving Convolution-based Knowledge Graph Embeddings by Increasing Feature Interactions](summary/InteractE.md), Shikhar Vashishth, Soumya Sanyal, Vikram Nitin, Nilesh Agrawal, Partha Talukdar, AAAI 2020 [[arXiv](https://arxiv.org/pdf/1911.00219.pdf)]

* [Translating Embeddings for Modeling Multi-relational Data](summary/TransE.md), Antoine Bordes, Nicolas Usunier, Alberto Garcia-Duran, NIPS 2013 [[arXiv](https://papers.nips.cc/paper/5071-translating-embeddings-for-modeling-multi-relational-data.pdf)]

* [K-Adapters: Infusing Knowledge into Pre-Trained Models with Adapters](summary/k-adapter.md), Ruize Wang, Ming Zhou et al. ACL 2020 [[arXiv](https://arxiv.org/pdf/2002.01808.pdf)]

* [ERWISE: Zero-shot Word Sense Disambiguation using Sense Definition Embeddings](summary/ERWISE.md) Sawan Kumar, Partha Talukdar, ACL 2019 [[arXiv](https://malllabiisc.github.io/publications/papers/EWISE_ACL19.pdf)]

* [KnowBERT: Knowledge Enhanced Contextual Word Representations](summary/knowbert.md) Peters et al, ACL 2019 [[arXiv](https://arxiv.org/abs/1909.04164)]

* [Sequential Latent Knowledge Selection For Knowledge-Grounded Dialogue](summary/KGD_SKT.md), Byeongchang Kim, Jaewoo Ahn, Gunhee Kim, ICLR 2020 [[arXiv](https://arxiv.org/abs/2002.07510)]

* [Knowledge-Augmented Language Model and Its Application to Unsupervised Named-Entity Recognition](summary/KALM.md), Angli Liu, Jingfei Du, Veselin Stoyanov [[arXiv](https://www.aclweb.org/anthology/N19-1117/)]
]

* [Barack’s Wife Hillary: Using Knowledge Graphs for Fact-Aware Language Modeling](summary/KGLM.md), Logan IV, ACL 2019, [[arXiv](https://www.aclweb.org/anthology/P19-1598/)]

* [Knowledge Infused Learning (K-IL): Towards Deep Incorporation of Knowledge in Deep Learning](summary/KIL.md), Kursuncu et al. AAAI 2020 [[arXiv](https://arxiv.org/pdf/1912.00512.pdf)]

* [COMET: Commonsense Transformers for Automatic Knowledge Graph Construction](summary/comet.md), Bosselut et al. ACL 2019 [[arXiv](https://www.aclweb.org/anthology/P19-1470/)]

* [ERNIE: Enhanced Language Representation with Informative Entities](summary/ernie.md), Zhang et al, ACL 2019 [[arXiv](https://arxiv.org/pdf/1905.07129.pdf)]

* [EmbedKGQA: Improving Multi-hop Question Answering over Knowledge Graphs using Knowledge Base Embeddings](summary/embed_kgqa.md), Apoorv Saxena, Aditay Tripathi, Partha Talukdar, 2020 [[ACLWeb](https://www.aclweb.org/anthology/2020.acl-main.412.pdf)]

## Software packages on NLP
* [jiant: A Software Toolkit for Research on General-Purpose Text Understanding Models](summary/jiant.md), Pruksachatkun et al, 2020 [[arXiv](https://arxiv.org/pdf/2003.02249.pdf)]

* [Huggingface's Transformers: State-of-the-art Natural Language Processing](summary/huggingface.md), Wolf et al, 2020 [[arXiv](https://arxiv.org/pdf/1910.03771.pdf)]

* [AllenNLP Interpret: A Framework for Explaining Predictions of NLP Models](summary/allen_nlp.md), Wallace et al, 2019 EMNLP [[arXiv](https://www.aclweb.org/anthology/D19-3002.pdf)]

## AI Ethics & Futuer

* [Climbing towards NLU: On Meaning, Form, and Understanding in the Age of Data](summary/meaning.md) Bender, Koller, ACL 2020 [[arXiv](https://www.aclweb.org/anthology/2020.acl-main.463.pdf)]


* [THIEVES ON SESAME STREET! MODEL EXTRACTION OF BERT-BASED APIS](summary/bert_extraction.md), Krishna, Mohit Iyyer et al. ICLR 2020 [[arXiv](https://arxiv.org/pdf/1910.12366.pdf)]

## Deep Learning Building Blocks
* [A disciplined approach to neural network hyper-parameters: Part 1 -- learning rate, batch size, momentum, and weight decay](summary/one_cycle_learning.md), Leslie N Smith, 2018 [[arXiv](https://arxiv.org/abs/1803.09820)]

* [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](summary/batch_normalization), Sergey Ioffe, Christian Szegedy, 2015 [[arXiv](https://arxiv.org/pdf/1502.03167.pdf)]

* [Kaiming Initialization: Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification](summary/kaiming_initialization.md), Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun [[arXiv]](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/He_Delving_Deep_into_ICCV_2015_paper.pdf)

* [LAMB: Large Batch Optimization for Deep Learning: Training BERT in 76 minutes](summary/lamb.md), Yang You, Jing Li [[arXiv]](https://arxiv.org/abs/1904.00962)

* [Sentencepience: Subword Regularization: Improving Neural Network Translation Models with Multiple Subword Candidates](summary/sentencepiece.md) Taku Kudo, Google, 2018 [[arXiv](https://arxiv.org/abs/1804.10959)]