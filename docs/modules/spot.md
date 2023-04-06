
@yijun 

### Description 

The mapKurator system provides two state-of-the-art approaches for spotting text instances on scaned historical maps. Both approaches, <a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a> and Spotter-v2, are built upon <a href="https://github.com/fundamentalvision/Deformable-DETR" target="_blank">Deformable-DETR</a>.


### Training 

- Training Datasets
  - Synthetic datasets: TBD 
    - We use <a href="https://github.com/ankush-me/SynthText" target="_blank">SynthText</a>> to generate synthetic text images. Dataset: TBD
    - We propose a method to generate synthetic maps. Code & Dataset: TBD.
  - Human Annotations: TBD

- Text Spotters
  - <a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a>
  - Spotter-v2: The appoach adopts a novel feature sampling strategy that samples relevant image features around the target points for predicting boundary points, which leads to enhanced detection and recognition performance. Code: TBD.

- Training Process
  - Pretrain: We train the models with the synthetic datasets.
  - Finetune: We finetune the models with human annotations.
  

### Inference Commands 

#### 1) Use run.py 

```
python run.py --module_text_spotting 
              --sample_map_csv_path ./sample_maps.csv
              --text_spotting_model_dir ./spotter-v2/PALEJUN/
              --expt_name sample_maps 
              --spotter_model spotter-v2
              --spotter_config ./spotter-v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml
              --spotter_expt_name test
```

where

* `--module_text_spotting` turns on the spotting module in this run
* `--sample_map_csv_path` stores the metadata of the input map, a sample file can be found [here](https://drive.google.com/drive/folders/1Nby1JaIzNSwrGtGFn5Af0VL5y3TGLZGQ). 
* `--text_spotting_model_dir` switches to the model directory
* `--expt_name` is the experiment name for running the pipeline
* `--spotter_model` is the spotter model name, choices=["testr", "spotter-v2"]
* `--spotter_config` is the configuration file for running the spotting model
* `--spotter_expt_name` is the experiment name for running the spotter


#### 2) Use inference.py

```

```
