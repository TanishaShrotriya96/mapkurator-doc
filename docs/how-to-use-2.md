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
A sample image can be found in the folder <b><u>"/home/mapKurator-test-images/"</b></u> in the docker container. For more info, check out this quick walkthrough <a href="https://youtu.be/QgheuJ6yyF8">tutorial</a>.</p> 

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
IIIF files take between 5 to 15mins to finish processing due to their high quality and size. A sample link for IIIF can be found in <b><u>"/home/mapKurator-test-images/test_links.txt"</b></u> in the docker container. For more info, check out this quick walkthrough <a href ="https://youtu.be/yFRAkdSWmEk"> tutorial</a>.</p>

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
The annotations will appear on the image. Please note: Clicking on the "mapKurator" option from the "options" drop down on the homepage will throw an error message for WMTS. A sample link for WMTS can be found in <b><u>"/home/mapKurator-test-images/test_links.txt"</b></u> in the docker container. For more info, check out this quick walkthrough <a href="https://youtu.be/P3xnpeZMEWY">tutorial</a>.<br></p>

<h3> Model Card </h3> 
 <h4> mapKurator Spotting Models </h4>
 <p align="justify"> The docker image presently contains two spotting models, which are <b>spotter_v2</b> and <b>spotter_testr</b>. The default model when the docker image is first run, is the <b>spotter_v2</b> model. You can switch over to the spotter_testr model, by editing the file <b><u>"/home/recogito2/app/transform/mapkurator/MapKuratorService.scala"</b></u>. Search for the phrase, "//spotter V2 command", you should find the block of code shown below. <br>

* spotter v2 command
```
val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_v2/PALEJUN/ --spotter_model=spotter_v2 --spotter_config=/home/spotter_v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 
```

* spotter testr command
```
val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_testr/TESTR/ --spotter_model=testr --spotter_config=/home/spotter_testr/TESTR/configs/TESTR/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 
```
  
First, comment out the spotter_v2 code and then uncomment the spotter_testr code as shown below. This will need to be done in three places for all three input methods of recogito. Save the file when you are done, and re-run recogito with the <code>sbt runProd</code> command. <br>
 
* spotter v2 command
 ```
//val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_v2/PALEJUN/ --spotter_model=spotter_v2 --spotter_config=/home/spotter_v2/PALEJUN/configs/PALEJUN/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 
```

* spotter testr command
```
val cli = s"python /home/mapkurator-system/recogito_integration/process_image.py iiif --url=$filename --dst=data/test_imgs/sample_output/ --filename=${part.getId} --text_spotting_model_dir=/home/spotter_testr/TESTR/ --spotter_model=testr --spotter_config=/home/spotter_testr/TESTR/configs/TESTR/SynthMap/SynthMap_Polygon.yaml --gpu_id=3" 
```

 
 To learn more about the integration code refer to the file /home/mapkurator-system/recogito_integration/README.md in the docker container. 
</p>
