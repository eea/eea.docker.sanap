# eea.docker.sanap - Sanap Orchestration

This repository contains the orchestration for https://github.com/eea/eea.sanap,
the Self Assessment for National Adaptation Policy application. 

The application image is automatically built upon commit on Docker Hub: 
eeacms/sanap - https://registry.hub.docker.com/u/eeacms/sanap/

## Starting up an instance

    git clone https://github.com/eea/eea.docker.sanap
    # this will clone just the repo, without submodules
    docker-compose up

## Migrating existing data

To move data from an existing instance of sanap, you should copy the MongoDB
files into the mongo container.

To do that, run:

    # create a folder
    mkdir -p data/db
    # copy here the files, it should look like:
    # journal  local.0  local.ns sanap.0  sanap.1  sanap.ns

    # copy the folder to the container, assuming the label is: eeasanap_db_1
    docker run --rm -v `pwd`/data/:/host --volumes-from=eeasanap_db_1 busybox cp -r /host/db /data/

## Environment variables
The **sanap** container allows for the following environment variables which should be passed as a secret env_file:

    SECRETY_KEY=""  # unique secret string
    SENTRY_DSN=""   # url to Sentry logging endpoint
    HOSTNAME=""     # public url of the sanap installation, defaults to http://projects.eionet.europa.eu
    

## Development Setup

You can use git submodules for fast development.

    git clone --recursive https://github.com/eea/eea.docker.sanap
    # the source code will be cloned inside ./eea.sanap
    # changes to the source code are automatically reflected in the docker container
    docker-compose -f docker-compose.dev.yml up

To commit changes, just go inside `eea.sanap` and use it as a regular git repo.

To update orchestration with the latest source, run:

    git submodules udpate --remote
    git commit ...
    