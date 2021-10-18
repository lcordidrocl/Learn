docker run -i f1e52bb4ee56

-i : interactive, since we expect inputs from command line, we need to tell docker to allow this feature. By default input is not available, executing just run throws error.
docker run -t: creates a terminal in the container. We can use this combined with -i, we can do docker run -i -t, or alltoghether, docker run -it

if want to restart the container:
docker start -a - i {containerName}
Remember that start by default is detached, so attached is needed for console, and -i for interactive and input working fine.