

mapKurator is a **fully automatic** pipeline to process a large amount of scanned historical map images. **Outputs** include the recognized text labels, label bounding polygons, labels after post-OCR correction, and geo-entity identifier in OSM database. 

### Model Summary

- **Orange boxes:** Modules in the pipeline
- **Blue boxes:** Inputs of the modules
- **Green boxes:** Outputs of the modules

<img width="1627" alt="image" src="https://user-images.githubusercontent.com/5383572/189727942-80ad63c6-6c2e-478a-9992-c0f1519a0549.png">

### Model Details
- **ImageCropping** module divides huge map images (>10K pixels) to map image patches (1000 x 1000 pixels) for PatchTextSpotter module to process.

- **PatchTextSpotter** module automatically detects and recognizes the text labels on map image patches. We offer two state-of-the-art approaches for text spotting and provide the models trained with synthetic datasets and human annotations.

- **PatchtoMapMerging** is the module to merge the patch-level spotting results into map-level. Output polygons can be loaded in QGIS for visualization, and they should be aligned with the *ungeorefernced* map image. **Note:** QGIS is **not able to show JP2 file** directly. JP2 should be converted to JPEG before loading in QGIS. 

- **GeocoordinateConverter** converts the text label bounding polygons from image coordinates system to geocoordinates system. Note: polygons in both coordinate systems are saved in the output. 

- **PostOCR & EntityLinker** 
  - **PostOCR** helps to verify the output and correct misspelled words from PatchTextSpotter using the OpenStreetMap dictionary. PostOCR module finds words' candidates using [fuzzy query function](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html) from elasticsearch, which contains the place name attribute from the Openstreetmap dictionary. Once PostOCR module identifies words' candidates, the module picks one candidate by the word popularity from the dictionary.

  - **EntityLinker** links each map text to the candidate geo-entities in the OpenStreetMap. The entity linking retrieves the candidates that satisfy two criteria: 1) the word candidate retrieved from PostOCR module contains the geo-entities' name 2) the geocoordinates of geo-entities are within the map boundary. (Geo-coordinates are obtained from GeocoordConverter)