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