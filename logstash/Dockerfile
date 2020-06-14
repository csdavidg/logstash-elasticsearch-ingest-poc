FROM docker.elastic.co/logstash/logstash:7.5.1
COPY logstash.yml /usr/share/logstash/config/logstash.yml
COPY logstash.conf /usr/share/logstash/pipeline/logstash.conf
COPY ojdbc8.jar /usr/share/logstash