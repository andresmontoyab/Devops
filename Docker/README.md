# Docker

## Comandos

docker ps -a --> Muestra contenedores locales.

docker ps --> Muestra imagenes corriendo

docker run -d image --> Corre un contedor sin deshabilitar la terminal

docker stop numberImage --> Detiene un contenedor que este corriendo

docker run -p 27017:27017 -d image --> Expone el contenedor por el puerto 27017

docker start <image_name> --> Inicial una imagen que previamente fue inicializada.

docker logs -f numberImage --> Muestra los logs de un contenedor


## ¿What is Docker?

1. Docker es un estandar para contenedores Linux.

2. Un contenedor es runtime aislado dentro de linux.

3. Un contenedor brinda una maquina privada como espacio bajo linux.

4. Contenedores correran bajo cualquier Kernel de linux moderno.

5. Tiene su propio espacio de procesos.

6. Sus propias interfaces de red.

7. Corre procesos como root.

8. Tiene su propio espacio de disco (Puede compartirlo con host)

## ¿ Diferencia VM vs Docker?

## Terminologia Docker

1. Docker Image --> Es una representacion de un contenedor Docker. Como un Jar o War File en Java.

2. Docker Container --> El estandar de runtime de Docker. Efectivamente una imagen docker desplegada y corriendo. Como un Spring Boot ejecutable JAR.

3. Docker Engine --> Codigo que gestiona las "cosas" de Docker. Crea y corre Contenedores Docker.

# Docker Editions

## Docker Enterprise Edition 

1. CaaS (Container As A Service).

2. Releases Trimestrales.

3. Soporte clase empresarial.

4. Infraestructura certificada

## Docker Community Edition

1. Free Docker edicion, para desarrolladores y operaciones.

2. Releases "edge" cada mes con las ultimas caracteristicas para desarrolladores.

3. Releases trimestrales para operaciones.

## Instalar Docker 

Para la instalacion de Docker bastará con descargar las fuentes proporcionadas en su pagina oficial, si usted posee un computador con
SO windows menor a a Windows 10 deberá utilizar Docker QuickTools.

## Docker File 

Docker File es un concepto supremamente en docker, con base en estos serán creadas las Docker Images

## Docker Images

Como ya se ha mencionado con anterioridad, las Docker Image se crean por medio de Docker Files, a su ves las Docker Images estan compuesta por un conjunto de Layers con un identificador unico, esas layers se crean con base a el Docker File, segun los comandos de ejecucion que hayan en este.

Es importante anotar que cada una de las Layers con las cuales esta compuesta una Docker Image tiene un Id Hash, si en nuestro repositorio local tenemos dos imagenes y estas dos imagenes comparten Layers es decir utilizan las mismas "funcionalidades" entonces docker solo deberá descargar solo una vez estas funcionalidades y ambas imagenes la utilizaran. Esto resulta ser un metodo muy eficiente de compartir contenedores y imagenes corriendo en el mismo host.


## Docker Hub

1. Es un repositorio publico en el cual se encuentran Imagenes Docker las cuales podremos descargar, para descargar la imagen se utilizará una busqueda por convencion de nombres o URL

## Running DB Images

docker run mongo --> La primera vez que lo tiremos, el sabrá que no habrá ninguna imagen mongo, por ende irá a docker hub y buscará una y la descargará.

Una vez tengamos nuestra DB arriba y podamos utilizarla y conectarnos surge la siguiente pregunta ¿La informacion que inserte en la DB persistirá?, y para responder esto dependerá como este configurado nuestro Docker File, existen Imagenes que tendrán la capacidad de almacenamiento y otras que no, las cuales en el instante que matemos nuestro contenedor se perderá la informacion.

Inicialmente hay que decir que una vez iniciamos nuestro contenedor, este creará una capa en la cual puede persistir informacion, solamente esta layer podrá escribir 

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

## Temas Docker

1. Environment Variables

2. Mapping Ports

3. Mapping Storage

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



## Construir una imagen docker con base en un docker file.

	1. docker build -t spring-boot-docker .

	Este comando buscará en el directorio donde nos encontremos parados el dockerFile existente y ejecutará los comandos que en estes se indique y si todo ejecuta adecuadamente nuestra imagen será creada con el nombre que se le asigno, para nuestro caso es spring-boot-docker.

	2. Para verificar que nuestra imagen este corriendo adecuadametne lanzaremos el siguiente comando.
		
		docker run -d -p 8080:8080 spring-boot-docker

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

3. Is an alternative for Kubernetes.

## Kubernetes

1. People often compare Docker with kubernates, that is not a fair comparison because docker is a container technology, docker has multiples products multiples offering. What is a fear comparison is Docker Swarm with Kubernetes.

2. Kubernetes is allow to run containers and nowaway the main container technoly is docker, kubernet can not survive without docker.

3. Povides an Orchestration framework on top of docker.

4. Provide declarative primitives for the "desired state"

		4.1 Self Healing
		4.2 Auto Restaring
		4.3 Replicating

## Concepts.

1. PODS: Collocated group of Docker containers that share an IP and Storage colume.

2. Service : Single, stable name for a set of pods also acts as LB.

	2.1 Abstract a set of pods as a single IP and port
	2.2 Creates environment varibles in other pods.
	2.3 Stable endpoint for pods to reference.

3. Label: used to organize and group of objects.

4. Replication Controller: manages the lifecycle of pods and ensures specified number are running.

5. Basically allow you yo communicate among differents nodes.

## Components

1. Node: Docker host running kubelet(node agent) and proxy services.
	- Monitored by systemd or monit.

2. Master: hots cluster-level control services, including the API server, scheduler and controller manager.

3. etcd: Distributed key-value store used to persist kubernetes system state. 

## Kubectl

1. Controls the kubernetes cluster manager.

2. kubetctl get pods or minions

3. kubectl create -f <filename>

4. kubectl update or delete

5. kubectl resize -replicas=3 replicationcontrollers <name>


## Source Information

https://github.com/arun-gupta/docker-java


72d1b7ecf715
0604e5a5fc63
50b3666b33ef


