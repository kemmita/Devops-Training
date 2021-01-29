0. List containers
```
docker ps -a
```
1. Run the command below to remove a docker container. Without powershell, we can only delete one at a time.
```
docker rm containerid
```
2. We can delete all container at once with powershell
```
docker rm $(docker ps -a -q)
```
3. To delete one image, run the command below
``` 
docker rmi 0ba3d13d991e
```
4. To remove all on poweshell run
```
docker rmi $(docker images -q)
```
