# Microsoft Reactor - Python Web Apps Containerization With Docker

This is part in a series on developing Python WebApps.

## Overview

"Everything Python and Containers"

Tools in Use:

- VSCode or Dev Containers.
- Docker Extension for VSCode/Dev Containers.
- Docker Desktop (for viewing, managing local Docker Containers, Images, and more).
- Flask.
- Azure.

Presenter: Pamela Fox, Cloud Advocate in Pythong, MSFT Reactor

## Intro to Docker Containers

Docker Engine is:

- An engine that runs on top of an OS.

Containers:

- Host Application Code, binaries, and libraries.
- Databases are supported, along with Django, etc.
- Fully-isolated environment.
- Helpful for splitting Apps that rely on separate app versions and dependencies without pollution.

Why?

- Environemnt consistency. Dev, test, staging, and prod environments are the same every time.
- Application portability. Scalability. Move to newer, other hardware.
- Efficient hardware use. Share hardware resources among multiple containers.

Docker Images:

- aka "The Container"
- Container Image is a software package that inludes everything needed to run an application.
- Containers is running instance of a "Container Image".
- Multiple containers can be run from a single Docker Image.
- Image Registry: Get Images. Docker Hub, GitHub Container Registry, Azure Container Registry, AWS Container Registry, Google Cloud Container Registry.
- Python, Node, NGINX, PostgreSQL.
- Base images are usually an OS starting point (Debian Bullseye, etc), and then the desired apps on top of that for a ready-to-build/go image!

Image Layers:

- Base image: Debian or Ubuntu flavor.
- Development environment.
- Supporting App1.
- Supporting App2.
- Others, as there are items that customize the Docker Image for your project goals/specific to your application.

Containerization Steps:

1. Write dockerfile: Base/parent image, Additional software, application code, set working directory, decide on service(s) to expose (e.g. TCP/UDP port), custom commands to launch when Container RUNS. File format is similar to YAML but without tabbing.
2. Build images from Dockerfile: `docker build {cmd, cmd, ...}`
3. Run a Container from the Image: `docker run {name of image} {published_ports} {app_name}`

Docker ignore:

- `.dockerignore`
- Anything that should be ignored by a 'copy' command in the Dockerfile.

_Note_: Multiple instances of Docker Images _can_ be run simultaneously, however separate ports must be configured.

Rebuild:

- After the first build, actions are cached so they don't have to run again.
- Only changed files and version requirements will cache-miss and will redo everything from that point forward.

## How to use DBs with Containers

Local vs. Remote Databases: Demo will be in Local DB instance.

Data Persistence:

- Stopping a Container removes written data.
- Container data is difficult to move between environments.
- Container storage drivers tend to be slower performers.
- Store _persistent_ or _performance-heavy_ data _outside_ of a Docker Container.

Docker Volumes:

- Directory on host machine.
- Maps to a Directory _inside_ of a configured Container.
- This is available in Local Development (not cloud-hosted, remote).

Configuring a Database Docker Instance:

1. Create database
2. Create network
3. Run the PostgreSQL Container Image with Volume and Network created in steps 1 and 2.
4. Connect an App to the DB. `.env` file was used for this step in the demo. Note that the hostname will need to be the _container name_.
5. Build the App Container to generate an App Image.
6. Run the image on the same network as the PostgreSQL Container using `docker run ...` command.

When Data is stored on a Volume mapped to a local host machine, it will persist between Docker Instance runs and builds.

There is an easier way to do this using Docker Compose!

- Declare once in a YAML file.
- Every time it is used, the configuration will be the same and completed at the same time.
- Allows overriding Entrypoints.
- Enables "autoreload" so Docker App will restart if code is being edited while live. Be sure to set up a Volume for the App Code.
- Depends can be configured such that a DB is built and running before the App (that uses the DB) will be started.
- Healthchecks can be defined.

To Run the config: `docker compose up`.

- Locates the YAML in the same folder.
- Executes YAML configuration.
- Logs progress/status to the terminal.

## Deploy Containerized App to Azure

Azure Kubernetes:

- Orchestration framework for containers.
- Very sys-ops/dev-ops.

Azure Container Apps:

- Optimized for Containers.
- Temporary file storage: Ephemeral Volume within the Container App.
- Azure Files: Not optimized for database use but will persist data.
- Manage DB Services: Use network calls to talk to Cosmons DB, Cosmons for PostgreSQL, and Azure DB for PostgreSQL - Flexible Server.
- Container App Environment: Used to manage a Container App, pulled from an Azure Container Registry.
- Container App itself communicated with the DB via Azure virtual networks.
- AZD UP: Azure CLI command to perform Docker commands with Azure Container App.

Azure App Service and Azure Functions support Docker Containers!

Azure Cli:

- azd env new: Answer questions to create a new environment.
- azd up: Looks at `infra` directory (Bicep declarative config) to develop the Container Apps, Key Vault (for secrets), etc.

_Note_: Azure Container Registry has a subscription cost (about $5/mo).

## Resources

- [blog.pamelafox.org](https://blog.pamelafox.org)

## Footer

- Return to [ContEd Index](./conted-index.html).
- Return to [Root README](../README.html).
