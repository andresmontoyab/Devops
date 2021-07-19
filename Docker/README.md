# Docker Documentation.

# Index

* [Commands](#Commands)
* [Docker](#Docker)
	* [What is Docker](#What-is-Docker)
	* [Differences VM vs Docker](#Differences-VM-vs-Docker)
	* [Concepts Docker](#Concepts-Docker)
	* [Images](#Images)
	* [Volumes](#Volumes)
	* [Docker Hub](#Docker-Hub)
		* [Docker Push](#Docker-Push)
		* [Docker Search](#Docker-Search)
	* [Docker File](#Docker-File)
		* [Docker File Instructions](#Docker-File-Instructions)
	* [Docker Push](#Docker-Push)
	* [Docker Compose](#Docker-Compose)
		* [Some tags docker compose](#Some-tags-docker-compose)
	* [Docker Network](#Docker-Network)
	* [Docker Swarm](#Docker-Swarm)
* [Docker Editions](#Docker-Editions)
	* [Docker Enterprise Edition](#Docker-Enterprise-Edition)
	* [Docker Community Edition](#Docker-Community-Edition)
* [Examples](#Examples)

## Commands

<table>
<thead>
	<tr>
	<th>Commands</th>
	<th>Action</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>docker images</td>
		<td>List all the images.</td>
	</tr>
	<tr>
		<td>docker rmi <strong>image_name</strong></td>
		<td>Delete an image.</td>
	</tr>
	<tr>
		<td>docker run <strong>image_name</strong> </td>
		<td>Docker run is going to start a container</td>
	</tr>
	<tr>
		<td>docker run -d <strong>image_name</strong> </td>
		<td>Run the image withouth disabling the terminal</td>
	</tr>
	<tr>
		<td>docker run --name <strong>name</strong> <strong>image_name</strong></td>
		<td>Create a container with a specific name</td>
	</tr>
		<tr>
		<td>docker run -p 27017:27017 -d <strong>image_name</strong></td>
		<td>Exposse a container port in the port 27017</td>
	</tr>
	</tr>
	<tr>
		<td>docker run -it <strong>image_name</strong></td>
		<td>Iterative mode when create a container</td>
	</tr>
		<tr>
		<td>docker start <strong>image_name</strong> </strong></td>
		<td>Start a container that was previously created</td>
	</tr>
	<tr>
		<td>docker exec -it <strong>container_name</strong> bash </td>
		<td> Enter to iterative mode in a container already created.</td>
	</tr>
		<tr>
		<td> docker stop <strong>container_number</strong> </td>
		<td> Stop a container that is running</td>
	</tr>
	</tr>
		<tr>
		<td> docker rm <strong>container_number</strong> </td>
		<td> Delete the container, when you run docker ps -a the container shouldn't be there.</td>
	</tr>
	<tr>
		<td>docker ps</td>
		<td>Show the list of running containers</td>
	</tr>
	<tr>
		<td>docker ps -a</td>
		<td>Show the list of the container running or sttoped</td>
	</tr>
	<tr>
		<td>docker logs -f <strong>image_number</strong></td>
		<td>Show the container logs</td>
	</tr>
	<tr>
		<td>docker commit <strong>container_name</strong> <strong>name_new_image</strong></td>
		<td>Create an image in base on an existing container container</td>
	</tr>
	<tr>
		<td>docker pull <strong> image_name </strong> </td>
		<td>Download the information of the image without running</td>
	</tr>
	<tr>
		<td>docker login </td>
		<td>Login into docker</td>
	</tr>
	<tr>
		<td>docker login </td>
		<td>Login into docker</td>
	</tr>
	<tr>
		<td>docker push <strong>image_name></strong></td>
		<td>Publish a image in docker hub</td>
	</tr>
</tbody>
</table>

docker tag <current_name> <new_name> --> Change name Image

# Docker

## What is Docker

- Docker is an standar for linux containers.

- A container is a process or amount of process that run isolate wihtin linux.

- A container give us a private machine as space under linux OS.

- Virtual machine, everything running inside the VM is independent of the host operating system, or hypervisor

- Containers are going to run in every linux kernel- 

- Containers have their own space of process.

- Docker have their own network interfaces. 

- Run process as root.

- Has its own disk space. 

## VM vs Docker

- Docker containers and virtual machines are both ways of deploying applications inside environments that are isolated from the underlying hardware. 

- Virtual Machine is a Software that tried to emulate a OS.

- In Docker, the containers running share the host OS kernel.

- Containers are typically much smaller and faster, which makes them a much better fit for fast development cycles and microservices

![](https://github.com/andresmontoyab/Devops/tree/master/Docker/resources/containers-vs-virtual-machines.jpeg) 

## Docker Concepts

1. Docker Image --> Is a template, is the basis for the containers.

2. Docker Container --> Is an image running. 

3. Docker Engine --> Is the code that manage the Docker features. Create and run containers.

4. Docker file -> The images are created in bases of docker files, in these docker files are specific command to build the images.

## Images

1. Initially, we understood as Images the templates that are used to create containers.

2. Additionally it is also important to note that docker images are composed of layers, these layers are more specific elements to create the image, for example OS linux.

3. Each of these layers contains a unique identifier, each time we run an image the relevant information of each of those capable is searched locally, in case it is not found it will be downloaded.

4. The images that share layers will use the same information, that is to say if the information of a layer has already been downloaded, several layers can use it.


## Volumes

One thing with the containers is, when you turn off the container all the information is lost, the question is, If I have a DB container how can I preserve the information? The answer is Volumes.

Example:

```sh
docker run --name db -d -v C:\dir\mongodata:/data/db mongo
```

In the previous command we are running a mongo image, with name db, and map the volume to the folder mongodata.


## Docker Hub

In previous section we use commands as docker run mongo. This command download all the require information needed to run a mongo container. But from where is this information.?

All of this information comes from hub.docker.com or Docker Hub.

- Docker Hub is public repository in which we can find all the docker images.

If we want to upload a docker image we can use the command `docker push`

### Docker Search

If we want to check which images are available in docker hub from a specific technology we can use the command ```docker search```

```sh
docker search <name_image_to_search>
docker search ubuntu # Retrieve us all the ubuntu images available
```

### Docker Push

As we can download information from Docker Hub we can also publish our own images.

To do that we will perform the following steps.

```sh
docker login
docker push <image_name>
```

### Docker Pull

As we saw in previous section we can use the command `docker push` to upload new images to `docker hub` and also we can use the command `docker search` to search images in `docker hub`, but how to download the images? In order to download the images we can use the command `docker pull`

```sh
docker pull <image_name>
```

## Docker File

Dockerfile it is a text document that contains all the required commands to mount a sprecifc image

Let's see the next example

```docker
FROM node:7

WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app

CMD npm start

EXPOSE 3001
```

The above commands are a docker file, with those command we are telling to the docker engine the steps to create our image.

One important thing to highlight here is that every different step create a new layer.

After we create our docker file we can use the next command to create the expected image.

```sh
docker -t prueba .
```

In the previous command the -t mean the tag, so the tag for the new image will be "prueba" and also the "." tells to the docker engine where is the dockerfile base to build the image.

Finally we can run our new image.

```sh
docker run - d prueba
```

One important thing with docker is the use of cache, for example if we rebuild are previous image, we can notice that the build is going to take less time that the first execution, that is because a lot of information was cached.

Nevertheless if we made some changes and at least one layer detect that the cache is not goint to work for this update all the next layers can not use the cache too. For this reason all the pending layer need to run all again.

One posible solution to not reload all the layers is re order the instructions in order to only re load the necesary.

### Docker File Instructions

<table>
<thead>
	<tr>
	<th>Commands</th>
	<th>Action</th>
	<th>Example</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>FROM</td>
		<td>Initializes the <strong>Base Image</strong> for subsequent instructions</td>
		<td>FROM Ubuntu:16.04</td>
	</tr>
	<tr>
		<td>RUN</strong></td>
		<td>Runs command in the base image just before the creation</td>
		<td>RUN npm install</td>
	</tr>
	<tr>
		<td>COPY</td>
		<td>Copy information from the local host to the new image</td>
		<td>COPY . /app</td>
	</tr>
	<tr>
		<td>EXPOSE</td>
		<td>Expose a default port in the new image</td>
		<td>EXPOSE 3001</td>
	</tr>
		<tr>
		<td>WORKDIR</td>
		<td>Pending</td>
		<td>Pending</td>
	</tr>
		<tr>
		<td>CMD</td>
		<td>Pending</td>
		<td>Pending</td>
	</tr>

</tbody>
</table>




## Docker Compose	

1. Defining and running multi-container applications.

2. Configuration defines in one or more files.

		- docker-compose.yml(default)
		- docker-compose.override.yml(default)

3. Great for dev, staging and CI.

Let's say that we already create a image with the name dockerImage, if we want to run the image we can use a command like:

		docker run -d -p 8091-8093:8091-8093 11210:11210 dockerImage

If we execute this docker is going to run the container in base of this image.

Instead of running the above command we can put all of this configuration in a compose file.

		version: "2"
		services:
			db:
				image: dockerImage
				ports:
					- 8091:8091
					- 8092:8092
					- 8093:8093
					- 11210:11210

As you can notice the the structure of this file is YAML.

To run docker compose we use the next command 

		docker-compose up -d

Bring up the default developer environment.

## Some tags docker compose

1. image: -> Search the image name in the local repository or in docker.hub.

2. build: -> Build the image in base a dockerfile, to run this tag in require to send the lcoation of the dockerfile.

3. ports: set up the require port to run the application.

4. depends_on: Tells docker what the dependencies are.

5. environment: With this tag we can configure the environment variables require for the application.

## Overriden Docker Compose Files.

Let's say that we have two docker compose files

docker-compose.yml

		db:
			container_name: "db-dev"
			image: db
			ports:
				- ...
		web:
			image: web-app
			environment
				-URI=db-dev:8093
			ports:
				- 8080:8080	

production.yml

		db:
			container_name: "db-prod"
			image: db
			ports:
				- ...
		web:
			image: web-app
			environment
				-URI=db-prod:8093
			ports:
				- 8080:8080	

To run and override this configuration i can use the next command

		docker-compose up -f docker-compose.yml -f production.yml -d

## Docker Network

1. Create virtual Networks and attach contqainers.

2. Bridge network span single host.

3. Overlay network spans multiple host.

4. Work with Swarm and compose.

## Docker Swarm

1. Native clustering for Docker.

2. Provides a unified interface to a pool of Docker Hosts.

3. Fully integrated with machine and compose.

4. Serves the standard Docker API.

Sirve para describir la arquitectura de una app completa con todos sus servicios y segund para ejecutarlo

## Instalar Docker 

Para la instalacion de Docker bastará con descargar las fuentes proporcionadas en su pagina oficial, si usted posee un computador con
SO windows menor a a Windows 10 deberá utilizar Docker QuickTools.


# CLeaning Docker

En muchas ocasiones cuando utilizamos docker, nuestro volumenes, imagenes y contenedores antiguos persisten en nuestro sistema local ocupando un espacio, para esto es adecuado
utilizar una seria de passos en los cual podamos limpiar nuestro sistema local de la informacion que no se necesite.

	1. Kill all the running docker container

			docker kill $(docker ps -q)

	2. Kill all the stopped container

			dokcer rm $(docker ps -a -q)

	3. Remove a Specific Docker Image

			docker rmi <image name>

	4. Remove untagged imagens

			docker rmi $(docker images -q -f dangling=true)

	5. Delete All Images

			docker rmi $(dcoker images -q)

Una vez que un volumen no esta asociado a un contenedor, este es considerado un "Dangling".

	6. Remove all dangling volumes.

			docker volume rm $(docker volumes ls -f dangling=true -q)		

# Docker Editions

## Docker Enterprise Edition 

1. CaaS (Container As A Service).

2. Releases every three months.

3. Enterprise Support.

4. Certified Infrastructure

## Docker Community Edition

1. Free Docker edicion, for developers.

2. Releases "edge" every month with the latest features.

# Examples


## Running DB Images

docker run mongo --> La primera vez que lo tiremos, el sabrá que no habrá ninguna imagen mongo, por ende irá a docker hub y buscará una y la descargará.

Una vez tengamos nuestra DB arriba y podamos utilizarla y conectarnos surge la siguiente pregunta ¿La informacion que inserte en la DB persistirá?, y para responder esto dependerá como este configurado nuestro Docker File, existen Imagenes que tendrán la capacidad de almacenamiento y otras que no, las cuales en el instante que matemos nuestro contenedor se perderá la informacion.

Inicialmente hay que decir que una vez iniciamos nuestro contenedor, este creará una capa en la cual puede persistir informacion, solamente esta layer podrá escribir 

## Iniciar contenedor con asignacion de almacenamiento para BD

docker run -p 27017:27017 -v /users/jt/dockerdata/mongo:/data/db -d mongo

La instruccion anterior funciona particularmente para sistemas linux.

## Run RabbitMQ Container.

docker run -d --hostname guru-rabbit --name some-rabbit -p 8080:15672 -p 5671:5671 -p 5672:5672 rabbitmq:3-management

## Run MySql Container.

Correr MySql con las siguientes caracteristica, una variable de ambiente con la cual la contraseña por defecto de mysql pueda ser vacia y generar una asignacion de volumenes.

docker run --name guru-mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -v /Users/jt/tmp:/var/lib/mysql -p 3306:3306 -d mysql

## Inicializar una imagen centos y entrar a modo Iteractivo

	1. Utilizar una imagen centos 

			docker run -d centos tail -f /dev/null --> Iniciará una imagen centos en un contendor

	2. Ingresar a la termina del contenedor Centos.

			docker exec -it <name-container> bash --> it(iteractiva mode) 
