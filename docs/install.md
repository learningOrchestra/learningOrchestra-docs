# Install and deploy learningOrchestra on a cluster

:bell: This documentation assumes that the users are familiar with a number of advanced computer science concepts. We have tried to link to learning resources to support beginners, as well as introduce some of the concepts in the [last section](#concepts). But if something is still not clear, don't hesitate to [ask for help](support.md).

## Setting up your cluster

learningOrchestra operates from a [cluster](#what-is-a-cluster) of Docker [containers](#what-is-a-container).

All your hosts must operate under Linux distributions and have [Docker Engine](https://docs.docker.com/engine/install/) installed.

Configure your cluster in [swarm mode](https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/). Install [Docker Compose](https://docs.docker.com/compose/install/) on your manager instance.

You are ready to deploy! :tada:

## Deploy learningOrchestra

Clone the main learningOrchestra repository on your manager instance.
- Using HTTP protocol, `git clone https://github.com/learningOrchestra/learningOrchestra.git`
- Using SSH protocol, `git clone git@github.com:learningOrchestra/learningOrchestra.git`
- Using GitHub CLI, `gh repo clone learningOrchestra/learningOrchestra`

Move to the root of the directory, `cd learningOrchestra`.

Deploy with `sudo ./run.sh`. The deploy process should take a dozen minutes.

### Interrupt learningOrchestra

Run `docker stack rm microservice`.

### Check cluster status

To check the deployed microservices and machines of your cluster, run `CLUSTER_IP:80` where *CLUSTER_IP* is replaced by the external IP of a machine in your cluster.

The same can be done to check Spark cluster state with `CLUSTER_IP:8080`.

## Install-and-deploy questions

###### My computer runs on Windows/OSX, can I still use learningOrchestra?

You can use the microservices that run on a cluster where learningOrchestra is deployed, but **not deploy learningOrchestra**.

###### I have a single computer, can I still use learningOrchestra?

Theoretically, you can, if your machine has 12 Gb of RAM, a quad-core processor and 100 Gb of disk. However, your single machine won't be able to cope with the computing demanding for a real-life sized dataset.

###### What happens if learningOrchestra is killed while using a microservice?

If your cluster fails while a microservice is processing data, the task may be lost. Some fails might corrupt the database systems.

If no processing was in progress when your cluster fails, the learningOrchestra will automatically re-deploy and reboot the affected microservices.

###### What happens if my instances loose the connection to each other?

If the connection between cluster instances is shutdown, learningOrchestra will try to re-deploy the microservices from the lost instances on the remaining active instances of the cluster.

## Concepts

###### What is a container?

Containers are a software that package code and everything needed to run this code together, so that the code can be run simply in any environment. They also isolate the code from the rest of the machine. They are [often compared to shipping containers](https://www.ctl.io/developers/blog/post/docker-and-shipping-containers-a-useful-but-imperfect-analogy).

###### What is a cluster?

A computer cluster is a set of loosely or tightly connected computers that work together so that, in many respects, they can be viewed as a single system. (From [Wikipedia](https://en.wikipedia.org/wiki/Computer_cluster))

###### What are microservices?

Microservices - also known as the microservice architecture - is an architectural style that structures an application as a collection of services that are: highly maintainable and testable, loosely coupled, independently deployable, organized around business capabilities, owned by small team.

[An overview of microservice architecture](https://medium.com/hashmapinc/the-what-why-and-how-of-a-microservices-architecture-4179579423a9)
