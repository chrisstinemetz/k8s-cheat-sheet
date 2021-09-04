# My Guide to Kubernetes

# Table of Contents <a name="toc"></a>

1. [Pods](#pod-section)
2. [ReplicaSets](#replicasets-section)
3. [Deployment](#deployment-section)
4. [Tips and Tricks](#tips-tricks-section)

## Pod Section <a name="pod-section"></a>

[Back to table of contents](#toc)

- pod definition file

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx
```

- create pod

        kubectl run <pod name> --image=<image name>

  - create pod yaml file

          kubectl run <pod name> --image=<image name> --dry-run=client -o

- list pods

        kubectl get pods

- pod description

        kubectl describe pod <pod name>

  - list additional information _node_ info

          kubectl pods -o wides

- edit existing pod

        kubectl edit pod <podname>

## ReplicaSets Section <a name="replicasets-section"></a>

[Back to table of contents](#toc)

- ReplicaSet definition file

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```

- create ReplicaSet

        kubectl create -f <replicaset-definition.yml>

- delete ReplicaSet

        kubectl delete replicasets.apps <replicaset name>

- edit ReplicaSet

        kubectl edit replicasets.apps <replicaset name>

- get ReplicaSets

        kubectl get replicaset

- get information

        kubectl describe replicasets.apps <replicaset name>
        kubectl describe pod <replicaset name>

- scale

       kubectl scale replicaset <replicaset name> --replicas=<num>
       kubectl scale deployment <deployment name> --replicas=<num>
       kubectl replace -f <replicaset-definition.yml>

## Deployment Section <a name="deployment-section"></a>

[Back to table of contents](#toc)

- Deployment definition file

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
  replicas: 3
  selector:
    matchLabels:
```

- create Deployment

        kubectl create -f <deployment-definition.yml>

- list deployment

        kubectl get deployments

## Tips and Tricks Section <a name="tips-tricks-section"></a>

[Back to table of contents](#toc)

- commands

  - list all objects

        kubectl get all

Here's a tip!

As you might have seen already, it is a bit difficult to create and edit YAML files. Especially in the CLI. During the exam, you might find it difficult to copy and paste YAML files from browser to terminal.
Using the `kubectl run` command can help in generating a YAML template. And sometimes, you can even get away with just the `kubectl run` command without having to create a YAML file at all. For example, if you were asked to create a pod or deployment with specific name and image you can simply run the `kubectl run` command.

Use the below set of commands and try the previous practice tests again, but this time try to use the below commands instead of YAML files. Try to use these as much as you can going forward in all exercises
Reference [Bookmark this page for exam. It will be very handy](https://kubernetes.io/docs/reference/kubectl/conventions/)

### Create an NGINX Pod

        kubectl run nginx --image=nginx

### Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)

        kubectl run nginx --image=nginx --dry-run=client -o yaml

### Create a deployment

        kubectl create deployment --image=nginx nginx

### Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)

        kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

### Generate Deployment YAML file (-o yaml). Don't create it(--dry-run) with 4 Replicas (--replicas=4)

        kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

### Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.

        kubectl create -f nginx-deployment.yaml

### In k8s version 1.19+, we can specify the --replicas option to create a deployment with 4 replicas.

        kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
