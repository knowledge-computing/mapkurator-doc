### Dataset Card   
Recogito accepts three types of input data formats. 
#### File Upload
You can upload an image file with the extensions .png,.jpg,.jpeg,.tif on the Recogito webapplication. To do so, click the "+New" button on the left side pane and click the "File Upload" option. To run mapKurator, select the file and click on the "options" dropdown. Then, click on the mapKurator drop down option.
A sample image can be found in the folder mapKuratorTest in the docker image. 

#### WMTS
Recogito also supports Web Map Tile Service (WMTS) which is a standard protocol for serving pre-rendered or run-time computed georeferenced map tiles over the Internet.
To upload a WMTS file, click the "+New" button on the left side pane and, click on the "WMTS Web Map Service" option. To run mapKurator on a WMTS file, double click on the WMTS file. This should take you to the image display page, with the name of the file displayed at the top, and the WMTS file displayed below it. Please zoom into the WMTS file to select a section of the image. The smaller the section, the lesser time it will take for mapKurator to finish processing. A gear icon will be present at the bottom right corner of the screen with the label "mapKurator". Click this button and select the region on the image that you want to annotate. The annotations will appear on the image. 
Here is a sample WMTS link for you to try -https://wmts.maptiler.com/aHR0cDovL3dtdHMubWFwdGlsZXIuY29tL2FIUjBjSE02THk5dFlYQnpaWEpwWlhNdGRHbHNaWE5sZEhNdWN6TXVZVzFoZW05dVlYZHpMbU52YlM4eU5WOXBibU5vTDNsdmNtdHphR2x5WlM5dFpYUmhaR0YwWVM1cWMyOXUvanNvbg/wmts"

#### IIIF  
IIIF is a set of open standards for delivering high-quality, attributed digital objects online at scale. You can also upload an IIIF file to the webapplication and run recogito. To do so, click on the "+New" button on the left side pane, and click on "From IIIF manifest" option. To run mapKurator, select the file and click on the "options" dropdown. Then, click on the mapKurator drop down option. IIIF files take between 5 to 15mins to finish processing due to their high quality and size. 
Here is a sample IIIF link for you to try - https://map-view.nls.uk/iiif/2/12563%2F125635459/info.json

### Common Errors 
 
