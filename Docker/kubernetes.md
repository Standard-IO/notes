# Kubernetes

Is service for orchestration to the containers developed for Google and give to Cloud Native society.

What can do?

* Service discovery and load balancing
* Storage orchestration
  * Local or cloud based
* Automated rollouts and rollbacks
* self healing
* Secret and configuration management
* Use the same API across on-promise and every cloud providers

What can't do?

* Does not deploy source code
* Does not build your application
* Does not provide application-level services
  * messages buses, databases, caches, etc.


## Kuberntes context

The context  is the cluster where all the comamnd will be apply to. Is like a configuration in the CLI this configuration helps us to avoid to write the namespace every time we type a command. We can set the namespace and then just use that context. [namespace](#name-spaces)


* `kubectl config current-context` get the current context
* `kubectl config get-contexts` List all context
* `kubectl config use-context [contextName]` Set the current context
* `kubectl config delete-context [contextName]` Delete a context from the config file

## Kuberntes deploy

There are many ways to deploy a container. But mainly there are two ways declarativea and imperative. Imperative is the classic way with code and declarative is through the yaml file.

**Imperative way**

```bash
kubectl create deployment mynginx1 --image=nginx
```

**Declarative**

```bash
kubectl create -f deploy-example.yaml
```

**Clean deployment**

```bash
kubectl delete deployment mynginx1
kubectl delete deploy myginx2
```

## Name spaces

This allows to you to group resources under a name space like production, dev, etc.
Kubernetes has a default name space is "default". When you erase a name space is erased all the child with it.

* `kubetct get namespaces` list all the namespaces
* `kubetct get ns` shortcut
* `kubetct config set-context --current --namespace=[nameSpaceName]` set the current context to use a namespace
* `kubetct create ns [nameSpaceName]` Create a namespace
* `kubetct delete ns [nameSpaceName]` Delete a namespace
* `kubetct get pods --all-namespaces` List all pods in all namespaces


## pods

The pods are part important the pods are virtual machinees, not containers. When you scale containers are not scale out intead are the scale out the pods in the node. 

* `kubectl create -f [pod-definition.yml]` create a pod
* `kubectl run [podname] --image=busybox -- /bin/sh -c "sleep 3600"` Run a pod
* `kubectl get pods` list the running pods
* `kubectl get pods -o wide` same but with more info
* `kubectl describe pod [podname]` show pod info
* `kubectl get pod [podname] -o yaml > file.yaml` Extract the pod definition in yaml and save it to a file
* `kubectl exec -it [podname] -- sh` interative pod
* `kubectl delete  -it [podname] -- sh` interactive mode
* `kubectl delete pod [podname]` Same using the pod's name
* `kubectl 
* `kubectl 
* `kubectl 
* `kubectl 