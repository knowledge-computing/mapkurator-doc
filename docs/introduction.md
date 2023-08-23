

mapKurator is a fully automatic pipeline developed by the **Knowledge Computing Lab** at the **University of Minnesota** to process a large number of scanned historical map images. **Outputs** include the recognized text labels, label bounding polygons, labels after post-OCR correction, and a geo-entity identifier from OpenStreetMap.


### Model Summary

- **Green boxes:** Modules in the pipeline
- **Blue boxes:** Inputs of the modules
- **Orange boxes:** Outputs of the modules

<img width="1000" alt="image" src="_media/system.png">



### Model Details
- **ImageCropping** divides large map images (>10K pixels) into map image patches (1000 x 1000 pixels) for **PatchTextSpotter** to process.

- **PatchTextSpotter** automatically detects and recognizes the text labels on map image patches. The mapKurator system offers two state-of-the-art approaches for text spotting, where the models are trained with synthetic datasets and human annotations.

- **PatchtoMapMerging** merges the patch-level spotting results into map-level. The output polygons can be loaded in QGIS for visualization, and they should be aligned with the *ungeoreferenced* map image. **Note:** JP2 files should be converted to JPEG before loading in QGIS. 

- **PostOCR** aims to verify the output and correct misspelled words from **PatchTextSpotter** using a dictionary created from OpenStreetMap. **PostOCR** identifies a word's candidates using the [fuzzy query function](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html) from an elasticsearch index of the OpenStreetMap dictionary, which contains the place name attribute from OpenStreetMap. Then **PostOCR** picks one candidate based on the word's popularity in the OpenStreetMap dictionary.

- **GeocoordinateConverter**  converts the bounding polygons of text labels from the image coordinate system to the geocoordinate system. **Note**: The polygons in both coordinate systems are saved in the output. 

- **EntityLinker** links each map text to all the candidate geo-entities in OpenStreetMap. The entity linking retrieves candidates that satisfy both criteria: 1) the suggested word (i.e. output from PostOCR) is a substring of the candidate geo-entity's name 2) the geocoordinates of a geo-entity is within the map boundary. (Geo-coordinates are obtained from GeocoordConverter)

### Cite

```
@inproceedings{li2020automatic,
  title={An automatic approach for generating rich, linked geo-metadata from historical map images},
  author={Li, Zekun and Chiang, Yao-Yi and Tavakkol, Sasan and Shbita, Basel and Uhl, Johannes H and Leyk, Stefan and Knoblock, Craig A},
  booktitle={Proceedings of the 26th ACM SIGKDD International Conference on Knowledge Discovery \& Data Mining},
  pages={3290--3298},
  year={2020}
}

@article{kim2023mapkurator,
  title={The mapKurator System: A Complete Pipeline for Extracting and Linking Text from Historical Maps},
  author={Kim, Jina and Li, Zekun and Lin, Yijun and Namgung, Min and Jang, Leeje and Chiang, Yao-Yi},
  journal={arXiv preprint arXiv:2306.17059},
  year={2023}
}
```

### License
CC BY-NC 2.0 
