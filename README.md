# Docker image to run the Coastal and Regional Ocean COmmunity model - CROCO

NOTE: this project is in very early stages of development.  

## Pre-requisites

- Install docker in your system. Some guidelines [here](https://docs.docker.com/engine/installation/).
- Create a Dockerhub account [here](https://hub.docker.com/).
- Pull the CROCO docker image:
```
docker pull andressepulveda/croco_oceanv1.2.1a
```

## Getting started 

- Clone this GitHub repository at your preferred location, let's call it `$HOME` hereinafter.

- Create a folder `/data/roms/upwelling` to store the output data outside the docker container. Make sure there are compatible ownerships and writting permissions between host OS and docker container. 

- Browse to `$HOME` and run:

```
docker run -it andressepulveda/croco_oceanv1.2.1a bash
```

- Done, you're inside the docker container now. Let's run the Benguela test case. 
```
cd /home/croco/croco-v1.2.1/Benguela/CROCO_FILES
wget http://mosa.dgeo.udec.cl/CROCO2022/CursoBasico/Tutorial01/ArchivosIniciales/croco_grd.nc
wget http://mosa.dgeo.udec.cl/CROCO2022/CursoBasico/Tutorial01/ArchivosIniciales/croco_frc.nc
wget http://mosa.dgeo.udec.cl/CROCO2022/CursoBasico/Tutorial01/ArchivosIniciales/croco_clm.nc
wget http://mosa.dgeo.udec.cl/CROCO2022/CursoBasico/Tutorial01/ArchivosIniciales/croco_ini.nc
cd ..
./jobcomp
./croco croco.in
```

## Build your own ROMS executable

- Create the folder `/source/roms/include` and `/source/roms/bin`, and make sure there are compatible ownerships and writting permissions between host OS and docker container.
- Place your `myapp.h` CPP definitions file and any other necessary header file there. 
- Use docker-compose to trigger the build:

```
docker-compose run -e roms_app=MYAPP build
```

- If everything goes well, you should have the binary file `MYAPP` created. To be continued...

## Building your own docker image

If you are familiar with docker, you may want to use a different ROMS version, or customise the Dockerfile, and build your own image. You're more than welcome to fork this repository and share your image with the community. 

- For your ROMS login credentials, set `roms_username` and `roms_password` as ENV variables in your system. The `docker-compose.yml` and `Dockerfile` files will pipe them through when checking out the ROMS source code. 

```
docker-compose build
```

To test your image, you can use the `test` tag in the docker-compose file, writting your specific test and:

```
docker-compose run test
```

## User application

- step 1
- step 2

Please report any bugs [here](https://github.com/metocean/docker-roms-public/issues).
