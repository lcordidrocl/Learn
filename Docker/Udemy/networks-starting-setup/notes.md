if we want tell docker which is the host ULR in which Docker container is currently running, we can use : 'host.docker.interal' instead of 'localhost'.
For exmaple, if we have a mongo server running locally and the container tries to connect.

If we have a mongo DB instance running in a conntainer, we need to inscpect the container and see which is it's local ip, so we can use that address in the app.js connect code

TO MAKE THIS EXAMPLE WORK ( manually copying the mongo db ip ):
-- have a mongo container running: docker run mongo --name mongodb
-- inspect it and copy it's network address: mongon inspect mongondb
-- use that url in the app.js, in the connect line.
-- run the built image for this folder

Netwroks:
we can specify the network that the container will run, and we can have many containers on the network so they can communicate with each other.
Networks are not automatically creted, we need to define them:
- dokcer network --help -> docker network create {networkName}
- docker network ls -> list networks

- After that we can do docker run -d --name mongodb --network {networkName} mongo
- We can now use the container name to make reference to its path, so we can update app.js from   'mongodb://172.17.0.2:27017/swfavorites', to   'mongodb://mongodb:27017/swfavorites', where mongodb is the mongo container name
- since we changed this code, we need to RE BUILD the IMAGE!!!
- we should now run the favorites app using the network: docker run --name favoritesapp --network {networkName} - d --rm -p 3000:3000 {favoritesImage}


How it Works:
Docker does not inspect source code, it intercepts REQUESTS and use a lookup to replace hosts with understood values, like like host.docker.internal or container images like mongondb

Default network pattern: bridge, there are more, can be specified when creating the network