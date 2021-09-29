# Docker

## Containers

Use `docker <container> <my_command>`
`create` — Create a container from an image.  
`start` — Start an existing container.  
`run` — Create a new container and start it.  
`ls` — List running containers.  
`inspect` — See lots of info about a container.  
`logs` — Print logs.  
`stop` — Gracefully stop running container.  
`kill` —Stop main process in container abruptly.  
`rm` —Delete a stopped container.

## Images

Images are the casting molds used to make containers
Use docker image my_command
build — Build an image.
push — Push an image to a remote registry.
ls — List images.
history — See intermediate image info.
inspect — See lots of info about an image, including the layers.
rm — Delete an image.

## Misc

docker version — List info about your Docker Client and Server versions.
docker login — Log in to a Docker registry.
docker system prune — Delete all unused containers, unused networks, and dangling images.
