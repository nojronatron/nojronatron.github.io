# Docker Learnings

Recently, it became apparent I needed to learn how to _use_ Docker, and not just be aware of it.

These space will contain scribblings from my studies, and use of, Docker.

## Table of Contents

- [Introductory Concepts](#introductory-concepts)
- [How To Think About Docker](#how-to-think-about-docker)
- [Docker Compose](#docker-compose)
- [Questions](#questions)
- [References](#references)
- [Footer](#footer)

## Introductory Concepts

Features:

- Run processes _in isolation_.
- Host resources are leveraged without full bi-directional sharing.
- A lightweight environment that is bound in isolation from the host but allowed to leverage the hosts resources.

Docker File: New project that describes the base image, run commands, copy files and folders into the image, run a script/file within the image to setup or configure and run the service that the Container will house. Change _docker file_ in order to alter an image _build_.

Image: The thing our Container runs from. Usually a `tag` is needed to define which image _version_ to use. Images are immutable and cannot be changed. Build a new version of the Image using a Dockerfile, instead.

Docker Daemon: Manages Container Creation from Images and streams to Docker Client for logging and interaction.

Docker Hub: Docker's Image Repository.

Container: A running Docker Image.

Basic Docker Process/Workflow:

1. Write a Dockerfile which defines which image (and tag) to use and the commands to run and/or files to copy into the image instance.
2. `docker build ...` an Image using the Dockerfile.
3. `docker run ...` uses the Dockerfile and Image to deploy a Container to the host.

Installation:

`apt install docker`

Build:

`docker build -t "myImage:latest" .`:

- `-t myImage`: Name the Image 'myImage' with a tag of 'latest' (the default).
- `.`: Build in this current directory.
- Update the Dockerfile and use Build to create new Images.

Run:

`docker run name:tag`:

- `name:tag` identifies the specific Image name and Tag.

## How To Think About Docker

Consider Docker a means to rapidly build, configure, deploy, and redeploy images using a recipe of an existing _Image_ and a _Dockerfile_.

The Dockerfile identifies the Image, and instructs Docker to `COPY` files, `RUN` scripts, and execute `CMD` commands to setup and configure a specific environment.

It is possible to point Docker Build to a `path` where a project lives (e.g. Web front-end, etc) instead of a Docker Image. This is done by declaring the path rather than the Docker Image name.

> Doing this ensures that the latest dev build is used every time a service is deployed. This is particularly helpful in multi-project environments (see Docker Compose, later in this document).

### How To Think About Docker Deploy

Deploy and redeploy is fast because:

1) Pre-built images are ready-to-run.
2) Configuration and files are injected during Image start-up.
3) Execution of CMDs is done on the image if configured to do so.

Redeployment:

- Docker caches images already downloaded.
- Docker updates by creating a new Container _version_ using cached Image with a diff of Dockerfile instructions.

### Docker Gotchas

- Docker Containers should be considered _ephemeral_ and therefore quickly and consistently replaceable.
- Do _not_ try to update an existing Image unless losing changes is not a problem.
- Consider an `Image` to be a static, immutable thing that can only be changed through an added `Build` command set.

## Docker Compose

Create multi-container apps where Containers can communicate with each other easily.

### Multiple Services Can Talk With One Another

Docker-compose uses YAML.

1. Create a project of multiple services (e.g. Web Service and Database Service).
2. Create a `compose.yml` file to define the docker-compose definition.
3. Docker CLI: `docker compose up` from the directory with the `compose.yml` file.

### Yaml Breakdown

- Services: List of service items the docker-compose project consists of.
- service-name e.g. 'db' or 'web': Define the Services.
- Image: Which Docker Image to launch to a Docker Container.
- Environment: Env-vars to load when the Container loads. External Enivronment Variables can be used here! e.g. `.env`
- Volumes: Tells Docker Container where to store persisted data. Format `- name:/path/...`. If current dir `.` is specified, a working directory defines where the source files are found.
- Healthcheck: Defines how to run a 'healthcheck' for the service (current context). Exit Code 0 is 'successful', anything else is a failure or _unhealthy_. Test, Interval, Timeout, and Retries can be used to define the test, how often to run it, the timeout between executions, and the number of failure retries before 'unhealthy' is reported.
- Build: Filepath where a dockerfile exists, for e.g. `.`
- Command: What to run after the Image is built from the Dockerfile.
- Volumes: Again, identify where to store persisted data. This can be defined as a `Volumes` item later in the Docker-Compose file, or as a `/path` such as `.`.
- Ports: External-to-Container instance port mappings.
- Depends_on: Define the condition under which this service should be considered healthy e.g. If the DB service is down, this API service should be marked 'unhealthy'.
- Environment: Env-vars (see above).

### HOW Docker Composed Containers Communicate

Docker Compose has its own Network and DNS services:

- DNS maps services together e.g. DB service ports; WebApp ports.
- IP addressing is automatic and DNS allows Docker Services to find each other by name only.

Run a command within a Docker Compose container:

- `docker compose exec web bash` opens a bash session to the Docker Componse unit named 'web'.
- Type `exit` to return to the local Docker terminal.

### Launch Docker Compose Solution

`docker compose up`:

1. Builds the Images based on `compose.yml`
2. Configures the internal IP, DNS and mappings.

_Note_: Use `-d` flag to run Docker Compose services in 'detached state', which returns control of Terminal back to the user, but removes the ability to interact with Docker logs and status information.

## Docker Compose Logs

1. Run in detached state.
2. Execute `docker compose logs name-of-service` at the terminal.

Logs are output on-screen top-to-bottom.

Use `-f` to 'tail' the logs.

## Questions

How does a running Docker Image return output to the Docker command terminal?

> This is the default behavior.

Can a running Docker Image stdout be piped elsewhere (file, web server, etc)?

Is a running Docker Image `Screen` redirectable to the host?

## References

- Typecraft [The intro to Docker I wish I had when I started](https://www.youtube.com/watch?v=Ud7Npgi6x8E).
- [Docker Online Documentation](https://docs.docker.com/).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
