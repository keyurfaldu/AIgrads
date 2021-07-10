## Montreal Forced Aligner: Trainable Text-Speech Alignment Using Kaldi
### McAuliffe, Michael, Michaela Socolof, Sarah Mihuc, Michael Wagner, and Morgan Sonderegger.
### In Interspeech, vol. 2017, pp. 498-502. 2017. [[PDF](https://www.isca-speech.org/archive/Interspeech_2017/pdfs/1386.PDF)]

**Whats Unique**
This paper present the tool to align orthographic transcript at word level and phonene level to the speech. And, it retains trainability with new datasets.

**Key Take Aways**
* MFA has been scuccessfully applied to 29 languages.
* Its training process involve following steps:
    * 40 iterations of monophone GMM training
    * 15 iterations of monophone realignment
    * 35 iterations of triphone training
    * 15 iterations of triphone realignment
    * 35 iterations of speaker-adapted triphone training
    * 15 iterations of speaker-adapted realignment
* It uses mel-frequency cepstral coefficients (MFCCs) as acoustic features.
* Training on LibriSpeech corpus of 1000 hours data took 80 hours.
* It is evaluated against the manual annotation, Buckeye Corpus contains 20.7 hours of conversational speech from 40 speakers with manual transcript and boundaries at phone and word level.
* Average difference in actual and word level boundary is around 25 ms, and for phoneme it is around 17 ms.
* It uses Kaldi toolkit for underlying audio processing.
