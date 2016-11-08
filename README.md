ELK Docker Compose
==================

This is a quick [DockerCompose] file which brings up a ELK stack. Currently this brings up the following containers:

* elasticsearch
* kibana
* logstash

## Instructions

When started Kibana will be listening on port 5601 on localhost (http://localhost:5601). Elastic is on port 9200 (http://localhost:9200/).

If you wish to provide extra configuration files to logstash, put them in the `conf.d/` directory, making sure they end in `.conf`.

### Starting

To bring the stack, make sure you are in the same directory as the `docker-compose.yml` file and run:

    docker-compose up

This will run up three containers in the foreground. To background them so you can have your terminal back run:

    docker-compose up -d

This will start all the containers in the background.

To inspect the logs run:

    docker-compose logs

That will tail the last few hundred lines from each container, add `-f` to follow the logs.  You can inspect an individual containers logs like:

    docker-compose logs -f elasticsearch


### Stopping

**Note:** If you ran `docker-compose up` then you will need to switch to another window first.

Run from the same directoy as the `docker-compose.yml` file.

    docker-compose kill


[DockerCompose]: (https://docs.docker.com/compose/)
