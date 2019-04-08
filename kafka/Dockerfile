FROM java:openjdk-8-jre

ENV DEBIAN_FRONTEND noninteractive
ENV KAFKA_HOME /opt/kafka_2.10-0.10.0.0

# Install Kafka, Zookeeper and other needed things
RUN apt-get update && \
    apt-get install -y wget supervisor dnsutils net-tools && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    curl -o /tmp/kafka_2.10-0.10.0.0.tgz https://archive.apache.org/dist/kafka/0.10.0.0/kafka_2.10-0.10.0.0.tgz && \
    tar xfz /tmp/kafka_2.10-0.10.0.0.tgz -C /opt && \
    rm /tmp/kafka_2.10-0.10.0.0.tgz

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/

# 2181 is zookeeper, 9092 is kafka
EXPOSE 9092 2181

CMD ["supervisord", "-n"]
