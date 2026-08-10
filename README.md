# dphp - Dockerized legacy php

Provide legacy php images updated with all dependencies for legacy application and those who prefer these versions. 
The default image simply uses php internal server and almalinux+remi packages. An apache variant is provided.

## Disclaimer
- *Do not expose these applications to the open internet. These are EOL versions of PHP.*
- PHP internal server is slow, especially when serving static assets, it is used to be able to scale the application up easily on k8s
- Some of the CI/Readme/boilerplate code is AI generated 
- The Apache variant has .htaccess support enabled by default. Also it needs a writable /etc/httpd/run directory (mount with tmpfs)

## Quick Start

Run the container locally with your current directory mounted:

```bash
docker run -p 8080:8080 -v $(pwd):/app ghcr.io/fkaempfer/dphp:7.4
```

Build a container

```Dockerfile
FROM ghcr.io/fkaempfer/dphp:7.4

COPY --chown=php:php project/ /app/
```

## Container Registry & Index

All published images and timestamped tags are hosted on GitHub Container Registry (GHCR):

* 🌐 [https://github.com/fkaempfer/dphp/pkgs/container/dphp](https://github.com/fkaempfer/dphp/pkgs/container/dphp)
