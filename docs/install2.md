Mapkurator now has its very own docker image! It can be used with the [Recogito](https://github.com/pelagios/recogito2) software by Pelagios. 
To do so, first pull the [docker image](https://hub.docker.com/r/knowledgecomputing/mapkurator_recogito_2023/tags) with the following command - 

`docker pull knowledgecomputing/mapkurator_recogito_2023:latest`

### Environment Details : 
This container was created on a remote server with the underlying host OS as Ubuntu 20.04.5 LTS.
The setup instructions for section 1 have been thoroughly tested. If you opt for setup shown in section 2, there may be some issues which have not been tested, due to lack of gpu resources on local machine for testing. 

Run the following command to start the docker container.

```docker run -it --name <REPLACE_WITH_YOUR_NAME> --gpus all -p 9900:9900 knowledgecomputing/mapkurator_recogito_2023```  

### Section 1: Remote instance of docker image on a server - 
If you want to run the docker container on a remote server, but view the website for recogito on your local machine follow the steps below - 

For this you will require two terminals in which the docker container must be run. You  may choose to setup the [dev container](https://code.visualstudio.com/docs/devcontainers/tutorial) for VSCode or proceed with simple commandline. If you wish to attach a container to VSCode, please refer to this [link](https://code.visualstudio.com/docs/devcontainers/attach-container)   
The steps below assume that you are working with a simple bash terminal. 
#### Step 1:   
#### Step 2:   
#### Step 3:   

```docker run -it --name <REPLACE_WITH_YOUR_NAME> --gpus all -p <YOUR_PORT_ON_LOCAL>:<YOUR_PORT_ON_DOCKER> knowledgecomputing/mapkurator_recogito_2023```   

### Section 2: Local instance of docker image –
If you are planning to run the docker image on your local machine, then you should be able to view the recogito website on the local port of your choosing. 
Run the docker container with the following command -    
```docker run -it --name <REPLACE_WITH_YOUR_NAME> --gpus all -p <YOUR_PORT_ON_LOCAL>:<YOUR_PORT_ON_DOCKER> knowledgecomputing/mapkurator_recogito_2023```   
The website should be visible at - [localhost:<YOUR_PORT_ON_LOCAL>](localhost:<YOUR_PORT_ON_LOCAL>)   


Forward the port form server to local   
ssh -L 9980:localhost:9980 tanisha@cs-u-sansa.cs.umn.edu  

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

 

