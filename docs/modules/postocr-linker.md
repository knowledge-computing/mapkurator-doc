### Description
#### PostOCR
@min 

#### Entity Linker
EntityLinker retrieves the candidate geo-entities in [OpenStreetMap](https://www.openstreetmap.org/) that satisfy two criteria: 1) the suggested word (i.e. output from PostOCR) is a substring of the candidate geo-entity's name and 2) the geocoordinates of a geo-entity is within the map boundary. Geo-coordinates are obtained from Geocoordinate Converter.

### Index Creation Procedures

To retrieve OpenStreetMap geo-entities and popularity score (i.e., frequency of geo-entities' names), we utilize [Postgres](https://www.postgresql.org/) database and [Easticsearch](https://www.elastic.co/elasticsearch/) search engine.

<img width="800px" src="_media/databases.jpg"></br>

Figure shows an outline of tables on Postgres and indicies on Elasticsearch. The details of each component are as follows.

* table `all_continents` : A table of all OpenStreetMap geo-entities' id, names, and the corresponding source tables
* schema `{each continent}` table `{points, lines, multilinestrings, multipolygons, other_relations}`: A source table of OpenStreetMap geo-entities including names, semantic types, and geometries
* index `osm`: An elasticsearch index of table `all_continents`
* index `osm-voca`: @min

### Commands
The inputs for this module are geocoordinate converter results in `GeoJSON` format.

#### 1) Use run.py 

##### Stand-alone PostOCR 

@min 

##### PostOCR and Entity Linker
```
python3 run.py --output_folder='/home/maplord/mapkurator_output/' --expt_name='57k_maps' --module_post_ocr_entity_linking
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

* `--in_geojson_file`: input GeoJSON
* `--out_geojson_dir`: output path to save the updated GeoJSON

