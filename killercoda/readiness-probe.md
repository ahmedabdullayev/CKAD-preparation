### Question

#### Link: https://killercoda.com/killer-shell-ckad/scenario/readiness-probe

Create a Deployment with a ReadinessProbe
A ReadinessProbe will be executed periodically all the time, not just during start or until a Pod is ready
Create a Deployment named space-alien-welcome-message-generator of image httpd:alpine with one replica.

It should've a ReadinessProbe which executes the command stat /tmp/ready . This means once the file exists the Pod should be ready.

The initialDelaySeconds should be 10 and periodSeconds should be 5 .

Create the Deployment and observe that the Pod won't get ready.

### Solution

1. Create deployment file

```
k create deployment space-alien-welcome-message-generator --image=httpd:alpine --replicas=1 -o=yaml --dry-run=client > deployment.yaml
```

2. Add readiness probe

```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: space-alien-welcome-message-generator
  name: space-alien-welcome-message-generator
spec:
  replicas: 1
  selector:
    matchLabels:
      app: space-alien-welcome-message-generator
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: space-alien-welcome-message-generator
    spec:
      containers:
      - image: httpd:alpine
        name: httpd
        readinessProbe:
          exec:
            command: ['sh', '-c', 'stat /tmp/ready']
          initialDelaySeconds: 10
          periodSeconds: 5
status: {}
```

3. Create file inside a pod

```
k exec space-alien-welcome-message-generator-668c949c77-qf5fn -- touch /tmp/ready
```