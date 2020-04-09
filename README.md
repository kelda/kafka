# Kafka Cloud Boot

Example of booting Kafka in the cloud during local development. Useful for
reducing local resource usage, and quickly getting a test Kafka cluster.

Runs on the [Blimp](http://kelda.io) cloud. To boot locally instead, install
`docker` and `docker-compose`, and run `docker-compose up`.

## Booting Kafka

1. Clone this repo

    ```
    git clone https://github.com/kelda-inc/kafka
    cd kafka
    ```

1. Download Blimp. This command installs the CLI used to boot Kafka.

    ```
    curl -fsSL 'https://kelda.io/install-blimp.sh' | sh
    ```

1. Create a development sandbox to run Kafka in

    ```
    blimp login
    ```

1. Deploy Kafka into the sandbox. This deploys Kafka and Zookeeper as specified
   in the [Docker Compose file](./docker-compose.yml).


    ```
    blimp up
    ```

## Interacting With Kafka

The Kafka instance is accessible at `localhost:9093`, and you can interact with
it as if it were running locally.

You can also [add services](https://kelda.io/blimp/docs/config/) to the
`docker-compose.yml`, and have them connect to Kafka at `kafka:29092`.

1. Download the Kafka CLI tools

    ```
    curl -o kafka.tgz https://apache.osuosl.org/kafka/2.4.1/kafka_2.12-2.4.1.tgz
    tar xzf kafka.tgz
    cd kafka_2.12-2.4.1
    ```

1. Publish some messages

    ```
    bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
    ```

    Type some messages, and hit `Ctrl-D` to exit.

1. Read the messages

    ```
    bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
    ```
