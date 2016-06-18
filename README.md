# Real-Time Big Data Analytics
With more and more companies focusing on speed, efficency, and scalability, the need for sophisticated and elegant streaming applications has become more and more apparant. 
My goal in this project is to build a boilerplate architecture that intakes generic data feeds and computes business logic quickly and efficently. 
I will now discuss the type of architecture that I envision. 
## Pipeling architecture
### Apache Flume
Flume is specifically designed to push data from a massive number of sources to the various storage systems in the Hadoop ecosystem, like HDFS and HBase.
In general, when there is enough data to be processed on a Hadoop cluster, there is usually a large number of servers producing the data. 
This number could be in the hundreds or even thousands of servers. Such a huge number of servers trying to write data to an HDFS or HBase cluster can cause major problems, for multiple reasons.
Flume is designed to be a flexible distributed system that can scale out very easily and is highly customizable. 
A correctly configured Flume agent and a pipeline of Flume agents created by connecting agents with each other is guaranteed to not lose data, provided durable channels are used.
Each Flume agent has three components: the source, the channel, and the sink. 
The source is responsible for getting events into the Flume agent, while the sink is responsible for removing the events from the agent and forwarding them to the next agent in the topology, or to HDFS, HBase, Solr, etc. 
The channel is a buffer that stores data that the source has received, until a sink has successfully written the data out to the next hop or the eventual destination.
![alt text](https://github.com/ifilonenko/backend-architecture/spark-streaming/bin/flume1.png?raw=true "Apache Flume")
If the number of servers producing data consistently increases, the number of Flume agents in the tier receiving data from the application servers also needs to increase. 
This means that at some point, it may be required to increase subsequent tiers, though the number of agents in subsequent tiers can be increased at a far slower rate than in the outer tiers. 
This also ensures increased buffering capacity within the Flume setup, to accommodate the increase in data production.
![alt text](https://github.com/ifilonenko/backend-architecture/spark-streaming/bin/flume2.png?raw=true "Apache Flume")
For further reading on Apache Flume click [here](https://flume.apache.org/)
### Apache 
### Amazon Kinesis