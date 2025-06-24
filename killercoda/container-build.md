### Question

Build a container from scratch
Create a new file /root/Dockerfile to build a container image from. It should:

use bash as base
run ping killercoda.com
Build the image and tag it as pinger .

Run the image (create a container) named my-ping .

You can use docker or podman for this scenario. Just stick to your choice throughout all steps.

### Solution

1. Create dockerfile

```
touch /root/Dockerfile
```

```
FROM bash
CMD ["ping", "killercoda.com"]
```

2. Build image

```
podman -t build pinger .
```

3. Run the image(create container)

```
podman run --name my-ping pinger
```