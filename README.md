# SpringBootKafka

Installing Kafka on windows

⦁Download Kafka binaries file  and unzip it to any path.

⦁To make it work on windows we need to change some configurations

Change Zookeeper configuration

⦁Open the zookeeper.properties file from [C:\Users\JDOE\kafka\kafka_2.11-2.3.0\config]

⦁change the dataDir to a valid directory on you machine e.g I create a new folder zookeeper_data in  [C:\Users\JDOE\kafka\kafka_2.11-2.3.0]

⦁So In zookeeper.properties change                                                                                                      dataDir=C:\Users\JDOE\kafka\kafka_2.11-2.3.0\zookeeper_data 

Change Kafka server configuration

⦁Now we need to change the Kafka server configuration

⦁open server.properties file and change kafka log location same as above

⦁log.dir=C:\Users\JDOE\kafka\kafka_2.11-2.3.0\kafka-logs

⦁Add a new properties right above offset.topic.replciation.factor=1 as offset.topic.num.partitions=1                                                                                             min.insync.replicas=1                                                                                                                                         default.replication.factor=1                                        

⦁These configuration are for setting a single node cluster. For multi node cluster configurations are different.

Running Kafka on windows

In Kafka /bin directory there is a /window directory which contains batch files which allow to run kafka on windows

For simplicity add this path to windows environment variables path as 

 

Kafka needs zookeeper so open the cmd and run the following

C:\Users\JDOE&gt;zookeeper-server-start.bat C:\Users\JDOE\kafka\kafka_2.11-2.3.0\config\zookeeper.properties

Start a new cmd to start the kafka server. 

C:\Users\JDOE&gt;kafka-server-start.bat C:\Users\JDOE\kafka\kafka_2.11-2.3.0\config\server.properties

Testing Kafka Installation

Open a new cmd and ask for the list of broker ids with the following command

 

Lets create a kafka topic with following command 

&gt;kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

 

Lets start a Producer and send some messages with following command

&gt;kafka-console-producer.bat --broker-list localhost:9092 --topic test

 

Lets start a Consumer to check the messages with following command

&gt;kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test --from-beginning

 
