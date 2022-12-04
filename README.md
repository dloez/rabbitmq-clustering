# RabbitMQ (AMQP + MQTT) and HAProxy docker compose

## Description
This repository contains an example `docker-compose.yaml` file which:
- Deploys a cluster of 3 nodes of RabbitMQ.
- Enables the following plugins on RabbitMQ nodes:
    - rabbitmq_management
    - rabbitmq_prometheus
    - rabbitmq_mqtt
- Deploys a HAProxy server balancing traffic to the RabbitMQ cluster.

This Docker compose file exposes the following ports:
- 1883  -> MQTT
- 1936  -> HAProxy status page
- 15672 -> RabbitMQ Management
- 5672  -> AMQP

## Usage
1. Modify permissions of `volumes/rabbit/.erlang.cookie` so only the RabbitMQ user can access this file:  
    `chmod 600 volumes/rabbit/.erlang.cookie`
3. Create an external Docker network of remove `external` from `iris` network on `docker-compose.yaml` file. The idea behind creating an external network is to be able to reach haproxy from containers outside this `docker-compose.yaml` file:
    `docker network create iris`
2. Run Docker compose:  
    `docker compose up`
