# Learning Docker
- Concepts
	- Docker Engine: docker daemon, receive cmd from docker-client via REST API or CLI
	- Docker compose: run multiple docker containers instance simultaneously
	- Docker machine: install the docker engine at the local system
	- Kitematic: UI tool for docker in windows
	- Docker image: read only template used to create containers created via dockerfile
	- Docker container: runtime instance of docker image
	- Docker registry: a storage component for docker image, e.g., DockerHub
	- Docker Swarm: docker engine cluster management system
	- istio: service mesh
	- knative: serverless
- Commands
	- '''docker --version'''
	- '''docker run hello-world'''
	- '''docker images'''
	- '''docker pull ubuntu'''
	- '''docker run -it -d ubuntu'''
	- '''docker ps -a'''
	- '''docker exec -it container-id bash'''
	- '''docker start container-id'''
	- '''docker stop container-id'''
	- '''docker login''' 
	- '''docker rm container-id'''
	- '''docker image rm image-id''' / '''docker rmi image-id'''

# Resource
[Docker for Windows](https://www.youtube.com/watch?v=iJeL2tOFfvM)
[Windows Docker 安装](https://www.runoob.com/docker/windows-docker-install.html)
[Docker Quick Start](https://hub.docker.com/?overlay=onboarding)
[Docker github](https://github.com/docker?utf8=%E2%9C%93&q=doodle&type=&language=)
[Install Docker on Windows 10](https://runnable.com/docker/install-docker-on-windows-10)
[How to remove docker images, containers, and volumes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)
[Docker edge release notes](https://docs.docker.com/docker-for-windows/edge-release-notes/)
[Getting started with Docker and Kubernetes on Win10](https://learnk8s.io/blog/installing-docker-and-kubernetes-on-windows/)

# MISC
- 查看windows version的命令： '''winver'''
