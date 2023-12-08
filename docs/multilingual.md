

### Description 

Historical maps contain valuable information for unlocking the rich historical and cultural information with multiple languages. The mapKurator system provides multilingual text spotting on scanned historical maps with two state-of-the-art approaches.(<a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a> and <a href="https://knowledge-computing.github.io/mapkurator-doc/#/docs/modules/spot" target="_blank"> Spotter-v2</a>) 

### Supported Languages
English, Russian, Arabic, Chinese, Japanese


### Training Datasets and Training Process
- Training Datasets and training process are described in <a href="https://knowledge-computing.github.io/mapkurator-doc/#/docs/modules/spot" target="_blank">here</a> 

### Inference Commands 

#### 1) Use run.py 

To run spotting with multilingual models, you can download (1) a config directory and paired (2) pretrained model weight of each language <a href="https://github.com/knowledge-computing/mapkurator-spotter" target="_blank">here</a> . Make sure to place the config directory under `/spotter-v2/PALEJUN/configs/PALEJUN/`and then change a path of `MODEL.WEIGHTS` in `SynthMap_Polygon.yaml` correctly following your downloaded model path. 

You can call `run.py` with the following command, which is a same steps of English spotter in <a href="https://knowledge-computing.github.io/mapkurator-doc/#/docs/modules/spot" target="_blank">here</a> : 

```
python run.py --module_text_spotting 
              --sample_map_csv_path /home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv
              --text_spotting_model_dir ./spotter-v2/PALEJUN/
              --expt_name sample_maps 
              --spotter_model spotter-v2
              --spotter_config ./spotter-v2/PALEJUN/configs/PALEJUN/config-ru/SynthMap-ru/SynthMap_Polygon.yaml
              --spotter_expt_name test
              --gpu_id 0
```

where

* `--module_text_spotting` turns on the spotting module in this run
* `--sample_map_csv_path` stores the metadata of the input map, a sample file can be found [here](https://drive.google.com/drive/folders/1Nby1JaIzNSwrGtGFn5Af0VL5y3TGLZGQ). 
* `--text_spotting_model_dir` switches to the model directory
* `--expt_name` is the experiment name for running the pipeline
* `--spotter_model` is the spotter model name, choices=[ "spotter-v2"]
* `--spotter_config` is the configuration file for running the spotting model
* `--spotter_expt_name` is the experiment name for running the spotter
* `--gpu_id` selects a GPU for running the spotter


#### 2) Use inference.py

If you do not have a metadata csv file, or wish to specify the input path of image directly, you can use `tools/inference.py` in the model folder (i.e., text_spotting_model_dir). 

```
python tools/inference.py --config-file ./spotter-v2/PALEJUN/configs/PALEJUN/config-ru/SynthMap-ru/SynthMap_Polygon.yaml
                          --output_json 
                          --input ./test_images
                          --output ./output

```
where

* `--config-file` is the configuration file for running the spotting model
* `--output_json` indicates the output file format is JSON
* `--input` is the input image directory
* `--output` is the output file directory
* You can set GPU with `CUDA_VISIBLE_DEVICES={gpu_id}`, default gpu_id=0

  
