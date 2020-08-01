## Leveraging Pre-trained Checkpoints for Sequence Generation Tasks
### Sascha Rothe, Shashi Narayan, Aliaksei Severyn
### ACL 2020

**Whats New** Mainly, pre-trained checkpoints are available for encoder-only or decoder-only setups. Can these checkpoints are used for seq to seq generation tasks like sentence fusing, abstractive summarisation, translation etc? This paper presents set of experiments on the same.

**Key Insights** 
* Paper has mainly evaluated BERT, Roberta and GPT, and Random weights. It uses combinations of these pre-trained model as encoder and decoders, and compares performance on downstream tasks like sentence fusion, summarisation, translation etc.

* On sentence fusion tasks - ROBERTA2GPT, and ROBERTASHARE gave better performance.

* On sentence split and rephrase - BERTSHARE and ROBERTASHARE has better performance.

* On translation:
    * BERT2BERT and BERT2RAND has better performance. Note, ROBERTa was not used as its public check point was not available for target language.
    * **BERT Multilingual Cased** checkpoint was used for both encoder and decoder. Note that, it has 108 languages support and with the vocabolary of 110k word pieces.
    * Sharing encoder and decoder weights in translation task does not give better performance, possibly because vocab, grammer and linguistic patterns are different for source and target language.
    * BERT Multilingual vocab is so large, hence model can be improved by limiting the vocab to around 30K words which are required for souce and traget lanauge.

* Ablation:
    * When **just embedding matrix** are initialized, generally no improvement is found.
    * When **just layers** were trained keeping embeddings frozen, not much improvement was found.
    * It is possible to limit vocabolary first, and add new vocabolary, keep all the layers frozen and just train embedding weigths of vocabolary. Afterwhich model can be fine tuned in standard fashion. It gives relative improvement because of injecting new task specific vocabolary.
