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
		* [Docker Compose environment file](#Docker-compose-environment-file)
		* [Docker Compose Profiles](#Docker-Compose-Profiles)
		* [Some tags docker compose](#Some-tags-docker-compose)
		
		* [Docker](#Docker)
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
		<td>docker start <strong>image_name</strong> </strong></td>
		<td>Start a container that was previously created</td>
	</tr>
	<tr>
		<td>docker run -it <strong>image_name</strong></td>
		<td>Creates a container in Iterative mode</td>
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
		<td>docker container ls</td>
		<td>Show the list of running containers</td>
	</tr>
		</tr>
		<tr>
		<td>docker container ls -a</td>
		<td>Show the list of the container running or sttoped</td>
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
		<td>docker logs -f <strong>container_name</strong></td>
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
		<td>docker push <strong>image_name></strong></td>
		<td>Publish a image in docker hub</td>
	</tr>
	<tr>
		<td>docker container top <strong>container_name</strong></td>
		<td>Show what are the process that container is running</td>
	</tr>
	<tr>
		<td>docker container inspect <strong>container_name</strong></td>
		<td>Returns a json with all the container information</td>
	</tr>
	<tr>
		<td>docker container inspect --format '{{ .NetworkSettings.IPAddress }}' <strong>container_name</strong></td>
		<td>Returns specific container information</td>
	</tr>
	<tr>
		<td>docker container stats </td>
		<td>Returns information about the CPU use of each contianer</td>
	</tr>
	<tr>
		<td>docker <strong>image_name</storng> history </td>
		<td>Show layers of changes made in image</td>
	</tr>
	<tr>
		<td>docker image build -t<strong>tag_name</storng> <strong>path_docker_file</strong> </td>
		<td>Build an image in base of a docker file</td>
	</tr>
	<tr>
		<td>docker image prune</td>
		<td>Clean up just dangling images</td>
	</tr>
	<tr>
		<td>docker system prune</td>
		<td>Clean up Everything</td>
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

- Containers are not mini VMs

- Containers are just processes

- Docker containers and virtual machines are both ways of deploying applications inside environments that are isolated from the underlying hardware. 

- Virtual Machine is a Software that tried to emulate a OS.

- In Docker, the containers running share the host OS kernel.

- Containers are typically much smaller and faster, which makes them a much better fit for fast development cycles and microservices

![](https://github.com/andresmontoyab/Devops/blob/master/docker/resources/containers-vs-virtual-machines.jpeg)


## Docker Concepts

1. Docker Image --> Is a template, is the basis for the containers.

2. Docker Container --> Is an image running. 

3. Docker Engine --> Is the code that manage the Docker features. Create and run containers.

4. Docker file -> The images are created in bases of docker files, in these docker files are specific command to build the images.

## Images

- App binaries and dependencies
- Metadata about the image data and how to run the image
- An image is an ordered collection of root filesystem changes and the corresponding execution parameters for use within a container runtime
- An image is the application we want to run.


## Containers

- A container is an instance of that image running as a process.

### How docker creates a container

- Looks for that image locally in image cache. If does not find any image then looks in remote image repository.

- Download the latest versions

- Create new container based on that image and prepares to start.

- Gives a virtual IP on a private network inside docker engine.

- Opens up port on host and forwards to container port 

- We can hace many containers running off the same image

## Images

An image is the application we want to run.

1. Initially, we understood as Images the templates that are used to create containers.

2. Additionally it is also important to note that docker images are composed of layers, these layers are more specific elements to create the image, for example OS linux.

3. Each of these layers contains a unique identifier, each time we run an image the relevant information of each of those capable is searched locally, in case it is not found it will be downloaded.

4. The images that share layers will use the same information, that is to say if the information of a layer has already been downloaded, several layers can use it.


## Persistent Data

- Containers are usually immutable and ephemeral
- "Immutable Infrastructure": Only re deploy containers, never change.
- But what about databases or unique data?
- Docker gives us feature to ensure these "separation of concerns"
- This is known as "Persistent Data"

Docker has two options for containers to store files in the host machine, so that the files are persisted even after the container stops: volumes, and bind mounts.

### Volumnes

Volumes are stored in a part of the host filesystem which is managed by Docker (/var/lib/docker/volumes/ on Linux). Non-Docker processes should not modify this part of the filesystem. Volumes are the best way to persist data in Docker.

- Created and managed by Docker
- A given volume can be mounted into multiple containers simultaneously
-  When no running container is using a volume, the volume is still available to Docker and is not removed automatically. You can remove unused volumes using docker volume prune
- Volumes are the preferred way to persist data in Docker containers and services
- Volumes are easier to back up or migrate than bind mounts.
- Volumes work on both Linux and Windows containers

### Bind Mounts

Bind mounts may be stored anywhere on the host system. They may even be important system files or directories. Non-Docker processes on the Docker host or a Docker container can modify them at any time.

- Available since the early days of Docker
- When you use a bind mount, a file or directory on the host machine is mounted into a container
- The file or directory is referenced by its full path on the host machine.
- f you are developing new Docker applications, consider using named volumes instead
- Bind Mounts basically are a mapping of host files or directories to a container files or directories
- Basically just two colications poiting to the same file.

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

It is very important the order of our instrucctions, docker is going to use cache if the docker file has the same instruction, but if one instruction changes, that instruction and the next ones can not be cached.

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

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

- Compose works in all environments: production, staging, development, testing, as well as CI workflows.

Using Compose is basically a three-step process:

1. Define your app’s environment with a Dockerfile so it can be reproduced anywhere.
2. Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.
3. Run ```docker compose``` up and the Docker compose command starts and runs your entire app

The next snipped is a ```docker-compose``` example:

```yml
version: "3.9"  # optional since v1.27.0
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

### Starting docker compose

In order to run our docker compose we can run the next commands

```sh
docker-compose up 
docker-compose up -d # The -d runs the services in the background
```

### Stopping docker compose

In order to stop our docker compose we can run the next command

```sh
docker-compose down # Is going to stop and remove all the containers
docker-compose down --volumes # Is going to stop and remove, all the containers and volumes
```

### Docker Compose environment file

There are multiple parts of Compose that deal with environment variables in one sense or another

It’s possible to use environment variables in your shell to populate values inside a Compose file:

Let's see the next example.

We have the next ```docker-compose``` file with:

```yml
version: '3'
services:
  web:
    image: "webapp:${TAG}"
```

We want to make this `docker-compose` a little bit more dynamic, for that reason we use the `TAG` variable!

The question is, Where is the `TAG` value? The answer could be in the `.env` file.

the `.env` for this `docker-compose` should look like.

```sh
TAG=v2.0
```

If we put both concepts in mind this is what is going to happend.

1. We run the `docker-compose up` command to start up our application
2. When `docker-compose` is setting up everything, the process found a variable called `TAG`.
3. `docker-compose` search for the `TAG` key in our `.env` file and finally assigned the value.


Keep in mind that the `.env` file should be placed in the same project directory.

### Docker Compose Profiles

Profiles allow adjusting the Compose application model for various usages and environments by selectively enabling services

 If unassigned, the service is always started but if assigned, it is only started if the profile is activated.

 In order to enable one profile we need supply the `--profile`

 ```sh
 docker-compose --profile profile_name up
 ```

 Let's see one `docker-compose` example with profiles

 ```yml
version: "3.9"
services:
  frontend:
    image: frontend
    profiles: ["frontend"]

  phpmyadmin:
    image: phpmyadmin
    depends_on:
      - db
    profiles:
      - debug

  backend:
    image: backend

  db:
    image: mysql
 ```

Lets do quick review about what is happening in the above `docer-compose`

- The `frontend` service has set the `frontend` profile
- The `phpmyadmin` service has set the `debug` profile
- The `backend` service does not has any profile.
- The `db` service does not has any profile.

 Now let see how the profiles works

 ```sh
docker-compose --profile debug up # Start db, backend and frontend
docker-compose --profile frontend up # Start db, backend and phpmyadmin
 ```



2. Configuration defines in one or more files.

		- docker-compose.yml(default)
		- docker-compose.override.yml(default)

### Some tags docker compose

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

Each container connected to a private virtual network "bridge"

Each virtual network routes through NAT firewall on host IP

All containers on a virtual network can talk to each other without -p

### Network Commands

<table>
<thead>
	<tr>
	<th>Commands</th>
	<th>Action</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>docker network ls</td>
		<td>Show networks</td>
	</tr>
	<tr>
		<td>docker network inspect <strong>network_name</strong></td>
		<td>Inspect a network</td>
	</tr>
	<tr>
		<td>docker network create --driver <strong>network_name</strong></td>
		<td>Create a network</td>
	</tr>
		<tr>
		<td> docker container run -d --network my_app_net <strong>image_name</strong></td>
		<td>Create a container with an attach it to a network</td>
	</tr>
	<tr>
		<td>docker network connect <string>network_id</strong> <string>container name</strong></td>
		<td>Attach a network to container</td>
	</tr>
	<tr>
		<td>docker network disconnect <string>network_id</strong> <string>container name</strong></td>
		<td>Detach a network from a container</td>
	</tr>
</tbody>
</table>

### Docker Network: DNS 

Docker daemon has a built in DNS server that containers use by default

- Understand how DNS is the key to easy inter-container comms.
- See how it works by default with custom networks
- Leran how to use --link to enable DNS on default bridge network

### Network Drivers

- Bridge: Default docker virtual network.
- Host: It gains performance by skipping virtual networks but sacrifices security of container model
- None: Removes eth0 and only leaves you with localhost interface in container


1. Create virtual Networks and attach containers.

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
