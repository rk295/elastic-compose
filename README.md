ELK Docker Compose
==================

This is a quick [DockerCompose] file which brings up a ELK stack. Currently this brings up the following containers:

* elasticsearch
* kibana
* logstash
* grafana

## Instructions

When started Kibana will be listening on port 5601 on localhost (http://localhost:5601/). Elastic is on port 9200 (http://localhost:9200/) and Grafana is on port 3000 (http://localhost:3000/) Logstash will be started with a simple configuration, listening for connection via TCP port 5000 on localhost.

If you wish to provide extra configuration files to logstash, put them in the `conf.d/` directory, making sure they end in `.conf`.

## Starting

To bring the stack, make sure you are in the same directory as the `docker-compose.yml` file and run:

    docker-compose up

This will run up three containers in the foreground. To background them so you can have your terminal back run:

    docker-compose up -d

This will start all the containers in the background.

To inspect the logs run:

    docker-compose logs

That will tail the last few hundred lines from each container, add `-f` to follow the logs.  You can inspect an individual containers logs like:

    docker-compose logs -f elasticsearch

## Stopping

**Note:** If you ran `docker-compose up` then you will need to switch to another window first.

Run from the same directoy as the `docker-compose.yml` file.

    docker-compose kill

## Grafana Setup

The first time you run it, you need to add a datasource to Grafana. The `grafana-setup` script in this directory will do that for you, simply run:

    ./grafana-setup

Once the services have started.

## Configuring

If you wish to add additional configuration to logstash add it to the `conf.d` directory. The files must end in `.conf`. Out of the box this contains two files:

* `elastic-output.conf` - Sends all output to the ElasticSearch container.
* `tcp-5000.conf` - Accepts logs on `TCP:5000`

## Data

Elastic Search is configured to store its data in the `elastic-data` in the current directory. This will enable saving of state between runs of these containers. If you wish to clear out all data and start a fresh copy of Elastic Search simply remove that directory:

    rm -rf elastic-data

## More reading

The containers are all built from the official Docker Hub images. Lots more info can be found on each page:

* [ElasticSearch]
* [Kibana]
* [Logstash]

[DockerCompose]: (https://docs.docker.com/compose/)
[ElasticSearch]: (https://hub.docker.com/_/elasticsearch/)
[Kibana]: (https://hub.docker.com/_/kibana/)
[Logstash]: (https://hub.docker.com/_/logstash/)
