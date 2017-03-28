ELK Docker Compose
==================

This is a quick [DockerCompose] file which brings up a ELK stack. Currently this brings up the following containers:

* [ElasticSearch]
* [Kibana]
* [Logstash]

## Prerequisites

The only prerequisite is to have [Docker] installed and running on your machine. If you wish to fire logs into [Logstash] using the examples below you also need the NetCat utility. The package is often just called `nc` in Linux distributions.

## Quick Start

To quickly get going simply run the following from the root of this repo:

    docker-compose up

Then open a browser and type in [http://localhost:5601/](http://localhost:5601/), Kibana will load and you should be good to go.

If you want to push logs into ELK, read through the 'Initial Configuration' section below.

## Initial Configuration

When started Kibana will be listening on port 5601 on localhost (http://localhost:5601). Elastic is on port 9200 (http://localhost:9200/).

If you wish to provide extra configuration files to logstash, put them in the `conf.d/` directory, making sure they end in `.conf`.

The config provided in `logstash.d` in this repo will configure Logstash to listen on two TCP ports:

* `5000` - expecting JSON
* `5001` - expecting plain text lines.

You can push log lines into either of these ports using netcat utility:

    cat <<EOF | nc localhost 5001
    Mar 28 09:22:43 box dhcpd: Can't create new lease file: Permission denied
    EOF

Of if you want to insert JSON, use port 5000


    cat <<EOF | nc localhost 5000
    { "foo": "bar", "other_thing": "this"}
    EOF

## More detailed start/stop Instructions

### Starting

To bring the stack, make sure you are in the same directory as the `docker-compose.yml` file and run:

    docker-compose up

This will run up three containers in the foreground. To background them so you can have your terminal back run:

    docker-compose up -d

This will start all the containers in the background.

### Viewing the logs

If you ran `docker-compose up -d` the containers will be in the background and their logs will not be printed to your terminal. In that case, if you want to view the logs you can run:

    docker-compose logs

That will tail the last few hundred lines from each container, add `-f` to follow the logs.  You can inspect an individual containers logs like:

    docker-compose logs -f elasticsearch

### Stopping

**Note:** If you ran `docker-compose up` then you will need to switch to another window first.

Run from the same directoy as the `docker-compose.yml` file.

    docker-compose kill


[Docker]: (https://docker.com/)
[DockerCompose]: (https://docs.docker.com/compose/)
[netcat]: (http://nc110.sourceforge.net/)
[ElasticSearch]: (https://www.elastic.co/products/elasticsearch)
[Kibana]: (https://www.elastic.co/products/kibana)
[Logstash]: (https://www.elastic.co/products/logstash)
