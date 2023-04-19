# Simple Static Page with NGINX

This shows a simple static page being served with an nginx container.

It is a single podman call that spins off an nginx container. This is what the flags mean:

1. `--rm` - this will remove the container after we close nginx just so we don't have to worry about cleaning up
1. `-it` - these two combined put the container in interactive mode(`-i`) and allocate a pty so the container will detect we are calling from a terminal (`-t`
1. `--security-opt label=disable` - we disable SELinux separation to avoid any access control issues
1. `-v "$PWD/public:/usr/share/nginx/html"` - we bind mount the `$PWD/public` directory onto `/usr/share/nginx/html` inside the container. This mounts the public directory to the default directory served by nginx
1. `-p 8080:80` - here we expose the port 80 inside the container as 8080 on the host that way we don't need root access

```bash
#!/bin/bash

podman run --rm -it \
    --security-opt label=disable \
    -v "$PWD/public:/usr/share/nginx/html" \
    -p 8080:80 \
    nginx:latest
```
