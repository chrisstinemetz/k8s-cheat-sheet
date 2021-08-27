# My Guide to Kubernetes

# Table of Contents <a name="toc"></a>

1. [Pods](#pod-section)
2. [ReplicaSets](#replicasets-section)

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

- get ReplicaSets

        kubectl get replicaset

- scale

       kubectl scale replicaset <replicaset name> --replicas=<num>
       kubectl scale deployment <deployment name> --replicas=<num>
       kubectl replace -f <replicaset-definition.yml>
