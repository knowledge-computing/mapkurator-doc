The stand-alone mapkurator-system requires that *cuda_11.3* with *cudnn* and *nvidia-smi* is working properly on the underlying host OS.    
For a successful installation, you may need to use *cuda_11.3-devel*. You can learn more [here](https://github.com/NVIDIA/nvidia-docker/wiki/CUDA).  
Note that *cuda_11.3* only provided support for *Ubuntu 20.04* and below at the time this document was created. 
If you face issues with the cuda installation, please consider using our [docker image](install2.md) which is built on [nvidia/cuda:11.3.0-devel-ubuntu18.04](https://hub.docker.com/layers/nvidia/cuda/11.3.0-devel-ubuntu18.04/images/sha256-79ba930c17842750cd646dd9e78911199f48b7ea1f7ec378dbf90fdea1d95ba1?context=explore).

If you wish to create a docker container with just mapkurator-system, please refer to section......
