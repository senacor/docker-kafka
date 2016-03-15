[![](https://badge.imagelayers.io/senacor/kafka:latest.svg)](https://imagelayers.io/?images=senacor/kafka:latest 'Get your own badge on imagelayers.io')

Kafka in Docker
===

This repository provides everything you need to run Kafka in Docker.

Why?
---
The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run
---

Kafka with log retention limited to 7 days (default)
```bash
docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=`docker-machine ip \`docker-machine active\`` --env ADVERTISED_PORT=9092 senacor/kafka
```

Kafka with (more or less) unlimited log retention
```bash
docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=`docker-machine ip \`docker-machine active\`` --env ADVERTISED_PORT=9092 --env LOG_RETENTION_HOURS=2147483647 senacor/kafka
```

```bash
export KAFKA=`docker-machine ip \`docker-machine active\``:9092
kafka-console-producer.sh --broker-list $KAFKA --topic test
```

```bash
export ZOOKEEPER=`docker-machine ip \`docker-machine active\``:2181
kafka-console-consumer.sh --zookeeper $ZOOKEEPER --topic test
```

In the box
---
* **senacor/kafka**

  The docker image with both Kafka and Zookeeper. Built from the `kafka`
  directory.


Public Builds
---

https://registry.hub.docker.com/u/senacor/kafka/


Build from Source
---

    docker build -t senacor/kafka .

Todo
---

* Not particularily optimzed for startup time.
* Better docs

