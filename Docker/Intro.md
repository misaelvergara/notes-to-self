# Intro

Docker is one implementation of the container based virtualization technologies.

Why should applications be deployed in different runtime environments?

To avoid any conflicts between applications that share the same runtime environment, each application should be isolated to its own environment. That is a principle called **Runtime Isolation**.



# Architecture
Docker uses a client-server architecture, with the daemon being the server and the docker client being the client.

Docker Daemon is also referred to as Docker Engine or Docker Server.

## Running Docker on Windows or OS X

Docker uses Linux specific kernel features. So, on OS X or Windows installation, the Docker daemon is running inside a **Docker machine**. 

## Docker machine

The Docker machine is a **lightweight virtual machine** made specially to run the Docker daemon on OS X or Windows.



# Images

Images are **read only templates** used to create containers. Images are composed of layers of other images.



# Containers

Containers are instances of images (a runtime object). They are lightweight and portable encapsulations of an environment in which to run applications.


# Registries and Repositories

A registry is where images are stored. Inside a registry, images are stored in repositories.  Repositories contain different tags, each tag represents a different version of an image.

`docker run <image>:<tag>` - creates a container using the image specified

- runs image x tagged y.
- `docker run <image>:<tag> <command>` runs `<command>` after spinning up the container.




