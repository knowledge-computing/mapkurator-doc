### Description
EntityLinker links text labels to the corresponding geo-entities in external knowledge bases (e.g., [OpenStreetMap](https://www.openstreetmap.org/)) to enable advanced search queries on scanned maps.
In the current version of the mapKurator, EntityLinker retrieves the candidate geo-entities in OpenStreetMap that satisfy two criteria: 1) the suggested word (i.e., output from PostOCR) is a substring of the candidate geo-entity's name and 2) the geocoordinates of text bounding polygon (i.e., output from Geocoordinate Converter) is in the buffer of OpenStreetMap geo-entities.

### Commands
The inputs for this module are 1) metadata in `CSV` format and 2) PostOCR results in `GeoJSON` format.

#### 1) Use run.py 
```
python3 run.py --sample_map_csv_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv' --expt_name='57k_maps' --module_entity_linking
```

where

* `--sample_map_csv_path` stores the metadata of the input map, a sample file can be found [here](https://searchworks.stanford.edu/view/ss311gz1992).
* `--output_folder`: output directory
* `--expt_name`: experiment name for running the pipeline
* `--module_entity_linking` turns on the entity linker module in this run

#### 2) Use entity_linking.py

If you wish to specify the input and output specifically, you can use `convert_geojson_to_geocoord.py` in `m4_geocoordinate_converter` folder. 

Sample command: 
```
python3 entity_linking.py --sample_map_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv' --in_geojson_dir='{directory_path of PostOCR results}' --out_geojson_dir='{directory_path}' 
```

* `--sample_map_path`: stores the list of the map
* `--in_geojson_dir`: input path of PostOCR output
* `--out_geojson_dir`: output path to save the generated GeoJSON