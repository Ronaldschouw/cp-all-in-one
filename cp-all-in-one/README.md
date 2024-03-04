# cp-all-in-one

Use `cp-all-in-one` to run the Confluent Enterprise License version of Confluent Platform in Docker.
This Docker Compose file launches Confluent Platform services locally in containers.

## Run the Example

You can refer to the [Quick Start for Confluent Platform](https://docs.confluent.io/platform/current/platform-quickstart.html) for a guided quick start that is based on `cp-all-in-one`. The quick start shows you how to build a basic streaming app on mock data.

Or, to get started with a fresh Confluent Platform installation:

1. Clone this repository.

       git clone https://github.com/confluentinc/cp-all-in-one.git

1. Navigate to the `cp-all-in-one` directory.

       cd cp-all-in-one

1. Checkout the `<github-branch>` branch.

       git checkout <github-branch>

1. Bring up all services:

       docker compose up -d

## Ports

To connect to services in Docker, refer to the following ports:

- ZooKeeper: 2181
- Kafka broker: 9092
- Kafka broker JMX: 9101
- Confluent Schema Registry: 8081
- Kafka Connect: 8083
- Confluent Control Center: 9021
- ksqlDB: 8088
- Confluent REST Proxy: 8082

    environment:
      CONTROL_CENTER_BOOTSTRAP_SERVERS: 'broker-dc2:29092'
      CONTROL_CENTER_CONNECT_DC1_CLUSTER: http://connect-dc1:8381
      CONTROL_CENTER_CONNECT_DC2_CLUSTER: http://connect-dc2:8382
      CONTROL_CENTER_SCHEMA_REGISTRY_URL: http://schema-registry-dc2:8082
      CONTROL_CENTER_KAFKA_DC1_BOOTSTRAP_SERVERS: 'broker-dc1:29091'
      CONTROL_CENTER_KAFKA_DC2_BOOTSTRAP_SERVERS: 'broker-dc2:29092'
      CONTROL_CENTER_REPLICATION_FACTOR: 1
      CONTROL_CENTER_INTERNAL_TOPICS_PARTITIONS: 1
      CONTROL_CENTER_MONITORING_INTERCEPTOR_TOPIC_PARTITIONS: 1
      CONTROL_CENTER_DEPRECATED_VIEWS_ENABLE: "true"
      CONFLUENT_METRICS_TOPIC_REPLICATION: 1
      PORT: 9021