1. Create a new directory and within the directory create a html directory and an index.html file inside of the html directory.

2. In the new directory that containes the html directory, we will create a file called "dockerfile"
```
FROM httpd:alpine
COPY ./html/ /usr/local/apache2/htdocs/
```
3. Now we need to build the docker file
```
docker build -t hello-docker:1.0.0 .
```
4. Next create a run name for the container
```
docker run --name hello-docker-container -p 8080:80 hello-docker:1.0.0
```
5. You can now view your html files at localhost:8080
6. If you kill your docker container and want to rerun the container to bring up the application, run the command below.
```
docker start firstfourcharsofthecontainer id
```
7. If you do not know the container id, run command
```
docker ps -a
```
