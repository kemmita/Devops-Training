1. Creat docker file like so
```
# Define base image
FROM node

# copy all files and dirs in path of Dockerfile on local machine to the container in a dir specified as app
COPY . /app

# Specify the dir that all commands below should be executed in
WORKDIR /app

# Run the necessary commands in
RUN npm install

# Run command after container is created
CMD ["node", "server.js"]
```

##RUN COMMANDS ON TERMINAL
2. build the new Image from the docker file above. It will spit out an id we will need below
```
docker build .
```

3. Now create a new container using the newly created image
```
docker run -p 80:80 <image id from above output> 
```
