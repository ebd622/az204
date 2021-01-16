(Under construction)
# Implement solutions that use Azure Event Hub

### Resources
* [Enable reliable messaging for Big Data applications using Azure Event Hubs](https://docs.microsoft.com/en-us/learn/modules/enable-reliable-messaging-for-big-data-apps-using-event-hubs/1-introduction)

### Key Conecpts
To deploy Azure Event Hubs, you must configure an **Event Hubs namespace**, and then configure the **Event Hub** itself.

#### Events
- An event is a small packet of information that contains a notification; 
- Events can be published individually, or in batches; 
- A single publication (individual or batch) can't exceed 1 MB.

#### Partitioning
- Each Event Hub is partitioned;
- You may have up to 32 patirions (minimum 1);
- You have to choose partitions when creating e-hub (no way to change it later on);
- When you send messages to e-hub there is no garantie that each partition will be utilized equaly. So, each partition may grow at a different rate:

<img src="../../images/event_hub_11.gif" width="550" height="275"/>

- All events in a partition are ordered ```older -> newer ``` (like in a queue);
- An order is NOT maintened across partitions;
- If you need to process multiple events in order you need to introduce a *Partition Key*:

<img src="../../images/event_hub_21.gif" width="550" height="275" />


#### Namespaces
- Event hub represents a unique stream of data;
- Event hub namespace is a collection of event hubs
  - Scoping a container;
  - Shared properties
  
<img src="../../images/ns_1.PNG" width="60%" and height="60%"/>

### Java-examplea to send/receive events from Azure Event Hubs

#### Send events

```Java
import com.azure.messaging.eventhubs.*;

public class Sender {
    public static void main(String[] args) {
        final String connectionString = "EVENT HUBS NAMESPACE CONNECTION STRING";
        final String eventHubName = "EVENT HUB NAME";

        // create a producer using the namespace connection string and event hub name
        EventHubProducerClient producer = new EventHubClientBuilder()
            .connectionString(connectionString, eventHubName)
            .buildProducerClient();

        // prepare a batch of events to send to the event hub    
        EventDataBatch batch = producer.createBatch();
        batch.tryAdd(new EventData("First event"));
        batch.tryAdd(new EventData("Second event"));
        batch.tryAdd(new EventData("Third event"));
        batch.tryAdd(new EventData("Fourth event"));
        batch.tryAdd(new EventData("Fifth event"));

        // send the batch of events to the event hub
        producer.send(batch);

        // close the producer
        producer.close();
    }
}

```


#### Receive events


