# Deploy

## Description
In this project, a node application is containerize. Service can be started via docker compose, in order to also run a controller container which can modify target1 (container that hosts node application).

## Pre-requisites

* [Docker](https://docs.docker.com/desktop/) installed
  * `docker --version` should show the docker version
* [Git](https://github.com/git-guides/install-git) installed
  * `git --version` should show the git version

## Run Application
- Clone repository
- Go to folder `capstone_project`
- Run `docker-compose up` .

## Modify homepage via ansible
- Connect to ansible controller: `docker exec -it controller bash`
- Run ansible playbook: `ansible-playbook playbook.yml -i inventory.ini`
