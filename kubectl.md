# pod-section [Back to table of contents](./readme.md##table-of-contents)

- create pod

        kubectl run <pod name> --image=<image name>

  - create pod yaml file

          kubectl run <pod name> --image=<image name> --dry-run=client -o

- list pods

        kubectl get pods

  - list additional information _node_ info

          kubectl pods -o wide

- edit existing pod

        kubectl edit pod <podname>
