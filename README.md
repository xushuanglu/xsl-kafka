#启动kafka
.\bin\windows\kafka-server-start.bat .\config\server.properties

#创建一个toptic
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 1 --partitions 1 --topic kafka-action

#错误描述--replication-factor参数用来设置主题副本数，3个节点的kafka集群最多只有3个副本，若创建主题时副本大于3，则抛出如下异常：
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 4 --partitions 1 --topic kafka-action
Error while executing topic command : Replication factor: 4 larger than available brokers: 3.
[2019-06-20 19:14:51,773] ERROR org.apache.kafka.common.errors.InvalidReplicationFactorException: Replication factor: 4 larger than available brokers: 3.
 (kafka.admin.TopicCommand$)
 
#创建topic成功
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 3 --partitions 1 --topic kafka-action
Created topic kafka-action.

#创建一个config-test主题，设置主题的max.message.bytes=404800字节。
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 3 --partitions 1 --topic kafka-action-config-test --config max.message.bytes=404800
Created topic kafka-action-config-test.

在创建主题时若使用了config参数，则通过Zookeeperk客户端可以在/config/topics节点下查看到该主题所覆盖的配置


#错误
reqpath:n/a Error Path:/config/topics/config-test Error:KeeperErrorCode = NoNode for /config/topics/config-test


#删除主题
kafka-topics --delete --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test
#报错
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --delete --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test
Topic config-test is marked for deletion.
Note: This will have no impact if delete.topic.enable is not set to true.

#解决方案
在kafka  D:\kafka\kafka_2.11-2.2.1\config\server.properties添加下面配置
#设置删除
delete.topic.enable=true

D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --delete --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test
Topic config-test is already marked for deletion.


#查看主题   list:列出所有kafka所有的主题名  or  describe：查看所有主题或某个特定的主题的信息

#列出所有kafka所有的主题名
kafka-topics --list --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183

D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --list --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183
__consumer_offsets
config-test - marked for deletion
kafka
kafka-action
kafka-action-config-test
kafka-action1
kafkaTest
test
test6

#查看所有主题或某个特定的主题的信息
kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183

**************************************************************************************************************************************
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183
Topic:__consumer_offsets        PartitionCount:50       ReplicationFactor:3     Configs:segment.bytes=104857600,cleanup.policy=compact,compression.type=producer
        Topic: __consumer_offsets       Partition: 0    Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 1    Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 2    Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 3    Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 4    Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 5    Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 6    Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 7    Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 8    Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 9    Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 10   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 11   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 12   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 13   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 14   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 15   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 16   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 17   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 18   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 19   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 20   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 21   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 22   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 23   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 24   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 25   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 26   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 27   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 28   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 29   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 30   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 31   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 32   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 33   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 34   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 35   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 36   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 37   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 38   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 39   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 40   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 41   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 42   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 43   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 44   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 45   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 46   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 47   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 48   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 49   Leader: 0       Replicas: 2,0,1 Isr: 0
Topic:config-test       PartitionCount:3        ReplicationFactor:2     Configs:max.message.bytes=404800        MarkedForDeletion:true
        Topic: config-test      Partition: 0    Leader: -1      Replicas: 0,1   Isr: 0
        Topic: config-test      Partition: 1    Leader: -1      Replicas: 1,2   Isr: 1
        Topic: config-test      Partition: 2    Leader: -1      Replicas: 2,0   Isr: 0
Topic:kafka     PartitionCount:2        ReplicationFactor:2     Configs:
        Topic: kafka    Partition: 0    Leader: 0       Replicas: 2,0   Isr: 0
        Topic: kafka    Partition: 1    Leader: 0       Replicas: 0,1   Isr: 0
Topic:kafka-action      PartitionCount:1        ReplicationFactor:3     Configs:
        Topic: kafka-action     Partition: 0    Leader: 0       Replicas: 1,2,0 Isr: 0
Topic:kafka-action-config-test  PartitionCount:1        ReplicationFactor:3     Configs:max.message.bytes=404800
        Topic: kafka-action-config-test Partition: 0    Leader: 0       Replicas: 2,1,0 Isr: 0
Topic:kafka-action1     PartitionCount:1        ReplicationFactor:3     Configs:max.message.bytes=404800
        Topic: kafka-action1    Partition: 0    Leader: 0       Replicas: 0,1,2 Isr: 0
Topic:kafkaTest PartitionCount:2        ReplicationFactor:2     Configs:
        Topic: kafkaTest        Partition: 0    Leader: 2       Replicas: 2,1   Isr: 1,2
        Topic: kafkaTest        Partition: 1    Leader: 0       Replicas: 0,2   Isr: 0
Topic:test      PartitionCount:1        ReplicationFactor:1     Configs:
        Topic: test     Partition: 0    Leader: 0       Replicas: 0     Isr: 0
Topic:test6     PartitionCount:2        ReplicationFactor:2     Configs:
        Topic: test6    Partition: 0    Leader: 0       Replicas: 2,0   Isr: 0
        Topic: test6    Partition: 1    Leader: 0       Replicas: 0,1   Isr: 0
		
**********************************************************************************************************************************

#查看正在同步的主题
#通过describe与under-replicated-partitions命令组合使用，可以查看处于"under replicated"状态的分区


kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183  --under-replicated-partitions

