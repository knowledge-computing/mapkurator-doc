## PostOCR

@min 

## Entity Linker 
### Description
EntityLinker retrieves all the candidate geo-entities in [OpenStreetMap](https://www.openstreetmap.org/) that satisfy two criteria: 1) the suggested word (i.e. output from PostOCR) is a substring of the candidate geo-entity's name and 2) the geocoordinates of a geo-entity is within the map boundary. (Geo-coordinates are obtained from GeocoordConverter)