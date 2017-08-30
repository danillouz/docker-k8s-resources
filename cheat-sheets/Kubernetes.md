# Kubernetes Commands
Cheatsheet of usefull `kubectl` commands to run on a Kubernetes cluster.

**Kubernetes v1.7.**

# Inspecting Resources

In order to display information of all resources or of a specific resource, execute the following.

```
kubectl get <resource>
```

 - `kubectl get pods` or `kubectl get po`
 - `kubectl get deployments` or `kubectl get deploy`
 - `kubectl get relplicasets` or `kubectl get rs`
 - `kubectl get services` or `kubectl get svc`
 - `kubectl get pods` or `kubectl get no`

With the `-o,--output` you can format the resource result, e.g.:
 - `kubectl get all -o name` to get all the resources names
 - `kubectl get all -o json` to get all the resources as json
 - `kubectl get all -o yaml` to get all the resources as yaml

To export the json or yaml output, of your cluster, to a file execute respectively:
 - `kubectl get all -o json > <filename>.json` or
 - `kubectl get all -o yaml > <filename>.yml`
