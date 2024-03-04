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
    environment:
      CONNECT_BOOTSTRAP_SERVERS: 'broker-dc2:29092'
      CONNECT_REST_ADVERTISED_HOST_NAME: connect-dc2
      CONNECT_LISTENERS: http://connect-dc2:8382
      CONNECT_GROUP_ID: "connect-dc2"
      CONNECT_PRODUCER_CLIENT_ID: "connect-worker-producer-dc2"
      CONNECT_CONFIG_STORAGE_TOPIC: connect-configs-dc2
      CONNECT_CONFIG_STORAGE_REPLICATION_FACTOR: 1
      CONNECT_OFFSET_FLUSH_INTERVAL_MS: 10000
      CONNECT_OFFSET_STORAGE_TOPIC: connect-offsets-dc2
      CONNECT_OFFSET_STORAGE_REPLICATION_FACTOR: 1
      CONNECT_STATUS_STORAGE_TOPIC: connect-status-dc2
      CONNECT_STATUS_STORAGE_REPLICATION_FACTOR: 1
      CONNECT_KEY_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      CONNECT_VALUE_CONVERTER: "org.apache.kafka.connect.json.JsonConverter"
      CONNECT_PLUGIN_PATH: /usr/share/java
      CONNECT_LOG4J_LOGGERS: org.apache.zookeeper=ERROR,org.I0Itec.zkclient=ERROR,org.reflections=ERROR
      # Confluent Monitoring Interceptors for Control Center Streams Monitoring
      CONNECT_PRODUCER_INTERCEPTOR_CLASSES: "io.confluent.monitoring.clients.interceptor.MonitoringProducerInterceptor"
      CONNECT_PRODUCER_CONFLUENT_MONITORING_INTERCEPTOR_BOOTSTRAP_SERVERS: broker-dc2:29092
      CONNECT_CONSUMER_INTERCEPTOR_CLASSES: "io.confluent.monitoring.clients.interceptor.MonitoringConsumerInterceptor"
      CONNECT_CONSUMER_CONFLUENT_MONITORING_INTERCEPTOR_BOOTSTRAP_SERVERS: broker-dc2:29092
      CONNECT_REST_EXTENSION_CLASSES: io.confluent.connect.replicator.monitoring.ReplicatorMonitoringExtension
      KAFKA_JMX_PORT: 9892
      KAFKA_JMX_HOSTNAME: localhost