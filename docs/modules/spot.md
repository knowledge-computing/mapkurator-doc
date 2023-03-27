
@yijun 

The mapKurator system provides two state-of-the-art approaches for spotting text instances on scaned historical maps. Both approaches, <a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a> and Spotter-v2, are built upon <a href="https://github.com/fundamentalvision/Deformable-DETR" target="_blank">Deformable-DETR</a>.

- Training Datasets
  - Synthetic datasets: TBD 
  - Human Annotations: TBD

- Text Spotters
  - <a href="https://github.com/mlpc-ucsd/TESTR" target="_blank">TESTR</a>
  - Spotter-v2: The appoach adopts a novel feature sampling strategy that samples relevant image features around the target points for predicting boundary points, which leads to enhanced detection and recognition performance. Code: TBD

- Training Process
  - Pretrain: We train the models with the synthetic datasets.
  - Finetune: We finetune the models with human annotations.
  

