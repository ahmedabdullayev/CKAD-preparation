# CKAD-preparation
CKAD Exam-style Questions with Solutions

Playlist: https://youtube.com/playlist?list=PLpbwBK0ptssyIgAoHR-611wt3O9wobS8T&si=QGwH-2YiUpPqGbHT


## Useful commands


### Exec commands

#### to investigate inside a pod's volume: sh / bash / cat / ls

```
kubectl exec <pod-name> -c <container-name> -- <sh/bash/cat/ls>
```

#### CURL simple request

```
kubectl exec <pod-name> -i --rm --restart=Never -- curl <ip-address>
```

