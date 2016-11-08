ELK Docker Compose
==================

This is a quick [DockerCompose] file which brings up a ELK stack.

## Instructions

To bring the stack up run:

    docker-compose up

This will bring up three containers:

* elasticsearch
* kibana
* logstash

They will all be hooked up to communicate correctly.

Kibana will be listening on port 5601 on localhost (http://localhost:5601). Elastic is on port 9200 (http://localhost:9200/).

If you wish to provide extra configuration files to logstash, put them in the `conf.d/` directory, making sure they end in `.conf`.

[DockerCompose]: (https://docs.docker.com/compose/)
