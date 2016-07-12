```
java -jar http-source-rabbit-1.0.0.RC1.jar --server.port=9000 --spring.cloud.stream.bindings.output.destination=http2tuple
```

```
java -jar spring-cloud-stream-processor-flat2tuple-0.0.1-SNAPSHOT.jar --server.port=9090 --spring.cloud.stream.bindings.input.destination=http2tuple --spring.cloud.stream.bindings.output.contentType=application/json --spring.cloud.stream.bindings.output.destination=tuple2gem
```

```
java -jar target/spring-cloud-stream-sinksource-gemfire-1.0.jar --server.port=8000 --gemfire.source.cacheEventExpression=newValue --gemfire.source.region.region-name=RegionTopTen --spring.cloud.stream.bindings.output.destination=topten --gemfire.sink.region.region-name=RegionRaw --gemfire.sink.json=true --gemfire.sink.key-expression="payload.getField('uuid')" --spring.cloud.stream.bindings.input.destination=tuple2gem
```

```
java -jar spring-cloud-stream-sink-stomp-0.0.1-SNAPSHOT.jar --server.port=8888 --stomp.topic=topten --stomp.withSockJS=true --logging.level.io.pivotal.spring.cloud.stream.sink=TRACE --spring.cloud.stream.bindings.input.destination=topten
```

curl -H "Content-Type: application/json" -X POST -d'{"pickupLatitude":40.760326,"pickupLongitude":-73.967758,"dropoffLatitude":40.779728,"dropoffLongitude":-73.855383,"pickupDatetime":"2013-01-01 00:00:00","dropoffDatetime":"2013-01-01 00:04:00","route":"C161.160_C180.155","uuid":"7a49cba6-d3fc-47a4-8e1a-c2503b8144e1"}' 'http://localhost:9000'

----------
