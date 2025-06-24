### Question

#### Link: https://killercoda.com/killer-shell-ckad/scenario/configmap-pod-access

1. Create a ConfigMap named trauerweide with content tree=trauerweide
2. Create the ConfigMap stored in existing file /root/cm.yaml
3. Create a Pod named pod1 of image nginx:alpine
4. Make key tree of ConfigMap trauerweide available as environment variable TREE1
5. Mount all keys of ConfigMap birke as volume. The files should be available under /etc/birke/*
6. Test env+volume access in the running Pod

### Solution

1. 
```
k create cm trauerweide --from-literal=tree=trauerweide
```

2.
```
k apply -f /root/cm.yaml
```

3. 
```
k run pod1 --image=nginx:alpine -o=yaml --dry-run=client > pod1.yaml
```

result:

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod1
  name: pod1
spec:
  containers:
  - image: nginx:alpine
    name: pod1
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

4. Add env

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod1
  name: pod1
spec:
  containers:
  - image: nginx:alpine
    name: pod1
    env:
      - name: TREE1
        valueFrom:
          configMapKeyRef:
            name: trauerweide
            key: tree  
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

5. add volumes

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod1
  name: pod1
spec:
  containers:
  - image: nginx:alpine
    name: pod1
    env:
      - name: TREE1
        valueFrom:
          configMapKeyRef:
            name: trauerweide
            key: tree
    volumeMounts:
      - name: birke
        mountPath: /etc/birke/
  volumes:
    - name: birke
      configMap:
        name: birke 
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

6. test

```
kubectl exec pod1 -- env | grep -i "traud"
```
```
kubectl exec pod1 -- ls /etc/birke
```