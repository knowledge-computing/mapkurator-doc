The stand-alone mapKurator-system requires that *cuda_11.3* with *cudnn* and *nvidia-smi* is working properly on the underlying host OS. For a successful installation, you may need to use *cuda_11.3-devel*. You can learn more [here](https://github.com/NVIDIA/nvidia-docker/wiki/CUDA).     
     
Note that *cuda_11.3* only provided support for *Ubuntu 20.04* and below at the time this document was created. 

### Installing mapKurator on Ubuntu18.04 with cuda_11.3_devel 

#### Setup Anaconda 
Setup an anaconda environment by running the following commands.   
    
1. Download the latest anaconda setup -    
```wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh```
   You may replace the link above with the latest link from [anaconda](https://www.anaconda.com/products/distribution#Downloads).   
2. Run the installation file.   
```bash Anaconda3-2022.10-Linux-x86_64.sh```       
      
3. Create a conda environment to install all software packages required by mapKurator-system.    
```conda create --name mapKurator -y python=3.8```   
4. Activate the environment.       
```conda activate mapKurator```   

#### Clone the mapKurator repository

``` git clone https://github.com/knowledge-computing/mapkurator-system```

#### Install Required Libraries     

1. Install all python packages with the commands below.        

```python -m pip install numpy==1.21.6```<br>
```python -m pip install opencv-python```<br>
```python -m pip install pandas==1.4.3```<br>
```python -m pip install Pillow==9.4.0```<br>
```pip install Polygon3```<br>
```python -m pip install shapely==1.8.2```<br>
```python -m pip install geojson==2.5.0```<br>
```python3 -m pip install setuptools==59.5.0```<br>

```conda install pytorch==1.10.0 torchvision==0.11.0 torchaudio==0.10.0 cudatoolkit=11.3 -c pytorch -c conda-forge```<br>
```pip install scikit-image```<br>
```pip install matplotlib```<br>
```pip install numba```<br>
```pip install jupyterlab```


3. Install ```gdal``` by following the instructions [here](https://mothergeo-py.readthedocs.io/en/latest/development/how-to/gdal-ubuntu-pkg.html) 
4. Install ```PostgreSQL``` by following the instructions [here](https://www.postgresql.org/download/). Tested version: 14.7
5. Install ```elasticsearch``` by following the instructions [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/targz.html). Tested version: 7.10.1
6. Install ```logstash``` by following the instructions [here](https://www.elastic.co/guide/en/logstash/current/installing-logstash.html). Tested version: 8.7.0
7. Install Detectron      
```python -m pip install detectron2 -f  https://dl.fbaipublicfiles.com/detectron2/wheels/cu113/torch1.10/index.html```     
  
8. Install Adelaidet     
```git clone https://github.com/aim-uofa/AdelaiDet.git```      
```cd AdelaiDet```      
```python setup.py build develop```           
 
Please note that the mapKurator-system has been tested with the versions shown above only. If you test it on latest versions and find any issues, please let us know!       

#### Clone the mapKurator-textspotter repository
```git clone https://github.com/knowledge-computing/mapkurator-spotter.git``` <br>
```cd /mapkurator-spotter/spotter-v2``` <br>
```python setup.py build develop```<br>



#### Index Creation Procedures for PostOCR and Entity Linker Modules

To retrieve OpenStreetMap geo-entities and popularity score (i.e., frequency of geo-entities' names), we utilize [Postgres](https://www.postgresql.org/) database and Elasticsearch search engine.

<img width="800px" src="_media/databases.jpg"></br>

Figure shows an outline of tables on Postgres and indices on Elasticsearch. The details of each component are as follows.

* table `all_continents` : A table of all OpenStreetMap geo-entities' id, names, and the corresponding source tables
* schema `{each continent}` table `{points, lines, multilinestrings, multipolygons, other_relations}`: A source table of OpenStreetMap geo-entities including names, semantic types, and geometries
* index `osm`: An Elasticsearch index of table `all_continents`
* index `osm-voca`: An Elasticsearch index which contains place name attributes and its' popularity from the index `osm`

Once you have `osm` index, you can create `osm-voca` index, please follow this procedure:

```python m5_post_ocr/preprocess.py```

Then, you can find `total.csv` is created. Now, we can create osm-voca index by running:

```sudo /usr/share/logstash/bin/logstash -f m5_post_ocr/logstash-postocr.conf```.


### Using mapKurator-Recogito docker image for standalone mapKurator - 
NOTE: This section tested upto stitch module.       

If you face issues with the cuda installation, please consider using our docker image which is built on [nvidia/cuda:11.3.0-devel-ubuntu18.04](https://hub.docker.com/layers/nvidia/cuda/11.3.0-devel-ubuntu18.04/images/sha256-79ba930c17842750cd646dd9e78911199f48b7ea1f7ec378dbf90fdea1d95ba1?context=explore). 

To try it out, first pull the docker image with the following command - ```docker pull knowledgecomputing/mapkurator_recogito_2023:latest```
Then run the container with - 
```
docker run -it --name YOUR_CONTAINER_NAME --gpus all -v /PATH/TO/INPUT/FOLDER/ON/HOST_MACHINE:/home/mapkurator-test-images/input/ -v /PATH/TO/OUTPUT/FOLDER/ON/HOST_MACHINE:/home/mapkurator-test-images/output/  knowledgecomputing/mapkurator_recogito_2023 
```  
**NOTE**: 
1) Remember to change `/PATH/TO/INPUT/FOLDER/ON/HOST_MACHINE` in the above command to an actual path on your host machine. 
2) The -v option in the command above gives your docker container access to the folders on host machine. More documentation can be found at this [link](https://docs.docker.com/storage/volumes/)

Then refer to this how-to-use [link](https://knowledge-computing.github.io/mapkurator-doc/#/docs/how-to-use-1). Ensure that you place any test images in the /PATH/TO/INPUT/FOLDER/ON/HOST_MACHINE mentioned above. The docker image comes with two spotting modules which can be found in the /home directory. These are spotter_v2 and spotter_testr. 
