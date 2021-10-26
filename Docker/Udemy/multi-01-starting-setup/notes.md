In this excercise we will have 3 containers
- one for the Mongo DB 
- one for the node.js API
- one for the client-side React SPA

Requriments:
MongoDB: 
- data must persist if the image is removed
- Access should be limited ( user name and password )

Node.js API:
- data must persists (logs)
- Live source code Update

React SPA
- Live source code Update

Implementation notes:
we can use a named volume for the logs, and for the DB
we can use a bind mount for the live source update -> this requires installing the "re-start server when file changes occur js" library, and update the npm start command on the js apps.


Commands:

### Baisic initial conteneraized apps ( db - back - ui ) - after building respectively each image
- docker run --name mongodb -p 27017:27017 -d --rm mongo 
- docker run --name goals-backend --rm goals-node -> after building the backend image with host.docker.internal ( we are not publishin ports, just getting sure it works)
- docker run --name goals-backend --rm -d -p 8080:80 goals-node  ->once we verified it connects with DB we then run it publishing the ports
- docker run --name goals-frontend --rm -d -it -p 3000:3000 goals-react -> runs UI -> we need --it flag, because if not, docker closes its

-- since we can't run backend on default port 80 (console errors), we manually modified front URLS to force consuming port 8080. after rebuilding the front image, we could succesfully wired up the 3 containers. 
-- This is really dependent on each container. Improve using networks.