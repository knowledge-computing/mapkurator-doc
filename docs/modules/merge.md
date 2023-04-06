### Description
When you crop a high-resolution map image into smaller tiles, you can analyze each tile independently, which can make it easier to process the image as a whole. However, in order to get a complete understanding of the image, you may need to merge the results from each individual tile to get a map-level prediction.

### Commands

The inputs for this module are patch-level spotting results 

#### 1) Use run.py 
```
python3 run.py --sample_map_csv_path='/home/maplord/maplist_csv/luna_omo_metadata_56628_20220724.csv'  --expt_name='57k_maps' --module_img_geojson```
