# cors-ambassador-test

Steps to reproduce
1. You should be connected to any available kubernetes cluster. I am using minikube for the test purposes(minikube start).
2. Create dev namespace `kubectl create namespace dev`
3. Apply the k8s configuration (`kubectl apply -f {project_home}/deploy/dev.yaml`)
4. Wait for it to start and be ready. (`kubectl get pods -ndev`)
5. Get cluster ip and port to use in the request `kubectl cluster-info` for ip and `kubectl get services -ndev|grep "ambassador "` for port
6. Execute OPTION request `curl -X OPTIONS http://192.168.99.108:32063/api/service/hello -v`
7. Read the response
```curl -X OPTIONS http://192.168.99.108:32063/api/service/hello -v
*   Trying 192.168.99.108:32063...
* TCP_NODELAY set
* Connected to 192.168.99.108 (192.168.99.108) port 32063 (#0)
> OPTIONS /api/service/hello HTTP/1.1
> Host: 192.168.99.108:32063
> User-Agent: curl/7.66.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< allow: GET,HEAD,OPTIONS
< content-length: 0
< date: Thu, 17 Oct 2019 16:51:17 GMT
< x-envoy-upstream-service-time: 1
< server: envoy
< 
* Connection #0 to host 192.168.99.108 left intact
```
Expected to see cors headers like access-control-allow-origin and others.
