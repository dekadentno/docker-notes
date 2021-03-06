# Docker Notes
:whale: My notes created while learning Docker

References:
1. https://docs.docker.com/engine/reference/builder/
2. https://rock-it.pl/how-to-write-excellent-dockerfiles/
3. https://github.com/wsargent/docker-cheat-sheet

## What is Docker?
"With Docker, developers can build any app in any language using any toolchain. “Dockerized” apps are completely portable and can run anywhere - colleagues’ OS X and Windows laptops, QA servers running Ubuntu in the cloud, and production data center VMs running Red Hat."

A docker container is just an environment with all necessary installations done for the app running on the container. Each container has a running app and each container itself runs on top of the docker engine which itself runs on top of the host OS.

It solves the problem "it works on my machine, it doesn't work in production". That problem happens because of the different environments - OS's, toolsets etc.

## What is a Dockerfile?
Dockerfile is a script that contains instructions needed to create an image. The Dockerfile builds the Docker image. It's a text file with instructions to build Docker images and it automates the creation of Docker images.

The Docker image contains the project code, installation of node, installments of other programs etc. This image sits on top of a machine and it doesn't contain a machine, like a ubuntu machine. From that image you can run as many containers as you want.

If a machine has Docker installed, the container can run on it and it's going to work.

Pros: You don't need to install node or anything else on the dev/prod machines because the Docker image has everything, the complete environment in itself. Images behave like virtual machines, but in fact they are self contained processes.

![Docker](https://www.docker.com/sites/default/files/d8/styles/large/public/2018-11/container-what-is-container.png?itok=vle7kjDj")

## Writing a Dockerfile

#### FROM
Sets the Base Image for subsequent instructions. (ubuntu, node:12...)
```Dockerfile
# syntax
FROM [--platform=<platform>] <image> [AS <name>]
# e.g.
FROM node:12 as build
```

#### LABEL
Sets the Author field of the generated images - name and email or other data
```Dockerfile
# syntax
LABEL <key>=<value> <key>=<value> <key>=<value> ...
# e.g.
LABEL version="1.0"
LABEL description="bla bla bla"
```

#### RUN
Execute a command in a shell or exec form
```Dockerfile
# syntax
RUN <command> 
or
RUN ["executable", "param1", "param2"]
# e.g.
RUN chmod 644 bla.txt
RUN rm -f .npmrc
```

#### CMD
Run something in the command line. DockerFile allows usage of the CMD instruction only once.
```Dockerfile
# syntax
CMD ["executable","param1","param2"]
CMD ["param1","param2"]
CMD command param1 param2
# e.g.
CMD echo "This is a test." | wc -
```

#### COPY
Copies new files or directories to container.
```Dockerfile
# syntax
COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
# e.g.
COPY test.txt relativeDir/
```

#### WORKDIR
Sets the working directory.
```Dockerfile
# syntax
WORKDIR /path/to/workdir
# e.g.
WORKDIR /app
```

#### ENV
Sets the environment variable <key> to the value <value>
```Dockerfile
# syntax
ENV MY_NAME="John Doe"
ENV MY_DOG=Rex\ The\ Dog
ENV MY_CAT=fluffy
# e.g.
# ommiting = is possible
ENV HOST 0.0.0.0 

#### EXPOSE
Informs Docker that the container listens on the specified network ports at runtime. NOTE: does not actually make ports accessible.
```Dockerfile
# syntax
EXPOSE <port> [<port>/<protocol>...]
# e.g.
EXPOSE 3000/tcp
```

#### USER
Sets the user name for following RUN / CMD / ENTRYPOINT commands.
```Dockerfile
# syntax
USER <user>[:<group>]
# e.g.
USER patrick
USER 1001
```

#### ENTRYPOINT
Configure a container to run as an executable, which means a specific application can be set as default and run every time a container is created using the image. This also means that the image will be used only to run and target the specific application each time it is called.
```Dockerfile
# syntax
ENTRYPOINT ["executable", "param1", "param2"]
ENTRYPOINT command param1 param2
# e.g.
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```
