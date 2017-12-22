# Docker Commands

Cheatsheet of usefull Docker commands.

**Docker `v17.06` or greater.**

## Cleanup

[Remove all unused images, not just dangling ones](https://docs.docker.com/engine/reference/commandline/system_prune/):

```
docker system prune -a
```

## Inspecting Resources

[Display system-wide information](https://docs.docker.com/engine/reference/commandline/info/):

```
docker info -D --format "{{ json . }}" | jq .
```

* The global -D option causes all docker commands to output debug information.
* [jq](https://stedolan.github.io/jq/) is a command line JSON processor.

[Return low-level information on Docker objects](https://docs.docker.com/engine/reference/commandline/inspect/):

```
docker inspect NAME|ID [NAME|ID...] | jq
```

* [jq](https://stedolan.github.io/jq/) is a command line JSON processor.

## Pushing an Image to a Registry

Tag the image:

```
docker tag <image[:tag]> <registryHost[:registryPort]>/<image>[:tag]
```

Or, build and tag the image in one go:

```
docker build -f <path-to-docker-file> -t <registryHost[:registryPort]>/<image>[:tag] .
```

Push the image:

```
docker push <registryHost[:registryPort]>/<image>[:tag]
```

Example tag and push:

```
docker tag f1e2e7e696d5 repo.org.com:443/awesome-api:2.4.0
docker tag f1e2e7e696d5 repo.org.com:443/awesome-api:canary
docker push repo.org.com:443/awesome-api
```

Example build, tag and push

```
docker build -f ./api/Dockerfile -t repo.org.com:443/awesome-api:2.4.0 -t repo.org.com:443/awesome-api:canary .
docker push repo.org.com:443/awesome-api
```

* [Docker tag docs](https://docs.docker.com/engine/reference/commandline/tag/)
* [Docker build docs](https://docs.docker.com/engine/reference/commandline/build/)
* [Docker push docs](https://docs.docker.com/engine/reference/commandline/push/)
