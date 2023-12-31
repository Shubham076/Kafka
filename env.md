#### KAFKA_CFG_NODE_ID=1

- This sets the node ID for the Kafka broker. Each broker in a Kafka cluster should have a unique ID. In this case, the ID is set to 1.

#### KAFKA_CFG_PROCESS_ROLES=controller,broker

- This defines the roles that the broker will play. Kafka in KRaft mode combines the roles of a broker and controller (previously called ZooKeeper) into single entities. Here, the broker is designated to be both a controller and a broker.

##### KAFKA_CFG_INTER_BROKER_LISTENER_NAME=BROKER

- Kafka can have multiple listener names for different purposes. The inter-broker listener name defines which listener other brokers in the cluster should use to communicate with this broker. Here, it's set to BROKER.


#### KAFKA_CFG_CONTROLLER_LISTENER_NAMES=CONTROLLER

- This specifies the names of the listeners used for controller-to-broker communication and broker-to-controller communication. Here, it's set to CONTROLLER.


#### KAFKA_CFG_LISTENERS=BROKER://:9092,CONTROLLER://:9093

- Purpose: Specifies on which interfaces and ports the Kafka brokers will listen for incoming connections.
- Format: BROKER://:9092,CONTROLLER://:9093,CONNECTIONS_FROM_HOST://:19094
- Here, the absence of a domain or hostname (just :) means Kafka will bind these listeners to all available network interfaces on the host machine. It's listening on ports 9092, 9093, and 19094 on any network interface the server has.

#### KAFKA_CFG_ADVERTISED_LISTENERS
- Purpose: Tells clients how they can reach the Kafka brokers. This is what Kafka uses to advertise itself to clients.
- Format: BROKER://kafka3:9092,CONNECTIONS_FROM_HOST://localhost:19094
- BROKER://kafka3:9092 is likely for internal clients (within the same network, such as a Docker network) to connect to the Kafka broker using the hostname kafka3 on port 9092.
- CONNECTIONS_FROM_HOST://localhost:19094 is for external clients. This configuration is crucial when Kafka is running inside a Docker container, and you want to connect to it from the host machine on which Docker is running. The localhost here refers to the Docker host for external connections.

#### KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=CONTROLLER:PLAINTEXT,BROKER:PLAINTEXT

- This maps listener names to security protocols. Both CONTROLLER and BROKER listeners are set to use PLAINTEXT, which means no encryption.


#### KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=1@kafka1:9093,2@kafka2:9093,3@kafka3:9093

- In KRaft mode, Kafka uses a Raft-like protocol to manage metadata and requires a quorum of controllers to make decisions. This specifies the voters in the quorum. It lists three voters (which can be both brokers and controllers) with their node IDs and addresses.


#### KAFKA_KRAFT_CLUSTER_ID=OTMwNzFhYTY1ODNiNGE5OT

- This sets the unique cluster ID for a Kafka cluster running in KRaft mode. This ID helps differentiate between different Kafka clusters and should remain consistent throughout the life of the cluster.
