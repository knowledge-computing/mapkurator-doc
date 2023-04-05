

mapKurator is a **fully automatic** pipeline to process a large amount of scanned historical map images. **Outputs** include the recognized text labels, label bounding polygons, labels after post-OCR correction, and geo-entity identifier in OSM database. 

### Model Summary

- **Orange boxes:** Modules in the pipeline
- **Blue boxes:** Inputs of the modules
- **Green boxes:** Outputs of the modules

<img width="1000" alt="image" src="https://user-images.githubusercontent.com/5383572/230233058-b4852134-9e2c-4622-af69-d8794cf298ed.png">


### Model Details
- **ImageCropping** divides huge map images (>10K pixels) to map image patches (1000 x 1000 pixels) for **PatchTextSpotter** to process.

- **PatchTextSpotter** automatically detects and recognizes the text labels on map image patches. The mapKurator system offers two state-of-the-art approaches for text spotting, where the models are trained with synthetic datasets and human annotations.

- **PatchtoMapMerging** merges the patch-level spotting results into map-level. The output polygons can be loaded in QGIS for visualization, and they should be aligned with the *ungeorefernced* map image. **Note:** JP2 files should be converted to JPEG before loading in QGIS. 

- **GeocoordinateConverter**  converts the bounding polygons of text labels from the image coordinates system to the geocoordinates system. **Note**: The polygons in both coordinate systems are saved in the output. 

- **PostOCR & EntityLinker** 
  - **PostOCR** aims to verify the output and correct misspelled words from **PatchTextSpotter** using the OpenStreetMap dictionary. **PostOCR** identifies words' candidates using [fuzzy query function](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html) from elasticsearch, which contains the place name attribute from Openstreetmap. Then **PostOCR** picks one candidate by the word popularity from the dictionary.

  - **EntityLinker** links each map text to the candidate geo-entities in the OpenStreetMap. The entity linking retrieves the candidates that satisfy two criteria: 1) the word candidate retrieved from PostOCR module contains the geo-entities' name 2) the geocoordinates of geo-entities are within the map boundary. (Geo-coordinates are obtained from GeocoordConverter)
