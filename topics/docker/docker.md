
* Platform for building , running and shipping applications 
* The code runs on my machine problem : reasons 
  * Config files may be different on env
  * Some version of software may be different 
  * Some files may be missing in the env 
* With docker we package our application with everything it needs and run 
* Each application in docker runs with all its dependencies 
* Container : isolated env for running an application 
  * Shares same OS
  * Lightweight
  * Quick to start
  * Need less hardware resource
  * All containers share the Kernel of the host
* Virtual Machines : Like two or more machines running in a single machine
  * Hypervisor helps to do that , ex : VMWare
  * Each VM needs a full blown OS
  * Slow to start coz OS has to be loaded 
  * Takes some slice of hardware : cpu , memory , disk space 
  * Memory divided b/w VMs

## Docker Architecture 

* Client - Server model 
* Server is Docker engine 
* Uses Request - Response model to communicate via REST API
* Containers are process 
* On Linux and Windows Kernel is there 
* On Mac , kernel doesn't have support for containers
* So in Mac , containers are run on top of linux VM (Linux VM is created and then container is run)

## Development

* We create an application 
* We create a docker file 
* This docker file is used by docker to create an image 
* Image has everything needed for an application to run 
  * OS
  * application files
  * run time env
  * third party libs 
  * env variables
* We provide the image to docker which runs it inside a container(as a process)
* We can push this image to registry(docker-hub) and use it in any computer(like pushing files to github)
