Kafka Connect is a framework service based around connector to move data into and out of Kafka.




# Common use case on Kafka are

<img width="1010" alt="screen shot 2018-05-08 at 7 04 04 pm" src="https://user-images.githubusercontent.com/23295769/39760346-b238316e-52f2-11e8-9f74-bdfd9f1d7169.png">

### Kafka Connect allows to

- Import data from a various data source like Database, Filesystem, Twitter, FTP etc.
- Export data to a various data source like Twitter, Filesystem, Database, Splunk etc.


# High-Level Kafka Connect & Streams Architecture

<img width="1199" alt="screen shot 2018-05-08 at 7 04 12 pm" src="https://user-images.githubusercontent.com/23295769/39760347-b2645e10-52f2-11e8-9162-b647001dfa7e.png">

- Source or Sink System can be any data source e.g Oracle, MySQL, Postgres, MongoDB, filesystem, FTP, Twitter etc.
- Kafka connect pulls data from the source system and push data directly to Kafka.
- Kafka streams which can be used for data aggregation, transformation and republishing data on Kafka.
- Kafka connect gets data from Kafka and pushes directly to sink data source.

# File and JDBC connector 
### This example purely focuses on File and JDBC connector. It has four set of configuration


 - [File to Kafka](https://github.com/MetaArivu/kafka-connect/blob/master/file-connector/file-standalone-source.properties)
 - [Kafka to File](https://github.com/MetaArivu/kafka-connect/blob/master/file-connector/file-standalone-sink.properties)
 - [Postgres to Kafka](https://github.com/MetaArivu/kafka-connect/blob/master/jdbc-connector/postgres-standalone-source.properties)
 - [Kafka to Postgres](https://github.com/MetaArivu/kafka-connect/blob/master/jdbc-connector/postgres-standalone-sink.properties)

<img width="1202" alt="screen shot 2018-05-08 at 7 04 23 pm" src="https://user-images.githubusercontent.com/23295769/39760348-b2906668-52f2-11e8-8405-fa32c963a8d5.png">


## Note

Make sure you have kafka connect(kafka-connect-jdbc-4.1.0.jar) & Postgres(postgresql-9.4-1206-jdbc41.jar) jars placed in Kafka lib OR in your classpath.

## Run 
Steps for executing [file](https://github.com/MetaArivu/kafka-connect/tree/master/file-connector) and [jdbc](https://github.com/MetaArivu/kafka-connect/tree/master/jdbc-connector) connector are specified in respective folders. 


 ## License

Copyright © [MetaMagic Global Inc](http://www.metamagicglobal.com/), 2017-18.  All rights reserved.

Licensed under the [Apache 2.0](http://www.amexio.org/metamagic-showcase/license.html)  License.

**Enjoy!**
