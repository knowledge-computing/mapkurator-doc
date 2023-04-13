

### Description 

As historical maps are written in multiple languages, extracting multilingual text from scanned maps could be valuable information for unlocking the rich historical and cultural information in historical maps with multilingual text. 

The mapKurator system provides multilingual text spotting on scanned historical maps with two state-of-the-art approaches.(<a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a> and Spotter-v2) 

### Supported Language
English, Russian, Arabic, Chinese, Japanese


### Training Datasets
- Synthetic datasets:
  Using two approaches to synthesize text-free images with text, we generated synthetic datasets in English, Russian, Arabic, Chinese, and Japanese.  

  - SynthText datasets :
    - <a href="https://github.com/ankush-me/SynthText" target="_blank">Github</a>; <b>Dataset:</b> TBD;

  - Synmap datasets :
   - <b>Code:</b> TBD; <b>Dataset:</b> TBD;

### Training Process

- Training Process
  - Train: We train the TESTR and Spotter-v2 with the synthetic datasets.

  