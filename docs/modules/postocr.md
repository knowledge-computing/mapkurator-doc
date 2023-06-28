### Description
#### PostOCR
PostOCR helps to verify the output and correct misspelled words from PatchTextSpotter using the [OpenStreetMap](https://www.openstreetmap.org/) dictionary. PostOCR module finds words' candidates using [fuzzy query function](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html) from [Elasticsearch](https://www.elastic.co/elasticsearch/), which contains the place name attribute from the OpenStreetMap dictionary. Once PostOCR module identifies words' candidates, the module picks one candidate by the word popularity from the dictionary.

### Commands
The inputs for this module are geocoordinate converter results in `GeoJSON` format.

#### 1) Use run.py 

Although the map image does not have Geo-coordinate, you can run stand-alone postOCR module.  

```
python3 run.py --expt_name='57k_maps' --module_post_ocr
```

where

* `--expt_name`: experiment name for running the pipeline
* `--module_post_ocr`: turns on the postOCR module in this run

#### 2) Use post_ocr_main.py
If you do not have a metadata csv file, you can directly use post_ocr_main.py in m5_post_ocr folder.

Sample command:
```
python3 post_ocr_main.py --in_geojson_file --out_geojson_dir
```