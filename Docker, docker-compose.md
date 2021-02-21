1. Compose file
```
# Version of dokcer-compose
version: '3'

# Containers we want created
services:
  # We want a container called redis using the redis image from docker hub
  redis-server:
    image: 'redis'
  # We want a container called fast-app using the docker file found in the same dir as this docker-compose file 
  fast-app:
    build: .  
    ports:
      - "80:80"
```
2. Command to run the compose file
```
docker-compose up --build
```
