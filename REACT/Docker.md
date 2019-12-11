### Docker provides us with Containers. What are these so called "Containers"?

Well, they are packaged environments that run an application isolatedly. All the necessary dependencies for an application are packed with it inside a container. 

### Why is Docker scalable?
Because containers can run anyware, from local laptops to cloud providers.

### Docker Daemon and Docker Client
> **`Docker Client`**: is a CLI (Command Line Interface) that communicates with the Docker Daemon.
> **`Docker Daemon`**: is the "server" itself, a daemon process that serves containers. 

The Docker Daemon and Client can run on the same system, or, the Docker Client can connect to a remote Docker Daemon.

## Docker Fundamentals: Objects

### Images
Read-only templates with instructions for creating Docker containers.
> **`Custom Images`**: to build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. 

### Containers
Containers are runnable instances of an image. They are created using the Docker API or CLI (ps: the CLI users the Docker API). When a container is removed, any changes to its state that are not stored in persistent storage disappear.

### Services

Services are used when you want to scale containers to multiple Docker daemons. This allows containers to work as a *swarm*. Each member of a swarm is a Docker daemon and they communicate through the Docker API. What they do (services) is allow us to define the desire state, such as the number of replicas of the service that must be available at any given time. The service is load-balanced across all worker nodes. To the user, the service appears to be a single application.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MDQxMTkwNDUsLTY2NTI3Njc0MCwtMT
c3ODU5Mjg5OF19
-->