# PPH Docker and Digital Ocean

Build tools and hosting, and how they work.

## Presenter

Robert Shepley, Code Fellows Alum

## Tools

Good to put tools into your toolbelt!

- Docker
- Digital Ocean

### Docker

What is it?

- Package and run an app in a specialized environment.
- Isolated environments that can communicate with other environments and systems.

Why Docker?

Containers:

- Package code and dependencies.
- Allows running anywhere without setup/installation steps.
- Isolate software from its environment.
- Lives on top of an operating system.
- Applications run on top of the Container Engine.

Makes Dev Efficient and Predictable (from Docker website):

- Find a Docker Image, run the image (or use Docker Componse) and the application is completed.
- Swap-in a different database server into your environment.
- Which version of Node is on the platform (laptop, desktop, server) etc? Docker specifies the dependencies out of the gate.
- Node on your workstation doesn't have to be same as Node on your Docker Image.
- Containers allow multiple versions of *anything* to run on the same hosting platform.

#### Using Docker

There are many ways to setup and use Docker, so use the documentation.

Docker Command: Create and deploy a container in a CLI.

YML: Execute a YML file to define a Docker instance via DockerCompose.

DockerFile: Similar to YAML setup.

Image: Definition for a Container.

Container: A running instance of a Docker Image.

Example: Dockerize an Expressjs server with a DB backend and run using DockerComponse.

DevContainers: VSCode-integration with Docker to deploy entire environments on local or in the cloud.

*Can* be used in productions as well as dev and test.

#### Learning Docker

Have a goal in mind when learning Docker e.g.: Build a solution you want to build. This helps you avoid the complexity of Docker overall to focus on the parts of Docker necessary to get the target system/service built and deployed.

### Digital Ocean

Simpliar to AWS or Heroku: Can upload code and execute it on the platform.

Droplets: Server instances.

- Some droplets are one-click-apps!
- Less than 1 minute to setup, just a few minutes to ready!
- Lower cost than AWS.
- Great for simple, small applications and servers.
- (It sounds like) Pushing code to DigitalOcean requires deploying a Droplet, and then uploading the code to the Container instance.

## Footer

Return to [PPH Index](pph-index.html)

Return to [Root README](../README.html)
