### Description
#### PostOCR
PostOCR helps to verify the output and correct misspelled words from PatchTextSpotter using the [OpenStreetMap](https://www.openstreetmap.org/) dictionary. PostOCR module finds words' candidates using [fuzzy query function](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html) from [Elasticsearch](https://www.elastic.co/elasticsearch/), which contains the place name attribute from the OpenStreetMap dictionary. Once PostOCR module identifies words' candidates, the module picks one candidate by the word popularity from the dictionary.

### Index Creation Procedures

To retrieve OpenStreetMap geo-entities and popularity score (i.e., frequency of geo-entities' names), we utilize [Postgres](https://www.postgresql.org/) database and Elasticsearch search engine.

<img width="800px" src="_media/databases.jpg"></br>

Figure shows an outline of tables on Postgres and indices on Elasticsearch. The details of each component are as follows.

* table `all_continents` : A table of all OpenStreetMap geo-entities' id, names, and the corresponding source tables
* schema `{each continent}` table `{points, lines, multilinestrings, multipolygons, other_relations}`: A source table of OpenStreetMap geo-entities including names, semantic types, and geometries
* index `osm`: An Elasticsearch index of table `all_continents`
* index `osm-voca`: An Elasticsearch index which contains place name attributes and its' popularity from the index `osm`

### Commands
The inputs for this module are geocoordinate converter results in `GeoJSON` format.

#### 1) Use run.py 

##### Stand-alone PostOCR 

Although the map image does not have Geo-coordinate, you can run stand-alone postOCR module.  

```
python3 run.py --expt_name='57k_maps' --module_post_ocr_entity_linking --module_post_ocr_only
```

where

* `--expt_name`: experiment name for running the pipeline
* `--module_post_ocr_entity_linking`: turns on the postOCR and entity linking module in this run
* `--module_post_ocr_only`: turns on stand-alone postOCR module in this run

##### PostOCR and Entity Linker
```
python3 run.py --expt_name='57k_maps' --module_post_ocr_entity_linking
```

where

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

