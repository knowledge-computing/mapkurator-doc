Mapkurator now has its very own docker image, which allows it to be used with the [Recogito](https://github.com/pelagios/recogito2) software by Pelagios. 
To do so, first pull the [docker image](https://hub.docker.com/r/knowledgecomputing/mapkurator_recogito_2023/tags) with the following command - 

`docker pull knowledgecomputing/mapkurator_recogito_2023:latest`

Run the following command to start the docker container.

```docker run -it --name <REPLACE_WITH_YOUR_NAME> --gpus all -p 9900:9900 knowledgecomputing/mapkurator_recogito_2023```

Incase you want to change the port please run –

```docker run -it --name <REPLACE_WITH_YOUR_NAME> --gpus all -p <YOUR_PORT_ON_DOCKER>:<YOUR_PORT_ON_LOCAL> knowledgecomputing/mapkurator_recogito_2023```

Ensure that you see the following list of folders in the home directory.
Good job!
To start recogito, you need to run the following commands in one terminal –
Open a terminal
 
As root user - 
service postgresql start
Switch user to -
sudo su elasticuser
cd /home/elasticuser/elasticsearch-5.6.5/
bin/elasticsearch
 
Open new terminal
docker exec -it <container_id> bash
cd home/recogito2
conda activate mapkurator
sbt "runProd -Dhttp.port=9990"
 
You should be able to see the following page in the browser when you go to –
If you want to learn more about how this image was created, please follow the guide at.

How to Use Mapkurator : 
There are three types of data you can feed into recogito to run with  mapkurator.

File Upload - test if jp2 image works. 
WMTS
IIIF

To run the sample files go to - 
You can replace the spotter by editing the file Mapkurator.scala 
If you want to unit test the mapkurator script, you can refer to the test commands in - 
Common Errors and how to fix them - 

 

