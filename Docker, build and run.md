1. First you will need to make your changes to your application.
2. Go into the cmnd line and run the command below
```
docker stop containerName
```
3. Update your image
```
docker build -t hello-docker:1.0.1 .
```
4. Name the container
```
docker run --name hello-docker-container-threev2 -p 8080:80 hello-docker:1.0.1
```
