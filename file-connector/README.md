# File connector
This example focus on getting data from file to Kafka & from kafka to file.

## Configuration changes

-  If you are running your broker on different host and port, please make changes to [file-standalone.properties](https://github.com/MetaArivu/kafka-connect/blob/master/file-connector/file-standalone.properties) 
- Please change source file location in [file-standalone-source.properties](https://github.com/MetaArivu/kafka-connect/blob/master/file-connector/file-standalone-source.properties) 
- Please change sink file location in [file-standalone-sink.properties](https://github.com/MetaArivu/kafka-connect/blob/master/file-connector/file-standalone-sink.properties) 
- Copy all files from [file-connector](https://github.com/MetaArivu/kafka-connect/tree/master/file-connector) folder to config folder inside kafka installation folder.

## Demo 1 - Source data from file to kafka

- Step 1 - Start zookeeper and kafka

- Step 2 - Create Topic (file-connector)
  - sh kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --topic file-connector --partitions 3 --replication-factor 1
  
- Step 3 - Go to bin folder inside kafka installation folder and type.
  - sh connect-standalone.sh ../config/file-standalone.properties ../config/file-standalone-source.properties
  
- Step 4 - Start Kafka Consumer
  - sh kafka-console-consumer.sh --bootstrap-server localhost:9093 --topic file-connector --from-beginning
  
- Step 5 - Keep adding new content to end of file and verify you are able to see message on consumer console.


## Demo 2 - Sink data from kafka to file

- Step 1 - Start zookeeper and kafka

- Step 2 - Create Topic (file-connector)
  - sh kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --topic file-connector --partitions 3 --replication-factor 1
  
- Step 3 - Go to bin folder inside kafka installation folder and type. 
  - sh connect-standalone.sh ../config/file-standalone.properties ../config/file-standalone-source.properties ../config/file-standalone-sink.properties
  
- Step 4 - Start Kafka Producer
  - sh kafka-console-producer.sh --bootstrap-server localhost:9093 --topic file-connector
  
- Step 6 - Verify the sink file, you will be able to see new message getting appended to sink file


## License

Copyright © [MetaMagic Global Inc](http://www.metamagicglobal.com/), 2017-18.  All rights reserved.

Licensed under the [Apache 2.0](http://www.amexio.org/metamagic-showcase/license.html)  License.

**Enjoy!**
