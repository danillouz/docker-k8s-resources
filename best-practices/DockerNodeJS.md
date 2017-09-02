# Docker and Node.js Best Practices
**Docker `v17.06` or greater, Node.js `8.4` or greater.**

## Set environment to production
```Dockerfile
ENV NODE_ENV=production
```

This will make sure that  npm will not install modules listed in `devDependencies`.

## Only rebuild node modules when package.json changes
First copy package files, install them before copying files:

```Dockerfile
COPY package.json package-lock.json ./

RUN npm i

COPY common api ./
```

## Run container as non root
Containers are run as `root` by default, which can be a security issue. The
Node.js images provide an unprivileged user called `node`:

```Dockerfile
USER node
```

## Resources
- [Dockerizing a Node.js web app](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)
- [Node.js Docker best practices](https://github.com/nodejs/docker-node/blob/master/docs/BestPractices.md)