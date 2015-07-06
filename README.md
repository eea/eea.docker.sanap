# eea.docker.sanap - Sanap Orchestration

This repository contains the orchestration for https://github.com/eea/eea.sanap,
the Self Assessment for National Adaptation Policy application.

## Starting up an instance

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
    
