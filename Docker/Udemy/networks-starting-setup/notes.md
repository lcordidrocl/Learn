if we want tell docker which is the host ULR in which Docker container is currently running, we can use : 'host.docker.interal' instead of 'localhost'.
For exmaple, if we have a mongo server running locally and the container tries to connect.

If we have a mongo DB instance running in a conntainer, we need to inscpect the container and see which is it's local ip, so we can use that address in the app.js connect code

TO MAKE THIS EXAMPLE WORK:
-- have a mongo container running: docker run mongo --name mongodb
-- inspect it and copy it's network address: mongon inspect mongondb
-- use that url in the app.js, in the connect line.
-- run the built image for this folder