**********************************************************************************************************************
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183  --under-replicated-partitions
        Topic: __consumer_offsets       Partition: 0    Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 1    Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 2    Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 3    Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 4    Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 5    Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 6    Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 7    Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 8    Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 9    Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 10   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 11   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 12   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 13   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 14   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 15   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 16   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 17   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 18   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 19   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 20   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 21   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 22   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 23   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 24   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 25   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 26   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 27   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 28   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 29   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 30   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 31   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 32   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 33   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 34   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 35   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 36   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 37   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 38   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 39   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 40   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 41   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 42   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 43   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: __consumer_offsets       Partition: 44   Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: __consumer_offsets       Partition: 45   Leader: 0       Replicas: 1,0,2 Isr: 0
        Topic: __consumer_offsets       Partition: 46   Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: __consumer_offsets       Partition: 47   Leader: 0       Replicas: 0,2,1 Isr: 0
        Topic: __consumer_offsets       Partition: 48   Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: __consumer_offsets       Partition: 49   Leader: 0       Replicas: 2,0,1 Isr: 0
        Topic: config-test      Partition: 0    Leader: -1      Replicas: 0,1   Isr: 0  MarkedForDeletion: true
        Topic: config-test      Partition: 1    Leader: -1      Replicas: 1,2   Isr: 1  MarkedForDeletion: true
        Topic: config-test      Partition: 2    Leader: -1      Replicas: 2,0   Isr: 0  MarkedForDeletion: true
        Topic: kafka    Partition: 0    Leader: 0       Replicas: 2,0   Isr: 0
        Topic: kafka    Partition: 1    Leader: 0       Replicas: 0,1   Isr: 0
        Topic: kafka-action     Partition: 0    Leader: 0       Replicas: 1,2,0 Isr: 0
        Topic: kafka-action-config-test Partition: 0    Leader: 0       Replicas: 2,1,0 Isr: 0
        Topic: kafka-action1    Partition: 0    Leader: 0       Replicas: 0,1,2 Isr: 0
        Topic: kafkaTest        Partition: 1    Leader: 0       Replicas: 0,2   Isr: 0
        Topic: test6    Partition: 0    Leader: 0       Replicas: 2,0   Isr: 0
        Topic: test6    Partition: 1    Leader: 0       Replicas: 0,1   Isr: 0

*******************************************************************************************


#查看没有Leader的分区:通过describe与unavailable-partitions命令组合使用，可以查看没有Leader副本的主题。同样也可以指定topic参数，查看某个特定主题的哪些分区的Leader已不可用。

kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183  --unavailable-partitions

******************************************************************************************************************
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183  --unavailable-partitions
        Topic: config-test      Partition: 0    Leader: -1      Replicas: 0,1   Isr: 0  MarkedForDeletion: true
        Topic: config-test      Partition: 1    Leader: -1      Replicas: 1,2   Isr: 1  MarkedForDeletion: true
        Topic: config-test      Partition: 2    Leader: -1      Replicas: 2,0   Isr: 0  MarkedForDeletion: true
        Topic: kafkaTest        Partition: 0    Leader: 2       Replicas: 2,1   Isr: 1,2

*************************************************************************************************************************


#查看主题覆盖的配置:topics-with-overrides只显示describe命令执行的第一行信息。

kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topics-with-overrides

********************************************************************************************************************************
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topics-with-overrides
Topic:__consumer_offsets        PartitionCount:50       ReplicationFactor:3     Configs:segment.bytes=104857600,cleanup.policy=compact,compression.type=producer
Topic:config-test       PartitionCount:3        ReplicationFactor:2     Configs:max.message.bytes=404800        MarkedForDeletion:true
Topic:kafka-action-config-test  PartitionCount:1        ReplicationFactor:3     Configs:max.message.bytes=404800
Topic:kafka-action1     PartitionCount:1        ReplicationFactor:3     Configs:max.message.bytes=404800

********************************************************************************************************************************


#修改主题

****************修改主题级别配置**********************

1、查看config-test001的相关命令的具体用法：
kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topics-with-overrides --topic config-test001
2、修改max.message.bytes配置使起为204800
kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test001 max.message.bytes=204800
3、覆盖主题"config-test" 的segment.bytes大小为20MB(200*1024*1024)，执行命令如下：
kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --config segment.bytes=209715200
4、删除配置项segment.bytes的设置，使其恢复为默认值
kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --delete-config segment.bytes

****************增加分区*********************************
kafka并不支持减少分区的操作，我们只能为一个主题增加分区。

kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --partitions 5

D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --partitions 5
WARNING: If partitions are increased for a topic that has a key, the partition logic or ordering of the messages will be affected
Adding partitions succeeded!


#生产者基本操作
1、启动生产者
kafka-console-producer --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic kafka-action --property parse.key=true

默认是以制表符分割，若修改分隔符，则通过配置项key.separator指定。
kafka-console-producer --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic kafka-action --property parse.key=true --property key.separator=' '

#验证消息是否发送成功   time参数表示查看在指定时间之前的数据，支持-1(latest)、-2(earliest)两个时间选项，默认取值为-1
kafka-run-class kafka.tools.GetOffsetShell --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic kafka-action --time -1


2、创建主题
kafka-console-producer --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic producer-create-topic

3、查看消息
kafka-run-class kafka.tools.DumpLogSegments --files D:\kafka\kafka_2.11-2.2.1\tmp\kafka-logs\__consumer_offsets-49\00000000000000000000.log


