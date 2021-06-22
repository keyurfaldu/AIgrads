## Simplifying Paragraph-level Question Generation via Transformer Language Models.
### Lopez, Luis Enrico, Diane Kathryn Cruz, Jan Christian Blaise Cruz, and Charibeth Cheng.  
### arXiv preprint arXiv:2005.01107 (2020)[[arXiv](https://arxiv.org/pdf/2005.01107.pdf)].

**Whats Unique**

This paper formulate question generation as a decoder only language model and fine tune GPT-2 to generate questions without using answer awareness. 

**How It Works**
* Fine tunes decoder only language model
* Does not use answer-awareness (possibly because it does not suit language model)
* It has two schemes to generate questions: AQPL (All questions per line) and OQPL (one question per line)
* It uses SQUAD and RACE datasets
* It uses top-p nucleus sampling method to generate diverse questions
* Automated evaluation using BLEU scores and METEOR and ROUGE-L scores.
* Human evaluation on relevance, difficulty and naturalness. Cohen's Kappa for IAA
* It performs bunch of other analysis on top of how questions are generated.

