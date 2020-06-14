# logstash-elasticsearch-poc

This POC was developed in the simplest way to ingest data from Oracle DB to Elasticsearch using Logstash and its JDBC plugin.

The POC has been created locally using docker images and Kubernetes with the following tools.

- Oracle DB:  It's going to be the data source and the INPUT on logstash
- Logstash:  It's going to manage the interaction between Oracle DB and Elasticsearch, pulling the data from the table person, creating the index and pushing into Elasticsearch as an indexed document.
- Elasticsearch:  It's going to store as indexed documents the information pulling from de data source.
- Kibana:  It's a data visualization dashboard that works with Elasticsearch and provides the Dev Tools which let's interact with the information indexed  in Elasticsearch throughout its REST API 



As the image above shows the cluster was created with three POD's. 

#### POD-DB
This POD contains a docker image of oracle DB wich is exposed by the service oracle-svc in the port 1521.
The oracledb.yaml file contains the configurations necessary to start the Oracle DB image and expose the service oracle-svc.
To create this POD execute the following command.

`$ kubectl apply -f oracledb.yaml`

POD-logstash

This POD contains the docker custom image of logstash, where it's necessary overwrite the files  
