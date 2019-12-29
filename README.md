# demo-webapi-containerised using docker

Created a `docker file` to : 

- [x] Get `aspnet:3.0` & `dotnet/core/sdk:3.0`
- [x] `Build` and `publish` the project 
- [x] Copy required files to the image working directory `app`
- [x] Expose internal port to the container as `80`



## Build the docker image 
```
docker build -t demo-container . 
```

## Create Container using the image 


- [x]  Mapped internal port to the exteranl user of the container and disposing container.


```
docker run -it --rm -p 8080:80 demo-container 
```

- [x]  Always running the container without disposing it once closing the app.

```
docker run -d -p 8080:80 --name mywebapi demo-container
```

## Run the web api inside the container

```
docker exec -it mywebapi bash -c 'curl http://localhost:8080/weatherforecast’
```