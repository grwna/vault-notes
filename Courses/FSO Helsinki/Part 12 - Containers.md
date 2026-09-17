# Introduction to Containers
A container is a runtime instance of an image. An image is what you download and what you build. Once you run the image, it becomes a container.

Image name format: `registry/organisation/image:tag`

Output of `docker container run hello-world`:
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:5122f6204b6a3596e048758cabba3c46b1c937a46b5be6225b835d091b90e46c
Status: Downloaded newer image for hello-world:latest
```


In docker, you can build application manually, or use an IaC (infrastructure as code) method with Docker Compose.

# Dockerfile
```dockerfile
// base image
FROM node:24

// set CWD
WORKDIR /usr/src/app

// copy local file into the container
COPY ./index.js ./index.js // you can add the flag '--chown=user:user'

RUN npm install // note that it is recommended to use 'npm ci --omit=dev' instead

USER node

// execute commands (here 'its node index.js')
CMD ["node", "index.js"]
```

To Docker, only copy files that you would push to Github. 

**Dockerfile best practices**
There are 2 rules of thumb you should follow when creating images:
- Try to create as **secure** of an image as possible
- Try to create as **small** of an image as possible
Smaller images are more secure by having less attack surface area, and also move faster in deployment pipelines.

Snyk has a great list of the 10 best practices for Node/Express containerization. Read those from [here](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/).

Or here:
[1. Use explicit and deterministic Docker base image tags](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#1-use-explicit-and-deterministic-docker-base-image-tags)
[2. Install only production dependencies in the Node.js Docker image](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#2-install-only-production-dependencies-in-the-node-js-docker-image)
[3. Optimize Node.js tooling for production](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#3-optimize-node-js-tooling-for-production)
[4. Don’t run containers as root](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#4-don-t-run-containers-as-root)
[5. Safely terminate Node.js Docker web applications](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#5-safely-terminate-node-js-docker-web-applications)
[6. Graceful shutdown for your Node.js web applications](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#6-graceful-shutdown-for-your-node-js-web-applications)
[7. Find and fix security vulnerabilities in your Node.js docker image](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#7-find-and-fix-security-vulnerabilities-in-your-node-js-docker-image)
[8. Use multi-stage builds](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#8-use-multi-stage-builds)
[9. Keeping unnecessary files out of your Node.js Docker images](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#9-keeping-unnecessary-files-out-of-your-node-js-docker-images)
[10. Mounting secrets into the Docker build image](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/#10-mounting-secrets-into-the-docker-build-image)


# Docker Compose
An infrastructure as code, declarative way to orchestrate docker containers.
Compose includes building, running containers, and removing both containers and image afterwards.
```yaml
services:
  app:                    # The name of the service, can be anything
    image: express-server # Declares which image to use
    build: .              # Declares where to build if image is not found
    ports:                # Declares the ports to publish
      - 3000:3000
```

# Docker for Dev
Containerize app when developing? a challenge, but using containers for database is the usual use case.

**Bind-Mount**
You can use `-v` run commands or `volumes` in a compose file to attach a bind mount. These are similar to symlinks to connect files in host and files in a container, useful for development.

Volumes are not removed by default on `docker compose down`, have to add `--volumes`.

Bind mounts can be used to **preserve** container data, like database files.

Bind mounts means the files are not stored inside the container, but the containers can access them.

Bind mounts are defined under `services -> volumes`

**Volumes**
While bind mounts store files in a project's directory, named volumes are managed by docker (but still not the container). Volumes are defined under `volumes`, but you still have to define `services -> volumes`.
Example:
```yaml
services:
  mongo:
    image: mongo
    ports: - 3456:27017
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

****
# Summary
Steps of containerization:
Composeless:
- `docker build` using Dockerfile to build an image
- `docker run -p [port] [image name]` to run an instance of the image

Compose:
- `docker compose up`

It seems compose only wins by one command, but usually you would use `docker run` with many flags (ENVs, port, naming, rules, etc.)