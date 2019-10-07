``` run zookeeper
docker run -d --name zookeeper --publish 2182:2181 \
  --volume /Users/l0j011d/Developers/flink-recommandSystem-demo/localtime:/var/localtime \
  --restart=always \
  wurstmeister/zookeeper
```

```run kafka
docker run --name kafka \
  -p 9092:9092 \
  --link zookeeper:zookeeper \
  -e KAFKA_ADVERTISED_HOST_NAME=127.0.0.1 \
  -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2182 \
  -d  wurstmeister/kafka 
```

```run kafka manager
docker run -d \
  --link zookeeper:zookeeper \
  -p 9001:9000  \
  -e ZK_HOSTS="zookeeper:2182" \
  hlebalbau/kafka-manager:stable \
  -Dpidfile.path=/dev/null
```

## Change config.properties
`flink-2-hbase/src/main/resources/cofig.properities` to config

## Change application.yml
`web/src/main/resources/application.yml` to use my own
