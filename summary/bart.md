## BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension

### Lewis et al. Facebook AI, 2019

* BART is all about
    * Corrupting text with an arbitary noising function
    * Learning a model to reconstruct the original text
* Its architecture generalise 
    * BERT, by leveraging bidirectional encoder
    * GPT, by left to right decoder
    * Following Image Illustrates it really well
        <p align="center">
        <img width=600 src="images/bart_architecture.png">
        <em>Source: Author</em>
        </p>
* BART is trained with different pretraining objectives:
    * Masked Language Model: Following BERT approach.
    * Masked Seq2Seq: Inspired by MASS, mask a span containing 50% of tokens.
    * Language Model: Similar to GPT, BART Encoder becomes irrelevant here.
    * Permuted Language Model: Similar to XLNet, generating permuted 1/6 tokens in random order.
    * Multitask Masked Language Model: Similar to UniLM with additonal self attentions. 
* It compares various noising approaches, where,
    * novel in-filling scheme (inspired by SpanBERT), where span of input tokens are replaced by single mask (unline spanbert)
    * random shuffling of input sentences.
    * BART has evaluated following noising approaches:
        * Token Masking
        * Token Deletion
        * Text Infilling
        * Document Rotation
        * Sentence Shuffling
        * Text Infilling + Sentence Shuffling (BART best)
* BART is suitable for both generation, translation and comprehension tasks.
    * Classification: Seq to seq, in decoder a label can be trained.
    * Translation: A randomly initialized encoder gives input to pretrained encoder, and BART decoder to expects to generate target langugage. 
    * Summarisation: Encoder inputs can handle all kinds of noise, while decoder output can generate summaries.

