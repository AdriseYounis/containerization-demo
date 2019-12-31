# Aspnetcore 3.0 web api containerized and orchestrated by kubernetes

The `docker file` in this repository : 

- [x] Gets `aspnet:3.0` & `dotnet/core/sdk:3.0`
- [x] `Builds` and `publishes` the project 
- [x] Copies the required files to the image working directory `app`
- [x] Exposes internal port to the container as `80`

## Create a docker Image
```
docker build -t demo-container . 
```

## Create docker container


- [x]  Maps port exposed in the docker file to port 8080 in order to access the api through the container
  
- [x] Removes the containers once it is stopped

```
docker run -it --rm -p 8080:80 --name containerName demo-container 
```

- [x]  Keep the container running without shutting it down

```
docker run -d -p 8080:80 --name containerName demo-container
```

## Runing app inside the `container`

```
docker exec -it containerName bash -c 'curl http://localhost:8080/weatherforecast’
```

# Orchestrating containerized web api by kubernetes

The `deployment.yaml file ` in this repository : 

- [x] Creates the `pod` , `container` and locates the `image`
- [x] Maps the `port` for the `container` to 80 

The `service.yaml file ` in this repository : 

- [x] Allows access to the pod for the client to access the api
- [x] Maps `port : 8080` to the internal `container port: 80`

## Check for available `pods`

- [x]  A group of one or more containers deployed to a single node
```
kubectl get po
```

## Create `pod` for the container 

- [x]  The container will be running in the `pod`

```
kubectl apply -f ./deployment.yaml 
```
- [x]  The app should be running and waiting to listen via a port 

```
kubectl logs -f demo-aspnetcore-deployment-54978666d5-l4kq5
```

## Create a `service` which will : 

- [x]  Allow `access` to the `pod`
- [x]  `Load balance` the requests coming into the pod

## To run the `service.yaml` file run 

```
kubectl apply -f ./deployment.yaml 
```
## See that your `service` has :

- [x]  Type as `LoadBalancer`
- [x]  External-IP `localhost`
- [x]  Port is mapped to `8080`

```
kubectl get services
```
## Run the api

- [x]  Should output the data from the get endpoint

```
http://localhost:8080/WeatherForecast
```

## `Scale` the app from 1 to 5 

- [x]  5 instances of the app should be running

```
kubectl scale --replicas=5 deployment/demo-aspnetcore-deployment
```
# Useful kubectl commands 

## Get `Nodes / Clusters`

```
kubectl get nodes
```
## Delete `Pods / Deployment`

```
kubectl delete -f ./deployment.yaml 
```

## Investigate why a `POD` is `not running`

```
kubectl describe pods <POD-ID>
```
- [x]  View all pods and compare 

```
kubectl describe pods
```

## View `POD` logs

```
kubectl logs -f <POD-ID>
```

