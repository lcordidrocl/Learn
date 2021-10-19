We can define containers as one layer more added to the image, with write/read permissions over the filesystem natively defined for the image.
If we stop and start a container, that file system isn't erased so if we had files the container will still have those files after restarting.
But, if we remove de container from docker, and we then run a new container based on the same initial image, that container will be empty.
And that makes sense because that is what docker is about, independent containers. The newly container will have a fresh new filesystem, with empty files.

Take also mind that, updating the image and rebulding will demand to run a new fresh container, so this is a common scenario

How do we persist data even if we remove containers ? VOLUMES

VOLUMES: folders in the host machine that are mapped into the containers, and made available to them

We can define a volume in the image doing VOLUME["pathInTheContainerWeWantToPersist"] 
IT IS IMPORTANT to remark that we are specifying a path in the CONTAINER FILESYSTEM.

so If we defined the root as WORKDIR /app, we should do something like VOLUME ["/app/feedback"]

Types of Volumes: anonymus and named

a Volume defined in the Docker Image Layer, which corresponds to the container file path, is mapped to a folder in the host, managed by docker, which we don't know

Named Volumes persist after the container is removed.

Commnands:
-docker volumnes ls
- docker run --rm -p 3000:80 --name -v feedback:app/feedback feedbackapp feedbackappi -> we define the named volumen when running the container, so, this volume is not "binded to a particular container through the image definition", like it happens with anonymus volumes


Bind Mounts: 
* manually managed containers, we tell docker where to create the volume, so if we specify the path where we have all the files, then updating the files will achieve real-time app update, which is needed for development.
We define the bind mount when running a container, using the -v for a second time (the first one tells docker that we are going to use a named volume, and it won't be deleted when removing the container, the second one tells it where to create it and it defines the binded mount)
* since we spceify with the second volume to copy everything from the abs defined path to a given container file path (/app), the result is that we overwrite everything in the container files, and we erase in that process the node_modules folders created when running npm install. 
	Fix: create an annonymus container for node modules, so docker saves that folder locally (don't know where). When the binded mount volume tries to copy everything and overwrite the container filesystem, it will find a container for a longer path (bindmount: /app, ann volumne: app/node_modules), and it will skipp that folder. This way we grant 2 things:
	* Data Persistence
	* Code refresh instantly (can update code in real time, with the container running)
	
shortcut:
-v "%cd%":/app -> when defining the bind mount we need to define the absolute path of the folder where we want to place the volume. This is a shortcut so we don't write the full pathx