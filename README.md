# Docker Notes
:whale: My notes created while learning Docker

## What is Docker?
"With Docker, developers can build any app in any language using any toolchain. “Dockerized” apps are completely portable and can run anywhere - colleagues’ OS X and Windows laptops, QA servers running Ubuntu in the cloud, and production data center VMs running Red Hat."

A docker container is just an environment with all necessary installations done for the app running on the container. Each container has a running app and each container itself runs on top of the docker engine which itself runs on top of the host OS.

It solves the problem "it works on my machine, it doesn't work in production". That problem happens because of the different environments - OS's, toolsets etc.

## What is a Dockerfile?
Dockerfile is a script that contains instructions needed to create an image. The Dockerfile builds the Docker image. It's a text file with instructions to build Docker images and it automates the creation of Docker images.

The Docker image contains the project code, installation of node, installments of other programs etc. This image sits on top of a machine and it doesn't contain a machine, like a ubuntu machine. From that image you can run as many containers as you want.

If a machine has Docker installed, the container can run on it and it's going to work 

![Docker](https://www.docker.com/sites/default/files/d8/styles/large/public/2018-11/container-what-is-container.png?itok=vle7kjDj")
