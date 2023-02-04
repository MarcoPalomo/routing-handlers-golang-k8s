#Routing handlers golang k8s

### What it does ?

`app`uses gorilla mux library for routing. Get your /health and /readiness endpoints apart from the '/' endpoint.

## RUN

You will need a minikube (or kind, microk8s...) to deploy your app locally. Using minikube, you can do :

```bash
$ minikube start
```

Deployment will be made applying the manifest with kubectl.

```bash
$ kubectl apply -f manifests/deploy.yaml
  deployment.apps/go-hello-world created
```

Done! You can get the deployments like this:

```bash
$ kubectl get deployments
  NAME             READY   UP-TO-DATE   AVAILABLE   AGE
  go-hello-world   3/3     3            3           25s
```

Pods are allocated a private IP address by default and cannot be reached outside of the cluster. You can use the kubectl port-forward command to map a local port to a port inside the pod like this:

```bash
$ kubectl port-forward go-hello-world-69b45499fb-7fh87 8080:8080
  Forwarding from 127.0.0.1:8080 -> 8080 
  Forwarding from [::1]:8080 -> 8080 
```

...And interact with the Pod on the forwarded port:

```bash
$ curl localhost:8080
  Hello, Guest
  
 $ curl localhost:8080?name=Marco
 Hello, Marco
```
