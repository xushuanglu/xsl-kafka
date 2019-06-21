#����kafka
.\bin\windows\kafka-server-start.bat .\config\server.properties

#����һ��toptic
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 1 --partitions 1 --topic kafka-action

#��������--replication-factor���������������⸱������3���ڵ��kafka��Ⱥ���ֻ��3������������������ʱ��������3�����׳������쳣��
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 4 --partitions 1 --topic kafka-action
Error while executing topic command : Replication factor: 4 larger than available brokers: 3.
[2019-06-20 19:14:51,773] ERROR org.apache.kafka.common.errors.InvalidReplicationFactorException: Replication factor: 4 larger than available brokers: 3.
 (kafka.admin.TopicCommand$)
 
#����topic�ɹ�
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 3 --partitions 1 --topic kafka-action
Created topic kafka-action.

#����һ��config-test���⣬���������max.message.bytes=404800�ֽڡ�
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics.bat --create --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --replication-factor 3 --partitions 1 --topic kafka-action-config-test --config max.message.bytes=404800
Created topic kafka-action-config-test.

�ڴ�������ʱ��ʹ����config��������ͨ��Zookeeperk�ͻ��˿�����/config/topics�ڵ��²鿴�������������ǵ�����


#����
reqpath:n/a Error Path:/config/topics/config-test Error:KeeperErrorCode = NoNode for /config/topics/config-test


#ɾ������
kafka-topics --delete --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test
#����
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --delete --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test
Topic config-test is marked for deletion.
Note: This will have no impact if delete.topic.enable is not set to true.

#�������
��kafka  D:\kafka\kafka_2.11-2.2.1\config\server.properties�����������
#����ɾ��
delete.topic.enable=true

D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --delete --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test
Topic config-test is already marked for deletion.


#�鿴����   list:�г�����kafka���е�������  or  describe���鿴���������ĳ���ض����������Ϣ

#�г�����kafka���е�������
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

#�鿴���������ĳ���ض����������Ϣ
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

#�鿴����ͬ��������
#ͨ��describe��under-replicated-partitions�������ʹ�ã����Բ鿴����"under replicated"״̬�ķ���


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


#�鿴û��Leader�ķ���:ͨ��describe��unavailable-partitions�������ʹ�ã����Բ鿴û��Leader���������⡣ͬ��Ҳ����ָ��topic�������鿴ĳ���ض��������Щ������Leader�Ѳ����á�

kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183  --unavailable-partitions

******************************************************************************************************************
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183  --unavailable-partitions
        Topic: config-test      Partition: 0    Leader: -1      Replicas: 0,1   Isr: 0  MarkedForDeletion: true
        Topic: config-test      Partition: 1    Leader: -1      Replicas: 1,2   Isr: 1  MarkedForDeletion: true
        Topic: config-test      Partition: 2    Leader: -1      Replicas: 2,0   Isr: 0  MarkedForDeletion: true
        Topic: kafkaTest        Partition: 0    Leader: 2       Replicas: 2,1   Isr: 1,2

*************************************************************************************************************************


#�鿴���⸲�ǵ�����:topics-with-overridesֻ��ʾdescribe����ִ�еĵ�һ����Ϣ��

kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topics-with-overrides

********************************************************************************************************************************
D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topics-with-overrides
Topic:__consumer_offsets        PartitionCount:50       ReplicationFactor:3     Configs:segment.bytes=104857600,cleanup.policy=compact,compression.type=producer
Topic:config-test       PartitionCount:3        ReplicationFactor:2     Configs:max.message.bytes=404800        MarkedForDeletion:true
Topic:kafka-action-config-test  PartitionCount:1        ReplicationFactor:3     Configs:max.message.bytes=404800
Topic:kafka-action1     PartitionCount:1        ReplicationFactor:3     Configs:max.message.bytes=404800

********************************************************************************************************************************


#�޸�����

****************�޸����⼶������**********************

1���鿴config-test001���������ľ����÷���
kafka-topics --describe --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topics-with-overrides --topic config-test001
2���޸�max.message.bytes����ʹ��Ϊ204800
kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test001 max.message.bytes=204800
3����������"config-test" ��segment.bytes��СΪ20MB(200*1024*1024)��ִ���������£�
kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --config segment.bytes=209715200
4��ɾ��������segment.bytes�����ã�ʹ��ָ�ΪĬ��ֵ
kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --delete-config segment.bytes

****************���ӷ���*********************************
kafka����֧�ּ��ٷ����Ĳ���������ֻ��Ϊһ���������ӷ�����

kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --partitions 5

D:\kafka\kafka_2.11-2.2.1\bin\windows>kafka-topics --alter --zookeeper 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic config-test --partitions 5
WARNING: If partitions are increased for a topic that has a key, the partition logic or ordering of the messages will be affected
Adding partitions succeeded!


#�����߻�������
1������������
kafka-console-producer --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic kafka-action --property parse.key=true

Ĭ�������Ʊ���ָ���޸ķָ�������ͨ��������key.separatorָ����
kafka-console-producer --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic kafka-action --property parse.key=true --property key.separator=' '

#��֤��Ϣ�Ƿ��ͳɹ�   time������ʾ�鿴��ָ��ʱ��֮ǰ�����ݣ�֧��-1(latest)��-2(earliest)����ʱ��ѡ�Ĭ��ȡֵΪ-1
kafka-run-class kafka.tools.GetOffsetShell --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic kafka-action --time -1


2����������
kafka-console-producer --broker-list 127.0.0.1:2181,127.0.0.1:2182,127.0.0.1:2183 --topic producer-create-topic

3���鿴��Ϣ
kafka-run-class kafka.tools.DumpLogSegments --files D:\kafka\kafka_2.11-2.2.1\tmp\kafka-logs\__consumer_offsets-49\00000000000000000000.log


