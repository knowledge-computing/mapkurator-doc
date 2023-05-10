### Stand-alone mapKurator with Ubuntu18.04 with cuda_11.3_devel
All the modules can be launched from `run.py`. All the outputs will be saved in the `expt_name` subfolder in `output_folder` specified in the input arguments. 

```
usage: run.py [-h] [--map_kurator_system_dir MAP_KURATOR_SYSTEM_DIR] [--text_spotting_model_dir TEXT_SPOTTING_MODEL_DIR]
              [--sample_map_csv_path SAMPLE_MAP_CSV_PATH] [--output_folder OUTPUT_FOLDER] [--expt_name EXPT_NAME] [--module_get_dimension]
              [--module_gen_geotiff] [--module_cropping] [--module_text_spotting] [--module_img_geojson] [--module_geocoord_geojson] [--module_post_ocr_entity_linking] [--spotter_model {abcnet,testr}] [--spotter_config SPOTTER_CONFIG] [--spotter_expt_name SPOTTER_EXPT_NAME] [--print_command]

optional arguments:
  -h, --help            show this help message and exit
  --map_kurator_system_dir MAP_KURATOR_SYSTEM_DIR
  --text_spotting_model_dir TEXT_SPOTTING_MODEL_DIR
  --sample_map_csv_path SAMPLE_MAP_CSV_PATH
  --output_folder OUTPUT_FOLDER
  --expt_name EXPT_NAME
  --module_get_dimension
  --module_gen_geotiff
  --module_cropping
  --module_text_spotting
  --module_img_geojson
  --module_geocoord_geojson
  --module_post_ocr
  --module_entity_linking
  --spotter_model {abcnet,testr}
                        Select text spotting model option from ["abcnet","testr"]
  --spotter_config SPOTTER_CONFIG
                        Path to the config file for text spotting model
  --spotter_expt_name SPOTTER_EXPT_NAME
                        Name of spotter experiment, if empty using config file name
  --print_command
  ```

Example for running the **cropping** module
```
python3 run.py --sample_map_csv_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv'  
                  --expt_name='57k_maps' 
                  --module_cropping
```

Example for running the **spotting** module
```
python run.py --module_text_spotting 
              --text_spotting_model_dir ./spotter-v2/PALEJUN/
              --sample_map_csv_path ./sample_maps.csv
              --expt_name sample_maps 
              --spotter_model spotter-v2
              --spotter_config ./spotter-v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml
              --spotter_expt_name test
```

Example for running the **PatchtoMapMerging** module
```
python3 run.py  --sample_map_csv_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv'  
                --expt_name='57k_maps' 
                --module_img_geojson
```

Example for running the **GeocoordinateConverter** module
```
python3 run.py  --sample_map_csv_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv'  
                --expt_name='57k_maps' 
                --module_geocoord_geojson
```

Example for running the stand-alone **PostOCR** module
```
python3 run.py --expt_name='57k_maps' 
               --module_post_ocr
```

### Using mapKurator-Recogito docker image for standalone mapKurator 

To run mapKurator from the docker image, first change directory as -     
```
cd /home/mapkurator-system/
```
Then, activate the conda environment with -    
```
conda activate mapkurator
```

Then you can use run_img.py upto the stitch module using the sample command below.     

```
python run_img.py --map_kurator_system_dir /home/mapkurator-system/ --sample_map_csv_path /home/mapkurator-test-images/input/test/ --expt_name mapKurator_test --module_cropping --module_get_dimension --module_text_spotting --text_spotting_model_dir /home/spotter_v2/PALEJUN/ --spotter_model spotter_v2 --spotter_config /home/spotter_v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml --spotter_expt_name test --module_img_geojson --output_folder /home/mapkurator-test-images/output/ --gpu_id 3
```

```
usage: run_img.py [-h] [--map_kurator_system_dir MAP_KURATOR_SYSTEM_DIR] [--text_spotting_model_dir TEXT_SPOTTING_MODEL_DIR]
                  [--sample_map_csv_path SAMPLE_MAP_CSV_PATH] [--output_folder OUTPUT_FOLDER] [--expt_name EXPT_NAME] [--module_get_dimension]
                  [--module_gen_geotiff] [--module_cropping] [--module_text_spotting] [--module_img_geojson] [--module_geocoord_geojson]
                  [--module_entity_linking] [--module_post_ocr] [--spotter_model {abcnet,testr,spotter_v2,spotter_v3}] [--spotter_config SPOTTER_CONFIG]
                  [--spotter_expt_name SPOTTER_EXPT_NAME] [--print_command] [--gpu_id GPU_ID]
                  
optional arguments:
--module_cropping 
--module_get_dimension 
--module_text_spotting 
--text_spotting_model_dir="/home/spotter_v2/PALEJUN/" 
--spotter_model=spotter_v2 
--spotter_config="/home/spotter_v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml"
--spotter_expt_name=test 
--module_img_geojson 
--output_folder=/home/mapkurator-system/data/ 
--gpu_id=ADD_YOUR_GPU_ID
```

Commands for spotter_testr configuration:      
```
--text_spotting_model_dir=/home/spotter_testr/TESTR/
--spotter_model=testr
--spotter_config=/home/spotter_testr/TESTR/configs/TESTR/SynthMap/SynthMap_Polygon.yaml  
```

Commands for spotter_v2 configuratiom:       
```
--text_spotting_model_dir=/home/spotter_v2/PALEJUN/
--spotter_model=spotter_v2    
--spotter_config=/home/spotter_v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml
```
