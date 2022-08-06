
# Cgroups

> https://dockerlabs.collabnix.com/advanced/security/cgroups/
# Starting


// to run docker without sudo create the group 'docker' and add you 'user' to it like so
	# groupadd docker
	# usermod [user] -a -G docker


# Creating
*Note that "Containers" are an instance of an "Image/Blueprint"

// search for images with
	# docker search [related_term]
	*Note that [related_term] doesn't have to be [container_name] but any [term] related to it
	*You can alse use the docker hub web site to search

// to download a docker image "blueprint" form docker hub use
	# docker pull [image_name]
	you can pull different version of an image using ':' after the name
	# docker pull [image_name]:[version]

// listing all docker images "blueprints" in the system
	# docker images
	or
	# docker image ls

// check if docker is running correctly with
	# docker run hello-world

// create a container with
	# docker run [container_name] [command_in_container]

// open interactive shell inside container with
	# docker run -it [container_name] sh ; or use if exists bash,zsh...


# Building_Images

// to build an image you need a "Dockerfile"
	example :

		FROM python:3

		# set a directory for the app
		WORKDIR /usr/src/app

		# copy all the files to the container
		COPY . .

		# install dependencies
		RUN pip install --no-cache-dir -r requirements.txt

		# tell the port number the container should expose
		EXPOSE 5000

		# run the command
		CMD ["python", "./app.py"]

// building using 'docker build'
	# docker build -t [[your_dockerhub_nam]/[container_name_youwant]] [/path/to/Dockerfile] or . "for current dir"



# Networking

// Creating a subnet
	# docker network --subnet "192.168.1.0/24" [net_name]

// Static address for container in subnet and hostname
	#docker run --net [net_name] --ip [ip] --hostname [hostname]

// running container in detached mode with '-d' and exposing its ports to random ports on the host with '-P'
	# docker run -d -P --name [custom_name_for_container] [container_image]

// you can also chose ports you want with '-p' instead of '-P'
	# docker run -p [host_port]:[container_port] --name [custom_name_for_container] [container_image]

// check port mapping
	#docker port [custom_container_name]/[token]



# Status

// check for conatiners
	# docker ps ; for running ones
	# docker ps -a ; for all of them



# Cleaning

// stop containers with
	# docker stop [custom_container_name]/[token]

// delete container right after exiting it
	# docker run --rm [container_name] [command_in_container] ; you can use -it with --rm

// delete exited containers with
	# docker rm $(docker -a -q -f status=exited)
	# docker container prune ; exactly the same as befor but easier
	# docker rmi ; for deleting ones that are no running

	or copy container token from 'docker ps -a' and past it after 'rm'
	# docker rm [token]

