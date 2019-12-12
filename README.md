```
kubectl apply -f <filename> --> feed a config file to kubectl to create a new object/ update desire state
```

```
kubectl get <object-type> --> print the status of an entire group of object example pods
```

```
minikube ip --> List the IP of the cluster node
```

2 type of deployments:<br/>
-- Imperative deployments ==> DO exactly these steps to arrive at this container setup <br/>
-- Declarative deployments ==> Our container setup should look like this, make it happen <br/>

With a Declarative approach you simply need to edit your config file and pass it to the master<br/>

When you need to update a state to a certain pod, just give it the same config file with the modified parameter.<br/>
However the name and the type or kind must not be changed for the master to bring changes to the assigned pod or object
# kub8sconf
