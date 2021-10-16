Images: Definition, set of instrucctions and command to be exceuted in order to set up the environment and run any app
Container: Actual implementation and execution of an Image. Is the Running instance of an image

We write Shareable Images, we can then have many containers based on the same image.
The image define the commands, is the container the one that executes them.

Code Update -> It doesn't update the image! if we want to run a container with the source code updated we need to RE-BUILD the dockerfile Image !
After BUILD images are locked and are not modified from outside. NEED TO REBUILD to REFRESH, like when doing the COPY 


Layer Based Architecture: each dockerfile command is a LAYER
CACHE:
Docker store the result of each layer and when building again, it infers if the layer (or INSTRUCTION) will generate a different result or not. If it is the same result, it does not execute the command (I guess it hashes the result somehow?)
If one layer changes, all the following images will be re-executed.
-> Design the layers taking this in count, add not expected changing layers at the beggining when possible (like copy package.json and run npm install)

A container adds a Read/Write Layer, the ultimate layer, that becomes active when we run the image and has the running app.
