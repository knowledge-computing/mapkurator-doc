<body>
<p align = "justify"> The mapKurator system now has its very own docker image which allows it to be used with the <a href="https://github.com/pelagios/recogito2">Recogito</a>, a software by Pelagios. To try it out, first pull the <a href="https://hub.docker.com/r/knowledgecomputing/mapkurator_recogito_2023/tags">docker image</a> with the following command -<br> </p> 

<code> docker pull knowledgecomputing/mapkurator_recogito_2023:latest </code>
 
<h3 id="environment-details">
 <a href="#/docs/install2?id=environment-details" data-id="environment-details" class="anchor">
  <span>Environment Details</span>
 </a>
</h3> 
 
<p align = "justify"> This container was created on a remote server with the underlying host OS as Ubuntu 20.04.5 LTS.<br>     
The setup instructions for section 1 have been thoroughly tested. If you opt for setup shown in section 2, there may be some issues which have not been tested.<br>
</p>
 
<h3 id="section1"> 
 <a href="#/docs/install2?id=section1" data-id="section1" class="anchor">
  <span>
   Section 1: Docker Container on a Remote Server 
  </span>
 </a>
</h3> 
 
<p align="justify"> To run the docker container on a remote server, and view the website for recogito on your local machine follow the steps below. For this you will require two terminals in which the docker container must be run. You  may choose to setup the <a href="https://code.visualstudio.com/docs/devcontainers/tutorial">dev container</a> for VSCode or proceed with simple commandline. If you wish to attach a container to VSCode, please refer to this <a href="https://code.visualstudio.com/docs/devcontainers/attach-container">link</a>.<br></p>     
<p align="justify"> The steps below assume that you are working with a simple bash terminal. The docker image requires two bash terminals to run the mapKurator-Recogito integrated system successfully. The first instance is required to run Postgres and Elasticsearch used by the Recogito software. The second instance is used to run the Recogito web application from where mapKurator may be accessed. In this tutorial, we will run the docker image on an Ubuntu server. The underlying host machine has Nvidia GPUs and Linux OS 20.04.5 LTS. We will use port forwarding between the docker container, the remote server and the local machine to view the Recogito web application on the local browser.<br></p>
You can follow the video tutorial below, and use the commands shown in this document.<br>
<a href="https://youtu.be/WYKBsvrISoE">Tutorial: mapKurator Recogito Docker Image Installation</a>
 
<h4> Step 1: Connect to Remote Server </h4> 
<p align="justify"> Connect to 2 bash terminals. One is used by step 4 and the other is used by step 5.<br>
<code> ssh USER@SERVER </code><br></p>               
<img src="_media/assets/install2/1_ssh.png" height=400 width=550 alt="SSH Example">
 
<h4> Step 2: Run New Docker Container </h4> 
<p align="justify"> If you are running the docker image for the first time, then you will need to run a new container. If you are re-running an already created container please skip to Step 3.<br>
Run the docker container with the command shown below.<br></p>
<div><code> docker run -it --name YOUR_CONTAINER_NAME --gpus all -p YOUR_PORT_ON_REMOTE_SERVER:YOUR_PORT_ON_DOCKER knowledgecomputing/mapkurator_recogito_2023 </code><br><br> </div>
<img src="_media/assets/install2/2_docker.png" height=400 width=550 alt="Docker Run Example"> 
 
<h4> Step 3: Run Existing Docker Container </h4>
<p align="justify"> If you are already inside your docker container after following step 2, please skip to step 4.<br>     
Otherwise, get the container id -> <code> docker ps </code><br></p>  
<img src="_media/assets/install2/4_dockerps.png" height=70 width=400 alt="Docker ps example">     
<p align="justify">Start the container -> <code> docker start -i CONTAINER_ID </code><br></p>
 
<h4> Step 4: Run Postgres and ElasticSearch in Docker Container </h4> 
<p align="justify"> As root user start postgres -> <code> service postgresql start </code><br>  
Switch user to elasticuser -> <code> sudo su elasticuser </code><br>  
Switch directory to elasticsearch -> <code> cd /home/elasticuser/elasticsearch-5.6.5/ </code><br>
Run elasticsearch -> <code> bin/elasticsearch </code><br><br> </p>
<img src="_media/assets/install2/3_dockerdbedit.png" height=200 width=600 alt="Elasticsearch and Postgres Example">    
        
