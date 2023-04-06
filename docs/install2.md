Mapkurator now has its very own docker image! It can be used with the [Recogito](https://github.com/pelagios/recogito2) software by Pelagios.     
To do so, first pull the [docker image](https://hub.docker.com/r/knowledgecomputing/mapkurator_recogito_2023/tags) with the following command -     

`docker pull knowledgecomputing/mapkurator_recogito_2023:latest`    
 
### Environment Details :     
This container was created on a remote server with the underlying host OS as Ubuntu 20.04.5 LTS.     
The setup instructions for section 1 have been thoroughly tested. If you opt for setup shown in section 2, there may be some issues which have not been tested, due to lack of gpu resources on local machine for testing.    

### Section 1: Run docker image on a remote server -    
If you want to run the docker container on a remote server, but view the website for recogito on your local machine follow the steps below -    
 
For this you will require two terminals in which the docker container must be run. You  may choose to setup the [dev container](https://code.visualstudio.com/docs/devcontainers/tutorial) for VSCode or proceed with simple commandline. If you wish to attach a container to VSCode, please refer to this [link](https://code.visualstudio.com/docs/devcontainers/attach-container).       
The steps below assume that you are working with a simple bash terminal.    
The docker image requires two bash terminals to run the mapKurator-Recogito Integrated system successfully. The first instance is required to run Postgres and Elasticsearch used by the Recogito software. The second instance is used to run the recogito web application. In this tutorial, we will run the docker image on an Ubuntu server. The underlying host machine has GPU support and Linux OS <add version>. We will use port forwarding between the docker container, the remote server and the local machine to view the Recogito web-application on the local browser. If you are using a windows machine as the localhost, a git bash terminal or VSCode installation may be required, or the use of Windows WSL. The assumption is that a bash terminal is available at your disposal.    
#### Step 1: Connect to Remote Server   
```ssh <USER>@<SERVER>```     
#### Step 2: Run New Docker Container     
 If you are running the docker image for the first time, then you will need to run a new container. If you are re-running an already created container please skip to Step 3.    
```docker run -it --name <REPLACE_WITH_YOUR_NAME> --gpus all -p <YOUR_PORT_ON_REMOTE_SERVER>:<YOUR_PORT_ON_DOCKER> knowledgecomputing/mapkurator_recogito_2023```     
 
#### Step 3: Run Existing Docker Container 
 If you are already inside your docker container after following step 2, please skip to step 4.     
 ```docker ps```
 ```docker start -i <CONTAINER_ID>```
#### Step 4: Run Postgres and ElasticSearch in Docker Container 
Ensure that you see the following list of folders in the home directory. <INSERT Directory Image>    
As root user run the command -> ```service postgresql start```    
Switch user to elasticuser with command -> ```sudo su elasticuser```    
Run elastic search.      
 ```cd /home/elasticuser/elasticsearch-5.6.5/```     
```bin/elasticsearch```     
Expected output <INSERT Image>
#### Step 5: Execute Second Instance of Docker Container
```docker exec -it <CONTAINER_ID> bash```       
Activate conda environment created for mapKurator-system and run the Recogito web-application.    
```conda activate mapkurator```  
```cd home/recogito2```  
```sbt "runProd -Dhttp.port=9990"```  
Expected output - <INSERT Image>  
#### Step 6: Forward Server Port to Localhost 
To view the Recogito web-application do local port forwarding with ssh. This allows the localhost to access resources on remote server. 
Open a new connection to the remote server using the following command. 
```ssh -L 9800:localhost:9803 tanisha@cs-u-sansa.cs.umn.edu```
You should be able to see the following page in the browser. 
<ADD IMAGE>

### Section 2: Local instance of docker image     
If you are planning to run the docker image on your local machine, then you should be able to view the recogito website on the local port of your choosing.     
Set GPUs to persistent mode. To learn more about setting up a windows machine for running docker please refer to this [link](https://docs.docker.com/desktop/windows/wsl/).     

Run the docker container with the following command -      
```docker run -it --name <REPLACE_WITH_YOUR_NAME> --gpus all -p <YOUR_PORT_ON_LOCAL>:<YOUR_PORT_ON_DOCKER> knowledgecomputing/mapkurator_recogito_2023```   
The website should be visible at - localhost:\<YOUR_PORT_ON_LOCAL\>     

You should be able to see the following page in the browser. 
<ADD IMAGE>

 If you want to learn more about how this image was created, please follow the guide at.  

 #### Common Errors During Installation
