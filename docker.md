# Docker

## Containers

Use `docker <container> <command>`
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

"Images are the casting molds used to make containers"
Use `docker <image> <command>`
`build` — Build an image.
`push` — Push an image to a remote registry.
`ls` — List images.
`history` — See intermediate image info.
`inspect` — See lots of info about an image, including the layers.
`rm` — Delete an image.

## Misc

`docker container ls ` or `docker ps ` - Listing Containers
`Docker image ls` - Listing Images
`docker network ls` - Listing Networks
`docker container rm -f $(docker ps -aq)` - Delete all running and stopped containers

Run a container from alpine 3.9 image, name the container "web" and expost port 5000 internally, mapped to port 80 inside the container
(access from port 5000 outside will go to port 80 in the container)
**tdlr**: port 5000 now hosts a website that would noramlly be on port 80
`docker container run --name web -p 5000:80 alpine:3.9`

`docker container logs --tail 100 web`

docker version — List info about your Docker Client and Server versions.
docker login — Log in to a Docker registry.
docker system prune — Delete all unused containers, unused networks, and dangling images.

# Docker-Compose

Docker Compose allows us to take the options we use when running a docker container and put them into a .yml file
