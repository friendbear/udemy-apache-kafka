##

### Kafka Topics CLI

```sh

#kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1
kafka-topics --bootstrap-server 127.0.0.1:9092 --topic first_topic --create --partitions 3 --replication-factor 1

WARNING: Due to limitations in metric names, topics with a period ('.') or underscore ('_') could collide. To avoid issues it is best to use either, but not both.
Created topic first_topic.

kafka-topics --bootstrap-server 127.0.0.1:9092 --list
first_topic

kafka-topics --bootstrap-server 127.0.0.1:9092 --topic first_topic --describe
Topic: first_topic      TopicId: eR7sqPPtRK6MgolSIiFuhQ PartitionCount: 3       ReplicationFactor: 1    Configs: segment.bytes=1073741824
        Topic: first_topic      Partition: 0    Leader: 0       Replicas: 0     Isr: 0
        Topic: first_topic      Partition: 1    Leader: 0       Replicas: 0     Isr: 0
        Topic: first_topic      Partition: 2    Leader: 0       Replicas: 0     Isr: 0

kafka-topics --bootstrap-server 127.0.0.1:9092 --topic second_topic --create --partitions 6 --replication-factor 1
kafka-topics --bootstrap-server 127.0.0.1:9092 --topic second_topic --describeTopic: second_topic     TopicId: ehRk2zMwQ3GfNK-1XbCc7Q PartitionCount: 6       ReplicationFactor: 1    Configs: segment.bytes=1073741824
        Topic: second_topic     Partition: 0    Leader: 0       Replicas: 0     Isr: 0
        Topic: second_topic     Partition: 1    Leader: 0       Replicas: 0     Isr: 0
        Topic: second_topic     Partition: 2    Leader: 0       Replicas: 0     Isr: 0
        Topic: second_topic     Partition: 3    Leader: 0       Replicas: 0     Isr: 0
        Topic: second_topic     Partition: 4    Leader: 0       Replicas: 0     Isr: 0
        Topic: second_topic     Partition: 5    Leader: 0       Replicas: 0     Isr: 0

kafka-topics --bootstrap-server 127.0.0.1:9092 --topic second_topic --delete

kafka-topics --bootstrap-server 127.0.0.1:9092 --list
first_topic

```

### Kafka Console Producer CLI

```sh
kafka-console-producer
Missing required option(s) [bootstrap-server]
Option                                   Description                            
------                                   -----------                            
--batch-size <Integer: size>             Number of messages to send in a single 
                                           batch if they are not being sent     
                                           synchronously. (default: 200)        
--bootstrap-server <String: server to    REQUIRED unless --broker-list          
  connect to>                              (deprecated) is specified. The server
                                           (s) to connect to. The broker list   
                                           string in the form HOST1:PORT1,HOST2:
                                           PORT2.                               
--broker-list <String: broker-list>      DEPRECATED, use --bootstrap-server     
                                           instead; ignored if --bootstrap-     
                                           server is specified.  The broker     
                                           list string in the form HOST1:PORT1, 
                                           HOST2:PORT2.                         
--compression-codec [String:             The compression codec: either 'none',  
  compression-codec]                       'gzip', 'snappy', 'lz4', or 'zstd'.  
                                           If specified without value, then it  
                                           defaults to 'gzip'                   
--help                                   Print usage information.               
--line-reader <String: reader_class>     The class name of the class to use for 
                                           reading lines from standard in. By   
                                           default each line is read as a       
                                           separate message. (default: kafka.   
                                           tools.                               
                                           ConsoleProducer$LineMessageReader)   
--max-block-ms <Long: max block on       The max time that the producer will    
  send>                                    block for during a send request      
                                           (default: 60000)                     
--max-memory-bytes <Long: total memory   The total memory used by the producer  
  in bytes>                                to buffer records waiting to be sent 
                                           to the server. (default: 33554432)   
--max-partition-memory-bytes <Long:      The buffer size allocated for a        
  memory in bytes per partition>           partition. When records are received 
                                           which are smaller than this size the 
                                           producer will attempt to             
                                           optimistically group them together   
                                           until this size is reached.          
                                           (default: 16384)                     
--message-send-max-retries <Integer>     Brokers can fail receiving the message 
                                           for multiple reasons, and being      
                                           unavailable transiently is just one  
                                           of them. This property specifies the 
                                           number of retries before the         
                                           producer give up and drop this       
                                           message. (default: 3)                
--metadata-expiry-ms <Long: metadata     The period of time in milliseconds     
  expiration interval>                     after which we force a refresh of    
                                           metadata even if we haven't seen any 
                                           leadership changes. (default: 300000)
--producer-property <String:             A mechanism to pass user-defined       
  producer_prop>                           properties in the form key=value to  
                                           the producer.                        
--producer.config <String: config file>  Producer config properties file. Note  
                                           that [producer-property] takes       
                                           precedence over this config.         
--property <String: prop>                A mechanism to pass user-defined       
                                           properties in the form key=value to  
                                           the message reader. This allows      
                                           custom configuration for a user-     
                                           defined message reader. Default      
                                           properties include:                  
                                                parse.key=true|false                  
                                                key.separator=<key.separator>         
                                                ignore.error=true|false               
--request-required-acks <String:         The required acks of the producer      
  request required acks>                   requests (default: 1)                
--request-timeout-ms <Integer: request   The ack timeout of the producer        
  timeout ms>                              requests. Value must be non-negative 
                                           and non-zero (default: 1500)         
--retry-backoff-ms <Integer>             Before each retry, the producer        
                                           refreshes the metadata of relevant   
                                           topics. Since leader election takes  
                                           a bit of time, this property         
                                           specifies the amount of time that    
                                           the producer waits before refreshing 
                                           the metadata. (default: 100)         
--socket-buffer-size <Integer: size>     The size of the tcp RECV size.         
                                           (default: 102400)                    
--sync                                   If set message send requests to the    
                                           brokers are synchronously, one at a  
                                           time as they arrive.                 
--timeout <Integer: timeout_ms>          If set and the producer is running in  
                                           asynchronous mode, this gives the    
                                           maximum amount of time a message     
                                           will queue awaiting sufficient batch 
                                           size. The value is given in ms.      
                                           (default: 1000)                      
--topic <String: topic>                  REQUIRED: The topic id to produce      
                                           messages to.                         
--version                                Display Kafka version. 
```

