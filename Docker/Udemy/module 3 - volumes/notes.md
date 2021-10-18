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
