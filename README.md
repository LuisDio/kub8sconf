### Main object type

| Object type  | Functions |
| ------------- | ------------- |
| Pods  | Runs one or more closely related container  |
| Services  | Sets up networking in a kubernetes cluster  |
| Deployment  | Maintains a set of identical pods(pod template), ensuring they have the correct config and the right number exists  |
| Secrets  | Securely stores a piece of information in the cluster, such as a database password  |

As for Service Object, there exists 4 subtype such as:<br/>

| Object type  | Functions |
| ------------- | ------------- |
| ClusterIP  | Expose a set of pods to other objects in the cluster  |
| NodePort  | exposes a set of pods to the outside world(only good for dev purpose)  |
| LoadBalancer  | Legacy way of getting network traffic into a cluster  |
| Ingress  | Exposes a set of services to the outside world  |


```
kubectl apply -f <filename> --> feed a config file to kubectl to create a new object/ update desire state
```
```
kubectl apply -f <folder> --> apply confi to a group of file within a folder
kubectl apply -f k8s
```

```
kubectl get <object-type> --> print the status of an entire group of object example pods
```

```
minikube ip --> List the IP of the cluster node
```

2 type of deployments:<br/><br/>
-- Imperative deployments ==> DO exactly these steps to arrive at this container setup <br/>
-- Declarative deployments ==> Our container setup should look like this, make it happen <br/>

With a Declarative approach you simply need to edit your config file and pass it to the master<br/>

When you need to update a state to a certain pod, just give it the same config file with the modified parameter.<br/>
However the name and the type or kind must not be changed for the master to bring changes to the assigned pod or object

```
kubectl describe <object type> <object name> --> Get detailed info about an object
```

```
kubectl delete -f <confi-file>  --> remove a created running object
kubectl delete <object-type> <object-name>
kubectl delete deployment client-deployment
```

```
kubectl get pods -o wide --> Give a wider range of information such as pods running and their respective internal IP
```

Get our deployment to recreate our pods with latest version of multi-client docker<br/>

If no changes were found within our config file, it would not apply.<br/>
In the case of our docker pull the latest image, it would not apply change since there was not actionable changes<br/><br/>

### Possible solution:

| Solution 1: Deleting pods(very bad)  | Solution 2: Adds an extra step in the production deployment process(painful every single time) | Solution 3: Use an imperative command(feasible and ok) |
| ------------- | ------------- |------------- |
| Manually delete pods to get the deployment to recreate them with the latest version  | Tag built image with a real version number and specify that version in the config file  | Use an Imperative command to update the image version the deployment should |

```
solution 3

kubectl set image <object-type> / <object-name> <container-name> = <new image to use> --> Imperative command to update the image
kubectl set image deployment/client-deployment client=multi-client:v1
```

### Reconfiguring local Docker CLI to talk to different docker-server
```
minikube docker-env --> give list of config
eval $(minikube docker-env) --> This only reconfigure your current terminal window(temporally)
```

| Why changing server  |
| ------------- |
| Use all the same debugging techniques we can do with docker CLI  |
| Manually kill the container to test kubernetes ability to self-heal |
| Delete cached image in the nodes |

Note you can also use the same docker CLI command with kubectl
```
kubectl get pods --> give the info such as name
kubectl logs <image-name>
kubectl exec -it <image-name>
```

```
kubectl get pv --> list persistent volume 
kubectl get pvc --> list persistent volume claim created(advertisement)
```

# kub8sconf
