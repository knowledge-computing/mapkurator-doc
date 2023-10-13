
### Description 

The mapKurator system provides two state-of-the-art approaches for spotting text instances on scaned historical maps. Both approaches, <a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a> and Spotter-v2, are built upon <a href="https://github.com/fundamentalvision/Deformable-DETR" target="_blank">Deformable-DETR</a>.

### Training Processs

- Training Datasets
  - Synthetic datasets:  
    - <b>SynthText:</b> We select 40k text-free background images from <a href="https://cocodataset.org/#home" target="_blank">COCO</a> and use them to generate synthetic text images (see the left image). <b>Code:</b> <a href="https://github.com/ankush-me/SynthText" target="_blank">Github</a> and Dataset: <a href="https://s3.msi.umn.edu/rumsey-spotter-train-data-en/SynthText.zip" target="_blank" > here </a> 
    - <b>SynMap:</b> We propose an approach to generate synthetic maps that mimic the text (e.g., font, spacing, orientation) and background styles in the real historical maps (see the right image). <b>Code:</b> TBD  and Dataset : <a href="https://s3.msi.umn.edu/rumsey-spotter-train-data-en/SynthMap.zip" target="_blank" > here </a> 
    - The synthetic datasets are in English, Arabic, Russian, and Chinese. We use these datasets for training multilingual text spotters (see <a href="https://knowledge-computing.github.io/mapkurator-doc/#/docs/multilingual" target="_blank"> Multilingual Spotting</a>).
  - Human Annotations : <a href="https://s3.msi.umn.edu/rumsey-spotter-train-data-en/rumsey-train.zip" target="_blank" > here </a> 

<p align="center">
<img width="650" alt="image" src="_media/syn_image_example.jpg">
</p>

- Text Spotters
  - <a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a>: A state-of-the-art text spotting model, originally on scene images, using <a href="https://arxiv.org/abs/2010.04159" target="_blank">Deformable Transformers</a>. <a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">[Code]</a>
  - Spotter-v2: We propose a new appoach adopts a novel feature sampling strategy that samples relevant image features around the target points for predicting boundary points, which leads to enhanced detection and recognition performance. <a href="https://github.com/knowledge-computing/mapkurator-spotter/tree/main" target="_blank">[Code]</a>

- Training Process
  - Pretrain: We train the TESTR and Spotter-v2 with the synthetic datasets.
  - Finetune: We finetune the models with human annotations.
  

### Inference Commands 

#### 1) Use run.py 

To run spotting, you can call `run.py` with the following command: 

```
python run.py --module_text_spotting 
              --sample_map_csv_path /home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv
              --text_spotting_model_dir ./spotter-v2/PALEJUN/
              --expt_name sample_maps 
              --spotter_model spotter-v2
              --spotter_config ./spotter-v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml
              --spotter_expt_name test
              --gpu_id 0
```

where

* `--module_text_spotting` turns on the spotting module in this run
* `--sample_map_csv_path` stores the metadata of the input map, a sample file can be found [here](https://drive.google.com/drive/folders/1Nby1JaIzNSwrGtGFn5Af0VL5y3TGLZGQ). 
* `--text_spotting_model_dir` switches to the model directory
* `--expt_name` is the experiment name for running the pipeline
* `--spotter_model` is the spotter model name, choices=["testr", "spotter-v2"]
* `--spotter_config` is the configuration file for running the spotting model
* `--spotter_expt_name` is the experiment name for running the spotter
* `--gpu_id` selects a GPU for running the spotter


#### 2) Use inference.py

If you do not have a metadata csv file, or wish to specify the input path of image directly, you can use `tools/inference.py` in the model folder (i.e., text_spotting_model_dir). 

```
python tools/inference.py --config-file ./spotter-v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml
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
