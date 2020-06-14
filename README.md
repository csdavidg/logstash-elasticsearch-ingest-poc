# logstash-elasticsearch-poc

This POC was developed in the simplest way to ingest data from Oracle DB to Elasticsearch using Logstash and its JDBC plugin.

The POC has been created locally using docker images and Kubernetes with the following tools.

- Oracle DB:  It's going to be the data source and the INPUT on logstash
- Logstash:  It's going to manage the interaction between Oracle DB and Elasticsearch, pulling the data from the table person, creating the index and pushing into Elasticsearch as an indexed document.
- Elasticsearch:  It's going to store as indexed documents the information pulling from de data source.
- Kibana:  It's a data visualization dashboard that works with Elasticsearch and provides the Dev Tools which let's interact with the information indexed  in Elasticsearch throughout its REST API 

![Alt text](ELK-cluster-POC.png?raw=true "Cluster diagram")

As the image above shows the cluster was created with three POD's. 

#### POD-DB
This POD contains a docker image of oracle DB wich is exposed by the service `oracle-svc` in the port `1521`.
To create this POD execute the following command.

`$ kubectl apply -f oracledb.yaml`

#### POD-ElasticSearch-Kibana

This POD contains the docker images of ElasticSearch and Kibana, they are exposed by the service `elk-service`, ElasticSearch in the port `9200` and Kibana in the port `5601`. To create this POD execute the following command.

`$ kubectl apply -f elk.yaml`

#### POD-logstash

This POD contains the custom Docker image of logstash which is exposed by the service `logstashservice` in the port `9600`. The image also contains the values to define where the data  are going to be pulled from (INPUT) and where the data  are going to be pushed on (OUTPUT), to doing it, it's necessary to overwrite the files `logstash.conf` and `logstash.yml`, also it's necessary to add the JDBC driver library, the files and the Dockerfile used to create this Docker image is inside the logstash folder.

The Docker image also can be found on DockerHub `https://hub.docker.com/repository/docker/csdavidg/logstash.custom`
To create this POD execute the following command.

`$ kubectl apply -f logstash.yaml`

Once the POD of logstash  is initialized the ingest process should start.


