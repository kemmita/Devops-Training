1. Compose file
```
version: "3.8"
services:
  <!-- This Service will be pulled from docker hub    -->
  mongodb:
    image: 'mongo'
    environment:
      - MONGO_INITDB_ROOT_USERNAME=russ
      - MONGO_INITDB_ROOT_PASSWORD=secret
    volumes:
      - data:/data/db  
 <!--  This service will come from a customer dockerfile we  define found in a dir called backend     -->
  backend:
    build: ./backend
    ports:
      - '80:80'
    depends_on:
      - mongodb
    environment:
      - MONGO_INITDB_ROOT_USERNAME=russ
      - MONGO_INITDB_ROOT_PASSWORD=secret  
    volumes:
      - logs:/app/logs  
      - ./backend:/app
      - /app/node_modules  
  frontend:
    build: ./frontend
    ports:
      - '3000:3000'
    depends_on:
      - backend
    volumes:
      - ./frontend:/app  

volumes:
  data:
  logs:

      - "80:80"
```
2. Command to run the compose file
```
docker-compose up --build
```
