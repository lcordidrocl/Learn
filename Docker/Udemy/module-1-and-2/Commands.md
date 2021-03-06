Docker Commands

- docker build .
    it builds the dockerfile found on current directory
    this means that it creates an image based on the instructions on that file, it downloads dependencies and that stuff.
    After build that image will be ready to mount as a container. 

    build result: writing image sha256:7e416e5c9efeac81a62a895538e04bfecfccd57f7d5265559510407c999f8f91 -> The image Id that was succesfully created
- docker build --no-cache

- docker run {imageId} - It runs a container based on the given image Id. (the id given as the build result)
- docker run -p {hostPort}:{containerExposedPort} {imageId} - We define the mapping port (connect containerExposedPort in the container to the hostPort in the host)
    Since the container has an exposed port (3000) we need to tell the host system to map that port (in the container) to one on the host machine (otherwise, the port in the container is exposed (defined on the image) but not binded to any port) 
- docker start {dockerId/dockerName} -> it starts a previously executed container. Remember that docker run creates a new container, and docker start it starts one that was already created. It works like a restarting command. Good thing: we don't need to spcift ports again!
IMPORTANT: if we ran a container as --it, then when we want to start it it won't work unless we define the related flags. We need to specifiy the -a flagg (attached) and -i (interactive) : docker start -ai
- docker run is in attached mode by default, and start is detached. we can change this with running containers.

- docker ps -a- lists running containers
- docker stop {containerName} - stops the container
- docker run -it node -> pulls node image and runs a contatiner. -it tells docker to expose the interactive part (node command line )
- docker run --rm -> it removes the container once finished.
- docker rm {dockerName}-> removes NOT running containers from the daemon. we can remove many conntainers separating them by commasdocker

Images Commands:

COPY . . 
-> FIRST . indicates the path from where we will pick files (host)
-> SECOND . indicates the path to where we will copy all the files (container) (every container has a filesystem)

WORKDIR path
-> it tells docker where to execute the RUN commands
For exmaple, if we copy everything into /app (COPY . /app) we may then want to run NPM INSTALL in the /app path. So, Define workdir before we execute the command.
-> after MKDIR, the relative path in the docker image is pointint to that path. so copy . ./ would mean copy . /app after MKDIR was executed
-> CMD: it is a command that will be executed when the container is started, and not when the image is being built. The main difference with RUN is that one, RUN would be exceuted while building the image, CMD when running the container (CMD nod server.js, we want the server to start when the image is conteinerized)

-docker images -> list all images
-docker rmi {imageName/imageId} -> removes images, if they are not used by a container
- docker image prune -> removes all the images not used

# Docker Hub
- docker login
after that we can create a repository (docker hub)
rename an image with the name of the repository(docker tag oldname newname) ( a repository in the docker hub is actually an image)
we can the call:
-docker push {locaDockerImageNameThatMatchesRepositoryName}