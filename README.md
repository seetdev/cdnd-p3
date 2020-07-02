# Udagram Image Filtering Application

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into the following components parts:

1. Frontend - Angular web application built with Ionic Framework
2. Reverse Proxy - Reverse Proxy to access the user and feed Microservices
3. User Microservice - Node-Express application that provides all functionality related to a Udagram user. 
4. Feed Microservice - Node-Express application that provides all functionality related to a Udagram feed for posts. 

## Prerequisite

1. Docker version >= 19.03.8
2. Node JS lts/erbium
3. Postgres SQL (Hosted locally or in the Cloud)
4. AWS S3 with read write access

## Getting Started

### Setup environment

1. Clone the repository using `git clone git@github.com:seetdev/cdnd-p3.git`
2. Go into repository folder
3. Create `set_env.sh` using the template `set_env.template.sh` and fill out the variable values
4. Run `source set_env.sh`

### Running locally

Run `docker-compose up`

### Building locally

Run `docker-compose -f docker-compose-build.yaml build --parallel`

### Pushing to DockerHub (*)

1. echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
2. Run `docker-compose -f docker-compose-build.yaml push`

* To push to DockerHub `docker-compose-build.yaml` should be modified to match a repository that user has access.

### Removing the images

1. Run `docker image prune --filter="label=dev.seet.build=true"` to remove build images
2. Run `docker rmi $(docker images --filter=reference="seetdev/udagram-*" -q)` to remove code images

## Access

Front-End UI = `http://localhost:8100`

### API

1. Feed - `http://localhost:8080/api/v0/feed`
2. User - `http://localhost:8080/api/v0/users`