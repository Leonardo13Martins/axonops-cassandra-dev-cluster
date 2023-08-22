# AxonOps Cassandra Development Cluster

This Docker Compose file will create a Cassandra cluster containing 3 nodes along with AxonOps for
cluster monitoring and management.

## Getting Started

### Prerequisites

This environment requires a recent version of Docker (Docker Engine 19.03.0 or later) with Docker Compose V2.
If you do not have Docker installed the easiest way to get started is to install Docker Desktop which you can
find at [docker.com](https://docker.com/).

If you already have Docker installed then check your versions using these commands:
```bash
docker version
docker compose version
```
On Linux you may need to install the `docker-compose-plugin` package in order for Docker Compose to work.

### Start up
1. Download [docker-compose.yml](https://github.com/axonops/axonops-cassandra-dev-cluster/blob/main/docker-compose.yml) from this repository, or use this command to download it from the command-line:
```bash
curl -O https://raw.githubusercontent.com/axonops/axonops-cassandra-dev-cluster/main/docker-compose.yml
```
2. Run `docker compose up -d` from the directory containing `docker-compose.yml`
3. After a few minutes the containers will start up and initialise the Cassandra cluster
4. After startup is complete open [http://127.0.0.1:3000/](http://127.0.0.1:3000/) in your browser to see the AxonOps dashboard

### Accessing Cassandra

Once the cluster has started up you can use this command to run `cqlsh` inside one of the Cassandra containers:
```bash
docker compose exec -it cassandra-0 cqlsh
```

The CQL port for each node is also exposed on the host's loopback IP address as follows:
```
cassandra-0: 127.0.0.1:9042
cassandra-1: 127.0.0.1:9043
cassandra-2: 127.0.0.1:9044
```
Client applications running on the host should be able to use these addresses to connect to Cassandra.

### Shutting Down

You can stop the cluster with this command:
```bash
docker compose down
```
This will preserve the data for Cassandra and AxonOps in Docker volumes so it will be available when the
cluster is started up again.

Use this command to start the cluster back up:
```bash
docker compose up -d
```

To shut down the cluster and remove all data use this command:
```bash
docker compose down -v
```
This will stop and remove all running containers and delete the Docker volumes containing the Cassandra and AxonOps data.
