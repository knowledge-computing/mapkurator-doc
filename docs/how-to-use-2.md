<body>
<h3> Dataset Card </h3>   
 <p align="justify">Recogito accepts three types of input data formats.</p> 
<h4> File Upload </h4>
<p align="justify">You can upload an image file with the extensions .png,.jpg,.jpeg,.tif on the Recogito webapplication.<br>
Steps:<br>
 <ol>
  <li> Click the <b>"+New"</b> button on the left side pane.</li>
  <li> Click the <b>"File Upload"</b> option.</li>
  <li> Select the file and click on the <b>"options"</b> dropdown.</li>
  <li> Click on the <b>"mapKurator"</b> drop down option.</li>
  <li> Wait for the message <b>"processing completed"</b> to appear. </li>
  <li> Click on the image to see the annotated text.</li> 
 </ol>
A sample image can be found at <a href="https://drive.google.com/file/d/1lIm9Xh9zNmaZ8gT9H_lrovtHaT97Sb9G/view?usp=sharing">https://drive.google.com/file/d/1lIm9Xh9zNmaZ8gT9H_lrovtHaT97Sb9G/view?usp=sharing </a>
For more info, check out this quick walkthrough <a href="https://youtu.be/QgheuJ6yyF8">tutorial</a>.</p> 

<h4>IIIF Upload</h4>  
<p align="justify">IIIF is a set of open standards for delivering high-quality, attributed digital objects online at scale. You can also upload an IIIF file to the webapplication and run recogito.<br>
Steps:<br> 
 <ol>
  <li> Click the <b>"+New"</b> button on the left side pane.</li> 
  <li> Click on "From IIIF manifest" option.</li> 
  <li> Select the file and click on the <b>"options"</b> dropdown.</li>
  <li> Click on the <b>"mapKurator"</b> drop down option.</li>
  <li> Wait for the message <b>"processing completed"</b> to appear. </li>
  <li> Click on the image to see the annotated text.</li> 
 </ol>
IIIF files take between 5 to 15mins to finish processing due to their high quality and size. A sample link for IIIF is 

```
https://map-view.nls.uk/iiif/2/12563%2F125635459/info.json
``` 


For more info, check out this quick walkthrough <a href ="https://youtu.be/yFRAkdSWmEk"> tutorial</a>.</p>

<h4>WMTS Upload</h4>
<p align="justify">Recogito also supports Web Map Tile Service (WMTS) which is a standard protocol for serving pre-rendered or run-time computed georeferenced map tiles over the Internet. To upload a WMTS file follow the steps below.<br>
Steps:<br> 
<ol>
 <li> Click the <b>"+New"</b> button on the left side pane</li>
 <li> Click on the <b>"WMTS Web Map Service"</b> option.</li>
 <li> Double click on the uploaded WMTS image.</li> 
 <li> Zoom into the WMTS file to select a section of the image. The smaller the section, the lesser time it will take for mapKurator to finish processing.</li> 
 <li> Press the <b>gear</b> icon at the bottom right corner of the screen with the label "mapKurator".</li>
 <li> Select the region on the image that you want to annotate.</li> 
</ol>
The annotations will appear on the image. Please note: Clicking on the "mapKurator" option from the "options" drop down on the homepage will throw an error message for WMTS. A sample link for WMTS is 

```
https://wmts.maptiler.com/aHR0cDovL3dtdHMubWFwdGlsZXIuY29tL2FIUjBjSE02THk5dFlYQnpaWEpwWlhNdGRHbHNaWE5sZEhNdWN6TXVZVzFoZW05dVlYZHpMbU52YlM4eU5WOXBibU5vTDNsdmNtdHphR2x5WlM5dFpYUmhaR0YwWVM1cWMyOXUvanNvbg/wmts
````
For more info, check out this quick walkthrough <a href="https://youtu.be/P3xnpeZMEWY">tutorial</a>.<br></p>

<h3> Model Card </h3> 
 <h4> mapKurator Spotting Models </h4>
 <p align="justify"> The docker image presently contains two spotting models, which are <b>spotter-v2</b> and <b>spotter_testr</b>. The default model when the docker image is first run, is the <b>spotter-v2</b> model. Following steps show how to switch the spotting modules for recogito.
<ul>
<li>If you have a running instance of recogito, ie the terminal used for Step 5, then exit from the recogito instance using Ctrl+C
 You should see the following in the bash terminal <code>(mapkurator)root@CONTAINER_ID:/home/recogito2#</code>
 </li> 
<li> 
To switch the spotting model to <b>spotter_testr</b> use command - <code>bash /select.sh SpotterTestr</code></li>
<li> 
<b>OR</b> to switch the spotting model to <b>spotter-v2</b> use command - <code>bash /select.sh SpotterV2</code></li>
</li>
<li>
Run the Recogito web-application ->  <code>sbt "runProd -Dhttp.port=YOUR_PORT_ON_DOCKER"</code>
</li>
</ul>
To learn more about the integration code refer to the file /home/mapkurator-system/recogito_integration/README.md in the docker container. 
</p>