<h4>Step 5: Execute Second Instance of Docker Container</h4>
<p align="justify"> Get the container id -> <code> docker ps </code><br>     
Execute container -> <code> docker exec -it <CONTAINER_ID> bash </code><br>       
Change directory to recogito2 -> <code> cd home/recogito2 </code><br>
Activate conda environment created for mapKurator-system -> <code> conda activate mapkurator </code><br>
Run the Recogito web-application -> <code> sbt "runProd -Dhttp.port=YOUR_PORT_ON_DOCKER" </code><br> </p>

<h4>Step 6: Forward Server Port to Localhost</h4>
<p align="justify"> To view the Recogito web-application do local port forwarding with ssh. This allows the localhost to access resources on remote server.<br> 
Open a new connection to the remote server using the following command.<br>    
 <code> ssh -L YOUR_PORT_ON_LOCAL:localhost:YOUR_PORT_ON_SERVER USER@SERVER </code><br> </p>
      
<p align="justify">You should be able to see the following page in the browser.<br></p>    
<img src="_media/assets/install2/homepage_.png" height=250 width=400 alt="Homepage"><br>      
<p align="justify">You can login with the test user with details as <b>username:</b> Test2, <b>password:</b> Test123 or create a new user as well.<br></p>
<img src="_media/assets/install2/6_login.png" height=250 width=400 alt="Loginpage"><br>     
<p align="justify">You will be redirected to the screen below.<br></p>
<img src="_media/assets/install2/7_exampleimgs.png" height=250 width=400 alt="User Homepage"><br>   
     
<h3 id="section2"> 
 <a href="#/docs/install2?id=section2" data-id="section2" class="anchor">
  <span>
   Section 2: Docker Container on Local Machine 
  </span>
 </a>
</h3> 
 
<p align="justify">If you want to run the docker container on your local machine, and view the recogito website on the local port of your choosing follow the steps below. Ensure that the local machine has a GPU setup that is compatible with cuda11.3.</p>
 
<h4> Linux OS </h4>
 <p align="justify">Run the docker container with the following command -<br>
<code> docker run -it --name YOUR_CONTAINER_NAME --gpus all -p YOUR_PORT_ON_LOCAL:YOUR_PORT_ON_DOCKER knowledgecomputing/mapkurator_recogito_2023 </code><br> 
Follow steps 1 through 2-4 in section 1. The website should be visible at - <code> localhost:YOUR_PORT_ON_LOCAL </code> <br></p>    
 
<h4> Windows OS </h4> 
<p align="justify">You may need to set GPUs to persistent mode. To learn more about setting up a windows machine for running docker please refer to this <a href="https://docs.docker.com/desktop/windows/wsl/">link</a>.</p>     
<p align="justify">Run the docker container with the following command -<br>
<code>docker run -it --name YOUR_CONTAINER_NAME --gpus all -p YOUR_PORT_ON_LOCAL:YOUR_PORT_ON_DOCKER knowledgecomputing/mapkurator_recogito_2023</code><br> 
Follow steps 1 through 2-4 in section 1. The website should be visible at - <code>localhost:YOUR_PORT_ON_LOCAL</code> <br></p>     

<p align="justify">You should be able to see the following page in the browser.<br></p>    
<img src="_media/assets/install2/homepage_.png" height=250 width=400 alt="Homepage"><br>      
<p align="justify">You can login with the test user with details as <b>username:</b> Test2, <b>password:</b> Test123 or create a new user as well.<br></p>
<img src="_media/assets/install2/6_login.png" height=250 width=400 alt="Loginpage"><br>     
<p align="justify">You will be redirected to the screen below.<br></p>
<img src="_media/assets/install2/7_exampleimgs.png" height=250 width=400 alt="User Homepage"><br>   

<h3 id="errors"> 
<a href="#/docs/install2?id=errors" data-id="errors" class="anchor">
 <span>
  Common Installation Errors
 </span>
</a>
</h3> 
 
<ol>
 <li> Check that you started the "mapkurator" conda environment with <code> conda activate mapkurator </code>
 <img src="_media/assets/mapkrec_how2/error1.png" height=250 width=400 alt="User Homepage"><br>   
 </li>
 <li> Check that your elastic search instance is running properly, go to Step 4 in Section 1.
 <img src="_media/assets/mapkrec_how2/error2.png" height=250 width=400 alt="User Homepage"><br>   
 </li>
 <li>Check that you are in the recogito2 directory before running the sbt command. 
 <img src="_media/assets/mapkrec_how2/error3.png" height=250 width=400 alt="User Homepage"><br> 
 </li>
 
 </ol>
</body>
