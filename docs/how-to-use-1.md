To run mapKurator from the docker image, first change directory as -     
```
cd /home/mapkurator-system/
```
Then, activate the conda environment with -    
```
conda activate mapkurator
```

Then you can use `run_img.py` upto the stitch module using the sample command below.     

```
python run_img.py --map_kurator_system_dir /home/mapkurator-system/ --input_dir_path /home/mapkurator-test-images/input/ --expt_name mapKurator_test --module_cropping --module_get_dimension --module_text_spotting --text_spotting_model_dir /home/spotter-v2/PALEJUN/ --spotter_model spotter-v2 --spotter_config  /home/spotter-v2/PALEJUN/configs/PALEJUN/Finetune/Rumsey_Polygon_Finetune.yaml --spotter_expt_name test --module_img_geojson --output_folder /home/mapkurator-test-images/output/ --gpu_id 0
```

```
usage: run_img.py [-h] [--map_kurator_system_dir MAP_KURATOR_SYSTEM_DIR] [--text_spotting_model_dir TEXT_SPOTTING_MODEL_DIR]
                  [--input_dir_path INPUT_DIR_PATH] [--output_folder OUTPUT_FOLDER] [--expt_name EXPT_NAME] [--module_get_dimension]
                  [--module_gen_geotiff] [--module_cropping] [--module_text_spotting] [--module_img_geojson] [--module_post_ocr] 
                  [--module_geocoord_geojson] [--module_entity_linking] [--spotter_model {abcnet,testr,spotter-v2,spotter_v3}] [--spotter_config SPOTTER_CONFIG]
                  [--spotter_expt_name SPOTTER_EXPT_NAME] [--print_command] [--gpu_id GPU_ID]
                  
optional arguments:
--module_cropping 
--module_get_dimension 
--module_text_spotting 
--text_spotting_model_dir="/home/spotter-v2/PALEJUN/" 
--spotter_model=spotter-v2 
--spotter_config  /home/spotter-v2/PALEJUN/configs/PALEJUN/Finetune/Rumsey_Polygon_Finetune.yaml
--spotter_expt_name=test 
--module_img_geojson 
--output_folder=/home/mapkurator-system/data/ 
--gpu_id=ADD_YOUR_GPU_ID
```
