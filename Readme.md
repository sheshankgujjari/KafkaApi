
Compile the code using 

mvn compile assembly:single


##Simple Producer and Consumer Testing

1. Download the sample code
2. Compile the code and create a fat JAR with the command: 
   mvn clean compile assembly:single
3. Start the consumer: 
   java -cp target/KafkaAPI-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.Consumer test group1.
4. Start the producer: 
   java -cp target/KafkaAPI-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.simple.Producer test.
5. Enter a message in the producer console and check to see whether that message appears in the consumer. 
6. Type "exit" in the consumer and producer consoles to close them.



##Using partitioning

1. Compile and create a fat JAR by invoking: 
   mvn compile assembly:single.
2. Create a topic named part-demo with three partitions and one replication factor:
    Note: The KAFKA_HOME is the home directory "kafka_2.11-0.11.0.1"
    <KAFKA_HOME>bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 3 --topic part-demo
  
3. Start a producer:

   java -cp target/KafkaAPI-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.partition.Producer part-demo

4. Start three consumers, then watch the console to see how your partitions are assigned and revoked every time you start a new instance of the consumer:

   java -cp target/KafkaAPI-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.partition.Consumer part-demo group1

5. Type some messages into your producer console and verify whether the messages are routed to the correct consumer:

        


##Using offset

Rest of the instructions is same as partitioning the only change here is to send a third argument as "0"
The value of the last argument equal to 0, the consumer will assume that you want to start from the beginning,


If you pass a value of -1 it will assume that you want to ignore the existing messages and only consume messages published after the consumer has been restarted. 

Finally, if you specify any value other than 0 or -1 it will assume that you have specified the offset that you want the consumer to start from; for example, if you pass the third value as 5, then on restart the consumer will consume messages with an offset greater than 5.



java -cp target/KafkaAPI-1.0-SNAPSHOT-jar-with-dependencies.jar com.spnotes.kafka.offset.Consumer part-demo group1 0