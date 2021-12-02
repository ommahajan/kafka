# kafka


Kafka :
=======

https://www.javainuse.com/misc/apache-kafka-hello-world
https://www.baeldung.com/ops/kafka-docker-setup
https://kafkatool.com/download.html
https://www.sipios.com/blog-tech/emailing-microservice-apache-kafka-spring-boot
https://www.stackchief.com/blog/Spring%20Boot%20Kafka%20Consumer
https://howtodoinjava.com/kafka/multiple-consumers-example/
https://medium.com/geekculture/multi-broker-insights-into-apache-kafka-cluster-architecture-617b0abfc53e

installation : 
------------

wget https://kafkatool.com/download2/offsetexplorer.sh
chmod +x offsetexplorer.sh
./offsetexplorer.sh
docker-compose down
vi docker-compose.yml ==> add the ip address of system instead of localhost. [KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092,PLAINTEXT_HOST://192.168.0.50:29092]
docker-compose up

create the cluster with name ==> mycluster
Zookeeper host ==> 192.168.0.50
Zookeeper port ==> 2181
chroot path ==> /

security ==> broker security ==> Plaintext

advanced ==> Bootstrap server ==> 192.168.0.50:29092
offet topic ==> tick the "use backgroung thread to read from_consumer_offset topic"

create the topic with name testapp
content type ==> key=string, value=string
create the partition start with index 0. (you can create any number of partition)



--------------------------
docker commonds:- 

	1.create microservice image
	2.docker run --rm --name=kafka-producer -p 8082:8080 kafka-producer
	3.docker rmi 1d14e2288730 (remove image)
	4.docker run -d -p 8081:8081 --restart=always --name kafkaproducer -e port=8081 -e bootstrap-address=192.168.0.51:39092 ujwalgautam/kafka-producer:v1 --> (if shutDown server or restart server then automatic create container)
	5.docker rm -f kafkaproducer --> (? latest check)
	6.docker logs -f --tail 500 kafkaproducer --> (check logs)
-------------------------
https://github.com/ujwal-gautam/kafka-producer
--------------------------



testapp-0


spring.kafka.properties.security.protocol=PLAINTEXT
spring.kafka.bootstrap-servers=kafka:9092
spring.kafka.producer.value-serializer=org.springframework.kafka.support.serializer.JsonSerializer
spring.kafka.producer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.consumer.group-id=messaging_api
spring.kafka.consumer.auto-offset-reset=earliest
spring.kafka.consumer.key-deserializer=org.springframework.kafka.support.serializer.ErrorHandlingDeserializer
spring.kafka.consumer.value-deserializer=org.springframework.kafka.support.serializer.ErrorHandlingDeserializer
spring.kafka.consumer.properties.spring.json.trusted.packages=*
spring.kafka.consumer.properties.spring.deserializer.key.delegate.class=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.properties.spring.deserializer.value.delegate.class=org.springframework.kafka.support.serializer.JsonDeserializer
spring.kafka.listener.missing-topics-fatal=false

https://howtodoinjava.com/java8/java-streams-by-examples/
---------------------------------------------------------
Kafka broker is a logical process, not a phsyical entity. It can be run in a physical machine or a virtual machine, or in a container. Though some people, might use the term broker and node interchangeably. But, as far as the definition goes, a node is a typically a physical entity, a machine or a VM, but a broker is a process. We can run multiple brokers in one physical node also.

A node represents one entity in a cluster. A Kafka cluster comprises of several Kafka brokers (from 1 to many). If it is a single broker cluster, then we can still call it a Kafka cluster or simply Kafka broker. Though, sometimes when people say a Kafka cluster, they mean every thing that is needed to run Kafka i.e. including the Zookeeper cluster also.

Adding more nodes is a way of scaling, but it isn't enough if we just add physical nodes, we need to run our Kafka broker processes in it and only then we can distribute the load among Kafka brokers. People use only a single Kafka cluster that is comprised of many brokers. Some organizations may also maintain multiple Kafka clusters, most typically for redundancy.
