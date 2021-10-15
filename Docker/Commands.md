- docker build .
    it builds the dockerfile found on current directory
    this means that it creates an image based on the instructions on that file, it downloads dependencies and that stuff.
    After build that image will be ready to mount as a container. 

    build result: writing image sha256:7e416e5c9efeac81a62a895538e04bfecfccd57f7d5265559510407c999f8f91 -> The image Id that was succesfully created
- docker build --no-cache

- docker run {imageId} - It runs a container based on the given image Id. (the id given as the build result)
- docker run -p 3000:3000 {imageId} - We define the mapping port (connect 3000 in the container to the 3000 in the host)
    Since the container has an exposed port (3000) we need to tell the host system to map that port (in the container) to one on the host machine (otherwise, the port in the container is exposed (defined on the image) but not binded to any port) 
    
- docker ps - lists running containers
- docker stop {containerName} - stops the container