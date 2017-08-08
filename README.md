# Docker Commands
Cheatsheet of usefull Docker commands.

**Docker v17.06 or greater.**

# Cleanup
[Remove all unused images, not just dangling ones](https://docs.docker.com/engine/reference/commandline/system_prune/):

```
docker system prune -a
```

# Inspecting Resources
[Display system-wide information](https://docs.docker.com/engine/reference/commandline/info/):

```
docker info -D --format "{{ json . }}" | jq .
```

- The global -D option causes all docker commands to output debug information.
- [jq](https://stedolan.github.io/jq/) is a command line JSON processor.

[Return low-level information on Docker objects](https://docs.docker.com/engine/reference/commandline/inspect/):

```
docker inspect NAME|ID [NAME|ID...] | jq
```

- [jq](https://stedolan.github.io/jq/) is a command line JSON processor.

# License
MIT Copyright (c) 2017 Daniël Illouz.