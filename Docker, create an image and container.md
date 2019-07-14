1. Create a new directory, within that directory create an html directory and within the html directory create an index.html file. back in the main diorecotry not the "html" directory, we will create a dockerfile with no extension.
```
FROM httpd:alpine
COPY ./html/ /usr/local/apache2/htdocs/
```
2. Next run command 
```
docker build -t hello-docker:1.0.0 .
```
3. Name your container and start initial run
```
docker run --name hello-docker-container -p 8080:80 hello-docker:1.0.0
```
4. If you cancel and want to rerun, run 
```
docker start hello-docker-container
```
5. if yopu want to cancel, run
```
docker stop containerName^^
```
