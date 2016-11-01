# Development Container

A Docker container with all dependencies required for developing this project.

## Preparation

Follow these steps only once:

### Build the Docker image

```
docker build \
  --tag my-js-stack-from-scratch-dev-image \
  --build-arg USER_NAME_ON_HOST=$(whoami) \
  --build-arg USER_ID_ON_HOST=$UID \
  dev/image
```

### Create the Docker container

```
docker create \
  --name my-js-stack-from-scratch-dev \
  --publish 8080:8080 \
  --user $UID \
  --volume $(pwd):/project \
  --workdir /project \
  my-js-stack-from-scratch-dev-image \
  /usr/bin/sleep-forever
```

## Execution

When you want to work on the project, first start the Docker container:

```
docker start my-js-stack-from-scratch-dev
```

And then start an interactive session in that container:

```
docker exec -it my-js-stack-from-scratch-dev env TERM=xterm script -q -c "/bin/bash" /dev/null
```

## Cleanup

To remove the Docker container and image, without deleting any project files:

```
docker rm --force my-js-stack-from-scratch-dev

docker rmi --force my-js-stack-from-scratch-dev-image
```
