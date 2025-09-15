# Docker Learnings

Recently, it became apparent I needed to learn how to _use_ Docker, and not just be aware of it.

These space will contain scribblings from my studies, and use of, Docker.

## Table of Contents

- [Introductory Concepts](#introductory-concepts)
- [Basic Docker Process/Workflow](#basic-docker-processworkflow)
- [Some Basic Docker Commands](#some-basic-docker-commands)
- [Docker File Contents](#docker-file-contents)
- [How To Think About Docker](#how-to-think-about-docker)
- [Docker Compose](#docker-compose)
- [Docker Compose Logs](#docker-compose-logs)
- [Questions](#questions)
- [References](#references)
- [Footer](#footer)

## Introductory Concepts

Docker is a linux-y thing:

- Files might not have a name.
- Paths are not Windows-y.
- Commands are linux-like.

Features:

- Run processes _in isolation_.
- Host resources are leveraged without full bi-directional sharing.
- A lightweight environment that is bound in isolation from the host but allowed to leverage the hosts resources.

Docker File:

- New project that describes the base image.
- Describes commands needed to copy files and folders into the image.
- Declares commands (and scripts, once copied) that should be run within the image.
- Describes how to set up (config and run) a service that the Container will house.
- Default filename is 'Docker.' (no extension).
- Change docker file contents to alter an image _build_.
- Docker build command can point to a Dockerfile in a separate directory by setting the unnamed 'Path' argument (usually `.` for `Docker.`).

Image:

- The thing our Container runs from.
- Usually a `tag` is needed to define which image _version_ to use.
- Images are _immutable_ and cannot be changed.
- Build a new version of the Image using a Dockerfile to change settings, files, services, etc.

Docker Daemon:

- Manages Container Creation from Images and streams to Docker Client for logging and interaction.

Docker Hub:

- Docker's Image Repository.

Container:

- A running Docker Image.

## Basic Docker Process/Workflow

1. (Optional) Pull a base image to use: `docker pull {name}:{tag}` where name is a Docker Registry image name, and tag is the ID (usually 'latest').
1. Write a Dockerfile which defines which image (and tag) to use and the commands to run and/or files to copy into the image instance. The `FROM` command will cause `docker pull ...` to run if the `FROM` image is not already local.
1. Build the Image `docker build -t {name}:{tag} -f {dir_to_Dockerfile|.}` builds an Image using the Dockerfile, naming it 'name' and 'tag'. The Dockerfile defines _which base image to target_.
1. Deploy: `docker run --rm -it -p nnnn:nnnn {image_name:image_tag}` uses the Dockerfile and Image to deploy a Container to the host.

## Some Basic Docker Commands

Install Docker:

- `apt install docker`

Build A Docker Image With a Dcokerfile:

`docker build -t "myImage:latest" .`:

- `-t myImage`: Name the Image 'myImage' with a tag of 'latest' (the default).
- `.`: Build in this current directory.
- Update the Dockerfile and use Build to create new Images.
- Use a Dockerfile in some other directory and store output here: `docker build -t "myImage:latest" -f "..\docker\files\Dockerfile" .`

Run A Docker Image In A Container:

- `docker run name:tag`:
- ID a name/tag by option flag: `-t name:tag` identifies the specific Image name and Tag.

Attach to a Running Docker Container:

- `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`
- `docker run --interactive --tty {container_name}:{container_tag}`

Command Argument Breakdowns:

- `--rm`: Remove Container and its volume when it exits.
- `-it`: Stands for `-i` and `-t` which means "Interactive" keeping STDIN open, along with attaching a pseudo-TTY to the container for cmdline i/o streams and piping.
- `-p`: Publish or expose port (case-sensitive). `--expose {host-port-protocol}:{container-port-protocol}` example to bind container port 5127 to host port 8080: `--expose 8080:5127`.

## Docker Desktop

Features for local machine Docker Images:

- Build
- Share
- Run
- Verify

Assists:

- Collaboration with others
- Minimal setup
- Low overhead


## Docker File Contents

Must start with `FROM` statement:

- Identifies the source image that this Dockerfile targets.
- e.g. `debian:latest`

The order of command entry is important:

- Caching speeds up subsequent build operations.
- The higher-up in the Dockerfile that a change is made, the fewer cached items can be re-used.
- Maintain the most critical, and least-likely to change commands near the TOP of the Dockerfile.

WORKDIR command:

- Set the working directory for any interactive operations: e.g. `/app`

RUN command:

- The command line for Docker to execute _inside the Container Image_.
  - e.g. `RUN apt update && apt install iputils-ping -y`.
- RUN commands are executed when the image is being BUILT.
- RUN can also be formatted like `RUN ["command", "param1", ...]`.

CMD command:

- An array of string-based command-line commands to run within the container.
  - e.g. `CMD["ping", "-c 4", "192.168.0.1"]`
- CMD commands are executed when the Container is RUN.
- Each item in the array represents strings in the chain to send serially to the interpreter.
- There is a 1:1 relationship between a group of a command and argument(s) and the set (square brackets),  meaning a 'ping ...' command that is followed by a 'tail /var/log' represent TWO commands and would be added to the Dockerfile like `CMD["ping", "-c 4", "192.168.0.1"]\nCMD["tail", "/var/log"]`
- It is possible to use CMD to start an application when the Container starts.
- Single command line can be run with just `CMD param1`

ENTRYPOINT command:

- `ENTRYPOINT ["command", "param1, ...]`
- Alternatively without quotes: `ENTRYPOINT command param1 ...`

ENV Command:

- Set Environment Variables.
  - `ENV key=value`

ARG Command:

- Set arguments, similar to ENV but ...
- `ARG name` or `ARG name=defaultvalue`

USER Command:

- Define a userID that starts the container e.g. non-root
- `USER user`
- `USER user:group`

EXPOSE Command:

- Expose a specified port with or without a protocol.
- `EXPOSE port`
- `EXPOSE port/protocol`

COPY Command:

- `COPY {source} {destination}`
- Copies source from local filesystem to destination in the Docker image currently being built.

## How To Think About Docker

Consider Docker as a means to rapidly build, configure, deploy, and redeploy images from a recipe using an existing _Image_ and a _Dockerfile_.

- The Dockerfile identifies the Image, and instructs Docker to `COPY` files, `RUN` scripts, and execute `CMD` commands to setup and configure a specific environment.

It is possible to point Docker Build to a `path` where a project lives (e.g. Web front-end, etc) instead of a Docker Image. This is done by declaring the path rather than the Docker Image name.

> Doing this ensures that the latest dev build is used every time a service is deployed. This is particularly helpful in multi-project environments (see Docker Compose, later in this document).

### Docker Networks

Three Network types:

- Bridge: Separate, isolated network from the host. Containers can talk to each other but not the host.
- Host: Containers share host machine's network stack directly.
- Default: Used when no network is specified.

Docker Networks and Managing Containers:

- Managing a Docker instance does not require network access.
- Docker command line accesses the Docker instance using Docker APIs instead.

Docker Commands:

- `docker network inspect -f json|template -v {networkID}`.
- `-f`: Format style (or skip for uncompressed JSON).
- `-v`: Verbose.

### How To Think About Docker Deploy

Deploy and redeploy is fast because:

1) Pre-built images are ready-to-run.
2) Configuration and files are injected during Image start-up.
3) Execution of CMDs is done on the image if configured to do so.

Redeployment:

- Docker caches images already downloaded.
- Docker updates by creating a new Container _version_ using cached Image with a diff of Dockerfile instructions.

## Docker Pros and Cons

### Pros

- Increase dev cycle speed, portability, and shareability, regardless of platform.
- Avoid shared infrastructure (like a shared dev/test lab).
- Avoid setting up physical or cloud infrastructure without managing those resources directly.
- If your application contains many services, each can be containerized individually, or as a group, whichever fits the requiremens.
- Whether or not the deploye application ends up in Kubernetes or another Container hosting system, the application can run natively, AND within a Docker container in most (if not all) cases.
- Team members are not bound to using Docker once an application has been "containerized".

### Docker Gotchas

- Docker Containers should be considered _ephemeral_ and therefore quickly and consistently replaceable.
- Do _not_ try to update an existing Image unless losing changes is not a problem.
- Consider an `Image` to be a static, immutable thing that can only be changed through an added `Build` command set.

## Docker Compose

Create multi-container apps where Containers can communicate with each other easily.

- Full-stack applications
- Single YAML file provides definitions for all Services and Volumes
- YAML also has environment variables and Terminal commands
- Bring-up and deploy multi-container app: `docker compose up -d --build`
- Tear-down: `docker compose down`

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

## Dev Lifecycle Using Docket

### Docker Watch

- Pull require image(s)
- Build image(s) based on Docker Compose file(s)
- Monitors changes to code
- Auto-updates image build
- Without Docker Watch, developer must execute Docker build or Docker compose for code changes to take effect

### Build and Push Custom Image

Container Images are executable packages with everything necessary to running software.

- Docker Registry: Allows access to built-in and custom Container Images, good for teams or OSS
- Docker Hub: Public registry platform to store and share images

> See [Docker Hub Explore](https://hub.docker.com/explore)

Use the VSCode DockerHub extension to simplify performing common actions:

- Run
- Run Interactive
- Inspect
- Pull
- Push
- Tag
- Copy Full Tag
- Remove

## Security

### Docker Scout

Assists with resolving Image security vulnerabilities:

- Base Image version
- Installed software and packages version(s)

Once a vulnerable version has been identified, simplly update one of the following and rebuild the Image to implement the changes:

- Update base Image version from a registry
- Update a package definition/property with updated version requirements
- Add updated file(s) that do not have the identified vulnerability

### Supply Chain Security

Best Practices:

- Only use trusted images: Docker official images, and images from a verified publisher
- Build Attestations: Software BOM (SBOM), Provenance Attestations
- Vulnerability detection (Docker Scout)
- Policy Enforcement during dev, test, and ci/cd

## Questions

How does a running Docker Image return output to the Docker command terminal?

> This is the default behavior.

Can a running Docker Image stdout be piped elsewhere (file, web server, etc)?

Is a running Docker Image `Screen` redirectable to the host?

## References

- Docker [Dockerfile Reference](https://docs.docker.com/reference/dockerfile/)
- Docker Container [Run Interactive reference](https://docs.docker.com/reference/cli/docker/container/run/#interactive)
- Typecraft [The intro to Docker I wish I had when I started](https://www.youtube.com/watch?v=Ud7Npgi6x8E)
- [Docker Online Documentation](https://docs.docker.com/)
- [Christian Lempa: Learning Docker // Build Container Images](https://www.youtube.com/watch?v=JDw3ZdQcv2g)

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
