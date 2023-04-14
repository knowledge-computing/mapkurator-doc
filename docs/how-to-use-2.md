<body>
<h3> Dataset Card </h3>   
 <p align="justify">Recogito accepts three types of input data formats.</p> 
<h4> File Upload </h4>
<p align="justify">You can upload an image file with the extensions .png,.jpg,.jpeg,.tif on the Recogito webapplication. To do so, click the "+New" button on the left side pane and click the "File Upload" option. To run mapKurator, select the file and click on the "options" dropdown. Then, click on the "mapKurator" drop down option. After the message "processing completed" is displayed, you can click on the image to see the annotated text. A sample image can be found in the folder /home/mapKurator-test-images in the docker image. For more info, check out this quick walkthrough <a href="https://youtu.be/QgheuJ6yyF8">tutorial</a>.</p> 

<h4>IIIF Upload</h4>  
<p align="justify">IIIF is a set of open standards for delivering high-quality, attributed digital objects online at scale. You can also upload an IIIF file to the webapplication and run recogito. To do so, click on the "+New" button on the left side pane, and click on "From IIIF manifest" option. To run mapKurator, select the file and click on the "options" dropdown. Then, click on the mapKurator drop down option. IIIF files take between 5 to 15mins to finish processing due to their high quality and size. After the message "processing completed" is displayed, you can click on the image to see the annotated text. For more info, check out this quick walkthrough <a href ="https://youtu.be/yFRAkdSWmEk"> tutorial</a>.<br> Here is a sample IIIF link for you to try - <code> https://map-view.nls.uk/iiif/2/12563%2F125635459/info.json </code></p>

<h4>WMTS Upload</h4>
<p align="justify">Recogito also supports Web Map Tile Service (WMTS) which is a standard protocol for serving pre-rendered or run-time computed georeferenced map tiles over the Internet. To upload a WMTS file, click the "+New" button on the left side pane and, click on the "WMTS Web Map Service" option. To run mapKurator on a WMTS file, double click on the uploaded WMTS image. This should take you to the image display page, with the name of the file displayed at the top, and the WMTS file displayed below it. Please zoom into the WMTS file to select a section of the image. The smaller the section, the lesser time it will take for mapKurator to finish processing. A gear icon will be present at the bottom right corner of the screen with the label "mapKurator". Click this button and select the region on the image that you want to annotate. The annotations will appear on the image. Please note: Clicking on the "mapKurator" option from the "options" drop down on the homepage will throw an error message for WMTS. For more info, check out this quick walkthrough <a href="https://youtu.be/P3xnpeZMEWY">tutorial</a>.<br> Here is a sample WMTS link for you to try -<code>https://wmts.maptiler.com/aHR0cDovL3dtdHMubWFwdGlsZXIuY29tL2FIUjBjSE02THk5dFlYQnpaWEpwWlhNdGRHbHNaWE5sZEhNdWN6TXVZVzFoZW05dVlYZHpMbU52YlM4eU5WOXBibU5vTDNsdmNtdHphR2x5WlM5dFpYUmhaR0YwWVM1cWMyOXUvanNvbg/wmts"</code></p>

<h3> Model Card </h3> 
 <h4> mapKurator Spotting Models </h4>
 <p align="justify"> The docker image presently contains two spotting models, which are spotter_v2 and spotter_testr. The default model which runs when the docker image is first run, is the spotter_v2 model. You can switch over to the spotter_testr model, by editing the file "/home/recogito2/app/transform/mapkurator/MapKuratorService.scala". Search for the word, "spotter", you should find the block of code shown below. <br>
 <code>        
// 1. Start mapKurator processing
//spotter v2 command
val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_v2/PALEJUN/ --spotter_model=spotter_v2 --spotter_config=/home/spotter_v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 

//spotter testr command
//val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_testr/TESTR/ --spotter_model=testr --spotter_config=/home/spotter_testr/TESTR/configs/TESTR/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 
</code><br>
  First, comment out the spotter_v2 code and then uncomment the spotter_testr code as shown below. This will need to be done in three places for all three input methods of recogito.<br>
<code>        
// 1. Start mapKurator processing
//spotter v2 command
//val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_v2/PALEJUN/ --spotter_model=spotter_v2 --spotter_config=/home/spotter_v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 

//spotter testr command
val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_testr/TESTR/ --spotter_model=testr --spotter_config=/home/spotter_testr/TESTR/configs/TESTR/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 
</code>
 
 To learn more about the integration code refer to the file /home/mapkurator-system/recogito_integration/README.md in the docker image. 
</p>
