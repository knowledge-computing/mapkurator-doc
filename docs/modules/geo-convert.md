### Description
GeocoordinateConverter converts predicted bounding polygons (i.e., spotting results) from image coordinates to geocoordinates. Module uses [ogr2ogr](https://gdal.org/programs/ogr2ogr.html) from GDAL. Source and target coordinate reference systems are [EPSG:4326](https://epsg.io/4326) and [EPSG:3857](https://epsg.io/3857), respectively.

### Commands
The inputs for this module are 1) metadata that stores transformation method and ground control points in `csv` format and 2) map-level results in `geojson` format. You can simply overlay the output json onto map background for visualization on QGIS.

#### 1) Use run.py 
```
python3 run.py --sample_map_csv_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv'  --expt_name='57k_maps' --module_geocoord_geojson
```

where

* `--sample_map_csv_path` stores the metadata of the input map, a sample file can be found [here](https://drive.google.com/drive/folders/1Nby1JaIzNSwrGtGFn5Af0VL5y3TGLZGQ). 
* `--module_img_geojson`:  turns on the stitching module for this run 
* `--expt_name`: experiment name for running the pipeline


#### 2) Use convert_geojson_to_geocoord.py

If you wish to specify the input and output specifically, you can use `convert_geojson_to_geocoord.py` in `m4_geocoordinate_converter` folder. 

Sample command: 
```
python3 stich_output.json --sample_map_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv' --in_geojson_file='{map_level_prediction.geojson}' --out_geojson_dir='{directory_path}' 
```

* `--sample_map_path`: path to sample map csv, which contains gcps info
* `--in_geojson_file`: input geojson
* `--out_geojson_dir`: output path to save the converted geojson
