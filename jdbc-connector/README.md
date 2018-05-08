# JDBC connector
This example focus on getting data from database to Kafka & from kafka to database.

## Configuration changes

-  If you are running your broker on different host and port, please make changes to [postgres-standalone.properties](https://github.com/MetaArivu/kafka-connect/blob/master/jdbc-connector/postgres-standalone.properties) 

- Please change source postgres configuration in [postgres-standalone-source.properties](https://github.com/MetaArivu/kafka-connect/blob/master/jdbc-connector/postgres-standalone-source.properties)

- Please change sink postgres configuration in [postgres-standalone-sink.properties](https://github.com/MetaArivu/kafka-connect/blob/master/jdbc-connector/postgres-standalone-sink.properties) 

- Copy all files from [jdbc-connector](https://github.com/MetaArivu/kafka-connect/tree/master/jdbc-connector) folder to config folder inside kafka installation folder.


## Demo 1 - Sink data from kafka to postgres

- Step 1 - Start zookeeper and kafka

- Step 2 - Create Topic (file-connector)
  - sh kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --topic postgres-sink --partitions 3 --replication-factor 1
  
- Step 3 - Go to bin folder inside kafka installation folder and type. 
  - sh connect-standalone.sh ../config/postgres-standalone.properties ../config/postgres-standalone-sink.properties
  
- Step 4 - Start Kafka Producer
  - sh kafka-console-producer.sh --broker-list localhost:9093 --topic postgres-sink
  - Enter below JSON in producer console
  > {"schema":{"type":"struct","fields":[{"type":"string","optional":false,"field":"name"},{"type":"string","optional":false,"field":"company"}],"optional":false,"name":"Person"},"payload":{"name":"deepak","company":"BT"}}
  
- Step 6 - Verify the table(postgres-sink) Postgres, you will be able to see new entries.


## Demo 2 - Source data from file to kafka

- Step 1 - Start zookeeper and kafka

- Step 2 - Create table (postgres-source) in postgres with two columns i.e id(int with PK) and name(text)
  
- Step 3 - Add couple of entries in table(postgres-source)
  
- Step 4 - Start Kafka JDBC Source Connector
  - sh connect-standalone.sh ../config/postgres-standalone.properties ../config/postgres-standalone-source.properties 
  
- Step 5 - Start Kafka Consumer
  - sh kafka-console-consumer.sh --bootstrap-server localhost:9093 --topic jdbc-connector-postgres-source --from-beginning
  
- Step 6 - Add some new entry in table and verify message are getting printed on consumer terminal  



## License

Copyright © [MetaMagic Global Inc](http://www.metamagicglobal.com/), 2017-18.  All rights reserved.

Licensed under the [Apache 2.0](http://www.amexio.org/metamagic-showcase/license.html)  License.

**Enjoy!**
