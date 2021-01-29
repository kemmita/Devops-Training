1. Create mysql container, -d is for detach so it will not run in our current terminial.
```
docker container run -d -p 3306:3306 -name db -e MYSQL_RANDON_ROOT_PASSWORD=yes mysql
```
2. Apache container. "8080:80" means that 8080 will run off our host machines 80 port
```
docker container run -d --name apache_server -p 8080:80 httpd
```
3. ngnix
```
docker container run --name ng -d -p 80:80 nginx
```
