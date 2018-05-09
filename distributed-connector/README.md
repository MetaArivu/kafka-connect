# Distributed Connector

Generally for production you will deploy kafka connector in cluster instead of standalone. In this example we will see how to setup cluster of kafka file connector. 

# Configuration Steps 

- If you are running your broker on different host and port, please make changes to [file-distributed.properties](https://github.com/MetaArivu/kafka-connect/blob/master/distributed-connector/file-distributed.properties) & [file-distributed-2.properties](https://github.com/MetaArivu/kafka-connect/blob/master/distributed-connector/file-distributed-2.properties) 

-  Copy all files from [distributed-connector](https://github.com/MetaArivu/kafka-connect/tree/master/distributed-connector) folder to config folder inside kafka installation folder.

- We have configured rest enpoint to 8083 and 8084.

# Demo - Start kafka file connector in distributed mode

- Step 1 - Start zookeeper and kafka

- Step 2 - Create Topic (file-connector)
  - sh kafka-topics.sh --zookeeper 127.0.0.1:2181 --create --topic file-distributed-source --partitions 3 --replication-factor 1
  
- Step 3 - Go to bin folder inside kafka installation folder and type below two command in seperate terminal.
  - sh connect-distributed.sh config/file-distributed.properties
  - sh connect-distributed.sh config/file-distributed-2.properties

  
- Step 4 - Verify both the worker of Kafka Connect cluster are running using below curl command
  - curl http://localhost:8083/
  - curl http://localhost:8084/
  - Above curl command will print JSON (e.g {"version":"1.1.0","commit":"fdcf75ea326b8e07","kafka_cluster_id":"-wFCkXSLSTSn99MfWztw6w"}). Verify it is printing same kafka_cluster_id for both curl commands.

- Step 5 - Add Kafka Connector using REST API.
  - curl -H "Content-Type: application/json" --request POST --data '{"name":"file-distributed-source","config":{"connector.class":"FileStreamSource","tasks.max":"1","topic":"file-distributed-source","name":"file-source1","file":"/tmp/file-distributed-source.txt"}}' http://localhost:8083/connectors

- Step 6 - Verify new connector is added to cluster
  - curl http://localhost:8083/connectors
  - curl http://localhost:8084/connectors
  - Above curl command will print JSON array with connector name.
  
- Step 7 - Start Consumer
  - sh kafka-console-consumer.sh --bootstrap-server localhost:9093 --topic file-distributed-source --from-beginning
  
- Step 8 - Add data to source file
  - echo "Testing 1 " >> /tmp/file-distributed-source.txt
  - Verify message is getting printed on consumer terminal
  
  
## License

Copyright © [MetaMagic Global Inc](http://www.metamagicglobal.com/), 2017-18.  All rights reserved.

Licensed under the [Apache 2.0](http://www.amexio.org/metamagic-showcase/license.html)  License.

**Enjoy!**