```sh
kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic
>Hello Stephane
>awesome course!
>lerning Kafka
>just another message :)
>^C

kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --producer-property acks=all
>some message that is acked
>just for fun
>jun learning!
>^C


kafka-console-producer --broker-list 127.0.0.1:9092 --topic new_topic
>hey this topic not exists.
[2021-11-05 10:49:14,652] WARN [Producer clientId=console-producer] Error while fetching metadata with correlation id 3 : {new_topic=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2021-11-05 10:49:14,757] WARN [Producer clientId=console-producer] Error while fetching metadata with correlation id 4 : {new_topic=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
>^C

kafka-topics --bootstrap-server 127.0.0.1:9092 --topic new_topic --describe
Topic: new_topic        TopicId: 19Ht124tRZu8YqeJ56jHPQ PartitionCount: 1       ReplicationFactor: 1    Configs: segment.bytes=1073741824
        Topic: new_topic        Partition: 0    Leader: 0       Replicas: 0     Isr: 0

```

change server.properties

```
# The default number of log partitions per topic. More partitions allow greater
# parallelism for consumption, but this will also result in more files across
# the brokers.
num.partitions=3
```

run

```
kafka-console-producer --broker-list 127.0.0.1:9092 --topic new_topic_2
>Hello new 2 topic
[2021-11-05 10:57:02,717] WARN [Producer clientId=console-producer] Error while fetching metadata with correlation id 3 : {new_topic_2=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2021-11-05 10:57:02,822] WARN [Producer clientId=console-producer] Error while fetching metadata with correlation id 4 : {new_topic_2=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2021-11-05 10:57:02,931] WARN [Producer clientId=console-producer] Error while fetching metadata with correlation id 5 : {new_topic_2=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
>^C
```

describe new_topic_2

```sh
 kafka-topics --bootstrap-server 127.0.0.1:9092 --topic new_topic_2 --describe
Topic: new_topic_2      TopicId: UQNwzS5ERBi40YZO7-tmZg PartitionCount: 3       ReplicationFactor: 1    Configs: segment.bytes=1073741824
        Topic: new_topic_2      Partition: 0    Leader: 0       Replicas: 0     Isr: 0
        Topic: new_topic_2      Partition: 1    Leader: 0       Replicas: 0     Isr: 0
        Topic: new_topic_2      Partition: 2    Leader: 0       Replicas: 0     Isr: 0
```

### Kafka Console Consumer CLI

consumer

run

```sh
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic
hi
how are you?
this is a new message
play play play
here is another message
btw really awesoome course


```

producer

send message.


```sh

kafka-console-producer --bootstrap-server 127.0.0.1:9092 --topic first_topic
>hi
>how are you?
>this is a new message
>play play play
>here is another message
>btw really awesoome course
>^C
```

--from-beginning

```sh
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning
awesome course!
just another message :)
some message that is acked
jun learning!
this is a new message
here is another message
lerning Kafka
hi
play play play
Hello Stephane
just for fun
how are you?
btw really awesoome course
```


### Kafka COnsumer Groups


3 pattition

```sh
kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic
```

2 groups

```
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-group
hi
how are you
a
c
d
2
4
6
1
c
3
5
how are you.
fine thank's
do not distrib

```

same group my-first-group

```sh
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-group
3 pattitions
b
1
3
5
8
2
4
```

second group 
```sh
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-second-group
1
c
2
3
4
5
how are you.
fine thank's
do not distrib
```

third group --from-biginning

```sh
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-third-group --from-beginning
awesome course!
just another message :)
some message that is acked
jun learning!
this is a new message
here is another message
hi
a
d
2
4
6
1
3
how are you.
do not distrib
lerning Kafka
hi
play play play
how are you
c
7
c
5
fine thank's
Hello Stephane
just for fun
how are you?
btw really awesoome course
3 pattitions
b
1
3
5
8
2
4
```
