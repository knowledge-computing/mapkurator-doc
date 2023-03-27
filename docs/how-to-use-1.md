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
  --module_post_ocr_entity_linking
  --spotter_model {abcnet,testr}
                        Select text spotting model option from ["abcnet","testr"]
  --spotter_config SPOTTER_CONFIG
                        Path to the config file for text spotting model
  --spotter_expt_name SPOTTER_EXPT_NAME
                        Name of spotter experiment, if empty using config file name
  --print_command
  ```

@zekun @yijun @jina @min @leeje 
Provide sample commands to run each module