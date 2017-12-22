# Docker and Node.js Best Practices

**Docker `v17.06` or greater, Node.js `8.4` or greater.**

## Set environment to production

```Dockerfile
ENV NODE_ENV=production
```

This will make sure that npm will not install modules listed in `devDependencies`.

## Copying dirs and contents of dirs

To `COPY` all contents of a dir into your `WORKDIR` use:

```Dockerfile
WORKDIR /usr/src/app

# All contents of the `common` dir will be copied into `/usr/src/app/`
COPY common .
```

To `COPY` a dir into your `WORKDIR` use:

```Dockerfile
WORKDIR /usr/src/app

# The `common` dir will be copied resulting into `/usr/src/app/common`
COPY common ./common
```

## Only rebuild node modules when package.json changes

First copy package files, install them before copying files:

```Dockerfile
COPY package.json package-lock.json ./

RUN npm i

COPY . .
```

## Run container as non root

Containers are run as `root` by default, which can be a security issue. The
Node.js images provide an unprivileged user called `node`:

```Dockerfile
RUN chown -R node:node .
USER node
```

## Exposing the host of a Web Service

Make sure to set the host of the web service to `0.0.0.0` instead of `localhost`.
This will bind to _all network interfaces_, not just _local-only interfaces_.

You can set an environment variable in the `Dockerfile`, which can be overriden
when running the image:

```Dockerfile
ENV API_HOST=0.0.0.0
```

## Resources

* [Dockerizing a Node.js web app](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)
* [Node.js Docker best practices](https://github.com/nodejs/docker-node/blob/master/docs/BestPractices.md)
* [Dockerfile ENV docs](https://docs.docker.com/engine/reference/builder/#env)
