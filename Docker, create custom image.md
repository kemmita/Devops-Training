1. Creat docker file like so
```
# Specify base image
FROM alpine

# Download dependincies
RUN apk add --update redis

# Run command
CMD ["redis-server"]
```

##RUN COMMANDS ON TERMINAL
2. build the new Image from the docker file above. It will spit out an id we will need below
```
docker build .
```

3. Now create a new container using the newly created image
```
docker run <image id from above output>
```
