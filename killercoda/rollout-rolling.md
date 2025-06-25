### Question

Application "wonderful" is running in default Namespace.

You can call the app using curl wonderful:30080 .

The app has a Deployment with image httpd:alpine , but should be switched over to nginx:alpine .

Set the maxSurge to 50% and the maxUnavailable to 0% . Then perform a rolling update.

Wait till the rolling update has succeeded.


### Solution

1. update to this:

```
rollingUpdate:
    maxSurge: 50%
    maxUnavailable: 0%
type: RollingUpdate
template:
metadata:
    labels:
    app: wonderful
spec:
    containers:
    - image: nginx:alpine
```

2. you can also restart it

```
k rollout restart deployment wonderful-v1
```