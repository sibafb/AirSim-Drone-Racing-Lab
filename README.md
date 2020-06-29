# AirSim Drone Racing Lab 


## Quickstart
- [Website](https://microsoft.github.io/AirSim-Drone-Racing-Lab/)
- [Linux and Windows Binaries](https://github.com/microsoft/AirSim-Drone-Racing-Lab/releases)
- [Python API Doc](https://microsoft.github.io/AirSim-Drone-Racing-Lab/api.html), [airsimdroneracinglab PyPI package](https://pypi.org/project/airsimdroneracinglab/)

<img src="https://github.com/madratman/airsim_neurips_gifs/blob/master/imgs/neurips_b99_3_drones.gif?raw=true" width="275"> <img src="https://github.com/madratman/airsim_neurips_gifs/blob/master/imgs/neurips_soccer_field_8_drones.gif?raw=true" width="275"> <img src="https://github.com/madratman/airsim_neurips_gifs/blob/master/imgs/neurips_zhangjiajie_4_drones.gif?raw=true" width="275">

### Using AirSim Drone Racing Lab Binaries
#### Downloading
- Linux
	- Use the [download_linux_binaries.sh](download_linux_binaries.sh) script
    - Python client:   
        `pip install airsimdroneracinglab`
	
- Windows 

#### Running
- Linux
	- Running in windowed mode:
		```
		./ADRL/ADRL.sh -windowed
		```
	- Running headless (with rendering of images enabled):
		```
		DISPLAY= ./ADRL/ADRL.sh
		```
	- To disable rendering completely for training planning and / or control policies, you can use:
		```
		./ADRL/ADRL.sh -nullrhi
		```
		Note that `simGetImages` will not work with this option. 
	- To increase speed of `simGetImages` / increase speed of Unreal Engine's game thread;
		- Add the `"ViewMode": "NoDisplay"` to your settings.json file, or use [this file](https://gist.github.com/madratman/5fadbb08f65e9c0187ccc1f5090fc086) directly.   
		This disables rendering in the main viewport camera.   
		Then run the binary with the following options.  
		```
		./AirSimDroneRacingLab.sh -windowed -NoVSync -BENCHMARK
		```
		You can also use the Unreal console commands `Stat FPS`, `Stat UnitGraph`, `r.VSync`, `t.maxFPS`. See [Issue #111](https://github.com/microsoft/AirSim-Drone-Racing-Lab/issues/111) for more details. 

- Windows
	- Navigate to the `ADRL/` directory, and double-click `run.bat` (or `ADRL.exe -windowed`)

## Using Docker
- Prerequisites:
	- Install [docker-ce](https://docs.docker.com/install/linux/docker-ce/ubuntu/). 
	- Complete the desired [post-installation steps for linux](https://docs.docker.com/install/linux/linux-postinstall/) after installing docker.    
	At the minimum, the page tells you how torun docker without root, and other useful setup options. 
	- Install [nvidia-docker2](https://github.com/NVIDIA/nvidia-docker/wiki/Installation-(version-2.0)). 

- Dockerfile:   
	We provide a sample [dockerfile](docker/Dockerfile) you can modify.   
	It downloads the training and qualification binaries automatically, and installs the python client.   
	By default, it uses Ubuntu 18.04 and CUDA 10.0 with OpenGL, and is build on top of [nvidia/cudagl:10.0-devel-ubuntu18.04](https://hub.docker.com/r/nvidia/cudagl).    
	This can be changed of course, as explained in the following section. 

- Building the docker image:    
	You can use [build_docker_image.py](docker/build_docker_image.py) to build the dockerfile above (or your own custom one)    
	**Usage** (with default arguments)
	```shell
	cd docker/;
	python3 build_docker_image.py \
		--dockerfile Dockerfile \
		--base_image nvidia/cudagl:10.0-devel-ubuntu18.04 \
		-- target_image airsim_neurips:10.0-devel-ubuntu18.04
	```
- Running the docker image:
	See [docker/run_docker_image.sh](docker/run_docker_image.sh) to run the docker image:   
	**Usage**
	- for running default image, training binaries, in windowed mode:    
	    `$ ./run_docker_image.sh "" training` 
	- for running default image, training binaries, in headless mode:    
	    `$ ./run_docker_image.sh "" training headless`
	- for running a custom image in windowed mode, pass in you image name and tag:    
	    `$ ./run_docker_image.sh DOCKER_IMAGE_NAME:TAG`
	- for running a custom image in headless mode, pass in you image name and tag, followed by "headless":    
	     `$ ./run_docker_image.sh DOCKER_IMAGE_NAME:TAG headless`

## AirSim Drone Racing Lab Features and API
- The API is documented at [airsimdroneracinglab API doc](https://microsoft.github.io/AirSim-Drone-Racing-Lab/api.html)
    
## Questions
Please open a Github Issue on **this** repository (not [AirSim](https://github.com/microsoft/AirSim)) for any technical questions associated with AirSim Drone Racing Lab. 
