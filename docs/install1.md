The stand-alone mapKurator-system requires that *cuda_11.3* with *cudnn* and *nvidia-smi* is working properly on the underlying host OS. For a successful installation, you may need to use *cuda_11.3-devel*. You can learn more [here](https://github.com/NVIDIA/nvidia-docker/wiki/CUDA).     
     
Note that *cuda_11.3* only provided support for *Ubuntu 20.04* and below at the time this document was created. 
If you face issues with the cuda installation, please consider using our [docker image](docs/install2.md) which is built on [nvidia/cuda:11.3.0-devel-ubuntu18.04](https://hub.docker.com/layers/nvidia/cuda/11.3.0-devel-ubuntu18.04/images/sha256-79ba930c17842750cd646dd9e78911199f48b7ea1f7ec378dbf90fdea1d95ba1?context=explore).

### Installing MapKurator on Ubuntu18.04 with cuda_11.3_devel 

#### Setup Anaconda 
Setup an anaconda environment by running the following commands.   
    
Download the latest anaconda setup -    
```wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh```       
You may replace the link above with the latest link from [anaconda](https://www.anaconda.com/products/distribution#Downloads).   
Run the installation file.   
```bash Anaconda3-2022.10-Linux-x86_64.sh```       
      
Create a conda environment to install all software packages required by mapKurator-system.    
```conda create --name mapKurator -y python=3.8```   
Activate the environment.       
```conda activate mapKurator```   

#### Install Required Libraries       
Install all python packages with the commands below.        
```python -m pip install numpy==1.21.6```    
```python -m pip install opencv-python==4.7```    
```python -m pip install pandas==1.4.3 ```    
```python -m pip install Pillow==9.4.0```     
```pip install Polygon3 ```   
```python -m pip install shapely==1.8.2```           
```python -m pip install geojson==2.5.0```       
```conda install pytorch==1.10.0 torchvision==0.11.0 torchaudio==0.10.0 cudatoolkit=11.3 -c pytorch -c conda-forge```     
Install gdal by following the instructions [here](https://mothergeo-py.readthedocs.io/en/latest/development/how-to/gdal-ubuntu-pkg.html) 

Please note that the mapKurator-system has been tested with the versions shown above only. If you test it on latest versions and find any issues, please let us know!       


