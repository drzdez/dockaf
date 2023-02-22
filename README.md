# dockaf
Docker Kafka and Avro Schema server

1. install docker desktop
2. run from project dir
docker-compose up -d

reference:

https://hub.docker.com/r/bitnami/kafka
https://github.com/bitnami/containers/issues/4315

https://hub.docker.com/r/bitnami/schema-registry



*kafka*
- internal port in docker - 9092 external 9093

test working:
  https://kafka.apache.org/quickstart

create topic:
bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092

chesk topic:
bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092

send events:
bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092

read events:
bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092

*schema*
https://aseigneurin.github.io/2018/08/02/kafka-tutorial-4-avro-and-schema-registry.html

Schema example:

{
  "type": "record",
  "name": "Person",
  "namespace": "com.ippontech.kafkatutorials",
  "fields": [
    {
      "name": "firstName",
      "type": "string"
    },
    {
      "name": "lastName",
      "type": "string"
    },
    {
      "name": "birthDate",
      "type": "long"
    }
  ]
}


curl -H "Content-Type: application/vnd.schemaregistry.v1+json" -X POST -d "{\"schema\":\"{\\\"type\\\":\\\"record\\\",\\\"name\\\":\\\"Person\\\",\\\"namespace\\\":\\\"com.ippontech.kafkatutorials\\\",\\\"fields\\\":[{\\\"name\\\":\\\"firstName\\\",\\\"type\\\":\\\"string\\\"},{\\\"name\\\":\\\"lastName\\\",\\\"type\\\":\\\"string\\\"},{\\\"name\\\":\\\"birthDate\\\",\\\"type\\\":\\\"long\\\"}]}\"}" http://localhost:8081/subjects/persons-avro-value/versions

curl http://localhost:8081/subjects/persons-avro-value/versions/1
