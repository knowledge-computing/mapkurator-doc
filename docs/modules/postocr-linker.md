## PostOCR

@min 

## Entity Linker 
### Description
EntityLinker retrieves all the candidate geo-entities in [OpenStreetMap](https://www.openstreetmap.org/) that satisfy two criteria: 1) the suggested word (i.e. output from PostOCR) is a substring of the candidate geo-entity's name and 2) the geocoordinates of a geo-entity is within the map boundary. (Geo-coordinates are obtained from Geocoordinate Converter)

### Commands
The inputs for this module are geocoordinate converter results in `geojson` format.

#### 1) Use run.py 

##### PostOCR standalone

@min 

##### PostOCR and Entity Linker
```
python3 run.py --output_folder='/home/maplord/mapkurator_output/' --expt_name='57k_maps' --module_geocoord_geojson
```

where

* `--output_folder`: output directory
* `--expt_name`: experiment name for running the pipeline
* `--module_post_ocr_entity_linking`: turns on the post ocr and entity linking module in this run


#### 2) Use post_ocr_entity_linker.py

If you wish to specify the input and output specifically, you can use `post_ocr_entity_linker.py` in `m5_post_ocr_entity_linker` folder. 

Sample command: 
```
python3 post_ocr_entity_linker.py --in_geojson_file='{map_level_prediction.geojson}' --out_geojson_dir='{directory_path}' 
```

* `--in_geojson_file`: input geojson
* `--out_geojson_dir`: output path to save the updated geojson

